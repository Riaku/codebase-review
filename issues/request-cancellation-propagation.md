---
categories: [correctness-pitfalls]
domains: [backend]
---

# Request Cancellation Propagation

**SHOULD** propagate the caller's cancellation through every downstream call and loop, so work stops when the client disconnects or the deadline expires.

**Why:** A handler that ignores cancellation keeps holding CPU, memory, and downstream connections for a response nobody will read, so one closed tab becomes load that outlives its request.

**Detect:** check handlers take a cancellable context or abort signal as the first parameter (`context.Context`, `AbortSignal`, `CancellationToken`), that `ctx.Done()` or `signal.aborted` is checked before each iteration of a long loop and passed into database and HTTP clients, and that server read and write timeouts are set; a `context.Background()` or a fresh `AbortController` created mid-handler is the finding.

**References:** Go context package, https://pkg.go.dev/context, MDN AbortSignal, https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal
