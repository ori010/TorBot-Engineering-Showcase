# TorBot — Repository Philosophy

## 1. Purpose

This repository is a public engineering showcase. Its purpose is to demonstrate how TorBot was designed and reasoned about — not to hand over a working copy of the production system. This document explains the thinking behind that boundary.

## 2. The Core Principle

Everything here is guided by one principle: **show the engineering judgment without enabling reconstruction.** A reader should come away understanding what was built, how it is structured, and why the decisions hold up — without learning anything that could be used to rebuild the system or reach its data.

## 3. What Is Included, and Why

- **Concepts and architecture** — so the system's structure and reasoning are clear.
- **Decisions and trade-offs** — so the judgment behind the system is visible.
- **Business and product context** — so the work is understandable on its own terms.

These are the parts that demonstrate engineering thinking, and they carry no reconstruction or privacy risk.

## 4. What Is Excluded, and Why

Production workflows, internal data contracts, schemas, identifiers, payloads, credentials, customer or tenant data, and infrastructure or deployment details are intentionally absent. These either expose how to rebuild the system or risk customer privacy, and neither is necessary to understand the engineering.

## 5. How the Boundary Is Decided

The test for any piece of content is simple: *does this reveal how to reconstruct the system, or expose data?* If yes, it stays out. If it explains reasoning without doing either, it can be included. When in doubt, the more conservative choice wins.

## 6. Relationship to the Disclaimer

The high-level statement of what is and isn't included lives in [`DISCLAIMER.md`](../DISCLAIMER.md). The detailed sanitization approach is covered separately in [`security-and-sanitization.md`](./security-and-sanitization.md). This document explains the *philosophy* behind the boundary; those describe the boundary itself — they are kept separate to avoid duplication.

## 7. How to Read This Repository

Start with the [README](../README.md), which links the published documentation in a suggested reading order. Each document stays at the conceptual level described here.

## 8. What Is Intentionally Not Documented

Consistent with its own principle, this document does not restate the detailed exclusion list or the sanitization procedure; it explains why the boundary exists and how it is drawn.
