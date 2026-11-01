# ADR 0005 — isolated execution and delivery without automatic deployment

Status: proposed, pending approval. Date: 2026-11-01.

## Context

Model-proposed code and commands are untrusted. The demo must run tests without
exposing the machine, database, or third-party credentials.

## Proposed decision

A separate local supervisor runs permitted job templates in ephemeral containers;
exclusive workspace per project/execution, bounded resources, non-root user,
network disabled by default, and no secrets or runtime socket in the child.
The API never accepts arbitrary shell. Exported artifacts are validated for paths,
size, and sensitive content; the package includes a manifest and checksums and
is not executed automatically on download. Terraform is delivered as code and a
reviewable plan; apply, publishing, and paid resources require separate explicit approval.

## Alternatives

Host execution is simple but exposes data and tools. A VM/microVM or managed
runner provides a stronger boundary at higher operational cost; it must be
reconsidered before accepting untrusted public code.

## Consequences and review

The supervisor holds sensitive privileges and must restrict its channel and
validation. Local Docker does not justify claiming a secure public service for
hostile code. Dependencies are prepared in a controlled phase, separate from jobs
without network access. Test traversal, symlinks, access to other workspaces,
timeout, cancellation, limits, and absence of secrets in M4; release review in M8.
