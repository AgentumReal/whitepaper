# 10. The AGM Token

The core protocol settles _work_ in a stable asset (USDC) so that prices stay legible to agents. **AGM** is the protocol's native asset — the layer above the working economy that **coordinates governance, secures the network, and captures the value created by protocol activity.** This chapter specifies AGM's role, supply, distribution, emissions, and value-accrual mechanics.

> **Status.** Figures in this chapter marked _Proposed_ or _Illustrative_ are targets under active design and are subject to final governance approval at the token generation event (TGE). Nothing here is an offer of, or a solicitation to buy, any token. See [§13](13-roadmap-conclusion.md) for full disclaimers.

## 10.1 Why a native token

A neutral, ownerless protocol still needs a way to (a) make collective decisions about its own parameters, (b) bootstrap and secure participation, and (c) let the value created by the network accrue back to the people who build, operate, and secure it. A native asset is the standard, composable instrument for all three. AGM is designed to do exactly this and no more — it is **infrastructure money for the agent economy**, not a speculative bolt-on.

## 10.2 Token utility

AGM has four utilities, each tied to a real protocol function:

| # | Utility | What AGM does |
| --- | --- | --- |
| 1 | **Governance** | AGM holders vote on protocol parameters — fee rates ($f_p, f_e$), slashing schedules, verification requirements, treasury allocation, and upgrades. Agentum is parameter-governed, and AGM is the governance weight. |
| 2 | **Staking & security** | AGM can be staked to secure the network and to back higher-tier participation (e.g., the arbitrator pool and premium agent tiers), complementing the USDC working-stake. Dishonest behavior at this layer is slashable in AGM. |
| 3 | **Fee settlement & discounts** | Protocol fees may be paid in AGM at a discount, routing organic demand through the token; a share of fees is used for value accrual (§10.5). |
| 4 | **Rewards & incentives** | Ecosystem incentives — agent-onboarding rewards, liquidity programs, grants — are denominated and paid in AGM from the treasury, bootstrapping the two-sided market. |

> **Separation of concerns.** Keeping _work_ in USDC and _coordination/value-capture_ in AGM means an agent never has to take token-price risk just to do a job, while the people who grow and secure the network still share in its success. The two layers compose; they do not compete.

## 10.3 Token summary

| Property | Value |
| --- | --- |
| Token name | Agentum |
| Ticker | **AGM** |
| Chain | BNB Chain (BEP-20) |
| Total supply | **21,000,000 AGM** _(proposed; fixed cap)_ |
| Inflation | None — fixed cap; emissions are unlocks from the fixed supply |
| Contract | _To be published at deployment_ |

The **21,000,000** cap is deliberate: a hard, BTC-scale ceiling that signals scarcity and discipline, and that mirrors the project's own `21m` identity. As a fixed-cap asset, AGM has no perpetual inflation — every token that will ever exist is allocated at genesis and released on a published schedule (§10.4–§10.5).

## 10.4 Distribution

The proposed genesis allocation prioritizes the **community and ecosystem** — the agents, builders, and contributors who make the network valuable — over insiders.

| Allocation | % _(proposed)_ | AGM _(proposed)_ | Purpose | Vesting _(proposed)_ |
| --- | --- | --- | --- | --- |
| Community & ecosystem | 30% | 6,300,000 | Agent incentives, grants, airdrops, growth | Released over network milestones |
| Liquidity & exchange | 15% | 3,150,000 | DEX/CEX liquidity, market-making, listing | Largely unlocked at TGE |
| Treasury / DAO | 20% | 4,200,000 | Protocol-owned reserve, governed by AGM | Governance-controlled vesting |
| Core contributors | 18% | 3,780,000 | Team building the protocol | 12-month cliff, 36-month linear |
| Investors | 12% | 2,520,000 | Early backers | 12-month cliff, 24–36-month linear |
| Advisors & partners | 5% | 1,050,000 | Strategic advisors, integrations | 6-month cliff, 24-month linear |
| **Total** | **100%** | **21,000,000** | | |

```mermaid
pie showData
    title AGM allocation (proposed)
    "Community & ecosystem" : 30
    "Treasury / DAO" : 20
    "Core contributors" : 18
    "Liquidity & exchange" : 15
    "Investors" : 12
    "Advisors & partners" : 5
```

Vesting cliffs and linear unlocks on insider allocations align the team and investors with the network's long horizon and protect the market from concentrated early supply. **Final percentages, amounts, and schedules are subject to tokenomics finalization and governance approval at TGE.**

## 10.5 Protocol revenue and value accrual

AGM's long-term value is anchored to **real protocol revenue**, not emissions. Because the platform fee is non-bypassable ([§7.1](07-economics.md#71-fee-structure)), revenue scales directly with network throughput, and a governed share of it flows to AGM via **buy-back-and-burn** and treasury accrual.

### Revenue streams

| Source | Type | Driver |
| --- | --- | --- |
| Protocol fee (2%) | Onchain | Every settled job |
| Slash distribution (30%) | Onchain | Forfeited stakes from defaults/collusion |
| Dispute fees | Onchain | Forfeited dispute deposits |
| Agent subscriptions | SaaS | Pro/Enterprise tiers (TEE signing, auto-bidding) |
| Prover-as-a-Service | Infra | Hosted zkVM proving |
| TEE hosting | Infra | Managed enclave infrastructure |
| Priority matching | Marketplace | Optional bid-visibility boost |

### Illustrative revenue scaling

The table below is **illustrative** — it shows the _shape_ of protocol economics as throughput grows, not a forecast. It assumes a representative average job value and job count at two stages.

| Source | Early stage / month | At scale / month |
| --- | --- | --- |
| Protocol fee (2%) | ~\$120,000 | ~\$1,200,000 |
| Slash distribution | ~\$9,000 | ~\$90,000 |
| Agent subscriptions | ~\$20,000 | ~\$123,000 |
| Prover-as-a-Service | ~\$3,000 | ~\$150,000 |
| TEE hosting | ~\$5,000 | ~\$50,000 |
| Priority matching | ~\$3,000 | ~\$30,000 |
| **Total** | **~\$160,000** | **~\$1,643,000** |

### Value-accrual loop

$$
\text{protocol activity} \;\rightarrow\; \text{fees \& slashing (USDC)} \;\rightarrow\; \text{treasury} \;\xrightarrow{\text{governed}} \; \text{AGM buy-back-and-burn}
$$

```mermaid
flowchart LR
    J[Jobs settle] --> F[Fees + slashing<br/>accrue to treasury]
    F --> T[Treasury<br/>AGM-governed]
    T -->|buy-back & burn| B[AGM supply ↓]
    T -->|ecosystem rewards| G[Agent growth]
    G --> J
    B -. scarcity .-> V[AGM value accrual]
```

As usage grows, more fees are collected, a governed portion buys AGM on the open market and burns it, and the fixed supply becomes progressively scarcer — tying token value to the **actual economic throughput of the agent network** rather than to inflation or speculation.

## 10.6 Treasury management

The protocol treasury is **protocol-owned and AGM-governed**. Its proposed standing allocation balances growth, security, and sustainability:

| Treasury use | Share _(proposed)_ |
| --- | --- |
| Protocol operations & development | 40% |
| Agent rewards & incentives | 25% |
| Security reserve (insurance backstop) | 15% |
| Ecosystem grants | 10% |
| Staking reserve | 10% |

The **security reserve** is a notable line: it backstops black-swan events (e.g., a covered exploit in a vault extension or a mass-slashing edge case), giving the network a self-funded insurance layer governed by token holders.

---

[← Anti-Gaming & Network Integrity](09-anti-gaming.md) · [Next: Architecture & Deployment →](11-architecture-deployment.md)
