---
title: Predefined variables
description: A comprehensive list of all available predefined variables
ms.topic: reference
ms.assetid: 3A1C529F-DF6B-470A-9047-2758644C3D95
ms.author: jukullam
author: juliakm
ms.date: 12/12/2024
ms.custom:  copilot-scenario-highlight 
monikerRange: '<= azure-devops'
---

# Use predefined variables

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)]

Variables give you a convenient way to get key bits of data into various parts of your pipeline.
This is a list of predefined variables that are available for your use. There may be a few other predefined variables, but they're mostly for internal use.

These variables are automatically set by the system and read-only. (The exceptions are Build.Clean and System.Debug.) 

::: moniker range=">=azure-devops-2020"

In YAML pipelines, you can reference predefined variables as environment variables. For example, the variable `Build.ArtifactStagingDirectory` becomes the variable `BUILD_ARTIFACTSTAGINGDIRECTORY`.

For classic pipelines, you can use [release variables](../release/variables.md) in your deploy tasks to share the common information (for example, Environment Name, Resource Group, etc.).

::: moniker-end

Learn more about [working with variables](../process/variables.md).

::: moniker range="azure-devops"

> [!TIP]
> You can ask [Copilot](/copilot/) for help with variables. To learn more, see [Ask Copilot to generate a stage with a condition based on variable values](#ask-copilot-to-generate-a-stage-with-a-condition-based-on-variable-values).

::: moniker-end

## Build.Clean 

This is a deprecated variable that modifies how the build agent cleans up source.
To learn how to clean up source, see [Clean the local repo on the agent](../repos/pipeline-options-for-git.md#clean-the-local-repo-on-the-agent).

<h2 id="systemaccesstoken">System.AccessToken</h2>

`System.AccessToken` is a special variable that carries the security token used by the running build.

# [YAML](#tab/yaml)

In YAML, you must explicitly map `System.AccessToken` into the pipeline using a
variable. You can do this at the step or task level. For example, you can use `System.AccessToken` to authenticate with a container registry.

```yaml
steps:
- task: Docker@2
  inputs:
    command: login
    containerRegistry: '<docker connection>'
  env:
    SYSTEM_ACCESSTOKEN: $(System.AccessToken)
```

You can configure the default scope for `System.AccessToken` using [build job authorization scope](../process/access-tokens.md#job-authorization-scope). 

# [Classic](#tab/classic)

You can allow scripts and tasks to access System.AccessToken at the job level.

1. Navigate to the job

1. Under **Additional options**, check the **Allow scripts to access the OAuth token** box.

Checking this box also leaves the credential set in Git so that you can run
pushes and pulls in your scripts.

---

## System.Debug

For more detailed logs to debug pipeline problems, define `System.Debug` and set it to `true`. 

1. Edit your pipeline. 
1. Select **Variables**. 
1. Add a new variable with the name  `System.Debug` and value `true`.

    :::image type="content" source="media/options/system-debug.png" alt-text="Set System Debug to true":::

1. Save the new variable. 

Setting `System.Debug` to `true` configures verbose logs for all runs. You can also configure verbose logs for a single run with the **Enable system diagnostics** checkbox. 

You can also set `System.Debug` to `true` as a variable in a pipeline or template. 

```yaml
variables:
  system.debug: 'true'
```

::: moniker range=">azure-devops-2022"

When `System.Debug` is set to `true`, an extra variable named `Agent.Diagnostic` is set to `true`. When `Agent.Diagnostic` is `true`, the agent collects more logs that can be used for troubleshooting network issues for self-hosted agents. For more information, see [Network diagnostics for self-hosted agents](../troubleshooting/review-logs.md#network-diagnostics-for-self-hosted-agents).

> [!NOTE]
> The `Agent.Diagnostic` variable is available with [Agent v2.200.0](https://github.com/microsoft/azure-pipelines-agent/releases/tag/v2.200.0) and higher.

::: moniker-end

For more information, see [Review logs to diagnose pipeline issues](../troubleshooting/review-logs.md).

::: moniker range=">=azure-devops"

[!INCLUDE [include](includes/variables-hosted.md)]

::: moniker-end

::: moniker range="= azure-devops-2022"

[!INCLUDE [include](includes/variables-server-2022.md)]

::: moniker-end

::: moniker range="= azure-devops-2020"

[!INCLUDE [include](includes/variables-server-2020.md)]

::: moniker-end

<a name="identity_values"></a>
### How are the identity variables set?

The value depends on what caused the build and are specific to Azure Repos repositories. 

| If the build is triggered... | Then the Build.QueuedBy and Build.QueuedById values are based on... | Then the Build.RequestedFor and Build.RequestedForId values are based on... |
| --- | --- | ---|
| In Git or by the [Continuous integration (CI) triggers](triggers.md) | The system identity, for example: `[DefaultCollection]\Project Collection Service Accounts` | The person who pushed or checked in the changes. |
| In Git or by a [branch policy build](../../repos/git/branch-policies.md#build-validation). | The system identity, for example: `[DefaultCollection]\Project Collection Service Accounts` | The person who checked in the changes. |
| In TFVC by a [gated check-in trigger](triggers.md) | The person who checked in the changes. | The person who checked in the changes. |
| In Git or TFVC by the [Scheduled triggers](triggers.md) | The system identity, for example: `[DefaultCollection]\Project Collection Service Accounts` | The system identity, for example: `[DefaultCollection]\Project Collection Service Accounts` |
| Because you clicked the **Queue build** button | You | You |

::: moniker range="azure-devops"

## Ask Copilot to generate a stage with a condition based on variable values

Use [Copilot](/copilot/) to generate a stage with a condition determined by the value of a variable.  

This example prompt defines a stage that runs when `Agent.JobStatus` indicates that the previous stage ran successfully:

> Create a new Azure DevOps stage that only runs when `Agent.JobStatus` is `Succeeded` or `SucceededWithIssues`.

You can customize the prompt to use values that meet your requirements. For example, you can ask for help creating a stage that only runs when a pipeline fails. 

> [!NOTE]
> GitHub Copilot is powered by AI, so surprises and mistakes are possible. Make sure to verify any generated code or suggestions. For more information about the general use of GitHub Copilot, product impact, human oversight, and privacy, see [GitHub Copilot FAQs](https://github.com/features/copilot#faq).

::: moniker-end