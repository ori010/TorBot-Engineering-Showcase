# TorBot

**TorBot is a production-grade, multi-tenant appointment booking platform that turns WhatsApp into a complete scheduling channel.** This repository is a public engineering showcase: it documents what was built and how it was designed, without exposing the production system itself.

TorBot lets small and mid-sized service businesses — salons, clinics, studios — manage bookings, customers, and availability through a conversational WhatsApp flow, backed by a business-facing dashboard and a calendar-aware automation engine.

It is not the production codebase, and it intentionally does not expose workflow implementations, internal contracts, or operational internals. See [`DISCLAIMER.md`](./DISCLAIMER.md) (and `docs/security-and-sanitization.md`, once published) for what is and isn't included here.

---

## Highlights

- WhatsApp-native booking, rescheduling, and cancellation
- Multi-tenant architecture with isolated customers and calendars per business
- Real-time availability checks to prevent double-booking
- Business dashboard for bookings, staff, and activity
- Waitlist handling for fully booked slots
- Calendar-synchronized appointment state

## The Problem

Service businesses lose bookings to friction: phone tag, missed messages, double-booked slots, and no-shows that go untracked. Most booking tools assume the customer will open an app or a web form. In practice, the channel customers already use — WhatsApp — is rarely treated as a first-class interface for scheduling.

TorBot was built to close that gap: let the customer book, reschedule, or cancel entirely inside a WhatsApp conversation, while giving the business owner a single dashboard to see and control what's happening across every customer and every tenant.

## What TorBot Does

- **WhatsApp-native booking** — customers schedule, modify, and cancel appointments through natural conversation, no app install required.
- **Multi-tenant by design** — a single platform instance serves multiple independent businesses, each with isolated customers, staff, and calendars.
- **Real-time availability** — bookings are checked and held against live calendar state to prevent double-booking.
- **Business dashboard** — owners and staff view bookings, manage availability, and track activity without touching the underlying automation.
- **Waitlist handling** — when a slot isn't available, customers can be queued and notified if one opens up.
- **Calendar integration** — appointment state stays synchronized with the business's calendar.

These are described here at a conceptual level. Implementation specifics — workflow logic, internal data contracts, and orchestration details — are intentionally out of scope for this repository.

## Architecture, at a Glance

TorBot is built as an automation-first system: a conversational front end (WhatsApp) talks to an orchestration layer that manages booking state, availability, and tenant isolation, with a lightweight dashboard giving businesses visibility into their own data.

A full architecture walkthrough — including the high-level component map and how multi-tenancy is handled — lives in `docs/architecture-overview.md`.

## Booking Flow

At a high level, a booking moves through: conversation start → intent recognition → availability check → slot hold → confirmation → calendar sync. Edge cases like conflicting requests, cancellations, and waitlisting are handled as variations of this same flow.

A simplified walkthrough is documented in `docs/booking-flow.md`.

## Technology

TorBot is built on a workflow-automation backend integrated with messaging and calendar services, with a lightweight dashboard for business visibility. Specific technology choices are documented separately in `docs/technology-stack.md`.

## Why This Repository Exists

This showcase exists to demonstrate engineering judgment, not to hand over a working clone. Every asset here — diagrams, flow descriptions, screenshots — has been deliberately reviewed and sanitized so the engineering story is clear while the production system stays protected.

If you're a recruiter, engineering manager, or technical peer evaluating this work, the goal is that within a few minutes you understand what was built, how it's structured, and why the decisions behind it hold up — without learning anything that could be used to reconstruct the production system.

## Explore Further

| Doc | What it covers |
|---|---|
| `docs/product-overview.md` | What TorBot does and who it's for |
| `docs/architecture-overview.md` | System components and how they fit together |
| `docs/booking-flow.md` | The booking lifecycle, simplified |
| `docs/technology-stack.md` | What TorBot is built with |
| `docs/engineering-decisions.md` | Notable trade-offs and why they were made |
| `docs/lessons-learned.md` | What changed during the build |

*(Some of the above are planned but not yet published in this repository — see the project roadmap.)*

## How to Navigate This Repository

New here? Read in this order: start with this README for the overview, then `docs/product-overview.md` for the product story, `docs/architecture-overview.md` for system structure, `docs/booking-flow.md` for the core user journey, and `docs/technology-stack.md` for what it's built with. `docs/engineering-decisions.md` and `docs/lessons-learned.md` are optional deeper reading.

## What's Intentionally Not Here

In line with this project's sanitization rules, this repository does not include and will never include: workflow exports, internal automation logic, API payloads, credentials or secrets, internal record identifiers, production URLs, or customer data. See `DISCLAIMER.md` for the full boundary.

---

## Repository Status

**Status:** Engineering Showcase
**Version:** 1.x
**State:** Work in Progress
