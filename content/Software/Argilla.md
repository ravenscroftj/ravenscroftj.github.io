---
public: true
date: 2024-03-01
title: Argilla
---

*   Argilla in [[Docker]]

*   By default see ms to want to use [[Software/ElasticSearch]]
*   does not have any credentials for elasticsearch
*   adding env var to disable security on elastic seems to work:

```yaml
environment:
    - xpack.security.enabled=false
```

*   The default credentials are `argilla` and `1234`
