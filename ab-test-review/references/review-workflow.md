# Review Workflow

## Classify First

Before grading, name:

- Evidence mode: design and results, design-only, or results-only (see SKILL.md Mandatory First Step).
- Test stage: idea/hypothesis, test design, launch-ready, in-flight, readout, post-decision.
- Test type: individually randomized A/B(/n), cluster-randomized (operator, team, branch, region), switchback, champion/challenger ramp, holdout, geo split, pre/post, matched cohorts / quasi-experiment.
- Treatment and control: what exactly differs between arms, and what the control represents (previous strategy, most conservative option, do-nothing).
- Unit of randomization vs unit of analysis vs unit of treatment delivery (customer, account, call, operator, day, region) — mismatches are a classic validity threat.
- Decision this test informs, decision owner, and what happens on win / loss / flat.
- Worst-case mistake and blast radius: shipping a harmful strategy, killing a good one, exposing customers to a non-compliant or degrading treatment.
- Available evidence: design doc, hypothesis log, assignment/exposure logs, dashboards, notebooks, readout deck, monitoring, mid-test change log, prior related tests.
- Operational-pilot triggers: human-in-the-loop delivery, AI-agent treatments, capacity constraints, shared queues, delayed outcomes, regulated communications.

Scale rigor to stage. A hypothesis sketch needs decision framing, treatment definition, a plausible primary metric, and a feasibility read. A readout needs validity checks, pre-registered analysis, uncertainty, and a decision recommendation.

## Evidence Pass

Read enough to answer these questions before judging:

- What decision is this test supposed to inform, and who owns it?
- Does this question need an experiment at all, and what is the cheapest credible way to answer it?
- What is the current strategy, and what exactly does the treatment change?
- What is the primary metric, what are the guardrails, and how do they map to business value?
- What is the unit of randomization, and can units in different arms affect each other?
- How were sample size, MDE, and duration chosen — and were they honored?
- How is assignment implemented and verified (SRM check, exposure logging, A/A evidence)?
- What was the analysis plan before results existed, and does the readout follow it?
- What changed mid-test (treatment tweaks, AI prompt versions, script edits, ramp changes), and is it recorded?
- Where do the results artifacts contradict or extend the design doc?
- Which numeric claims can be recomputed from the artifacts themselves (arm counts for SRM, baseline and N for power/MDE, estimates for CIs and reconciliation)? Recompute them per `verification-computations.md` rather than trusting the doc.

Prefer evidence in this order: assignment/exposure logs and analysis code, dashboards and experiment-platform records, the design doc, readout decks, memos, issue/PR discussion, remembered context.

## Design Doc Gate

The gate applies only when results are under review, the user has not provided a design doc, and none is found among the artifacts. A user-provided design plus results is design-and-results mode; a standalone design with no results is design-only mode — neither triggers the gate. Ask before continuing:

```text
I don't see a test design doc for this readout. Is it in Google Docs, Confluence, Notion, an experiment platform, or elsewhere? If no design doc exists, say so and I'll review results-only with explicit assumptions and post-hoc-analysis risk flagged.
```

Do not infer that no design exists just because it is absent from the provided files. If the user confirms none exists, continue in results-only mode and clearly mark inferred assumptions. When running unattended and no user can answer, do not block: proceed and put the missing-design caveat at the top of the report.

## Grade And Triage

Use `rubrics.md` for letter grades. Do not let the gradecard bury the review. After grading, rank findings by severity and leverage:

- What invalidates or blocks a trustworthy decision?
- What is the cheapest high-impact improvement?
- What uncertainty would change the design or the decision if answered?
- What good choices should not be rewritten away?

## Review Lenses

- Decision framing: hypothesis, decision informed, success criteria, antigoals, what happens on flat.
- Test-worthiness and alternatives: does this question need an experiment at all, is there a cheaper or faster way to learn it (prior tests, existing data, an obvious call, a reversible launch), is the primary metric the real business lever or a movable proxy, which competing hypotheses would the result fail to separate, and what is the opportunity cost of the traffic or capacity the test consumes. Stay inside the experiment framework — this challenges whether to test, not whether the business idea itself is good.
- Treatment and control: exact difference between arms, control choice rationale, treatment fidelity plan.
- Randomization: unit choice, assignment mechanism, stratification, interference/spillover, contamination paths.
- Metrics: primary metric, guardrails, OEC/business mapping, delayed-outcome handling, ratio-metric analysis units.
- Power: MDE tied to a decision-relevant effect, alpha/beta, sample and duration math, ramp plan.
- Instrumentation: exposure logging, SRM checks, A/A or pre-experiment balance evidence, data joins.
- Analysis: pre-registration, peeking policy, multiple comparisons, CIs, segment analysis discipline, variance handling for clustered or ratio metrics.
- Risk: cost of each mistake direction, compliance/ethics of the treatment, guardrail breach response, kill switch.
- Operations: ramp/stop rules, in-flight monitoring, owner, mid-test change log.
- Learning: readout quality, the result-to-belief leap (generalization boundary and carrying causal mechanism, not just a p-value), generalization limits, knowledge capture, follow-up tests.

For operational pilots, AI-agent treatments, and constrained designs, also apply `operational-pilots.md`.

## Output Discipline

- Findings ordered by severity, immediately after the gradecard; do not bury them in coverage.
- Include evidence references when reviewing files.
- A finding backed by a recomputation states its inputs and method; a verified numeric contradiction outranks any stylistic finding of the same severity.
- Phrase recommendations as concrete changes, not abstract advice.
- Separate blockers from improvements; for pre-launch reviews, separate launch blockers from nice-to-haves.
- Include praise only when tied to a specific design mechanism.
- Include an author verdict only after the technical verdict is supported by evidence.
- Every review opens with the Scorecard (`output-templates.md`); the verdict follows from the gradecard average per that template, and the comments never contradict the scorecard.
- The book-backed takeaway on the scorecard is a short lesson the team can reuse.
