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
