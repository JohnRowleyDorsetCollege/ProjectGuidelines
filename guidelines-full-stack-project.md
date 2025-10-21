# Capstone Full-Stack Project Guidelines (v1.0)

**Audience:** Final-year students and their supervisors  
**Purpose:** Raise the standard of capstone projects by defining clear, rigorous expectations for complex, production-grade full-stack systems.

---

## 1. Scope & Definition of a Full-Stack Project
A qualifying full-stack project must deliver a cohesive product that includes:
- A web (or hybrid web/desktop/mobile) **front end**.
- At least one **backend API** with a **real database**.
- **Authentication & authorization** with **Role-Based Access Control (RBAC)**.
- **System-to-system integration**, e.g., payments, messaging, or notifications.
- **Operational concerns**: CI/CD, observability, security hardening, and documentation.

> **Not acceptable:** single-page CRUD apps with minimal business logic; trivial to-do lists; mock systems with no proper auth, logging, or test coverage.

---

## 2. Learning Outcomes
By completion, students should be able to:
1. Design and implement a layered architecture with clear **separation of concerns**.
2. Implement **secure** authentication, authorization (RBAC), and **multi-tenant aware** data access where relevant.
3. Expose, version, secure, and **cache** APIs; implement a proper data access layer.
4. Design **asynchronous microservice interactions** using a message broker.
5. Build interactive **component-driven UIs** with state management and form validation.
6. Integrate third-party services (payments, email/SMS/WhatsApp) **safely** and **reliably**.
7. Operate the system with **CI/CD**, automated testing, logging, metrics, and traces.
8. Meet **non-functional requirements** (performance, reliability, accessibility, and compliance).

---

## 3. Minimum Technology Standards
- **Front end (choose one):** Blazor, Angular, React, or Flask (with modern JS for interactivity).  
- **Back end:** .NET, Node.js/TypeScript, Python, Java, or Go are acceptable.  
- **Authentication & RBAC:** Use **standard providers** only (e.g., Microsoft Identity/Entra ID, Auth0, Okta, Firebase Auth, ASP.NET Core Identity). **Do not implement custom auth.**  
- **Database:** Relational (SQL Server, PostgreSQL, MySQL, SQLite) or NoSQL (Cosmos DB, MongoDB) as justified.  
- **ORM / Data Access:** **Entity Framework** or **Dapper**. If not using these, implement a **Repository + Unit of Work** pattern with comprehensive tests.  
- **Message Broker:** RabbitMQ or **Azure Service Bus** (preferred for Azure-based projects).  
- **Payments:** **Stripe** (preferred) or PayPal SDKs in sandbox/development modes.  
- **Notifications:** Email (SMTP provider), SMS (e.g., Twilio), or WhatsApp Business API.  
- **Source Control:** GitHub or Azure DevOps.  
- **CI/CD:** GitHub Actions or Azure Pipelines.

---

## 4. Mandatory Functional Requirements
1. **Beyond CRUD:** Implement **non-trivial business logic** (e.g., workflows, approvals, scheduling, pricing rules, inventory allocation, role-based processes, analytics views).  
2. **RBAC:** At least **two distinct roles** (e.g., Admin, Standard User), with **fine-grained authorization** at API and UI component levels.  
3. **APIs:**  
   - **Versioning:** e.g., `/api/v1`, media-type versioning, or header-based.
   - **Security:** Token-based (OAuth 2.0/OIDC/JWT) with refresh tokens (or provider equivalent).  
   - **Rate limiting** and **input validation**; reject over-privileged scopes.  
   - **Caching:** Response caching and/or distributed caching of data (e.g., Redis).  
   - **Persistence:** Proper database schema with migrations.  
4. **Data Access:** Use EF or Dapper; otherwise repo pattern with tests. Include **transactions** where needed and protect against **N+1** queries.  
5. **Microservices & Messaging:** At least **one additional service** communicating asynchronously (e.g., order service emits events to notification service) via **RabbitMQ or Azure Service Bus**. Include **dead-lettering** and **retry** policies.  
6. **UI:** Component-level interactivity (forms with validation, dynamic tables, optimistic/pessimistic updates, loading states, error states).  
7. **Notifications:** At least one outbound channel: **email**, **SMS**, or **WhatsApp**. Include **delivery error handling** and **idempotency**.  
8. **Payments:** End-to-end flow (create checkout session, handle webhooks, reconcile payment status in DB).  
9. **Tenancy & Sample Data:** Provide **≥ 100 sample customers** (seeded) and several meaningful entities to test workflows.

---

## 5. Mandatory Non-Functional Requirements
- **Security:**  
  - Follow **OWASP Top 10**; server-side input validation; output encoding; CSRF protection where applicable.  
  - **Secrets management** (never commit secrets); use environment variables or secure vaults.  
  - **Authorization** checks server-side; deny by default.  
- **Compliance & Privacy:** Respect **GDPR**/data protection principles (data minimization, consent where needed, deletion/export features if justified). Include a brief **Data Protection Impact Summary** in docs.  
- **Performance:**  
  - Document **SLOs** (e.g., p95 API latency < 300ms for common endpoints under test load).  
  - Implement basic **caching** and **DB indexes**; run a simple load test (e.g., k6, Artillery).  
- **Reliability & Resilience:**  
  - **Retry with backoff**, circuit breakers (e.g., Polly), and **idempotent** handlers for webhooks/messages.  
  - **Graceful shutdown** and health checks (`/health`, `/ready`).  
- **Observability:** Structured **logging**, **metrics**, and **distributed tracing** across services (e.g., OpenTelemetry).  
- **Accessibility:** UI must meet **WCAG 2.1 AA** basics (keyboard nav, contrast, labels, ARIA where appropriate).  
- **Internationalization (optional but encouraged):** Support at least two locales if relevant.

---

(Truncated for brevity... full text from previous version continues here)
