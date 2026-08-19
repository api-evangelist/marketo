---
name: Add people to a list and trigger a campaign
description: Move people into a static list and run a Marketo smart campaign against them — the highest-consequence write on this API.
api: openapi/marketo-lead-database-openapi-original.json
operations:
  - getListsUsingGET
  - addLeadsToListUsingPOST
  - getCampaignsUsingGET
  - triggerCampaignUsingPOST
  - scheduleCampaignUsingPOST
  - getSmartCampaignMembershipUsingGET
generated: '2026-08-13'
method: generated
---

# Add people to a list and trigger a campaign

## Read this before you call anything

`triggerCampaignUsingPOST` **executes real marketing flow steps against real
people** — it sends emails, changes scores, writes to a CRM, calls webhooks.
Marketo has no sandbox and no test mode (`sandbox/marketo-sandbox.yml`), so
there is no environment in which an agent can rehearse this. Treat it as
human-in-the-loop.

## Steps

1. **Find the list.** `getListsUsingGET` (filterable by name or program) or
   `getListByIdUsingGET`.

2. **Add the people.** `addLeadsToListUsingPOST` with the list id and an array of
   lead ids. Use `removeLeadsFromListUsingDELETE` to reverse it and
   `areLeadsMemberOfListUsingGET` to check membership first.

3. **Find the campaign.** `getCampaignsUsingGET`, or `getCampaignByIdUsingGET`.
   Read the `type` field:
   - **trigger** campaign → use `triggerCampaignUsingPOST`
   - **batch** campaign → use `scheduleCampaignUsingPOST`

   Calling Request Campaign against a batch campaign returns error **1003**.
   Only trigger campaigns can be requested, and only a campaign whose smart list
   contains a **Campaign is Requested** trigger will respond.

4. **Run it.**
   - `triggerCampaignUsingPOST` — pass up to the documented maximum of lead ids
     plus optional `tokens` to override My Token values for this run.
   - `scheduleCampaignUsingPOST` — pass `runAt`. More than **two years** in the
     future returns error **1042**. `cloneToProgramName` is capped per day
     (error **1020**).

5. **Confirm.** `getSmartCampaignMembershipUsingGET` shows which smart campaigns
   a given lead is in.

## Errors to expect

| Code | Meaning |
|---|---|
| 1003 | Invalid data — commonly Request Campaign against a batch campaign |
| 1013 | Campaign or list not found |
| 1015 | Lead is not a member of the target list |
| 1042 | `runAt` more than two years out |
| 1020 | Daily `cloneToProgramName` allowance exhausted |
| 603 | Missing the **Execute Campaign** permission |

Remember: all of these arrive with **HTTP 200**. Check `success` in the body.

## Rules

- Require explicit human confirmation before `triggerCampaignUsingPOST`. Name the
  campaign, the list, and the record count in the confirmation.
- `addLeadsToListUsingPOST` is idempotent in effect — re-adding an existing
  member is a no-op. `triggerCampaignUsingPOST` is **not**; a retry runs the flow
  steps again.
- Trigger campaigns are the surface that fires outbound webhooks (see
  `asyncapi/marketo-events-asyncapi.yml`), so a retry can also double-fire a
  third-party system.

## Permissions

**Execute Campaign** to run a campaign; **Read-Only Campaign** to list them;
**Read-Write Lead** for list membership changes.
