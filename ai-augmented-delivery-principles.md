# Principles for AI-Augmented Software Delivery

> A living document. We version this like code. Practices are swappable;
> principles change slowly and only with good reason. When a practice and a
> principle conflict, the principle wins or the principle is wrong. Decide
> which, explicitly.

**Status:** Draft v0.1
**Last updated:** 2026-06-30
**How to use this:** Treat every principle as a hypothesis we are testing in
production. Each should eventually carry the practice that implements it and the
metric that tells us it's working.

---

## 0. The Reframe (why this document exists)

For decades, **writing code was the bottleneck**, and almost every practice we
inherited (specialized SDLC roles, story-point estimation, sprint time-boxing,
heavyweight coordination frameworks) is machinery built to manage the scarcity
and cost of producing code.

Agents collapse the cost of generation toward zero. So the constraint **moves**.
It moves to:

- **Specification.** Knowing precisely what to build.
- **Verification.** Trusting that what got built is correct and safe to own.
- **Integration.** Keeping many fast, locally-correct changes globally coherent.

Every principle below is downstream of this single shift. When in doubt, ask:
*does this practice relieve the new constraint, or is it machinery for the old one?*

---

## 1. Roles

**Principle.** Roles organize around the three new constraints (specification,
verification, integration), not around layers of the stack. Titles that
described *which part of the code you wrote* (frontend, backend) collapse,
because generation got cheap. Roles that *reduce ambiguity, establish trust, or
hold the whole system coherent* gain leverage, because those are the new
constraints. Read every role below as "which constraint do you sit on."

### 1a. Builder + Verifier (the production unit)

**Principle.** The fragmented SDLC roles (frontend, backend, SRE, devops, QA, and
so on) collapse into a unified **builder** who works across the lifecycle. But
building and verifying are distinct postures, and the pairing of
**builder + verifier** is the core unit of trusted delivery.

- Generation no longer needs to be parceled out by specialty, so the generalist
  builder is now viable and preferred.
- **Keep a depth anchor.** Every builder should have at least one domain where
  their judgment is genuinely better than the agent's. That depth is what
  calibrates their skepticism everywhere else. Guard against builders who are a
  mile wide and an inch deep, with the agent papering over gaps they can't
  evaluate.
- **Watch for new specializations** that are not "generalist builder." These are
  the new high-leverage roles because they relieve the new constraint for
  everyone:
  - Owner of the internal **agent harness / context platform**.
  - Owner of **verification infrastructure** (evals, test generation,
    regression gates, review tooling).

### 1b. The intent roles: PO / PM / TPM

**Principle.** Product Owner, PM, and TPM now sit directly on the
**specification** constraint, which is a primary one. Their generative tools
(wireframes, working prototypes, modeled requirements) let them produce
*executable specifications*. This is a real increase in their leverage: a running
prototype removes intent ambiguity that prose requirements never could, and it
kills the translation loss that used to occur at the handoff to engineering.

**Principle (the fidelity trap).** The new failure mode this introduces is that a
prototype now *runs*, which removes the signal that used to tell everyone it
wasn't done. There are two orthogonal axes of fidelity:

- **Intent fidelity.** Does this capture what we want built? Prototypes are now
  superb at this.
- **Production fidelity.** Is it safe to own and operate at scale (security,
  error handling, edge cases, observability, data integrity, maintainability,
  compliance)? Prototypes are near zero at this.

Functional behavior makes these axes *look* correlated when they are orthogonal.
A running happy path looks complete. The trap is the category error: mistaking a
high-intent-fidelity artifact for a high-production-fidelity one, and shipping
technical debt as if it were product.

**Principle (the working wireframe).** Name the artifact. What the intent roles
produce is a **working wireframe**: an executable specification whose job is to
give the builder + verifier unambiguous direction. It is the highest-fidelity
spec format we have ever had and the clearest instance of §5's durable spec. File
it under *spec*, not under *code*.

- **Definition of done** for a working wireframe: stakeholders agree it captures
  intent. NOT "it runs."
- **Explicit non-goal:** it is never a production candidate. The builder +
  verifier rebuild it to production fidelity (cheap, per §5; the prototype itself
  may be discarded, and that is fine).
- **Required gate:** a named acceptance step where the prototype is accepted *as
  a spec*, after which production is built from it. Make "rebuild from the spec"
  cheap (agents make it so) and make "ship the prototype" procedurally hard. The
  pull to ship a thing that already works is enormous and is the central
  discipline problem of this model.

### 1c. The architect (expanded scope)

**Principle.** **Integration** (global coherence across many fast,
locally-correct changes) is now a primary constraint, and it is the architect's
native domain. So the architect's role expands rather than shrinks.

What changed:

- **Old constraint: throughput.** The architect could only advise and review;
  their leverage was capped by what they could communicate and personally touch.
- **Now their intent is executable and propagable.** Architectural intent is
  encoded into scaffolds, interfaces, reference implementations, agent context,
  and policy guardrails, then enforced by automation across a huge surface.
  Leverage scales with the system, not with the architect's hours.

Because the architect is the one role that must hold the whole picture, and
because they now have the same generative tools as the intent roles, the boundary
between architect and TPM/PM blurs. An architect who can prototype is doing
product framing and system design in one motion, and can act as the TPM/PM, or
more.

**Guard the concentration risk.** This convergence raises bus-factor and can pull
the architect into product detail at the expense of the integration view. Be
deliberate about which hat is on and when. The architect's irreducible job is
coherence of the whole; product framing is an expansion of scope, not a
replacement of it.

### 1d. How the roles interact

**Principle.** Shift from sequential handoff (requirements, then design, then
build, with translation loss at every boundary) to concurrent co-production.

- Intent roles + architect **co-produce the working wireframe**: the executable
  spec plus the integration constraints it must live within.
- Builder + verifier **consume it and rebuild to production fidelity**.
- The architect **spans both halves**: sets integration constraints upstream,
  ensures coherence downstream. They are the connective tissue, which is exactly
  why their scope grew into product territory.

The old translation loss between "what we wanted" and "what got built" was a top
source of waste; the working wireframe largely kills it. The new risk it
introduces is the fidelity trap above, which the spec-acceptance gate exists to
contain.

---

## 2. Pairing: Builder + Verifier at the Terminal

**Principle.** Our evolution of XP pair programming is two humans, typically
senior + junior, driving an agent together. The agent is the thing being driven;
both humans stay in the loop. Learning flows in both directions.

What makes this configuration powerful:

- **Both humans move into a navigator posture.** The division is no longer "who
  types" but "who steers the agent" vs. "who evaluates output and plans the next
  move." The junior reasons at the senior's altitude the whole time, never
  relegated to watching someone type.
- **It flattens hierarchy usefully.** Context-building, decomposition, and
  parallel-agent management are new for everyone, so teaching is genuinely
  bidirectional. The junior may surface techniques the senior hasn't tried. This
  keeps the senior engaged rather than babysitting.
- **It is the ideal vehicle for transmitting calibrated skepticism**, the
  hardest senior skill to teach and the most valuable in an agentic world. The
  agent's output is the explicit shared object on the screen, so the senior can
  narrate judgment against it in real time ("looks right, but it'll break on
  empty input"; "confidently doing X, but that's the wrong abstraction, here's
  the tell"). Pairing makes otherwise-invisible judgment observable.

### 2a. STRONG PRINCIPLE: Protect the junior's time in the steering seat

The learning concentrates in the steering seat. The agent makes the senior so
fast that the pull toward "senior drives, junior watches" is *stronger* than it
ever was in classic pairing. Counteract it deliberately: build the handoff into
the ritual (ping-pong style), swap who holds the prompt on a cadence, regardless
of whose turn is "faster." Seat time is the thing we are actually allocating.

### 2b. STRONG PRINCIPLE: Don't let the agent anchor the pair

The agent is a confident, articulate third voice; classic pairing never had a
persuasive third party. The risk is both humans slide into reviewing the agent's
framing instead of forming their own. Discipline: before reading the agent's
output, each person states their own quick hypothesis about what good output
should look like. Then you review against your own model, not the agent's.

### 2c. Parallel-agent orchestration is its own literacy

Managing three or four agents at once has no classic analog. It's closer to
air-traffic control than to writing code, and it's the highest-leverage thing to
pair on precisely because it's so new and so cognitively distinct. Watching a
senior notice that agent #2 quietly went off the rails while attending to
agent #3, *and articulating how they noticed*, can't come from a doc.

**Literacies this practice exists to transmit:** context-building, decomposition,
parallel orchestration, output review / calibrated skepticism.

---

## 3. The Verification Bottleneck (the live problem)

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

> **Open question to resolve:** exactly which review tiers our SOC2 controls
> permit, and how to encode "risk surface" so tiering is auditable.

---

## 4. Process: Flow Over Ceremony

**Principle.** Optimize for flow against the *real* constraint, not for
predicting human output rates we no longer care about.

- **Condensed, measured Kanban with WIP limits** over time-boxed sprints.
  Flow-with-WIP-limits optimizes throughput against the actual constraint;
  time-boxing optimizes for predicting generation rates that are now cheap.
- **SAFe is waterfall with iterations.** It's elaborate coordination machinery
  optimized for a bottleneck that no longer exists. The ceremony tax defeats the
  point of agentic delivery. Reject heavyweight frameworks that manage the old
  constraint.
- **Velocity and story points measure the thing that got cheap.** Retire them.

---

## 5. Disposable Code, Durable Specs

**Principle.** If an implementation can be regenerated from a tight spec and a
strong test suite in an afternoon, then **the spec, the tests, and the
architectural constraints are the real assets**, and code is the cheap,
regenerable layer. Invest care accordingly. (Deeply continuous with TDD.)

---

## 6. Metrics That Match the New Constraint

Replace generation-era metrics (velocity, story points) with constraint-era ones:

- Lead time to a **verified** change
- Review / verification throughput
- Defect escape rate
- Rework rate
- Share of work that is spec-first vs. code-first

---

## 7. How We Evolve This Document

- **Principles-first, practices swappable.** Cargo-culting happens when people
  adopt the practice and lose the *why*. Keep the why attached.
- **Run changes as experiments, not rollouts.** One team, one change, a stated
  hypothesis, a few cycles, then inspect. This is the most XP-consistent way to
  invent an XP successor.
- **Constraints, not practices, drive the agenda.** Periodically re-run a
  Theory-of-Constraints pass: where does work pile up *now*? A practice earns
  its place only if it relieves the current constraint.

---

## Parking Lot / Open Threads

- Formalize the builder+verifier pairing practice into a named ritual: role
  definitions, swap protocol, the literacies list (see §2).
- ~~Define the auditable "risk surface" format for tiered review~~: addressed in
  `practices/pr-review-gate.md` (risk tiering, recorded tier + rationale per PR).
  Open sub-thread: confirm the tier-to-reviewer-count mapping with the SOC2 owner
  (see §3).
- Draft the agent harness / context platform ownership charter (see §1a).
- Baseline the §6 metrics on one team before changing anything else.
- ~~Define the **working wireframe spec-acceptance gate** concretely~~: drafted
  as a companion practice doc (`practices/spec-acceptance-gate.md`, v0.1). Open
  sub-thread: pilot it on one team and feed results back here (see §1b).
- Decide the **architect operating model**: when one person wears the
  architect/PM hats together vs. when to split them, and how to mitigate
  bus-factor (see §1c).
- Resolve whether the intent roles need a shared **prototyping standard** (tools,
  what to include, what to deliberately leave out) so working wireframes are
  legible to builders.