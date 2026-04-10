---
title: On-Prem Single Node Installation Guide
description: Step-by-step guide for installing AccuKnox on a single node (Ubuntu 24.04).
---

# On-Prem Single Node Installation Guide

This guide provides step-by-step instructions for installing AccuKnox on a single node.

!!! info "Supported Operating Systems"
    Installation was tested on **Ubuntu 24.04** and **Rocky Linux 8**.

## Prerequisites

### Hardware Requirements

* **VM:** 8 vCPU / 32GB Memory
* **Storage:** 256GB
* **Required Binaries:** `tar`, `wget`

!!! warning "Rocky Linux Users"
    SELinux should be disabled or set to permissive if you are installing on Rocky Linux.

## Installation Steps

### Step 1: Download the Installation Bundle

Download the AccuKnox bundle using `wget`:

```bash
wget https://accukno-xxxx-xxxx.xxxx.your-objectstorage.com/Accuknox-cp-v3_3.tar.gz
```

### Step 2: Extract the Installation Bundle

Extract the downloaded file, remove the archive to free up space, and navigate to the directory:

```bash
tar -xvf Accuknox-cp-v3_3.tar.gz
rm Accuknox-cp-v3_3.tar.gz
cd Accuknox/
```

### Step 3: Extract Helm Charts

Extract the Helm charts and navigate to their directory:

```bash
tar -xvf Helm-charts-accuknox-stable-helm-chart-v3.3-xx-xx.tar.gz
cd Helm-charts-accuknox-stable-helm-chart-v3.3-xx-xx
```

### Step 4: Install Dependencies

Run the scripts to install the required binaries and K3s:

```bash
./binaries.sh
./airgapped_k3s.sh
```

### Step 5: Configure Deployment Values

Update the necessary overrides in `override-values.yaml`. For an **IP-based deployment (recommended for POC)**, update the `nginxIngressGateway` with your appropriate `<PRIVATE-IP>`:

```yaml title="override-values.yaml"
ingressGateway:
  enabled: true
nginxIngressGateway:
  enabled: true
  loadBalancerHost: "<PRIVATE-IP>"
```

!!! note "SSL Configuration"
    If you are deploying with an IP-based method, disable SSL. The override values file should be updated as follows:

    ```yaml title="override-values.yaml"
    ssl:
      selfsigned: false
      customcerts: false
    ```

### Step 6: Install AccuKnox Charts

Execute the chart installation script:

```bash
./install_chart.sh
```

### Step 7: Access the UI and Complete Setup

1. Open the AccuKnox UI in your browser at: `https://<PRIVATE-IP>/`
2. Run the following command to retrieve the verification link:

    ```bash
    kubectl logs deploy/celery -n accuknox-divy | grep "check-email-verification"
    ```
3. To complete the sign-up process, please connect to the AccuKnox team.
