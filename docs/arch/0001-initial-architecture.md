# ADR 0001 — Initial Repository Architecture

| Field | Value |
|---|---|
| **ADR ID** | 0001 |
| **Title** | Initial Repository Architecture — Separation of Concerns across Repositories |
| **Status** | Accepted |
| **Author** | SaveStateGG Team |
| **Created** | 2026-03-31 |
| **Updated** | 2026-03-31 |

---

## Context

SaveStateGG is a new platform being built from the ground up. As the project grows, multiple teams or individuals will contribute to distinct areas of the system: the domain documentation, the API, the user interface, and the infrastructure.

We need to decide how to organise source code and documentation across repositories. The two primary options are:

1. **Monorepo** — all code lives in a single repository with tooling (e.g., Nx, Turborepo) to manage independent packages and deployments.
2. **Polyrepo (multi-repo)** — each logical concern lives in its own dedicated repository with independent versioning, CI/CD pipelines, and access controls.

---

## Decision

We will adopt a **polyrepo strategy**, separating the project into four dedicated repositories:

| Repository | Purpose |
|---|---|
| `savestategg-docs` | Single Source of Truth: domain documentation, Ubiquitous Language, API specs (SDD), and Architecture Decision Records. |
| `savestategg-api` | Back-end application — REST/GraphQL API, business logic, and data persistence layer. |
| `savestategg-web-ui` | Front-end web application — user interface, routing, and client-side state management. |
| `savestategg-infra` | Infrastructure as Code — cloud resource provisioning, CI/CD pipeline definitions, and environment configuration. |

The `savestategg-docs` repository serves as the **coordination hub**: before any new feature is implemented, its domain terms must be defined in the Ubiquitous Language and its API shape must be specified in a Spec document. No implementation repository takes precedence over the docs repository.

---

## Rationale

- **Clear separation of deployment lifecycles.** The API and the Web UI can be versioned, deployed, and rolled back independently without affecting each other or the infrastructure.
- **Focused access control.** Infrastructure secrets and deployment credentials need only be present in `savestategg-infra`, keeping them away from application code repositories.
- **Reduced blast radius.** A breaking change or misconfigured CI pipeline in the Web UI repository cannot affect the API repository's pipeline.
- **Docs-first culture.** By isolating documentation into its own repository, we reinforce the practice of updating domain language and specs *before* writing implementation code.

---

## Consequences

### Positive
- Teams can work in parallel on different repositories without merge conflicts across concerns.
- Each repository can adopt the best-suited toolchain, language, and CI configuration for its purpose.
- The documentation repository becomes a single, easy-to-audit record of all architectural and domain decisions.

### Negative / Trade-offs
- **Cross-repository changes require coordination.** A feature that touches the API, Web UI, and infrastructure will require pull requests across multiple repositories that must be merged in the correct order.
- **Discoverability.** Developers must know where to look for each type of concern. This is mitigated by the root `README.md` in `savestategg-docs` which links all repositories.
- **Dependency management.** Any shared types or contracts (e.g., TypeScript interfaces generated from API specs) must be published as a package or managed via the spec documents in this repository.

---

## Alternatives Considered

### Monorepo
A monorepo would simplify atomic commits across concerns and reduce duplication in tooling configuration. However, at the current team size and given the early stage of the project, the overhead of monorepo tooling (build caching, task orchestration, affected-project detection) is not justified. This decision may be revisited in a future ADR as the team scales.

---

## Related Documents

- [Ubiquitous Language](../domain/ubiquitous-language.md)
- [Spec 001 — Catalog Contract](../specs/001-catalog-contract.md)
