# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | 4/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | 3/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | 4/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | 2/5 |

### Correction Loop - 4/5
**What you capture today:** Every AI-recommended action (retry / reroute / tokenize) is applied or overridden by the analyst, and the outcome is observable within seconds — the retried transaction either approves or declines again. That's an automatic ground-truth label *plus* an explicit human correction on every action.

**How it compounds:** Each labeled outcome retrains the decline classifier and routing model, so next week's "false decline" calls get sharper. Payments is rare among AI domains: the world tells you within seconds whether you were right, so the signal is self-generating with almost no manual labeling. *(Held at 4, not 5: we only learn from actions we actually take, and brand-new programs cold-start.)*

### Preference Loop - 3/5
**What you capture today:** Segment-level routing and retry policies — which processor approves best for a given card brand, BIN range, amount band, or program — remembered and reused.

**How it compounds:** Each program builds its own optimal routing profile over time, so recommendations get tailored to that segment instead of one-size-fits-all. Weaker than Correction because it's segment-preference, not a core feedback signal, and it's stateless for any brand-new program.

### Domain Context Loop - 4/5
**What you capture today:** Proprietary cross-brand, cross-processor stored-value lifecycle data — activation, redemption, breakage, and decline reasons across many programs — that no single merchant or processor can see.

**How it compounds:** Patterns learned on one brand's prepaid BIN ranges transfer to adjacent brands and programs, building gift-card / prepaid decline expertise that generic models lack. This is the loop competitors literally cannot access.

### Network Loop - 2/5
**What you capture today:** Each new brand or program added to the platform contributes its decline/recovery outcomes to one shared model, so more programs = better recovery for everyone on it.

**How it compounds:** A real within-ecosystem data-network effect — but **bounded**: it spans only our own programs, while Stripe, Visa, and Mastercard enjoy a far larger cross-merchant network effect on raw volume. This is the weakest loop, and it's the M1 Platform-Exposure vulnerability resurfacing.

**Total Flywheel Score: 13/20**
**Weakest Loop:** Network (2/5)

**Fix for weakest loop:** Don't fight the volume war against the networks. Deepen the network effect *inside* our domain — pool decline and recovery signal from every brand and program into one shared stored-value model so each program added compounds the whole, and specialize in the gift-card / prepaid BIN behavior the big networks don't prioritize. Turn "less volume" into "more depth per unit of volume."

---

## Encroachment Threat Assessment

### 1. Platform Encroachment
**Attacker:** Stripe (and the card networks, Visa / Mastercard)

**Vector:** Ships native acceptance-optimization and decline-recovery (Authorization Boost: Adaptive Acceptance, Smart Retries, Card Account Updater, network tokens) free inside the processor dashboard — commoditizing the smart-retry + routing layer of our bet from underneath.

**Time-to-threat:** 0–6 months — already shipping; the pieces are live and only need bundling.

**% of value at risk:** ~40% (the "action" layer — retry + routing. The stored-value data layer stays protected.)

### 2. Vertical Competitor
**Attacker:** ProcessOut / Telescope (Checkout.com) and Yuno — cross-processor orchestration + payment-intelligence platforms.

**Vector:** Sell a turnkey, multi-processor optimization and recovery layer out of the box — attacking our Contextual Moat ("why build it ourselves?") and our Network loop, since they aggregate across many merchants and so have a bigger network effect than our single-company one.

**Time-to-threat:** 6–12 months — they exist today but would need to win our internal build-vs-buy decision and move into stored-value.

**% of value at risk:** ~30% (the orchestration/routing layer plus the internal "just buy it" risk.)

### 3. Adjacent Expansion
**Attacker:** Riskified / Forter (and Sift) — fraud-prevention platforms expanding from "block fraud" into "recover false declines."

**Vector:** They already score every transaction for fraud, so extending into false-decline recovery is one step sideways. That attacks our Correction and Domain Context loops on the false-decline slice specifically.

**Time-to-threat:** 12–18 months — further from the stored-value specifics, and they'd be learning our domain from scratch.

**% of value at risk:** ~20% (the false-decline-recovery portion.)

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:**
**Attack vector (target the weakest loop):**
**Weeks 1-4 - what they ship:**
**Weeks 5-8 - how they poach users:**
**Weeks 9-12 - why users don't come back:**
**Your defense:**
