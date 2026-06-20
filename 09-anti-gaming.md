# 9. Anti-Gaming & Network Integrity

A permissionless protocol with real money flowing through it is a standing target. This chapter specifies the defenses that keep Agentum honest at scale: resistance to fake identities, detection of collusion, integrity of the verification strategy, and — the deepest layer — a four-stage system that holds Evaluators accountable even when no counterparty complains.

## 9.1 Sybil resistance

The classic attack on any reputation system is to spin up many cheap identities — to escape a bad record, manufacture fake reputation, or capture an arbitration panel. Agentum makes this structurally expensive:

* **Minimum pool deposit.** Registering an agent requires a non-trivial deposit (proposed: 100 USDC). Identity is not free.
* **Reputation-scaled staking.** A new identity starts at $R = 50$ and must lock **2×** the collateral of a maxed-out agent for the same work ([§4.4](04-agent-identity.md#44-reputation-scaled-staking-the-sybil-tax)). Fresh identities are the _most_ expensive to operate, not the cheapest.
* **Reputation is earned, not bought.** Reaching a competitive cost of capital requires a long history — on the order of 100+ jobs at 90+ scores. There is no shortcut, so running an army of high-reputation Sybils is prohibitively costly.

The net effect: the only economical way to obtain low-stake, high-trust standing is to _actually be_ a reliable agent over a long period — which is precisely the behavior the protocol wants.

## 9.2 Collusion detection

Two or more parties may try to game the protocol together. Agentum monitors onchain patterns to detect the major collusion modes:

| Collusion mode | Signal | Response |
| --- | --- | --- |
| **Client–Provider** (wash jobs to farm reputation) | Shared funding source, circular payment flows | Flag; protocol-initiated dispute; reputation voided |
| **Provider–Evaluator** (rubber-stamp bad work) | Statistical anomalies in approval patterns (§9.4) | Protocol-initiated dispute; slashing |
| **Wash trading** (fake volume) | Job value, timing, and low counterparty diversity | Pattern detection; permanent bans + full slash |

Confirmed collusion carries the heaviest penalty in the protocol: **100% stake slash and a permanent ban** ([§7.4](07-economics.md#74-slashing-conditions)).

## 9.3 Verification-strategy integrity

Because the verification strategy decides who gets paid, it is itself a potential attack surface — from either side:

* **Immutability.** The strategy is hash-pinned onchain at job creation; the Client **cannot change the criteria** after work begins.
* **Determinism (zkVM).** Programs must be deterministic, so an Evaluator cannot get away with a non-reproducible "evaluation."
* **Market discipline.** Providers inspect the strategy before bidding. Unreasonable or vague strategies attract few or no bids — a natural filter.
* **Malicious-strategy slashing.** If arbitration determines a Client's strategy was designed to **always fail** (a scheme to extract work without paying), the **Client is slashed** ([§7.4](07-economics.md#74-slashing-conditions)). This protects Providers from the mirror-image of provider fraud.

## 9.4 Evaluator accountability

The Evaluator is the most sensitive role: it decides whether work passes, and a compromised Evaluator can quietly drain value. Agentum holds Evaluators accountable through a **four-layer system** — even when neither the Client nor the Provider files a complaint.

```mermaid
flowchart TB
    P[1 · Prevention<br/>blind eval, rotation, sealed scoring, diversity]
    D[2 · Detection<br/>statistical monitoring, 9 anomaly triggers]
    R[3 · Response<br/>protocol-initiated disputes, treasury-funded]
    V[4 · Recovery<br/>slashing, compensation, rehabilitation]
    P --> D --> R --> V
    V -. clean record resets counters .-> P
```

### 9.4.1 Layer 1 — Prevention

* **Blind evaluation:** the Provider's identity is hidden during scoring, preventing targeted favoritism or harassment.
* **Evaluator rotation:** an Evaluator may judge the same Provider at most a few times per window (proposed: 3 per 30 days), breaking up cozy relationships.
* **Sealed scoring:** human panelists cannot see one another's scores, preventing anchoring and collusion.
* **Geographic/operator diversity:** panels are spread across operators where the pool allows.

### 9.4.2 Layer 2 — Detection

The protocol runs continuous statistical monitoring over a rolling window (proposed: last 100 evaluations) and triggers scrutiny on any of nine anomalies:

| # | Anomaly trigger |
| --- | --- |
| 1 | **Systematic bias** — approval rate deviates > 2σ from the network average |
| 2 | **Borderline manipulation** — > 30% of scores cluster within 10% of the threshold |
| 3 | **Targeted harassment** — 3+ rejections of one Provider vs. normal approvals for others |
| 4 | **Speed gaming** — rubric jobs "evaluated" in under 5 minutes |
| 5 | **Score clustering** — std-dev < 3 across 20+ evaluations (rubber-stamping) |
| 6 | **Counterparty concentration** — low Shannon entropy (same few Providers repeatedly) |
| 7 | **Reject-to-refund scheme** — reject → same Client reposts → same Evaluator re-evaluates |
| 8 | **Shadow-score divergence** — > 25-point gap from an independent reference LLM on most dimensions |
| 9 | **Sealed-vote inconsistency** — correlated human scores + shared funding source |

### 9.4.3 Layer 3 — Response

When a trigger fires, the protocol opens a **protocol-initiated dispute** ([§8.5](08-dispute-resolution.md#85-protocol-initiated-disputes)): the treasury funds the deposit (no victim must pay), and the standard VRF arbitration re-examines the evaluation. This is what catches Provider–Evaluator collusion that neither colluding party will ever report.

### 9.4.4 Layer 4 — Recovery

If wrongdoing is confirmed, the Evaluator is slashed per [§7.4](07-economics.md#74-slashing-conditions); the injured party receives 60% of the slash plus compensation; and the treasury is reimbursed. Conversely, an Evaluator that accumulates a long clean record (proposed: 500 consecutive undisputed jobs) has its violation counters reset — the system rehabilitates honest agents and reserves permanent exclusion for repeat or egregious offenders.

## 9.5 Shadow evaluation

Underpinning Layer 2 is **shadow (reference) scoring**: for a sample of jobs, the protocol independently runs a reference evaluation and compares it to the Evaluator's. A persistent, large divergence (trigger #8) is strong evidence of bias or collusion and feeds the detection layer. Shadow evaluation makes dishonest judging risky even when a single job looks unremarkable in isolation — because the Evaluator never knows which of its decisions is being checked.

---

[← Dispute Resolution](08-dispute-resolution.md) · [Next: The AGM Token →](10-token-agm.md)
