# forgeflow-ia

A proposed agentic software engineering platform powered by Go, TypeScript, MCP,
and cloud-native infrastructure. Its goal is to coordinate specialized AI agents
to design, build, validate, and deliver reliable software.

## Current status

**Design proposal — pending architectural approval.** This repository contains
planning documents and contributor instructions. No platform functionality has
been implemented yet: there is no running API, dashboard, database, agent
orchestration, or deployment.

## What these files are for

| File | Purpose |
| --- | --- |
| [AGENTS.md](AGENTS.md) | Instructions for AI assistants and contributors: reading order, scope, security boundaries, and verification expectations |
| [Architecture](docs/architecture.md) | Proposed directory structure, high-level diagram, components, data model, and trade-offs |
| [MVP requirements](docs/requirements.md) | What the minimum demonstration should do, what is excluded, and how success will be observed |
| [Architecture Decision Records](docs/adr/) | Five proposed technical decisions, their alternatives, and consequences |
| [Roadmap](docs/roadmap.md) | Prioritized milestones, dependencies, risks, and exit gates |
| [Milestone 1](docs/milestone-1.md) | Exact scope and 15 verifiable acceptance criteria for the first implementation milestone |

All repository documentation is in English. These Markdown files can be read by
humans or AI assistants. For tools that do not load repository instructions
automatically, ask them to read `AGENTS.md` first. Reading these files does not
start agents or implement the platform.

## Next step

Review the proposed architecture, five ADRs, MVP boundaries, and M1 acceptance
criteria. Implementation of M1 starts only after human architectural approval.
Cloud deployment and paid resources require separate explicit approval.
