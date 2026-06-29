# Three-Axis Vulnerability Diagnostic

## Product
<!-- Name the product you're diagnosing. Real product at your company — not a hypothetical. -->

**Product:**
Payments Analytics Power BI Dashboard - It shows authorization rates, declines, fees, and processor comparisons across different time periods and payment types, so the team can see where payments are succeeding and failing.Goal is to grow this dashboard from a tool that shows what's failing into one that fixes it using AI to retry failed payments smartly, route to the best processor, and recover wrongly-declined transactions. 

**Your Role:**
Associate Product Manager, Payments

---

## Scores

### Contextual Moat — 2/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:**
It's an internal dashboard, and that's not a moat on its own. There's no real lock-in, the payments team uses it because it's useful, not because they're stuck. If a processor, my company already pays shows the same charts (and even fixes failed payments automatically), the team has little reason to open their own Power BI dashboard instead. The tool itself is easy to copy or replace; only the data behind it is hard to copy.

**Named attacker (from partner challenge):**
Stripe — its dashboard already shows auth rates, declines, and fees, and its Authorization Boost recovers failed payments natively.

---

### Data Advantage — 4/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:**
This is my company's one real strength. My company sees how customers move from purchase, to use, to leftover balance, across many brands and processors. No outside company sees that. As the AI upgrade rolls out, this advantage compounds: every payment the system recovers teaches it to recover the next one better. It's a 4, not a 5, because bigger players see more transactions overall, Blackhawk wins on knowing its own world deeply, not on having the most data.

**Named attacker (from partner challenge):**
Stripe — its AI is trained on billions of transactions, far more than BHN sees. Visa and Mastercard see even more raw volume across the whole market.

---

### Platform Exposure — 2/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?*

**Score rationale:**
The companies we rely on to process payments are already building the exact feature the AI bet depends on. So they could give away for free, part of what the bet is meant to deliver. And because we are a large company, we can't change direction quickly. High risk + slow to pivot = low score.

**Named attacker (from partner challenge):**
Adyen, Visa, and Mastercard — all building this into the rails BHN already uses.

---

## Top Vulnerability
The payment processors BHN depends on are starting to do this themselves for free, so the AI upgrade only wins if BHN leans on the one thing those processors can't see: its own data.

## Confidence Level
<!-- H / M / L — how confident are you in this bet after the diagnostic? -->
M (Medium, leaning High). The threat from processors is real and already happening. The only open question is exactly which processors carry BHN's volume across other processors as well.
