---
title: Add, rename, delete, and manage team dashboards
titleSuffix: Azure DevOps  
description: Learn how to create, rename, and delete team dashboards, manage dashboard permissions, and add widgets to view progress and trends in Azure DevOps.
ms.custom: "dashboards" 
ms.subservice: azure-devops-analytics
ms.assetid: B080CEFA-4D94-44B2-99E3-0E3E85616D04  
ms.author: chcomley
author: chcomley
ms.topic: quickstart
monikerRange: '<= azure-devops'
ms.date: 07/07/2022
---

# Add, rename, and delete dashboards in Azure DevOps

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)]

::: moniker range=">= azure-devops-2020"
Share progress and status with your team using configurable team or project dashboards. Dashboards provide easy-to-read, easy access, real-time information. At a glance, you can make informed decisions without having to drill down into other parts of your project. 
::: moniker-end

 
When a project is first created, a default team and default team dashboard is created labeled *Overview*. You can customize this dashboard by adding widgets. Each widget provides access to one or more features or functions. For more information about each widget, see [Widget catalog](widget-catalog.md). 

::: moniker range=">= azure-devops-2020"

## Project and team dashboards

When you add a dashboard, you can choose to make it a project dashboard or one specific to a team. Use project dashboards to display information or status about the project or when you want to control who can edit the dashboard. Use team dashboards to focus information specific to a team. 

> [!NOTE]  
> Project dashboards are owned by the person that created the dashboard. The owner can set permissions as to who can edit the dashboard. Team dashboards are owned by team administrators and can be edited by any member of the team. All dashboards can be viewed by members of the project. All widgets available to team dashboards are available for project dashboards. For team-specific widgets, if you aren't able to select a team through the widget, then the team defaults to the default project team.

::: moniker-end
 
## Prerequisites

[!INCLUDE [temp](../includes/dashboard-prerequisites.md)]

## Open Dashboards 

::: moniker range=">= azure-devops-2020"

All dashboards are associated with either a team or a project. From the **Overview>Dashboards** page, you can browse all dashboards and see which team they belong to, or if they are project dashboard.  
::: moniker-end

::: moniker range="<=azure-devops"

Open a web browser, connect to your project, and select **Overview>Dashboards**. The dashboard directory page opens. 

> [!div class="mx-imgBorder"]  
> ![Dashboards Directory, new navigation](media/dashboards/open-dashboards-vert.png)

It lists dashboards in the following order: 
- Your last visited dashboard
- Your favorited dashboards
- All dashboards of teams that you belong to
- All dashboards defined for the project in alphabetical order. 

Select the :::image type="icon" source="../../media/icons/filter-icon.png" border="false"::: filter icon to filter the list by keyword or team. Keywords apply to dashboard titles, descriptions, and team names.

> [!div class="mx-imgBorder"]  
> ![Filter the dashboard directory](media/dashboards/filter-directory.png)   

If you need to switch to a different project, select the :::image type="icon" source="../../media/icons/project-icon.png" border="false"::: Azure DevOps logo to [browse all projects](../../project/navigation/go-to-project-repo.md).  

::: moniker-end  

<a id="choose-dashboard"></a>

## Select a dashboard 

::: moniker range="<=azure-devops"

1. Select a dashboard from the directory list, or from the selector. To return to the dashboard directory, select the **Browse all dashboards** option. 
 
	> [!div class="mx-imgBorder"]
	> ![Dashboards, Browse all dashboards option](media/dashboards/browse-all-dashboards.png)  
	 
1. To favorite a dashboard, hover over the dashboard and select the ![star icon](../../media/icons/icon-favorite-star.png).  

	> [!div class="mx-imgBorder"]
	> ![Dashboards, Favorite a dashboard](media/dashboards/favorite-dashboard.png)  

	Favoriting a dashboard will cause it to appear under **My Favorites dashboards** list on the dashboards directory. Also, it will appear towards the top in the **Dashboards** selector and in your [personal Favorites list](../../project/navigation/set-favorites.md). 

::: moniker-end

  

## Add a dashboard 

Add a new dashboard as needed to support your team's needs. You can also edit and rename any existing dashboards associated with your team.

> [!NOTE]
> There is a limit of 500 dashboards per project. You'll receive an error message if you try to create a dashboard beyond that limit. Delete unused dashboards to resolve the error. 

::: moniker range=">= azure-devops-2020"

1. From the Dashboards directory, select **New Dashboard**. Or, when viewing a dashboard, open the selector and select the :::image type="icon" source="media/icons/blue-plus-icon.png" border="false"::: **New Dashboard** option. 

	> [!div class="mx-imgBorder"]  
	> ![Open the create a dashboard dialog](media/dashboards/open-new-dashboard-dialog.png)  

	If you don't see the :::image type="icon" source="media/icons/blue-plus-icon.png" border="false"::: **New Dashboard** option, then you're not a team admin for the currently selected team, or you don't have permissions to add and edit dashboards. Either [switch the context to your team](../../project/navigation/go-to-project-repo.md?toc=/azure/devops/report/toc.json&bc=/azure/devops/report/breadcrumb/toc.json), or request you be added as a [team admin](../../organizations/settings/add-team-administrator.md?toc=/azure/devops/report/toc.json&bc=/azure/devops/report/breadcrumb/toc.json). 

2. Enter the name of the dashboard and other information you want to capture. 

	Here we choose to create a Project dashboard. To create a team dashboard, select **Team Dashboard** and then select a team. To add a team, see [Add a team](../../organizations/settings/add-teams.md). 
	> [!div class="mx-imgBorder"]  
	> ![Create a Project dashboard.](media/dashboards/create-dashboard-project-dialog.png)  

1.	Select **Create**. 

3.  The widget catalog opens. You can add one or more widgets to the dashboard. You can then configure and resize each widget as needed. 

4.	You can move the widgets around the dashboard to place them where you want them. 

5.  When you're done making changes, select **Done Editing**. 

::: moniker-end

<a id="manage">  </a> 

## Rename, delete, and enable auto-refresh  

You can rename or delete a dashboard. When you enable auto-refresh, the dashboard automatically updates every 5 minutes.  

::: moniker range=">= azure-devops-2020"  
> [!NOTE]  
> To delete a project dashboard, be a member of the[**Project Collection Administrators** group](../../organizations/security/change-organization-collection-level-permissions.md).  
::: moniker-end

::: moniker range="<=azure-devops"

- To rename a dashboard, modify its description, or change its automatic refresh setting, open the dashboard, select the ![gear icon](media/icons/gear-icon.png) gear icon, and change the field options shown. Save your changes. 

- To delete a dashboard, open the Dashboards directory, select  :::image type="icon" source="../../media/icons/actions-icon.png" border="false"::: **More Actions** for the dashboard, and select **Delete**.  

	> [!div class="mx-imgBorder"]
	> ![Delete a dashboard](media/dashboards/delete-dashboard.png)  

- To set permissions for a dashboard, select the **Security** option. For details, see [Set dashboard permissions](dashboard-permissions.md).
::: moniker-end

## Move or delete a widget

> [!TIP]   
> When you're in dashboard edit mode, you can remove, rearrange, and configure widgets, as well as add new widgets. Once you leave edit mode, the widget tiles remain locked, reducing the chances of accidentally moving a widget.  

::: moniker range="<=azure-devops"
Select :::image type="icon" source="media/icons/edit-icon.png" border="false"::: **Edit** to modify your dashboard. 

You can now add widgets or drag tiles to reorder their sequence on the dashboard. 

To remove a widget, select ![actions icon](../../media/icons/actions-icon.png) **More actions** and select **Delete** .  

> [!div class="mx-imgBorder"]  
> ![Delete a widget from a dashboard](media/dashboards/delete-widget.png) 

When you're finished with your changes, select **Done Editing** to exit dashboard edit mode.
::: moniker-end

## Extensibility 

Using the REST API service, you can [create a dashboard widget](../../extend/develop/add-dashboard-widget.md). For more information about the REST APIs for dashboards and widgets, see [Dashboards (API)](/rest/api/azure/devops/dashboard/dashboards).

## Try this next 

As you can see, you can use team dashboards to provide guidance and keep your team in sync, providing visibility across your org about status, trends, and progress. 

> [!div class="nextstepaction"]
> [Add a widget to a dashboard](add-widget-to-dashboard.md)
  
## Related articles

- [FAQs on Azure DevOps dashboards, charts, and reports](faqs.yml)
- [Add a team](../../organizations/settings/add-teams.md)
- [Widget catalog](widget-catalog.md)
- [Marketplace widgets](https://marketplace.visualstudio.com/search?term=widget&target=VSTS&category=All%20categories&sortBy=Relevance)

