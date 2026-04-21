---
title: Jenkins Secret Scanning Integration
description: Integrate secret scanning in Jenkins pipelines with AccuKnox using TruffleHog to detect and manage sensitive data.
---

# Jenkins Secret Scanning Integration

## Overview

The **AccuKnox Secret Scanner** simplifies integrating secret scanning into Jenkins pipelines. This is used to detect sensitive data such as API keys, tokens, and secrets in the source code. The detected secrets are then uploaded to **AccuKnox SaaS** for centralized visibility and management.

## Key Features

1. **Secret Detection**: Scan repositories for sensitive information.

2. **Results Upload**: Seamlessly upload scan results to AccuKnox SaaS for centralized monitoring.

3. **Customizable Parameters**: Configure scanning options, including excluded paths, branch selection, and additional TruffleHog arguments.

This guide explains how to configure and run AccuKnox Secret scans in Jenkins pipelines.

## 1. One-Time Setup in Jenkins

### 1.1 Add Shared Library
Manage Jenkins → System → Global Trusted Pipeline Libraries

| Field | Value |
|------|------|
| Name | jenkins-aspm-scans |
| Default Version | main |
| Retrieval Method | Modern SCM |
| SCM | Git |
| Repository URL | https://github.com/accuknox/jenkins-aspm-scans |

### 1.2 Add Credentials
Manage Jenkins → Credentials → Global → Add Credentials

| ID | Type | Description |
|----|------|------------|
| accuknox-endpoint | Secret Text | AccuKnox API endpoint |
| accuknox-label | Secret Text | Project label |
| accuknox-token | Secret Text | AccuKnox API token |

## 2. Jenkinsfile Example
```groovy
@Library('jenkins-aspm-scans@main') _

pipeline {
  agent any
  environment {
    ACCUKNOX_ENDPOINT = credentials('accuknox-endpoint')
    ACCUKNOX_LABEL    = credentials('accuknox-label')
    ACCUKNOX_TOKEN    = credentials('accuknox-token')
  }
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/your-repo.git'
      }
    }
    stage('Secret Scan') {
      steps {
        AccuKnoxSecretScan()
      }
    }
  }
}
```


## Conclusion

By integrating the **AccuKnox Secret Scanning** into your CI/CD pipeline, you ensure that sensitive information is identified and securely managed during development. This streamlines secret scanning, centralizes findings in AccuKnox SaaS, and helps strengthen your organization's security posture.
