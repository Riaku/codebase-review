---
categories: [seo-web-quality]
domains: [frontend]
---

# LLMs.txt Agent Guidance

**SHOULD** publish `/llms.txt` — and `/agents.txt` only where a platform documents consuming it — as a curated index of canonical pages and reuse terms.

**Why:** Agent-mediated answers come from whatever a model can parse from the site, so without a curated index it scrapes navigation, stale pages and retired docs, then attributes the wrong price or an expired policy to the product.
**Detect:** `curl -sI https://example.com/llms.txt` returns 200 `text/plain`; every URL it lists returns 200 and is indexable; flag a file listing sitemap URLs only, auth-gated pages, or noindex pages. `/agents.txt` has no published standard, so treat it as in scope only where a platform's own docs name it — absence is not a finding.
**References:** https://llmstxt.org/
