---
name: Monitor a host's grade over time with a key and a webhook
description: Mint an API key to raise the scan quota, read a host's latest grade and history, queue rescans, register a signed scan.completed webhook, and embed the grade badge.
api: openapi/agentdisco-io-openapi.yml
base_url: https://agentdisco.io
operations: [post_api_key_create, get_api_website_show, get_api_website_scans, post_api_website_rescan, post_api_webhook_create, get_api_webhook_list, delete_api_webhook_delete, get_api_website_badge]
generated: '2026-09-19'
method: generated
---

# Monitor a host's grade over time

## Steps

1. **Mint a key** - `POST /api/v1/keys` (`post_api_key_create`), no auth, optional
   `{"label": "..."}`. Expect **201** `CreateApiKeyResponse`; the plaintext `token`
   (`ak_...`) is shown **once** - store it. Mints are capped at 5/hour per IP (**429**).
   Send it as `Authorization: Bearer ak_...` from now on: the scan quota moves from
   10/day per IP to 100/day per key.
2. **Read the latest grade** - `GET /api/v1/websites/{host}` (`get_api_website_show`)
   returns `{host, latestGrade, latestScore, lastScannedAt, scanCount}`; **404** means the
   host has never been scanned - submit one first (see the grade skill).
3. **Read the history** - `GET /api/v1/websites/{host}/scans?page=1&perPage=50`
   (`get_api_website_scans`), most-recent first, `perPage` capped at 50, with
   `totalCount`. Each entry links to the full findings via `statusUrl`.
4. **Queue a rescan** - `POST /api/v1/websites/{host}/rescan` (`post_api_website_rescan`)
   returns **202** with the new scan to poll; it spends the same quota as a new scan.
5. **Get told instead of polling** - `POST /api/v1/webhooks` (`post_api_webhook_create`)
   with `{"host": "example.com", "url": "https://you.example/hook"}`. This needs an
   **account-bound** key (a key from step 1 is anonymous-tier and gets **401** - sign in
   on the website or use the Colony agent skill). The response carries the HMAC `secret`
   **once**. The host must already have been scanned (**404** otherwise); receivers must
   be https (**400**); 5 registrations/hour per account (**429**).
6. **Verify each delivery** - every `scan.completed` POST carries
   `X-Agent-Disco-Signature: sha256=<hex>`; recompute `HMAC-SHA256(secret, raw_body)` and
   compare in constant time. Reject payloads whose `scan.completedAt` (or the UUIDv7
   `scan.id` timestamp) is older than ~5 minutes. Respond 2xx within 10 seconds; after 5
   consecutive failures the webhook auto-pauses (asyncapi/agentdisco-io-webhooks.yml).
7. **Check delivery health / clean up** - `GET /api/v1/webhooks` (`get_api_webhook_list`)
   shows `consecutiveFailures`, `lastSucceededAt`, `lastFailedAt`; `DELETE /api/v1/webhooks/{id}`
   (`delete_api_webhook_delete`) removes one. Delete + re-create is how you resume a paused hook.
8. **Embed the badge** - `GET /api/v1/websites/{host}/badge.svg` (`get_api_website_badge`)
   by URL; add `?strict=1` if a stale (>30 day) badge should return **410** rather than grey.

## Rules

- Keys and webhooks belong to the account behind the bearer key; another account's ids
  return **404**, never 403.
- No idempotency keys anywhere; every POST creates (conventions/agentdisco-io-conventions.yml).
- Revoking a key (`DELETE /api/v1/keys/{id}`) is immediate and is the only reversal path
  for a mint.
