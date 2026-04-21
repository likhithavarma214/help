---
title: Setting Up Jenkins SAST with AccuKnox Default Scanner for Code Security
description: Integrate AccuKnox SAST with Jenkins CI/CD pipeline to detect security vulnerabilities in source code.
---

# AccuKnox SAST Scan in Jenkins  
## End User Guide

This guide explains how to configure and run AccuKnox SAST scans in Jenkins pipelines.

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
    stage('SAST Scan') {
      steps {
        AccuKnoxSAST()
      }
    }
  }
}
```

## Conclusion

Once the AccuKnox SAST Scanner is set up, it seamlessly performs SAST scans in the Jenkins pipelines and sends the results to AccuKnox SaaS for centralized management. This ensures that security issues are captured and addressed during the CI/CD pipeline, enhancing the security posture of your application.