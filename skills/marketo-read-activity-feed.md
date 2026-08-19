---
name: Read the activity and change feeds
description: Consume Marketo's activity, data-value-change and deleted-lead streams with a paging token, without losing or replaying events.
api: openapi/marketo-lead-database-openapi-original.json
operations:
  - getActivitiesPagingTokenUsingGET
  - getAllActivityTypesUsingGET
  - getLeadActivitiesUsingGET
  - getLeadChangesUsingGET
  - getDeletedLeadsUsingGET
generated: '2026-08-13'
method: generated
---

# Read the activity and change feeds

Marketo has no event push. These three polling feeds are the entire change-data-
capture surface, and all of them share one cursor mechanism.

## Steps

1. **Learn the activity type vocabulary.** Call `getAllActivityTypesUsingGET`
   once and cache it. Activity types are per-subscription and extensible;
   `activityTypeId` is meaningless without this map.

2. **Seed the cursor.** Call `getActivitiesPagingTokenUsingGET` with a required
   `sinceDatetime`. **The token cannot be constructed client-side** — this call
   is mandatory, and it is the single most common thing integrators get wrong.

3. **Poll the feed.** Pass the token to:
   - `getLeadActivitiesUsingGET` — activity records
   - `getLeadChangesUsingGET` — data value changes
   - `getDeletedLeadsUsingGET` — deletions

   Each response returns `nextPageToken` and `moreResult`.

4. **Page until drained, then persist.** Keep calling with the returned
   `nextPageToken` while `moreResult` is true. When `moreResult` is false, store
   `nextPageToken` — it is your durable resume point for the next poll cycle.
   Do **not** re-seed from `sinceDatetime` on the next run; that replays events.

5. **Filter narrowly.** Both feeds accept `activityTypeIds`. Requesting every
   type on a busy instance burns the daily quota fast.

## Hard constraint you must handle before 2026-09-30

From **2026-09-30**, calling `getLeadActivitiesUsingGET` or
`getLeadChangesUsingGET` with a `listId` whose static list contains **10,000 or
more leads** fails with record error **1003**. If your integration scopes the
feed by a large static list, it stops working on that date. Split the list, or
drop the `listId` and filter downstream.

## Budget

Feeds are the biggest quota consumer in most Marketo integrations. The instance
gets 50,000 calls/day and 100 calls per 20 seconds — shared across every
integration in the subscription.

- There are **no rate-limit headers**. Exhaustion is body code **606** (rate) or
  **607** (daily quota) with **HTTP 200**.
- Calls that return a response-level error do not count against the quota.
- Poll `getDailyUsageUsingGET` to see where you stand. See
  `skills/marketo-watch-the-quota.md`.

## Pagination reference

| Field | Meaning |
|---|---|
| `nextPageToken` | Opaque cursor. Returned when the result set exceeds `batchSize`. |
| `moreResult` | Boolean. Stop when false. |
| `batchSize` | Max and default 300. |

## Permissions

**Read-Only Activity** (and **Read-Only Activity Metadata** for
`getAllActivityTypesUsingGET`). `getActivitiesPagingTokenUsingGET` accepts either
Read-Only or Read-Write Activity.
