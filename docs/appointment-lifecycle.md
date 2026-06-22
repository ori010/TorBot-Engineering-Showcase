# TorBot — Appointment Lifecycle

## 1. Lifecycle Philosophy

An appointment is TorBot's core unit of value: everything else in the system exists to bring one into existence reliably and keep it accurate until it's fulfilled. The lifecycle is designed so that, at every stage, both the business and the customer can trust what the system is telling them — a confirmed slot stays confirmed, a cancellation is reflected everywhere immediately, and nothing is promised that hasn't actually been checked.

## 2. Lifecycle Overview

An appointment moves through five core stages — Request, Availability Verification, Reservation, Confirmation, and Calendar Synchronization — with two additional paths for changes (Reschedule, Cancellation) and one for unmet demand (Waitlist). Every stage exists to protect the same guarantee: what the customer is told matches what the business's calendar actually reflects.

## 3. Appointment Request

The lifecycle begins when a customer expresses intent to book — typically a time, a service, or a general request to schedule — through a WhatsApp conversation. At this point, nothing is yet promised to the customer; the request simply initiates the process of finding a slot that works.

## 4. Availability Verification

Before anything is offered as confirmed, the requested time is checked against the business's real, current availability. This step exists specifically so that a customer is never told "yes" to a slot that's already taken — availability is verified before an appointment is confirmed, not after.

## 5. Reservation

Once a suitable slot is identified, it is held for the customer during the brief window needed to complete the booking. This reservation step prevents two customers from being offered the same slot at the same moment, which matters most when multiple conversations are happening at once.

## 6. Confirmation

When the customer accepts the held slot, the appointment becomes confirmed. From this point, both the customer and the business can rely on the booking as settled — the customer receives confirmation in the same WhatsApp conversation, and the business gains a finalized entry it can plan around.

## 7. Calendar Synchronization

Immediately after confirmation, the appointment is reflected in the business's calendar, so staff see the same accurate picture the customer was just given. This synchronization is what keeps the conversation and the calendar from ever telling two different stories.

## 8. Lifecycle Changes

**Reschedule** — A customer can request a new time for an existing appointment through the same conversation. The new time goes through the same availability verification as a fresh request before the change is accepted, so a reschedule can never silently create a conflict.

**Cancellation** — A customer can cancel directly within the conversation. Once cancelled, the slot is released back into availability immediately, so it can be offered to the next customer rather than sitting unused.

**Waitlist** — If no slot is available at the time of request, the customer can be added to a waitlist for that opening instead of being turned away. If a matching slot later becomes available — for example, through a cancellation — the waitlisted customer is notified and can claim it, following the same verification and confirmation steps as any other booking.

## 9. Completion

An appointment reaches completion when the scheduled time has passed and the service has taken place. At this point the appointment's role in the active lifecycle ends; it becomes part of the business's history rather than something still being tracked toward fulfillment.

## 10. Lifecycle Principles

- **Nothing is confirmed without verification.** Every path to a confirmed appointment passes through an availability check first.
- **State changes propagate immediately.** Cancellations free up availability right away; confirmations sync to the calendar right away. The system does not allow the conversation and the calendar to drift apart.
- **Unmet demand is captured, not discarded.** A fully booked slot results in a waitlist offer, not a dead end.
- **The customer never needs to leave the conversation.** Every lifecycle change — request, reschedule, cancellation — happens in the same channel the appointment was created in.

## 11. What Is Intentionally Not Documented

This document describes the appointment lifecycle as a business process. It does not describe the internal state machine, workflow implementation, data contracts, algorithms, or system internals that enforce this behavior — those belong to the production system and are not published as part of this showcase.
