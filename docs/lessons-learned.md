# TorBot — Lessons Learned

## 1. Purpose

This document collects the practical lessons that came out of building and operating TorBot. They are written after the fact, with the benefit of hindsight, and each is tied to a decision or case study elsewhere in this repository rather than offered as abstract advice. The goal is to show not just what was built, but what the building taught.

## 2. Lessons

### L1 — Make the expensive failure structurally hard

Not all failures cost the same. A double-booking is far more damaging than a slightly slower booking path, so the design effort went into making that one outcome hard to reach rather than treating every error equally. Verifying availability and holding a slot before confirming means a conflict requires breaking an explicit step, not just losing a timing race. The lesson is to spend the design budget where failure is most expensive. This is the reasoning behind [`engineering-decisions.md` D6](./engineering-decisions.md) and the [booking-consistency case study](./case-studies/booking-consistency.md).

### L2 — Separate the conversation from the domain

Early on it was tempting to let "where we are in the conversation" and "what makes a valid booking" live together. Keeping them separate turned out to matter: the messaging experience and the booking rules change for different reasons and at different rates, and entangling them would have made both harder to reason about. The lesson is that two things that change independently should be allowed to. This shows up in the [conversation-state case study](./case-studies/conversation-state.md) and in how the layers separated over time in [`architecture-evolution.md`](./architecture-evolution.md).

### L3 — Tenant scoping is a discipline, not a feature you add once

Sharing infrastructure across many businesses is cheap to run but unforgiving: scoping is only as strong as its least consistent use. The lesson was to treat tenant context as something carried and checked on every request, not assumed once at the edge and trusted afterward. The cost is constant discipline; the payoff is that isolation does not quietly erode as the system grows. This is the trade-off recorded in [`engineering-decisions.md` D5](./engineering-decisions.md).

### L4 — Treat external services as boundaries, not extensions

The business calendar is the source of truth the system does not own. Designing as if it were an internal, fully controlled component would have produced brittle assumptions the first time an external call was slow or rejected. Treating it as a boundary — reconciling against it rather than assuming ownership — made the integration more honest about what could go wrong. The lesson is to design for the seam between systems, not pretend it isn't there. See [`engineering-decisions.md` D7](./engineering-decisions.md).

### L5 — An unattended system has to report its own health

The most dangerous failures were the quiet ones, where nothing visibly broke but a booking never synced or a message never sent. Waiting for a complaint is waiting for the most expensive possible signal. The lesson was to make health observable in plain language and on a cadence, so problems can surface before a customer hits them. This is the thinking in the [operational-monitoring case study](./case-studies/operational-monitoring.md).

### L6 — Match the tool to the current scale, and know when that changes

Choosing a workflow-automation core and built-in structured storage over a custom backend kept iteration fast and operational overhead low — the right call for the platform's scale. The lesson is twofold: fit the tool to the problem you actually have, and stay honest that the fit is scale-dependent. Some of these choices are worth revisiting as needs grow, which is exactly what the next section is about. See [`engineering-decisions.md` D1, D3, and D4](./engineering-decisions.md).

## 3. Decisions I'd Revisit

A few choices fit the current scale well but are the first ones I would re-examine as the platform grows:

- **Structured storage.** The built-in data layer keeps overhead low, but advanced querying and reporting needs could eventually justify a dedicated database tier.
- **Snapshot-style visibility.** A periodic operational digest is enough today, but a busier platform might warrant moving toward more immediate signals.
- **Single shared deployment.** Per-request tenant scoping on shared infrastructure scales economically, but growth could change the calculus around stronger isolation boundaries.

Naming these is itself a lesson: a good decision is one you can articulate well enough to know when it stops being the right one.

## 4. What Is Intentionally Not Documented

This document does not include implementation details, workflow definitions, data contracts, identifiers, metrics, or any production internals. It records what the work taught, not how the system is built.
