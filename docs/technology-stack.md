# TorBot — Technology Stack

## 1. Technology Philosophy

TorBot's technology choices follow the architecture, not the other way around. Each layer — conversation, orchestration, data, and dashboard — is paired with a technology suited to that layer's job: fast iteration where the booking logic needs to evolve, reliability where availability state must stay correct, and simplicity where a business owner needs a clear view without friction.

The guiding rule was to choose proven, well-supported technologies over novel ones, so the system stays maintainable as it scales across many businesses.

## 2. Stack at a Glance

TorBot's layers map to concrete, well-supported technologies (see [architecture-overview.md](./architecture-overview.md) for how the layers fit together):

| Layer | Technology |
|---|---|
| Messaging | WhatsApp Cloud API (Meta Graph API) |
| Automation / orchestration | n8n (workflow automation) |
| Data | n8n DataTables (structured, tenant-scoped records) |
| Dashboard | Server-rendered HTML served from n8n webhooks |
| Calendar & email | Google Calendar, Gmail |
| Onboarding | Netlify static site + Cloudflare Turnstile |
| Documentation & diagrams | Markdown, Mermaid |

The sections below explain why each choice fits the layer it serves. Internal specifics — workflow definitions, data contracts, schemas, and identifiers — are intentionally out of scope (see section 9).

## 3. Messaging Layer

The messaging layer is the customer-facing entry point, built on the **WhatsApp Cloud API (Meta Graph API)**. It receives and sends WhatsApp messages, keeping the entire booking experience inside the channel customers already use rather than redirecting them to a separate app or website. This channel was chosen specifically because it removes the single biggest source of booking friction: asking the customer to go somewhere new.

## 4. Automation / Orchestration Layer

The orchestration layer runs the booking logic: interpreting customer intent, checking availability, and driving a request through to a confirmed appointment. **n8n**, a workflow-automation platform, was chosen for this layer because it lets booking logic be built, adjusted, and extended quickly as new business rules emerge, without requiring a full software release cycle for every change.

## 5. Data Layer

The data layer holds the records TorBot depends on — businesses, customers, staff, slots, and appointments — using **n8n DataTables** for structured, tenant-scoped records that are processed within a specific business context. Keeping data close to the orchestration layer lets booking logic read and write the records it needs reliably and in real time, without operating a separate database tier.

## 6. Dashboard Layer

The dashboard gives business owners and staff a simple, web-based view of bookings and availability. It is **server-rendered HTML served directly from n8n webhooks** — intentionally lightweight, with its job being visibility into state the orchestration layer already maintains rather than a separate application with its own complex logic. This keeps it easy to maintain and fast to load. Business onboarding is handled separately by a **static site hosted on Netlify**, protected against automated abuse by **Cloudflare Turnstile**.

## 7. Calendar & Communication Integrations

TorBot integrates with **Google Calendar** and **Gmail** at defined boundaries, so that appointment state stays consistent with the calendars businesses already use, and so the system can communicate with customers and staff through familiar channels. These integrations are treated as boundaries the system talks across — TorBot does not own or replace the underlying calendar or email infrastructure.

## 8. Why This Stack Works

Each technology was chosen to match the responsibility of its layer, not for novelty. Pairing a fast-to-iterate orchestration layer (n8n) with structured, tenant-scoped storage (n8n DataTables) means booking logic can evolve without putting availability correctness at risk. Keeping the messaging layer focused purely on the customer-facing WhatsApp conversation, and the dashboard focused purely on visibility, means each part of the system stays simple enough to reason about on its own — which is what allows the platform to scale across many businesses without each new tenant adding meaningful complexity.

## 9. What Is Intentionally Not Documented

This document does not include specific implementation details: workflow definitions, internal data contracts, table schemas, internal identifiers, deployment configuration, or step-by-step setup instructions. Those details belong to the production system and are not published as part of this showcase.
