---
title: Microsoft-hosted agents for Azure Pipelines
description: Learn about using the Microsoft-hosted agents provided in Azure Pipelines
ms.topic: conceptual
ms.assetid: D17E9C01-8026-41E8-B44A-AB17EDE4AFBD
ms.date: 08/01/2025
monikerRange: '<= azure-devops'
---

# Microsoft-hosted agents

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-eq-azure-devops.md)]

::: moniker range="< azure-devops"

Microsoft-hosted agents are only available with Azure DevOps Services, which is hosted in the cloud. You cannot use Microsoft-hosted agents or the Azure Pipelines agent pool with on-premises TFS or Azure DevOps Server. With these on-premises versions, you must use [self-hosted agents](agents.md).

[!INCLUDE [include](../../includes/version-selector.md)]

::: moniker-end

::: moniker range="azure-devops"

[!INCLUDE [include](includes/hosted-agent-intro.md)]

## Software

The **Azure Pipelines** agent pool offers several virtual machine images to choose from, each including a broad range of tools and software. You can see the installed software for each image by choosing the **Included Software** link in the following table. For more information on the software lifecycle and deprecation schedule of images and software, see [GitHub Actions Runner Images - Software and Image Support](https://github.com/actions/runner-images/tree/main?tab=readme-ov-file#software-and-image-support).

#### [Windows images](#tab/windows-images/)

You can see the installed software for each Windows hosted agent image by choosing the **Included Software** link in the table.

| Image | Classic Editor Agent Specification | YAML VM Image Label | Included Software |
| --- | --- | --- | --- |
| Windows Server 2025 with Visual Studio 2022 | *windows-2025* | `windows-2025` | [Link](https://github.com/actions/runner-images/blob/main/images/windows/Windows2025-Readme.md) |
| Windows Server 2022 with Visual Studio 2022 | *windows-2022* | `windows-latest` OR `windows-2022` | [Link](https://aka.ms/windows-2022-readme) |
| Windows Server 2019 with Visual Studio 2019 - See [Windows Server 2019 hosted image deprecation schedule](#windows-server-2019-hosted-image-deprecation-schedule)| *windows-2019* | `windows-2019` | [Link](https://aka.ms/windows-2019-readme) |

The **windows-2019** image is the default image for classic build pipelines. For more information, see [Designate a pool in your pipeline](pools-queues.md#designate-a-pool-in-your-pipeline).

#### Windows image updates

* [Windows Server 2025 with Visual Studio 2022 image is GA](https://aka.ms/azdo-windows)
  * The `windows-latest` label still refers to `windows-2022`. The change to `windows-2025` will be made in the future and this page will be updated at that time.
* [[Windows & Ubuntu] .NET 6 will be removed from the images on 2025-08-01.](https://github.com/actions/runner-images/issues/12241)
* [Windows Server 2019 hosted image deprecation schedule](#windows-server-2019-hosted-image-deprecation-schedule)

##### Windows Server 2019 hosted image deprecation schedule

The Windows Server 2019 image is scheduled to be deprecated:
* Deprecation start date: June 1, 2025
* Brownout period: June 3, 2025 to June 24, 2025
* Scheduled removal date for Windows Server 2019 hosted image: December 31, 2025

For more information, see [Upcoming Updates for Azure Pipelines Agents Images - Windows](https://aka.ms/azdo-windows)

#### [Linux images](#tab/linux-images/)

You can see the installed software for each Linux hosted agent image by choosing the **Included Software** link in the table.

| Image | Classic Editor Agent Specification | YAML VM Image Label | Included Software |
| --- | --- | --- | --- |
| Ubuntu 24.04 | *ubuntu-24.04* | `ubuntu-latest` OR `ubuntu-24.04` | [Link](https://github.com/actions/runner-images/blob/main/images/ubuntu/Ubuntu2404-Readme.md) |
| Ubuntu 22.04 | *ubuntu-22.04* | `ubuntu-22.04` | [Link](https://aka.ms/ubuntu-22.04-readme) |

The `ubuntu-latest` image is the default image for YAML pipelines if no image is specified. For more information, see [Designate a pool in your pipeline](pools-queues.md#designate-a-pool-in-your-pipeline).

#### Linux images updates

* [[Windows & Ubuntu] .NET 6 will be removed from the images on 2025-08-01.](https://github.com/actions/runner-images/issues/12241)
* The `ubuntu-latest` label has transitioned from `ubuntu-22.04` to `ubuntu-24.04`.
* [The Ubuntu 20.04 image is retired](https://devblogs.microsoft.com/devops/upcoming-updates-for-azure-pipelines-agents-images/#ubuntu).

#### [macOS images](#tab/macos-images/)

You can see the installed software for each macOS hosted agent by choosing the **Included Software** link in the table. When using macOS images, you can manually select from tool versions. [Read more](#mac-pick-tools).

| Image | Classic Editor Agent Specification | YAML VM Image Label | Included Software |
| --- | --- | --- | --- |
| macOS 15 Sequoia | *macOS-15* | `macOS-15` | [Link](https://github.com/actions/runner-images/blob/main/images/macos/macos-15-Readme.md) |
| macOS 14 Sonoma | *macOS-14* | `macOS-latest` OR `macOS-14` | [Link](https://aka.ms/macOS-14-readme) |
| macOS 13 Ventura | *macOS-13* | `macOS-13` | [Link](https://aka.ms/macOS-13-readme) |

#### macOS images updates

* The macOS 15 Sequoia hosted agent image is in GA.
 * The `macOS-latest` label still refers to `macOS-14`. The migration of `macos-latest` to refer to `macOS-15` will begin August 4, 2025, with a planned completion date of August 30, 2025. For more information, see [[macOS] macos-latest YAML-label will use macos-15 in August 2025](https://github.com/actions/runner-images/issues/12520).
* [[macOS] Xcode 15.4 will be removed from macOS15 images on May 29th, 2025](https://github.com/actions/runner-images/issues/12195)
* [The macOS-15 Sequoia image is available in preview](https://devblogs.microsoft.com/devops/upcoming-updates-for-azure-pipelines-agents-images/#mac-os)
* Apple silicon (ARM64) support for macOS image - for more information on joining the preview, see [Apple silicon (ARM64) support for macOS image](https://devblogs.microsoft.com/devops/upcoming-updates-for-azure-pipelines-agents-images/#mac-os).
* The macOS-12 Monterey image has been retired

* * *

> [!IMPORTANT]
> To request additional software to be installed on Microsoft-hosted agents, don't create a feedback request on this document or open a support ticket. Instead, open an issue on our [repository](https://github.com/actions/runner-images), where we manage the scripts to generate various images.


### How to identify pipelines using a deprecated hosted image

To identify pipelines that are using a deprecated image, browse to the following location in your organization: `https://dev.azure.com/{organization}/{project}/_settings/agentqueues`, and filter on the image name to check. The following example checks the `vs2017-win2016` image.

:::image type="content" source="media/pool-filter-vs2017-win2016.png" alt-text="Screenshot of filtering pipelines by image name.":::

You can also query job history for deprecated images across projects using the script located [here](https://github.com/microsoft/azure-pipelines-agent/tree/master/tools/FindPipelinesUsingRetiredImages), as shown in the following example.

```powershell
./QueryJobHistoryForRetiredImages.ps1 -accountUrl https://dev.azure.com/{org} -pat {pat}
```

## Use a Microsoft-hosted agent

# [YAML](#tab/yaml)

In YAML pipelines, if you do not specify a pool, pipelines default to the Azure Pipelines agent pool. You simply need to specify which virtual machine image you want to use.

```yaml
jobs:
- job: Linux
  pool:
    vmImage: 'ubuntu-latest'
  steps:
  - script: echo hello from Linux
- job: macOS
  pool:
    vmImage: 'macOS-latest'
  steps:
  - script: echo hello from macOS
- job: Windows
  pool:
    vmImage: 'windows-latest'
  steps:
  - script: echo hello from Windows
```

> [!NOTE]
> The specification of a pool can be done at multiple levels in a YAML file.
> If you notice that your pipeline is not running on the expected image, make sure that you verify the pool specification at the pipeline, stage, and job levels.

# [Classic](#tab/classic)

In classic build pipelines, you first choose the Azure Pipelines pool and then specify the image to use.

> [!NOTE]
> The specification of a pool can be done at multiple levels in a classic build pipeline - for the whole pipeline, or for each job. If you notice that your pipeline is not running on the expected image, make sure that you verify the pool specification at all levels.

---

### Avoid hard-coded references

When you use a Microsoft-hosted agent, always use [variables](../build/variables.md)
to refer to the build environment and agent resources. For example, don't
hard-code the drive letter or folder that contains the repository. The precise
layout of the hosted agents is subject to change without warning.

## Hardware

Microsoft-hosted agents that run Windows and Linux images are provisioned on Azure general purpose virtual machines with a 2 core CPU, 7 GB of RAM, and 14 GB of SSD disk space. These virtual machines are co-located in the same geography as your Azure DevOps organization.

Agents that run macOS images are provisioned on Mac pros with a 3 core CPU, 14 GB of RAM, and 14 GB of SSD disk space. These agents always run in the US irrespective of the location of your Azure DevOps organization. If data sovereignty is important to you and if your organization is not in the US, then you should not use macOS images. [Learn more](../../organizations/security/data-location.md).

All of these machines have at least 10 GB of free disk space available for your pipelines to run. This free space is consumed when your pipeline checks out source code, downloads packages, pulls docker images, or generates intermediate files.

> [!IMPORTANT]
> We cannot honor requests to increase disk space on Microsoft-hosted agents, or to provision more powerful machines. If the specifications of Microsoft-hosted agents do not meet your needs, then you should consider [self-hosted agents](agents.md) or [scale set agents](scale-set-agents.md) or [Managed DevOps Pools](../../managed-devops-pools/overview.md#usage-scenarios).

<a name="agent-ip-ranges"></a>

## Networking

In some setups, you may need to know the range of IP addresses where agents are deployed. For instance, if you need to grant the hosted agents access through a firewall, you may wish to restrict that access by IP address. Because Azure DevOps uses the Azure global network, IP ranges vary over time. Microsoft publishes a [weekly JSON file](https://www.microsoft.com/download/details.aspx?id=56519) listing IP ranges for Azure datacenters, broken out by region. This file is updated weekly with new planned IP ranges. Only the latest version of the file is available for download. If you need previous versions, you must download and archive them each week as they become available. The new IP ranges become effective the following week. We recommend that you check back frequently (at least once every week) to ensure you keep an up-to-date list. If agent jobs begin to fail, a key first troubleshooting step is to make sure your configuration matches the latest list of IP addresses. The IP address ranges for the hosted agents are listed in the weekly file under `AzureCloud.<region>`, such as `AzureCloud.westus` for the West US region.

Your hosted agents run in the same [Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/) as your organization. Each geography contains one or more regions. While your agent may run in the same region as your organization, it is not guaranteed to do so. To obtain the complete list of possible IP ranges for your agent, you must use the IP ranges from all of the regions that are contained in your geography. For example, if your organization is located in the **United States** geography, you must use the IP ranges for all of the regions in that geography.

To determine your geography, navigate to `https://dev.azure.com/<your_organization>/_settings/organizationOverview`, get your region, and find the associated geography from the [Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/) table. Once you have identified your geography, use the IP ranges from the [weekly file](https://www.microsoft.com/download/details.aspx?id=56519) for all regions in that geography.

> [!IMPORTANT]
> You cannot use private connections such as [ExpressRoute](https://azure.microsoft.com/services/expressroute/) or VPN to connect Microsoft-hosted agents to your corporate network. The traffic between Microsoft-hosted agents and your servers will be over public network.

### To identify the possible IP ranges for Microsoft-hosted agents

1. Identify the [region for your organization](../../organizations/accounts/change-organization-location.md) in **Organization settings**.
2. Identify the [Azure Geography](https://azure.microsoft.com/global-infrastructure/geographies/) for your organization's region.
3. Map the names of the regions in your geography to the format used in the weekly file, following the format of `AzureCloud.<region>`, such as `AzureCloud.westus`. You can map the names of the regions from the [Azure Geography](https://azure.microsoft.com/global-infrastructure/geographies/) list to the format used in the weekly file by reviewing the region names passed to the constructor of the regions defined in the [source code for the Region class](https://github.com/Azure/azure-libraries-for-net/blob/master/src/ResourceManagement/ResourceManager/Region.cs), from the [Azure Management Libraries for .NET](https://github.com/Azure/azure-libraries-for-net).
    > [!NOTE]
    > Since there is no API in the [Azure Management Libraries for .NET](https://github.com/Azure/azure-libraries-for-net) to list the regions for a geography, you must list them manually as shown in the following example.
1. Retrieve the IP addresses for all regions in your geography from the [weekly file](https://www.microsoft.com/download/details.aspx?id=56519). If your region is **Brazil South** or **West Europe**, you must include additional IP ranges based on your fallback geography, as described in the following note.

>[!NOTE]
>Due to capacity restrictions, some organizations in the **Brazil South** or **West Europe** regions may occasionally see their hosted agents located outside their expected geography. In these cases, in addition to including the IP ranges for all the regions in your geography as described in the previous section, additional IP ranges must be included for the regions in the capacity fallback geography.
>
>If your organization is in the **Brazil South** region, your capacity fallback geography is **United States**.
>
>If your organization is in the **West Europe** region, the capacity fallback geography is **France**.
>
>Our Mac IP ranges are not included in the Azure IPs above, as they are hosted in GitHub's macOS cloud. IP ranges can be retrieved using the [GitHub metadata API](https://docs.github.com/en/rest/reference/meta#get-github-meta-information) using the instructions provided [here](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners#ip-addresses).

#### Example

In the following example, the hosted agent IP address ranges for an organization in the West US region are retrieved from the weekly file. Since the West US region is in the United States geography, the IP addresses for all regions in the United States geography are included. In this example, the IP addresses are written to the console. 

```csharp
using Newtonsoft.Json.Linq;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace WeeklyFileIPRanges
{
    class Program
    {
        // Path to the locally saved weekly file
        const string weeklyFilePath = @"C:\MyPath\ServiceTags_Public_20230904.json";

        static void Main(string[] args)
        {
            // United States geography has the following regions:
            // Central US, East US, East US 2, East US 3, North Central US, 
            // South Central US, West Central US, West US, West US 2, West US 3
            // This list is accurate as of 9/8/2023
            List<string> USGeographyRegions = new List<string>
            {
                "centralus",
                "eastus",
                "eastus2",
                "eastus3",
                "northcentralus",
                "southcentralus",
                "westcentralus",
                "westus",
                "westus2",
                "westus3"
            };

            // Load the weekly file
            JObject weeklyFile = JObject.Parse(File.ReadAllText(weeklyFilePath));
            JArray values = (JArray)weeklyFile["values"];

            foreach (string region in USGeographyRegions)
            {
                string tag = $"AzureCloud.{region}";
                Console.WriteLine(tag);

                var ipList =
                    from v in values
                    where tag.Equals((string)v["name"], StringComparison.OrdinalIgnoreCase)
                    select v["properties"]["addressPrefixes"];

                foreach (var ip in ipList.Children())
                {
                    Console.WriteLine(ip);
                }
            }
        }
    }
}
```

### Service tags

Microsoft-hosted agents can't be listed by service tags. If you're trying to grant hosted agents access to your resources, you'll need to follow the IP range allow listing method.

## Security

Microsoft-hosted agents run on secure Azure platform. However, you must be aware of the following security considerations.

- Although Microsoft-hosted agents run on Azure public network, they are not assigned public IP addresses. So, external entities cannot target Microsoft-hosted agents. 
- Microsoft-hosted agents are run in individual VMs, which are re-imaged after each run. Each agent is dedicated to a single organization, and each VM hosts only a single agent.
- There are several benefits to running your pipeline on Microsoft-hosted agents, from a security perspective. If you run untrusted code in your pipeline, such as contributions from forks, it is safer to run the pipeline on Microsoft-hosted agents than on self-hosted agents that reside in your corporate network.
- When a pipeline needs to access your corporate resources behind a firewall, you have to allow the IP address range for the Azure geography. This may increase your exposure as the range of IP addresses is rather large and since machines in this range can belong to other customers as well. The best way to prevent this is to avoid the need to access internal resources. For information on deploying artifacts to a set of servers, see [Communication to deploy to target servers](agents.md#communication-to-deploy-to-target-servers).
- Hosted images do not conform to [CIS hardening benchmarks](https://www.cisecurity.org/benchmark/azure/). To use CIS-hardened images, you must create either self-hosted agents or scale-set agents or Managed DevOps pools.

## Capabilities and limitations

Microsoft-hosted agents:

* Have [the above software](#software). You can also add software during your build or release using [tool installer tasks](../process/tasks.md#tool-installers).
  * You get a freshly imaged agent for each job in your pipeline.
* Provide 10 GB of storage for your source and build outputs.
* Provide a free tier:
  * Public project: 10 free Microsoft-hosted parallel jobs that can run for up to 360 minutes (6 hours) each time, with no overall time limit per month. [Contact us](https://azure.microsoft.com/support/devops/) to get your free tier limits increased.
  * Private project: One free parallel job that can run for up to 60 minutes each time, until you've used 1,800 minutes (30 hours) per month. You can pay for additional capacity per parallel job. Paid parallel jobs remove the monthly time limit and allow you to run each job for up to 360 minutes (6 hours). [Buy Microsoft-hosted parallel jobs](https://marketplace.visualstudio.com/items?itemName=ms.build-release-hosted-pipelines).
  * When you create a new Azure DevOps organization, you are not given these free grants by default. To request the free grant for public or private projects, submit [a request](https://aka.ms/azpipelines-parallelism-request).
* Run on Microsoft Azure general purpose virtual machines [Standard_DS2_v2](/azure/virtual-machines/dv2-dsv2-series#dsv2-series).
* Run as an administrator on Windows and a passwordless sudo user on Linux.
* (Linux only) Run steps in a `cgroup` that offers 6 GB of physical memory and 13 GB of total memory.
* Use VM images that are regularly updated (every 3 weeks).

Microsoft-hosted agents do not offer:

* The ability to remotely connect.
* The ability to [drop artifacts to a UNC file share](/previous-versions/azure/devops/pipelines/artifacts/build-artifacts?view=tfs-2018&preserve-view=true#publish-from-tfs-to-a-unc-file-share).
* The ability to join machines directly to your corporate network.
* The ability to get bigger or more powerful build machines.
* The ability to pre-load custom software. You can install software during a pipeline run, such as through [tool installer tasks](../process/tasks.md#tool-installers) or in a script.
* Potential performance advantages that you might get by using self-hosted agents that might start and run builds faster. [Learn more](agents.md#private-agent-performance-advantages)
* The ability to run [XAML builds](/previous-versions/visualstudio/visual-studio-2013/ms181709(v=vs.120)).
* The ability to roll back to a previous VM image version. You always use the latest version.

If Microsoft-hosted agents don't meet your needs, then you can deploy your own [self-hosted agents](agents.md#install) or use [scale set agents](scale-set-agents.md) or [Managed DevOps Pools](../../managed-devops-pools/overview.md#usage-scenarios).

## FAQ

### How can I see what software is included in an image?

You can see the installed software for each hosted agent by choosing the **Included Software** link in the [Software](#software) table.

> [!NOTE]
> [!INCLUDE [include](includes/system-prefer-git-from-path.md)]

### How does Microsoft choose the software and versions to put on the image?

More information about the versions of software included on the images can be found at [Guidelines for what's installed](https://github.com/actions/runner-images/blob/main/docs/create-image-and-azure-resources.md). 

### When are the images updated?

Images are typically updated weekly. You can check the [status badges](https://github.com/actions/runner-images) which are in the format `20200113.x` where the first part indicates the date the image was updated.

### What can I do if software I need is removed or replaced with a newer version?

You can let us know by filing a GitHub issue by choosing the **Included Software** links in the [Use a Microsoft-hosted agent](#use-a-microsoft-hosted-agent) table.

You can also use a self-hosted agent that includes the exact versions of software that you need. For more information, see [Self-hosted agents](agents.md#install).

### What if I need a bigger machine with more processing power, memory, or disk space?

We can't increase the memory, processing power, or disk space for Microsoft-hosted agents, but you can use [self-hosted agents](agents.md#install) or [scale set agents](scale-set-agents.md) or [Managed DevOps Pools](../../managed-devops-pools/overview.md#usage-scenarios) hosted on machines with your desired specifications.

### I can't select a Microsoft-hosted agent and I can't queue my build or deployment. What should I do?

Microsoft-hosted agents are only available in Azure Pipelines and not in TFS or Azure DevOps Server.

By default, all project contributors in an organization have access to the Microsoft-hosted agents. But, your organization administrator may limit the access of Microsoft-hosted agents to select users or projects. Ask the owner of your Azure DevOps organization to grant you permission to use a Microsoft-hosted agent. See [agent pool security](pools-queues.md#security).

### My pipelines running on Microsoft-hosted agents take more time to complete. How can I speed them up?

If your pipeline has recently become slower, review our [status page](https://status.dev.azure.com/) for any outages. We could be having issues with our service. Or else, review any changes that you made in your application code or pipeline. Your repository size during check-out might have increased, you may be uploading larger artifacts, or you may be running more tests.

If you are just setting up a pipeline and are comparing the performance of Microsoft-hosted agents to your local machine or a self-hosted agent, then note the [specifications](#capabilities-and-limitations) of the hardware that we use to run your jobs. We are unable to provide you with bigger or powerful machines. You can consider using [self-hosted agents](agents.md) or [scale set agents](scale-set-agents.md) or [Managed DevOps Pools](../../managed-devops-pools/overview.md#usage-scenarios) if this performance is not acceptable.

### I need more agents. What can I do?

All Azure DevOps organizations are provided with several free parallel jobs for open-source projects, and one free parallel job and limited minutes each month for private projects. If you need additional minutes or parallel jobs for your open-source project, contact [support](https://azure.microsoft.com/support/devops/). If you need additional minutes or parallel jobs for your private project, then you can [buy more](../licensing/concurrent-jobs.md).

### My pipeline succeeds on self-hosted agent, but fails on Microsoft-hosted agents. What should I do?

Your self-hosted agent probably has all the right dependencies installed on it, whereas the same dependencies, tools, and software are not installed on Microsoft-hosted agents. First, carefully review the list of software that is installed on Microsoft-hosted agents by following the link to **Included software** in the table above. Then, compare that with the software installed on your self-hosted agent. In some cases, Microsoft-hosted agents may have the tools that you need (for example, Visual Studio), but all of the necessary optional components may not have been installed. If you find differences, then you have two options:

- You can create a new issue on the [repository](https://github.com/actions/runner-images), where we track requests for additional software. Contacting support can't help you set up new software on Microsoft-hosted agents.

- You can use [self-hosted agents](agents.md) or [scale set agents](scale-set-agents.md) or [Managed DevOps Pools](../../managed-devops-pools/overview.md#usage-scenarios). With these agents, you are fully in control of the images that are used to run your pipelines.

### My build succeeds on my local machine, but fails on Microsoft-hosted agents. What should I do?

Your local machine probably has all the right dependencies installed on it, whereas the same dependencies, tools, and software are not installed on Microsoft-hosted agents. First, carefully review the list of software that is installed on Microsoft-hosted agents by following the link to **Included software** in the table above. Then, compare that with the software installed on your local machine. In some cases, Microsoft-hosted agents may have the tools that you need (e.g., Visual Studio), but all of the necessary optional components may not have been installed. If you find differences, then you have two options:

- You can create a new issue on the [repository](https://github.com/actions/runner-images), where we track requests for additional software. This is your best bet for getting new software installed. Contacting support will not help you with setting up new software on Microsoft-hosted agents.

- You can use [self-hosted agents](agents.md) or [scale set agents](scale-set-agents.md) or [Managed DevOps Pools](../../managed-devops-pools/overview.md#usage-scenarios). With these agents, you are fully in control of the images that are used to run your pipelines.

### My pipeline fails with the error: "no space left on device".

Microsoft-hosted agents only have 10 GB of disk space available for running your job. This space is consumed when you check out source code, when you download packages, when you download docker images, or when you produce intermediate files. Unfortunately, we cannot increase the free space available on Microsoft-hosted images. You can restructure your pipeline so that it can fit into this space. Or, you can consider using [self-hosted agents](agents.md) or [scale set agents](scale-set-agents.md) or [Managed DevOps Pools](../../managed-devops-pools/overview.md#usage-scenarios).

### My pipeline running on Microsoft-hosted agents requires access to servers on our corporate network. How do we get a list of IP addresses to allow in our firewall?

See the section [Agent IP ranges](#agent-ip-ranges)

### Our pipeline running on Microsoft-hosted agents is unable to resolve the name of a server on our corporate network. How can we fix this?

If you refer to the server by its DNS name, then make sure that your server is publicly accessible on the Internet through its DNS name. If you refer to your server by its IP address, make sure that the IP address is publicly accessible on the Internet. In both cases, ensure that any firewall in between the agents and your corporate network has the [agent IP ranges](#agent-ip-ranges) allowed.

### I'm getting an SAS IP authorization error from an Azure Storage account

If you get an SAS error code, it is most likely because the IP address ranges from the Microsoft-hosted agents aren't permitted due to your Azure Storage rules. There are a few workarounds:

1. [Manage the IP network rules for your Azure Storage account](/azure/storage/common/storage-network-security?tabs=azure-portal#managing-ip-network-rules) and add the [IP address ranges for your hosted agents](#networking).
2. In your pipeline, use [Azure CLI to update the network ruleset for your Azure Storage account](/powershell/module/az.storage/update-azstorageaccountnetworkruleset) right before you access storage, and then restore the previous ruleset.
3. Use [self-hosted agents](agents.md#install) or [Scale set agents](scale-set-agents.md) or [Managed DevOps Pools](../../managed-devops-pools/overview.md#usage-scenarios).

<a name="mac-pick-tools"></a>
### How can I manually select versions of tools on the Hosted macOS agent?

#### Xcode

  If you use the [Xcode task](/azure/devops/pipelines/tasks/reference/xcode-v5) included with Azure Pipelines and TFS, you can select a version of Xcode in that task's properties. Otherwise, to manually set the Xcode version to use on the **Hosted macOS** agent pool, before your `xcodebuild` build task, execute this command line as part of your build, replacing the Xcode version number 13.2 as needed:

  `/bin/bash -c "sudo xcode-select -s /Applications/Xcode_13.2.app/Contents/Developer"`

  Xcode versions on the **Hosted macOS** agent pool can be found [here](https://github.com/actions/runner-images/blob/main/images/macos/).

#### Mono

  To manually select a Mono version to use on the **Hosted macOS** agent pool, execute this script in each job of your build before your Mono build task, specifying the symlink with the required Mono version:

  ```bash
  SYMLINK=<symlink>
  MONOPREFIX=/Library/Frameworks/Mono.framework/Versions/$SYMLINK
  echo "##vso[task.setvariable variable=DYLD_FALLBACK_LIBRARY_PATH;]$MONOPREFIX/lib:/lib:/usr/lib:$DYLD_LIBRARY_FALLBACK_PATH"
  echo "##vso[task.setvariable variable=PKG_CONFIG_PATH;]$MONOPREFIX/lib/pkgconfig:$MONOPREFIX/share/pkgconfig:$PKG_CONFIG_PATH"
  echo "##vso[task.setvariable variable=PATH;]$MONOPREFIX/bin:$PATH"
```

<!-- ENDSECTION -->

::: moniker-end
