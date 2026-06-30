# Practice: The Pull-Request Review Gate (Change Acceptance)

> Companion to *Principles for AI-Augmented Software Delivery*. Implements §3 (the
> verification bottleneck) and closes the verification spine opened by the
> spec-acceptance gate (`practices/spec-acceptance-gate.md`). This is a
> **practice**: swappable, iterate freely.

**Status:** Draft v0.1
**Last updated:** 2026-06-30

---

## What this gate is

The point where a human takes ownership of a change and **attests it is safe to
merge**, checked against a contract that was agreed before any code existed (the
acceptance criteria from the spec-acceptance gate).

**The one rule:** the human review is the *last and thinnest* layer of
verification, not the first. By the time a human looks, correctness should already
be established by automated layers. The human confirms judgment and provides the
irreducible attestation. If a human is the first thing to catch a class of defect
that automation could have caught, the pipeline is misbuilt and the bottleneck is
self-inflicted.

**Why the gate earns its cost:**

- Compliance (e.g. SOC2) makes some quantity of human attestation legally
  irreducible. This gate is where that attestation happens, deliberately and
  auditably.
- It closes the verification spine. The acceptance criteria defined at the
  spec-acceptance gate are the checklist confirmed here. Review becomes "does the
  build meet the contract we already agreed to," not open-ended code reading.

---

## The verification pipeline (what happens before the human)

Verification is layers, each catching everything it can so the next layer sees
only what genuinely needs it. Human review is layer 4.

1. **Generation-time (in the pair).** The builder + verifier already verified as
   they built: tests written, run locally, agent output reviewed in-pair. This is
   "push left" in action.
2. **Automated gates (CI).** Tests (including tests derived from the acceptance
   criteria), type checks, lint, static analysis, dependency and secret scanning,
   policy-as-code. **Correctness and mechanical safety live here.** Must be green
   to proceed.
3. **AI pre-review pass.** Summarizes the diff, maps it against the acceptance
   criteria, flags the risk surface, surfaces anything suspicious. It **aims** the
   human; it does not replace the attestation.
4. **Human review.** The irreducible layer. Confirms intent and judgment, attests
   ownership. Covered below.

The governing rule: **each layer owns what it is best at.** Humans should never
spend attention on what layers 1 to 3 already guarantee.

---

## Entry criteria (when a PR is ready for a human)

A PR is ready for human review when:

- All **automated gates are green** (correctness and mechanical safety
  established).
- The **AI pre-pass has run** and produced its summary and risk flags.
- The **PR package is complete** (see below).
- The diff is **small and single-purpose**. Oversized PRs are bounced, not
  reviewed; review cost is superlinear in diff size and large diffs produce
  rubber-stamping. Enforce a size ceiling as a generation discipline.
- It **references the accepted spec** and the acceptance criteria it satisfies.

If these are not met, bounce it. A half-ready PR consuming human attention is the
bottleneck forming.

---

## Required contents: the PR package (self-describing PR)

The diff alone forces the reviewer to reverse-engineer intent. The package makes
the change legible so the human reviews a narrative with the diff as backup. The
builder authors it; the agent can draft it.

1. **Spec link.** The accepted spec and acceptance criteria this satisfies (the
   contract).
2. **What changed and why.** A short narrative of the change and its intent.
3. **Acceptance-criteria checklist.** Each criterion mapped to the test or
   evidence proving it is met. This is the spine closure made concrete.
4. **Test evidence.** What tests were added or changed, what they cover, results.
5. **Risk surface.** Explicit "look hardest here": the parts touching security,
   auth, data, money, privacy, or cross-cutting concerns. Builder-declared and
   AI-flagged.
6. **Out of scope / known limitations.** What this deliberately does not do (ties
   to the spec's non-goals).
7. **AI pre-pass summary**, attached.

---

## What the human reviewer does

The job is **confirm judgment and attest**, not hunt for defects. Concretely:

- **Confirm intent.** Does the change satisfy the acceptance criteria? Review
  against the contract, not by cold-reading the code.
- **Exercise irreducible judgment** on what only a human should own: security
  implications, architectural fit and coherence (the integration constraint),
  privacy and compliance, whether this is the right abstraction, and the
  maintainability of the surface a human will own.
- **Scrutinize the flagged risk surface hardest.** Skim the mechanical and
  boilerplate; spend attention where judgment is actually required.
- **Attest.** "I have put eyes on this, I understand it, I take ownership, it is
  safe to merge." That attestation is the compliance control.

---

## What the human reviewer does NOT do

- Re-derive correctness the tests already prove.
- Re-run checks the automated gates own.
- Nitpick style the linter owns.
- Review disposable prototype code.

If a human is doing any of these, the fix is the **pipeline**, not the reviewer.
Every minute spent here is bottleneck you built yourself.

---

## Risk tiering (match review weight to blast radius)

Not every change needs the same depth. Tier by what the change *touches*,
classified automatically where possible (paths, labels, the AI pre-pass) and
recorded on the PR so tiering is **auditable**.

- **Tier 0 (trivial):** docs, comments, config behind flags, low-risk internal.
  Lightest path; single reviewer or, where compliance allows, automated merge with
  an async glance.
- **Tier 1 (standard):** typical feature work, no sensitive scope. Standard
  package, the human review above, reviewer count per policy.
- **Tier 2 (sensitive):** touches auth, payments, PII, security boundaries, data
  migrations, public APIs, or infrastructure. Full package, required multiple
  reviewers including a domain owner, deeper scrutiny, architect sign-off where the
  change affects system coherence.

Record on every PR: the assigned tier, the reason, and who attested. Auditors
favor deliberate, recorded risk-tiering.

> **Open question to resolve with the SOC2 owner:** the exact mapping of tier to
> required number of human attestations, and which tiers (if any) permit automated
> merge. Confirm before relying on Tier 0 automation.

---

## Compliance and attestation

- The **irreducible human attestation is the control.** Automation augments it; it
  does not replace it.
- Record, per PR: reviewers, that human eyes were on it, the tier and its
  rationale, the acceptance criteria confirmed, and the approval.
- Honor the **multi-reviewer requirement** per tier.

The aim throughout is to make the irreducible human judgment as small, fast, and
high-leverage as possible, never to remove it.

---

## Anti-bottleneck mechanisms (keep it flowing)

Review is the constraint this whole methodology is built around. Protect flow:

- **Shrink diffs** (the single biggest lever). Enforce a size ceiling; bounce
  oversized PRs.
- **WIP limits on the review queue.** Review is first-class work, not an
  interrupt-driven afterthought.
- **Fast turnaround / a review SLA.** Stale PRs are waste and grow merge conflicts.
- **Rotate and load-balance reviewers** so review does not pile on a few seniors.
- **Maximize the AI pre-pass triage** so human time is spent only on judgment.
- **Measure** review throughput and lead time to a verified change (principles §6).

If the review queue becomes a bottleneck, you have reintroduced the exact problem
this practice exists to relieve.

---

## Failure modes to watch

- **Human doing automation's job:** re-checking correctness. Self-inflicted
  bottleneck; fix the pipeline.
- **Rubber-stamping:** diff too large or package missing, reviewer overwhelmed,
  approves without understanding. Shrink diffs, enforce the package.
- **Attestation theater:** approval without real judgment, hollowing the control.
  The package and risk-surface focus are the countermeasures.
- **Over-trusting the AI pre-pass:** the reviewer defers to it and stops thinking.
  This is the agent-anchoring risk (principles §2b) reappearing at review. The AI
  aims; the human decides, against the criteria.
- **Tier mis-classification:** inflation or deflation of risk. Auto-classify and
  audit.
- **Review queue as bottleneck:** WIP limits, SLAs, diff ceilings.

---

## Definition of done (gate-level)

A PR is mergeable when:

- Automated gates are green.
- The AI pre-pass is clear, or its flags are resolved.
- Every acceptance criterion is mapped to evidence and confirmed.
- The required human attestation(s) for its tier are recorded, with tier and
  rationale.
- The reviewer understands the change and takes ownership of it.

If any of these is missing, it is not done.