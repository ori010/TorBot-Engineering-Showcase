# TorBot — Engineering Decisions

## 1. Purpose

This document records the engineering decisions that most shaped TorBot, in a lightweight decision-record format: **Context → Options → Decision → Trade-off**. It captures *why* the system looks the way it does, not how it is implemented.

## 2. Forces Behind the Decisions

A few constraints shaped almost every choice: a small team building and maintaining the system, many independent businesses sharing one platform, a need for booking logic to evolve quickly, and a hard requirement that availability stay correct. These forces consistently favored proven tools, clear boundaries, and fast iteration over novelty.

## 3. Decisions

### D1 — Orchestration on a workflow-automation platform
- **Context:** Booking logic needed to change often as new business rules emerged.
- **Options:** A hand-written backend service; a workflow-automation platform.
- **Decision:** n8n as the orchestration core.
- **Trade-off:** Faster iteration and visible logic, at the cost of some low-level control a custom service would offer.

### D2 — WhatsApp as the primary interface
- **Context:** Most booking friction comes from asking customers to use a new app or form.
- **Options:** A dedicated app or web form; a WhatsApp-native conversation.
- **Decision:** WhatsApp as the main channel.
- **Trade-off:** Meeting customers where they already are, at the cost of working within WhatsApp's conversational and formatting constraints.

### D3 — Records in n8n DataTables
- **Context:** The orchestration layer needed structured, tenant-scoped records it could read and write in real time.
- **Options:** A separate database tier; n8n's built-in structured storage.
- **Decision:** n8n DataTables.
- **Trade-off:** Less operational overhead and tight integration with orchestration, at the cost of the advanced querying a dedicated database would provide.

### D4 — Server-rendered dashboard from webhooks
- **Context:** Owners needed a simple view of state the orchestration layer already maintains.
- **Options:** A standalone single-page app; server-rendered HTML served from n8n webhooks.
- **Decision:** Server-rendered HTML.
- **Trade-off:** Minimal moving parts and easy maintenance, at the cost of rich client-side interactivity.

### D5 — Shared infrastructure with per-request tenant scoping
- **Context:** The platform serves many businesses and must keep their data separate.
- **Options:** A separate deployment per business; shared infrastructure with scoping enforced on every request.
- **Decision:** Shared infrastructure, scoped per request.
- **Trade-off:** Much lower operational cost and easier scaling, at the cost of requiring disciplined, consistent scoping at every layer.

### D6 — Verify-and-hold instead of optimistic booking
- **Context:** Multiple conversations can target the same slot at once.
- **Options:** Optimistic booking with later conflict resolution; verifying availability and holding a slot before confirming.
- **Decision:** Verify-and-hold before confirmation.
- **Trade-off:** A more deliberate booking path, in exchange for avoiding confirmed conflicts.

### D7 — Calendar and email as external boundaries
- **Context:** Businesses already rely on existing calendars and email.
- **Options:** Build internal calendar and email; integrate with established services.
- **Decision:** Integrate with Google Calendar and Gmail as boundaries.
- **Trade-off:** Consistency with tools businesses already use, at the cost of depending on external services at the boundary.

### D8 — Static onboarding site over in-chat onboarding
- **Context:** New businesses need a place to sign up and configure before using the chat flow.
- **Options:** Onboard entirely inside WhatsApp; a separate static site.
- **Decision:** A static site on Netlify, protected by Cloudflare Turnstile.
- **Trade-off:** A cleaner, abuse-resistant sign-up surface, at the cost of one more channel outside the conversation.

## 4. Decisions I'd Revisit

Some choices fit the current scale but are worth re-examining as the platform grows — for example, where structured-storage and querying needs might eventually outgrow the built-in data layer. These are explored further in [`lessons-learned.md`](./lessons-learned.md).

## 5. What Is Intentionally Not Documented

This document does not include workflow definitions, internal data contracts, schemas, identifiers, payloads, or deployment details. It records decisions and their trade-offs, not the production implementation.
