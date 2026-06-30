# §2. Pairing: Builder + Verifier at the Terminal

**Status:** Draft v0.1
**Canonical ID:** §2 (stable; numbers are never reused or reordered)

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

## 2a. STRONG PRINCIPLE: Protect the junior's time in the steering seat

The learning concentrates in the steering seat. The agent makes the senior so
fast that the pull toward "senior drives, junior watches" is *stronger* than it
ever was in classic pairing. Counteract it deliberately: build the handoff into
the ritual (ping-pong style), swap who holds the prompt on a cadence, regardless
of whose turn is "faster." Seat time is the thing we are actually allocating.

## 2b. STRONG PRINCIPLE: Don't let the agent anchor the pair

The agent is a confident, articulate third voice; classic pairing never had a
persuasive third party. The risk is both humans slide into reviewing the agent's
framing instead of forming their own. Discipline: before reading the agent's
output, each person states their own quick hypothesis about what good output
should look like. Then you review against your own model, not the agent's.

## 2c. Parallel-agent orchestration is its own literacy

Managing three or four agents at once has no classic analog. It's closer to
air-traffic control than to writing code, and it's the highest-leverage thing to
pair on precisely because it's so new and so cognitively distinct. Watching a
senior notice that agent #2 quietly went off the rails while attending to
agent #3, *and articulating how they noticed*, can't come from a doc.

**Literacies this practice exists to transmit:** context-building, decomposition,
parallel orchestration, output review / calibrated skepticism.
