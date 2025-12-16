---
title: LLM Static Scans
description: Learn how to perform LLM Static Scans using AccuKnox for GitHub and Hugging Face repositories to secure your Large Language Models.
---

# LLM Static Scans

AccuKnox provides static analysis for Large Language Models (LLM) to identify vulnerabilities, security risks, and compliance issues. This guide walks you through setting up and running LLM Static Scans for models hosted on GitHub and Hugging Face.

!!! tip "Subprompts and Probes"
    For a detailed list of subprompts and probes that ML and LLM scans rely on, please refer to the [Subprompts Categories](https://help.accuknox.com/use-cases/subprompts-categories/) page.

??? info "Why are LLM Scans Needed?"

    Large Language Models are becoming integral parts of modern applications, but they also introduce new attack vectors. LLM Static Scans are essential for:

    * **Vulnerability Detection**: Identifying known vulnerabilities in model files and configurations.
    * **Supply Chain Security**: Ensuring that models imported from public repositories (like Hugging Face) are safe to use.
    * **Compliance**: Meeting security standards by scanning AI/LLM assets for risks.
    * **Model Integrity**: Verifying that model weights and configurations have not been tampered with.

## Setting up an LLM Static Scan

Follow these steps to configure a scan for your LLM models.

### Step 1: Add a New Collector

1. Navigate to **Settings** > **Collectors** in the AccuKnox dashboard.
2. Click on **Add Collector**.
3. Select **LLM-Static-Scan** from the available options.
4. Choose your platform: **GitHub** or **Hugging Face**, depending on where your models reside.

![Select ML Static Scan](image-2.png)

### Step 2: Configure Repository Details

Enter the required credentials and repository information.

**For GitHub:**

* **Token**: Your GitHub Personal Access Token (PAT).
* **Repository Owner**: The username or organization name.
* **Repository Name**: The name of the repository.
* **Repository Branch**: The branch to scan (e.g., `main`).

**For Hugging Face:**

* **Token**: Your Hugging Face Access Token.
* **Repository Name**: The name of the model repository (e.g., `meta-llama/Llama-2-7b`).

![Configure Repository](image-3.png)

### Step 3: Add Identifiers

Add **Labels** and **Tags** to categorize your LLM models. This helps in filtering and managing assets within the AccuKnox platform.

### Step 4: Validate Connection

Once you have entered the credentials, click on **Test** to validate the connection to your repository. Ensure the validation is successful before proceeding.

### Step 5: Schedule the Scan

Configure the **Schedule and Notification** settings:

1. Under **Cron Job**, define the frequency of the scan (e.g., daily, weekly).
2. The system will display the **Next Scan** time based on your configuration.

![Schedule Scan](image-4.png)

Click **Save** to create the collector.

## Viewing Scan Results

Once the scan is triggered (either manually or via the schedule), AccuKnox will analyze the repository.

1. Go to **Issues** or the **Collectors** page.
2. Click on the **Findings** count for your LLM Static Scan collector.

![ML Findings](image-10.png)

You will be redirected to the **LLM Findings** page, which lists details such as:

* **Vulnerability Name**: The specific issue detected.
* **Model Path**: Location of the vulnerable file.
* **Source**: The repository source.
* **Scanner & Operator**: Tools used for detection.
* **Last Seen**: Timestamp of the latest detection.

![ML Findings List](image-6.png)

## Analyzing Findings

Click on any finding to open the **Detailed Pane**. Here you can:

* View a detailed **Description** of the vulnerability.

* **Create Ticket**: Integrate with your ticketing system (e.g., Jira) to track remediation.
* **Ask AI**: Use the "Ask AI" button for assisted remediation advice.

![Detailed Finding View](image-7.png)

* See the recommended **Solution**.
![Remediation Advice](image-8.png)

* Access **Raw Information** for in-depth analysis.
![Additional Details](image-9.png)
