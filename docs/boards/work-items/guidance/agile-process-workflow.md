---
title: Agile workflow in Azure Boards
titleSuffix: Azure Boards
description: Learn how to use the Agile process to track work using its work item types working in Azure Boards.
ms.custom: work-items, engagement-fy23
ms.service: azure-devops-boards
ms.assetid: d16d04fd-c073-45c0-b1b9-3724f0a7519b  
ms.topic: conceptual
ms.author: chcomley
author: chcomley
monikerRange: '<= azure-devops'
ms.date: 06/01/2023
---

# Agile workflow in Azure Boards  

[!INCLUDE [version-lt-eq-azure-devops](../../../includes/version-lt-eq-azure-devops.md)]

When you use the Agile process in Azure Boards, the following work item types (WITs) help your team to plan and track progress of your projects: epics, features, user stories, tasks, issues/bugs. Once you define your WITs, you can use the board to track progress by updating the status of those items.

:::image type="content" source="../../../organizations/settings/work/media/scrum-to-agile/agile-process-plan-wits.png" alt-text="Conceptual image of Agile process, work item types used to plan and track work.":::

To gain insight into a portfolio of features, scenarios, or user experiences, product owners and program managers map **user stories** to **features**. When a team works in sprints, they define **tasks** that automatically link to user stories. If you're new to the Agile process, review the section [Plan and track work with Agile](agile-process.md#start-using) to get started. 

From the web portal or Microsoft Test Manager, testers can create and run test cases against **bugs and issues**, which are used to track code defects and blocking issues.  

## Define user stories

Product owners typically define and stack rank user stories, which describe the work involved for developing applications, requirements, and elements. The team then estimates the effort and work to deliver the highest priority items.

Create user stories from the quick add panel on the [product backlog page](../../backlogs/create-your-backlog.md). From that page, you can also drag-and-drop items to reorder them or [map them to features](../../backlogs/organize-backlog.md). 
 
:::image type="content" source="../media/about-work-items/work-item-form-user-story.png" alt-text="Screenshot of User Story work item form.":::

You can open each user story to provide more details and estimate the story points. Define **Story Points** so your team can use the forecast feature and velocity charts to estimate future sprints or work efforts. By prioritizing the user stories on the backlog page (that's captured in the Stack Rank field), product owners can indicate which items should be given higher priority.

Use the guidance in the following table and the [common fields used across work item types](#definitions-for-common-work-tracking-fields) when you complete the form.  

:::row:::
   :::column span="1":::
   **Field/tab**
   :::column-end:::
   :::column span="3":::
   **Usage**
   :::column-end:::
:::row-end:::
---
:::row:::
   :::column span="1":::
   [Description](../../queries/titles-ids-descriptions.md)  
   :::column-end:::
   :::column span="3":::
   For user stories, provide enough detail for estimating how much work is required to implement the story. Focus on who the feature is for, what users want to accomplish, and why. Don't describe how the feature should be developed. Do provide sufficient details so that your team can write tasks and test cases to implement the item.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   [Acceptance Criteria](../../queries/titles-ids-descriptions.md) 
   :::column-end:::
   :::column span="3":::
   Provide the criteria to be met before the bug or user story can be closed. Before work begins, describe the customer acceptance criteria as clearly as possible. Conversations between the team and customers to define the acceptance criteria help ensure that your team understands your customers' expectations. You can use the acceptance criteria as the basis for acceptance tests to more effectively evaluate whether an item is satisfactorily completed.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   [Value Area](../../queries/planning-ranking-priorities.md)
   :::column-end:::
   :::column span="3":::
   The area of customer value addressed by the epic, feature, requirement, or backlog item. Values include:  
   - **Architectural**: Technical services to implement business features that deliver solution 
   - **Business**: Services that fulfill customers or stakeholder needs that directly deliver customer value to support the business (Default)
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   [Story Points](../../queries/query-numeric.md)
   :::column-end:::
   :::column span="3":::
   Estimate the amount of work required to complete a user story using any numeric unit of measurement your team prefers.

   Agile [velocity charts](../../../report/dashboards/team-velocity.md) and [forecast](../../sprints/forecast.md) tools reference the values in this field. For more information, see the [Estimating](/previous-versions/visualstudio/visual-studio-2013/hh765979(v=vs.120)) white paper.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   [Priority](../../queries/planning-ranking-priorities.md)
   :::column-end:::
   :::column span="3":::
   A subjective rating of the user story, feature, or requirement as it relates to the business. Allowed values are:
   - **1**: Product can't ship without the feature.
   - **2**: Product can't ship without the feature, but it doesn't have to be addressed immediately.
   - **3**: Implementation of the feature is optional, based on resources, time, and risk.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   [Risk](../../queries/planning-ranking-priorities.md)

   :::column-end:::
   :::column span="3":::
   A subjective rating of the relative uncertainty around the successful completion of a user story. Allowed values are:
   - **1 - High**
   - **2 - Medium**
   - **3 - Low**
   :::column-end:::
:::row-end:::

[!INCLUDE [temp](../../includes/discussion-tip-azure-devops.md)] 

## Track progress

As work progresses, you change the State field to update the status. Optionally, you can specify a reason. The state and reason fields appear on the work item form in the header area. 

:::image type="content" source="media/agile-bug-form-state-reason.png" alt-text="Screenshot of Bug work item form, header area.":::

### Agile workflow states 

When you update the workflow, teams know which items are new, in progress, or completed. Most WITs support transition both forward and backward from each workflow state. These diagrams show the main progression and regression states of the user story, bug, and task WITs. 


|User Story |Bug  |Task  |
|---------|---------|---------|
|:::image type="content" source="media/ALM_PT_Agile_WF_UserStory.png" alt-text="Conceptual image of User Story workflow states, Agile process.":::   |  :::image type="content" source="media/agile-bug-workflow.png" alt-text="Conceptual image of Bug workflow states, Agile process.":::       | :::image type="content" source="media/ALM_PT_Agile_WF_Task.png" alt-text="Conceptual image of Task workflow states, Agile process.":::        |

A typical workflow progression for a user story follows:

-  The product owner creates a user story in the **New** state with the default reason, **New user story**.  
-  The team updates the status to **Active** when they decide to complete the work during the sprint.  
-  A user story gets moved to **Resolved** when the team has completed all its associated tasks and unit tests for the story pass.  
-  A user story gets moved to the **Closed** state when the product owner agrees that the story has been implemented according to the Acceptance Criteria and acceptance tests pass.

### Update status with board or Taskboards

Teams can use the [board](../../boards/kanban-overview.md) to update the status of requirements, and the [Taskboard](../../sprints/task-board.md) to update the status of tasks. Dragging items to a new state column updates both the State and Reason fields.

![Screenshot of Track progress on the board.](../../boards/media/alm-cc-move-card.png)

You can customize the board to support more [swimlanes](../../boards/expedite-work.md) or [columns](../../boards/add-columns.md). For more information, see [Customize your work tracking experience](#customize-work-item-types).


## Map user stories to features

When you manage a suite of products or user experiences, you might want to view the scope and progress of work across the product portfolio. You can view the scope and progress of work by [defining features](../../backlogs/define-features-epics.md) and [mapping user stories to features](../../backlogs/organize-backlog.md).

Using portfolio backlogs, you can [drill down from one backlog to another](../../plans/portfolio-management.md) to view the level of detail you want. Also, use portfolio backlogs to view a rollup of work in progress across several teams when you [setup a hierarchy of teams](../../../organizations/settings/add-teams.md).

## Define tasks 

When your team manages their work in sprints, they can use the [sprint backlog page](../../sprints/assign-work-sprint.md) to break down the work to be accomplished into distinct tasks.  

:::image type="content" source="media/IC697761.png" alt-text="Screenshot of Sprint backlog, add task.":::

Name the task and estimate the work it takes.

:::image type="content" source="media/agile-task-form.png" alt-text="Screenshot of Agile task work item form.":::

When you use the Agile process, teams forecast work and define tasks at the start of each sprint. Each team member then performs a subset of those tasks. Tasks can include development, testing, and other kinds of work. For example, a developer defines tasks to implement user stories, and a tester defines tasks to write and run test cases.

When teams estimate work using hours or days, they define tasks and the **Remaining Work** and **Activity** (optional) fields.

:::row:::
   :::column span="1":::
   **Field/tab**
   :::column-end:::
   :::column span="3":::
   **Usage**
   :::column-end:::
:::row-end:::
---
:::row:::
   :::column span="1":::
   [Original Estimate](../../queries/query-numeric.md)
   :::column-end:::
   :::column span="3":::
   The amount of estimated work required to complete a task. Typically, this field doesn't change after it's assigned.
   You can specify work in hours or in days. There are no inherent time units associated with this field.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   [Remaining Work](../../queries/query-numeric.md)
   :::column-end:::
   :::column span="3":::
   The amount of work remaining to complete a task. As work progresses, update this field. This field is used to calculate [capacity charts](../../sprints/set-capacity.md), the [sprint burndown chart](../../../report/dashboards/configure-sprint-burndown.md), and the following SQL Server reports: [Burndown and Burn Rate](/previous-versions/azure/devops/report/sql-reports/burndown-and-burn-rate-report), [Remaining Work](/previous-versions/azure/devops/report/sql-reports/remaining-work-report), and [Status on All Iterations](/previous-versions/azure/devops/report/sql-reports/status-on-all-iterations-report).
   If you divide a task into subtasks, specify hours for the subtasks only. You can specify work in any unit of measurement your team chooses.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   [Completed Work](../../queries/query-numeric.md) 
   :::column-end:::
   :::column span="3":::
   The amount of work spent implementing a task.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   [Activity](../../queries/query-numeric.md) 
   :::column-end:::
   :::column span="3":::
   Select the type of activity this task represents when your team estimates sprint capacity by activity.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   [Integrated in Build](../../queries/build-test-integration.md)
   :::column-end:::
   :::column span="3":::
   Product build number that incorporates the code or fixes a bug.
   :::column-end:::
:::row-end:::  

## Track test progress 
Track testing progress with [user stories](#test-user-stories) and [code defects](#track-code-defects).

### Test user stories

From the web portal or Test Manager, you can [create test cases that automatically link to a user story or bug](../../../test/create-test-cases.md). Or, you can link a user story to a test case from the :::image type="icon" source="../../backlogs/media/icon-links-tab-wi.png" border="false"::: **Links** tab. 

:::image type="content" source="media/test-plan-new-item.png" alt-text="Screenshot of Test plan web portal.":::

The test case contains multiple fields, many of which are automated and integrated with Test Manager and the build process. For a description of each field, see [Query based on build and test integration fields](../../queries/build-test-integration.md).

:::image type="content" source="media/agile-test-case-form.png" alt-text="Screenshot of test case form.":::

The :::image type="icon" source="../../backlogs/media/icon-links-tab-wi.png" border="false"::: (links tab) captures the links to user stories and bugs in a test case. By linking user stories and bugs to test cases, the team can track the progress made in testing each item. By defining these links, you support information that appears in the [Stories Overview Report](../../../report/sql-reports/stories-overview-report-agile.md) report.

### Track code defects

You can [create bugs from the web portal, Visual Studio, or when testing with Test Manager](../../backlogs/manage-bugs.md). 

[!INCLUDE [temp](../../includes/common-work-item-fields.md)]   

## Customize work item types

[!INCLUDE [temp](../../includes/customize-work-tracking.md)] 


## Related content

[!INCLUDE [temp](../../includes/create-team-project-links.md)]  
   

### Track issues 

Issues are used to track events that may block progress or shipping a user story. Bugs, on the other hand, are used to track code defects. You can add an issue from the  [New work item widget](../../../report/dashboards/widget-catalog.md#new-work-item-widget) added to a [team dashboard](../../../report/dashboards/dashboards.md), or from the **New** menu on the Queries page. 

![Screenshot of Add work item from a New work item widget.](../../../user-guide/media/features/alm-feature-new-work-item-widget.png)  

Work items you add from the widget are automatically scoped to your team's default area and iteration paths. To change the team context, see [Switch team context](../../../project/navigation/go-to-project-repo.md?toc=/azure/devops/boards/plans/toc.json).  
 
### Track business value  
You can use the Priority field to differentiate the value of various stories. Or, you can add a custom field to the User Story WIT that tracks the relative value of stories. To learn how, see [Customize a field for a process](../../../organizations/settings/work/customize-process-field.md).

### Backlog list order

The [Stack Rank](../../queries/planning-ranking-priorities.md) field is used to track the relative ranking of user stories, however by default it doesn't appear on the work item form. The sequence of items on the backlog page is determined according to where you've [added the items or moved the items on the page](../../backlogs/create-your-backlog.md#move-items-priority-order). As you drag items, a background process updates this field.

