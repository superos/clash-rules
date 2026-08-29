# clash-rules

Clash proxy rules for AI providers blocked in China.

### Cache

jsDelivr CDN caches the `@master` branch for up to **12 hours**. If you modify `ai.yaml`, `hk.yaml`, or any rule file, new clients may still pull stale content until the cache expires or is purged.

Force refresh:

https://www.jsdelivr.com/tools/purge

Also consider pinning to a commit hash for production stability.

---

```yaml
HttpDomainRule: &HttpDomainRule { type: http, behavior: domain, interval: 86400 }
HttpIPRule: &HttpIPRule { type: http, behavior: ipcidr, interval: 86400 }

rule-providers:
  hk: { <<: *HttpIPRule, url: https://cdn.jsdelivr.net/gh/superos/clash-rules@main/hk.yaml, path: ./ruleset/hk.yaml }
  ai: { <<: *HttpDomainRule, url: https://cdn.jsdelivr.net/gh/superos/clash-rules@main/ai.yaml, path: ./ruleset/ai.yaml }

rules:
  - RULE-SET,hk,DIRECT
  - RULE-SET,ai,US
  - MATCH,DIRECT
```

`hk.yaml` is used for direct access to Hong Kong cloud ranges and should be placed before the AI provider rules so those IP ranges bypass the proxy.
