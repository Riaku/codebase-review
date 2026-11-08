---
categories: [deployment-release]
domains: [infrastructure]
---

# Toggle Registry

**MUST** declare every flippable setting in one registry that names its key, its default, and its owner.

**Why:** A toggle that exists only at its call site cannot be found, audited, or retired, so the flip surface grows until nobody can answer what this deploy is allowed to change.

**Detect:** diff the provider's toggle list or the registry file against `grep -rn 'isEnabled(\|getenv(\|os.environ\|process.env\|config.get('`; report any key read in code but absent from the registry, any registry entry with no reader, and any boolean default hardcoded at the call site instead of declared.

**References:** Feature toggles (Fowler), https://martinfowler.com/articles/feature-toggles.html, OpenFeature specification, https://openfeature.dev/docs/reference/intro, The Twelve-Factor App, config, https://12factor.net/config
