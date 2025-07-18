---
title: Navigating within the web portal  
titleSuffix: Azure DevOps
description: Navigate within the user interface/web portal of Azure DevOps
ms.custom: "navigation, cross-project, cross-service"
ms.subservice: azure-devops-projects 
ms.author: chcomley
author: chcomley
ms.topic: overview
monikerRange: '<= azure-devops'
ms.date: 03/11/2025
---

# Navigate the Azure DevOps web portal

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)] 

::: moniker range="azure-devops"

The Azure DevOps web portal is organized into various services, administrative pages, and task-specific features like the search box. Service labels vary depending on whether you’re using Azure DevOps Services or an on-premises version.

[!INCLUDE [temp](../../includes/version-selector.md)] 

Each service offers multiple pages with numerous features and functional tasks. Within each page, you can choose options to select or add specific artifacts.

::: moniker-end

## Key features and navigation

Here's what you need to know to start using the web portal effectively.  

- [**Open a service, page, or settings**](go-to-service-page.md): Use to switch to a different [service or functional area](../../user-guide/what-is-azure-devops.md) 
- [**Add an artifact or team**](add-artifact-team.md): Use to quickly add a work item, Git repo, build or release pipelines, or a new team
- [**Open another project or repo**](work-across-projects.md): Use to switch to a different project or access work items and pull requests defined in different projects, or your favorite items
- [**Open team artifacts, use breadcrumbs, selectors and directories**](use-breadcrumbs-selectors.md): Use to navigate within a service, open other artifacts, or return to a root function
- [**Work with favorites**](set-favorites.md): Mark your favorite artifacts for quick navigation  
- [**Search box**](../search/get-started-search.md): Use to find code, work items, or wiki content  
- [**Your profile menu**](../../organizations/settings/set-your-preferences.md?toc=/azure/devops/project/navigation/toc.json&bc=/azure/devops/project/navigation/breadcrumb/toc.json): Use to set personal preferences, notifications, and enable preview features  
- [**Settings**](../../organizations/settings/about-settings.md#project-administrator-role-and-managing-projects): Use to add teams, manage security, and configure other project and organization level resources.  

> [!NOTE]  
> Only enabled services are visible in the user interface. For example, if **Boards** is disabled, then **Boards** or **Work** and all pages associated with that service don't appear. To enable or disable a service, see [Turn an Azure DevOps service on or off](../../organizations/settings/set-services.md).

Select services—such as **Boards**, **Repos**, and **Pipelines**—from the sidebar and pages within those services. 

![Screenshot shows vertical sidebar.](media/gif-images/vertical-nav.gif)

Now that you understand the user interface structure, it’s time to start using it. You can find a wide range of features and functionalities to explore.

If all you need is a code repository and bug tracking solution, then start with [Get started with Git](../../repos/git/gitquickstart.md) and [Manage bugs](../../boards/backlogs/manage-bugs.md).  

To start planning and tracking work, see [About Agile tools](../../boards/get-started/what-is-azure-boards.md?context=vsts/default).

## Connect to the web portal, user accounts, and licensing  

::: moniker range="azure-devops"

You connect to the web portal through a supported web browser—such as the latest versions of Microsoft Edge, Chrome, Safari, or Firefox. Only users [added to a project](../../organizations/accounts/add-organization-users.md) can connect, which is typically done by the organization owner. 

Five account users are free as are Visual Studio subscribers and stakeholders. After that, you need to [pay for more users](../../organizations/billing/buy-basic-access-add-users.md). Find out more about licensing from [Azure DevOps pricing](https://azure.microsoft.com/pricing/details/devops/azure-devops-services/).

Limited access is available to an unlimited number of stakeholders for free. For details, see [Work as a Stakeholder](../../organizations/security/get-started-stakeholder.md). 

::: moniker-end

<a id="refresh-web-portal">  </a>

## Refresh the web portal

If data doesn't appear as expected, the first thing to try is to refresh your web browser. Refreshing your client updates the local cache with changes that were made in another client or the server. To refresh the page or object you're currently viewing, refresh the page or choose the ![Refresh icon](../../media/icons/refresh.png) **Refresh** icon if available.  

[!INCLUDE [temp](../../includes/when-to-refresh-client.md)]

## Differences between the web portal and Visual Studio  

Although you can access source code, work items, and builds from both clients, some task specific tools are only supported in the web browser or an IDE but not in both. Supported tasks differ depending on whether you connect to a Git or TFVC repository from Team Explorer. 

---
:::row:::
   :::column span="2":::
      **Web portal**
   :::column-end:::
   :::column span="2":::
      **Visual Studio**
   :::column-end:::
:::row-end:::
---
:::row:::
   :::column span="2":::
      - [Product backlog](../../boards/backlogs/create-your-backlog.md), [Portfolio backlogs](../../boards/boards/kanban-epics-features-stories.md), [Sprint backlogs](../../boards/sprints/assign-work-sprint.md), [Taskboards](../../boards/sprints/task-board.md), [Capacity planning](../../boards/sprints/set-capacity.md) 
      - [Boards](../../boards/boards/kanban-overview.md) 
      - [Dashboards](../../report/dashboards/dashboards.md), [Widgets](../../report/dashboards/widget-catalog.md), [Charts](../../report/dashboards/charts.md) 
      - [Request feedback](/previous-versions/azure/devops/project/feedback/get-feedback)  
      - [Web-based Test Management](../../test/overview.md)  
      - [Administration pages to administer accounts, team projects, and teams](../../organizations/settings/about-settings.md)   
   :::column-end:::
   :::column span="2":::
      - Git: [Changes](../../repos/git/commits.md#stage-your-changes-and-commit), [Branches](../../repos/git/create-branch.md), [Pull Requests](../../repos/git/pull-requests.md), [Sync](../../repos/git/pulling.md), [Work Items](../../boards/backlogs/add-work-items.md), [Builds](/previous-versions/ms181721(v=vs.140)) 
       - TFVC: [My Work](../../repos/tfvc/develop-code-manage-pending-changes.md), [Pending Changes](../../repos/tfvc/develop-code-manage-pending-changes.md) | [Source Control Explorer](../../repos/tfvc/develop-code-manage-pending-changes.md#use-solution-explorer-or-source-control-explorer-to-view-what-you-changed), [Work Items](../../boards/backlogs/add-work-items.md) | [Builds](/previous-versions/ms181721(v=vs.140)) 
       - Greater integration with work items and Office integration clients. You can open a work item or query result in an office supported client. 
   :::column-end:::
:::row-end:::
---
 
[!INCLUDE [temp](../../repos/git/includes/note-new-git-tool.md)]

## Related content

- [Manage projects](../../organizations/projects/about-projects.md) 
- [Manage settings for projects and organizations](../../organizations/settings/about-settings.md#project-administrator-role-and-managing-projects) 

