# Managing State in an Asynchronous Conversation

## Problem

A booking is rarely a single message. It unfolds across a back-and-forth — a request, a clarifying question, a choice between options, a confirmation. WhatsApp delivers these as independent, asynchronous events with no assumption of timing or order, and the person on the other end is free to go quiet for an hour, change their mind, answer a different question than the one asked, or start over. A system that handles each message in isolation loses the thread: it forgets what it just offered, asks the same question twice, or treats an unrelated reply as an answer. The difficulty is that the "conversation" is a single coherent thing in the user's mind but only a stream of disconnected events to the system.

## Constraints

- **Asynchronous, unordered messages.** No assumption of prompt or in-order replies.
- **Human unpredictability.** Interruptions, topic switches, and abandonment are normal, not rare.
- **Multi-tenant.** Conversation handling has to stay scoped to the right business.
- **Stateless transport.** The messaging channel carries messages, not memory.

## Engineering Approach

The decision was to make conversation state explicit and keep it separate from booking logic. Alternatives considered:

- **Stateless handling** (derive everything from the latest message) — cannot represent "we are halfway through choosing a time," so it produces repetition and dead-ends.
- **Folding state into the booking logic** — mixing "where we are in the conversation" with "what a valid booking is" makes both harder to change and to reason about.

Instead, each conversation carries an explicit notion of where it is in the flow, so an incoming message is interpreted in context rather than from scratch. Because that state is separated from the booking rules, the messaging experience and the booking logic can evolve independently — a separation that also shows up at the architecture level.

## Trade-offs

- Explicit state is bookkeeping that must be created, advanced, and eventually retired.
- Designing for resumption and re-entry is more work than scripting a happy path.
- Conversation state and booking state must be kept distinct without drifting apart.

In exchange, conversations recover gracefully: an interrupted or out-of-order exchange can pick up where it left off instead of collapsing.

## Outcome

Conversations behave like conversations. Context survives pauses and detours, the system stops repeating itself, and a customer can resume a booking rather than restart it.

## Engineering Principle

**Model the implicit unit explicitly.** When users perceive a coherent process that the transport represents only as scattered events, making that process a first-class piece of state — and isolating it from domain rules — is what turns brittle handling into reliable behavior.

## What Is Intentionally Not Documented

This case study does not include the state representation, identifiers, timeouts, message contracts, or any workflow implementation. It explains the reasoning, not how the state is stored or encoded.
