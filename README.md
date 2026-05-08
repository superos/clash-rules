# clash-rules

Clash proxy rules for AI providers blocked in China.

### Cache

jsDelivr CDN caches `@master` branch for up to **12 hours**. Force refresh:

https://www.jsdelivr.com/tools/purge

---

```yaml
HttpRule: &HttpRule { type: http, behavior: domain, interval: 86400 }

...

rule-providers:
  ai: { <<: *HttpRule, url: https://cdn.jsdelivr.net/gh/superos/clash-rules/ai.yaml, path: ./ruleset/ai.yaml }

rules:
  - ...
  - RULE-SET, ai, US
  - MATCH, DIRECT
```
