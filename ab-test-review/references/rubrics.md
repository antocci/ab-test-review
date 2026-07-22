# Rubrics

Use letter grades. A grade is a review aid, not the review itself.

Global anchors:

- A: specific, evidence-backed, decision-useful, and tied to tradeoffs.
- B: reviewable and plausible, with enough evidence to support a decision, but with remaining rigor or operational gaps.
- C: named and directionally reasonable, but incomplete, generic, or weakly supported.
- D: shallow label with little mechanism; the team would mostly be deciding from assumptions.
- F: missing, invalid, contradictory, or too vague to review.

Use `+` or `-` for meaningful nuance:

- Add `+` when a section exceeds the anchor on stage-critical evidence.
- Add `-` when a material caveat could change the decision.
- Avoid `A+` unless the artifact has verified assignment integrity, an honored pre-registered analysis, and a captured learning loop.
- The verdict is computed from the gradecard average per `output-templates.md`. The average never hides risk: stage-critical `F`/`D` grades and critical findings must still lead the findings.

## Base A/B Gradecard

Eleven dimensions. This table is the single source for the base gradecard rows: report one row per dimension, in this order. Operational pilots and constrained designs add one optional row, graded per `operational-pilots.md`. Within a merged dimension, grade the weakest stage-critical facet and name it in the one-line reason. Templates may also use `n/a (stage)` for stage-irrelevant dimensions and `not fairly gradeable` in results-only mode; these are explicit non-grades, not letter grades.

| Dimension | F | D | C | B | A |
|---|---|---|---|---|---|
| Hypothesis & decision framing | Starts with "let's test X"; no decision or success criteria | Vague hypothesis; generic goals | Hypothesis, decision informed, and a measurable success criterion named | Decision owner, win/loss/flat actions, and scope exclusions are clear | Causal hypothesis with expected mechanism, quantified stakes, antigoals, and what result would change which decision |
| Test-worthiness, alternatives & opportunity cost | Test exists by default; no case that the question needs an experiment; no alternatives or cost of the test itself considered | Reason to test asserted generically ("we should validate"); no cheaper learning path or competing hypotheses weighed | Test-worthiness argued; at least one cheaper signal or alternative named, but not seriously compared | Answer's decision value weighed against the test's cost (traffic, capacity, time); cheaper learning paths (prior tests, existing data, an obvious call, a reversible launch) ruled out; competing hypotheses acknowledged | Expected information value vs opportunity cost reasoned explicitly; the primary metric is shown to be the real business lever, not a movable local proxy; competing hypotheses enumerated with what result would separate them; a "no experiment needed" branch considered and rejected for a stated reason |
| Treatment, control & baseline | Arms not precisely defined; control absent or unclear | Arms named without exact difference; control choice unexplained | Exact treatment/control difference stated; control choice plausible | Control rationale explicit (previous or conservative strategy); confounding differences between arms controlled | Single isolated difference or acknowledged bundle; treatment fidelity plan; control protects downside for high-stakes treatments |
| Randomization unit & assignment | No randomization or unit unstated; assignment ad hoc | Unit named; assignment mechanism and integrity unaddressed | Unit fits the treatment; assignment mechanism described | Unit choice defends against interference; assignment implementation and exposure logging described | Unit vs analysis vs delivery alignment argued; interference paths named and handled; stratification or cluster handling where needed |
| Metrics: primary, guardrails & OEC | No primary metric, or a metric the treatment cannot plausibly move | Primary metric named; no guardrails or business mapping | Primary metric tied to the decision; some guardrails | Primary + guardrails with business mapping; delayed-outcome window stated | OEC or explicit tradeoff rule; guardrails with breach responses; metric sensitivity and maturity window justified |
| Power, MDE & duration | No sizing; duration arbitrary | "Run for two weeks" without math | Sample/duration estimated; MDE named | MDE tied to a decision-relevant effect; alpha/beta stated; duration covers cycles and maturity | Power analysis with realistic variance (clustered if clustered), ramp plan, and a pre-committed rule for extending or calling it |
| Instrumentation & data quality | Exposure not logged; arms not reconstructable | Logging assumed; no balance or SRM checks planned | Exposure logged; SRM check named | SRM/balance checks run and passed; joins and filters validated symmetric across arms | A/A or pre-period balance evidence; data-quality checks pre-launch; asymmetric loss/exclusion paths audited |
| Analysis plan & statistical rigor | No plan, or analysis invented after seeing results | Plan is "check significance"; peeking uncontrolled | Test statistic and CI approach named; peeking policy stated | Pre-registered plan honored; multiple comparisons and segment discipline handled | Variance treatment matches design (cluster/ratio/CUPED where relevant); sequential or fixed-horizon policy explicit; deviations disclosed and justified |
| Risk, ethics & guardrail response | Harmful/non-compliant exposure possible with no safeguards | Risks mentioned generically | Concrete failure modes of the treatment named | Mistake costs per direction tied to customer/business harm; compliance addressed for regulated treatments | Asymmetric costs drive design (conservative control, capped exposure); breach thresholds with owners and kill switch |
| Rollout, monitoring & stopping rules | Launch and stop are improvised | Start/end dates only | Ramp or start plan; someone watching | Stopping/extension rules, in-flight health checks, and owner named | Ramp with health gates, pre-committed stop/extend/kill rules, mid-test change log discipline |
| Readout, decision & learning capture | Results asserted without validity checks or uncertainty | Point estimates and a p-value; no interpretation limits | CIs and validity checks reported; decision recommendation present | Readout follows the plan; surprises investigated (Twyman); generalization limits stated | Decision recommendation with uncertainty and segments handled honestly; the leap from result to business belief is pressure-tested — generalization boundary (population, market, time) and the carrying causal mechanism stated rather than assumed; learning captured for reuse; follow-up tests proposed where warranted |

## Verdict Mapping

The verdict (approve | approve with concerns | needs improvement) is read off the gradecard average; the point mapping and bands live in `output-templates.md`. `n/a (stage)` and `not fairly gradeable` rows are excluded from the average, so grading a dimension `F` when it should be `n/a (stage)` corrupts the verdict — apply the stage gate below before grading.

## Author Verdicts

Add one short author verdict after the technical verdict when the evidence is strong enough. Keep it concrete and proportional.

| Overall shape | Author verdict pattern |
|---|---|
| A range | Ronny, Diane, and Ya would trust this test: the decision is named, the comparison is valid, and the readout would survive a hostile audience. |
| B range | Ronny, Diane, and Ya would call this a solid experiment draft: the core comparison is trustworthy, but the remaining gaps still decide whether the readout can carry the decision. |
| C range | Ronny, Diane, and Ya would likely find this WIP: enough structure to discuss, not enough rigor to bet the strategy on yet. |
| D range | Ronny, Diane, and Ya would label this testing theater: the artifact has experiment vocabulary, but the randomization, power, or analysis mechanism is doing too little work. |
| F range | Ronny, Diane, and Ya could write a cautionary tale from this: the setup can produce a confident wrong answer and ship it as evidence. |

Vary the sentence to match the finding. Do not force the exact wording when it sounds cute or unfair.

## Stage Adjustment

Do not punish a hypothesis sketch for missing a full analysis plan. Do punish a readout for missing validity checks, uncertainty, or a decision recommendation.

Decide stage relevance explicitly before grading each dimension:

- Stage-irrelevant and unaddressed: `n/a (stage)`, excluded from the verdict average. A missing readout section in a pre-launch design is `n/a (stage)`, not `F`.
- Stage-irrelevant but addressed anyway — a section, or an explicit deferral ("stopping rules to be finalized before launch, owner named"): grade what is written. A credible deferral with a revisit trigger is a good decision, not a gap.
- Stage-relevant: grade normally; here absence or silence is exactly the failure the `F` anchor describes.

Minimum acceptable by stage:

| Stage | Minimum useful evidence |
|---|---|
| Idea/hypothesis | Decision to inform, treatment sketch, control candidate, plausible primary metric, worst-case mistake, feasibility read, and a reason this needs a test over a cheaper alternative |
| Test design | Hypothesis, arms defined, unit, primary + guardrail metrics, power/MDE/duration, analysis plan, risks |
| Launch-ready | Instrumentation validated, assignment tested, SRM check planned, ramp plan, stop/kill criteria, owner |
| In-flight | Health checks running (SRM, guardrails), no unplanned result-driven stops, mid-test changes logged, peeking policy honored |
| Readout | Validity checks passed and reported, pre-registered analysis followed (deviations disclosed), CIs, segment discipline, decision recommendation |
| Post-decision | Decision executed and monitored, learning captured where the team can find it, follow-up hypotheses recorded |

## Grade Interpretation

- F means the reviewer cannot rely on the test to inform the decision.
- D means the team knows the word but not the mechanism.
- C means the section can start a review but cannot yet carry the decision alone.
- B means the section can support a decision with caveats.
- A means the section can survive a skeptical stakeholder and a surprising result.

When a dimension grades `F` or `D` and the test stage depends on it, make it a finding. When a dimension grades `C`, consider whether the missing evidence would change the decision. When a dimension grades `A`, consider praising the specific mechanism.
