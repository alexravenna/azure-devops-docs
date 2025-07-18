---
title: Follow changes to work
titleSuffix: Azure Boards & Azure Repos
description: Learn how to track updates made to a work item or pull request by following it when using Azure Boards or Azure Repos.
ms.custom: work-items, cross-project
ms.subservice: azure-devops-settings
ms.assetid: 77CAEE8E-BF1A-47DA-9818-A0C52BAC813C
ms.author: chcomley
author: chcomley
ms.topic: tutorial
monikerRange: '<= azure-devops'
ms.date: 07/13/2022
---

# Tutorial: Follow changes made to a user story, bug, or other work item or pull request  

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)]

<a id="follow"></a>  

To get notified of changes made to a specific work item or a pull request, you can choose to follow them. The Follow feature provides an improvised way of getting notified on a case-by-case basis. 

If you want to subscribe to receive notifications automatically based on changes that occur based on your targeted set of criteria, see [Manage personal notifications](../../organizations/notifications/manage-your-personal-notifications.md). For example, you can create a subscription to automatically get notified whenever a work item that you created or that was assigned to you is modified. 

> [!NOTE]  
> Notification subscriptions allow you to personalize the notifications you receive automatically based on additional criteria you specify for [yourself](../../organizations/notifications/manage-your-personal-notifications.md), a team, or a project. For example, you can create a subscription and add field criteria to receive changes based on one or more of the following templates. 
>
> ![Work item notification templates](media/follow-work/work-item-notifications.png) 

This article shows you how to:

>[!div class="checklist"]  
> * Follow a work item
> * Follow a pull request 
> * Manage work items that you're following

  

## Prerequisites

[!INCLUDE [prerequisites-work-items](../includes/prerequisites-work-items.md)]

## Follow a work item

When you want to track the progress of a single work item, choose the :::image type="icon" source="../media/icons/follow-icon.png" border="false"::: follow icon. This signals the system to notify you when changes are made to the work item.  

::: moniker range=">= azure-devops-2020"

> [!div class="mx-imgBorder"]  
> ![Work item form, Follow icon control](media/follow-work/follow-work-item.png) 

If you want to specify conditions on when you'll get notified of changes, choose the :::image type="icon" source="../media/icons/gear_icon.png" border="false"::: gear icon and choose from the options provided. 

> [!div class="mx-imgBorder"]  
> ![Work item form, Notification settings dialog for follow](media/follow-work/notification-settings-for-follow.png) 

By default, you're **Subscribed** to receive a notification when any change is made to the work item. Choose **Not Subscribed** to receive notification only when you're @mentioned. Or choose **Custom** to receive notifications when one of the checked fields changes, **State**, **Assigned To**, or **Iteration Path**. 

::: moniker-end

You'll only receive notifications when other members of your team modify the work item, such as adding to the discussion, changing a field value, or adding an attachment. 

Notifications are sent to your preferred email address, which [you can change from your user profile](../../organizations/notifications/change-email-address.md)

To stop following changes, choose the  :::image type="icon" source="../media/icons/following-icon.png" border="false":::  following icon.
 
<a id="follow-pr"></a>

## Follow a pull request 

To track the progress of a single pull request, choose the  :::image type="icon" source="../media/icons/actions-icon.png" border="false"::: actions icon for the pull request, and select the :::image type="icon" source="../media/icons/follow-icon.png" border="false"::: **Follow** option. This signals the system to notify you when changes are made to the PR.  

<img src="media/follow-pull-request.png" alt="Pull Request, context menu, Follow icon option" />  

You'll only receive notifications when other members of your team modify the PR, such as adding to the discussion or adding an attachment. 

Notifications are sent to your preferred email address, which [you can change from your user profile](../../organizations/notifications/change-email-address.md).  

To stop following changes, open the PR context menu and choose the  :::image type="icon" source="../media/icons/following-icon.png" border="false":::  Following icon. 

## Manage work items that you're following  

You can review and manage all the work items you've selected to follow.

::: moniker range="<=azure-devops"

Open **Boards>Queries**, choose **All**, and under **My Queries**, choose **Followed work items**.   

> [!div class="mx-imgBorder"]  
> ![Boards>Queries>All>Followed work items, new nav](media/follow-work/following-work-items-vert.png)   

From this view, you can view all items you're following across all projects. Also, you can complete similar actions supported with a query results view, such as:
- Refresh the view
- Add or remove visible columns
- Sort the order of specific columns
- Filter results by text or tags 
- Set work item pane
- Enter full screen mode. 

You can also view and manage work that you're following from **Boards>Work Items** and pivot to **Following**. 

> [!div class="mx-imgBorder"]  
> ![Boards>Work Items, and pivot to Following.](media/follow-work/open-work-items-vert.png)   

::: moniker-end   

 

## Query work items that you're following

You can use the **\@Follows** macro in a work item query to filter a list based on work items you're following along with other query filters. 

For example, the following query shows how to query across all projects for active work items that you're following. You use the **ID** field and the **In** operator with the **\@Follows** macro.  

:::image type="content" source="media/follow-work/query-follows.png" alt-text="Query Editor, with ID In @Follows query clause":::

## Next steps

> [!div class="nextstepaction"]
> [Add, update, and follow a work item](../backlogs/add-work-items.md) 

## Related content  

- [Manage personal notifications](../../organizations/notifications/manage-your-personal-notifications.md)  
- [View and update work items via the mobile work item form](../../project/navigation/mobile-work.md)  

### Q: Can I add someone else to follow a work item or PR?

**A:** No, you can't add another team member to follow a work item or pull request at this time. You can subscribe them to get notified based on select criteria, such as when a work item is create or modified, or a pull request is created. For more information, see [Manage team notifications](../../organizations/notifications/manage-team-group-global-organization-notifications.md).	
