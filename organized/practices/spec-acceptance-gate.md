# Practice: The Working Wireframe Spec-Acceptance Gate

> Companion to *Principles for AI-Augmented Software Delivery*. Implements §1b
> (the working wireframe) and connects to §3 (the verification bottleneck).
> This is a **practice**: swappable, iterate freely. The principles it serves are
> the durable part.

**Status:** Draft v0.1
**Last updated:** 2026-06-30

---

## What this gate is

The point where an executable prototype stops being *a thing someone built* and
becomes *an accepted specification that the builder + verifier will rebuild to
production fidelity*. It is a category transition with a short ceremony attached.

**The one rule:** passing the gate means the working wireframe is accepted **as
direction**. It is never, by passing, approved for deployment. Production is
always rebuilt from the accepted spec. There is no path that promotes a prototype
to production while skipping the rebuild.

**Why the gate earns its cost:** it does two jobs at once.

1. It transfers intent without translation loss (the receiver is in the room and
   the spec is executable).
2. It produces the **acceptance criteria** that the verifier will check the
   production build against later. The output of this gate is the input to the
   §3 review. Get this gate right and the expensive human review at PR time
   becomes "does the build meet the contract we already agreed to," not
   open-ended code reading.

---

## Entry criteria (when a wireframe is ready for the gate)

A working wireframe is ready when:

- It **runs** and the intended behavior can be interacted with end to end for the
  core path(s). Executability is the whole point; a static mock is not a working
  wireframe.
- It is scoped to a **coherent unit** (a feature or capability), not a sprawling
  everything-app.
- The author can state, in a sentence, the problem it solves and for whom.

Not required, and explicitly fine to be absent: real auth, scale, persistence
guarantees, error handling beyond what shows intent, observability, compliance.
Their absence is **expected** and is not a deficiency (see "What it must not
contain").

---

## Required contents: the spec package

The working wireframe is accompanied by a short package. Keep it lightweight; the
running prototype carries most of the load. The package exists to make intent and
boundaries explicit where a running artifact alone is ambiguous.

1. **Demonstrated behavior.** The runnable prototype itself: the happy path(s)
   and the important variations. This is what makes it a spec and not a document.
2. **Intent narrative.** What problem this solves, who for, and *why this shape*.
   The prototype shows *what*; the narrative carries the *why* the prototype
   can't encode. Builders need the why to make good production tradeoffs.
3. **Decided vs. undecided list.** THE most important item. For the specifics the
   prototype commits to, mark each as either:
   - **Decided (preserve):** a deliberate intent decision the builder must keep.
   - **Undecided / incidental (rebuild freely):** an accident of prototyping
     (a hardcoded value, whatever library the tool reached for, a placeholder
     layout) that the builder should treat as noise and redo correctly.
   This is what stops incidental prototype choices from silently becoming
   requirements. An executable spec is higher fidelity *and* noisier than prose;
   this list separates signal from noise.
4. **Data / contract shape.** The key entities, the states, what goes in and out.
   Even where the prototype fakes the backend, express the intended shape of the
   real thing.
5. **Boundaries / non-goals.** Explicit "this does NOT need to do X." Prevents
   scope creep in the build.
6. **Acceptance criteria (seed).** The observable behaviors that, if true in
   production, mean the build satisfied the intent. The prototype demonstrates
   these; naming them makes them testable. **These become the verifier's
   checklist at §3.**

---

## What it must NOT contain or claim

By design, a working wireframe punts production fidelity. The intent roles should
**not** spend effort on, and the gate should **not** judge:

- Security and auth internals (beyond demonstrating intended UX of them)
- Scale and performance
- Error handling beyond what is needed to show intent
- Real data integrity, persistence, migrations
- Observability, alerting
- Compliance posture

Over-building these is waste (they get rebuilt or thrown away) and worse, it
deepens the fidelity trap by making the prototype look production-ready. "It only
does the happy path" is the correct state, not a gap to close here.

---

## The review

**Keep it short and consultative, not a phase-gate.** A walkthrough, not a sign-off
committee. Risk-tier the depth (see "Keep it lightweight").

**Who is in the room:**

- The intent role(s): PO / PM / TPM who authored it.
- The architect: brings the integration constraints.
- A representative of the **builder + verifier** who will build it. Putting the
  receiver in the room is what kills translation loss. They leave able to build,
  not holding a document to decode later.

**What each evaluates:**

- **Intent roles:** does this capture what we want? Is the *why* sound?
- **Architect:** does it fit the system? What integration constraints apply? Is
  the implied data/contract shape coherent with the rest? What cross-cutting
  concerns must the build respect?
- **Builder + verifier rep:** is the intent legible enough to build from? What is
  still ambiguous? Can we name the acceptance criteria together right now?

**What the review does NOT evaluate:** the prototype's *code quality*. The
prototype code is disposable. Reviewing it is the fidelity trap running in the
opposite direction.

---

## Acceptance: what "accepted as spec" means

The gate is passed when these are recorded (version them like code):

- Intent is agreed and written down (the narrative).
- The **decided / undecided list** is finalized.
- The **acceptance criteria** are named and testable.
- The architect's **integration constraints** are attached.
- The prototype is **frozen and tagged** as the reference spec. Changes to intent
  after this mean a *new version through the gate*, not editing the prototype in
  place.
- A **production work item** is created that references the accepted spec.

Acceptance means approved **as direction**. It does not mean the prototype is
approved to deploy.

---

## The handoff to builder + verifier

The pair receives: the frozen prototype (executable reference), the intent
narrative, the decided/undecided list, the data/contract shape, the boundaries,
the acceptance criteria, and the integration constraints. They **rebuild to
production fidelity** (cheap, per principles §5; the prototype itself may be
discarded).

The closure: the verifier later checks the production build against the **same
acceptance criteria** set here. The gate output is the verification input. The
two gates (this one and the §3 PR review) are two ends of one verification spine.

---

## Anti-trap mechanisms (procedural friction)

The pull to ship a thing that already works is enormous. Make it structurally
hard, not just culturally discouraged:

- Prototypes live in a clearly separate, **non-deployable** space (sandbox or
  separate repo) with no promotion path into a deploy pipeline.
- They are **visibly labeled** as specs/prototypes, never products.
- The pipeline **structurally requires a rebuild**; there is no "promote
  prototype" button.
- The accepted spec is **immutable once frozen**; intent changes go through a new
  gate version.
- State it up front, culturally: **the prototype is throwaway by design**, so no
  one is attached to shipping it.

---

## Keep it lightweight (or it becomes the new SAFe)

This gate must not recreate waterfall. Guard it:

- **Risk-tier the ceremony.** A tiny change is a ten-minute walkthrough. A new
  capability gets the full package. Match depth to risk, the same way §3 tiers
  review.
- **Consultative, not approval-by-committee.** The goal is shared understanding
  and a clean handoff, not a stamp.
- **Fast.** If the gate becomes a queue, it is now the bottleneck, and you have
  reintroduced the exact ceremony tax the whole methodology rejects.
- **Receiver in the room.** Synchronous understanding beats asynchronous
  document-passing every time here.

---

## Failure modes to watch

- **Ship-the-prototype:** the trap itself. Contained by the anti-trap mechanisms.
- **Leak:** incidental prototype choices treated as requirements. Contained by the
  decided/undecided list.
- **Under-specify:** prototype accepted but intent unclear; builder reintroduces
  translation loss. Contained by the receiver being in the room and naming
  acceptance criteria live.
- **Over-build:** intent roles gold-plate production concerns. Contained by the
  "what it must not contain" list and stating throwaway-by-design.
- **Gate-as-bureaucracy:** ceremony so heavy it becomes the bottleneck. Contained
  by risk-tiering and keeping it consultative and fast.

---

## Definition of done (gate-level)

The gate is done when the builder + verifier can walk away and **build to
production fidelity without coming back for clarification**, and when the verifier
has, in hand, the acceptance criteria they will check the build against. If either
is not true, the gate has not been passed.
