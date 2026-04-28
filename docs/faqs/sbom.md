---
title: SBOM FAQs
description: Frequently asked questions about AccuKnox SBOM and supply chain risk management.
hide:
  - toc
---

# SBOM (Software Bill of Materials)

??? "**1. Why is SBOM important for my software supply chain?**"
    An SBOM provides a complete inventory of software components, dependencies, and versions used by an application. AccuKnox uses SBOMs to detect vulnerable libraries, verify component provenance, and reduce supply chain risk across CI/CD and runtime.

??? "**2. Which SBOM formats does AccuKnox support?**"
    AccuKnox supports standard SBOM formats such as CycloneDX and SPDX. This allows teams to ingest SBOMs from common tools and pipelines without needing custom translation.

??? "**3. How do I onboard SBOMs into AccuKnox?**"
    Create an SBOM project in the AccuKnox UI, upload your SBOM file, or automate ingestion through CI/CD workflows. Once onboarded, AccuKnox scans the SBOM for vulnerabilities, license issues, and dependency risk.

??? "**4. Can SBOM results be linked to vulnerability scanning and policy enforcement?**"
    Yes. SBOM findings can be combined with vulnerability data to show which components are risky and support enforcement rules in CI/CD. Teams can use SBOM-based policies to block builds or deployments when high-risk components are present.

??? "**5. How does AccuKnox help with SBOM change tracking?**"
    AccuKnox tracks SBOM updates over time so you can compare component lists across versions. This helps identify new dependencies, removed packages, and unexpected supply chain changes before they reach production.
