# Booking Consistency Under Concurrent Demand

## Problem

The core promise of a booking system is easy to state and hard to keep: when a customer is told a slot is theirs, it should actually be theirs. In a conversational, WhatsApp-first system this is harder than in a form-based one. Several customers can pursue the same slot in overlapping conversations, each moving at human speed with pauses between messages. Between the moment availability is checked and the moment a booking is confirmed, the situation can change. If the system treats "available a few seconds ago" as "available now," two customers can be confirmed into the same slot — a failure both the business and the customer feel immediately.

## Constraints

- **Conversational pace.** Decisions are spread across messages and seconds, not a single atomic form submission.
- **Concurrency.** Independent conversations can target the same slot at the same time.
- **External calendar boundary.** The business's calendar is an integration point, not an internal lock the system fully controls.
- **Multi-tenant.** The same logic has to hold for many businesses sharing infrastructure.
- **Lightweight core.** The platform favors a workflow-automation core over a custom transactional backend, so the solution had to fit that model.

## Engineering Approach

The decision was to treat availability as a verify-and-hold step rather than an optimistic assumption. Two alternatives were considered and set aside:

- **Optimistic booking** — confirm quickly and detect conflicts afterward. Resolving a conflict *after* telling a customer "confirmed" turns an internal race into a broken promise.
- **A heavyweight locking or transactional layer** — disproportionate to the platform's scale and at odds with the workflow-automation core.

The chosen approach makes availability a single authoritative step in the flow, and reserves (holds) a slot for the short window needed to complete confirmation. The check and the hold belong together: checking without holding leaves the race open; holding without a real check only moves the problem. The business calendar remains the boundary of truth, with the system reconciling against it rather than assuming ownership of it.

## Trade-offs

- A more deliberate booking path (check, hold, confirm) instead of an instant "yes."
- Short-lived holds add state that must be created, honored, and released.
- Treating the external calendar as a boundary means designing for reconciliation rather than total control.

In exchange, the system avoids the one outcome it can least afford: confirming two customers into the same slot.

## Outcome

Confirmations became trustworthy by construction. A confirmation is issued only after a real check and a hold, so the common concurrency failure is designed out of the normal path rather than patched after the fact.

## Engineering Principle

**Make the expensive failure structurally hard, not merely unlikely.** When one outcome (a double-booking) is far more costly than the rest, shape the flow so that outcome requires breaking an explicit step — verification, then reservation — rather than relying on timing to work out.

## What Is Intentionally Not Documented

This case study does not include hold durations, reservation mechanics, data schemas, identifiers, retry logic, or any workflow-level implementation. It describes the reasoning, not the production internals.
