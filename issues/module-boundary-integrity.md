---
categories: [correctness-pitfalls, security-practices]
domains: [backend]
---

# Module Boundary Integrity

**MUST** keep module boundaries one-way and public: no import cycles between modules, and no module reading another's internals instead of its declared interface.

**Why:** A cycle fuses two modules into one unit that cannot be tested, replaced or reasoned about separately, and a reach past a public interface turns an internal rename in one module into a breaking change in another that nobody edited.
**Detect:** `lint-imports` (import-linter), `depcruise --validate` (dependency-cruiser), ArchUnit layer/cycle rules, or `madge --circular`; plus grep imports that bypass a public surface (`from billing._internal import`, `../../other-module/src/private/`).
**References:** https://import-linter.readthedocs.io/en/stable/; https://github.com/sverweij/dependency-cruiser; https://www.archunit.org/userguide/html/000_Index.html
