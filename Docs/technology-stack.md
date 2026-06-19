# TorBot — Technology Stack

## 1. Technology Philosophy

TorBot's technology choices follow the architecture, not the other way around. Each layer — conversation, orchestration, data, and dashboard — is paired with a technology category suited to that layer's job: fast iteration where the booking logic needs to evolve, reliability where availability state must stay correct, and simplicity where a business owner needs a clear view without friction.

The guiding rule was to choose proven, well-supported technology categories over novel ones, so the system stays maintainable as it scales across many businesses.

## 2. Stack Overview

TorBot is built from four technology categories, matching the architectural layers described in `architecture-overview.md`:

- A **messaging layer** that connects the system to customers over WhatsApp.
- An **automation/orchestration layer** that runs the booking logic and coordinates between layers.
- A **data layer** that stores tenant-isolated business, customer, and appointment records.
- A **dashboard layer** that gives business owners and staff visibility into their operations.

External **calendar and communication integrations** sit at the system's boundary, connecting TorBot to services the business already relies on.

## 3. Messaging Layer

The messaging layer is the customer-facing entry point. It receives and sends WhatsApp messages, keeping the entire booking experience inside the channel customers already use rather than redirecting them to a separate app or website. This layer was chosen specifically because it removes the single biggest source of booking friction: asking the customer to go somewhere new.

## 4. Automation / Orchestration Layer

The orchestration layer runs the booking logic: interpreting customer intent, checking availability, and driving a request through to a confirmed appointment. A workflow-automation platform was chosen for this layer because it allows booking logic to be built, adjusted, and extended quickly as new business rules emerge, without requiring a full software release cycle for every change.

## 5. Data Layer

The data layer holds the records TorBot depends on — businesses, customers, staff, slots, and appointments — with isolation enforced so that no business can see or affect another's data. The technology here was chosen for its ability to support structured, tenant-scoped records that the orchestration layer can query reliably in real time.

## 6. Dashboard Layer

The dashboard gives business owners and staff a simple, web-based view of bookings and availability. It's intentionally lightweight: its job is visibility into state the orchestration layer already maintains, not a separate application with its own complex logic. This keeps the dashboard easy to maintain and fast to load.

## 7. Calendar & Communication Integrations

TorBot integrates with external calendar and email services at defined boundaries, so that appointment state stays consistent with the calendars businesses already use, and so the system can communicate with customers and staff through familiar channels. These integrations are treated as boundaries the system talks across — TorBot does not own or replace the underlying calendar or email infrastructure.

## 8. Why This Stack Works

Each technology category was chosen to match the responsibility of its layer, not for novelty. Pairing a fast-to-iterate orchestration layer with a reliable, tenant-aware data layer means booking logic can evolve without putting availability correctness at risk. Keeping the messaging layer focused purely on the customer-facing conversation, and the dashboard focused purely on visibility, means each part of the system stays simple enough to reason about on its own — which is what allows the platform to scale across many businesses without each new tenant adding meaningful complexity.

## 9. What Is Intentionally Not Documented

This document does not include specific implementation details: workflow definitions, internal data contracts, table schemas, internal identifiers, deployment configuration, or step-by-step setup instructions. Those details belong to the production system and are not published as part of this showcase.
