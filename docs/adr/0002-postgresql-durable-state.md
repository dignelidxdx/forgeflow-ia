# ADR 0002 — PostgreSQL as state store and queue

Status: proposed, pending approval. Date: 2026-11-01.

## Context

State changes, gates, and events must survive restarts and remain consistent;
two executions do not justify an additional broker.

## Proposed decision

Explicit SQL through pgx and its pool, versioned SQL migrations, and a queue in
`executions`. Claim work with a short lock and lease; commit state, event, and
audit together where applicable. No external calls inside transactions.
The migration library will be selected in M1 after reviewing maintenance.

## Alternatives

An in-memory queue loses work on restart. A separate broker requires resolving
the dual-write problem. An ORM adds unnecessary abstraction for a bounded schema.

## Consequences and review

Recovery, lease expiration, and deduplication are application responsibilities.
Exactly-once is not promised. One scheduler limits concurrency to two; the MVP
does not support horizontal scaling. Revisit when backlog or contention is
measured. Test failures, late commits, rollback, and idempotency in M3.
