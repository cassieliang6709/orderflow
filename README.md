# OrderFlow

OrderFlow is the portfolio-facing packaging of a Java Spring Boot order-processing backend built from an existing takeout-domain codebase. The goal is to present the project as a reusable backend system for order lifecycle management, inventory consistency, payment status handling, and operational workflows.

## Overview

This repository originally contained course-oriented material around a takeout application. For software engineering recruiting, especially `Amazon SDE Intern`, the project is now framed as an order-processing system with stronger emphasis on:

- REST APIs
- layered backend architecture
- order state transitions
- inventory and payment coordination
- persistence and mapper structure
- caching and reliability roadmap
- reproducible local development

The original domain model is still useful because it already contains the core business entities needed for a realistic transactional backend.

## Architecture

The current repository uses a modular Java structure at the repo root:

- `sky-common`: shared infrastructure, utilities, interceptors, and configuration helpers
- `sky-pojo`: entities, DTOs, and VOs for order, user, dish, category, and related business data
- `sky-server`: Spring Boot application, mappers, configuration, and runtime entrypoint

Portfolio-facing target architecture:

- `api`: REST controllers, request validation, global exception handling
- `service`: order orchestration, inventory coordination, payment status transitions, notification hooks
- `domain`: order, inventory, payment, and user lifecycle concepts
- `persistence`: MySQL-backed mapper and repository layer
- `cache`: Redis-backed hot data and idempotency support
- `infra`: logging, async tasks, configuration, and local container setup

## Tech Stack

- Java
- Spring Boot
- MyBatis
- MySQL
- Redis
- Docker / Docker Compose
- JUnit 5
- GitHub Actions

## Core Workflows

### Order lifecycle

- create order
- validate items and pricing
- persist order and order details
- transition status across processing steps

### Inventory consistency

- reserve or validate availability before submission
- update stock-related state during order flow
- expose operational queries for follow-up actions

### Payment status update

- receive payment-related state changes
- map them into order status transitions
- prepare the system for asynchronous handling and retries

## API Endpoints

The existing codebase already contains rich backend endpoints in the `sky-server` module. The next packaging step is to standardize the public-facing examples around:

- order submission
- order query and status update
- cart and checkout flow
- operational reporting endpoints

## Local Setup

Current local project root:

```bash
cd orderflow
```

Typical backend workflow:

```bash
mvn -DskipTests install
cd sky-server
mvn spring-boot:run
```

The repository also includes environment-specific configuration under `sky-server/src/main/resources`.

## Testing

Packaging goal for the next stage:

- add service-level tests for order lifecycle logic
- add API-level tests for critical request flows
- document reliability-oriented edge cases such as duplicate submission and failed status transitions

## Roadmap

1. Standardize the project naming across docs and portfolio pages
2. Add example API requests and architecture diagrams
3. Introduce idempotent submission and clearer async status handling
4. Add Redis-backed caching and structured test coverage
5. Publish a cleaner local demo and deployment story

## Supporting Docs

- [OrderFlow packaging notes](./docs/orderflow-overview.md)
- Public repository: [cassieliang6709/orderflow](https://github.com/cassieliang6709/orderflow)
- Upstream base repository: [shuhongfan/sky-take-out](https://github.com/shuhongfan/sky-take-out)
- legacy course materials remain in the repo for reference, but the portfolio narrative should prioritize backend systems engineering
