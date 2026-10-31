# Marketo

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Marketo, an Adobe company, develops and sells B2B marketing automation software for account-based marketing, lead management, email marketing and campaign execution. Adobe Marketo Engage publishes five machine-readable specifications covering 367 REST operations across five surfaces — a Lead Database API for person records, activity and change feeds, companies, opportunities, custom objects, static lists, smart campaigns and bulk import/export; an Asset API for emails, landing pages, forms, templates, snippets and segments; a User Management API for users, roles and workspaces; an Identity endpoint issuing two-legged OAuth 2.0 client-credentials tokens; and an asynchronous Data Ingestion API on a separate Adobe-hosted domain. The base URL is per-subscription (https://{munchkinId}.mktorest.com), authorization is role-permission rather than OAuth-scope based, and most failures — including rate-limit and quota exhaustion — are returned inside an HTTP 200 body.

**Areas:** Adobe · Automation · Marketing · Marketing Automation · Email Marketing · Lead Management · Campaign Management · CRM · Customer Engagement · B2B · Marketo

## Marketo on APIs.io

Everything profiled for Marketo is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/marketo/](https://apis.io/providers/marketo/)** — or go straight to one of the APIs or properties below.

### APIs (45)

- [Marketo Campaigns API](https://apis.io/apis/marketo/marketo-campaigns-api/) — The Campaigns API from Marketo — 7 operation(s) for campaigns.
- [Marketo Channels API](https://apis.io/apis/marketo/marketo-channels-api/) — Channel Controller
- [Marketo Email  Templates API](https://apis.io/apis/marketo/marketo-email-templates-api/) — The Email Templates API from Marketo — 10 operation(s) for email templates.
- [Marketo Emails API](https://apis.io/apis/marketo/marketo-emails-api/) — Email Controller
- [Marketo File  Contents API](https://apis.io/apis/marketo/marketo-file-contents-api/) — The File Contents API from Marketo — 1 operation(s) for file contents.
- [Marketo Files API](https://apis.io/apis/marketo/marketo-files-api/) — File Controller
- [Marketo Folders API](https://apis.io/apis/marketo/marketo-folders-api/) — Folder Controller
- [Marketo Form  Fields API](https://apis.io/apis/marketo/marketo-form-fields-api/) — The Form Fields API from Marketo — 9 operation(s) for form fields.
- [Marketo Forms API](https://apis.io/apis/marketo/marketo-forms-api/) — Form Controller
- [Marketo Landing  Page  Content API](https://apis.io/apis/marketo/marketo-landing-page-content-api/) — The Landing Page Content API from Marketo — 4 operation(s) for landing page content.
- [Marketo Landing  Page  Redirect  Rules API](https://apis.io/apis/marketo/marketo-landing-page-redirect-rules-api/) — The Landing Page Redirect Rules API from Marketo — 4 operation(s) for landing page redirect rules.
- [Marketo Landing  Page  Templates API](https://apis.io/apis/marketo/marketo-landing-page-templates-api/) — The Landing Page Templates API from Marketo — 9 operation(s) for landing page templates.
- [Marketo Landing  Pages API](https://apis.io/apis/marketo/marketo-landing-pages-api/) — The Landing Pages API from Marketo — 11 operation(s) for landing pages.
- [Marketo Programs API](https://apis.io/apis/marketo/marketo-programs-api/) — Program Controller
- [Marketo Segments API](https://apis.io/apis/marketo/marketo-segments-api/) — Segment Controller
- [Marketo Smart  Campaigns API](https://apis.io/apis/marketo/marketo-smart-campaigns-api/) — The Smart Campaigns API from Marketo — 8 operation(s) for smart campaigns.
- [Marketo Smart  Lists API](https://apis.io/apis/marketo/marketo-smart-lists-api/) — The Smart Lists API from Marketo — 4 operation(s) for smart lists.
- [Marketo Snippets API](https://apis.io/apis/marketo/marketo-snippets-api/) — Snippet Controller
- [Marketo Static  Lists API](https://apis.io/apis/marketo/marketo-static-lists-api/) — The Static Lists API from Marketo — 3 operation(s) for static lists.
- [Marketo Tokens API](https://apis.io/apis/marketo/marketo-tokens-api/) — Token Controller
- [Marketo Activities API](https://apis.io/apis/marketo/marketo-activities-api/) — Activities Controller
- [Marketo Bulk Export Activities API](https://apis.io/apis/marketo/marketo-bulk-export-activities-api/) — Bulk Export Activities Controller
- [Marketo Bulk Export Custom Objects API](https://apis.io/apis/marketo/marketo-bulk-export-custom-objects-api/) — Bulk Export Custom Objects Controller
- [Marketo Bulk Export Leads API](https://apis.io/apis/marketo/marketo-bulk-export-leads-api/) — Bulk Export Leads Controller
- [Marketo Bulk Export Program Members API](https://apis.io/apis/marketo/marketo-bulk-export-program-members-api/) — Bulk Export Program Members Controller
- [Marketo Bulk Import Custom Objects API](https://apis.io/apis/marketo/marketo-bulk-import-custom-objects-api/) — Bulk Import Custom Objects Controller
- [Marketo Bulk Import Leads API](https://apis.io/apis/marketo/marketo-bulk-import-leads-api/) — Bulk Import Leads Controller
- [Marketo Bulk Import Program Members API](https://apis.io/apis/marketo/marketo-bulk-import-program-members-api/) — Bulk Import Program Members Controller
- [Marketo Companies API](https://apis.io/apis/marketo/marketo-companies-api/) — Sync company records (createOnly, updateOnly, or createOrUpdate)
- [Marketo Custom Objects API](https://apis.io/apis/marketo/marketo-custom-objects-api/) — Upsert (insert or update) custom object records
- [Marketo Email Templates (New) API](https://apis.io/apis/marketo/marketo-email-templates-new-api/) — API endpoints for managing email templates created with the new Email Designer in Marketo Engage.
- [Marketo Emails (New) API](https://apis.io/apis/marketo/marketo-emails-new-api/) — API endpoints for managing emails created with the new Email Designer in Marketo Engage.
- [Marketo Fragments (New) API](https://apis.io/apis/marketo/marketo-fragments-new-api/) — API endpoints for managing fragments created with the new Email Designer in Marketo Engage.
- [Marketo Identity API](https://apis.io/apis/marketo/marketo-identity-api/) — Identity Controller
- [Marketo Leads API](https://apis.io/apis/marketo/marketo-leads-api/) — Leads Controller
- [Marketo Lists API](https://apis.io/apis/marketo/marketo-lists-api/) — Add leads to or remove leads from static lists
- [Marketo Named Account Lists API](https://apis.io/apis/marketo/marketo-named-account-lists-api/) — Named Account Lists Controller
- [Marketo Named Accounts API](https://apis.io/apis/marketo/marketo-named-accounts-api/) — Named Accounts Controller
- [Marketo Opportunities API](https://apis.io/apis/marketo/marketo-opportunities-api/) — Opportunities Controller
- [Marketo Persons API](https://apis.io/apis/marketo/marketo-persons-api/) — Upsert (insert or update) person/lead records
- [Marketo Program Members API](https://apis.io/apis/marketo/marketo-program-members-api/) — Sync program member status or delete (remove) members from programs
- [Marketo Tags API](https://apis.io/apis/marketo/marketo-tags-api/) — Tag Controller
- [Marketo Usage API](https://apis.io/apis/marketo/marketo-usage-api/) — Stats Controller
- [Marketo User Management API](https://apis.io/apis/marketo/marketo-user-management-api/) — Marketo Engage provides a set of User Management endpoints allow you to perform CRUD operations on user records in Marketo.
- [Marketo Salespersons API](https://apis.io/apis/marketo/marketo-salespersons-api/) — Sales Persons Controller

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Marketo Engage Events](https://apis.io/asyncapis/marketo/marketo-events-asyncapi/)

#### Event channels (4)

Individual events and webhooks the provider emits.

- [marketo/activities/deletedLeads](https://apis.io/channels/marketo/marketo-activities-deletedleads/)
- [marketo/activities/leadActivities](https://apis.io/channels/marketo/marketo-activities-leadactivities/)
- [marketo/activities/leadChanges](https://apis.io/channels/marketo/marketo-activities-leadchanges/)
- [marketo/webhook/outbound](https://apis.io/channels/marketo/marketo-webhook-outbound/)

#### GraphQL (1)

GraphQL schemas.

- [Moved to /providers/marketo/](https://apis.io/graphqls/marketo/marketo-graphql/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [marketo](https://apis.io/servers/marketo/marketo/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Marketo Agentic Access](https://apis.io/agentic-access/marketo/marketo-agentic-access/)

#### Collections (65)

Postman and Open Collection request collections.

- [Marketo Engage Rest Approve API](https://apis.io/collections/marketo/open-marketo-approve-api/)
- [Marketo Engage Rest Approve Assets API](https://apis.io/collections/marketo/open-marketo-assets-api/)
- [Marketo Engage Rest Approve Campaigns API](https://apis.io/collections/marketo/open-marketo-campaigns-api/)
- [Marketo Engage Rest Approve Cc API](https://apis.io/collections/marketo/open-marketo-cc-api/)
- [Marketo Engage Rest Approve Channel API](https://apis.io/collections/marketo/open-marketo-channel-api/)
- [Marketo Engage Rest Approve Channels API](https://apis.io/collections/marketo/open-marketo-channels-api/)
- [Marketo Engage Rest Approve Clone.json API](https://apis.io/collections/marketo/open-marketo-clone-json-api/)
- [Marketo Engage Rest Approve Content API](https://apis.io/collections/marketo/open-marketo-content-api/)
- [Marketo Engage Rest Approve Content.json API](https://apis.io/collections/marketo/open-marketo-content-json-api/)
- [Marketo Engage Rest Approve Delete.json API](https://apis.io/collections/marketo/open-marketo-delete-json-api/)
- [Marketo Engage Rest Approve Discard API](https://apis.io/collections/marketo/open-marketo-discard-api/)
- [Marketo Engage Rest Approve Dynamic API](https://apis.io/collections/marketo/open-marketo-dynamic-api/)
- [Marketo Engage Rest Approve Email API](https://apis.io/collections/marketo/open-marketo-email-api/)
- [Marketo Engage Rest Approve Email  Templates API](https://apis.io/collections/marketo/open-marketo-email-templates-api/)
- [Marketo Engage Rest Approve Emails API](https://apis.io/collections/marketo/open-marketo-emails-api/)
- [Marketo Engage Rest API](https://apis.io/collections/marketo/open-marketo-engage-rest-api/)
- [Marketo Engage Rest Approve Field API](https://apis.io/collections/marketo/open-marketo-field-api/)
- [Marketo Engage Rest Approve Fields API](https://apis.io/collections/marketo/open-marketo-fields-api/)
- [Marketo Engage Rest Approve File API](https://apis.io/collections/marketo/open-marketo-file-api/)
- [Marketo Engage Rest Approve File  Contents API](https://apis.io/collections/marketo/open-marketo-file-contents-api/)
- [Marketo Engage Rest Approve Files API](https://apis.io/collections/marketo/open-marketo-files-api/)
- [Marketo Engage Rest Approve Folder API](https://apis.io/collections/marketo/open-marketo-folder-api/)
- [Marketo Engage Rest Approve Folders API](https://apis.io/collections/marketo/open-marketo-folders-api/)
- [Marketo Engage Rest Approve Form API](https://apis.io/collections/marketo/open-marketo-form-api/)
- [Marketo Engage Rest Approve Form  Fields API](https://apis.io/collections/marketo/open-marketo-form-fields-api/)
- …and 40 more published on APIs.io

#### Overlays (5)

OpenAPI overlays, including conversational phrasing for each operation.

- [Marketo Asset Overlay](https://apis.io/overlays/marketo/marketo-asset-overlay/)
- [Marketo Data Ingestion Overlay](https://apis.io/overlays/marketo/marketo-data-ingestion-overlay/)
- [Marketo Identity Overlay](https://apis.io/overlays/marketo/marketo-identity-overlay/)
- [Marketo Lead Database Overlay](https://apis.io/overlays/marketo/marketo-lead-database-overlay/)
- [Marketo User Management Overlay](https://apis.io/overlays/marketo/marketo-user-management-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Marketo — asyncapi rules](https://apis.io/rules/marketo/marketo-asyncapi-spectral-rules/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Marketo Authentication](https://apis.io/security/marketo/marketo-authentication/)
- [Marketo Domain Security](https://apis.io/security/marketo/marketo-domain-security/)
- [Marketo Vulnerability Disclosure](https://apis.io/security/marketo/marketo-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Marketo Scopes](https://apis.io/scopes/marketo/marketo-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Marketo Plans Pricing](https://apis.io/plans/marketo/marketo-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Marketo Rate Limits](https://apis.io/rate-limits/marketo/marketo-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Marketo Finops](https://apis.io/finops/marketo/marketo-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.adobe.com/)
- [Documentation](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/rest-api)
- [Getting started](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/getting-started)
- [API reference](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/endpoint-reference)
- [Support](https://experienceleaguecommunities.adobe.com/)
- [Terms of service](https://www.adobe.com/legal.html)
- [Privacy policy](https://www.adobe.com/privacy/policy.html)
- [GitHub](https://github.com/Marketo)
- [Status](https://status.adobe.com/)

## API Evangelist rating

**Kin Score 56.4** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.4 |
| Contract quality | 48.8 |
| Contract governance | 18.2 |
| Operational transparency | 84.2 |
| Developer ergonomics | 63.7 |
| Access clarity | 21.1 |

**Agent readiness 31.1** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | derived (partial credit) |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly (partial credit) |

**Regulatory alignment 40.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/marketo/](https://apis.io/providers/marketo/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Marketo: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/marketo/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
