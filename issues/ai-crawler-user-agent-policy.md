---
categories: [seo-web-quality]
domains: [frontend]
---

# AI Crawler User-Agent Policy

**MUST** name AI crawlers explicitly in `/robots.txt` — `GPTBot`, `ClaudeBot`, `CCBot`, `Google-Extended` — with the allow-or-deny policy the product actually intends.

**Why:** A lone `User-agent: *` group leaves AI-crawler consent implicit, so every training and answer crawler inherits the generic rules: a site that means to exclude them grants access by omission, and when the policy changes there is no diff, no review and no artifact to test.
**Detect:** `curl -s https://example.com/robots.txt | grep -i '^user-agent: .*\(gptbot\|claudebot\|ccbot\|google-extended\|perplexitybot\)'`; flag a public content site whose robots.txt has only the `*` group, and an AI group whose `Disallow: /` contradicts the pages the product wants cited.
**References:** RFC 9309, https://www.rfc-editor.org/rfc/rfc9309.html; https://platform.openai.com/docs/bots; https://developers.google.com/search/docs/crawling-indexing/google-common-crawlers
