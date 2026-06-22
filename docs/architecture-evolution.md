# TorBot — Architecture Evolution

## 1. Why Document Evolution

Good architecture is rarely designed all at once; it responds to pressure. This document describes, at a conceptual level, how TorBot's architecture grew and why — not a precise timeline, but the direction of travel and the forces behind it.

## 2. Direction of Travel

The architecture evolved from a simpler booking automation into a more modular system as requirements grew. Early on, the priority was simply turning a WhatsApp message into a booking. As more businesses and more concurrent conversations came into play, the system was separated into clearer layers — conversation, orchestration, data, and visibility — so each concern could evolve on its own.

## 3. Pressures That Shaped It

Four pressures did the most to shape the architecture:

- **Conversation state** — handling multi-step, sometimes interrupted conversations reliably pushed conversation handling into its own concern, separate from booking logic.
- **Multi-tenant scoping** — serving many independent businesses on shared infrastructure required tenant context to be carried and checked consistently at every layer.
- **Booking consistency** — avoiding double-booking pushed the system toward verifying availability and holding a slot before confirming, rather than assuming a slot was free.
- **Operational visibility** — businesses needing to see and manage their bookings led to a dedicated dashboard that reads state without touching orchestration.

## 4. How the Layers Emerged

As these pressures accumulated, responsibilities that once sat together were separated:

- Conversation handling was distinguished from booking logic, so the messaging experience and the rules could change independently.
- Availability became a single, authoritative step in the flow rather than an assumption.
- Tenant scoping moved from something implicit to something enforced on each request.
- Visibility was added as a read-and-manage surface rather than bolted onto the conversation.

## 5. What Stayed Constant

Through these changes, a few commitments held: the conversation is the interface, availability is checked before anything is confirmed, and each business's data stays scoped to that business. The structure changed; these commitments did not.

## 6. Where It Is Now

The current structure is described in [architecture-overview.md](./architecture-overview.md). This document explains how it came to look that way; that one explains what it is today.

## 7. What Is Intentionally Not Documented

This document does not include a precise chronology, version history, internal implementation, or workflow details. It describes the architecture's evolution conceptually, consistent with the rest of this showcase.
