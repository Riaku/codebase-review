---
categories: [correctness-pitfalls]
domains: [backend]
---

# Release Resources on Every Exit Path

**MUST** release every resource it acquires — file handle, lock, connection, transaction, timer, subscription, temporary directory — on every exit path, including exceptions, early returns, and cancellation.

**Why:** A handle held only on the happy path leaks exactly when something goes wrong, so the failure a long-running service can least afford is the one that also holds the file descriptor, row lock, or pool slot until the process restarts.

**Detect:** grep `open(`, `acquire(`, `Lock`, `BEGIN`, `subscribe`, `setInterval`, `mkdtemp` for a `with`/`defer`/`try-finally`/`using`/RAII guard in the same scope; check React effects return a cleanup that unsubscribes and clears timers, and that HTTP clients, sessions, and response bodies are disposed. A `finally` that only logs is still a leak.

**References:** CWE-772 missing release of resource, https://cwe.mitre.org/data/definitions/772.html, Python context managers, https://docs.python.org/3/reference/datamodel.html, React effect cleanup, https://react.dev/reference/react/useEffect
