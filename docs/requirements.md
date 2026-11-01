# MVP specification

Status: proposed, pending approval. The integrated MVP is completed in M8;
M1 provides only the technical foundation, not an autonomous factory.

## Users and scope

An authenticated demo operator using public synthetic data. The operator can
create projects, review requirements and architecture, authorize execution, and
download a delivery package. This is not a public multiuser service or a commercial platform.

Demonstration case: generate a small Go CRUD API with PostgreSQL, tests, Docker,
and documentation from a request. The generated domain is initially limited to
one simple entity; payments, private data, and deployment are excluded.
Supported execution templates will cover Go and permitted delivery tools;
other languages or stacks may be recommended but will not be presented as
executable without actual runner support.

## Requirements and final evidence

| ID | Capability | Observable criterion in M8 |
| --- | --- | --- |
| F01 | Project registry | Create, list, and retrieve; data survives restart |
| F02 | Identity and permissions | PKCE login; reject invalid tokens, ID tokens, insufficient roles, and cross-project access |
| F03 | Real orchestration | Two projects progress concurrently, a third waits; persistent history |
| F04 | Four agents | Each role calls a real provider and produces validated output; errors remain visible |
| F05 | Human review | Requirements, architecture/execution, and delivery pause until current approval |
| F06 | Controlled execution | Permitted jobs only; generated code tests and artifacts linked to execution |
| F07 | Recovery | Killing a worker allows lease recovery; late results do not overwrite newer state |
| F08 | MCP | Four read-only tools, validated inputs, and negative authorization tests |
| F09 | Dashboard | Accessible login, creation/list/detail, requirements, ADRs, states, gates, and history |
| F10 | Delivery | Package with source, tests, results, Docker, CI, and example Terraform |
| F11 | Cancellation and limits | Cancellation stops work; timeout, attempts, and budget are verifiable |
| F12 | Operations | Visible metrics/traces, documented and rehearsed controlled failure and restoration |

A deterministic adapter may be used in tests, labeled as a fixture. The final
demo must include real execution; agent instructions or simulated responses do
not satisfy F04. Generated code must pass checks before being offered as a
delivery; COMPLETED does not imply universal software correctness.

## Outside the MVP

Billing, organizations, high availability, horizontal scaling, Kubernetes, an
agent marketplace, unrestricted shell, cross-project memory, autonomous deployment,
general support for any stack, and execution of untrusted public requests.

## Quality and security

- Input validation, size limits, consistent errors, and audit logging.
- Idiomatic Go, strict TypeScript, accessible components, and frontend tests.
- Initial coverage target of 80%, configurable through reviewed changes; it does
  not replace isolation, concurrency, authentication, and integration tests.
- M1 establishes tests and measurement; CI enforces the threshold and security gates in M7.
- Block critical findings; an approved exception needs an owner, justification,
  scope, expiration, and compensating control recorded in the repository.
- No real secrets, client data, or private components from another factory.
- Versioned global standards in `standards/`; project-specific requirements in DB.
- Model calls use cost limits and synthetic data; real test credentials are
  configured locally and are not stored in artifacts.
