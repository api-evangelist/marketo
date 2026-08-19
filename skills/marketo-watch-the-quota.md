---
name: Stay inside the API budget
description: Monitor and respect Marketo's subscription-wide call quota, rate limit and concurrency ceiling — none of which are signalled in response headers.
api: openapi/marketo-lead-database-openapi-original.json
operations:
  - getDailyUsageUsingGET
  - getLast7DaysUsageUsingGET
  - getDailyErrorsUsingGET
  - getLast7DaysErrorsUsingGET
generated: '2026-08-13'
method: generated
---

# Stay inside the API budget

## The problem

Marketo returns **no rate-limit headers**. No `X-RateLimit-*`, no RFC 9331
`RateLimit-*`, no `Retry-After`. It also does not return HTTP 429. Exhaustion
arrives as a response-level code inside an **HTTP 200** body. An agent that
watches status codes will not notice it is being throttled at all.

## The budget

Every limit below is **per subscription**, not per credential. Every integration
in the instance draws on the same pool.

| Limit | Value | Signal |
|---|---|---|
| Rate | 100 calls / 20 seconds | body code **606** |
| Daily quota | 50,000 calls, resets 12:00 AM CST | body code **607** |
| Concurrency | 10 in-flight calls | body code **615** |
| Bulk export volume | 500 MB / day | body code **1029** |
| Bulk export queue | 10 jobs | body code **1029** |
| Bulk import queue | 10 imports | body code **1016** |

Calls that return a response-level error do **not** count against the quota or
the rate limit. That is the one piece of good news in this design: a throttled
call is free.

## Steps

1. **Parse every response body.** Before anything else:

   ```
   if body.success is false:
       code = body.errors[0].code
   ```

   Codes 606, 607 and 615 are backoff signals, not failures.

2. **Back off deliberately.**
   - **606** — you exceeded 100 calls in the trailing 20 seconds. Sleep at least
     20 seconds. Exponential backoff from there.
   - **615** — you have 10 requests in flight. Cap your own concurrency at 10
     across the whole process, and lower if you share the instance.
   - **607** — the day is over. Do not retry until after 12:00 AM CST. Retrying
     into a daily quota wall accomplishes nothing and hides the outage.

3. **Poll your usage.** `getDailyUsageUsingGET` returns today's consumption;
   `getLast7DaysUsageUsingGET` gives the trend. These are the **only**
   programmatic view of the budget. Call one at the start of a batch run and
   decide whether the work fits before you start it.

4. **Poll your errors.** `getDailyErrorsUsingGET` and
   `getLast7DaysErrorsUsingGET` show error counts by API-Only user — which is
   exactly why each integration should own a separate custom service. Shared
   credentials make attribution impossible.

5. **Reduce calls before asking for more quota.** In order of impact:
   - Replace `getLeadsByFilterUsingGET` loops with a bulk export job.
   - Page at the maximum `batchSize` (300) rather than the default page walk.
   - Filter activity feeds by `activityTypeIds` instead of pulling everything.
   - Cache the describe/field-vocabulary responses; they change rarely.
   - Batch writes — `syncLeadUsingPOST` takes an array, up to a 1 MB body.

6. **Ask for more only then.** Adobe's documented path is "contact your account
   manager". There is no published overage rate and no self-service upgrade;
   Admin > Web Services shows the instance's current quota.

## Permissions

The Usage and Error operations require no special Access API permission beyond a
valid API-Only credential.
