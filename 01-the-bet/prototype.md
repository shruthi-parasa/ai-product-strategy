# The Prototype Bet

## What I Built
<!-- One sentence: what does this prototype demonstrate? -->
An interactive dashboard prototype that spots failed and wrongly-declined transactions, classifies each one (soft / hard / false decline with a confidence score), and recommends or applies the fix (retry, reroute to a better processor, or tokenize), turning payment analytics into recovered revenue.

## Tool Used
<!-- v0 / Cursor / Lovable / other -->
Lovable

## Prototype Link
<!-- Paste the shareable URL -->
https://aperture-insight-recovery.lovable.app

## AI Value Archetype
<!-- Automator / Copilot / Oracle / Creator / Orchestrator -->
Copilot. It works alongside the payments product manager and it surfaces which declines are recoverable and what to do about each, and the PM reviews and applies the recovery (e.g., "Apply all pending"). The human stays in control.
(It also carries Orchestrator DNA — routing volume across multiple processors — and has a clear path toward Automator as trust grows and low-risk retries get auto-applied.)

## The Bet in One Sentence
<!-- What you're building, for whom, why now -->
For my company's payments team, this turns the existing payments dashboard from something that shows failed transactions into an AI engine that recovers them, and now is the moment, because real-time decline-recovery AI has become cheap and reliable while the processors race to commoditize it.

## Kill Criteria
<!-- When would you stop? What evidence would kill this bet? -->
Kill the bet if, after a 90-day pilot, **any** of these is true:
1. **No incremental value** — recovered revenue is at or below what our processors already recover natively (e.g., Stripe Authorization Boost), meaning we rebuilt something we get for free.
2. **Negative net recovery** — false-positive retries push chargebacks and retry fees above the revenue recovered.
3. **No adoption** — PMs ignore the AI recommendations and keep working from the old reports.

Any one of these means the bet isn't earning its keep.
