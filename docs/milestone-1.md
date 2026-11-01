# Milestone 1 — scope and acceptance

Status: proposed; not implemented. Requires architecture approval.

## Scope

Reproducible local foundation: one Go module, HTTP with health/readiness,
PostgreSQL pool, migrations, environment configuration, Docker/Compose, and
initial documentation. No agents, login, project API, runner, MCP, frontend,
or cloud in this milestone. Bind locally by default; do not publish a business API before M2.

## Verifiable criteria

- [ ] M1-01: README describes prerequisites, Windows/PowerShell and Compose commands,
  variables, tests, migration, startup, and shutdown from a clean checkout.
- [ ] M1-02: `AGENTS.md` defines public repository boundaries, secrets, sensitive
  action review, standards, Definition of Done, and required validation. Preserve
  the license and any preexisting user changes.
- [ ] M1-03: `GET /healthz` returns 200 when HTTP is alive. `GET /readyz` returns
  200 only with DB available and expected schema; otherwise a sanitized 503.
- [ ] M1-04: Configuration validates required values and pool/timeout limits;
  invalid configuration fails at startup without exposing credentials.
- [ ] M1-05: Contexts and timeouts reach SQL queries. SIGTERM stops accepting
  traffic, drains requests within the configured deadline, and closes pool/process.
- [ ] M1-06: Error responses use a stable code, safe message, and request ID;
  JSON logs include correlation and contain no tokens or complete DSNs.
- [ ] M1-07: Initial migration creates `projects` with UUID, issuer/subject owner,
  name, request, timestamps, and constraints/owner index. Other tables are added
  in M3/M4. A test inserts/queries directly, without introducing the CRUD API early.
- [ ] M1-08: Explicit, versioned migrations work on an empty DB; rerunning does not
  alter data; an unexpected version blocks readiness. Do not migrate from every
  replica at API startup. Document local rollback and the forward-fix strategy.
- [ ] M1-09: Separate runtime/migration roles; runtime cannot execute DDL.
  A transaction test demonstrates commit and rollback without partial writes.
- [ ] M1-10: Dockerfile uses build stages, a minimal runtime image, and a non-root
  user. Compose configures persistent DB, healthcheck, and local API; restart
  preserves data. DB ports are unpublished except for a documented development override.
- [ ] M1-11: `.env.example` contains only placeholders and guidance for generating
  local values. Dev/test/prod have explicit policies; unsafe local configuration
  is not accepted by default in prod. No real secrets are added to the repository.
- [ ] M1-12: `go test ./...`, `go vet ./...`, and race detector tests pass in a
  compatible environment; Go formatting is clean. Integration uses real PostgreSQL
  and tests readiness, persistence, migrations, and transaction boundaries.
- [ ] M1-13: Publish the coverage command and initial measurement, with a configurable
  80% target and no coverage claims before execution. DB and configuration failures
  receive useful tests, without tests that merely copy the implementation.
- [ ] M1-14: Verify `docker compose config`, build, and startup; record the environment
  used and report any checks that cannot be executed as pending.
- [ ] M1-15: `docs/security.md`, `docs/quality-standards.md`, `docs/deployment.md`,
  and `docs/operations.md` exist, covering current limits, TLS outside local,
  DB users, backup/restore, startup, diagnosis, and safe shutdown.

## Work order after approval

1. Initial rules and documentation; pin tools and versions.
2. Configuration, logger, and HTTP server with a verifiable lifecycle.
3. Pool, migrator, initial schema, and DB checks.
4. Docker/Compose and reproducible integration environment.
5. Execute acceptance checks, record evidence, and present M1 for review.

Completing M1 does not authorize M2 or cloud provisioning.
