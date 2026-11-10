---
categories: [observability, resilience]
domains: [reliability]
---

# Circuit Breaker State Alerting

**MUST** export circuit breaker transitions as metrics and events, and alert when a breaker stays open or repeatedly flaps.

**Why:** A breaker that opens silently converts an outage into a degraded feature nobody investigates, and each half-open probe that fails hands a recovering dependency fresh load; the state changes are the earliest evidence that a dependency is failing, well before clients report the symptom.
**Detect:** Grep breaker wiring and exporters for a state callback or gauge (`onStateChange`, `state_transition`, `circuit_breaker_state`, `resilience4j.circuitbreaker.state`, Hystrix `circuitBreaker.*` events) and alert rules that reference them; flag a breaker with no state series, and a dashboard that charts calls to a dependency but never its breaker.
**References:** resilience4j CircuitBreaker, https://resilience4j.readme.io/docs/circuitbreaker, Martin Fowler CircuitBreaker, https://martinfowler.com/bliki/CircuitBreaker.html, Microsoft circuit breaker pattern, https://learn.microsoft.com/en-us/azure/architecture/patterns/circuit-breaker
