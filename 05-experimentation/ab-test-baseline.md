# A/B Test Baseline: Payday Alignment

Current state (control) of the self-service instalment journey, extracted from the module files. Use this as the reference point for testing the Payday Alignment variant.

**Status:** design frozen, launch conditional on the launch checklist (section 8). Launch go/no-go meeting: **Fri 23 Oct 2026**.

## 0. Test hypothesis

For consumers with variable income who cannot pay in full (Mara), asking when their income arrives and recommending a first payment date after payday, with a plain-language explanation, will increase the share of journey starters who complete a self-service plan without agent contact within 7 days from ~32% to ~37% (+15% relative), without raising the share of plans with a missed payment among the first two instalments by more than 3 percentage points, and without reducing the amount collected per journey starter from the first two instalments by more than 5%.

**What this test can and cannot claim:**
- Variant B is tested as one treatment package (income-timing question, payday-aligned default date with a minimum lead time of 5 days, explanation, timing shown on review and confirmation). A result tells us whether the package works, not which component drives it.
- The strongest rival explanation is not the 5-day minimum (it only applies when payday is less than 5 days away) but that **any** later default than "today" would have the same effect. This test does not separate payday alignment from a simple later first payment.
- A Go therefore justifies shipping B in this journey. It does **not** justify reusing the income-timing question in other journeys. That requires the follow-up test in section 7.6 (B vs. "today + 14 days, with explanation, no income question").

**Out of scope:** the persona's uncertainty about the consequences of a missed payment. Variant B does not change this, so the test makes no claim about it. Agent contacts about consequences are tagged separately (section 5) so they are not read as a failure of B.

## 1. Who is in the test

**Persona:** Mara, a consumer with limited time and an uncertain or variable income who wants to resolve her debt independently through Riverty's self-service portal. She is not a reluctant payer; she needs enough confidence to commit to a plan she can realistically keep.

**Eligible population:** consumers whose first journey start falls inside the enrolment window.
- **Day 0** = first journey start in the window. Assignment happens at day 0 and is sticky per consumer ID across sessions and devices.
- **Excluded before assignment:** consumers with a journey start in the 30 days before launch (already exposed to A), internal and test accounts, cases not eligible for an instalment plan under the existing eligibility rules.

## 2. Current journey (Control A)

1. Open the self-service portal to check whether an instalment plan is available.
2. Estimate an affordable monthly payment with little guidance. Pre-set slider values act as anchors (e.g. picking 150 without knowing if it is sensible).
3. Provide income information and upload income proof (e.g. payslip). There is no explanation of why income is requested or who sees it, and no alternative for cash-paid consumers.
4. Commit to the plan. The first payment date defaults to today; the consumer can change it, but it is not aligned with when income arrives, and there is no explanation of the timing.
5. If uncertain, stop the journey or call an agent for reassurance, and often complete the plan with the agent instead.

**Not in control:** income timing question, recommended first payment date, explanation of payment timing.

## 3. Moment of misery

Consumers cannot confidently commit to an instalment plan because they lack clarity about affordability and the consequences of their decision.

> "They ask me what I can afford per month. My pay changes every month. Do I put my best month? My worst month? Whatever I put, I feel like I'm signing up to it forever." (P3)

Timing-specific evidence: one consumer needs a start date of the 28th to match payday and exits despite understanding the journey (P9).

Observed behaviour: consumers under-report income, abandon the journey, or call an agent for reassurance instead of finishing online.

**Evidence limit:** only P9 is directly about the payment date. P3's fear is about amount and long-term commitment under variable income, which B addresses only indirectly. The qualitative case for the date mechanism rests on one participant; the test is what establishes it.

## 4. Baseline numbers

| Metric | Baseline | Source / status |
|---|---|---|
| Consumers contacted per month | 100,000 | Fictional baseline (M1) |
| Journey starters per month | ~8,360 (~1,920 per week) | Fictional baseline (M1) |
| Plans agreed per month | ~3,850 (46% of starters) | Fictional baseline (M1) |
| Starters contacting an agent within 7 days | 31% | M3 data |
| Drop-offs at income proof upload | 32.8% of all drop-offs (largest point) | M3 funnel |
| Drop-offs at affordability step | 26.8% of all drop-offs | M3 funnel |
| Agent contacts caused by missing documents | 21% | M3 data |
| Consumers accepting the default instalment who miss a payment within 60 days | 25% | M3 data |
| Plans missing a payment within 60 days | 19% | Current baseline; source unconfirmed (see AI synthesis). Working assumptions A2 and A3 (section 9). |
| **Starters completing a self-service plan without agent contact within 7 days** | **~32% (planning value)** | See note below. Working assumption A1. **Measured before launch.** |

**Note on the primary baseline.** The planning value 46% × 69% ≈ 32% assumes that agreeing to a plan and contacting an agent are independent. They are not: contacts are likely concentrated among consumers who abandon, and 46% may include agent-assisted plans. Without that assumption the logically possible range is 15–46%. The value is therefore measured directly (A1) and the sample check in section 5.7 is re-run on the measured value.

## 5. Metrics for the test

**Unit & exposure:** randomised per consumer at day 0, 50/50, sticky across sessions and devices. All assigned starters are analysed (intention-to-treat).

### 5.1 Primary metric

Share of assigned starters who **confirm a self-service instalment plan in the portal** and have **no inbound agent contact** (phone, chat, email) linked to the case within 7 days of day 0.
- Baseline: ~32% (planning value, measured before launch).
- Target: +15% relative (~32% → ~37%). This is the goal we report against, not the ship bar (section 7).
- Analysed as the absolute difference B − A in percentage points (pp), with a two-sided 95% confidence interval (unpooled Wald). The p-value and the CI come from the same test, so they cannot disagree.
- **MDE_pp** is computed from the measured baseline and the expected analysable sample on Fri 23 Oct and frozen in this document. Planning value: **+2.7 pp** (≈ +8.5% relative at a 32% baseline, 4,800 per arm).

**Known bias of the 7-day window:** in A the first payment, the reminder and any failed collection fall inside the 7 days; in B they usually fall later. B can therefore look better on the primary metric only because contacts are pushed outside the window. The displacement check (5.4) is a pre-registered Go criterion to rule this out.

### 5.2 Guardrail 1 (plan health)

Share of plans (self-service and agent-assisted) from assigned starters, created within 14 days of day 0, with at least one missed payment among the first two scheduled instalments.
- **Missed** = the instalment is not paid in full within the grace period after its due date (planning value: 5 days, A14).
- **Due dates** are those scheduled at plan confirmation. Later reschedules do not move the measurement point.
- A plan that is **cancelled or revoked before its second due date** counts as missed.
- Baseline: 19% on the old 60-day definition; recalculated on this definition from historical plans (A3).
- Non-inferiority margin: **+3 pp** (Risk/Collections sign-off, A4). Compared against the concurrent control arm, not the historical 19%.
- Analysed as B − A in pp with the upper bound of the one-sided 95% CI.
- A fixed 60-day window is not used: B moves the first payment later, so fewer instalments would be due in the window, biasing the result in B's favour.
- Power: ~2,650 plans per arm expected (46% of ~5,760). The one-sided 95% bound is about ±1.8 pp, so the +3 pp margin is passed with ~85% power if there is no true difference (~80% at the minimum of 2,200 plans per arm).
- **Composition caveat:** this metric is measured over plans, not starters. If B converts more marginal consumers, the plan mix changes. A starter-level version is reported as a secondary metric (5.5) to separate mix effects from real harm.
- **Mechanical caveat:** if A's "today" payment is collected at confirmation, A's first instalment can hardly be missed. This is part of what is being tested and is accepted, but it is reported (share of A plans with first payment collected on day of confirmation).

### 5.3 Guardrail 2 (cash)

Amount collected per assigned starter from the first two scheduled instalments of plans created within 14 days of day 0 (starters without a plan count as €0; same grace period as guardrail 1).
- Captures whether B brings in less money, e.g. because the income-timing step loses consumers or plans pay less.
- Anchored on due dates for the same reason as guardrail 1: a fixed calendar window would penalise B for the later first payment by design.
- Threshold: B ≥ 95% of A (Finance sign-off, A11).
- Analysed as the ratio of means B / A with a bootstrap CI (10,000 resamples, stratified by arm), with CUPED variance reduction using the outstanding case balance at day 0 as covariate.
- **Decision bound:** lower bound of the **one-sided 80% CI** ≥ 0.95. At an assumed coefficient of variation of 1.5 (A17) and ~5,760 per arm, the standard error of the ratio is about 0.028. B then passes with ~80% probability if it truly collects the same as A, and with only ~20% probability if it truly collects 5% less. A point-estimate rule would pass a true 5% loss 50% of the time and is therefore not used.
- Reported decomposed as plans per starter × cash per plan, because more plans can hide lower cash per plan.
- The calendar delay of the first payment is not part of this guardrail. It is covered by the cash-timing sign-off (A16) and reported as a secondary metric.

### 5.4 Displacement check (Go criterion)

Share of assigned starters with any inbound agent contact on the case within **45 days** of day 0.
- The window is the same length in both arms and covers the first due date + 7 days for almost all B plans (latest default first payment ≈ day 36).
- Read at readout 2. **No-go** if the two-sided 95% CI of B − A lies entirely above 0, i.e. B significantly increases total contacts and the primary gain is a shift, not a reduction.

### 5.5 Secondary metrics (reported, not decision gates)

Key secondary, closest to "moment of misery resolved":
- **Plan kept:** share of assigned starters who confirmed a self-service plan, paid both of the first two instalments within grace, and had no inbound agent contact from day 0 until 7 days after the first due date.

Other secondaries:
- Inbound agent contacts per starter in fixed windows: days 0–7, 8–21, 22–45.
- Contact reasons: reassurance or plan questions, date or affordability, consequences of missing a payment (out of scope), documents.
- Guardrail 1 at starter level: share of assigned starters with a plan that missed one of the first two instalments.
- Guardrail 1 restricted to self-service plans.
- Triggered analysis of the primary metric (definition in 5.6).
- Share of consumers who change the default first payment date, per arm, and the distance between chosen date and default.
- Time from day 0 to confirmation.
- Average and distribution of days from plan confirmation to first collection; share of first collections shifted from FY2026 into FY2027.
- All primary and guardrail results broken down by income-timing option in B (day of month, End of month, Middle of month, Every 4 weeks). "Every 4 weeks" earners drift away from a monthly instalment schedule after the first payment, so their second instalment is the most likely place for B to fail.

### 5.6 Definitions used in the decision rule

- **Trigger point:** the step immediately before the plan summary, after income proof upload. Logged in both arms (in A the income-timing screen would appear here). Using the plan summary as trigger would filter on behaviour after B's extra screen.
- **Triggered lift (T):** primary metric B − A among assigned starters who reached the trigger point within 7 days.
- **Incremental drop-off (D):** among starters who reached the trigger point, share who did not reach the plan summary within 7 days, B minus A, in pp. In A this is near 0 because the summary follows directly.

### 5.7 Sample and power check

| Measured primary baseline | Needed per arm for +8.5% relative (80% power, two-sided 5%) |
|---|---|
| 25% | ~6,700 |
| 32% | ~4,800 |
| 40% | ~3,300 |

Expected enrolment: 6 weeks × ~1,920 starters ≈ **11,500 starters, ~5,760 per arm**, i.e. ~20% buffer over 4,800 for exclusions, deduplication of returning consumers and a weaker November. At a 32% baseline this gives an MDE of about +2.5 pp.

**Pre-launch rule (Fri 23 Oct):** compute MDE_pp from the measured baseline and the expected analysable sample.
- MDE_pp ≤ 3.0 pp → launch as planned.
- MDE_pp > 3.0 pp → extend enrolment end (latest Sun 13 Dec, shifting readout 1 by one week). If that still gives MDE_pp > 3.0 pp, move the test to January 2027 or launch only with written acceptance of the larger MDE by the product owner.
- The end date is fixed before launch and is not changed during the test.

## 6. Variant B: Payday Alignment

Four-step flow added at the point of commitment:

1. Income timing: day of the month, or End of month / Middle of month / Every 4 weeks.
2. Recommended first payment date: 2 days after the next income date, at least 5 days from today, with a plain-language explanation.
3. Review: income timing and first payment date shown together; nothing is set up until the consumer confirms.
4. Confirmation: plan set, timing used, reminder before the first payment.

**Date rule (default date only):**
- Default first payment = next income date + 2 days.
- If that date is less than 5 days from today, use the following income cycle.
- "Every 4 weeks" asks for the date income last arrived; the next income date = last date + 28 days (repeated until in the future).
- "Middle of month" = the 15th. "End of month" = the last calendar day of the month.
- A day of month that does not exist in a month (29–31) = the last day of that month.
- The default is capped at the policy maximum for first-payment delay (A13). Cases where the cap applies are logged.
- Due dates on weekends or bank holidays follow the existing collection logic, identical in both arms.
- The 5-day minimum applies to the default only. The date picker and its allowed range are identical to A.

**Treatment package (everything that differs from Control):**

| # | Component | Control A | Variant B |
|---|---|---|---|
| a | Income-timing question | none | one screen before the plan summary |
| b | Default first payment date | today | 2 days after the next income date |
| c | Minimum lead time | none (today) | at least 5 days from today (default only) |
| d | Explanation of the date | none | one plain-language sentence |
| e | Income timing on review and confirmation | not shown | shown next to the date |

These components are tested together and analysed as one treatment (section 0).

**Held constant in both arms:** plan amounts and slider, income information and proof upload, plan summary, review and confirmation screen layout, the date picker and its allowed range, instalment frequency, payment reminder (same channel and same timing relative to the due date), dunning pause after plan confirmation, copy tone, agent entry points, eligibility rules, randomisation unit (consumer ID, sticky across sessions and devices).

## 7. Decision rule (pre-registered)

Rules are evaluated **in the order listed; the first matching rule decides**. Every possible outcome falls into exactly one rule. Thresholds are frozen on Fri 23 Oct and not changed afterwards.

### 7.1 Timeline

| Milestone | Date |
|---|---|
| Launch go/no-go meeting (checklist, section 8) | Fri 23 Oct 2026 |
| Enrolment | Mon 26 Oct – Sun 6 Dec 2026 (6 weeks) |
| Last 7-day window closes | Sun 13 Dec 2026 |
| Readout 1 (primary) | Wed 16 Dec 2026 (2 working days for CRM contact linkage) |
| Interim plan-health check | Mon 15 Feb 2027 |
| Readout 2 (guardrails, displacement) | Mon 15 Mar 2027 |

Readout 2 is fixed: the last guardrail plan is created by Sun 20 Dec; with a maximum first-payment delay of 45 days (A13), its second due date plus grace and settlement falls before mid-March.

### 7.2 Harm stops (during the test)

No early stopping for success. Harm checks only:

- **H1 (weekly, during enrolment):** cumulative 7-day inbound-contact rate among starters whose 7-day window has closed. If B − A > +5 pp (point estimate) → stop B for new starters, revert to A.
- **H2 (Mon 15 Feb 2027):** share of guardrail plans with the first instalment missed. If B − A > +3 pp (point estimate) → stop B for new starters, revert to A.

When B is stopped, existing B plans keep their confirmed dates. Consumers are not asked to re-commit.

### 7.3 Readout 1 (Wed 16 Dec 2026)

Δ1 = primary metric B − A in pp with two-sided 95% CI.

| # | Condition | Decision | Action |
|---|---|---|---|
| 1 | Sample ratio mismatch p < 0.001, or contact linkage check fails (> 2% of inbound contacts in the window not linked to a case) | **Invalid** | Revert to A. No conclusions. Relaunch requires a new pre-registration. |
| 2 | Upper CI bound of Δ1 < 0 | **Kill** (B harms) | Revert to A. |
| 3 | Lower CI bound of Δ1 > 0, and D ≤ 5 pp, and T > 0 | **Provisional Go** | B stays at 50% until readout 2. Starters after 6 Dec are randomised but not analysed. |
| 4 | Lower CI bound of Δ1 > 0, but D > 5 pp or T ≤ 0 | **Iterate** | Revert to A, fix the income-timing screen, plan a new test. |
| 5 | CI of Δ1 includes 0, and upper CI bound ≥ MDE_pp | **Iterate** | Revert to A, plan a follow-up test. Do not extend this test. |
| 6 | CI of Δ1 includes 0, and upper CI bound < MDE_pp | **Kill** | Revert to A. The package cannot deliver a worthwhile effect. |

The +15% target is reported against, not required: a significant lift below +15% can still reach Go.

### 7.4 Readout 2 (Mon 15 Mar 2027, only after Provisional Go)

| # | Condition | Decision | Action |
|---|---|---|---|
| 7 | Guardrail 1: upper bound of one-sided 95% CI of B − A > +3 pp | **No-go** | Revert to A, iterate on the design. |
| 8 | Guardrail 2: lower bound of one-sided 80% CI of B / A < 0.95 | **No-go** | Revert to A, iterate on the design. |
| 9 | Displacement: two-sided 95% CI of B − A (45-day contact rate) entirely above 0 | **No-go** | Revert to A, iterate on the design. |
| 10 | Otherwise | **Go** | B to 100%. |

### 7.5 Release freeze

- **Instalment journey:** frozen from Mon 26 Oct to Sun 13 Dec 2026 (enrolment plus last 7-day window). After that, journey changes no longer affect the analysed cohort.
- **Reminders, collection, dunning and grace logic:** frozen until readout 2 (Mon 15 Mar 2027), because they determine both guardrails.

### 7.6 After a Go

Before the income-timing question is reused in other journeys, run a follow-up test: B vs. "default today + 14 days, same explanation, no income-timing question". Until then, the following exploratory analyses (not causal) are reported:
- Lift in B by distance of the default date from day 0 (≤ 7, 8–20, > 20 days).
- Date-change rate in B vs. A, and where A consumers move the date to.
- In A, where the payday can be read from the uploaded proof of income: plan health of A plans whose chosen date happens to fall within 0–5 days after payday vs. others.

## 8. Launch checklist (all items must be done by Fri 23 Oct 2026)

Launch happens only if every item is done. If an item is not done, the launch moves; the design is not changed to work around it.

| # | Item | Owner | Assumption |
|---|---|---|---|
| L1 | Primary baseline measured on the last 3 monthly cohorts; MDE_pp computed and frozen (section 5.7) | Analytics | A1 |
| L2 | Guardrail 1 baseline recalculated on the due-date definition, source documented | Analytics, Collections | A2, A3 |
| L3 | Written sign-off of the +3 pp margin, the 5-day grace period and the missed-payment definition | Risk / Collections | A4, A14 |
| L4 | Written sign-off of the 95% cash threshold and the 80% one-sided bound | Finance | A11, A17 |
| L5 | Written sign-off of the first-collection delay (maximum average delay, FY2026 → FY2027 shift, one-off timing dip at rollout) | Finance | A16 |
| L6 | Policy maximum for first-payment delay confirmed; dunning, interest and escalation timers confirmed paused identically in both arms | Collections, Legal | A13, A15 |
| L7 | Data protection check for collecting income timing (purpose, retention, privacy notice text) | Data Protection Officer | A19 |
| L8 | Guardrail 2 variance estimated from historical first-two-instalment collections; power ≥ 70% confirmed or threshold re-agreed with Finance | Analytics | A17 |
| L9 | Tracking verified end to end in staging: assignment, trigger point, income-timing screen, plan summary, confirmation, due dates, payments, CRM contacts with case ID and reason tag; CRM linkage lag ≤ 2 working days | Engineering, Analytics | A8, A18 |
| L10 | Real weekly starter volume confirmed (≥ 1,600 analysable starters per week, otherwise section 5.7 rule applies) | Analytics | A6 |
| L11 | Date rule edge cases tested (29th–31st, February, Every 4 weeks, cap at policy maximum) | Engineering, QA | section 6 |
| L12 | Release freeze agreed for journey and for collection logic (section 7.5) | Engineering, roadmap owner | A9 |

## 9. Working assumptions

All values below are assumptions for planning, in line with the fictional M1 baseline. Each is confirmed or replaced via the launch checklist (section 8), and the affected numbers in sections 5–7 are updated before Fri 23 Oct.

| # | Open point | Assumption | Rationale | Validate by |
|---|---|---|---|---|
| A1 | Primary-metric baseline | **32%** of journey starters complete a self-service plan without agent contact within 7 days. | Planning value from 46% × 69%. That calculation assumes independence of agreement and contact, which is unlikely; the possible range is 15–46%. A lower real baseline needs a larger sample (section 5.7). | Funnel data joined with contact-centre data for the last 3 monthly cohorts (L1). |
| A2 | Source of the 19% guardrail baseline | 19% comes from an internal Collections portfolio report on plans created in the last 12 months (fictional, like the M1 volumes). | The AI synthesis showed it does not come from the interview quotes; treating it as a portfolio KPI is the most plausible origin. | Collections / Risk reporting (L2). |
| A3 | Guardrail baseline on the new definition | **19%** of plans miss at least one of the first two instalments. | With monthly instalments, a 60-day window from plan creation covers about the first two due dates, so the old and new definitions are close. | Recalculate on historical plans using due dates, grace period and cancellation rule from section 5.2 (L2). |
| A4 | Non-inferiority margin | **+3 percentage points** is accepted by Risk/Collections. | At ~3,850 plans per month, +3 pp means ~115 more broken plans per month, i.e. ~€21k recovery at risk per month (€600 × 30% loss, see problem hook) or ~€0.25M per year. That is small compared with the ~€3.8M per year recovery from additional agreements the initiative targets. | Sign-off with Risk/Collections (L3). |
| A5 | Drop-off threshold at the income-timing screen | Incremental drop-off **≤ 5 pp** (definition in section 5.6). | It is one dropdown or quick option with no document upload. The heavy step is income proof upload (32.8% of all drop-offs), which stays unchanged in both arms. | Read at readout 1; tracked weekly as a diagnostic. |
| A6 | Real volumes | **~8,360** journey starters per month (~1,920 per week), all eligible starters enter the test. | Fictional M1 baseline. 6 weeks give ~20% buffer over the required sample. | Portal analytics (L10). |
| A7 | Statistical power | 80% power, 5% significance (two-sided for the primary metric, one-sided for guardrail 1); one-sided 80% bound for guardrail 2. | Standard values for primary and guardrail 1. Guardrail 2 uses 80% because amounts are too skewed for a 95% bound at this sample (section 5.3). | Design decision; guardrail 2 bound signed off by Finance (L4). |
| A8 | Tracking | The CRM logs every inbound contact (phone, chat, email) with the case ID and a reason tag, and the portal events (including the trigger point in both arms) are built in the same sprint as the feature. | Without case-level contact data the primary metric cannot be measured; the PRD lists tracking as a Must. | Test run in staging through both arms, all events end to end (L9). |
| A9 | Release freeze | Journey frozen 26 Oct – 13 Dec 2026; reminders, collection, dunning and grace logic frozen until 15 Mar 2027. | Changes to the journey after the last 7-day window do not affect the analysed cohort; changes to collection logic would affect both guardrails. | Agreed with engineering and the roadmap owner (L12). |
| A10 | Timeline | See section 7.1. | 6 weeks cover at least one full pay cycle with buffer. Calendar effects: November payslips often include a Christmas bonus, and B's first instalments fall more often into post-Christmas January than A's. Both are part of the comparison, but the result may not transfer one-to-one to an average month. | Re-plan if any checklist item is not done by Fri 23 Oct. |
| A11 | Cash guardrail threshold | Finance accepts B down to **95%** of A in amount collected per starter from the first two instalments. | Only lost money counts against B in this guardrail; later money is handled by A16. | Sign-off with Finance (L4). |
| A12 | Date editability | The consumer can change the default first payment date in both arms, with the same date picker and range. | Matches the current journey; B changes the default and the explanation, not the control. | Confirm with product/engineering; track the share of changed dates per arm. |
| A13 | Policy maximum for first-payment delay | **45 days** from plan confirmation; B's default (at most ~36 days) stays below it. | Needed so B does not schedule dates that Collections policy does not allow, and to fix the readout 2 date. | Collections policy, Legal (L6). |
| A14 | Missed-payment definition | Not paid in full within **5 days** after the due date; cancellation before the second due date counts as missed. | Without a fixed definition the guardrail can be argued either way after the fact. | Sign-off with Risk/Collections (L3). |
| A15 | Case status between confirmation and first payment | Dunning, interest and escalation timers are paused after plan confirmation, identically in both arms. | B's longer gap must not trigger extra dunning letters or escalations. | Collections, Legal (L6). |
| A16 | First-collection delay | Finance accepts an average delay of up to **30 days** to first collection, the shift of part of the test cohort's first collections from FY2026 into FY2027, and a one-off timing dip of about one cycle of first instalments at rollout (~3,850 plans × average first instalment). | Makes "accepted by design" a signed decision instead of an assumption. | Sign-off with Finance (L5). |
| A17 | Guardrail 2 variance | Coefficient of variation of cash per starter ≈ **1.5**. | Zero-inflated (54% of starters have no plan) and skewed amounts. Determines the ~80% power stated in section 5.3. | Historical first-two-instalment collections (L8). |
| A18 | CRM linkage lag | Inbound contacts are linked to the case within **2 working days**. | Readout 1 on Wed 16 Dec relies on this. | Staging test and historical lag check (L9). |
| A19 | Data protection | Collecting income timing is covered by the existing purpose for affordability assessment; privacy notice text updated. | It is new personal data in the journey. | Data Protection Officer (L7). |
