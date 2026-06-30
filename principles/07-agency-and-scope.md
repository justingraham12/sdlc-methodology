# §7. Agency and Scope

**Status:** Draft v0.1
**Canonical ID:** §7 (stable; numbers are never reused or reordered)

**Principle.** This methodology expands the agency of the individual engineer: a
broader scope of ownership, more influence over what gets built, and more leverage
per person than Agile or Kanban could offer. This is a direct consequence of the
reframe, not a perk added on top. When generation stops being the bottleneck, the
reasons to slice work into narrow, specialized, dependent roles fall away, and the
individual's reach grows.

## Why agency expands

- **Ownership widens from component to outcome.** Work was sliced by specialty
  (frontend, backend, SRE, QA) largely because no one person could produce across
  all of it fast enough; specialization was a throughput necessity. With that
  constraint gone, a builder owns a capability end to end (§1c). Scope moves from
  "my layer" to "this result."
- **Agents are leverage the individual controls directly.** In classic flow,
  output was bounded by your own hands, and scaling meant adding people and
  coordination. Now one engineer orchestrates several agents and commands the
  output that used to require a team, deciding for themselves how to deploy that
  capacity (§2c). That is agency in the literal sense.
- **Engineers move up the value chain.** Builders engage with the *what*, not only
  the *how*: they consume and pressure-test working wireframes (§1a), exercise
  architectural judgment (§1b), and own the specs and tests (§5). In Agile and
  Scrum the product owner held the *what* and developers held the *how*; here that
  boundary is porous and the engineer's influence reaches into what gets built and
  why.
- **Value shifts from production to judgment.** When the machine generates, the
  human's contribution becomes the high-agency work: taste, calibrated skepticism,
  verification, deciding what is right. An engineer's value is now their judgment,
  which is portable and compounds, rather than their typing throughput, which was
  fungible.
- **They own the durable assets.** Per §5, the specs, tests, and architectural
  constraints are the real assets and the code is the regenerable layer. Owning
  the durable part is more meaningful ownership than owning lines of code.

## The additional value over Agile and Kanban

Agile and Kanban were real advances: they improved flow and feedback and began the
de-siloing of teams. But both kept work sliced and kept the *what* / *how* split,
so an engineer's ceiling stayed their own hands and their component. Here the
ceiling is their judgment and how many agents they can steer, and their unit of
ownership is the outcome. The engineer is closer to a small autonomous team of one
person plus agents than to a specialist executing a slice.

## The honest counterweight

- **Agency rises with accountability.** Broader scope means the builder is on the
  hook for security, operability, and correctness that used to be diffused across
  specialists. This is demanding by design.
- **Breadth without depth is a trap.** A mile wide and an inch deep, with the agent
  papering over the gaps (§1a), is the failure mode of expanded scope. Agency is
  only value when paired with the judgment to wield it, which is why pairing (§2)
  exists.
- **The gates are not a cage.** The spec-acceptance and PR-review gates are what
  make it *safe* to grant one person this much scope. Structured verification is
  precisely the thing that lets an organization trust broad individual agency
  without falling back to committee oversight. Agency and the gates are
  complements, not opposites.
