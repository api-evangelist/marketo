---
name: Authenticate against a Marketo instance
description: Obtain and refresh a Marketo Engage OAuth 2.0 access token, and address every call to the right per-subscription host.
api: openapi/marketo-identity-openapi-original.json
operations:
  - identityUsingGET
  - identityUsingPOST
generated: '2026-08-13'
method: generated
---

# Authenticate against a Marketo instance

## Before you start

You need three values, and none of them can be guessed:

| Value | Where it comes from |
|---|---|
| Base URL | Admin > Integration > Web Services, labelled "Endpoint:". Form: `https://{munchkinId}.mktorest.com/rest` |
| Identity URL | Same panel, "Identity" in the REST API section. Form: `https://{munchkinId}.mktorest.com/identity` |
| Client Id + Client Secret | Admin > Integration > LaunchPoint > select the Custom Service > View Details |

There is no shared production host. The Munchkin ID is unique to the
subscription, which is why Adobe's published specs carry `host: localhost:8080`.
Treat the host as required configuration and refuse to run without it.

## Steps

1. **Get a token.** Call `identityUsingGET` (or `identityUsingPOST`) at
   `{identityUrl}/oauth/token` with `grant_type=client_credentials`, `client_id`
   and `client_secret`.

   The response is:

   ```json
   { "access_token": "…", "token_type": "bearer", "expires_in": 3599, "scope": "apis@example.com" }
   ```

   `scope` is the API-Only user's **email address**, not a permission grant.
   Do not parse it as an OAuth scope.

2. **Cache it for 3,600 seconds.** A new token lives one hour. Tokens are
   per-custom-service; one service's expiry says nothing about another's.
   Re-requesting a token on every call wastes quota.

3. **Send it in the header, always.**

   ```
   Authorization: Bearer <access_token>
   ```

   Do **not** use the `access_token` query or form parameter. Adobe removes
   support for it on **2026-08-31**. Any code path that still builds a URL with
   `?access_token=` is a scheduled outage.

4. **Refresh on 602, not on a clock alone.** Marketo signals an expired token as
   a response-level error inside an **HTTP 200** body:

   ```json
   { "success": false, "errors": [ { "code": "602", "message": "Access token expired" } ] }
   ```

   Re-authenticate and replay the request once.

## Error handling

| Code | Where | Meaning | Action |
|---|---|---|---|
| 401 | Identity endpoint (real HTTP status) | Client Id or Client Secret invalid | Stop. Do not retry — fix the credential. |
| 601 | Response body, HTTP 200 | Access token invalid | Re-authenticate once, then stop. |
| 602 | Response body, HTTP 200 | Access token expired | Re-authenticate and replay. |
| 603 | Response body, HTTP 200 | Authenticated but not permitted, or blocked by IP allowlist | Stop. Needs an "Access API" role permission or an allowlist entry — not a retry. |

## Rules

- Never treat HTTP 200 as success. Read `success` in the body first.
- Never log the Client Secret or the access token.
- One Custom Service per integration. Usage and errors are tracked per API-Only
  user, so sharing a credential destroys your ability to attribute a quota burn.
- The credential's authority comes from the API-Only user's role permissions —
  see `scopes/marketo-scopes.yml`. Request the minimum set.
