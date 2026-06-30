# Kill Switch Audit

## Vendor Dependency Assessment
| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** | Insights layer runs on Glean (a model-neutral platform routing across 15+ LLMs). Core decline/routing models are owned in-house. | L / M | Model-level risk is low — Glean swaps models freely. Track the *platform* dependency on Glean, not the model. |
| **Abstraction** | Glean *is* the model-abstraction layer (strong), but our insight logic is wired into Glean's agent framework. | M | Keep the payments-insight logic in our own orchestration so it can call **either** Glean **or** a direct LLM — not 100% inside Glean. |
| **Routing** | Multi-model routing is built in — Glean auto-routes across 15+ models and fails over between them. | L | Confirm a direct-LLM fallback path (Bedrock / Azure OpenAI) for the day we might leave Glean entirely. |
| **Eval** | Core models have automatic ground-truth (retry outcomes); insight quality is checked manually, aided by Glean's usage observability. | M | Build an automated eval set for the insights layer so any platform/model change must pass before switching. |

## Portability Score
Partial — model-portable, platform-dependent. Swapping the underlying model is easy (Glean is model-neutral); swapping Glean itself would mean rebuilding the agent + connector layer.

## If Glean doubles pricing tomorrow:
Bounded blast radius — only the insights layer is exposed, since the core models are ours. Within 48 hours we cap Glean agent usage and route insight-generation to a direct LLM (Bedrock / Azure) behind our own interface. Margin impact is quantified in M3.

## If Glean ships a competing product:
Low threat. What they can't replicate is our proprietary cross-brand stored-value data (activation → redemption → breakage) and the in-house models trained on it. Glean abstracts models, not our data — so we treat their product as just another swappable provider and lean harder on the Domain Context loop.
