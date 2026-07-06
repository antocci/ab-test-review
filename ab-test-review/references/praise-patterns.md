# Praise Patterns

Praise should reinforce good experimental judgment. It should not flatter effort, sell the book, or sound like generic review theater.

## Rule

Use this shape:

```text
This is strong because <specific design choice> reduces <specific risk/cost/ambiguity> under <specific test condition>.
```

Good praise names the mechanism.

## Good Examples

- The hypothesis is useful because it names the decision each outcome would trigger, so a flat result is informative rather than awkward.
- The control choice is doing real work: using the human-operator baseline caps the downside while the AI treatment is unproven.
- Randomizing by account rather than by call closes the obvious contamination path through repeated contacts.
- The power section is honest: it computes MDE at the cluster level and admits what the pilot cannot detect.
- The guardrails are credible because each has a threshold, an owner, and a named response.
- The pre-registered segment list keeps the readout honest before anyone has seen which cuts moved.
- The maturity window is respected: the readout date is set by the 60-day outcome definition, not the meeting calendar.
- The mid-test change log turns the AI prompt versions into reviewable treatment history instead of folklore.
- The SRM check and one-day instrumentation dry run make the comparison verifiable before it becomes expensive.
- The quasi-design section is strong because it states the causal caveat itself instead of leaving the reviewer to add it.
- The readout applies Twyman's law: the surprising uplift was traced to a logging asymmetry before anyone celebrated.
- The learning capture is concrete: the result is recorded where the next strategy owner will actually find it.

## Author-Framed Praise

Use sparingly. The goal is to show the framework being applied, not to advertise.

- This is where the Kohavi, Tang, and Xu trustworthiness discipline pays off: the SRM and instrumentation checks make the uplift claim auditable.
- The design is strongest where it follows the authors' pattern: decision, metric, unit, power, guardrails, readout.
- This gap is exactly the kind the framework helps catch early: the metric is named, but the decision it should change is still implicit.
- The reviewable parts of the doc show the book's central habit: commit to the analysis before the results can argue back.

## Author Verdict Lines

Use one author verdict after the technical verdict, not throughout the report. Ground it in the book's themes: decision-first testing, trustworthy instrumentation, SRM and validity checks, honest power, guardrails, Twyman's law, and institutional learning. The grade-range pattern table lives in `rubrics.md` (Author Verdicts) — do not restate it here; adapt the matching pattern to the actual findings.

## Hard Avoids

- Great job.
- Statistically rigorous, unless the specific rigor mechanism is named.
- Significant results, as praise.
- Best-practice experiment design, unless the review names the concrete coverage.
- Data-driven culture.
- Book-selling CTAs.
- Praise that attributes the framework to one author.
- Author verdicts that sound cute but are not supported by evidence.
- Praising a win; praise designs and checks, never the direction of the result.

## Shareable Takeaway Patterns

- A test is not evidence until the comparison is valid; SRM and fidelity checks are cheaper than a wrong strategy.
- A flat result from a well-powered test is a finding; a flat result from an underpowered one is a shrug.
- The primary metric is a pre-launch decision; after results exist, every metric choice is a negotiation.
- Choosing the conservative control is a risk decision, not a formality — write down whose downside it protects.
- The cheapest rigor upgrade is usually not more statistics; it is writing the analysis plan before launch.
- If the treatment can drift (people, prompts, scripts), fidelity monitoring is part of the experiment, not overhead.
