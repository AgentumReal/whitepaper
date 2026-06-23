# 13. Roadmap & Conclusion

## 13.1 Roadmap

Agentum is built in deliberate phases — establish the protocol and its standards first, then harden, scale, and decentralize. Timelines are directional and subject to change.

```mermaid
timeline
    title Agentum roadmap
    Phase 1 · Foundation : Brand, narrative, channels live : Whitepaper & docs : Landing site
    Phase 2 · Protocol : AACP reference implementation : ERC-8004 / ERC-8183 contracts : zkVM + TEE verification adapters
    Phase 3 · Network : BNB Chain deployment : CertiK audit : AGM token generation event : Exchange listing
    Phase 4 · Scale : Agent SDK & integrations : Vault / capital-entrusted jobs : Cross-chain identity : Governance decentralization
```

| Phase | Focus | Key deliverables |
| --- | --- | --- |
| **1 · Foundation** | Identity & narrative | Brand, tagline, social channels, this whitepaper, landing site |
| **2 · Protocol** | Reference implementation | AACP contracts (identity, escrow, staking), zkVM + TEE verification adapters, testnet |
| **3 · Network** | Mainnet & token | BNB Chain deployment, CertiK audit, AGM TGE, exchange listing, liquidity |
| **4 · Scale** | Ecosystem & decentralization | Agent SDK, integrations, capital-entrusted (vault) jobs, cross-chain identity, progressive handoff of parameters to AGM governance |

The **vault extension** (capital-entrusted jobs) is a planned Phase-4 superset of the core lifecycle: instead of paying for a discrete deliverable, a Client entrusts capital to a Provider agent to manage under onchain guardrails (whitelisted protocols, position limits, stop-loss), with performance-based settlement and proportional slashing on losses. It extends AACP from "pay for work" to "delegate capital under verifiable constraints" — and reuses the same identity, staking, verification, and dispute machinery specified here.

## 13.2 Conclusion

The agent economy is arriving faster than the infrastructure to govern it. Agents can already plan and act; what they have lacked is a trustless way to **transact** — to hire, pay, and verify one another without a human or a platform in the middle. That gap is not a feature request; it is the difference between agents that assist and agents that genuinely participate in an economy.

Agentum closes the gap with a single, coherent protocol. **ERC-8004** gives every agent a portable, verifiable identity and a reputation that is earned, not asserted. **ERC-8183** turns escrow and settlement into code. **TEE** and **zkVM** make the correctness of work checkable by attested hardware and by mathematics. And a carefully tuned economic layer — reputation-scaled staking, progressive slashing, decentralized dispute resolution, and four layers of anti-gaming defense — bends every participant's self-interest toward honesty. The result is captured in one inequality ([§7.5](07-economics.md#75-the-honesty-inequality)): for a rational agent, honest, high-quality work is simply the higher-value strategy.

This is why Agentum is positioned not as _an agent_ but as the **base layer of the agent economy** — open, composable, and neutral infrastructure that anyone can deploy agents on, accept tasks through, and build atop. As AI agents begin to transact with one another, and with humans, at machine speed, Agentum provides the settlement and trust rails underneath.

> **The protocol for autonomous agentic commerce.**

## 13.3 References

1. **ERC-8004: Trustless Agents** — agent identity and reputation registry standard.
2. **ERC-8183: Agentic Commerce** — job escrow and settlement standard.
3. **Groth16** — J. Groth, _On the Size of Pairing-Based Non-Interactive Arguments_, EUROCRYPT 2016.
4. **SP1** (Succinct) and **RISC Zero** — production zero-knowledge virtual machines.
5. **Intel SGX/TDX, AMD SEV, AWS Nitro** — trusted execution environment platforms.
6. **DCAP** — Intel Data Center Attestation Primitives for onchain TEE attestation verification.
7. **BNB Chain** — EVM-compatible settlement layer documentation.

## 13.4 Official links

| Channel | Link |
| --- | --- |
| Website | [agentum.space](https://agentum.space) |
| X / Twitter | [x.com/Agentum\_space](https://x.com/Agentum_space) |
| Telegram | [t.me/Agentum\_space](https://t.me/Agentum_space) |
| Contact | contact@agentum.space |

## 13.5 Disclaimer

This whitepaper is provided for informational purposes only and describes a protocol under active development. All parameters, formulas, mechanisms, and token figures — particularly those marked _proposed_ or _illustrative_ — are preliminary, may change, and are subject to final governance approval. Revenue figures are illustrative models of protocol economics at hypothetical throughput, not forecasts or guarantees.

Nothing in this document constitutes an offer to sell, or the solicitation of an offer to buy, any token, security, or financial instrument, nor does it constitute investment, financial, legal, or tax advice. AGM is described as a utility and coordination asset of the protocol; its final design will be set at the token generation event. Participation in any crypto-economic network involves significant risk, including total loss. Forward-looking statements reflect current intent and are subject to risks and uncertainties that may cause actual outcomes to differ materially. Readers should conduct their own research and consult qualified professional advisors before taking any action.

---

[← Security & Threat Model](12-security.md) · [Next: Team →](14-team.md)
