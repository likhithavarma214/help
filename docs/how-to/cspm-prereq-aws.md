---
title: Pre-requisite for AWS
description: Onboarding pre-requisites for AWS accounts, including necessary permissions and configurations for secure integration.
---

# Pre-requisite for AWS Cloud Account Onboarding

## CSPM Pre-requisite for AWS

When the AccuKnox control plane is hosted in a cloud environment, scanning is performed using Cloud account Readonly Access permissions.

![image](images/aws-arch.png)

AWS onboarding requires creation of an IAM user. Please follow the following steps to provide a user with appropriate read access:

**Step 1:** Navigate to IAM → Users and click on Add Users

![image](images/iam-user-0.png)

**Step 2:** Give a username to identify the user

![image](images/iam-user-1.png)

**Step 3:** In the "Set Permissions" screen:

a. Select "Attach policies directly"

b. Search "ReadOnly", Filter by Type: "AWS managed - job function" and select the policy

![image](images/iam-user-2.png)

c. Search "SecurityAudit", Filter by Type: "AWS managed - job function" and select the policy

![image](images/iam-user-3.png)

**Step 4:** Finish creating the user. Click on the newly created user and create the Access key and Secret Key from the Security Credentials tab to be used in the AccuKnox panel

![image](images/iam-user-4.png)

## Permissions for AI Asset Scanning (AWS)

### General Scan Permission (Required)

Create an **IAM User** and attach the following managed policies:

    * `ReadOnly` (AWS managed -- job function)
    * `SecurityAudit` (AWS managed -- job function)

### Permissions for Bedrock & SageMaker

Create an **inline policy** with the following permissions:

=== "Bedrock"

    ```json
    [
        "bedrock:InvokeModel",
        "bedrock:ListImportedModels",
        "bedrock:ListModelInvocationJobs"
        "aws-marketplace:Subscribe",
        "aws-marketplace:ViewSubscriptions"
    ]
    ```

=== "SageMaker"

    ```json
    [
        "sagemaker:InvokeEndpoint"
    ]
    ```

=== "Bedrock AgentCore"

    ```json
    [
        "bedrock-agentcore:GetEvaluator",
        "bedrock-agentcore:InvokeAgentRuntime",
        "bedrock-agentcore:ListPolicies",
        "bedrock-agentcore:ListOnlineEvaluationConfigs",
        "bedrock-agentcore:ListPolicyEngines",
        "bedrock-agentcore:GetPolicyEngine",
        "bedrock-agentcore:ListTagsForResource",
        "bedrock-agentcore:ListActors",
        "bedrock-agentcore:GetOnlineEvaluationConfig",
        "bedrock-agentcore:ListEvaluators",
        "bedrock-agentcore:GetPolicy"
    ]
    ```

## Configure IAM User for AI Asset Scanning (AWS)

1. Navigate to **IAM > Users > Create User**.
2. Select the AWS managed policies **ReadOnlyAccess** and **SecurityAudit** to attach to the user.
3. Go to **Add Permissions > Create inline policy**.
    * **For AgentCore permissions**, add an additional inline policy by selecting the service **Bedrock-Agentcore**.
    * Allow the required read and runtime actions (including `InvokeAgentRuntime`, `GetEvaluator`, `GetPolicy`, `GetPolicyEngine`, `GetOnlineEvaluationConfig`, and the corresponding `List*` actions such as `ListPolicies`, `ListPolicyEngines`, `ListEvaluators`, `ListOnlineEvaluationConfigs`, `ListActors`, and `ListTagsForResource`).
    * Set **Resources** to **All**.

        ![alt text](image-52.png)

        ![alt text](image-53.png)

        ![alt text](image-54.png)

4. For **SageMaker Permissions**, add another set of permissions by selecting the service **SageMaker**, allowing the action **InvokeEndpoint**, and choosing **All** under resources.
5. For **Bedrock Permissions**, select the service **Bedrock**, allow the actions **InvokeModel**, **ListImportedModels**, and **ListModelInvocationJobs**, and choose **All** under resources.
6. Finally, review and create the policy to attach it to the IAM user.

- - -
[SCHEDULE DEMO](https://www.accuknox.com/contact-us){ .md-button .md-button--primary }
