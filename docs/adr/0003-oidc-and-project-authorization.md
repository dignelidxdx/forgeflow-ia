# ADR 0003 — external OIDC and project authorization

Status: proposed, pending approval. Date: 2026-11-01.

## Context

Demonstrate standard authentication without implementing custom passwords or
JWTs, and without allowing one project to read another project's data.

## Proposed decision

Configurable OIDC provider; local test Keycloak as the initial option. A public
SPA uses Authorization Code + PKCE S256, state and nonce as required by the
protocol; access tokens stay in memory. The backend uses a maintained library,
issuer/JWKS from trusted configuration, allowed algorithms, audience, and time
validation. Stable identity is issuer + subject; roles and ownership are evaluated
together. The provider must issue JWT access tokens intended for this API; do not
assume any OIDC token is a compatible access token. MCP has an explicit resource/
audience and does not use token passthrough.

## Alternatives

Custom authentication increases risk. A cookie-based BFF reduces token exposure
to JavaScript but adds sessions and CSRF protection; reconsider before public
hosting. API keys do not demonstrate interactive identity or PKCE.

## Consequences and review

Dependency on provider, JWKS rotation, clocks, and discovery failures. Validate
configuration, cache keys with limits, and fail closed for an unknown key that
cannot be verified. No token-supplied `jku` URL determines the key source.
Test issuer/audience/signature/expiration/role/ownership, PKCE, and rotation in M2;
the dashboard integrates the flow in M6. Review BFF before opening a public service.
