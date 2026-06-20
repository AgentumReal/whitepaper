# 12. Security & Threat Model

A protocol that custodies value and renders automated judgment must be honest about its attack surface. This chapter states what Agentum defends against, how, and — importantly — where the **residual trust assumptions and limitations** lie. Security is treated as a property of the whole system: cryptography, economics, and operations together.

## 12.1 Smart-contract security

The contracts are the foundation; a bug there can bypass every economic safeguard above it.

* **Audits & monitoring.** Full third-party audit (CertiK) before mainnet, with continuous post-deployment monitoring and a bug-bounty program ([§11.4](11-architecture-deployment.md#114-audit--security-operations)).
* **Minimal surface.** Simple, modular contracts with no exotic mechanisms reduce the space of possible bugs.
* **Upgrade discipline.** UUPS upgradeability behind a timelock and AGM governance; user-protective paths (e.g., escrow refunds) designed to remain non-blockable by hooks or upgrades.
* **Isolation.** Verification adapters are separated from settlement so a verifier flaw cannot directly drain escrow.

## 12.2 TEE limitations

TEE (L1, and the hardware half of L3) is powerful but **not unconditionally trustworthy**, and the protocol treats it accordingly.

* **Vendor trust.** A TEE attestation is only as sound as the chip vendor (Intel, AMD, AWS). Using TEE means trusting that hardware root of trust.
* **Side channels.** Known side-channel attacks exist against SGX and similar enclaves. An attacker with deep hardware access may, in principle, extract or influence enclave state.
* **Mitigation.** **TEE is never the sole trust anchor for high-value work.** Such jobs use L2 (zkVM, trustless) or L3 (TEE + zkVM defense-in-depth), so that defeating verification requires breaking _mathematics_ in addition to hardware. The verification-level incentives ([§6.1](06-verification.md#61-verification-levels-l0l3)) steer high-value jobs toward these tiers.

## 12.3 zkVM limitations

zkVM (L2, and the proof half of L3) provides the strongest guarantee in the system, but has its own boundaries.

* **Scope.** A zkVM proof certifies that _a deterministic program ran and returned a result_ — it cannot, by itself, judge inherently subjective quality. That is why semantic work routes through TEE/human rubrics ([§6.5](06-verification.md#65-semantic-verification-framework)).
* **Performance cost.** Proving time scales with program complexity (seconds to minutes); complex checks carry real proving cost. The protocol exposes this as a market (Prover-as-a-Service) rather than hiding it.
* **Cryptographic assumptions.** Groth16 soundness rests on standard cryptographic assumptions. A sufficiently capable quantum adversary could threaten current SNARKs; the architecture anticipates migration to post-quantum proof systems (e.g., STARKs) as they mature.

## 12.4 Economic attacks

Beyond code and cryptography, an adversary may attack the _incentives_. The major economic attacks and their mitigations:

| Attack | Description | Mitigation |
| --- | --- | --- |
| **Sybil** | Many cheap identities to farm reputation or escape slashing | Min deposit + reputation-scaled staking (new identity = 2× lock) ([§9.1](09-anti-gaming.md#91-sybil-resistance)) |
| **Collusion** (Provider–Evaluator, Client–Provider) | Parties cooperate to extract value | Statistical detection + protocol-initiated disputes + 100% slash & ban ([§9.2](09-anti-gaming.md#92-collusion-detection), [§9.4](09-anti-gaming.md#94-evaluator-accountability)) |
| **Griefing** | Wealthy actor burns its own stake to harm a target | Progressive slashing + pattern detection + bounded blast radius |
| **Arbitration capture** | Pack a dispute panel with confederates | VRF random selection + reputation gate + diversity + minimum pool size ([§8.2](08-dispute-resolution.md#82-arbitrator-selection)) |
| **Work theft** | Client uses an always-fail strategy to get work for free | Pre-bid inspection + Client slashing on malicious strategy ([§9.3](09-anti-gaming.md#93-verification-strategy-integrity)) |
| **Evaluation gaming** | Rubber-stamp, borderline-cluster, or harass | Nine-trigger monitoring + shadow scoring + overturn slashing ([§9.4.2](09-anti-gaming.md#942-layer-2--detection)) |
| **Frivolous disputes** | Spam appeals to grief Evaluators | Scaled dispute deposits + deposit forfeiture on loss ([§8.6](08-dispute-resolution.md#86-dispute-cost-scaling)) |

## 12.5 Residual trust — the honest bottom line

Agentum **minimizes** trust; it does not pretend to eliminate it. The irreducible assumptions are, in order of robustness:

1. **Mathematics** — zkVM proof systems are sound (the strongest anchor; used for trustless L2).
2. **Decentralized consensus** — BNB Chain validators are honest and live.
3. **Audited code** — the contracts faithfully implement this specification.
4. **Attested hardware** — _only at L1/L3_, that TEE vendors' enclaves are sound — and never as the sole anchor for high value.

Notably, participants do **not** need to trust each other, any Evaluator's good faith, or any central operator. Where trust is unavoidable, it is placed in the most robust available anchor and layered (defense-in-depth) so that no single failure compromises the system. This honest accounting of the trust surface is itself a security property: builders and operators can make informed decisions about which verification level a given task warrants.

---

[← Architecture & Deployment](11-architecture-deployment.md) · [Next: Roadmap & Conclusion →](13-roadmap-conclusion.md)
