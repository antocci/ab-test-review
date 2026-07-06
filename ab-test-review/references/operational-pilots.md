# Operational Pilots And Constrained Designs

Load this reference for pilots of operational strategies (calls, letters, contact policies, AI vs human delivery), human-in-the-loop or AI-agent treatments, cluster/switchback/geo/quasi designs, capacity-constrained settings, delayed outcomes, or regulated communications.

Operational pilots are still controlled experiments. The difference is that the treatment is delivered by people or agents rather than code, the arms can leak into each other through shared operations, outcomes mature slowly, and mistakes touch real customers in regulated channels. Review the comparison, not the ceremony.

When reporting, collapse this reference into the single optional "Operational pilot" gradecard row: grade the weakest stage-critical aspect across the sections below and name it in the one-line reason.

## Core Review Questions

- What strategy decision does this pilot inform, and what is the conservative fallback if the treatment underperforms?
- Why this control: previous strategy, most conservative option, or do-nothing — and does it protect the downside for high-stakes treatments?
- Can the two arms actually stay different in practice, and who or what guarantees treatment fidelity?
- Through which shared resources (operators, queues, capacity, budgets, customer households) can arms affect each other?
- When do outcomes mature, and does the test duration and readout window respect that?
- What can the treatment do to a customer that the control cannot, and is that within policy and regulation?

## Control And Holdout Choice

Grade the design higher when the control choice is an explicit risk decision.

- Control as the previous strategy answers "is the new strategy better than what we do today" — the usual pilot question.
- Control as the most conservative option (e.g., human operator call when testing an AI caller) is appropriate when the treatment's downside is plausible and costly; say so in the doc.
- A per-test control is sufficient for per-test decisions. The absence of a global or long-term holdout is context, not automatically a finding — flag it only when the team makes cumulative or long-term claims ("our strategy changes added X% this year") that only a holdout could support.
- Champion/challenger ramps and unequal splits are fine when sized honestly; grade the power math at the actual split.

Red flags:

- Control arm silently receives partial treatment (spillover through shared scripts, retrained operators, or shared queues).
- Control is a strawman: an outdated or deliberately weakened version of the current strategy.
- "No effect vs control" claimed at a split and duration that could not detect a decision-relevant effect.

## Randomization Under Operational Constraints

Review the unit against how the treatment is delivered:

- If operators deliver both arms, contamination through learning and habit is likely — prefer randomizing operators/teams, or name and monitor the contamination path.
- Cluster randomization (operator, team, branch, region, day) shrinks effective sample size; power and variance must be computed at the cluster level, not the row level.
- Customer- or account-level randomization must respect households, linked accounts, and repeated contacts — one person hit by both arms is a defect.
- Switchback (alternating periods) suits capacity-constrained or queue-shared settings; check period length against carryover.
- Stratify or block on strong prognostic variables (debt size, delinquency bucket, region) when samples are small; small pilots live or die on variance control.

## Quasi-Experiments

When randomization is genuinely infeasible, grade the fallback on honesty, not on failing to be an RCT.

- Pre/post needs stability arguments: seasonality, mix shift, and concurrent changes addressed, ideally with a comparison group (diff-in-diff).
- Geo or site splits need comparability evidence and, where possible, pre-period balance.
- Matched cohorts need the matching variables, the unmatched tail, and the residual-confounding caveat stated.
- Any quasi design must carry a visible causal-strength caveat in the readout; presenting a pre/post delta with an RCT-grade tone is a finding.

Grade anchors for the optional row:

- F: arms contaminated, treatment fidelity unknown, or a quasi design presented as causal proof.
- D: constraints acknowledged but not designed around; row-level power math on clustered delivery.
- C: unit and control choices defensible; contamination and maturity named but weakly handled.
- B: contamination paths monitored, cluster-aware analysis, maturity window respected, fidelity evidence collected.
- A: constraint-driven design argued end to end — control protects downside, fidelity measured, interference bounded, delayed outcomes built into duration and readout.

## Delayed And Maturing Outcomes

Collections-style outcomes (payments, cures, recoveries) mature over weeks or months.

- Define the outcome window in the design (e.g., recovery within 60 days of first contact) and hold the readout to it.
- Early proxy metrics (contact rate, promise-to-pay) may steer in-flight decisions but must not silently replace the primary outcome in the readout.
- Cohort entry over time means late entrants have immature outcomes at readout — require maturity-aligned cohorts or explicit truncation handling.
- Watch for treatments that shift timing rather than totals (pulling payments forward looks like uplift in a short window).

## AI-Agent Treatments

When the treatment is an AI caller, AI-written messages, or an agent-driven strategy:

- Version the treatment: model, prompt, and script versions logged per contact; a mid-test prompt rewrite is a treatment change and belongs in the change log — large changes may reset the test.
- Monitor treatment quality as a guardrail (complaint rate, escalation rate, compliance flags, conversation quality sampling), not only the primary outcome.
- Compliance is a first-class guardrail in regulated communications: disclosure requirements, contact-time rules, prohibited language; a compliance breach is a critical finding regardless of uplift.
- Human-comparison fairness: the AI and human arms should face comparable case mix and routing; selective routing of easy cases to the AI arm is a validity defect.
- Define degradation behavior: what happens when the AI fails mid-call, and does the fallback leak the customer into the other arm's treatment.

## Human Factors

- Hawthorne and novelty effects: operators and customers behave differently early; prefer durations that outlive novelty, or say the readout measures the novelty period.
- Operator buy-in asymmetry: an arm delivered by skeptical or overloaded staff measures morale, not strategy — collect fidelity evidence.
- Incentives: if bonuses or targets differ across arms, the comparison is confounded.
