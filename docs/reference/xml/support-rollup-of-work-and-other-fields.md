---
title: Support rollup of work and other fields
titleSuffix: Azure DevOps
description: Provides summed values of select fields for all child work items of a parent.
ms.service: azure-devops-boards
ms.custom: process, archive-candidate
ms.assetid: 03d26ae1-cbfa-4156-82e3-1d2fc27f48f3
ms.author: chcomley
author: chcomley
ms.topic: conceptual
monikerRange: '<= azure-devops'
ms.date: 09/16/2024
---

# Rollup of work and other fields

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)]

Rollup provides summed values of selected fields for all child work items of a parent. Since Azure DevOps supports multiple levels of nesting, ensure you don't double-count values during rollup. Project managers typically seek rollup for estimated or completed work, effort, size, or story points.
  
> [!NOTE]    
> The system doesn't support rollup of the Effort, Story Points, or Size fields across product backlogs and portfolio backlogs.

## Native support of rollup within the web portal 

::: moniker range=">= azure-devops-2020"

Azure Boards supports rollup columns on product and portfolio backlogs, rollup within the sprint Planning pane, as well as rollup on sprint backlogs and taskboards. 

### Display rollup progress bars, counts, or totals 

From any product or portfolio backlog, you can add rollup progress bars, counts of descendant work items within a hierarchy, or sum of select fields, such as Story Points or Remaining Work.

[!INCLUDE [temp](../../boards/includes/display-progress-bars.md)]

For more information, see [Display rollup progress or totals](../../boards/backlogs/display-rollup.md).

### View rollup within sprint Planning pane

As you assign backlog items to a sprint using the Planning pane, the sprint window updates with a running tally of the number of backlog items and tasks, as well as the **Planned Effort**. 

> [!div class="mx-imgBorder"]
> ![Product backlog page, drag work items to sprint or assign to sprint through the context menu](../../boards/sprints/media/assign-items-sprint/sprint-window-effort.png)   

*Planned Effort* provides a sum of all *Story Points* or *Effort* defined for backlog items assigned to the sprint. For more information, see [Assign backlog items to a sprint](../../boards/sprints/assign-work-sprint.md).

### View rollup of sprint backlogs and taskboards 

In addition, you can view rollup of Remaining Work from a sprint backlog or taskboard.  

::: moniker-end 

 

From the sprint backlog, the sum of all **Remaining Work** defined for all tasks is displayed for the parent work item. This value also displays on the parent work item card when you view the task board.  

::: moniker range=">= azure-devops-2020"

> [!div class="mx-imgBorder"]  
> ![Sprint backlog displays rollup of Remaining Work](media/rollup/remaining-work-rollup-s155.png )

::: moniker-end

  
From a sprint task board, there are three types of rollup: 
- The rollup of Remaining Work displays on the card for the parent work item
- The sum of all Remaining Work defined for all tasks within a column displays at the top of each column
- The sum of all Remaining Work defined for all tasks for a backlog item displays within each row, grouped by column.      

::: moniker range=">= azure-devops-2020"

> [!div class="mx-imgBorder"]  
> ![Sprint Taskboard displays rollup of Remaining Work](media/rollup/taskboard-remaining-work-s155.png )

::: moniker-end

When you update the status of a task as Completed, the system automatically zeros out the Remaining Work for that task. For more information, see [Task board](../../boards/sprints//task-board.md).

## Other tools that support rollup 

You can obtain rollup of additional data fields in Azure DevOps work tracking data by using one of the following methods:  

::: moniker range="<=azure-devops"

|Method|Azure DevOps Services|On-premises Azure DevOps|  
|------------|----------|----------------------|  
|Work item query charts|![check mark](media/icon_witcheckgreen.png "Icon_WITcheckgreen")|![check mark](media/icon_witcheckgreen.png "Icon_WITcheckgreen")|  
|Microsoft Excel|![check mark](media/icon_witcheckgreen.png "Icon_WITcheckgreen")|![check mark](media/icon_witcheckgreen.png "Icon_WITcheckgreen")|
|Marketplace extensions|![check mark](media/icon_witcheckgreen.png "Icon_WITcheckgreen")|![check mark](media/icon_witcheckgreen.png "Icon_WITcheckgreen")|   
| Analytics |![check mark](media/icon_witcheckgreen.png "Icon_WITcheckgreen")|![check mark](media/icon_witcheckgreen.png "Icon_WITcheckgreen")| 
|SQL Server Reporting Services report|![Not supported](media/icon_witerror.png "Icon_WITerror")|![check mark](media/icon_witcheckgreen.png "Icon_WITcheckgreen")|  

::: moniker-end

<a name="charts"></a>

## Work item query charts and rollup

You can create a flat list query that sums the values of a field you specify. For more information, see [Track progress by creating status and trend query-based charts](../../report/dashboards/charts.md). Charts support a count of work items or a sum of a field. 

For example, here we show a pivot table that sums the story points for user stories by area path and work item state. 
 
![Example rollup of story points by area and state](media/support-rollup-chart.png)

  
## Microsoft Excel and rollup of work tracking data 

You can export a query to Excel that contains the work items you want to provide rollup. You can then write an Excel macro to get the sums and publish data back to TFS.  For more information about Excel integration, see [Bulk add or modify work items with Excel](../../boards/backlogs/office/bulk-add-modify-work-items-excel.md).  
  
For more information about Excel macros, see [Automate tasks with the Macro Recorder](https://support.office.com/article/Automate-tasks-with-the-Macro-Recorder-974ef220-f716-4e01-b015-3ea70e64937b).  

> [!TIP]
> To provide support for opening work items and query results in Excel from the web portal, add the [VSTS Open in Excel](https://marketplace.visualstudio.com/items?itemName=blueprint.vsts-open-work-items-in-excel) Marketplace extension to your organization or collection.

<a name="marketplace"></a>

## Marketplace extensions and custom controls   

There are several extensions available from the [Marketplace](https://marketplace.visualstudio.com/vsts) that provide rollup. Here are a few that may support your needs: 

- [VSTS Rollup](https://marketplace.visualstudio.com/items?itemName=canarysautomationspvtltd.vstsrollup), supports Azure DevOps Services only
- [TFS Aggregator](https://marketplace.visualstudio.com/items?itemName=tfsaggregatorteam.tfs-aggregator-server-plugin), supports Azure DevOps Services and TFS 

Or, you can write an extension using the [REST API for work tracking](/rest/api/azure/devops/wit/work%20items) to get rollup. A code sample available on github that can get you started is [TFS Aggregator](https://tfsaggregator.github.io/).  

::: moniker range="<=azure-devops"

## Analytics service

You can use the [Analytics Service](../../report/powerbi/what-is-analytics.md) to answer quantitative questions about your projects. With this service, you can add [Analytics widgets](../../report/dashboards/analytics-widgets.md) to your dashboard. Or, you can create additional reports using [Power BI](../../report/powerbi/overview.md).  

::: moniker-end  

::: moniker range="< azure-devops"  

## SQL Server Reporting Services report  

 Several OOB reports provide rollup. Here's an example of rollup of completed and remaining work that the Stories Overview report provides. This report is part of the default TFS Agile process template.  
  
 ![Stories Overview example report](media/procguid_agilereports.png "ProcGuid_AgileReports")  
  
 If you have SQL Server Analysis Services deployed, you can get rollup for backlog items from these reports. The refresh frequency for these reports is 2 hours.  
  
-   [Backlog Overview](/previous-versions/azure/devops/report/sql-reports/backlog-overview-scrum)  
-   [Stories Overview](/previous-versions/azure/devops/report/sql-reports/stories-overview-report-agile)   
-   [Requirements Overview](/previous-versions/azure/devops/report/sql-reports/requirements-overview-report-cmmi)  
  
If you need to add reports to your on-premises TFS deployment, see [Add reports to a project](/previous-versions/azure/devops/report/admin/add-reports-to-a-team-project).  

::: moniker-end  

<a name="requirements"></a>  
 
##  Rollup requirements
  
 To support rollup, structure your work items according to the following recommendations:  
  
- Use parent-child links to link work items that contain values that you want to rollup.  
  
- Add required fields to the WITs that will capture the rollup values. Default fields used to schedule work are only present on the task work item. These fields are:  
  - Original Estimate (Microsoft.VSTS.Scheduling.OriginalEstimate): The amount of work required to complete a task. (Agile and CMMI) 
  - Completed Work (Microsoft.VSTS.Scheduling.CompletedWork): The amount of work that has been spent implementing a task. (Agile and CMMI)   
  - Remaining Work (Microsoft.VSTS.Scheduling.RemainingWork): This field is used to support burndown charts.  
  
    If your project was created using the Visual Studio Scrum process template, only Remaining Work is defined in the task.  
  
    For more information about adding fields, see [Modify a field or add a custom field](../add-modify-field.md).  
  
- Determine the unit of time used to track work and make sure it is used consistently across your team or organization. For example, you can track tasks using hours or days.    
- Determine if you want to make rollup values read-only on the work item form. By making them read-only you prevent users from entering inaccurate data. You make fields read-only using the `Control` field `Readonly` attribute.  
  
## Q & A  
  
### Q: Can I get rollup of team capacity?  
 **A:** No. The data entered for team capacity isn't stored in the regular data stores.