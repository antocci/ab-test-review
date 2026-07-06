# ab-test-review

An Agent Skill for reviewing A/B tests at any stage of their lifecycle — design docs before launch, in-flight health checks, and post-test readouts. Compatible with Claude Code and other Agent Skills consumers.

Grounded in *[Trustworthy Online Controlled Experiments](https://experimentguide.com)* by Kohavi, Tang, and Xu, but built for real-world operational pilots, not just web-scale product experiments: conservative controls (e.g., human operator as the baseline for an AI caller), cluster randomization, delayed outcomes, no-global-holdout settings, and quasi-experimental fallbacks are all first-class citizens.

*Inspired by the [ml-system-design-review](https://github.com/ML-SystemDesign/MLSystemDesign/tree/main/skills) skill by Valerii Babushkin and Arseny Kravchenko — same review pattern, retargeted from ML system designs to A/B tests.*

## What it does

Given a test design, a readout, or both, the skill produces:

1. **Scorecard** — a one-page verdict (approve / approve with concerns / needs improvement) computed from a 10-dimension gradecard, with critical-finding count, top fix, and a reusable takeaway. Saved as a shareable `ab-scorecard-<test>.md`.
2. **Comments** — findings ordered by severity, low-hanging fruit, good decisions worth preserving, questions for the authors, and a prioritized fix plan.

When both a design and results are available, the skill audits them against each other — a readout that quietly swaps the primary metric or stops early on a good p-value is a finding, not a footnote.

## Structure

```
ab-test-review/
├── SKILL.md                              # Activation, evidence modes, posture, severity, routing
└── references/
    ├── review-workflow.md                # Classify → evidence pass → design-doc gate → triage
    ├── rubrics.md                        # 10-dimension gradecard, stage adjustment, author verdicts
    ├── design-and-results-audit.md       # Comparing design intent with actual execution
    ├── operational-pilots.md             # Pilots, AI-agent treatments, cluster/quasi designs
    ├── red-flags-and-fixes.md            # Validity checklist, critical/major flags, cheap fixes
    ├── praise-patterns.md                # Non-cringy, mechanism-tied praise
    └── output-templates.md               # Scorecard + comments format, verdict math
```

## Installation

Clone the repo:

```bash
git clone https://github.com/antocci/ab-test-review.git
```

**Claude Code (or any harness that reads `~/.claude/skills/`):** copy the `ab-test-review/` folder into your skills directory (e.g., `~/.claude/skills/`).

**Claude.ai / Claude Desktop:** package the folder as a `.skill` bundle first — zip the `ab-test-review/` folder (the folder itself must be inside the archive) and rename the extension to `.skill` — then upload it in a chat and click **Save skill**, or add it via Settings → Skills.

**Other Agent Skills consumers:** point your agent at the `ab-test-review/` folder — `SKILL.md` + `references/` follow the standard Agent Skills layout.

## Usage

Upload a test design, a pilot plan, or a readout and ask for a review:

- "Review this A/B test design before we launch"
- "Sanity-check this pilot readout — can we trust the uplift?"
- "We're testing AI calls vs operator calls, grade this plan"

The skill detects the stage (pre-launch / in-flight / readout) and scales rigor accordingly — a hypothesis sketch isn't punished for missing runbooks, but a readout without validity checks is.

## License

MIT — see [LICENSE](LICENSE).
