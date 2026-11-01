# ADR 0001 — modular Go monolith

Status: proposed, pending approval. Date: 2026-11-01.

## Context

Public demo with four roles and two concurrent executions; priority is verifiable
engineering and straightforward operations.

## Proposed decision

One Go module and one control process containing API, worker, and domain modules.
React/TypeScript as a separate client. Execution supervisor separated by privilege;
do not distribute agents as microservices.

## Alternatives

Microservices per agent allow independent scaling but add networking, distributed
contracts, and consistency concerns. An external durable engine facilitates complex
workflows but introduces an unnecessary operational dependency at the outset.

## Consequences and review

Simple deployment and transactions; process failures affect API and worker.
Small interfaces at IO boundaries, without speculative generic layers.
Revisit if multiple replicas or independently measured scaling needs arise.
Verify with module tests, shutdown, and two executions in M3.
