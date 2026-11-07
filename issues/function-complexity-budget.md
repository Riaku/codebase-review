---
categories: [correctness-pitfalls]
domains: [backend]
---

# Function Complexity Budget

**SHOULD** keep each function under a measured complexity, length, and nesting budget, and fail the pipeline when a change pushes one over.

**Why:** Every branch multiplies the paths a reviewer and a test suite must cover, so an unbounded function drifts into a shape where the error branches are never exercised and nobody holds the whole flow in their head.

**Detect:** run `radon cc -s` (Python), `ruff check --select C901`, `eslint complexity` with `max-depth` and `max-lines-per-function` (JS/TS), `gocyclo` or `golangci-lint cyclop` (Go), PMD or Checkstyle `CyclomaticComplexity` (JVM); flag functions over the project threshold, and check the gate ratchets on changed files rather than printing a full-repo total nobody has to lower.

**References:** Radon complexity metrics, https://radon.readthedocs.io/en/latest/, Sonar cognitive complexity, https://www.sonarsource.com/resources/cognitive-complexity/
