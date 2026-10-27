### Hi, I'm Mirjana :wave:

Backend engineer from Novi Sad, Serbia :serbia: — Java, Spring Boot, PostgreSQL, Kafka.

<p align="center">
<a href="mailto:mirkamsc@gmail.com">Email me</a> ·
<a href="https://github.com/self-improvement-mirjana/beauty-health">See my main project</a>
</p>

 - :mag: I care about what keeps data correct when several services and concurrent requests touch it at once, and what happens when a call fails halfway.
 - :memo: I start from requirements: specification, data model and tickets with acceptance criteria first, then code against them.
 - :robot: I build with AI coding assistants (Cursor, Claude Code), and I review and test everything they write.
 - :briefcase: Freelance backend developer: new features for an ERP system that a business runs on every day.
 - :books: In a 1:1 backend mentorship: concurrency, transactions and isolation, web security, testing, distributed systems design.

---

#### :hammer_and_wrench: Featured: [Beauty & Health](https://github.com/self-improvement-mirjana/beauty-health)

A multi-service e-commerce platform, built end to end: three Spring Boot services (shop API, mock bank, analytics), each with its own PostgreSQL database, plus three React + TypeScript front ends, all run with Docker Compose.

| Problem | How it's handled |
|---|---|
| Two customers buy the last item at the same time | Checkout is one transaction; inventory rows are locked pessimistically in a fixed order (no deadlocks); out of stock → full rollback and `409 Conflict` |
| Someone replays a payment request | Server-to-server calls are signed (RSA-SHA256 / HMAC-SHA256) over timestamp, nonce and body; stale timestamps and reused nonces are rejected |
| The payment webhook arrives twice | The bank retries with exponential backoff; the shop verifies the signature and skips payments it has already processed |
| The database commits but Kafka is down | Transactional outbox: the event is saved in the same transaction as the order and published later with retries; the consumer drops duplicate event IDs |
| An order jumps to an invalid state | The order lifecycle is an explicit state machine: `NEW → CONFIRMED → SHIPPED → COMPLETED` |

Tested with JUnit 5, MockMvc, Testcontainers (real PostgreSQL) and Playwright (full customer-to-moderator journey).

---

#### :toolbox: Toolbox

 - **Backend:** Java 17/21 · Spring Boot 3 (Web, Data JPA, Security, Kafka) · REST / OpenAPI · PostgreSQL · Liquibase · Apache Kafka · Maven · Gradle
 - **Distributed systems:** transactional outbox · idempotent consumers & webhooks · retries with backoff · request signing & replay protection · pessimistic locking · rate limiting · versioned event contracts
 - **Security & testing:** JWT · role-based access · BCrypt · JUnit 5 · MockMvc · Testcontainers · Playwright
 - **Also:** TypeScript · React · Docker & Docker Compose · Git

---

> "It works on my machine" is a hypothesis. "It works when the network drops halfway through" is engineering.
