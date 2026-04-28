---
title: API Security FAQs
description: Frequently asked questions about AccuKnox API Security and API posture protection.
hide:
  - toc
---

# API Security

??? "**1. What problems does AccuKnox API Security solve?**"
    AccuKnox API Security protects APIs from runtime exposure, shadow endpoints, unsafe request patterns, and compliance drift. It gives API teams visibility into active traffic, detects undocumented or unused APIs, and helps secure live services before they become an attack surface.

??? "**2. Which API platforms and connectors does AccuKnox support?**"
    AccuKnox supports API traffic connectors for AWS API Gateway, Kubernetes-based API proxies, Istio, Nginx ingress, Kong, and F5. This means teams can secure both cloud-native and hybrid API deployments with a consistent control plane.

??? "**3. How does AccuKnox discover and organize APIs?**"
    AccuKnox discovers APIs from runtime traffic and OpenAPI/Swagger specifications. It organizes endpoints into inventory records and collections, allowing you to group APIs by host, path patterns, methods, or custom filters for targeted scans and reporting.

??? "**4. What kinds of API findings does the platform provide?**"
    The platform reports Shadow APIs (traffic-only endpoints), Zombie APIs (defined but inactive), Orphan APIs (documented but unused), and Active APIs. These findings help you identify unexpected behavior, unused attack surfaces, and drift between design and runtime.

??? "**5. How do I use API specs and scans to improve my API posture?**"
    Upload your OpenAPI/Swagger spec, map it to runtime traffic, and run scans to compare expected API behavior against actual requests. This lets you catch undocumented endpoints, ensure compliance with API contracts, and prioritize fixes on high-risk API findings.
