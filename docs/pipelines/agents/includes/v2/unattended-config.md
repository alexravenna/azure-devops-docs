---
ms.topic: include
ms.service: azure-devops-pipelines
ms.manager: mijacobs
ms.author: sdanie
author: steved0x
ms.date: 04/17/2024
---

To configure an agent, it must know the URL to your organization or collection and credentials of someone authorized to set up agents.
All other responses are optional.
Any command-line parameter can be specified using an environment variable instead:
put its name in upper case and prepend `VSTS_AGENT_INPUT_`.
For example, `VSTS_AGENT_INPUT_PASSWORD` instead of specifying `--password`.

### Required options

- `--unattended` - agent setup will not prompt for information, and all settings must be provided on the command line
- `--url <url>` - URL of the server. For example: https://dev.azure.com/myorganization or http://my-azure-devops-server:8080/tfs
- `--auth <type>` - authentication type. Valid values are:
  - `pat` (Personal access token) - PAT is the only scheme that works with Azure DevOps Services.
  - `negotiate` (Kerberos or NTLM)
  - `alt` (Basic authentication)
  - `integrated` (Windows default credentials)

### Authentication options

- If you chose `--auth pat`:
  - `--token <token>` - specifies your personal access token
  -  PAT is the only scheme that works with Azure DevOps Services.
- If you chose `--auth negotiate` or `--auth alt`:
  - `--userName <userName>` - specifies a Windows username in the format `domain\userName` or `userName@domain.com`
  - `--password <password>` - specifies a password

### Pool and agent names
- `--pool <pool>` - pool name for the agent to join
- `--agent <agent>` - agent name
- `--replace` - Specify `--replace` if you are replacing the current agent installation with an agent with the same name. If your intention is to replace an agent with the same name that's hosted elsewhere, unconfigure the other agent first before configuring this one (and you don't need to specify `--replace`); otherwise if you have two agent instances with the same name, you'll get conflicts, and after a few moments of conflicts, one of the agents will shut down.

### Agent setup
- `--work <workDirectory>` - work directory where job data is stored. Defaults to `_work` under the
root of the agent directory. The work directory is owned by a given
agent and should not be shared between multiple agents.
- `--acceptTeeEula` - accept the Team Explorer Everywhere End User License Agreement (macOS and Linux only)
- `--disableloguploads` - don't stream or send console log output to the server. Instead, you may retrieve them from the agent host's filesystem after the job completes.

### Windows-only startup
- `--runAsService` - configure the agent to run as a Windows service (requires administrator permission)
- `--runAsAutoLogon` - configure auto-logon and run the agent on startup (requires administrator permission)
- `--windowsLogonAccount <account>` - used with `--runAsService` or `--runAsAutoLogon` to specify the Windows user
name in the format `domain\userName` or `userName@domain.com`
- `--windowsLogonPassword <password>` - used with `--runAsService` or `--runAsAutoLogon` to specify Windows logon password (not required for [Group Managed Service Accounts](https://aka.ms/gmsa) and Windows built in accounts such as 'NT AUTHORITY\NETWORK SERVICE')
- `--enableservicesidtypeunrestricted` - used with `--runAsService` to configure the agent with service SID type as `SERVICE_SID_TYPE_UNRESTRICTED` (requires administrator permission)
- `--overwriteAutoLogon` - used with `--runAsAutoLogon` to overwrite the existing auto logon on the machine
- `--noRestart` - used with `--runAsAutoLogon` to stop the host from restarting after agent configuration completes

[!INCLUDE [troubleshooting-autologon](./troubleshooting-autologon.md)]

### Deployment group only
- `--deploymentGroup` - configure the agent as a deployment group agent
- `--deploymentGroupName <name>` - used with `--deploymentGroup` to specify the deployment group for the agent to join
- `--projectName <name>` - used with `--deploymentGroup` to set the project name
- `--addDeploymentGroupTags` - used with `--deploymentGroup` to indicate that deployment group tags should be added
- `--deploymentGroupTags <tags>` - used with `--addDeploymentGroupTags` to specify the comma separated list of tags for
the deployment group agent - for example "web, db"

### Environments only
- `--addvirtualmachineresourcetags` - used to indicate that environment resource tags should be added
- `--virtualmachineresourcetags  <tags>` - used with `--addvirtualmachineresourcetags` to specify the comma separated list of tags for
the environment resource agent - for example "web, db"
