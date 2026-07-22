# Verification Computations

When the artifacts contain checkable numbers, recompute instead of trusting. A claim contradicted by its own numbers is the strongest finding class a review can produce — it needs no appeal to authority and cannot be argued away. Run a scratch script (Python is fine) whenever the arithmetic is nontrivial; a finding built on a recomputation states the inputs, the method, and the result.

## Discipline

- Compute only from numbers actually present in the artifacts. Never invent an input; a missing input becomes a question for authors, not a guess.
- State assumptions next to each result: two-sided alpha 0.05, equal split, normal approximation, intent-to-treat — whatever the computation leaned on. Label approximations as approximations.
- Grade against the design's declared statistical framework. Fixed-horizon math applies to fixed-horizon plans; if the platform declares sequential or always-valid statistics, in-flight looks are legal there — do not flag them from a fixed-horizon lens.
- Rounding disagreements are not findings. A recomputation matters when it changes the decision, the severity, or the honesty of a claim.
- A recomputation that confirms the claim is worth one line of credit in the evidence, not a section.

## Core Checks

Run whichever of these the available numbers permit:

- **SRM (sample ratio mismatch).** Chi-square goodness-of-fit of observed arm counts against the designed split. `scipy.stats.chisquare([n_a, n_b], f_exp=[N*r, N*(1-r)])`. p < 0.001 is an unhandled SRM if the readout proceeded anyway — critical per SKILL.md. Between 0.001 and 0.01, ask what investigation happened.
- **Power and MDE.** From baseline rate, per-arm N, and alpha, recompute the detectable effect: MDE ≈ (z_α/2 + z_β) · sqrt(2·p·(1−p)/n) for proportions, at the unit the design randomizes. Compare with the claimed power or MDE. An underpowered test presented as proof of "no effect" is critical; power math done at the wrong unit is major.
- **CI and p-value consistency.** From the point estimate, N, and baseline, recompute the standard error and check the reported interval and p-value against each other and against the estimate. A CI excluding zero alongside p > 0.05 (or the reverse) means at least one of them is wrong.
- **Cluster design effect.** For clustered delivery, effective N = N / (1 + (m−1)·ICC) where m is average cluster size. If ICC is unreported, do not invent one — show the power surviving at labeled sensitivity values (e.g., ICC 0.01 and 0.05) and ask which the team believes.
- **Multiplicity expectation.** With k independent cuts at alpha, roughly k·α significant results are expected by chance. Twenty segments at 0.05 buy one free "win"; say so when a readout celebrates its one significant cut.
- **Maturity arithmetic.** Cohort entry dates plus the outcome window against the readout date: what share of units had immature outcomes at readout, and are they handled per the design (truncation, maturity-aligned cohorts) or silently included.
- **Reconciliation.** Totals and rates should reproduce each other across tables and slides: arm Ns consistent between the SRM table and the results table, rate × denominator ≈ reported count, segment rows summing to the topline population. Numbers that do not reconcile are a finding even when no single number is provably wrong.

## Reporting

Phrase the finding with its inputs, like other evidence references:

- `readout.pptx` slide 3 reports 50,412 vs 48,919 exposures at a designed 50/50 split — chi-square SRM p ≈ 2e-6; critical until the imbalance is explained.
- `design.md:22` claims 80% power at a 2pp MDE; from the stated 18% baseline and 4,100 per arm, the detectable effect at 80% power is ≈ 3.4pp — the readout's "no effect" conclusion is unsupported at the effect size the decision cares about.
- `results.xlsx` arm totals (61,240) do not reconcile with the exposure log summary in slide 2 (58,003); the 3,237-unit gap is unexplained and could hide an asymmetric filter.

Classify each confirmed contradiction per the Severity section in SKILL.md; a computation that merely narrows uncertainty goes to questions for authors with the recommended default.

## When Not To Compute

- Verification is spot-checking claims, not redoing the analysis. If the checks suggest the analysis itself is untrustworthy, recommend a reanalysis as a fix with an owner — do not build a parallel pipeline inside the review.
- No checkable numbers means skip silently. Do not pad the report with "could not verify" lines; the absence of numbers is itself a finding only where the number is load-bearing (a readout with no arm counts anywhere cannot support an SRM claim, and says so once).
