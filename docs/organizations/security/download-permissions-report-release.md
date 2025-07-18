---
title: Download permissions report for a pipeline release
titleSuffix: Azure DevOps Services
description: Download json-formatted permission report for a pipeline release.  
ms.subservice: azure-devops-audit
ms.author: chcomley
author: chcomley
ms.topic: how-to
monikerRange: 'azure-devops'
ms.date: 07/07/2022
---

# Download permission report for a release 

[!INCLUDE [version-eq-azure-devops](../../includes/version-eq-azure-devops.md)]

To determine the effective permissions of users and groups for a release, you can download the permissions report. Requesting the report generates an email with a link to download the report. The report lists the effective permissions for the release you select, for each user and group specified at the time the report is generated. Inherited permissions come from a parent group that you can view from the web portal. The report is a json-formatted report that you can open using Power BI or other json reader.  

You can also use the [Permissions Report REST API](/rest/api/azure/devops/permissionsreport/?view=azure-devops-rest-6.1&preserve-view=true) to download the report. 

## Prerequisites

[!INCLUDE [prerequisites-pca-only](../../includes/prerequisites-pca-only.md)]

## Open the security dialog for the release

You can download the report for a specific release from the release's Security dialog.  

- Open the web portal, navigate to **Pipelines>Releases**, and choose the release you want to download permissions for. Choose :::image type="icon" source="../../media/icons/more-actions.png" border="false"::: **More actions** and then choose **Security**.   

 

## Download report  

1. Choose **Download detailed report**. 

	:::image type="content" source="media/download-report/release-permissions-dialog.png" alt-text="Screenshot of Permissions dialog for a release, Download detailed report button.":::

	The following message displays indicating the request was submitted to the server. 

	:::image type="content" source="media/download-report/request-submitted-message.png" alt-text="Screenshot of request submitted message.":::

1. Once you receive the email from Azure DevOps Notifications, open it and choose **Download Report**. 

	A report labeled **PermissionsReport_**<em>GUID</em>.json appears in your **Downloads** folder. 

	> [!IMPORTANT]
	> Reports are automatically deleted after 28 days of the request. 

## Related content  

- [Set different levels of pipeline permissions](../../pipelines/policies/permissions.md#pipeline-permissions) 
- [Manage permissions with command line tool](manage-tokens-namespaces.md) 
- [Permissions Report REST API](/rest/api/azure/devops/permissionsreport/?view=azure-devops-rest-6.1&preserve-view=true)

