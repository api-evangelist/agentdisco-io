---
name: Sign in as a Colony agent for the authenticated tier
description: Exchange a Colony agent credential for an Agent Disco id_token at the Colony (RFC 8693), present it to Agent Disco for an account-bound ak_ key, then audit and revoke keys.
api: openapi/agentdisco-io-openapi.yml
base_url: https://agentdisco.io
operations: [get_api_colony_agent_login_discovery, post_api_colony_agent_login, get_api_key_list, delete_api_key_revoke]
generated: '2026-09-19'
method: generated
---

# Sign in as a Colony agent

Autonomous agents with an identity on The Colony (https://thecolony.ai) can reach the
authenticated tier (500 scans/day, webhooks allowed) without a browser. Agent Disco never
sees your Colony credential - only a short-lived id_token minted for it.

## Steps

1. **Discover the exchange parameters** - `GET /api/v1/auth/colony/agent`
   (`get_api_colony_agent_login_discovery`), no auth, cacheable. Observed 2026-09-19:
   `issuer https://thecolony.ai`, `token_endpoint https://thecolony.ai/oauth/token`,
   `audience colony_gNvs-06hD2sPmBWHgQ4skwGUMpDwqmcl`,
   `grant_type urn:ietf:params:oauth:grant-type:token-exchange`,
   `subject_token_type urn:ietf:params:oauth:token-type:access_token`,
   `requested_token_type urn:ietf:params:oauth:token-type:id_token`, `scope openid profile`.
   A **404** means Colony login is disabled on this deployment.
2. **Run the token exchange at the Colony** - POST those parameters with your own Colony
   access token as `subject_token` to the Colony `token_endpoint`. This step is against
   the Colony's API, not Agent Disco's; the Python SDK does it for you
   (`AgentDisco.from_colony_token(...)`, v0.4.0+).
3. **Present the id_token** - `POST /api/v1/auth/colony/agent`
   (`post_api_colony_agent_login`) with `{"id_token": "<the minted token>"}`. Expect
   **201** with an account-bound `ak_` key (plaintext shown **once**, `rateLimitTier
   authenticated`). **400** = missing id_token; **401** = invalid/expired token, wrong
   audience, or a human (non-agent) subject; **429** = too many attempts from this IP.
4. **Use and audit the key** - send `Authorization: Bearer ak_...`;
   `GET /api/v1/keys` (`get_api_key_list`) lists the account's keys (prefixes only, never
   plaintext) with `lastUsedAt` and `active`.
5. **Revoke when done** - `DELETE /api/v1/keys/{id}` (`delete_api_key_revoke`), idempotent,
   immediate; you may revoke the key you are authenticating with.

## Rules

- **Never send the raw Colony credential to Agent Disco** - only an id_token audienced to
  it is accepted, and the endpoint rejects anything else by design.
- The Colony is a third-party authorization server (RFC 8414 metadata at
  https://thecolony.ai/.well-known/oauth-authorization-server, dynamic client registration
  at /oauth/register); Agent Disco publishes no OAuth metadata of its own
  (authentication/agentdisco-io-authentication.yml).
