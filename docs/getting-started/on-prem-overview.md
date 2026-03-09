---
title: On-Premises Overview
description: Overview of On-Premises Deployment for AccuKnox
---

# On-Prem Deployment Modes

::cards:: cols=3

 - title: Installation Guide
   image: ./images/on-prem/install-guide.png
   url: ../getting-started/on-prem-installation-guide.md
   description: Step-by-step guide for AccuKnox on-prem installation.

 - title: Single Node Installation
   image: ./images/on-prem/single-node.png
   url: ../getting-started/on-prem-single-node-installation.md
   description: Deploy AccuKnox on a single node for quick setup.

 - title: Managed Installation (EKS, AKS, GKE)
   image: ./images/on-prem/managed-cloud.png
   url: ../getting-started/cluster-onboarding-managed.md
   description: Managed Kubernetes installation for AWS, Azure, and GCP.

 - title: Security on OpenShift
   image: ./images/on-prem/openshift.png
   url: ../getting-started/security-on-openshift.md
   description: Secure your OpenShift environment with AccuKnox.

 - title: Health Monitoring (RINC)
   image: ./images/on-prem/health-monitoring.png
   url: ../getting-started/health-monitoring.md
   description: Monitor cluster health and runtime security (RINC).

 - title: AWS Control Plane Installation
   image: ./images/on-prem/aws-control-plane.png
   url: ../getting-started/aws-control-plane-installation.md
   description: Install AccuKnox control plane on AWS for centralized management.

::/cards::

## High-Level Architecture Overview

![](./images/on-prem/3.png)

AccuKnox onprem deployment is based on Kubernetes native architecture.

## AccuKnox OnPrem k8s components

### Microservices

Microservices implement the API logic and provide the corresponding service endpoints. AccuKnox uses Golang-based microservices for handling streaming data (such as alerts and telemetry) and Python-based microservices for other control-plane services.

### Databases

PostgreSQL is used as a relational database and MongoDB is used for storing JSON events such as alerts and telemetry. Ceph storage is used to keep periodic scanned reports and the Ceph storage is deployed and managed using the Rook storage operator.

### Secrets Management

Within the on-prem setup, there are several cases where sensitive data and credentials have to be stored. Hashicorp's Vault is used to store internal (such as DB username/password) and user secrets (such as registry tokens). The authorization is managed purely using the k8s native model of service accounts. Every microservice has its service account and uses its service account token automounted by k8s to authenticate and subsequently authorize access to the secrets.

### Scaling

K8s native horizontal and vertical pod autoscaling is enabled for most microservices with upper limits for resource requirements.

### AccuKnox-Agents

Agents need to be deployed in target k8s clusters and virtual machines that have to be secured at runtime and to get workload forensics. Agents use Linux native technologies such as eBPF for workload telemetry and LSMs (Linux Security Modules) for preventing attacks/unknown execution in the target workloads. The security policies are orchestrated from the AccuKnox onprem control plane. AccuKnox leverages SPIFFE/SPIRE for workload/node attestation and certificate provisioning. This ensures that the credentials are not hardcoded and automatically rotated. This also ensures that if the cluster/virtual machine has to be deboarded then the control lies with the AccuKnox control plane.

## Onboarding Steps for AccuKnox

The onboarding process for AccuKnox's on-prem security solution consists of four concise steps:

![on-prem](images/on-prem/user_journey.png)

=== "Hardware & Prerequisites"
	* Verify hardware, email user, and domain configurations.
	* Ensure your environment meets all requirements.
	* **Time:** Varies, allocate sufficient time for review.

=== "Staging Images (Airgapped)"
	* Stage AccuKnox container images in airgapped setups.
	* Reconfirm hardware, email user, and domain requirements.
	* **Time:** ~1 hour.

=== "Installation"
	* Install AccuKnox system in your environment.
	* Ensure all prerequisites remain satisfied.
	* **Time:** ~45 minutes.

=== "Verification/Validation"
	* Confirm all steps completed successfully.
	* Validate hardware, email user, and domain configurations.
	* **Time:** ~1 hour.

AccuKnox onprem deployment is based on Kubernetes native architecture.
