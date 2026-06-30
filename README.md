# SDLC Methodology: AI-Augmented Software Delivery

A living, version-controlled methodology for building and delivering software in a
world where code generation is cheap and the binding constraints have moved to
**specification, verification, and integration**.

## The reframe

For decades, writing code was the bottleneck, and most inherited practice
(specialized roles, story points, sprint time-boxing, heavyweight frameworks) is
machinery for managing the cost of producing code. Agents collapse that cost
toward zero, so the constraint moves to three places:

- **Specification:** knowing precisely what to build.
- **Verification:** trusting that what got built is correct and safe to own.
- **Integration:** keeping many fast, locally-correct changes globally coherent.

Every document here is downstream of that single shift.

## How this repo is organized

- **Principles** are the durable *why*. They change slowly and only with good
  reason.
- **Practices** are the swappable *how*. They implement principles and are
  expected to be iterated, replaced, or retired as we learn.

When a practice and a principle conflict, either the principle wins or the
principle is wrong. Decide which, explicitly.

## Contents

- [`ai-augmented-delivery-principles.md`](ai-augmented-delivery-principles.md):
  the core principles (the spine). Covers roles (builder + verifier, the intent
  roles, the architect), pairing, the verification bottleneck, flow over
  ceremony, durable specs, and metrics.
- [`practices/spec-acceptance-gate.md`](practices/spec-acceptance-gate.md): the
  working-wireframe spec-acceptance gate. Implements principles §1b and produces
  the acceptance criteria that feed the §3 verification gate.

## How we evolve it

- **Principles-first.** Keep the *why* attached to every practice; that is what
  prevents cargo-culting.
- **Run changes as experiments, not rollouts.** One team, one change, a stated
  hypothesis, a few cycles, then inspect.
- **Constraints drive the agenda.** Re-run a Theory-of-Constraints pass
  periodically: a practice earns its place only if it relieves the *current*
  constraint.

## Status

Early draft (principles v0.1, gate practice v0.1). Open threads live in the
parking lot at the end of the principles doc.
