---
title: Troubleshoot an Analytics view
titleSuffix: Azure DevOps
description: Learn how to resolve errors that occur with an Analytics view and Power BI for Azure DevOps.
ms.subservice: azure-devops-analytics
ms.author: chcomley
author: chcomley
ms.topic: troubleshooting
monikerRange: "<=azure-devops"
ms.date: 10/13/2021
---

# Resolve errors associated with an Analytics view

[!INCLUDE [version-gt-eq-2019](../../includes/version-gt-eq-2019.md)]

An Analytics view provides a simplified way to specify the filter criteria for a Power BI report based on Analytics data. Analytics provides the reporting platform for Azure DevOps. You manage Analytics views in the web portal for Azure DevOps and then access them with the [Power BI Connector](data-connector-connect.md). 

[!INCLUDE [temp](includes/analytics-views-warning.md)]

## Prerequisites

[!INCLUDE [prerequisites-simple](../includes/analytics-prerequisites-simple.md)]

## Resolve size warnings

### Warning: This view may contain too much data

This warning appears when Power BI determines that it can't load all the data contained within the view. It typically occurs when you haven't specified sufficient filters within the view or you've specified to load all history with a daily granularity. 

To resolve this warning, specify other [work items filters](analytics-views-create.md#specify-wi-filters) or modify the [History or Granularity](analytics-views-create.md#select-trend-data) to scope the view's results. 

Views that pull a large amount of data might take a long time to refresh and load in Power BI. For organizations with a large amount of data, it might even fail to load. To make sure your view will successfully load in Power BI, [Verify](analytics-views-create.md#verify-and-save) your view before saving it. 

## Resolve verification errors

### Error: The field 'FieldName' already exists

This error indicates that one of your project's [custom fields](../../organizations/settings/work/customize-process-field.md) is a duplicate of an [Analytics field](../extend-analytics/data-model-analytics-service.md). 

To resolve this error, rename your custom field.

### Error: Field doesn't exist anymore

This error means that one of your [work items filters](analytics-views-create.md#specify-wi-filters) or [view fields](analytics-views-create.md#select-fields) references a field that was removed from your [project process](../../organizations/settings/work/customize-process-field.md). 

To resolve this error, [edit your view](analytics-views-manage.md#edit-an-existing-view) and remove the filter or field from the view's definition. 

## Resolve errors in Power BI

### Analytics view ... Doesn't exist or you don't have permission to view it

This error occurs when you try to refresh a view in Power BI that is no longer available in Azure DevOps. One or more of the following actions may have occurred: 
- The view was renamed
- The view was deleted
- Your permissions to access the view were explicitly removed
- The view has been modified from a **Shared** view to a **Private** view.  

![Refresh fail - view does not exists](media/editable-views/pbi-refresh-fail.png)

To resolve this issue, check that you can access the view in Azure DevOps and that you have [permission to use the view](analytics-views-manage.md#manage-permissions).  

If the view no longer exists, you can still use the rest of your report in Power BI by deleting the loaded table from your Power BI desktop.

### The field ... already exists in the record

This error indicates that you have a custom field with the same display name as one of the Azure DevOps reserved fields.

To resolve this collision, remove the duplicate column from the view's fields. You'll need to customize your fields selection and remove the duplicate field from the [field list](analytics-views-create.md#select-fields). 

## Related articles

- [Create an Analytics view](analytics-views-create.md) 
- [Manage Analytics views](analytics-views-manage.md).  
- [Data available from Analytics](data-available-in-analytics.md)
- [Grant permissions to access Analytics](./analytics-security.md)
- [Power BI integration overview](overview.md)
