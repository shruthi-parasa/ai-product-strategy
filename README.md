# My AI Product Strategy

> A living strategy built across 6 sessions. Each module adds one component. By Module 6, this repo IS your strategy — version-controlled, board-ready, portable.

---

## Strategy at a Glance
| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | [`01-the-bet/`](01-the-bet/) |
| **The Moat** | M2 | [x] | [`02-the-moat/`](02-the-moat/) |
| **The Margin** | M3 | [x] | [`03-the-margin/`](03-the-margin/) |
| **The Contract** | M4 | [x] | [`04-the-contract/`](04-the-contract/) |
| **The Guardrails** | M5 | [x] | [`05-the-guardrails/`](05-the-guardrails/) |
| **The Pitch** | M6 | [ ] | [`06-the-pitch/`](06-the-pitch/) |
---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** My company's Payments Analytics Power BI dashboard (today) → **Aperture**, an AI Payment Performance Intelligence engine that recovers revenue lost to failed and wrongly-declined transactions (the bet).
- **AI Value Archetype:** Copilot — surfaces recoverable declines and recommended fixes; the analyst reviews and applies. (Orchestrator DNA via cross-processor routing; path to Automator.)
- **Vulnerability Scores:** Moat **2**/5 · Data **4**/5 · Platform **2**/5
- **Top Risk:** The processors we rely on are shipping native acceptance-optimization (e.g., Stripe Authorization Boost), so the bet only wins by leaning on cross-brand gift-card/prepaid data those processors can't see.
- **Confidence:** M (leaning H) — threat is real and live; firms to H once we confirm exactly which processors carry our volume.
- **Prototype:** [Lovable Prototype](https://aperture-insight-recovery.lovable.app)
- **Kill Criteria:** After a 90-day pilot, kill if (1) recovered revenue ≤ what processors already recover natively, (2) false-positive retries cost more in fees/chargebacks than they recover, or (3) analysts don't adopt the recommendations.

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)
**Why this won't get copied in 6 months.**
- **Data Flywheel Score:** 13/20 (Correction 4 · Preference 3 · Domain Context 4 · Network 2)
- **Weakest Loop:** Network — decline/recovery data is siloed per program, so new programs don't yet make the whole smarter.
- **Competitive Position:** strong on data (cross-brand stored-value signal others can't see), weak on platform (we sit on processors who can copy generic optimization).
- **Encroachment Defense:** lean into the stored-value data moat; the more programs pooled, the harder to copy.
- **Vendor Portability:** Partial — core models are owned and portable; the LLM insights layer is platform-dependent.

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)
**Will this make money or bleed it?**
- **Gross Margin (current):** cost center — the dashboard doesn't directly recover revenue.
- **Gross Margin (AI-adjusted):** ~99% — AI cost per transaction is trivial next to recovered revenue.
- **Pricing Model:** outcome-based (a share of recovered revenue); no-win-no-fee if ever productized externally.
- **Cascading Strategy:** small cheap model triages, frontier model only on hard cases (~95/5 split).
- **Break-even at:** holds margin even at 3× cost stress; recovered revenue dwarfs inference cost. *(Figures held as placeholders in the public repo.)*

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)
**Why users will trust a probabilistic system.**
- **Reliability Target:** 92% accuracy (decline class + action), <1% wrong-recovery rate.
- **Golden Dataset:** ~150 rows v1, 3 adversarial cases (incl. fraud that looks retryable but must be left alone).
- **Confidence UX:** >90% auto-apply · 70–90% one-click confirm · <70% block & escalate.
- **HITL Architecture:** low-confidence or fraud-flagged cases route to a rotating analyst; every correction feeds the weekly gold-set audit (the M2 flywheel) so the queue shrinks.
- **Failure Mode Coverage:** "wrong recovery" (our hallucination) auto-rolls back; drift triggers a gold-set audit, not a rollback.

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)
**What breaks when this scales — and what compounds.**
- **Compounding System:** Recursive Learning (active — each action labels its own ground truth) and Cross-Domain Transfer (active, underused); Network Intelligence is broken (siloed per program).
- **Governance Posture:** any money-moving action is gated; reading is free, writing is approved by confidence + value caps.
- **Shadow AI Status:** 5 user workarounds found · 3 triaged to "build" — and they *are* the roadmap.
- **Agent Boundaries:** can retry/reroute/tokenize on high-confidence soft/false declines; can't touch fraud/hard declines or exceed value caps.
- **Regulatory Exposure:** PCI-DSS, GDPR/CCPA, fair-treatment; EU AI Act risk tier *limited*.

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):**
- **Horizon 2 (Next):**
- **Horizon 3 (Bet):**
- **Board Narrative:** [1-sentence thesis]
- **Key Metric:**

→ Details: [`06-the-pitch/`](06-the-pitch/)
