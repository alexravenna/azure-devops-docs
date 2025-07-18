---
title: Customize work item type for inherited process
titleSuffix: Azure DevOps Services
description: Customize a process by adding or modifying a work item type for a project 
ms.custom: inherited-process
ms.service: azure-devops-boards
ms.assetid: DBF41880-62A4-43A9-9A31-8DB701EB888E
ms.author: chcomley
author: chcomley
monikerRange: "<=azure-devops"
ms.topic: how-to
ms.date: 04/22/2019
---

# Add and manage work item types      

[!INCLUDE [version-gt-eq-2019](../../../includes/version-gt-eq-2019.md)]

You can add custom work item types (WITs) or modify existing WITs to add fields, remove or hide fields, add custom rules, and more. For example, you may want to capture customer issues in a custom Ticket WIT.   

> [!div class="mx-imgBorder"]  
> ![Custom Ticket work item form](media/process/custom-wit-new-ticket-form.png) 

[!INCLUDE [temp](../includes/note-on-prem-link.md)]

## Prerequisites

[!INCLUDE [temp](../includes/process-prerequisites.md)] 

[!INCLUDE [temp](../includes/open-process-admin-context-ts.md)]
 
[!INCLUDE [temp](../includes/automatic-update-project.md)] 

<a id="add-wit">  </a>

## Add a work item type

1. From the <strong>Work Item Types</strong> page, choose :::image type="icon" source="../../../media/icons/blue-add-icon.png" border="false"::: <strong>New work item type</strong>.

	![Process, Inherited process, Work Item Types, Add new work item type](media/process/cpwit-add-new-wit.png)

2. Name the WIT and optionally specify a description, icon and color. The icon and color you specify appear throughout the web portal, including on the work item form and when associated work items appear on a backlog, boards, query results, and more. Choose <strong>Create</strong> to save. 

	<img src="media/process/cwit-create-wit-ticket.png" alt="Create new work item type dialog" /> 

3. From the Layout page, you can add fields, groups, or pages to specify the form and fields you want to track. Each new WIT comes predefined with a Details page with the Description field, and Discussion, Development, and Related Work groups. For details, see [Add and manage fields](customize-process-field.md) or [Customize the web layout for a process](customize-process-form.md).    

   > [!div class="mx-imgBorder"]  
   > ![New WIT, customize layout](media/process/cpwit-new-ticket-define.png)    

   Also added, but not shown nor editable from the **Layout** page, are the standard elements included with the header of the form as shown in the following image, as well as the history, links, and attachment pages.

   ![WIT header details](media/process/weblayout-system-controls-details-page.png) 

4. Open the States page to view the default workflow states. Optionally, [customize the workflow states](customize-process-workflow.md).  
   <a id="backlog">  </a> 

5. Optional. To add the WIT to a backlog, see [Customize your backlogs or boards for a process](customize-process-backlogs-boards.md). By default, custom WITs aren't added to any backlog. To learn more about different backlog levels, see [Backlogs, boards, and plans](../../../boards/backlogs/backlogs-boards-plans.md).   

6. Verify the custom work item type appears as expected. Open the **Work>Work Items** page (user context) and choose **New Work Item** and select the WIT you customized. Here we choose **Ticket**. 

	> [!div class="mx-imgBorder"]  
	> ![Work>Work Items page, add new work item, Ticket](media/process/add-custom-wit-verify-ticket.png) 

	If you don't see the custom WIT, refresh your browser to make sure it registers all the custom changes you've made. 

7. Verify that the field you added appears on the form. Note that the :::image type="icon" source="../../../media/icons/required-icon.png" border="false"::: (exclamation mark) icon indicates the field is required.  

   > [!div class="mx-imgBorder"]  
   > ![Ticket form, Customer Ticket field added to Customer Focus group](media/process/add-custom-field-verify-ticket-form.png) 

<a id="overview">  </a>

## Change description, icon or color

To change the description, icon or color of a custom WIT, choose Edit from the WIT context menu. 

Here we change the description, icon and color for the Ticket custom WIT.  

<img src="media/process/cpwit-edit-color-description.png" alt="Overview page, edit custom ticket description, icon and color" /> 

<a id="enable-disable"></a>

## Enable or disable a WIT  

You can disable a custom WIT, which prevents users from being able to add work items using it. However, all existing work items defined using the custom WIT remain available. You can query for them and edit them.

You may want to disable a custom WIT until you have defined all the fields, workflow, and layout that you have planned.

To disable a custom WIT, choose **Disable** from the WIT context menu. 

To re-enable the WIT, choose **Enable** from the WIT context menu. 

> [!NOTE]    
> Disabling a WIT removes the WIT from the **New** drop down and add experiences. Creating a work item of that WIT is also blocked via REST APIs.  
>
> No changes are made to existing work items of that type. You can update or delete them and they continue to appear on backlogs and boards. Both work item types need to be enabled in order to do a change type operation.

<a id="destroy">  </a>

## Delete or destroy a custom WIT 

> [!IMPORTANT]  
> Destroying a WIT deletes all work items and data associated with that WIT, including historical values. Once destroyed, you can't recover the data.

1. To completely remove a custom WIT and all work items based on that WIT, choose **Destroy** from the WIT context menu.

	To destroy a WIT, be a member of the Project Collection Administrators group or be [granted explicit permissions to edit a specific process](../../../organizations/security/set-permissions-access-work-tracking.md#process-permissions). 

2. To complete the delete operation, you must type the name of the WIT as shown. 

	<img src="media/process/cpit-destroy-wit-confirm.png" alt="Delete field, confirmation dialog" />  
 
## WIT extensibility

To work with WITs programmatically, see [Work Item Types REST API](/rest/api/azure/devops/wit/work%20item%20types). 

## Q & A

[!INCLUDE [temp](includes/qa-custom-work-item-on-backlog.md)] 

## Related content  

[!INCLUDE [temp](../includes/note-audit-log-support-process.md)]

- [Add and manage fields](customize-process-field.md)  
- [Customize the layout](customize-process-form.md)
- [Customize a workflow for a work item type](customize-process-workflow.md)
- [Customize a project using an inherited process](customize-process.md) 

 
