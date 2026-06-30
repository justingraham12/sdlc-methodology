# §5. Disposable Code, Durable Specs

**Status:** Draft v0.1
**Canonical ID:** §5 (stable; numbers are never reused or reordered)

**Principle.** If an implementation can be regenerated from a tight spec and a
strong test suite in an afternoon, then **the spec, the tests, and the
architectural constraints are the real assets**, and code is the cheap,
regenerable layer. Invest care accordingly. (Deeply continuous with TDD.)

This is the principle the working wireframe (§1b) instantiates: the prototype is
a durable spec, and the production code rebuilt from it is the disposable layer.
