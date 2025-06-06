---
title: Configure a chart for work items widget
titleSuffix: Azure DevOps  
description: Learn how to configure a chart for work items widgets to view status, progress, and trend charts in a dashboard based on a flat-based query in Azure DevOps.
ms.custom: dashboards  
ms.subservice: azure-devops-analytics
ms.author: chcomley
author: chcomley
ms.topic: how-to
monikerRange: '<= azure-devops'
ms.date: 08/17/2022
---

# Configure a chart for work items widget  

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)]

The **Chart for Work Items** widget lets you select any flat-list query and configure it to support any of the supported chart types. The steps you take to configure this widget are very similar to those you take to configure a query-based chart.  

To view a chart on a dashboard, you can start from **Queries>Charts** page and choose to add the chart to the dashboard. Charts added to the dashboard show up as a **Chart for Work Items** widget that you can relabel, resize, and reconfigure. Or, you can add a **Chart for Work Items** widget, select the query, and configure the chart as normal. 
::: moniker range=">= azure-devops-2022"
The only task you can accomplish from the **Chart for Work Items** widget that you can't from the **Queries>Charts** page is grouping work items by Tags. This feature is supported for Azure DevOps server 2022 and later versions. 
::: moniker-end
  
## Prerequisites 

::: moniker range="azure-devops"

> [!NOTE]  
> Users with **Stakeholder** access for a public project have full access to query chart features just like users with **Basic** access. For more information, see [Stakeholder access quick reference](../../organizations/security/stakeholder-access.md).

::: moniker-end

::: moniker range=">= azure-devops-2020"

| Category | Requirements |
|-------------|-------------|
| **Access** | [Project member](../../organizations/accounts/add-organization-users.md) with at least **Basic** access. Users with **Stakeholder** access can't view or create charts from the **Queries** page. They can view charts added to a team dashboard. For more information, see [Stakeholder access quick reference](../../organizations/security/stakeholder-access.md). |
| **Permissions** |- By default, users with at least **Basic** access can create charts. Users with **Stakeholder** access can't view or create charts from the **Queries** page, however, they can view charts added to a team dashboard. For more information, see [Stakeholder access quick reference](../../organizations/security/stakeholder-access.md).<br>- To save a query to a **Shared Queries** folder: Permissions to save queries under a folder. For more information, see [Set permissions on queries and query folders](../../boards/queries/set-query-permissions.md).<br>- To add a widget to a team dashboard: Member of the team or member of the **Project Administrators** security group.<br>- To add a widget to a project dashboard: Dashboard creator or **Edit** permissions for the dashboard, or member of the **Project Administrators** security group.<br>- To view a query-based widget added to a dashboard: **Read** permissions to the underlying query. If that permission is denied, the widget displays a *Widget failed to load* message. |
| **Queries** | - Only [flat-list queries](charts.md#create-a-flat-list-query) support charts.<br>- To add a chart to a dashboard: Save the query to a **Shared Queries** folder. To do so, [get permissions to save queries under a folder](../../boards/queries/set-query-permissions.md). |

::: moniker-end

 
For more information about dashboard permissions, see [Set dashboard permissions](dashboard-permissions.md). 

### Define and save a flat-list query 

From the **Chart for Work Items** widget, you select the query that contains the work items you want to chart. When creating a query to support your chart, follow the guidelines provided in [Create a flat-list query](charts.md#create-a-flat-list-query).  
> [!TIP]   
> If you start to configure a **Chart for Work Items** widget and then add the query you want to select, you must refresh your dashboard browser page in order to select the newly added query. 

### Create a dashboard 

Prior to adding a widget to a dashboard, you must first add the dashboard to the project. To learn how, see [Add, rename, and delete dashboards](dashboards.md). 

<a name="add-chart-widget"></a> 

## Add the Chart for Work Items widget to a dashboard   

::: moniker range="<=azure-devops"

1. From the web portal, open the dashboard you want to add the chart to.  

2. To add widgets to the dashboard, select :::image type="icon" source="media/icons/edit-icon.png" border="false"::: **Edit** to open the widget catalog.  

	> [!NOTE]   
	> If you don't see the :::image type="icon" source="media/icons/edit-icon.png" border="false"::: **Edit** option, then you need to [get permissions to edit the dashboard](dashboard-permissions.md). 

3. Select the **Chart for Work Items** widget and then select **Add** or drag it onto the dashboard.    

	![Web portal, Dashboards page, Widget catalog, Chart for work items widget](media/widget-chart-work-query.png) 

4. To configure the widget, select the widget's :::image type="icon" source="../../media/icons/actions-icon.png" border="false"::: **More actions** and choose the :::image type="icon" source="../../media/icons/gear_icon.png" border="false"::: **Configure** option.  

	:::image type="content" source="media/chart-work-items/widget-more-actions-menu.png" alt-text="Screenshot of dashboard widget More actions menu options.":::

	The Configuration dialog opens. 

5. Enter a **Title**, select the **Width** and **Height**, and then select the flat-list **Query** on which the chart is based. Next, choose the **Chart type**.   

5. Give the chart a title, select the flat list query on which the chart is based, and choose the chart type.   

	:::image type="content" source="media/chart-work-items/configure-chart-widget-2020.png" alt-text="Configuration dialog for chart work items widget, Azure DevOps Server 2020 and later versions.":::

	Based on your chart type, specify values for the remaining fields. Change a chart color simply by choosing another color from those shown. For additional guidance on choosing and configuring specific chart types, see [Track progress with status and trend query-based charts](charts.md).

6. After you save your changes, you'll see the new chart has been added to the dashboard. 

	:::image type="content" source="media/chart-work-items/pivot-chart-type-state.png" alt-text="Chart for work items widget, Pivot on type and state example. ":::

	> [!TIP]  
	> If the chart doesn't display all the rows or columns you want, try changing the chart **Width** and **Height**. Pivot tables and other chart types will display more data based on the area provided on the dashboard.  
7. Drag the tile anywhere on the dashboard to put it where you want it. 

8. When you're finished with your changes, select **Done Editing** to exit dashboard edit mode.
::: moniker-end

::: moniker range=">= azure-devops-2022"

<a name="group-by-tags"></a> 

## Group by Tags chart 

> [!NOTE]   
> You can't group a query-based chart by tags, however, you can group a **Chart for Work Items** widget by tags that you add to a dashboard.  

To group a chart by tags, perform the same steps provided in the previous section. Make sure that your flat-list query contains **Tags** in the query clause or as a column option. Then, select **Tags** for the **Group by** selection. To filter the chart to show only some tags, select the **Selected tags** radio button and then choose the tags you want the chart to display.  

:::image type="content" source="media/charts/configure-chart-widget-tags.png" alt-text="Screenshot of Chart by Work Items, Configure, Group by Tags.":::

For more information about using tags, see [Add tags to work items](../../boards/queries/add-tags-to-work-items.md). 

::: moniker-end
 

## Related articles

- [Track progress with status and trend query-based charts](charts.md)
- [FAQs on Azure DevOps dashboards, charts, and reports](faqs.yml) 
- [View/configure sprint burndown](configure-sprint-burndown.md)  
- [Track test status](../../test/track-test-status.md)  
- [Add widgets and chart to a dashboard](add-widget-to-dashboard.md)
- [Widget catalog](widget-catalog.md)
