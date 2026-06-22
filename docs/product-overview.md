# TorBot — Product Overview

## 1. Product Summary

TorBot is a multi-tenant appointment booking platform that lets customers schedule, reschedule, and cancel appointments entirely through WhatsApp conversation. It's built for service businesses that depend on bookings — and whose customers already live in WhatsApp.

Rather than asking customers to download an app, fill out a web form, or call during business hours, TorBot meets them in the channel they already use, while giving the business a single dashboard to manage everything happening across their customers, staff, and calendar.

## 2. Target Users

TorBot serves two distinct audiences:

**Business owners and staff** — small and mid-sized service businesses (salons, clinics, studios, and similar appointment-based operations) who need to manage bookings, availability, and customers without operating complex software.

**End customers** — the people booking appointments, who interact with the business exclusively through WhatsApp and expect a fast, conversational experience rather than a form-filling one.

TorBot is multi-tenant: a single platform instance serves many independent businesses, each with its own isolated customers, staff, and calendar.

## 3. Business Problems

Service businesses lose revenue and time to booking friction that most scheduling tools don't actually solve:

- **Missed bookings from channel mismatch.** Customers want to book where they already communicate. If that channel isn't supported, the business loses the booking to a competitor or to no-shows from forgotten phone calls.
- **Double-booking and availability errors.** Manual or loosely-integrated calendars create conflicts that erode customer trust.
- **No visibility across customers.** Without a central dashboard, staff can't see who's booked, who's waiting, or what's happening across the business at a glance.
- **Lost demand when slots are full.** Without a waitlist, a fully booked calendar simply turns customers away instead of capturing that demand for later.

TorBot is built to remove these specific points of friction, not to be a general-purpose scheduling tool.

## 4. Core Capabilities

- **WhatsApp-native booking** — customers book, modify, and cancel appointments through natural conversation, with no app to install.
- **Multi-tenant architecture** — each business operates with isolated customers, staff, and calendar data — enforced per request — while running on shared infrastructure.
- **Real-time availability** — every booking request is checked against live calendar state before being confirmed, which is designed to prevent double-booking.
- **Business dashboard** — owners and staff get a single view of bookings, availability, and activity without needing to understand the automation behind it.
- **Waitlist handling** — when a desired slot isn't available, customers can be queued and notified automatically if one opens up.
- **Calendar synchronization** — appointment state is kept consistent with the business's actual calendar.

## 5. Typical User Journey

A customer messages the business's WhatsApp number to book an appointment. TorBot understands the request, checks real-time availability, and either confirms a slot or offers alternatives — including joining a waitlist if nothing is currently open. Once confirmed, the appointment is reflected on the business's calendar and visible to staff on the dashboard. If the customer needs to reschedule or cancel later, the same WhatsApp conversation handles it, with availability re-checked automatically.

Throughout, the business owner never has to manually reconcile messages, calendar entries, and customer records — TorBot keeps them in sync.

## 6. Business Value

- **Lower booking friction** translates directly into fewer missed or abandoned bookings.
- **Centralized visibility** means staff spend less time reconciling double bookings or hunting for customer history across channels.
- **Captured demand** through waitlisting turns "fully booked" from a dead end into a pipeline.
- **Multi-tenant design** means the same platform scales across many businesses without each one needing separate infrastructure.

## 7. Scope & Boundaries

TorBot is purpose-built for appointment-based service businesses with a conversational, WhatsApp-first booking experience. It is not a general calendar tool, a CRM, or a marketing platform — its scope is the booking lifecycle: discovery, scheduling, confirmation, and follow-through, with the supporting visibility a business needs to operate that lifecycle.

This document describes TorBot as a product. It does not describe how TorBot is built — that's covered separately in the architecture and technology documentation.

## 8. What's Next

To understand how TorBot is structured technically, continue to `architecture-overview.md` and `technology-stack.md`. To see the booking lifecycle in more detail, see `booking-flow.md`.
