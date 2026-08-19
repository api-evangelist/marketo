---
name: Run a bulk lead export job
description: Export large person datasets out of Marketo using the four-stage bulk job lifecycle, inside the queue and daily-volume limits.
api: openapi/marketo-lead-database-openapi-original.json
operations:
  - createExportLeadsUsingPOST
  - enqueueExportLeadsUsingPOST
  - getExportLeadsStatusUsingGET
  - getExportLeadsFileUsingGET
  - cancelExportLeadsUsingPOST
  - getExportLeadsUsingGET
generated: '2026-08-13'
method: generated
---

# Run a bulk lead export job

Bulk export is a **job**, not a request. Anything above a few thousand records
belongs here rather than in `getLeadsByFilterUsingGET`, which will exhaust the
daily quota long before it finishes.

## Steps

1. **Create the job.** `createExportLeadsUsingPOST` with the fields you want, a
   filter (a date range, a static list, or a smart list) and a format
   (`CSV`, `TSV` or `SSV`). Returns an `exportId` in state **Created**.

2. **Enqueue it.** `enqueueExportLeadsUsingPOST` with that `exportId`. A created
   job does not run until it is enqueued — this second call is the step people
   forget. State moves to **Queued**.

3. **Poll status.** `getExportLeadsStatusUsingGET`. States are
   `Created`, `Queued`, `Processing`, `Cancelled`, `Completed`, `Failed`.
   Poll on a sane interval; each poll costs a call against the same 50,000/day
   quota the export was meant to protect.

4. **Download.** On `Completed`, call `getExportLeadsFileUsingGET`. The response
   is the file body, not JSON.

5. **Cancel if you must.** `cancelExportLeadsUsingPOST` releases a queue slot.
   `getExportLeadsUsingGET` lists jobs created in the past 7 days and accepts a
   `status` filter and a `batchSize` (max and default 300).

## Limits that will stop you

| Limit | Value | Signal |
|---|---|---|
| Concurrent queued jobs | 10 per subscription | error **1029** |
| Daily export volume | 500 MB, resets 12:00 AM CST | error **1029** |
| Unsupported filter types | `updatedAt`, `smartListId`, `smartListName` are unavailable in some subscriptions | error **1035** |
| Job already queued | Enqueueing twice | error **1029** |

Error **1029** is overloaded across all three of those causes — read the message
string, not just the code.

## Rules

- Never poll faster than the job can plausibly progress. There is no
  `Retry-After` and no webhook to tell you it finished.
- Job listings only cover the **past 7 days**. Persist your own `exportId`s.
- Export jobs and their file downloads still count against the daily API quota.
- The same four-stage lifecycle applies to bulk export of activities, custom
  objects and program members, and to the bulk **import** operations — the
  operationIds differ but the state machine does not.

## Permissions

**Read-Only Lead** for the export content, plus **Read-Only Activity** for
activity exports.
