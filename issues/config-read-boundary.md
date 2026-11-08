---
categories: [correctness-pitfalls]
domains: [backend]
---

# Config Read Boundary

**MUST** read configuration at one boundary resolved during start-up, then pass the values down, rather than reading ambient environment from inside components.

**Why:** Scattered reads make the effective configuration unknowable from any single file, so a missing key fails at an arbitrary call site under production traffic instead of at start-up.

**Detect:** count `os.environ`, `getenv(`, `process.env`, and `config.get(` call sites per module; every hit outside the settings module is a finding, as is a default restated at a call site instead of declared once, and a test that mutates the process environment globally to reach a branch.

**References:** The Twelve-Factor App, config, https://12factor.net/config, Pydantic settings management, https://docs.pydantic.dev/latest/concepts/pydantic_settings/, Node.js `process.env`, https://nodejs.org/api/process.html#processenv
