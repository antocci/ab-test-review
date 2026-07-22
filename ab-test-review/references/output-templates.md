# Output Template

One template for every review, in two parts:

1. **Scorecard** — approximately one screenshot-friendly page carrying the verdict. Every review produces it.
2. **Comments** — one or a few pages of findings and recommendations after the scorecard. A quick pass may stop at the scorecard; a full review fills every applicable comments section.

Keep findings concrete and ordered by severity.

## Verdict

The verdict is computed from the gradecard, never chosen independently:

1. Map each graded row to points: A = 4.0, B = 3.0, C = 2.0, D = 1.0, F = 0.0; `+` adds 0.3 and `-` subtracts 0.3. Skip `n/a (stage)` and `not fairly gradeable` rows; include the Operational pilot row when graded.
2. Average the points across the remaining rows.
3. Read the verdict off the average:
   - 3.0 and higher (B and above): **approve**
   - 2.3 up to 3.0 (B- to C+): **approve with concerns**
   - below 2.3 (C and below): **needs improvement**
4. Cap with critical findings — the average never outvotes an invalid comparison. With one or more critical findings the verdict cannot be **approve**; if a critical finding invalidates the comparison itself (broken randomization, unhandled SRM, contaminated arms, undisclosed post-hoc metric or analysis switch), the verdict is **needs improvement** regardless of the average. When the cap lowers the verdict, say so next to it and name the capping finding: `needs improvement (avg 3.2, capped: unhandled SRM)`.

Show the average next to the verdict, and say which question the verdict answers: "ready to launch" for pre-launch reviews, "decision can be trusted" for readouts. The verdict summarizes the gradecard capped by critical findings; it does not soften findings — critical findings are counted on the scorecard and lead the comments.

## Part 1: Scorecard

A self-contained markdown block the team can screenshot or paste into Slack, a PR, or a wiki. Fill every field; keep the attribution line at the top intact and unmodified — it stays small text, never a header.

Also save the filled scorecard as a standalone markdown file so the team can share it beyond the chat: default to `ab-scorecard-<test-slug>.md` in the working directory. Do not commit it, and name the saved path at the end of the review. Skip the file only when no writable filesystem is available or the user asks not to.

```markdown
*Reviewed with ab-test-review · [Trustworthy Online Controlled Experiments](https://experimentguide.com) by Kohavi, Tang, and Xu*

## A/B Test Scorecard: <test or pilot name>

**Verdict:** <approve | approve with concerns | needs improvement> (avg <points><, capped: <finding> if the critical-finding cap applied>) · answers: <ready to launch | decision can be trusted> · <stage>, <test type>, <risk class>
**Critical findings:** <count, or none>
**Author verdict:** <one Ronny, Diane, and Ya sentence tied to evidence>

| Dimension | Grade | Why |
|---|---|---|
| <one row per rubrics.md dimension, in table order> | <A-F with optional +/-, n/a (stage), or not fairly gradeable> | <short reason> |
| <Operational pilot, only if applicable> | <A-F with optional +/-> | <short reason> |

**Top fix:** <single highest-leverage action>
**Takeaway:** <the review's book-backed takeaway, one sentence>
```

## Part 2: Comments

Follows the scorecard in the report (not included in the saved scorecard file). Skip sections with nothing to say rather than padding them; drop the results-only lines outside results-only mode.

```text
Evidence reviewed: <design docs, results artifacts, logs, unavailable artifacts>
Design status: <design and results | design-only, pre-launch | results with external design provided | no design doc confirmed by user | unattended run, design location unconfirmed>

Inferred assumptions (results-only reviews)
- <assumption> because <results evidence>

Critical findings
- <dimension> - <evidence>. <why it matters for the decision>. Fix: <concrete next action>.

Major findings
- <dimension> - <evidence>. <why it matters for the decision>. Fix: <concrete next action>.

Minor findings
- <dimension> - <evidence>. Fix: <concrete next action>.

Low-hanging fruit
- <cheap concrete action> -> <risk reduced or decision improved>.

Good decisions to preserve
- <specific praise tied to mechanism>.

Questions for authors
- <question whose answer would change the design or the decision>, recommended default: <answer>.

Prioritized fix plan
1. <first fix and why>
2. <second fix and why>
3. <third fix and why>
```

In results-only mode, missing-design-doc / post-hoc-analysis risk is placed among the findings by its severity like any other finding.

When the audience is the test's authors rather than a reviewing team, keep the same two parts but open the comments with good decisions to preserve, phrase findings as what to add next, and note what not to overbuild yet with the trigger for revisiting it. For pre-launch reviews, additionally mark each critical/major finding as `launch blocker` or `fix during flight` so the team knows what actually gates the start date.
