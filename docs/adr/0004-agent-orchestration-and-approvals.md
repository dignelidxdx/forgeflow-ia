# ADR 0004 — structured agents and human gates

Status: proposed, pending approval. Date: 2026-11-01.

## Context

Four prompts do not constitute orchestration. Verifiable progress, limits,
recovery, and approvals that the model cannot issue for itself are required.

## Proposed decision

The Go orchestrator runs sequential analyst → architect → engineer → devops stages.
Each agent uses an LLM adapter with JSON Schema output and project-scoped context.
Gates follow requirements, architecture before code, and delivery before acceptance;
approval is bound to version/hash and human identity. MCP provides consultative
tools; it is neither an agent nor a workflow engine.

## Alternatives

Free-form agent chat makes reproducibility and control harder. A full agent
framework could accelerate tool integration but does not eliminate persistence,
isolation, or authorization; defer until a concrete need exists.

## Consequences and review

Less exploratory autonomy, more traceability. Schema and quality are validated
through separate controls; valid JSON does not prove correctness. Bounded retries,
budget, and visible errors. Fixtures are identified as tests, never real execution.
Validate states and gates in M3; a real provider and outputs from all four roles
in M4. Revisit internal parallelism only when a measured need exists.
