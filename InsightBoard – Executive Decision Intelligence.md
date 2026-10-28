# 🧠 InsightBoard

LLM-powered decision intelligence for a Bharti Airtel–style telecom: which of the many KPIs actually explain revenue and margin? (Synthetic illustrative data, 18 months to Sep 2026.)

**Explain:** **in month:**

## Outcome

## Why did it change? (driver contributions)

## KPI evidence – 14 indicators tested

## Executive brief (LLM)

The LLM is given only the computed evidence below, nothing else.

Click to generate. Without LLM access the page shows a rule-based summary.

Answers are grounded in the evidence table.

## Algorithm used by the system

1. **Ingest** 14 operational KPIs (network, customer, commercial, people) and two financial outcomes (revenue, EBITDA margin).
2. **Remove shared trends**: use month-over-month changes. Two series that merely both rise over time have a high raw correlation but a near-zero correlation in changes.
3. **Lag search**: correlate each KPI change with the outcome change at lag 0, 1 and 2 months and keep the best. Significance threshold `|r| > 2/√n`.
4. **Classify** each KPI as *Driver* (significant), *Spurious trend* (high raw r, no change-r) or *Noise*.
5. **Joint model**: ridge regression on standardized, lag-aligned changes of the top drivers (λ = 1.5), to separate overlapping signals.
6. **Attribute a month**: contribution = β × (that month’s standardized KPI change) × outcome spread; the rest is “unexplained”.
7. **Evidence pack → LLM**: top drivers with r, lag, contribution and KPI movement are sent as JSON; the LLM writes the headline, insights, actions and caveats using only that evidence.
8. **Guardrail**: correlation is not proof of causation; the brief must say so and recommend a validation step.