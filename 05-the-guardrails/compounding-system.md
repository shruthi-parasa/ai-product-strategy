# Compounding System Design

## Feedback Loops
| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| **Recursive Learning** | Every retry/reroute outcome | Sharper decline + routing models | Y | **active** — each action labels its own ground truth |
| **Cross-Domain Transfer** | Patterns from one brand's prepaid BINs | Better recovery on adjacent programs | Y | **active** — but underused; programs aren't pooled yet |
| **Network Intelligence** | Each new program on the platform | A smarter shared model for all programs | Y | **broken** — data is siloed per program |

**Broken loop:** Network Intelligence. Today each program's data sits in its own silo, so adding a program doesn't make the system smarter. Same gap as the M2 flywheel's Network loop (2/5) and the M1 Platform risk — three modules pointing at one weakness.

**Fix:** Pool decline + recovery outcomes across programs into one shared model (with per-program privacy controls), so every new program lifts the whole. Until that's live, we're running a model, not compounding.

## Context Connectivity
Knowledge silos by program and by processor — each brand's data and each processor's decline reasons live in separate reporting. The fix is a shared feature store and model, so a pattern learned on one processor/brand helps the next. What silos worst is the stored-value-specific signal (activation, redemption, breakage) — which is exactly our moat.

## Governance Policy
**Scope:** Aperture's automated recovery decisions (retry / reroute / tokenize) plus the LLM insights layer — anything that moves or recommends moving money.

**Autonomy boundaries:** *On its own* — auto-apply recovery on high-confidence (>90%) soft/false declines, plus read-only analytics. *Needs a human* — any recovery on a fraud-flagged or hard decline, anything above a value cap, anything under 70% confidence. Reading is free; writing to money is gated.

**Escalation triggers:** Confidence <70%, **or** the fraud-safety rule fires, **or** value > $X → analyst review queue.

**Audit cadence:** Weekly gold-set audit (accuracy + wrong-recovery), real-time monitoring for latency and the fraud rule, quarterly bias/governance review.

**Regulatory exposure:** PCI-DSS, GDPR/CCPA, and fair-treatment rules (no unlawful bias in who gets recovered). EU AI Act risk tier: **limited** — we optimize acceptance of already-attempted transactions, not credit decisions — but transparency and logging still apply. Model cards and a documented bias posture are part of the story, not just the floor.

## Agent Topology
Aperture leans Copilot, but auto-apply makes it act agentically — so the boundaries are locked:
- **Can:** retry, reroute, or tokenize on high-confidence soft/false declines.
- **Can't:** touch fraud/hard declines, exceed the per-action value cap, or move money outside defined recovery actions. Tool calls are whitelisted, rate-limited, and logged.
- **Approvals:** high-confidence within caps = auto; medium = one-click analyst confirm; low / high-value / fraud-flagged = named on-call analyst. If a step fails, that analyst owns the handoff.

## Shadow AI Audit
What payments/ops teams already build with AI around today's Power BI dashboard. *(Tool = workaround · Owner = signal source · Risk = frequency · Decision = build/partner/ignore.)*

| Tool | Owner | Risk Level | Decision |
|------|-------|-----------|----------|
| Export decline CSVs into ChatGPT to triage | Support tickets + interviews | H | **build** — native decline classification |
| Manual Excel retry-tracking / "who approved" pivots | Analyst workflows + forums | H | **build** — native routing recs |
| Zapier/Make recipes piping alerts into Slack | Zapier/Make directory | M | **partner** — thin alerting integration |
| Eyeballing fraud vs. false decline off the dashboard | Sales/ops calls | M | **build** — native confidence scores |
| BI screenshots pasted into LLMs for exec write-ups | Internal | L | **ignore + monitor** |

**Total tools found:** 5.
**Tools after triage:** 3 build (decline classification, routing, confidence scoring) — these *are* Aperture's roadmap. 1 partner (Slack alerts). 1 ignore.
**Estimated hidden spend:** _placeholder — AI subscriptions + analyst hours these consume per month; this is the adjacent spend Aperture absorbs._
