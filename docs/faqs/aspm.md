---
title: ASPM FAQs
description: Frequently asked questions about AccuKnox Application Security Posture Management (ASPM) - SAST, DAST, IaC scanning, secrets scanning, and DevSecOps.
hide:
  - toc
---

# ASPM (Application Security Posture Management)

??? "**1. What is the differentiation of AccuKnox in ASPM Security?**"
    In the ASPM Security solution, unlike other tools, AccuKnox provides flexibility to integrate a variety of open source and commercial security scanning tools through built-in parsers to provide you a composite security posture of your infrastructure. This is mainly done for the following two contexts:

    + Remove dependencies and scoped results from one tool
    + Bring in contextual understanding of vulnerabilities and prioritization based on that

    Further on this, we also correlate and normalize results from a variety of security scanning tools and provide detailed results of vulnerabilities across infrastructure.

??? "**2. What components of ASPM are supported by AccuKnox?**"
    AccuKnox provides a comprehensive ASPM solution integrated within our CNAPP. The core components include:
    + Static Application Security Testing (SAST)
    + Dynamic Application Security Testing (DAST)
    + Secrets Scanning
    + Infrastructure as Code (IaC) Scanning
    + Container Scanning

??? "**What are the different frameworks supported by IaC scanning?**"
    AccuKnox's IaC scanning is designed to support industry-standard frameworks and languages. Our primary focus is on providing broad coverage for the most common tools used in modern DevOps environments, ensuring misconfigurations are identified before they reach production.

??? "**We are currently handling manual pen testing of our endpoints every few months. However, we see the risk of exposure if the DevOps/dev team makes a basic configuration change that could leave us vulnerable for a longer period. How can AccuKnox help?**"
    AccuKnox directly addresses this gap by shifting security from periodic point-in-time assessments to a continuous, automated process. Our platform helps in the following ways:
    + Pipeline Integration: We integrate security checks directly into your CI/CD pipeline, catching vulnerabilities and misconfigurations automatically with every build and deployment.
    + Continuous Compliance: The platform continuously monitors your cloud and Kubernetes environments for configuration drift and compliance violations, providing real-time alerts.
    + Prioritization and Automation: Instead of manual checks, you can focus on automating security and prioritizing the most critical risks identified by the platform across your entire software development lifecycle.
    This "built-in, not bolted-on" approach drastically reduces the window of exposure that exists between manual penetration tests.

??? "**Does AccuKnox provide auto-patching or auto-PR creation services?**"
    This capability is currently a work in progress and is scheduled to be available by October 2025.

??? "**Is AccuKnox tooling natively integrated with IDE?**"
    No, AccuKnox does not provide a native IDE plugin. Our strategy focuses on integrating security at the most critical control plane: the DevOps pipeline. Users can continue using their preferred IDE and its existing tooling, while AccuKnox provides native integration with CI/CD tools like Jenkins, Azure DevOps, and GitHub Actions to ensure security is enforced centrally and consistently.

---

[SCHEDULE DEMO](https://www.accuknox.com/contact-us){ .md-button .md-button--primary }
