# Personal Finance Tracker — System Design (Java 21 + Spring Boot 3.3)

> Status: Draft v0

---

## Documentation Index

* [System Design](system-design.md)
* [Roadmap](roadmap.md)
* [Architecture Decisions (ADRs)](adr/)

---

# Roadmap

This roadmap defines small, progressive sprints to deliver the project step by step. Each sprint has a clear goal, tasks, and a definition of done (DoD).

## Sprint 0 — Skeleton 09/09/2025 Done!

**Goal:** Project runs locally with Spring Boot 3.5.5 and Java 21.
**Tasks:** Generate project with Gradle Kotlin DSL, Web, Validation, Actuator. Start app with `./gradlew bootRun`.
**DoD:** `curl http://localhost:8080/actuator/health` responds `UP`.

## Sprint 1 — Hello endpoint 09/09/2025

**Goal:** First REST endpoint and test pipeline.
**Tasks:** Add `GET /api/v1/hello` returning `{ "message": "Hello, Ledgerly" }`. Add a Spring Boot test.
**DoD:** Test green with `./gradlew test`.

## Sprint 2 — Modular structure

**Goal:** Introduce modules for clean architecture.
**Tasks:** Create modules `app`, `domain`, `application`, `adapters:rest`. Move controller to `rest`.
**DoD:** `./gradlew :app:bootRun` works.

## Sprint 3 — Account domain (in-memory)

**Goal:** Implement domain and use case without DB.
**Tasks:** Define `Account` record in `domain`. Add service in `application`. Create REST endpoints for create/list. Use in-memory repo.
**DoD:** POST and GET work with fake data.

## Sprint 4 — Virtual Threads

**Goal:** Enable Java 21 virtual threads.
**Tasks:** Set `spring.threads.virtual.enabled=true`. Optionally add `Executors.newVirtualThreadPerTaskExecutor()`.
**DoD:** Logs confirm VT enabled.

## Sprint 5 — PostgreSQL with Flyway

**Goal:** Real persistence with Postgres.
**Tasks:** Add persistence adapter with JPA. Setup Docker for Postgres. Create `V1__init.sql`.
**DoD:** DB runs via `docker compose up -d db`. App boots and health is OK.

## Sprint 6 — Replace memory with JPA

**Goal:** Real persistence for accounts.
**Tasks:** Implement `AccountService` using JPA repo. Add Bean Validation.
**DoD:** Accounts persist and list from DB.

## Sprint 7 — Security with JWT

**Goal:** Protect endpoints with stateless JWT.
**Tasks:** Implement register/login with BCrypt. Add JWT filter.
**DoD:** Unauthorized requests return 401. Authorized requests succeed.

## Sprint 8 — Transactions

**Goal:** Add financial transactions.
**Tasks:** Define sealed type `TransactionKind`. Add entity `Transaction`. Create endpoints to add/list transactions with filters.
**DoD:** Transactions can be created and listed by account and date range.

## Sprint 9 — Monthly report

**Goal:** Provide reporting API.
**Tasks:** Implement `GET /reports/balance`. Use modern Java features like `switch` expressions.
**DoD:** Returns totals for income, expense, and net.

## Sprint 10 — Observability + README

**Goal:** Make project professional.
**Tasks:** Enable Actuator endpoints. Write README in English B2 with: what it is, stack, how to run, example curl, link to docs.
**DoD:** Recruiter-friendly repo with docs.

## Sprint 11 — Kafka events (optional)

**Goal:** Event-driven extension.
**Tasks:** Publish `TransactionCreated` event to Kafka. Add Docker Kafka service.
**DoD:** Event visible when transaction is created.

---

This roadmap will guide development from a simple skeleton to a full-featured, modern Java 21 backend showcasing clean architecture, virtual threads, and event-driven extensions.
