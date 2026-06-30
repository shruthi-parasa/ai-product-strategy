# Golden Dataset & Reliability Contract

## Golden Dataset Spec
| # | Input | Expected Output | Edge Case? | Judge Type |
|---|-------|----------------|-----------|-----------|
| 1 | Visa credit decline, reason `insufficient funds`, $330, processor Fiserv | Class: **Soft decline** → action: **Retry now** (timed); recoverable | N | rule + LLM |
| 2 | Visa digital-wallet decline, reason `do not honor`, $149, Chase Paymentech | Class: **False decline** → action: **Reroute to Fiserv**; recoverable | Y | rule + LLM |
| 3 | Mastercard credit decline, reason `suspected fraud`, $319, Chase Paymentech | Class: **Hard decline** → action: **No action** (do NOT retry — genuine fraud) | Y | rule |
| 4 | Amex credit decline, reason `AVS mismatch`, $333, Fiserv, tokenized BIN | Class: **False decline** → action: **Reroute + network token**; recoverable | Y | rule + LLM |
| 5 | Visa debit decline, reason `issuer unavailable`, $446, Fiserv | Class: **Soft decline** → action: **Retry now** after backoff; recoverable | N | rule |

**Adversarial rows included:** **3** (rows 2, 3, 4 — target ≥3 met). These are the cases that punish the model for the *wrong* instinct: row 3 looks retryable but is real fraud (retrying = loss + chargeback); rows 2 & 4 look like hard declines but are recoverable false-positives.

**Coverage gaps identified by partner:**
- No **multi-currency / cross-border** declines yet.
- No **stored-value-specific** reasons (activation fail, redemption-velocity block) — our actual domain edge; must be added before v1.
- No **repeat-offender** rows (same card declined N times) to test retry-loop guards.

## Confidence UX Design
**Approach:** **tiered confidence + human-in-loop trigger** (the AI-class confidence score from the prototype drives the tier).

**High confidence (>90%):** Auto-apply the recovery (retry/reroute) silently; log it; surface in the "Recovered" tally. No analyst action needed — HITL queue stays small.

**Medium confidence (70-90%):** Show the recommendation **with reasoning + projected $**, but require a one-click analyst confirm before acting. Visible uncertainty ("84% — likely false decline").

**Low confidence (<70%):** **Block auto-action; escalate to the analyst review queue.** Never auto-retry a low-confidence case (a wrong retry on real fraud costs money + chargebacks).

**User control surface:**
- Analysts can **adjust the auto-apply threshold** (default 90%).
- Every recommendation shows **AI reasoning** (decline reason + why this class).
- Analysts can **correct / override** any call — and **each correction flows back to retrain the model** (this is the M2 flywheel's Correction loop made real, so the HITL queue *shrinks* over time rather than becoming permanent babysitting).

## Reliability Contract

| Metric | Target | Measurement | Alert Threshold |
|--------|--------|-------------|-----------------|
| **Accuracy** (correct decline class + action) | 92% | Weekly · golden set (v1 ~150 rows) · auto-graded against real retry/reroute outcomes (rule + LLM judge) | <88% → page on-call PM + gold-set audit |
| **Wrong-recovery rate** (our "hallucination": retried/rerouted a txn that shouldn't have been — esp. real fraud) | <1% | Same weekly run · safety rule flags any "recover" action on a fraud-classed or hard decline | ≥2% → **auto-rollback** to last good model + pause auto-apply |
| **Latency (p95)** | <800 ms | Continuous prod monitoring (Datadog) · p95 per decision | >1200 ms for 5 min → PagerDuty on-call |
| **Drift velocity** (recovery accuracy decay) | <0.5%/wk | 4-week rolling accuracy trend vs golden set | >1%/wk → **gold-set audit** (the world changed — issuer/processor behavior — not the model) |

**Defensible bands (why these numbers):** Accuracy 90–95%, not 99% — 99% sounds great but you can't ship or measure it weekly. Wrong-recovery <1% is the load-bearing one: in payments a wrong "recover" costs money + a chargeback, so it auto-rolls back rather than just paging (the Air-Canada logic — the system speaks with money, so a confident wrong action is expensive).

## HITL Architecture
**Trigger — when a human enters:** Confidence <70% **OR** the safety rule fires (a "recover" action proposed on a fraud-classed / hard decline). Those route to the analyst review queue; >90% auto-applies, 70–90% needs one-click confirm.

**Reviewer — who reviews:** Rotating payments-ops analyst on-call (weekday business hours); high-value (> $X) low-confidence cases flagged for same-day review.

**Feedback loop — do corrections feed back?** Yes — every analyst correction/override is logged and feeds the weekly gold-set audit, with a retrain trigger when ≥N rows are updated. This is the M2 flywheel's Correction loop: corrections become training signal, so the HITL queue **shrinks** over time instead of becoming permanent babysitting. *(Without this feedback, HITL is just a crutch.)*
