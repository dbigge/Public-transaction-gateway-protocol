Transaction Gateway Protocol (TGP-00)

Version: 0.1-draft
Status: Draft
Published: 2025
Organization: Ledger of Earth

⸻

Table of Contents
	•	Abstract
	•	0. Introduction
	•	0.1 Where TGP Runs
	•	0.2 Relationship to x402
	•	0.3 Design Principles
	•	1. Architecture
	•	1.1 Network Topology
	•	1.2 Gateway Functions
	•	1.3 Message Flow
	•	1.4 Settlement Topologies
	•	2. Message Types
	•	2.1 QUERY … 2.7 ERROR
	•	3. State Machine
	•	4. Security Considerations
	•	5. Attribute Registry
	•	6. x402 Integration
	•	7. Example Flows
	•	8. Future Extensions
	•	9. References
	•	10. The 11-Layer Trust Stack (Informative)
	•	11. TGP L8/L9/L10 Info Block (TIB)
	•	12. Policy Expression Language (PEL-0.1)
	•	13. State Summary Objects (SSO)
	•	14. Receipts & TDR Triplet
	•	15. Prover Abstraction & Settlement Middleware (Normative)
	•	Appendix A: Extensible Settlement Mechanisms
	•	Appendix B: Terminology
	•	Appendix C: Revision History
	•	Appendix D: Deprecation Note

⸻

Abstract

(unchanged except final line)

TGP provides:
	•	…
	•	Pluggable settlement middleware (“Provers”) that implement escrow, burn-based, or ZK-based assurance models behind a common abstraction.

TGP-01 defines the optional Economic Envelope extension.

⸻

0. Introduction

(same as prior draft, plus bullet 10)
	10.	Pluggable settlement logic: Settlement and assurance models (escrow, burn, ZK) are implemented in Prover middleware; TGP standardizes how they are selected and bound to paths, not their internal mechanics.

⸻

1. Architecture

1.1 Network Topology

┌─────────────┐         ┌─────────────┐         ┌─────────────┐
│  Domain A   │◄───────►│  Gateway 1  │◄───────►│  Gateway 2  │
│ (Client)   │  mTLS   │ (Boundary)  │  mTLS   │ (Boundary)  │
└─────────────┘         └─────────────┘         └─────────────┘
│                       │
│ TGP Peering           │
▼                       ▼
┌─────────────┐         ┌─────────────┐
│ Domain B   │◄───────►│ Domain C   │
│ (Provider) │  mTLS   │ (Provider) │
└─────────────┘         └─────────────┘

Settlement may occur in either of two planes:
	1.	Direct HTLC /on-ledger locks (original model)
	2.	Gateway + Prover middleware, where gateways invoke on-chain or off-chain Provers (§15) that implement escrow, single-sided escrow, proof-of-burn, or ZK attestation.

         ┌───────────────────────────── TGP / x402 Control Plane ─────────────────────────────┐
┌─────────────┐   ┌─────────────┐                     ┌─────────────┐   ┌─────────────┐
│ Client/Agent│◄─►│ Gateway A  │◄───────────────────►│ Gateway B  │◄─►│ Provider   │
└─────────────┘   └─────────────┘                     └─────────────┘  └─────────────┘
                       │                                               │
                       ▼                                               ▼
                ┌───────────┐                                       ┌───────────┐
                │ Prover A  │                                      │ Prover B  │
                │ (escrow/  │                                      │ (burn/    │
                │ burn/zk)  │                                      │ zk)       │
                └───────────┘                                      └───────────┘

1.2 Gateway Functions
	•	Settlement management through HTLCs or Provers
	•	Prover orchestration and capability matching
	•	Policy enforcement (L10)
	•	Message routing between peers
	•	Identity mediation (L9)
	•	State bounding (L8)
	•	Economic Envelope handling (TGP-01)
	•	TDR logging including Prover handles

1.3 Message Flow

(standard TGP flow diagram retained — then add)

1.3.1 Prover-Mediated Sub-Flow

(1) Client → Gateway A: TGP QUERY/SELECT with prover_id/profile  
(2) Gateway A → Prover A: openPosition(params)  
(3) Gateways A↔B: normal TGP LOCKED/PROOF/SETTLE, referencing ProverID and handle  
(4) Gateway B → Prover B (optional): open/close mirrors  
(5) Gateways closePosition on settlement or refund.

The original HTLC-only design remains valid; the Prover layer adds structured escrow, single-sided escrow, or reputation models.

1.4 Settlement Topologies

1.4.1 Direct HTLC Settlement (Original Model)
	•	Atomic hash-timelock contracts on ledger(s)
	•	No external Prover
	•	Simple, channel-style flows

1.4.2 Gateway + Prover (CoreProver/Escrow Model)
	•	Gateways invoke Provers (openPosition/closePosition)
	•	Supports single-sided escrow, legal commitments, and optional fulfillment
	•	Extensible to proof-of-burn and ZK policies
	•	The CoreProver architecture (EscrowCommitmentProverV0) is the reference implementation of this topology (see Appendix E: CoreProver Reference Profile).

⸻

(Sections 2 – 14 remain as previous version, unchanged except attributes already referencing prover_id etc.)

⸻

15. Prover Abstraction & Settlement Middleware — Normative

(full section exactly as previously printed, unchanged)

⸻

Appendix A – Extensible Settlement Mechanisms

(includes bullet “Prover-mediated escrow and reputation models (see §15)”).

⸻

Appendix E – CoreProver Reference Profile (Informative Placeholder)

(to be defined next — will document EscrowCommitmentProverV0 including PreAuth, Commitment, and Fulfillment flows.)

⸻

Appendix C – Revision History

Version	Date	Changes
0.1-draft	2025-11	Added Prover abstraction, CoreProver topology, and updated Architecture & Message Flow to reflect Gateway + Prover design.