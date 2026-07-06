# Design And Results Audit

The skill reviews the design artifact and the results artifacts together. Either one can hide problems the other exposes.

## Finding Design Docs

Search likely locations and names:

- Experiment platform records, `README*`, `docs/**`, `experiments/**`, `tests/**`, `pilots/**`, `analysis/**`, `notebooks/**`, wiki exports.
- Files containing `design`, `experiment`, `pilot`, `ab`, `test plan`, `hypothesis`, `power`, `readout`, `results`, `uplift`, `postmortem`.
- Tickets, briefs, or decision memos when there is no dedicated experiments folder.

If no design doc is found and the user has not provided one, apply the Design Doc Gate in `review-workflow.md`: ask the user where it lives; unattended, proceed with the missing-design caveat at the top of the report. Do not assume absence.

## What To Inspect In Results Artifacts

Map the execution enough to compare it with the design:

- Assignment and exposure logs: who was randomized, when, into what, at what unit.
- Sample sizes per arm over time; entry/exit filters and exclusions.
- SRM and balance checks; A/A or pre-period evidence if any.
- Analysis code or notebook: test statistic, variance treatment, filters, joins, metric definitions.
- Dashboards and monitoring during the test; guardrail values over time.
- Mid-test change log: treatment edits, AI prompt/script versions, ramp changes, incidents.
- Readout deck or memo: which metrics are shown, which are omitted, how uncertainty is presented.
- Decision record: what was shipped, when, and what monitoring followed.

For operational pilots also inspect delivery evidence (call logs, letter send logs, agent transcripts), treatment fidelity (was the treatment actually delivered as designed), and capacity or queue constraints that could contaminate arms.

## Compare Design Claims With Results Evidence

Useful finding patterns:

- Design randomizes by customer; analysis is at call level with no cluster correction.
- Design names one primary metric; readout leads with a different metric that happened to move.
- Design commits to 6 weeks or N per arm; test stopped at week 2 on a good p-value.
- Design promises SRM checks; no evidence they were run, or they failed and were not addressed.
- Design excludes a segment; results include it (or silently drop another).
- Design says treatment is fixed; change log or transcripts show the AI script was rewritten mid-test.
- Design defines the control as the previous strategy; in practice control operators drifted toward the treatment behavior (contamination).
- Guardrail breached mid-test; no recorded response despite a documented threshold.
- Readout reports twenty segment cuts with the significant ones highlighted and no multiplicity handling.
- Results team applied a useful safeguard (capping, maturity window, exclusion rule) absent from the design, making the analysis hard to review or repeat.

## Results-Only Mode

Entered only after explicit user confirmation that no design doc exists — or, when running unattended with no user to ask, entered directly with the missing-design caveat at the top of the report.

Report structure changes:

- Add `Design status: no design doc confirmed by user` (or `unattended run, design location unconfirmed`).
- Add `Inferred assumptions` with each assumption labeled.
- Add a severity-labeled `post-hoc analysis risk` finding: without a pre-registered plan, the reviewer cannot distinguish planned analysis from result-driven choices; grade the uncertainty rather than assuming bad faith.
- Grade from results evidence, but mark dimensions that cannot be fairly graded without a design artifact (typically hypothesis framing, power, and analysis pre-registration).

Do not penalize a scrappy first pilot for missing a polished doc. Do penalize a decision-carrying test when the hypothesis, metric, and stopping rule exist only in memory.

## Evidence References

When possible, cite files, slides, cells, and lines. If the relevant artifact is external or unavailable, state that explicitly and grade the uncertainty rather than inventing evidence.

Good evidence phrasing:

- `design.md:31` commits to recovery rate at 60 days as primary, but `readout.pptx` slide 4 leads with 14-day contact rate.
- `analysis.ipynb` cell 12 computes a t-test on call-level rows while `design.md:18` randomizes by account — no cluster correction found.
- No design doc was provided; user confirmed none exists, so the results-only audit assumes the notebook's filters define the intended population.
