# TorBot — Security and Sanitization

## 1. Purpose

This document describes *how* the public material in this repository is sanitized — the practical process and techniques used to keep it safe to share. It is the operational companion to two related documents: [`DISCLAIMER.md`](../DISCLAIMER.md) states at a high level what is included and excluded, and [`repository-philosophy.md`](./repository-philosophy.md) explains the reasoning behind that boundary. This document focuses on the method, and deliberately does not restate the other two.

## 2. The Test Applied to Every Item

Each piece of content is checked against a single question: *could this be used to reconstruct the system, or could it expose data?* If the answer is yes to either, it does not go in. The intent is to make engineering judgment visible while keeping the repository free of anything operationally sensitive. When a piece of content sits near the line, the more conservative choice is taken.

## 3. How Content Is Sanitized

Rather than copying production material and editing it down, the public documentation is written at the conceptual level from the start. Four techniques do most of the work:

- **Generalization.** Technologies are named where that aids understanding (for example, the messaging channel or the orchestration platform), but their configuration, settings, and tuning are not.
- **Abstraction.** Behavior and reasoning are described — what a step accomplishes and why — without the mechanics that would let it be reproduced.
- **Omission.** Some categories are simply left out entirely rather than abstracted, including credentials, customer and tenant data, and internal contracts.
- **Conceptual examples only.** Diagrams and walkthroughs are illustrative models of the design, not exports or traces drawn from the running system.

## 4. What This Is Designed to Protect

The sanitization process is designed with two goals in mind: protecting the privacy of any business or customer that uses the system, and avoiding a blueprint that would make the production system easier to reconstruct or attack. The detailed reasoning for why these matter lives in [`repository-philosophy.md`](./repository-philosophy.md) and is not repeated here.

## 5. Verifying the Boundary

The boundary is maintained by review rather than assumed. New documentation is read back against the test in section 2 before publication, with attention to incidental detail — an offhand identifier, a real value in an example, a diagram that reveals more than intended. Where a judgment call is close, content is removed or generalized rather than kept. No repository can claim to be perfectly sanitized, so the working assumption is conservative by default: when in doubt, leave it out.

## 6. A Note on Sensitive Material

This repository is intended to contain nothing operationally exploitable: no credentials, secrets, production endpoints, or live configuration. If you believe something sensitive has been included inadvertently, the appropriate response is to flag it privately so it can be reviewed and removed, rather than to build on it.

## 7. What Is Intentionally Not Documented

Consistent with its own subject, this document does not include the specific items that were removed, the internal review checklist in detail, or any example of sanitized-out content. It describes the approach to sanitization, not the material it excludes.
