---
categories: [testing-strategy]
domains: [backend, infrastructure]
---

# Performance Regression Gate

**SHOULD** benchmark the hot paths that carry latency or memory cost against a stored baseline in CI, and fail the change that regresses beyond the harness's noise band.

**Why:** Without a baseline, performance only gets attention after an incident, and the commit that doubled a hot path's cost is indistinguishable from the hundred that did not.

**Detect:** look for a benchmark suite wired into CI — `pytest-benchmark` with `benchmark-action/github-action-benchmark`, `criterion` (Rust), `go test -bench` with `benchstat`, `k6` thresholds on end-to-end latency — and a committed baseline to compare against; a suite that prints numbers without comparing them, or a threshold loose enough to swallow the regression, is the finding.

**References:** pytest-benchmark, https://pytest-benchmark.readthedocs.io/en/latest/, github-action-benchmark, https://github.com/benchmark-action/github-action-benchmark, criterion benchmarks, https://bheisler.github.io/criterion.rs/book/
