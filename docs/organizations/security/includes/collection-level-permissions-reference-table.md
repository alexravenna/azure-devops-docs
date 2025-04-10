---
ms.subservice: azure-devops-security
ms.author: chcomley
author: chcomley
ms.topic: include
ms.date: 10/19/2022
---

<!--- collection-level permissions for cloud (old layout) and on-premises versions ---> 

::: moniker range="< azure-devops"
:::row:::
   :::column span="2":::
   ### Permission (UI)    
   `Namespace permission`  
   :::column-end:::
   :::column span="2":::
  ### Description 
   :::column-end:::
:::row-end:::
---
:::row:::
   :::column span="2":::
  <a id="administer-build-resource-permissions-permission"></a>Administer build resource permissions  
  `BuildAdministration, AdministerBuildResourcePermissions`
   :::column-end:::
   :::column span="2":::
  Can modify permissions for build pipelines at the project collection-level. This includes the following artifacts: 
  - [Set retention policies](../../../pipelines/policies/retention.md)
  - [Set resource limits for pipelines](../../../pipelines/licensing/concurrent-jobs.md) 
  - [Add and manage agent pools](../../../pipelines/agents/pools-queues.md) 
  - [Add and manage deployment pools](../../../pipelines/release/deployment-groups/index.md) 
   :::column-end:::
:::row-end:::
::: moniker-end
::: moniker range="<azure-devops"
:::row:::
   :::column span="2":::
  <a id="administer-process-permissions-permission"></a>Administer process permissions  
  `Process, AdministerProcessPermissions`
   :::column-end:::
   :::column span="2":::
  Can modify permissions for customizing work tracking by creating and customizing [inherited processes](../../settings/work/inheritance-process-model.md). Requires the collection to be configured to support the Inherited process model. See also: 
  - [Customize a project](../../settings/work/customize-process.md) 
  - [Add and manage processes](../../settings/work/manage-process.md) 
   :::column-end:::
:::row-end:::
::: moniker-end
::: moniker range="< azure-devops"
:::row:::
   :::column span="2":::
  <a id="administer-shelved-changes-permission"></a>Administer shelved changes  
  `VersionControlPrivileges, AdminWorkspaces`
   :::column-end:::
   :::column span="2":::
  Can delete [shelvesets created by other users](../../../repos/tfvc/suspend-your-work-manage-your-shelvesets.md). Applies when TFVC is used as the source control. 
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
  <a id="administer-workspaces-permission"></a>Administer workspaces  
  `Workspaces, Administer`
   :::column-end:::
   :::column span="2":::
  Can [create and delete workspaces for other users](../../../repos/tfvc/create-work-workspaces.md). Applies when TFVC is used as the source control.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
  <a id="alter-trace-settings-permission"></a>Alter trace settings  
  `Collection, DIAGNOSTIC_TRACE`
   :::column-end:::
   :::column span="2":::
  Can [change the trace settings](/previous-versions/ms400797%28v%3dvs.80%29) for gathering more detailed diagnostic information about Azure DevOps Web services.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
  <a id="create-a-workspace-permission"></a>Create a workspace  
  `VersionControlPrivileges, CreateWorkspace`
   :::column-end:::
   :::column span="2":::
  Can create a version control workspace. Applies when TFVC is used as the source control. This permission is granted to all users as part of their membership within the Project Collection Valid Users group.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
   <a id="create-new-team-projects-permission"></a>Create new projects  
   (formerly Create new team projects)  
  `Collection, CREATE_PROJECTS`
   :::column-end:::
   :::column span="2":::
  Can [add projects to a project collection](../../projects/create-project.md). Additional permissions may be required depending on your on-premises deployment. 
   :::column-end:::
:::row-end:::
::: moniker-end
::: moniker range="<azure-devops"
:::row:::
   :::column span="2":::
  <a id="create-process-permission"></a>Create process  
  `Process, Create`
   :::column-end:::
   :::column span="2":::
  Can [create an inherited process](../../settings/work/manage-process.md) used to customize work tracking and Azure Boards. Requires the collection to be configured to support the Inherited process model.  
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
   <a id="delete-field-permission"></a>Delete field from organization  
   (formerly Delete field from account)  
  `Collection, DELETE_FIELD`
   :::column-end:::
   :::column span="2":::
  Can [delete a custom field that was added to a process](../../settings/work/customize-process-field.md). For on-premises deployments, requires the collection to be configured to support Inherited process model.  
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
   <a id="delete-process-permission /"> 
   Delete process  
  `Process, Delete`
   :::column-end:::
   :::column span="2":::
  Can [delete an inherited process](../../settings/work/manage-process.md) used to customize work tracking and Azure Boards. Requires the collection to be configured to support Inherited process model. 
   :::column-end:::
:::row-end:::
::: moniker-end
::: moniker range="< azure-devops"
:::row:::
   :::column span="2":::
  <a id="delete-team-project-permission"></a> Delete team project   
  `Project, DELETE`
   :::column-end:::
   :::column span="2":::
  Can [delete a project](../../projects/delete-project.md).
  > [!NOTE]  
  > Deleting a project deletes all data that is associated with the project. You cannot undo the deletion of a project except 
  by restoring the collection to a point before the project was deleted.  
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
   <a id="edit-collection-level-information-permission">  
   Edit collection-level information  
   `Collection, GENERIC_WRITE`
   :::column-end:::
   :::column span="2":::
   Can set organization and project-level settings.

   > [!NOTE]   
   > **Edit collection-level information** includes the ability to perform these tasks for all projects defined in an organization or collection:  
   > - Modify **Extensions**, and **Analytics**  settings
   > - Modify version control permissions and repository settings
   > - Edit [event subscriptions](#alerts) or alerts for global notifications, project-level, and team-level events 
   > - Edit all project and team-level settings for projects defined in the collections.
   
   :::column-end:::
:::row-end:::
::: moniker-end
::: moniker range="<azure-devops"
:::row:::
   :::column span="2":::
  <a id="edit-process-permission"></a>Edit process  
  `Process, Edit`
   :::column-end:::
   :::column span="2":::
  Can edit a [custom inherited process](../../settings/work/customize-process.md). Requires the collection to be configured to support the Inherited process model. 
   :::column-end:::
:::row-end:::
::: moniker-end
::: moniker range="< azure-devops"
:::row:::
   :::column span="2":::
  <a id="make-requests-on-behalf-of-others-permission"></a>Make requests on behalf of others  
  `Server, Impersonate`    
   :::column-end:::
   :::column span="2":::
  Can perform operations on behalf of other users or services. 
  Assign this permission only to on-premises [service accounts](/azure/devops/server/admin/service-accounts-dependencies). 
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
  <a id="manage-build-resources-permission"></a>Manage build resources  
  `BuildAdministration, ManageBuildResources`
   :::column-end:::
   :::column span="2":::
  Can manage build computers, build agents, and build controllers. 
   :::column-end:::
:::row-end:::
::: moniker-end
::: moniker range=">= azure-devops-2020 < azure-devops"
:::row:::
   :::column span="2":::
   <a id="manage-enterprise-policies-permission"></a> Manage enterprise policies  
  `Collection, MANAGE_ENTERPRISE_POLICIES`
   :::column-end:::
   :::column span="2":::
   Can enable and disable application connection policies as described in [Change application connection policies](../../accounts/change-application-access-policies.md). 
   > [!NOTE]
   > This permission is only valid for Azure DevOps Services. While it may appear for Azure DevOps Server on-premises, it doesn't apply to on-premises servers. 
   :::column-end:::
:::row-end:::
::: moniker-end
::: moniker range="< azure-devops"
:::row:::
   :::column span="2":::
  <a id="manage-process-template-permission"></a>Manage process template  
  `Collection, MANAGE_TEMPLATE`
   :::column-end:::
   :::column span="2":::
  Can [download, create, edit, and upload process templates](../../../boards/work-items/guidance/manage-process-templates.md). A process template defines the building blocks of the work item tracking system as well as other subsystems you access through Azure Boards. Requires the collection to be configured to support ON=premises XML process model.  
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
  <a id="manage-test-controllers-permission"></a>Manage test controllers  
  `Collection, MANAGE_TEST_CONTROLLERS`
   :::column-end:::
   :::column span="2":::
  Can register and de-register test controllers. 
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
  <a id="trigger-events-permission"></a>Trigger events  
  `Collection, TRIGGER_EVENT`
  `Server, TRIGGER_EVENT`
   :::column-end:::
   :::column span="2":::
  Can trigger project alert events within the collection. Assign only to service accounts. Users with this permission can't remove built-in collection level groups such as Project Collection Administrators. 
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
  <a id="use-build-resources-permission"></a>Use build resources  
  `BuildAdministration, UseBuildResources`
   :::column-end:::
   :::column span="2":::
  Can reserve and allocate build agents. Assign only to service accounts for build services.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
  <a id="view-build-resources-permission"></a>View build resources  
  `BuildAdministration, ViewBuildResources`
   :::column-end:::
   :::column span="2":::
  Can view, but not use, build controllers and build agents that are configured for an organization or project collection.  
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
  <a id="view-collection-level-information-permission"></a>View instance-level information    
  or View collection-level information  
  `Collection, GENERIC_READ`
   :::column-end:::
   :::column span="2":::
   Can view collection-level permissions for a user or group. 
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="2":::
  <a id="view-system-synchronization-information-permission"></a>View system synchronization information  
  `Collection, SYNCHRONIZE_READ`  
   :::column-end:::
   :::column span="2":::
  Can call the synchronization application programming interfaces. Assign only to service accounts. 
   :::column-end:::
:::row-end:::
::: moniker-end 