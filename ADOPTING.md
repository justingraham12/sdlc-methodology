# Adoption and Quick-Start Guide

> How to move to this methodology from the framework you are already running.
> Companion to the principles (`principles/`) and practices (`practices/`). Read
> the root `README.md` first for the reframe everything here rests on.

**Status:** Draft v0.1

## The one lens

Every process framework is machinery built to optimize *some* constraint. The
fastest way to understand how this methodology relates to the one you run today is
to ask two questions about your current framework:

1. **Which constraint was it built to optimize?**
2. **Does that constraint still bind once code generation is cheap?**

Most inherited frameworks were built when *writing code was the bottleneck*. When
generation collapses toward zero, the constraint moves to specification,
verification, and integration (see `README.md`). Practices that managed the old
bottleneck become ceremony tax; practices that happen to relieve the new
constraints carry over almost unchanged. This guide sorts your current practices
into those two buckets and gives you the first moves.

## Comparison at a glance

| Framework | Built to optimize | Does that constraint still bind? | Keep | Change |
|-----------|-------------------|----------------------------------|------|--------|
| **Waterfall** | Predictability when change is expensive; upfront correctness and traceability | Change is cheap now, so no. But its respect for *specification* is partly rehabilitated. | Spec rigor, traceability, architectural forethought | Frozen document-first specs become executable working wireframes; phase-gate handoffs become concurrent co-production plus two light gates |
| **Agile (Manifesto values)** | Responsiveness; feedback over planning; working software over documents | Yes. Fully aligned; we are an XP successor. | All four values | Update the *practices* under the values, and note "working" no longer means "production-ready" (the fidelity trap, §1a) |
| **Scrum (as commonly run)** | Predictable team cadence and protected focus when human throughput binds | The cadence optimizes a throughput that got cheap, so largely no. | The retro (inspect-and-adapt is our evolution engine), a single clear owner of intent, small increments | Time-boxed sprints become continuous flow with WIP limits (§4); story points and velocity become lead-time-to-verified (§6); the dev team becomes builder + verifier pairs (§1c) |
| **Kanban** | Smooth flow and throughput against a bottleneck | Yes. Closest ancestor to our process layer. | Flow, pull, WIP limits, your board, continuous delivery | Set WIP limits against the *verification* constraint, not generation; add the two gates as explicit policies (§3 practices) |
| **SAFe** | Cross-team alignment, portfolio governance, predictability at enterprise scale | The coordination *need* is real; the heavyweight cadence is not the right tool now. | The need for cross-team coherence, portfolio-level intent, compliance gates | PI-planning cadence becomes continuous flow plus architect-encoded integration constraints (§1b); layered ceremony becomes the two gates. Honest gap below. |
| **Ad hoc agentic ("vibe coding")** | Raw generation speed | Speed is real, but unmanaged it manufactures debt | The speed and willingness to let agents generate | Add the discipline you are missing: the fidelity trap is already biting you; install both gates and builder + verifier pairing |

> **DevOps / Continuous Delivery** is not a competing framework here; it is
> assumed. The PR-review gate (§3) presumes automated pipelines, tests, and
> trunk-based delivery. If you have strong CD already, you are ahead.

## Coming from Scrum

You are probably the most common starting point. Most of Scrum's *intent* survives;
its cadence machinery does not.

- **Carries over:** the retrospective is our inspect-and-adapt engine (§7 of the
  README); your Product Owner becomes the intent role (§1a), now producing working
  wireframes rather than written stories; small increments are still the rule.
- **Stop doing:** estimating in story points and tracking velocity. They measure
  the thing that got cheap. Stop time-boxing work into sprints as the primary
  rhythm.
- **First moves:** (1) stop pointing; start measuring lead time to a *verified*
  change. (2) Route your PO's mockups through a spec-acceptance gate so they become
  accepted specs, not shipped prototypes. (3) Keep the retro exactly as is.

## Coming from Kanban

You have the least to change; you are most of the way here.

- **Carries over:** flow, pull, WIP limits, your board, continuous delivery.
- **Change the target:** set your WIP limit against the *verification* constraint
  (usually the review queue), because that is where work now piles up, not
  generation.
- **First moves:** (1) instrument where work actually stalls; expect it to be
  review. (2) Add a spec-acceptance step as a column or policy before "in
  progress." (3) Cap review WIP and treat the PR-review queue as first-class work.

## Coming from SAFe

SAFe exists for real reasons: large organizations genuinely need cross-team
alignment, portfolio-level funding and governance, and predictability for
stakeholders who are not in the room. Do not throw those needs away; replace the
*mechanism*, not the goal.

- **Carries over:** the need for system coherence (now owned by the architect and
  encoded as integration constraints, §1b), portfolio-level intent, and
  compliance-aware gates (our PR-review gate is built for SOC2-style attestation).
- **Stop doing:** treating cadenced PI planning as the coordination mechanism, and
  paying the layered ceremony tax. Coherence comes from architect-owned,
  machine-enforced integration constraints, not from synchronized planning events.
- **First moves:** pick one train or team, suspend PI planning for a quarter,
  replace coordination-by-ceremony with architect-encoded constraints plus the two
  gates, and measure flow against the old baseline.
- **Honest gap:** this methodology does not yet have a fully worked answer for
  governing hundreds of teams and a portfolio at once. That is an open thread (see
  `OPEN-THREADS.md`). If you operate at that scale, pilot on one slice and keep
  your portfolio governance until we have a tested replacement.

## Coming from Waterfall

You are a surprising partial ally: this methodology *also* prizes specification.

- **Carries over:** rigor about specs and traceability, and upfront architectural
  thinking.
- **Change:** the frozen, document-first, single-pass spec becomes the executable,
  iterative working wireframe (§1a); phase-gate sign-offs become concurrent
  co-production plus two lightweight gates; no-feedback sequencing becomes the loop
  (§1d).
- **First moves:** (1) convert one requirements document into a working wireframe.
  (2) Replace its phase sign-off with the spec-acceptance gate. (3) Let the builder
  + verifier rebuild from it rather than implementing the document directly.

## Coming from ad hoc agentic work ("vibe coding")

You adopted agents but no process, and the fidelity trap is almost certainly
already costing you: prototypes that run are shipping as product and accruing debt.

- **Carries over:** the speed, and the instinct to let agents generate.
- **Add the missing discipline:** name working wireframes as specs, not product
  (§1a); install the PR-review gate's automated layers so correctness is
  established before a human looks (§3); pair builder + verifier so juniors plus
  agents are not shipping plausible-but-wrong code (§2).
- **First moves:** (1) draw the line between "working wireframe" and "production."
  (2) Turn on the automated verification layers. (3) Start one builder + verifier
  pair.

## The universal quick start (first three experiments)

Regardless of where you are coming from, adopt by experiment, not by rollout. One
team, one change, a stated hypothesis, a few cycles, then inspect (README, "How we
evolve this methodology").

1. **Instrument the constraint.** Measure lead time to a verified change and find
   where work piles up. This is your baseline and it tells you which gate you need
   first.
2. **Install one gate where you are weakest.** Fuzzy specs and rework point to the
   spec-acceptance gate. A review pile-up points to the PR-review gate. Do not
   install both at once.
3. **Pilot builder + verifier pairing on one team.** It is the mechanism that
   trains people into the whole model.

## Common adoption mistakes

- **Cargo-culting the practices without the why.** Keep the principle attached to
  every practice, or it rots.
- **Big-bang rollout.** This is a set of experiments, not a migration project.
- **Shipping working wireframes.** The fidelity trap. Wire in the spec-acceptance
  gate before you let intent roles prototype freely.
- **Setting WIP limits against generation instead of verification.** You will
  optimize the wrong queue.
- **Removing human review entirely.** Compliance and judgment both still require
  it; the goal is to make it small and fast, not to delete it.

## What stays the same

This is an evolution, not a repudiation. Carried forward from what you already do:
XP roots and pairing, inspect-and-adapt, small batches, continuous integration and
delivery, and close collaboration with whoever owns the intent. If your current
framework already does these well, you are adopting less than you think.
