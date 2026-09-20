---
name: Grade a site and read the result
description: Submit a public URL to Agent Disco, poll until the scan completes, read the grade and per-check findings, and diff it against the previous scan of the same host.
api: openapi/agentdisco-io-openapi.yml
base_url: https://agentdisco.io
operations: [post_api_scan_create, get_api_scan_show, get_api_scan_diff, get_api_checks_index]
generated: '2026-09-19'
method: generated
---

# Grade a site and read the result

Agent Disco grades a host for AI-agent discoverability. A scan is asynchronous: you get a
scan id back immediately and poll for the result (typically under a minute). No credential
is needed for up to 10 scans per day per IP; see the monitor skill to raise that.

## Steps

1. **Submit the scan** - `POST /api/v1/scans` (`post_api_scan_create`) with body
   `{"url": "https://example.com"}`. Expect **202** and a `ScanAcceptedResponse`:
   `{id, status, statusUrl, resultUrl, grade: null, score: null}`. A **400** means the URL
   failed validation; a **429** means the daily quota is spent (`{"error", "message"}`).
2. **Poll** - `GET /api/v1/scans/{id}` (`get_api_scan_show`) every ~5 seconds until
   `status` is `completed` or `failed` (the enum is `queued|running|completed|failed|cancelled`).
   A completed `ScanDetailResponse` carries `grade` (A-F), `score` (0-100), `summary` and
   `findings[]`, each finding with `checkKey`, `status` (`pass|fail|warn|skip|error`),
   `pointsEarned`, `pointsPossible` (null when skipped/errored), `notes` and `evidence`.
3. **Explain a finding** - `GET /api/v1/checks` (`get_api_checks_index`) returns the
   catalogue keyed by `checkKey` with `label`, `category`, `weight` and a Markdown
   `description` that names the standard being measured. It is ETag'd; send
   `If-None-Match` and accept **304** on revisits.
4. **See what changed** - `GET /api/v1/scans/{id}/diff` (`get_api_scan_diff`) returns
   `gradeFrom/gradeTo`, `scoreFrom/scoreTo`, `scoreDelta`, `newFailures[]` and
   `newPasses[]` against the previous completed scan of the host; `previousScanId` is
   null on a first scan.

## Rules

- **Not idempotent.** Every `POST /api/v1/scans` queues a new scan and spends quota; do not
  retry a timed-out submit blindly - check `GET /api/v1/websites/{host}` first
  (conventions/agentdisco-io-conventions.yml).
- **No cancel.** There is no operation to cancel a queued scan.
- **Quota signal is the 429 status only** - no `Retry-After` or `RateLimit-*` headers
  (rate-limits/agentdisco-io-rate-limits.yml).
- **Errors are `{error, message}` JSON**, not RFC 9457 (errors/agentdisco-io-problem-types.yml).
- Only scan hosts you operate or that permit benign third-party probing (terms, section 2).
