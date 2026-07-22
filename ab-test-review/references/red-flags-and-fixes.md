# Red Flags And Fixes

Use this file to prioritize. A finding is useful when it explains why the gap matters and what concrete next action reduces risk.

## Critical Red Flags

- No decision the test can change; the pilot exists to confirm a choice already made.
- No control group, or a control that received partial treatment (contaminated arms).
- Unhandled SRM: arm sizes deviate from the design and the readout proceeds anyway.
- Primary metric, population, or analysis switched after seeing results, without disclosure.
- Early stop on a good p-value under a fixed-horizon plan, presented as a valid result.
- Underpowered test presented as evidence of "no effect" for a decision-relevant effect size.
- Unit-of-analysis mismatch: clustered delivery analyzed at the row level, producing fake precision.
- Guardrail breach (complaints, compliance, customer harm) observed with no response despite a threshold.
- Treatment exposes customers to non-compliant, deceptive, or harmful behavior in a regulated channel.
- Readout of a quasi-experiment presented with causal certainty and no design caveat.

## Major Red Flags

- Hypothesis exists, but win/loss/flat actions and antigoals are absent.
- Metrics copied from a template without mapping to the business decision.
- No guardrail metrics, or guardrails without thresholds and owners.
- Power/MDE math absent, or computed at the wrong unit, or MDE not tied to a decision-relevant effect.
- Duration chosen by calendar convenience, ignoring weekly cycles, novelty, or outcome maturity.
- Exposure logging assumed rather than verified; arms not reconstructable from data.
- Peeking without a sequential design or correction; dashboards treated as significance tests.
- Segment results reported without multiplicity discipline; significant cuts cherry-picked.
- Ratio metrics analyzed without matching the randomization unit (delta method, bootstrap, or user-level aggregation).
- Mid-test treatment changes (scripts, prompts, ramp) not logged or not assessed for impact.
- Delayed outcomes read out before maturity; early proxies silently promoted to primary.
- Ownership is a team name, not a responsible owner with stop/extend authority.
- Prior related tests ignored; the pilot re-learns a known result at customer expense.
- Question does not need an experiment: the effect is obvious, the decision is cheaply reversible, or existing data already answers it — traffic or capacity spent for no incremental information.
- Primary metric is a movable local proxy (clicks, opens, a single funnel step) not shown to track the business outcome it stands in for; a "win" can be gamed without moving value.
- Result generalized into a business belief beyond the tested population, market, or time window, with no boundary stated and no causal mechanism named to carry it.

## Validity Checklist

Walk this list when grading randomization, instrumentation, or analysis — against the design's claims and, when results are available, against the actual logs and analysis code. Classify confirmed items per the Severity section in SKILL.md: invalid comparisons are critical, weaker rigor gaps are major.

- Assignment is random at the stated unit, and the mechanism is verifiable (seedable code, platform record), not manual list-splitting.
- SRM check: observed arm ratio matches design within statistical tolerance; investigated before any readout claim.
- No unit straddles arms: same customer, household, or linked account never receives both treatments.
- Exposure defined consistently: analysis population is those exposed (or intent-to-treat, stated), symmetric across arms.
- Filters, exclusions, and joins applied identically to both arms; dropped-data rates compared across arms.
- Variance treatment matches the design: cluster-robust for cluster randomization, delta method or equivalent for ratio metrics, CUPED or stratification honestly reported if used.
- Fixed-horizon vs sequential policy stated and honored; any peeking is either corrected or decorative.
- Multiple comparisons across metrics and segments handled (hierarchy, correction, or explicitly exploratory labeling).
- Outcome maturity respected: readout window matches the design's outcome definition; late cohorts truncated consistently.
- Twyman's law applied: surprising results (huge uplift, impossible direction) investigated for bugs before celebration.
- External events and seasonality during the test window checked for asymmetric impact.
- Treatment fidelity verified: the treatment delivered matches the treatment designed (scripts followed, AI version stable, letters actually sent).

For operational pilots, AI treatments, and quasi designs, also check `operational-pilots.md`.

## Low-Hanging Fixes

- Add a one-paragraph plain-language statement: decision, hypothesis, and what each outcome would trigger.
- Add a win/loss/flat action table with the decision owner.
- Add a metric table: business goal, primary metric, guardrails, maturity window, expected direction, owner.
- Add power math at the correct unit: MDE, alpha/beta, per-arm N, duration; a spreadsheet is enough.
- Add an SRM check and a pre-launch instrumentation dry run (one day of exposure logs inspected).
- Add stopping rules: fixed horizon or sequential design, plus guardrail-breach kill criteria with an owner.
- Add a mid-test change log template: date, change, arms affected, expected impact.
- Replace row-level analysis with cluster-aware analysis where delivery is clustered.
- Pre-declare segment cuts (3-5 that would change the decision) and label everything else exploratory.
- Add a maturity-aligned readout date to the calendar at design time, so nobody reads out early by accident.
- Add a treatment-fidelity check: sample calls/letters/transcripts per arm on a schedule.
- Record the design in a findable place before launch; a one-page pre-registration beats a perfect doc after results.
- Before designing, write one line: why this needs an experiment, and what the cheapest alternative (prior test, existing data, an obvious call, a reversible launch) would cost instead.
- State the generalization boundary in the readout: which population, market, and time window the result is claimed to hold for, and the mechanism you believe carries it there.

## Fix Plan Ordering

Prefer this sequence:

1. Stop invalid or misleading comparisons (contamination, SRM, unit mismatch, post-hoc switches).
2. Fix the decision link and test-worthiness: hypothesis, primary metric as the real lever (not a movable proxy), win/loss/flat actions, and whether the question needs an experiment at all.
3. Fix power, duration, and outcome maturity so the test can answer its question.
4. Add instrumentation verification and analysis-plan pre-registration.
5. Add guardrails, stopping rules, ownership, and change-log discipline for launch and in-flight.
6. Only then polish: extra segments, secondary metrics, prettier readouts.
