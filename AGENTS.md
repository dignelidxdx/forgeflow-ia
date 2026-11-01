# Repository instructions for AI assistants and contributors

## Purpose and actual status

ForgeFlow IA is a proposed public, portfolio-grade Agentic Software Factory.
The repository currently contains design documentation only. There is no Go API,
React application, database schema, working agent orchestration, MCP server,
Docker environment, or deployed infrastructure yet.

These instructions guide work on this repository. They do not create or run the
four product agents. Agent instructions alone are not a working software factory.

## Start here

Before making changes, read:

1. `README.md` for repository status and the document map.
2. `docs/requirements.md` for MVP scope and observable outcomes.
3. `docs/architecture.md` for structure, boundaries, data model, and workflow.
4. All five records in `docs/adr/` for proposed technical decisions and trade-offs.
5. `docs/roadmap.md` for milestone order, dependencies, and risks.
6. `docs/milestone-1.md` before planning or implementing M1.

Resolve relative paths from the repository root. This file is plain Markdown and
can be read by any assistant or human contributor. Automatic instruction-file
loading depends on the tool; when it is not supported, explicitly ask the
assistant to read `AGENTS.md` before working. No particular AI product, account,
local skill installation, or machine path is required to understand these documents.

## Scope and approval

- The architecture and ADRs are proposals, not approved or implemented behavior.
- Do not treat documentation translation or instruction-file updates as approval
  to implement the platform.
- The original project request requires human architectural approval before M1.
  Check the current conversation and recorded decisions for that authorization.
- Once authorized, implement only the approved milestone; do not build the full
  platform at once. Ask again only when a new decision actually requires approval.
- Mark a decision accepted only after human approval. Record the date and scope
  of approval in the relevant documents; never invent approval or test evidence.
- Cloud provisioning, paid resources, publishing, and sensitive actions require
  explicit authorization covering that action.

## Working conventions

- Write repository documentation, code, comments, and identifiers in English.
  Follow the user's preferred language in conversation.
- Inspect the checkout and applicable instructions before editing. Preserve
  preexisting user changes, including `.gitignore`, and preserve the license.
- Keep changes small, idiomatic, and maintainable. Use the standard library and
  platform capabilities where appropriate; avoid speculative abstractions.
- Use Go for the backend, React with strict TypeScript for the frontend, and
  PostgreSQL for persistent data, as specified in the project request.
- Prefer a modular monolith; do not add microservices, brokers, or a workflow
  platform without a documented need and reviewed architectural decision.
- Create implementation directories only when their milestone needs them.
- Keep factory-wide standards separate from project-specific requirements.
- Update related docs when approved behavior or scope changes. Clearly distinguish
  proposed, approved, implemented, and verified work.

## Security boundaries

- This is a public demonstration repository. Never add real credentials, private
  client information, or components from a private commercial software factory.
- Use placeholders in examples. Never print secrets in logs, reports, or artifacts.
- Do not implement custom password or token cryptography.
- Enforce project authorization in addition to roles. Never trust a client-supplied
  owner identity or allow project identifiers alone to grant access.
- MCP tools remain read-only within the MVP; no arbitrary shell or filesystem access.
- Generated code is untrusted. Keep execution separate from the API, use only
  approved job templates and isolated workspaces, and follow ADR 0005.
- A model cannot grant approvals, bypass quality gates, or authorize paid actions.
- Block critical security findings unless a human-approved, scoped, expiring
  exception with compensating controls is documented.

## Verification and reporting

There are no application build or test commands to run in the current docs-only
state. Do not report an implementation, coverage result, or passing application
tests until the corresponding code exists and the checks have actually run.

For documentation changes, check local links, document consistency, and diff
formatting. Preserve requirement IDs, acceptance criteria, and approval status
when translating or editing.

For implementation milestones, run the checks defined by that milestone and the
available project tooling. M1 requires Go tests, vet, race checks on a compatible
environment, real PostgreSQL integration, and Compose/build/startup verification.
Record commands, outcomes, and any unavailable checks honestly. The initial 80%
coverage target is a goal, not existing evidence or proof of correctness.

A milestone is done only when its acceptance criteria have evidence, applicable
security and quality checks pass, documentation matches the implementation, and
limitations are disclosed. Do not mark an unchecked acceptance item complete.

Report what changed, what was verified, what remains incomplete, and the next
step within the authorized scope.
