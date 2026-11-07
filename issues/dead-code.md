---
categories: [correctness-pitfalls]
domains: [backend]
---

# Dead Code

**SHOULD NOT** ship code paths that cannot be reached (no call site, permanently-off feature flag, disabled branch); an unexercised reachable branch is a coverage finding, not dead code.

**Why:** Unreachable branches hide vulnerabilities that no test covers, rot silently, and mislead reviewers into trusting unverified logic.

**Detect:** `vulture` (Python), `knip` (JS/TS), `deadcode` or `staticcheck` U1000 (Go) for zero-call-site symbols; grep `if False`, commented-out blocks, feature flags permanently off. An exclusion entry added to silence the detector is the finding, not the fix.

**References:** CWE-561
