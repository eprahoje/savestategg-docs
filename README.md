# savestategg-docs

> **Single Source of Truth** for the SaveStateGG platform — architecture decisions, domain language, and API contracts.

## Overview

SaveStateGG is a platform for video game enthusiasts, inspired by Letterboxd, allowing users to log, review, and curate lists of games they have played or want to play.

This repository serves as the **central documentation hub** for the entire SaveStateGG ecosystem. It is organised around two complementary methodologies:

- **Domain-Driven Design (DDD)** — models the business domain using a shared, precise vocabulary (Ubiquitous Language) that is reflected in code and documentation alike.
- **Spec-Driven Development (SDD)** — captures API contracts and behaviour specifications *before* implementation, ensuring that all teams (backend, frontend, infrastructure) work from an agreed-upon interface.

## Repository Structure

```
savestategg-docs/
├── README.md                          # This file
├── docs/
│   ├── domain/
│   │   └── ubiquitous-language.md     # Shared domain vocabulary (DDD)
│   ├── specs/
│   │   └── 001-catalog-contract.md    # API contract specifications (SDD)
│   └── arch/
│       └── 0001-initial-architecture.md  # Architecture Decision Records (ADRs)
```

### `/docs/domain/`
Contains the **Ubiquitous Language** glossary — the authoritative list of domain terms used across all repositories, conversations, and documentation. Every term here should be reflected consistently in code (class names, method names, database columns, API fields).

### `/docs/specs/`
Contains **API Contract Specifications** written as machine-readable (JSON/YAML) mock examples before implementation begins. These specs drive front-end development and serve as acceptance criteria for back-end implementation.

### `/docs/arch/`
Contains **Architecture Decision Records (ADRs)** — lightweight documents that capture the *context*, *decision*, and *consequences* of significant architectural choices. ADRs are numbered sequentially and never deleted; superseded decisions are marked as such.

## Related Repositories

| Repository | Description |
|---|---|
| `savestategg-docs` | This repository — Single Source of Truth |
| `savestategg-api` | REST / GraphQL API (back-end) |
| `savestategg-web-ui` | Web front-end application |
| `savestategg-infra` | Infrastructure as Code (IaC) |

## Contributing

1. For domain changes, update `docs/domain/ubiquitous-language.md` and open a discussion.
2. For new API endpoints, add a spec under `docs/specs/` before writing any implementation code.
3. For architectural decisions, create a new ADR under `docs/arch/` using the existing ADR as a template.
