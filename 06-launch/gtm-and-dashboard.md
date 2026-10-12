# GTM Launch Plan, Riverty business-unit case

| Field | Value |
|---|---|
| Feature | Payday Alignment |
| Goal | Conversion |
| Launch tier | M, Targeted |

## Goal & Audience
- **Goal:** Conversion, Payday Alignment is an in-journey change, tested as an A/B experiment, not a market launch. Consumers meet it at the moment of commitment, so awareness adds nothing and external promotion would bias who enters the test. The goal is to move a business metric: self-service plans without agent contact within 7 days from ~32% to ~37%, without raising missed payments by more than 3 pp or reducing cash per starter below 95% of control. The GTM work is mainly internal: Risk, Finance, Legal and client management sign off the thresholds before launch, agents are briefed to handle both arms identically and tag every contact, and management commits to the pre-registered decision rule.
- **Target audience:** Primary (external): consumers in collection who start the instalment journey in the self-service portal, cannot pay in full and have variable or irregular income (persona Mara). Reached in-product only; no campaign during the test. Secondary (internal): contact-centre agents and team leads (handle both arms identically, tag contacts by reason); Risk/Collections and Finance (sign-off of margins and cash timing); client management (creditor contracts and remittance timing); Legal and data protection (income-timing data, consumer copy).

## Launch Tier
- **M, Targeted**, M, targeted internal comms, no external outreach. Reach: an in-journey change for ~8,360 journey starters per month, ~4,180 of them in the variant during the 6-week test; consumers learn about it in the product, so a campaign would add nothing and would bias who enters the test. Revenue impact: the initiative targets ~€3.8M per year in additional recovery, while up to ~€0.25M per year is at risk if missed payments rise by the +3 pp margin, and the variant shifts first collections later (partly from FY2026 into FY2027). Risk of silence is internal: agents who are not briefed override the recommended date or mis-tag contacts, which breaks the primary metric; Finance is surprised by the cash timing; creditor contracts on first-payment delay may be breached; Legal and data protection have not cleared the new income-timing question. Comms therefore go to a small, defined set of internal groups (contact centre, Risk/Collections, Finance, client management, Legal/DPO, engineering/payment operations, management), each with a clear ask and deadline before launch on 26 Oct.

## Channels
1. **Owned: In-product: the self-service instalment journey itself. The income-timing question, the recommended first payment date with one plain-language sentence explaining why, and income timing shown on review and confirmation. This is where Mara actually is at the moment of commitment; every variant starter sees it, no other consumer touchpoint changes (payment reminder and dunning letters stay identical in both arms).**
2. **Owned: Contact-centre enablement: briefing sessions for agents and team leads, knowledge-base article and call guidance in the agent desktop/CRM. Agents are the fallback Mara calls for reassurance; they must handle both arms identically, not override the recommended date, and tag every inbound contact with case ID and reason, otherwise the primary metric cannot be measured.**
3. **Owned: Internal stakeholder channel: launch one-pager and sign-off meeting (go/no-go Fri 23 Oct) for Risk/Collections, Finance, client management, Legal/data protection and management, followed by a weekly test status update (harm checks) and the fixed readouts on 16 Dec, 15 Feb and 15 Mar. Keeps sign-offs explicit and avoids surprises in cash forecasts and creditor reporting.**

## Enablement & Assets
Contact centre: 30-minute briefing before 26 Oct, FAQ and call guidance ("what the variant looks like, why the date is recommended, how to handle date questions, same treatment in both arms"), new CRM reason tags (reassurance/plan, date/affordability, consequences, documents), knowledge-base article. Risk, Finance, client management, management: one-page launch brief (what changes, thresholds, decision rule, timeline), Finance note on first-collection timing and FY2026 → FY2027 shift, client-management note on creditor contracts and remittance timing, decision-rule sheet signed off before launch. Complaints handling: short note that a test is running and how to flag date-related complaints. Product/legal: final consumer copy (income-timing question, explanation sentence, review/confirmation), updated privacy notice text. Monitoring: weekly harm-check dashboard (7-day contact rate by arm, drop-off at the income-timing screen, sample ratio).

## Ownership, Budget & Timeline
- **Ownership & budget:** Waldemar Brunkov, PM Owns the GTM plan, the launch go/no-go meeting on Fri 23 Oct, the pre-registered decision rule and all readouts (16 Dec, 15 Feb, 15 Mar). Owns the launch one-pager and the weekly status update to stakeholders.

Eveline, Engineering Lead Owns the feature build, tracking implementation, date-rule edge cases and the release freeze (journey until 13 Dec, reminders/collection/dunning until 15 Mar). Runs the production smoke test on 26 Oct.

Dimitar, Analytics Lead Owns the baseline measurement, the MDE freeze before launch, the weekly harm-check dashboard and the analysis for all readouts.

Tanja, Contact Centre Lead Owns the agent briefing, the FAQ and call guidance, and the correct use of the new CRM reason tags. Makes sure agents handle both arms identically.

Nils, Risk/Collections Lead Signs off the +3 pp margin, the grace period and the first-payment policy maximum. Owns the interim plan-health check on 15 Feb.

Michael, Finance Controller Signs off the 95% cash threshold and the later first collection (incl. FY2026 → FY2027 shift). Updates the cash forecast.

Janos, Client Manager Checks creditor contracts for limits on first-payment delay and informs creditors about remittance timing where needed.

Alexander, Legal / Data Protection Officer Clears the income-timing question, the privacy notice text and the consumer copy.

Andre, Complaints Lead Briefs the complaints team that a test is running and flags date-related complaints to the PM.

Budget No external spend (no paid or earned channels). Internal cost only: ~30 minutes of agent time for the briefing, CRM configuration for the new reason tags, and the tracking work already planned in the feature sprint.

Asset gaps to close before launch CRM reason tags, harm-check dashboard, final consumer copy, updated privacy notice text.
- **Timeline:** Phase 1, readiness (Mon 12 – Fri 23 Oct): baseline measured and MDE frozen; written sign-offs from Risk, Finance, client management and Legal/DPO; end-to-end tracking test in staging; date-rule edge cases tested; agent briefing, FAQ and CRM tags live; launch one-pager shared. Go/no-go meeting Fri 23 Oct; if any item is missing, launch moves. Phase 2, launch (Mon 26 Oct – Wed 16 Dec): variant live for 50% of journey starters on 26 Oct, production smoke test with test accounts on day 1; journey freeze until 13 Dec; weekly harm check and status update to stakeholders; enrolment ends Sun 6 Dec; primary readout Wed 16 Dec (Kill, Iterate or Provisional Go per pre-registered rule). Phase 3, post-launch (Dec 2026 – Mar 2027): on Provisional Go the variant stays at 50%; freeze on reminders, collection and dunning until 15 Mar; interim plan-health check Mon 15 Feb; guardrail readout Mon 15 Mar. On Go: rollout to 100%, update agent guidance, inform client management and Finance of the full rollout, plan the follow-up test (B vs. "today + 14 days, no income question"). On No-go: revert to A and iterate.

## Success Metrics
- **Metrics:** Primary: share of journey starters who complete a self-service instalment plan with no inbound agent contact within 7 days (target ~32% → ~37%; ship bar: significant lift, 95% CI lower bound > 0).
Plan health guardrail: share of plans with a missed payment among the first two instalments; B − A must stay ≤ +3 pp (one-sided 95% upper bound).
Cash guardrail: amount collected per journey starter from the first two instalments; B / A ≥ 0.95 (one-sided 80% lower bound).
- **Bad signal to watch for:** 7-day agent contacts fall, but contacts within 45 days rise: calls were shifted past the window, not removed. Also: drop-off at the income-timing screen > 5 pp, or most consumers overriding the recommended date.
- **Likely post-launch decision:** Iterate. Trigger: at readout 1 (16 Dec) the lift is positive but not significant and the CI still includes the MDE (+2.7 pp), guardrails hold → revert to A, test the next version (e.g. combined with the low-month confidence check). Double-down only if all Go criteria hold on 15 Mar; deprioritize if the CI's upper bound is below +2.7 pp.
