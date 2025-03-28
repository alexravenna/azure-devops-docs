---
title: Deploy to Azure SQL Database
description: Deploy to an Azure SQL database from Azure Pipelines
ms.assetid: B4255EC0-1A25-48FB-B57D-EC7FDB7124D9
ms.topic: conceptual
ms.date: 03/19/2025
monikerRange: '<= azure-devops'
---

# Azure SQL database deployment

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)]

You can automatically deploy your database updates to Azure SQL database after every successful build.

## DACPAC

The simplest way to deploy a database is to create [data-tier package or DACPAC](/sql/relational-databases/data-tier-applications/data-tier-applications). DACPACs can be used to package and deploy schema changes and data. You can create a DACPAC using the **SQL database project** in Visual Studio.

#### [YAML](#tab/yaml/)
::: moniker range="<=azure-devops"

To deploy a DACPAC to an Azure SQL database, add the following snippet to your azure-pipelines.yml file.

```yaml
- task: SqlAzureDacpacDeployment@1
  displayName: Execute Azure SQL : DacpacTask
  inputs:
    azureSubscription: '<Azure service connection>'
    ServerName: '<Database server name>'
    DatabaseName: '<Database name>'
    SqlUsername: '<SQL user name>'
    SqlPassword: '<SQL user password>'
    DacpacFile: '<Location of Dacpac file in $(Build.SourcesDirectory) after compilation>'
```

::: moniker-end

#### [Classic](#tab/classic/)
When setting up a build pipeline for your Visual Studio database project, use the **.NET desktop** template. This template automatically adds the tasks to build the project and publish artifacts, including the DACPAC.

When setting up a release pipeline, choose **Start with an empty pipeline**, link the artifacts from build, and then add an [Azure SQL Database Deployment](/azure/devops/pipelines/tasks/reference/sql-azure-dacpac-deployment-v1) task.

* * *
See also [authentication information when using the Azure SQL Database Deployment task](/azure/devops/pipelines/tasks/reference/sql-azure-dacpac-deployment-v1).

## SQL scripts

Instead of using a DACPAC, you can also use SQL scripts to deploy your database. Here’s a simple example of a SQL script that creates an empty database.

```sql
  USE [main]
  GO
  IF NOT EXISTS (SELECT name FROM main.sys.databases WHERE name = N'DatabaseExample')
  CREATE DATABASE [DatabaseExample]
  GO
```

To run SQL scripts as part of a pipeline, you’ll need Azure PowerShell scripts to create and remove firewall rules in Azure. Without the firewall rules, the Azure Pipelines agent can’t communicate with Azure SQL Database.

The following PowerShell script creates firewall rules. You can check in this script as `SetAzureFirewallRule.ps1` into your repository.

#### [ARM](#tab/arm/)

```powershell
[CmdletBinding(DefaultParameterSetName = 'None')]
param
(
  [String] [Parameter(Mandatory = $true)] $ServerName,
  [String] [Parameter(Mandatory = $true)] $ResourceGroupName,
  [String] $FirewallRuleName = "AzureWebAppFirewall"
)
$agentIP = (New-Object net.webclient).downloadstring("https://api.ipify.org")
New-AzSqlServerFirewallRule -ResourceGroupName $ResourceGroupName -ServerName $ServerName -FirewallRuleName $FirewallRuleName -StartIPAddress $agentIP -EndIPAddress $agentIP
```

#### [ASM (Classic)](#tab/asm/)

```powershell
[CmdletBinding(DefaultParameterSetName = 'None')]
param
(
  [String] [Parameter(Mandatory = $true)] $ServerName,
  [String] [Parameter(Mandatory = $true)] $ResourceGroupName,
  [String] $FirewallRuleName = "AzureWebAppFirewall"
)

$ErrorActionPreference = 'Stop'

function New-AzureSQLServerFirewallRule {
  $agentIP = (New-Object net.webclient).downloadstring("https://api.ipify.org")
  New-AzureSqlDatabaseServerFirewallRule -StartIPAddress $agentIP -EndIPAddress $agentIP -RuleName $FirewallRuleName -ServerName $ServerName
}

function Update-AzureSQLServerFirewallRule{
  $agentIP= (New-Object net.webclient).downloadstring("https://api.ipify.org")
  Set-AzureSqlDatabaseServerFirewallRule -StartIPAddress $agentIP -EndIPAddress $agentIP -RuleName $FirewallRuleName -ServerName $ServerName
}

if ((Get-AzureSqlDatabaseServerFirewallRule -ServerName $ServerName -RuleName $FirewallRuleName -ErrorAction SilentlyContinue) -eq $null)
{
  New-AzureSQLServerFirewallRule
}
else
{
  Update-AzureSQLServerFirewallRule
}
```
* * *

The following PowerShell script removes firewall rules. You can check in this script as `RemoveAzureFirewallRule.ps1` into your repository.

#### [ARM](#tab/arm/)

```powershell
[CmdletBinding(DefaultParameterSetName = 'None')]
param
(
  [String] [Parameter(Mandatory = $true)] $ServerName,
  [String] [Parameter(Mandatory = $true)] $ResourceGroupName,
  [String] $FirewallRuleName = "AzureWebAppFirewall"
)
Remove-AzSqlServerFirewallRule -ServerName $ServerName -FirewallRuleName $FirewallRuleName -ResourceGroupName $ResourceGroupName
```

#### [ASM (Classic)](#tab/asm/)

```powershell
[CmdletBinding(DefaultParameterSetName = 'None')]
param
(
  [String] [Parameter(Mandatory = $true)] $ServerName,
  [String] [Parameter(Mandatory = $true)] $ResourceGroupName,
  [String] $FirewallRuleName = "AzureWebAppFirewall"
)

$ErrorActionPreference = 'Stop'

if ((Get-AzureSqlDatabaseServerFirewallRule -ServerName $ServerName -RuleName $FirewallRuleName -ErrorAction SilentlyContinue))
{
  Remove-AzureSqlDatabaseServerFirewallRule -RuleName $FirewallRuleName -ServerName $ServerName
}
```
* * *

#### [YAML](#tab/yaml/)

::: moniker range="<=azure-devops"

Add the following to your azure-pipelines.yml file to run a SQL script.

```yaml
variables:
  AzureSubscription: '<SERVICE_CONNECTION_NAME>'
  ResourceGroupName: '<RESOURCE_GROUP_NAME>'
  ServerName: '<DATABASE_SERVER_NAME>'
  ServerFqdn: '<DATABASE_FQDN>'
  DatabaseName: '<DATABASE_NAME>'
  AdminUser: '<DATABASE_USERNAME>'
  AdminPassword: '<DATABASE_PASSWORD>'
  SQLFile: '<LOCATION_OF_SQL_FILE_IN_$(Build.SourcesDirectory)>'

steps:
- task: AzurePowerShell@5
  displayName: 'Azure PowerShell script'
  inputs:
    azureSubscription: '$(AzureSubscription)'
    ScriptType: filePath
    ScriptPath: '$(Build.SourcesDirectory)\scripts\SetAzureFirewallRule.ps1'
    ScriptArguments: '-ServerName $(ServerName) -ResourceGroupName $(ResourceGroupName)'
    azurePowerShellVersion: LatestVersion

- task: PowerShell@2
  inputs:
    targetType: 'inline'
    script: |
      if (-not (Get-Module -ListAvailable -Name SqlServer)) {
          Install-Module -Name SqlServer -Force -AllowClobber
      }
  displayName: 'Install SqlServer module if not present'

- task: PowerShell@2
  inputs:
    targetType: 'inline'
    script: |
      Invoke-Sqlcmd -InputFile $(SQLFile) -ServerInstance $(ServerFqdn) -Database $(DatabaseName) -Username $(AdminUser) -Password $(AdminPassword)
  displayName: 'Run SQL script'

- task: AzurePowerShell@5
  displayName: 'Azure PowerShell script'
  inputs:
    azureSubscription: '$(AzureSubscription)'
    ScriptType: filePath
    ScriptPath: '$(Build.SourcesDirectory)\scripts\RemoveAzureFirewallRule.ps1'
    ScriptArguments: '-ServerName $(ServerName) -ResourceGroupName $(ResourceGroupName)'
    azurePowerShellVersion: LatestVersion
```

::: moniker-end

#### [Classic](#tab/classic/)

When you set up a build pipeline, make sure that the SQL script to deploy the database and the Azure PowerShell scripts to configure firewall rules are part of the build artifact.

When you set up a release pipeline, choose **Start with an Empty process**, link the artifacts from build, and then use the following tasks:

1. Use the [Azure PowerShell](/azure/devops/pipelines/tasks/reference/azure-powershell-v5) task to add a firewall rule in Azure to allow the Azure Pipelines agent to connect to Azure SQL Database. The script requires one argument - the name of the SQL server you created.

1. Use the [PowerShell](/azure/devops/pipelines/tasks/reference/powershell-v2) task to invoke SQLCMD and execute your scripts. Add the following inline script to your task:

    ```PowerShell
    if (-not (Get-Module -ListAvailable -Name SqlServer)) {
      Install-Module -Name SqlServer -Force -AllowClobber
    }

    Invoke-Sqlcmd -InputFile $(SQLFile) -ServerInstance $(ServerFqdn) -Database $(DatabaseName) -Username $(AdminUser) -Password $(AdminPassword)
    ```

1. Use another [Azure PowerShell](/azure/devops/pipelines/tasks/reference/azure-powershell-v5) task to remove the firewall rule in Azure.

    :::image type="content" source="media/sql-add-firewall-rules.png" alt-text="A screenshot displaying a classic pipeline to add firewall rules and run SQL scripts.":::

* * *

## Azure service connection

The **Azure SQL Database Deployment** task is the primary mechanism to deploy a database to Azure. This task, as with other built-in Azure tasks, requires an Azure service connection as an input. The Azure service connection stores the credentials to connect from Azure Pipelines to Azure.

::: moniker range="azure-devops"

The easiest way to get started with this task is to be signed in as a user that owns both the Azure DevOps organization and the Azure subscription.
In this case, you won't have to manually create the service connection.
Otherwise, to learn how to create an Azure service connection, see [Create an Azure service connection](../library/connect-to-azure.md).

::: moniker-end

::: moniker range="< azure-devops"

To learn how to create an Azure service connection, see [Create an Azure service connection](../library/connect-to-azure.md).

::: moniker-end

## Deploying conditionally

You may choose to deploy only certain builds to your Azure database.

#### [YAML](#tab/yaml/)
::: moniker range="<=azure-devops"

To do this in YAML, you can use one of these techniques:

* Isolate the deployment steps into a separate job, and add a condition to that job.
* Add a condition to the step.

The following example shows how to use step conditions to deploy only those builds that originate from main branch.

```yaml
- task: SqlAzureDacpacDeployment@1
  condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/main'))
  inputs:
    azureSubscription: '<Azure service connection>'
    ServerName: '<Database server name>'
    DatabaseName: '<Database name>'
    SqlUsername: '<SQL user name>'
    SqlPassword: '<SQL user password>'
    DacpacFile: '<Location of Dacpac file in $(Build.SourcesDirectory) after compilation>'
```

To learn more about conditions, see [Specify conditions](../process/conditions.md).

::: moniker-end

#### [Classic](#tab/classic/)

In your release pipeline, you can implement various checks and conditions to control the deployment.

> [!NOTE]
> In some setups, you might need to allowlist the range of IP addresses for the specific region that is updated in the [weekly JSON file](https://www.microsoft.com/download/details.aspx?id=56519). Learn about [networking Microsoft-hosted agents](../agents/hosted.md#networking).

* Set **branch filters** to configure the **continuous deployment trigger** on the artifact of the release pipeline.
* Set **pre-deployment approvals** as a pre-condition for deployment to a stage.
* Configure **gates** as a pre-condition for deployment to a stage.
* Specify conditions for a task to run.

For more information, see [Release, branch, and stage triggers](../release/triggers.md), [Release deployment control using approvals](../release/approvals/approvals.md), [Release deployment control using gates](../release/approvals/gates.md), and [Specify conditions for running a task](../process/conditions.md).

* * *
## More SQL actions

**SQL Azure Dacpac Deployment** may not support all SQL server actions
that you want to perform. In these cases, you can simply use PowerShell or command-line scripts to run the commands you need.
This section shows some of the common use cases for invoking the [SqlPackage.exe tool](/sql/tools/sqlpackage-download).
As a prerequisite to running this tool, you must use a self-hosted agent and have the tool installed on your agent.

> [!NOTE]
> If you execute **SQLPackage** from the folder where it is installed, you must prefix the path with `&` and wrap it in double-quotes.

### Basic Syntax 

`<Path of SQLPackage.exe> <Arguments to SQLPackage.exe>`

You can use any of the following SQL scripts depending on the action that you want to perform

### Extract

Creates a database snapshot (.dacpac) file from a live SQL server or Microsoft Azure SQL Database.

**Command Syntax:**

```command
SqlPackage.exe /TargetFile:"<Target location of dacpac file>" /Action:Extract
/SourceServerName:"<ServerName>.database.windows.net"
/SourceDatabaseName:"<DatabaseName>" /SourceUser:"<Username>" /SourcePassword:"<Password>"
```

or

```command
SqlPackage.exe /action:Extract /tf:"<Target location of dacpac file>"
/SourceConnectionString:"Data Source=ServerName;Initial Catalog=DatabaseName;Integrated Security=SSPI;Persist Security Info=False;"
```

**Example:**

```command
SqlPackage.exe /TargetFile:"C:\temp\test.dacpac" /Action:Extract /SourceServerName:"DemoSqlServer.database.windows.net.placeholder"
 /SourceDatabaseName:"Testdb" /SourceUser:"ajay" /SourcePassword:"SQLPassword"
```

**Help:**

```command
sqlpackage.exe /Action:Extract /?
```

### Publish

Incrementally updates a database schema to match the schema of a source .dacpac file. If the database doesn’t exist on the server, the publish operation will create it. Otherwise, an existing database will be updated.

**Command Syntax:**

```command
SqlPackage.exe /SourceFile:"<Dacpac file location>" /Action:Publish /TargetServerName:"<ServerName>.database.windows.net"
/TargetDatabaseName:"<DatabaseName>" /TargetUser:"<Username>" /TargetPassword:"<Password> "
```

**Example:**

```command
SqlPackage.exe /SourceFile:"E:\dacpac\ajyadb.dacpac" /Action:Publish /TargetServerName:"DemoSqlServer.database.windows.net.placeholder"
/TargetDatabaseName:"Testdb4" /TargetUser:"ajay" /TargetPassword:"SQLPassword"
```

**Help:**

```command
sqlpackage.exe /Action:Publish /?
```

### Export

Exports a live database, including database schema and user data, from SQL Server or Microsoft Azure SQL Database to a BACPAC package (.bacpac file).

**Command Syntax:**

```command
SqlPackage.exe /TargetFile:"<Target location for bacpac file>" /Action:Export /SourceServerName:"<ServerName>.database.windows.net"
/SourceDatabaseName:"<DatabaseName>" /SourceUser:"<Username>" /SourcePassword:"<Password>"
```

**Example:**

```command
SqlPackage.exe /TargetFile:"C:\temp\test.bacpac" /Action:Export /SourceServerName:"DemoSqlServer.database.windows.net.placeholder"
/SourceDatabaseName:"Testdb" /SourceUser:"ajay" /SourcePassword:"SQLPassword"
```

**Help:**

```command
sqlpackage.exe /Action:Export /?
```

### Import

Imports the schema and table data from a BACPAC package into a new user database in an instance of SQL Server or Microsoft Azure SQL Database.

**Command Syntax:** 

```command
SqlPackage.exe /SourceFile:"<Bacpac file location>" /Action:Import /TargetServerName:"<ServerName>.database.windows.net"
/TargetDatabaseName:"<DatabaseName>" /TargetUser:"<Username>" /TargetPassword:"<Password>"
```

**Example:**

```command
SqlPackage.exe /SourceFile:"C:\temp\test.bacpac" /Action:Import /TargetServerName:"DemoSqlServer.database.windows.net.placeholder"
/TargetDatabaseName:"Testdb" /TargetUser:"ajay" /TargetPassword:"SQLPassword"
```

**Help:**

```command
sqlpackage.exe /Action:Import /?
```

### DeployReport

Creates an XML report of the changes that would be made by a publish action.

**Command Syntax:** 

```command
SqlPackage.exe /SourceFile:"<Dacpac file location>" /Action:DeployReport /TargetServerName:"<ServerName>.database.windows.net"
/TargetDatabaseName:"<DatabaseName>" /TargetUser:"<Username>" /TargetPassword:"<Password>" /OutputPath:"<Output XML file path for deploy report>"
```

**Example:**

```command
SqlPackage.exe /SourceFile:"E: \dacpac\ajyadb.dacpac" /Action:DeployReport /TargetServerName:"DemoSqlServer.database.windows.net.placeholder"
/TargetDatabaseName:"Testdb" /TargetUser:"ajay" /TargetPassword:"SQLPassword" /OutputPath:"C:\temp\deployReport.xml" 
```

**Help:**

```command
sqlpackage.exe /Action:DeployReport /?
```

### DriftReport

Creates an XML report of the changes that have been made to a registered database since it was last registered.

**Command Syntax:** 

```command
SqlPackage.exe /Action:DriftReport /TargetServerName:"<ServerName>.database.windows.net" /TargetDatabaseName:"<DatabaseName>"
/TargetUser:"<Username>" /TargetPassword:"<Password>" /OutputPath:"<Output XML file path for drift report>"
```

**Example:**

```command
SqlPackage.exe /Action:DriftReport /TargetServerName:"DemoSqlServer.database.windows.net.placeholder" /TargetDatabaseName:"Testdb"
/TargetUser:"ajay" /TargetPassword:"SQLPassword" /OutputPath:"C:\temp\driftReport.xml"
```

**Help:**

```command
sqlpackage.exe /Action:DriftReport /?
```

### Script

Creates a Transact-SQL incremental update script that updates the schema of a target to match the schema of a source.

**Command Syntax:**

```command
SqlPackage.exe /SourceFile:"<Dacpac file location>" /Action:Script /TargetServerName:"<ServerName>.database.windows.net"
/TargetDatabaseName:"<DatabaseName>" /TargetUser:"<Username>" /TargetPassword:"<Password>" /OutputPath:"<Output SQL script file path>"
```

**Example:**

```command
SqlPackage.exe /Action:Script /SourceFile:"E:\dacpac\ajyadb.dacpac" /TargetServerName:"DemoSqlServer.database.windows.net.placeholder"
/TargetDatabaseName:"Testdb" /TargetUser:"ajay" /TargetPassword:"SQLPassword" /OutputPath:"C:\temp\test.sql"
/Variables:StagingDatabase="Staging DB Variable value"
```

**Help:**

```command
sqlpackage.exe /Action:Script /?
```
