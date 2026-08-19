---
name: Upsert people safely
description: Create or update Marketo person records without duplicating them, using the right lookupField and action mode, and read the per-record results correctly.
api: openapi/marketo-lead-database-openapi-original.json
operations:
  - describeUsingGET_6
  - getLeadsByFilterUsingGET
  - syncLeadUsingPOST
  - getLeadByIdUsingGET
generated: '2026-08-13'
method: generated
---

# Upsert people safely

Marketo has **no `Idempotency-Key` header**. Replay safety comes entirely from
choosing the right `lookupField` and the right `action`. Get this wrong and a
retry creates duplicate people in a live marketing database.

## Steps

1. **Discover the field vocabulary first.** Call `describeUsingGET_6`
   (Describe Lead2). Marketo's `Lead` schema declares only `id`, `membership`,
   `reason` and `status`; every other field is defined per subscription. Never
   assume a field exists. Cache the result — it changes rarely, but it is
   different in every instance.

2. **Choose a `lookupField`.** Defaults to `email`. If you own a stable external
   identifier and it exists as a custom field on the Lead object, use that
   instead — it is the closest thing this API has to an idempotency key.
   The field must be present on **every** record in the input array.

3. **Choose an `action`.** `syncLeadUsingPOST` takes an enum:

   | action | Effect | Replay-safe? |
   |---|---|---|
   | `createOrUpdate` | Upsert. The default. | **Yes** |
   | `createOnly` | Fails with record error 1005 if the key already matches | Yes (fails loudly) |
   | `updateOnly` | Fails with record error 1004 if no match | Yes (fails loudly) |
   | `createDuplicate` | Always inserts | **No — never retry this** |

4. **De-duplicate your own batch.** Two input records sharing the same key in one
   request return error **1036** "Duplicate object found in input". Collapse them
   before sending.

5. **Set `partitionName` when partitions are enabled.** Adobe's own guidance is
   to set it "whenever possible". Omitting it in a partitioned instance risks
   error 1009 or 1010.

6. **Read the result per record, not per response.** `syncLeadUsingPOST` returns
   HTTP 200 with `success: true` even when individual records failed:

   ```json
   { "requestId": "e42b#14272d07d78", "success": true,
     "result": [ { "id": 50, "status": "created" },
                 { "status": "skipped", "reasons": [ { "code": "1005", "message": "Lead already exists" } ] } ] }
   ```

   Records appear in the same order as your input array. Walk every entry and
   check `status` and `reasons`.

7. **Verify by id when it matters.** `getLeadByIdUsingGET` reads back a single
   record; `getLeadsByFilterUsingGET` finds records by `filterType` +
   `filterValues`.

## Sizing

- Request body maximum **1 MB** (HTTP 413 above it). Import Lead allows 10 MB.
- A GET URI over **8 KB** returns HTTP 414. Re-issue as POST with `_method=GET`
  and the query string in the body — this is required for any real filter on
  GUID-valued fields.
- `getLeadsByFilterUsingGET` pages with `batchSize` (max and default 300) and
  `nextPageToken`; stop when `moreResult` is false.

## Errors that mean "do not retry"

| Code | Meaning |
|---|---|
| 1007 | Multiple leads match the lookup criteria — the key is not unique. Fix the key. |
| 1011 | Field not supported as a lookup/filter field. |
| 1008 / 1010 | Partition access denied / partition update not allowed. |
| 1018 | Blocked because a native CRM integration is enabled on this instance. |

## Permissions

`syncLeadUsingPOST` requires **Read-Write Lead**. Read-only flows need
**Read-Only Lead**. See `scopes/marketo-scopes.yml`.
