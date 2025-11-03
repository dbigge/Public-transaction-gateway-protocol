# Transaction Gateway Protocol (TGP)

**Status:** Draft Specification – v0.1  
**Maintainer:** [Ledger of Earth](https://github.com/LedgerOfEarth)  
**Linked PR:** [coinbase/x402#593](https://github.com/coinbase/x402/pulls)  
**License:** MIT

---

## Overview

This repository hosts the **proof-of-concept (PoC)** and reference materials for the **Transaction Gateway Protocol (TGP)** — a proposed extension to [x402](https://github.com/coinbase/x402) that enables value routing, policy negotiation, and atomic settlement across **Transaction Areas (TAs)**.

TGP aims to provide an **application-layer equivalent of BGP** for autonomous transaction domains, allowing secure coordination and pricing of value paths across different policy zones while using x402 as the signaling substrate.

---

## Purpose and Scope

This repository is intended **for demonstration and discussion only.**  
It serves as a working reference for reviewers evaluating the [TGP-00 specification draft](./specs/TGP-00.md).

It is **not production code**, and no guarantees of security, correctness, or backward compatibility are implied.

---

## Contents

- `specs/TGP-00.md` – Draft specification  
- `examples/` – Demonstration scripts and message flow examples  
- `schemas/` – JSON and TypeScript schemas for protocol metadata  
- `docs/` – Supplementary reference notes  

---

## Usage

The PoC demonstrates how a Transaction Gateway might:
1. Advertise its policy and transaction capabilities to peers  
2. Negotiate cost, risk, and compliance metadata  
3. Execute a single-hop payment using x402 signaling  
4. Generate transaction-data-records (TDRs) for later audit  

For full context, see the TGP pull request to the [x402 project](https://github.com/coinbase/x402).

---

## Disclaimer

This repository is part of the **Ledger of Earth** research initiative exploring blockchain-based transaction control planes for autonomous agents and telecom-grade systems.

> **Important:**  
> This is a **conceptual prototype** released for peer review.  
> It is *not audited, production-ready, or intended for commercial deployment.*

---

## Citation / Reference

When referencing this repository, please cite as:

> Bigge, D. (2025). *Transaction Gateway Protocol (TGP-00): Draft Specification and Proof of Concept.* Ledger of Earth.  
> https://github.com/LedgerOfEarth/transaction-gateway-protocol

