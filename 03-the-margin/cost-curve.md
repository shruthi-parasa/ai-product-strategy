# Cost Curve & Pricing Strategy

> **Unit note:** "User" = a payments-analyst seat. AI cost actually scales with **transaction volume**, not headcount, so figures below assume one analyst oversees ~500,000 transactions/month (~45,000 declines analyzed). All numbers are fake, and used solely for assignment purposes.

## Cost Model
| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) | ~$74 | Mid-tier routing on the ~30% recoverable declines + periodic frontier insights (Glean) |
| Inference (cascading/triage) | ~$13.50 | Cheap small model classifies *every* decline (soft/hard/false) at ~$0.0003 each |
| Infrastructure | ~$15 | Hosting in-house decline/routing models + pipelines |
| Data/storage | ~$8 | Transaction history, feature store, model outputs |
| Human-in-the-loop | ~$10 | Analyst QA / labeling of edge cases (outcomes auto-label the rest) |
| **Total AI COGS** | **~$120 / analyst / month** | Against ~$40k/month net recovered revenue per analyst → **~99.7% gross margin** |

## Cascading Strategy
**Triage model:** A cheap **small** model classifies every decline (soft / hard / false) for a fraction of a cent — runs on 100% of declines.
**Frontier model:** **Glean / LLM** generates complex, aggregate strategic insights and handles the highest-value recoveries only — never per-transaction by default.
**Routing rule:** Escalate to a higher tier only when value-at-stake or complexity crosses a threshold (e.g., transaction > $X, or an ambiguous decline reason).
**Expected cascade ratio:** ~95% small / mid · ~5% frontier.

## Pricing Model
**Current pricing:** None — funded as part of payments-ops cost; the value is invisible on the P&L (a cost center).
**Proposed AI pricing:** Outcome-based internal value-capture — Aperture is credited with a share of the **recovered revenue** it generates. If ever productized for partners, the same model externalizes as **no-win, no-fee** (a fee only on revenue actually recovered).
**Model:** ~~seat-based~~ / ~~usage-based~~ / **outcome-based** / (hybrid if productized: small base + outcome fee)

## Stress Tests
| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3× | ~99.7% → ~99.2% gross — negligible | No structural action; the cascade discipline already keeps frontier usage at ~5%. |
| Heaviest segment doubles | Frontier-insight volume rises but stays a small slice; low single-digit margin impact | Tighten the routing threshold so only the highest-value cases hit the frontier model. |
| Model provider raises prices 50% | Bounded — only the ~5% frontier slice is exposed | Route that slice to a cheaper / open-weights model behind our interface (M2 kill switch); core models unaffected. |

## Board One-Pager
**Before (traditional / pre-AI):** The Power BI dashboard *reports* what failed. It's a pure cost center — analysts read it, but declined transactions stay lost. Revenue impact: **$0**.

**After (AI-enabled):** Aperture *recovers* a share of failed transactions automatically. New recovered revenue ≈ **~$40k / analyst / month** (illustrative) at **~99% gross margin**, since AI cost is ~$120 / analyst / month.

**Net margin shift:** Converts reporting from a **cost center into a high-margin recovery engine** — effectively new revenue at ~99% margin, with inference cost rounding to a rounding error. The constraint isn't profitability; it's how much transaction volume we can point it at (and defending the moat from M2).
