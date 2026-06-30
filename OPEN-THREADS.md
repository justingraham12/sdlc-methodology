# Open Threads

The active parking lot for the methodology. Each item is unresolved work. The
likely long-term home for these is GitHub Issues (one thread per issue); kept here
as a file for now.

## Practice-shaped (ready to draft)

- **Builder + verifier pairing ritual.** Formalize §2 into a named practice: role
  definitions, the swap protocol, and the literacies it transmits
  (context-building, decomposition, parallel orchestration, output review).
- **Architect operating model.** Decide when one person wears the architect/PM
  hats together vs. when to split them, and how to mitigate bus-factor (see §1b).
- **Prototyping standard for the intent roles.** Resolve whether working
  wireframes need a shared standard (tools, what to include, what to deliberately
  leave out) so they are legible to builders (see §1a).
- **Agent harness / context platform ownership charter** (see §1c).

## Operational

- **Baseline the §6 metrics on one team** before changing anything else.

## Compliance sub-threads

- **SOC2 tier-to-reviewer mapping.** Confirm the exact mapping of risk tier to
  required number of human attestations, and which tiers (if any) permit automated
  merge. Owner: SOC2 owner. Context: `practices/pr-review-gate.md` (§3).

## Done (kept for traceability)

- ~~Define the working-wireframe spec-acceptance gate~~: drafted as
  `practices/spec-acceptance-gate.md` (v0.1). Open sub-thread: pilot on one team
  and feed results back into §1a.
- ~~Define the auditable risk-surface format for tiered review~~: addressed in
  `practices/pr-review-gate.md` (risk tiering with recorded tier + rationale per
  PR). Remaining sub-thread: the SOC2 mapping above.
