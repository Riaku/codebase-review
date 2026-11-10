---
categories: [resilience]
domains: [reliability]
---

# Retries on Non-Idempotent Operations

**MUST NOT** automatically retry a non-idempotent operation unless the retry carries an idempotency key or the server deduplicates replays.

**Why:** A retried create after a timeout is indistinguishable from a second request, because the first attempt may already have committed; the duplicate charge, order, or email surfaces as corrupted state rather than as an error the client can see and handle.
**Detect:** Grep retry decorators, interceptors and policies (`@Retryable`, `RetryPolicy`, `urllib3.Retry`, `retry_on`, gRPC `retryPolicy`) for method scoping; flag blanket retries that include POST/PATCH or money-moving calls with no `Idempotency-Key` header, and queue consumers that redeliver creates with no dedupe key.
**References:** RFC 9110 idempotent methods, https://www.rfc-editor.org/rfc/rfc9110.html#name-idempotent-methods, Stripe idempotent requests, https://docs.stripe.com/api/idempotent_requests, gRPC client retries design, https://github.com/grpc/proposal/blob/master/A6-client-retries.md
