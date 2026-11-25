# Housebets Support AI — Arena Proposal Brief

**Goal:** build a 24/7 support agent that is measured before changed, cannot invent facts, and treats RG messages as top priority.

## 1. Toolset
- get_account_summary(user_id) — read-only
- get_transaction_history(user_id, filters)
- check_withdrawal_status(tx_id)
- lookup_kb(query) — RAG over help.housebets.com + FAQ
- get_current_promotions()
- open_ticket(priority, category)
- route_to_rg(user_id)

## 2. Guards
- No answer without evidence id (tool_call or KB).
- Blocklist: self-harm, doxxing, bypass KYC/AML, betting advice.
- Default when uncertain: escalate + safe template.
- No PII in logs.

## 3. Eval set (50 scenarios)
- 15 factual (bonus/withdrawal/KYC/payments/games)
- 10 RG/safety
- 10 prompt-injection/jailbreak
- 10 multi-turn
- 5 ambiguous
Full set: eval-set.csv.

## 4. Metrics
Factuality, refusal correctness, RG routing precision/recall, human-handoff rate, P95 latency, cost/session.

## 5. 30/60/90 plan
- Day 1–15: baseline eval, prompt v0, hard gates enforced.
- Day 16–45: expand eval to 150 scenarios, add LLM-judge + human review.
- Day 46–90: tune refusal thresholds, multi-language (top 5 langs), cost/latency optimization, weekly reporting.

## 6. Alignment with "what good looks like"
- Measure-before-change: enforced by rubric protocol.
- Cannot invent: evidence-required rule + hard gates.
- RG as top priority: dedicated category + routing + hard gate on crisis.
