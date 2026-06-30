# Three-Horizon Roadmap & Board Pitch

## Roadmap

### Horizon 1 — Now (0-3 months)
*Quick wins. Ship with existing capabilities.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Native decline classification (soft / hard / false) on the dashboard — replaces analysts exporting CSVs into ChatGPT | % of declines auto-classified; analyst CSV-export workaround retired | H |
| Confidence scoring on every recovery suggestion (Copilot, analyst applies) | % suggestions with a confidence tier; analyst accept rate | H |

### Horizon 2 — Next (3-9 months)
*Bets. Requires new capabilities or integrations.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Routing recommendations (best processor per transaction) | Recovery uplift vs. baseline; reroute success rate | M |
| Expand auto-apply on high-confidence (>90%) soft/false declines as the reliability contract holds | % actions auto-applied; wrong-recovery rate <1%; HITL queue size trending down | M |

### Horizon 3 — Bet (9-18 months)
*Moonshots. High uncertainty, high potential.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Fix the Network loop — pool decline/recovery data across every brand & program into one shared stored-value model (the moat) | # programs pooled; recovery accuracy lift per program added; Network loop 2/5 → 4+/5 | M |

## Board Pitch

**Thesis (1 sentence):** We already sit in the transaction path, so every wrongly-declined payment is our own lost revenue — Aperture turns that leak into recovered margin using cross-brand data the processors can't see.

**The case:**
1. **Why now:** Real-time decline-recovery AI has become cheap and reliable, and the dashboard already has the data; the window is open before processors close the gap.
2. **What's defensible:** Cross-brand stored-value signal the processors and networks can't see — and the more programs we pool, the harder it is to copy.
3. **The economics:** AI cost per decision rounds to nothing against recovered revenue → ~99% margin, holding even at 3× cost stress; outcome-based value capture (a share of what it recovers).

**The risks:**
1. **Trust / failure modes:** A wrong "recover" on real fraud costs money — mitigated by confidence tiers, a fraud-safety rule, and auto-rollback when wrong-recovery rate exceeds threshold.
2. **Scale / governance:** Any money-moving action is gated (confidence + value caps), with weekly gold-set audits and a *limited* EU AI Act posture; reading is free, writing is approved.
3. **Competitive:** Processors (Stripe Authorization Boost, Visa/Mastercard) ship generic acceptance-optimization for free — we only win on the data they can't see, which is why Horizon 3 (the data moat) is the real bet.

**The ask:** Fund the shared-data foundation (Horizon 3). The near-term builds are already validated by what users hacked together themselves; the data moat is what makes the whole thing compound.

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:** For my company's payments team, this turns the existing payments dashboard from something that shows failed transactions into an AI engine that recovers them. Now is the moment, because real-time decline-recovery AI has become cheap and reliable while the processors race to close the same gap. The bet is a Copilot that classifies declines and recommends recoveries, with the PM in control.

**Now:** The strategy is sharper on *where the edge actually is*: not the recovery feature itself (processors give that away free), but the cross-brand stored-value data only we can see — so the real investment is fixing the data-silo loop that recurs across the moat, the flywheel, and the guardrails. Trust is now an explicit contract (confidence tiers, fraud-safety auto-rollback, <1% wrong-recovery) rather than a vague promise. And the roadmap isn't guesswork — three of its items are things users *already built themselves* with ChatGPT and Excel, which is the strongest demand signal there is.
