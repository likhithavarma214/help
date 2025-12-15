---
title: On-Prem Single Node Installation Guide
description: Step-by-step guide for installing AccuKnox on a single node (Ubuntu 24.04).
---

# On-Prem Single Node Installation Guide

!!! info "Environment"
    Installation tested on **Ubuntu 24.04**.

## Prerequisites

!!! warning "Hardware Requirements"
    **VM:** 8vCPU/32GB Memory And 256GB Storage

## Installation Steps

### 1. Download Accuknox Installation Bundle

```bash
wget https://accuknox-onprem.s3.eu-west-2.amazonaws.com/Accuknox-cp.tar.gz
```

### 2. Extract Accuknox Installation Bundle

```bash
tar -xvf Accuknox-cp.tar.gz
cd Accuknox/
```

### 3. Extract Helm Chart

```bash
tar -xvf Helm-charts-accuknox-stable-helm-chart-v3.3-Dec-08.tar.gz
cd Helm-charts-accuknox-stable-helm-chart-v3.3-Dec-08
```

### 4. Install Binaries and K3s

```bash
./binaries.sh
./airgapped_k3s.sh
```

## Configuration

Update the following fields in `override-values.yaml`:

### Storage Configuration

Use the default storageclass (`local-path`) if you are deploying on k3s. Update the `StorageClass` `<storageclass>` to `local-path`.

### Ingress Configuration

For IP-based deployment (recommended for POC):


| Parameter                     | Value            |
| :---------------------------- | :--------------- |
| `ingressGateway.enabled`      | `true`           |
| `nginxIngressGateway.enabled` | `true`           |
| `loadBalancerHost`            | `"<PRIVATE-IP>"` |

### SSL Configuration

If you are deploying with ip IP-based method make SSL false:

| Parameter         | Value   |
| :---------------- | :------ |
| `ssl.selfsigned`  | `false` |
| `ssl.customcerts` | `false` |

### 5. Install AccuKnox Charts

```bash
./install_chart.sh
```

## Access the UI

- Open the UI (`https://<PRIVATE-IP>/`) in a browser
- To complete sign-up, please connect to AccuKnox team
