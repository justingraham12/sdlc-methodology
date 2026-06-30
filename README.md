# SDLC Methodology: AI-Augmented Software Delivery

A living, version-controlled methodology for building and delivering software in a
world where code generation is cheap and the binding constraints have moved to
**specification, verification, and integration**.

This README is the root: it states the reframe everything hangs off, explains how
the repo is organized, indexes the principles and practices, and describes how we
evolve the methodology.

## The reframe (the lens for everything here)

For decades, writing code was the bottleneck, and almost every practice we
inherited (specialized SDLC roles, story-point estimation, sprint time-boxing,
heavyweight coordination frameworks) is machinery built to manage the scarcity and
cost of producing code.

Agents collapse the cost of generation toward zero. So the constraint **moves**.
It moves to:

- **Specification.** Knowing precisely what to build.
- **Verification.** Trusting that what got built is correct and safe to own.
- **Integration.** Keeping many fast, locally-correct changes globally coherent.

Every principle in this repo is downstream of this single shift. When in doubt,
ask: *does this practice relieve the new constraint, or is it machinery for the
old one?*

## How this repo is organized

- **Principles** (`principles/`) are the durable *why*. They change slowly and
  only with good reason. Each principle is its own file with a **stable canonical
  number** (`§1`, `§2`, ...). Numbers are never reused or reordered; new
  principles only append. This keeps every cross-reference (including from the
  practice docs) valid forever, independent of reading order.
- **Practices** (`practices/`) are the swappable *how*. They implement principles
  and are expected to be iterated, replaced, or retired as we learn. Practices are
  a catalog with no inherent order, so they are named by slug rather than numbered.

When a practice and a principle conflict, either the principle wins or the
principle is wrong. Decide which, explicitly.

## Principles

| # | Principle | File |
|---|-----------|------|
| §1 | Roles (builder + verifier, intent roles, architect) | [`principles/01-roles.md`](principles/01-roles.md) |
| §2 | Pairing: builder + verifier at the terminal | [`principles/02-pairing.md`](principles/02-pairing.md) |
| §3 | The verification bottleneck | [`principles/03-verification-bottleneck.md`](principles/03-verification-bottleneck.md) |
| §4 | Process: flow over ceremony | [`principles/04-flow-over-ceremony.md`](principles/04-flow-over-ceremony.md) |
| §5 | Disposable code, durable specs | [`principles/05-disposable-code-durable-specs.md`](principles/05-disposable-code-durable-specs.md) |
| §6 | Metrics that match the new constraint | [`principles/06-metrics.md`](principles/06-metrics.md) |
| §7 | Agency and scope: engineers own more and drive more value | [`principles/07-agency-and-scope.md`](principles/07-agency-and-scope.md) |

A **lifecycle diagram** showing how the roles engage from inception through
delivery to maintenance (and where the two gates sit) is in
[`principles/01-roles.md`](principles/01-roles.md) under §1d.

## Practices

| Practice | Implements | File |
|----------|-----------|------|
| Working-wireframe spec-acceptance gate | §1a, feeds §3 | [`practices/spec-acceptance-gate.md`](practices/spec-acceptance-gate.md) |
| Pull-request review gate (change acceptance) | §3, closes the spine from §1a | [`practices/pr-review-gate.md`](practices/pr-review-gate.md) |

The two gates are two ends of one **verification spine**: the spec-acceptance gate
defines the acceptance criteria before any code exists, and the PR-review gate
confirms the build against those same criteria at merge.

## How we evolve this methodology

- **Principles-first, practices swappable.** Cargo-culting happens when people
  adopt the practice and lose the *why*. Keep the why attached.
- **Run changes as experiments, not rollouts.** One team, one change, a stated
  hypothesis, a few cycles, then inspect. This is the most XP-consistent way to
  invent an XP successor.
- **Constraints, not practices, drive the agenda.** Periodically re-run a
  Theory-of-Constraints pass: where does work pile up *now*? A practice earns its
  place only if it relieves the current constraint.

Treat every principle as a hypothesis we are testing in production. Each should
eventually carry the practice that implements it and the metric that tells us it
is working.

## Adopting this methodology

Coming from SAFe, Scrum, Kanban, Waterfall, or ad hoc agentic work? The
[`ADOPTING.md`](ADOPTING.md) guide compares each against this approach and gives
the first moves for migrating from where you are.

## Open threads

Active, unresolved work lives in [`OPEN-THREADS.md`](OPEN-THREADS.md). (GitHub
Issues is the likely long-term home, one thread per issue.)

## Status

Early draft (principles and practices at v0.1).
