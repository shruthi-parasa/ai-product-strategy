# Payments Analytics Dashboard

It shows authorization rates, declines, fees, and processor comparisons across different time periods and payment types, so the team can see where payments are succeeding and failing. Goal is to grow this dashboard from a tool that shows what's failing into one that fixes it — using AI to retry failed payments smartly, route to the best processor, and recover wrongly-declined transactions.

> For my company's payments team, this turns the existing payments dashboard from something that shows failed transactions into an AI engine that recovers them, and now is the moment, because real-time decline-recovery AI has become cheap and reliable while the processors race to close the same gap.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | [`01-the-bet/`](01-the-bet/) |
| **The Moat** | M2 | [x] | [`02-the-moat/`](02-the-moat/) |
| **The Margin** | M3 | [x] | [`03-the-margin/`](03-the-margin/) |
| **The Contract** | M4 | [x] | [`04-the-contract/`](04-the-contract/) |
| **The Guardrails** | M5 | [x] | [`05-the-guardrails/`](05-the-guardrails/) |
| **The Pitch** | M6 | [x] | [`06-the-pitch/`](06-the-pitch/) |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** Payments Analytics Power BI Dashboard — it shows authorization rates, declines, fees, and processor comparisons across different time periods and payment types, so the team can see where payments are succeeding and failing. Goal is to grow this dashboard from a tool that shows what's failing into one that fixes it, using AI to retry failed payments smartly, route to the best processor, and recover wrongly-declined transactions.
- **AI Value Archetype:** Copilot. It works alongside the payments product manager and surfaces which declines are recoverable and what to do about each; the PM reviews and applies the recovery (e.g., "Apply all pending"). The human stays in control.
- **Vulnerability Scores:** Moat 2/5 · Data 4/5 · Platform 2/5
- **Top Risk:** The payment processors my company depends on are starting to do this themselves for free, so the AI upgrade only wins if my company leans on the one thing those processors can't see: its own cross-brand stored-value data.
- **Confidence:** M
- **Prototype:** https://aperture-insight-recovery.lovable.app
- **Kill Criteria:** Kill the bet if, after a 90-day pilot, **any** of these is true: (1) **No incremental value** — recovered revenue is at or below what our processors already recover natively (e.g., Stripe Authorization Boost), meaning we rebuilt something we get for free; (2) **The data gap closes** — processors expose the cross-brand signal we relied on, erasing our edge; (3) **Wrong-recovery cost** — the cost of bad "recover" actions (chargebacks, fraud) outweighs the revenue recovered.

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:** 13/20 (Correction 4 · Preference 3 · Domain Context 4 · Network 2)
- **Weakest Loop:** Network (2/5)
- **Top Encroachment Threat:** Stripe (and the card networks, Visa / Mastercard)
- **Encroachment Defense:** Don't fight the volume war against the networks. Deepen the network effect *inside* our domain — pool decline and recovery signal from every brand and program into one shared stored-value model so each program added makes the whole system smarter.
- **Vendor Portability:** Partial — model-portable, platform-dependent. Swapping the underlying model is easy (Glean is model-neutral); swapping Glean itself would mean rebuilding the agent + connector layer.

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** Cost center — the dashboard reports but doesn't directly recover revenue, so the value is invisible on the P&L.
- **Gross Margin (AI-adjusted):** 99%
- **Pricing Model:** ~~seat-based~~ / ~~usage-based~~ / **outcome-based** / (hybrid if productized: small base + outcome fee)
- **Pricing Today → Tomorrow:** None — funded as part of payments-ops cost; the value is invisible on the P&L (a cost center). → Outcome-based internal value-capture — Aperture is credited with a share of the **recovered revenue** it generates. If ever productized for partners, the same model externalizes as **no-win, no-fee** (a fee only on revenue actually recovered).
- **Total AI COGS / unit:** _placeholder — fractions of a cent per decision; small-model triage on 100% of declines plus rare frontier calls (figure held private in this public repo)._
- **Cascading Strategy:** Triage: a cheap **small** model classifies every decline (soft / hard / false) for a fraction of a cent — runs on 100% of declines; frontier: **Glean / LLM** generates complex, aggregate strategic insights and handles the highest-value recoveries only — never per-transaction by default; ratio ~95% small / mid · ~5% frontier.
- **Net Margin Shift:** Converts reporting from a **cost center into a high-margin recovery engine** — effectively new revenue at ~99% margin, with inference cost rounding to a rounding error.
- **Break-even at:** Holds margin even under 3× cost stress — recovered revenue dwarfs inference cost, so there's no realistic volume at which the economics invert.

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:** 92% accuracy (correct decline class + action) · <1% wrong-recovery rate (recovering a txn that shouldn't be, esp. fraud) · p95 latency <800 ms · drift <0.5%/wk.
- **Golden Dataset:** 5 rows, 3 adversarial
- **Confidence UX:** **tiered confidence + human-in-loop trigger** (the AI-class confidence score from the prototype drives the tier).
- **HITL Architecture:** **Trigger — when a human enters:** Confidence <70% **OR** the safety rule fires (a "recover" action proposed on a fraud-classed / hard decline). Those route to the analyst review queue; >90% auto-applies, 70–90% needs one-click confirm.
- **Failure Mode Coverage:** No **multi-currency / cross-border** declines yet; missing stored-value-specific decline reasons. Covered: soft/hard/false classification, fraud-vs-false-decline, the auto-rollback path for wrong recovery.

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales — and what compounds.**

- **Compounding System:**

  | Loop | Input | Output | Compounds? | Status |
  |------|-------|--------|-----------|--------|
  | **Recursive Learning** | Every retry/reroute outcome | Sharper decline + routing models | Y | **active** — each action labels its own ground truth |
  | **Cross-Domain Transfer** | Patterns from one brand's prepaid BINs | Better recovery on adjacent programs | Y | **active** — underused; programs not pooled yet |
  | **Network Intelligence** | Each new program on the platform | A smarter shared model for all programs | Y | **broken** — data is siloed per program |

- **Governance Posture:** Aperture's automated recovery decisions (retry / reroute / tokenize) plus the LLM insights layer — anything that moves or recommends moving money.
- **Autonomy Boundaries:** *On its own* — auto-apply recovery on high-confidence (>90%) soft/false declines, plus read-only analytics. *Needs a human* — any recovery on a fraud-flagged or hard decline, anything above a value cap, anything under 70% confidence.
- **Escalation Triggers:** Confidence <70%, **or** the fraud-safety rule fires, **or** value > $X → analyst review queue.
- **Audit Cadence:** Weekly gold-set audit (accuracy + wrong-recovery), real-time monitoring for latency and the fraud rule, quarterly bias/governance review.
- **Shadow AI Audit (user-side):** 5 workarounds found · 3 build (decline classification, routing, confidence scoring) — these *are* Aperture's roadmap · 1 partner (Slack alerts) · 1 ignore. Adjacent spend: _placeholder — AI subscriptions + analyst hours these consume per month; this is the adjacent spend Aperture absorbs._
- **Agent Boundaries:** Aperture leans Copilot, but auto-apply makes it act agentically — so the boundaries are locked. **Can:** retry, reroute, or tokenize on high-confidence soft/false declines. **Can't:** touch fraud/hard declines, exceed the per-action value cap, or move money outside defined recovery actions; tool calls are whitelisted, rate-limited, and logged.
- **Regulatory Exposure:** PCI-DSS, GDPR/CCPA, and fair-treatment rules (no unlawful bias in who gets recovered). EU AI Act risk tier: **limited** — we optimize acceptance of already-attempted transactions, not credit decisions — but transparency and logging obligations apply.

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):**
- **Horizon 2 (Next):**
- **Horizon 3 (Bet):**
- **Board Narrative:** **The case:**
- **Ask:** ## M1 Baseline vs. Now
- **Key Strategic Change:**

→ Details: [`06-the-pitch/`](06-the-pitch/)
