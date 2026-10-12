---
description: "Create a production-minded .NET REST API boilerplate with hexagonal architecture, identity and health endpoints, OWASP-aligned security, and Docker support."
name: ".NET Web API Boilerplate"
argument-hint: "Optional: solution name, database preference, or constraints"
agent: "agent"
---

Create a working .NET Web API boilerplate in the current workspace. Treat `$ARGUMENTS` as optional project name, database preference, and additional constraints. If the workspace already contains a project, inspect it first and extend it without overwriting unrelated work. If it is empty, create the complete solution structure.

## Baseline

- Target the latest released .NET LTS version supported at the time this prompt is run. Verify the version against Microsoft's official .NET support policy when possible. Do not use preview releases; state the chosen version in the final summary.
- Use C# and ASP.NET Core. Follow REST conventions: resource-oriented routes, correct HTTP methods and status codes, request validation, consistent `ProblemDetails` errors, and API versioning where appropriate.
- Use hexagonal architecture with clear inward dependencies, for example `Domain`, `Application`, `Infrastructure`, and `Api` projects. Keep domain and application logic independent of ASP.NET Core, persistence, and external services. Define ports at the inner boundary and implement adapters in infrastructure.
- Apply clean-code principles: cohesive responsibilities, descriptive names, small focused units, explicit boundaries, and no unnecessary abstractions or boilerplate duplication.

## Required API Surface

- Add a liveness/health endpoint and a readiness endpoint that checks required dependencies without exposing sensitive details. Configure container health checks to use the appropriate endpoint.
- Add versioned identity endpoints for registration, login, and the authenticated user's profile. Include refresh/revocation endpoints only when supported by the chosen authentication design.
- Use PostgreSQL for persistence and ASP.NET Core Identity with its PostgreSQL store for user management and password hashing. Do not invent cryptography, store plaintext credentials, or expose account-existence details unnecessarily. Protect authenticated routes with authorization and apply appropriate rate limits to authentication endpoints.
- Make the authentication/token approach explicit; ASP.NET Core Identity does not itself define a production-ready JWT issuance strategy. Use an established OAuth2/OIDC-compatible approach or a well-maintained library, never roll cryptography by hand, and do not present development-only token issuance or keys as production-ready. Document key management and any external identity-provider assumptions.

## Security and Operations

- Apply OWASP-aligned practices for API security: strict input validation, least-privilege authorization, secure password handling, rate limiting, restrictive CORS, safe error responses, security headers, and protection against injection and mass assignment.
- Keep secrets out of source control and container images. Use configuration/environment variables for deployment and development user-secrets where appropriate. Do not log passwords, tokens, or sensitive personal data.
- Use HTTPS in deployed environments, pin compatible package versions, and avoid adding dependencies without a clear need. Document remaining production hardening and configuration requirements.
- Add focused unit tests for domain/application behavior and integration tests for API routing, health checks, and identity/security behavior. Tests must not depend on real external services.

## Containers and Delivery

- Add a multi-stage `Dockerfile` that publishes the API, runs as a non-root user, and supports graceful shutdown.
- Add `docker-compose.yaml` with the API and PostgreSQL, durable development data, health checks, and dependency readiness conditions. Do not put real secrets in the compose file; provide safe local defaults only when they cannot be mistaken for production credentials.
- Include concise setup/run instructions and configuration documentation. Ensure the solution builds and the tests run; report commands and any blockers rather than claiming unverified success.

Before finishing, inspect the generated project for incorrect project references or architecture dependency direction, run the available build and tests, and summarize the project structure, selected .NET LTS version, run commands, security choices, and any explicit limitations.