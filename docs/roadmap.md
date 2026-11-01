# Prioritized roadmap

Status: proposed. Progress depends on acceptance evidence, not assumed dates.
Architecture approval authorizes M1 only; each subsequent milestone requires
reviewed scope and evidence from the previous one.

| Priority / milestone | Delivery | Dependencies | Exit gate |
| --- | --- | --- | --- |
| P0 M1 — Foundation | Repository governance, Go API, PostgreSQL, migrations, Compose, docs | Design approval; Go and Docker runtime | All criteria in milestone-1.md |
| P0 M2 — Identity | Local OIDC provider, JWT/JWKS, PKCE test client, RBAC | M1; provider issuing JWT access tokens for the API | Positive/negative authentication and authorization matrix |
| P0 M3 — Workflow | Projects, DB queue, states, gates, audit, retries | M2; stable identity | Two concurrent projects, a third queued, recovery, and no cross-project access |
| P0 M4 — Agents | Four roles, schemas, LLM adapter, supervisor, delivery | M3; selected provider and budget | Real synthetic request, gates, validation, isolated jobs |
| P1 M5 — MCP | Four read-only tools and resource permissions | M2–M4; compatible SDK/transport | Real authorized client and rejection of cross-project queries |
| P1 M6 — Interface | Strict React/TS, PKCE login, review, history | M2–M5 APIs | Automated user journey, keyboard access, error states |
| P0 M7 — Hardening | CI/CD, scans, OTel, dashboards, optional Terraform | M1–M6; cloud destination if desired | Gates, telemetry, reviewable plan without apply, documented rollback |
| P0 M8 — Demo and release | Real E2E, controlled failure, backup/restore, public package | M7 | F01–F12, published limitations, secret review |

P0 means required to declare the MVP complete. M5/M6 remain mandatory parts of
the demo despite their lower risk-reduction priority. M7 consolidates security;
identity, validation, isolation, and secret handling are implemented from the
milestone that introduces each surface, not postponed until M7.

## Dependencies and deferred decisions

- M1: select supported Go/PostgreSQL versions and pin images; confirm Docker
  Desktop/WSL2 for Windows development. Do not install unnecessarily.
- M2: local Keycloak is the proposed test provider, with reproducible configuration
  and locally generated credentials; external OIDC is an alternative.
- M4: choose LLM provider, data policy, budget, and limits; separate provider calls
  from jobs without credentials. The specific SDK has not been selected.
- M5: confirm provider support for MCP audience and required metadata; pin
  protocol/SDK versions and conformity tests.
- M7: GitHub Actions, secret scanning, Go/TS SAST, vulnerability scanning, and image
  scanning; specific tools/versions are selected and pinned in that milestone.
  Terraform uses modules and dev/test/prod configurations; no real credentials.
  The production workflow requires a protected environment, review, and approval.

## Risks and responses

| Risk | Mitigation / evidence |
| --- | --- |
| Malicious generated code or prompt injection | Permitted isolated jobs, closed network, gates outside the model, path escape tests |
| Duplication after failure | Leases, version fencing, idempotent operations, restart test |
| Valid token for the wrong resource | Validate audience/issuer; test ID tokens and API tokens against MCP |
| Provider costs or failures | Quotas, timeout, bounded retries, budget, cancellation |
| Cross-project leaks | Per-request identity, filters, composite FKs; negative API/MCP/runner tests |
| Stale approvals | Approved hash and version; invalidate approval when content changes |
| Insufficient Docker isolation | Trusted local demo; public service requires redesign and specific review |
| Excessive scope | Bounded generation case, one control process, incremental delivery |

## Controlled failure scenario in M8

Interrupt the worker after it claims a stage; verify lease expiration, recovery,
and a single effective result. Repeat with a provider timeout and temporary
PostgreSQL unavailability: readiness must fail, liveness must keep working if
the process responds, and history must support diagnosis. Record steps, metrics,
recovery, and limitations in `docs/operations.md`.
