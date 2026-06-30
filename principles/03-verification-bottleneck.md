# §3. The Verification Bottleneck (the live problem)

**Status:** Draft v0.1
**Canonical ID:** §3 (stable; numbers are never reused or reordered)

**Principle.** Generation is cheap, so work now piles at the first place a human
is structurally required: **review**. Treat verification as a *pipeline with
layers*, where the human PR review is the last and thinnest layer, not the only
one. Push verification left, into generation, so the PR becomes attestation
rather than the place all the verification work actually happens.

Constraint to respect: compliance (e.g. SOC2) makes some quantity of human
review **legally irreducible**. The goal is not to remove humans. It is to make
the irreducible human judgment as small, fast, and high-leverage as possible.

Levers, roughly in order of impact:

1. **Shrink the diff.** Review cost is superlinear in diff size. Small,
   single-purpose changes are a *generation* discipline, so constrain the
   agents. Likely the biggest unlock, at near-zero cost.
2. **Change what the human reviews.** Ship self-describing PRs: what changed and
   why, the spec it satisfies, the test evidence, an explicit risk surface
   ("look hardest here"). Reviewer reviews a narrative with the diff as backup.
3. **Aim human attention with an AI pre-pass.** AI review doesn't replace the
   human; it triages the diff and points the scarce, compliance-required
   attention at the 10% that needs judgment.
4. **Split correctness from judgment.** Tests and gates answer "is it correct."
   Humans answer the irreducible part: intent, security judgment, architectural
   fit, and the attestation itself. The reviewer's job shifts from "hunt for
   defects" to "confirm this matches intent and is safe to own."
5. **Tier review by risk.** Heavyweight multi-reviewer for sensitive scope;
   lighter for low-risk change. (Confirm contours with the SOC2 owner; auditors
   tend to favor deliberate risk-tiering.)

Implemented by `practices/pr-review-gate.md`, which consumes the acceptance
criteria produced at the spec-acceptance gate (§1b). The two gates are two ends
of one verification spine.

> **Open question to resolve:** exactly which review tiers our SOC2 controls
> permit, and how to encode "risk surface" so tiering is auditable.
