# A/B Experiment Brief, Riverty business-unit case

## Parameters
| Parameter | Decision |
|---|---|
| Feature under test | Payday alignment |
| Persona | Mara represents financially constrained consumers who want to resolve their debt independently through Riverty's self-service portal. She has limited time, an uncertain or variable income, and cannot pay her outstanding balance in full. Her priority is not simply to start an instalment plan, but to understand whether one is affordable and sustainable before making a commitment.  She values clarity, transparency, and reassurance throughout the journey. Rather than avoiding repayment, she wants confidence that she is making the right financial decision. If the process feels unclear, asks for information without explanation, or leaves uncertainty about the consequences of missing a payment, she loses trust, abandons the journey, or contacts an agent for reassurance. |
| Expected outcome | The goal is for consumers to commit to an instalment plan on their own, because the first payment lands after their payday.  User outcome: a faster, calmer decision with no need to call an agent for reassurance. Business metrics: self-service plan completions without agent contact within 7 days go up by 15%. Missed payments within 60 days stay at or below 19%. |
| Primary success metric | the % of consumers who complete a self-service instalment plan without contacting an agent within 7 days. The target is a +15% increase. Today, 31% of people who start the journey contact an agent within 7 days.  Guardrail: missed payments within 60 days must stay at or below 19%. |
| Baseline rate | about 32% of journey starters complete a self-service plan without contacting an agent within 7 days. This is an estimate derived from your existing numbers, not a measured value.  Calculation: a 46% agreement rate multiplied by the 69% who don't contact an agent gives about 32%. Since people who call an agent are less likely to complete, the real figure is probably a bit higher, around 32–40%. Target: +15% relative takes it from 32% to about 37%, which is realistic. +15 percentage points would mean 47%, which is very ambitious. |
| Guardrail metric | Percentage of repayment plans with at least one missed payment within 60 days. This rate must not exceed the current baseline of 19%. |
| Guardrail boundary | Must remain ≤ 19% (no statistically significant increase compared to baseline). |
| Second guardrail | · |
| Minimum Detectable Effect | 9 % |
| Sample size per arm | 4100 |
| Traffic split | 50/50 |
| Test duration | 30 days |
| Significance threshold | 5% |

## Control vs. Variant
- **Control (A):** Consumers start the digital instalment journey in the self-service portal and go through the existing flow. They choose a monthly amount, provide income information and upload proof of income. They then see a plan summary (amount, first payment date, frequency), review the plan and confirm it. The first payment date is set by the system as today, without asking when the consumer's income arrives and without explaining why this date was chosen. After confirmation, they see "Your repayment plan is set" and receive the same payment reminder before the first payment as in Variant B.

Not included: income-timing question, recommended first payment date, explanation of the payment date.
- **Variant (B):** Same journey as Control (A), with one change: the first payment date is aligned with the consumer's payday.

Before the plan summary, consumers answer "When do you usually receive your income?" (day of the month, or End of month / Middle of month / Every 4 weeks). The system then recommends a first payment date 2 days after the next income date and at least 5 days from today; otherwise it uses the following income cycle. The date is shown with a short, plain-language explanation of why it was chosen. The review and confirmation screens additionally show the income timing used.

Everything else is identical to Control (A): plan amounts and slider, income information and proof upload, plan summary layout, review and confirmation step, payment reminder, copy tone, agent entry points and eligibility rules.
- **Held constant (isolation check):** _(not filled in)_

## Hypothesis
> I believe that Payday alignment for Mara represents financially constrained consumers who want to resolve their debt independently through Riverty's self-service portal. She has limited time, an uncertain or variable income, and cannot pay her outstanding balance in full. Her priority is not simply to start an instalment plan, but to understand whether one is affordable and sustainable before making a commitment.  She values clarity, transparency, and reassurance throughout the journey. Rather than avoiding repayment, she wants confidence that she is making the right financial decision. If the process feels unclear, asks for information without explanation, or leaves uncertainty about the consequences of missing a payment, she loses trust, abandons the journey, or contacts an agent for reassurance. will result in The goal is for consumers to commit to an instalment plan on their own, because the first payment lands after their payday.  User outcome: a faster, calmer decision with no need to call an agent for reassurance. Business metrics: self-service plan completions without agent contact within 7 days go up by 15%. Missed payments within 60 days stay at or below 19%., as measured by a 9 % change in the % of consumers who complete a self-service instalment plan without contacting an agent within 7 days. The target is a +15% increase. Today, 31% of people who start the journey contact an agent within 7 days.  Guardrail: missed payments within 60 days must stay at or below 19%. within 30 days. We will protect Percentage of repayment plans with at least one missed payment within 60 days. This rate must not exceed the current baseline of 19%. throughout the test.

## Shipping criteria
> We will **ship** if the % of consumers who complete a self-service instalment plan without contacting an agent within 7 days. The target is a +15% increase. Today, 31% of people who start the journey contact an agent within 7 days.  Guardrail: missed payments within 60 days must stay at or below 19%. improves by ≥ 9 % at 5% and Percentage of repayment plans with at least one missed payment within 60 days. This rate must not exceed the current baseline of 19%. does not reach Must remain ≤ 19% (no statistically significant increase compared to baseline). after 30 days.
> We will **iterate** if direction is positive but lift is below the MDE.
> We will **kill** if the primary metric shows no improvement or moves negatively.
> The read date is fixed at the end of 30 days, no results reviewed before this date.
