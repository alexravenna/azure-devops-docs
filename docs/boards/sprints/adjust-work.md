---
title: Adjust work to fit sprint capacity
titleSuffix: Azure Boards
description: Learn how to adjust items assigned to a sprint to align with a team's sprint capacity. 
ms.custom: boards-sprints
ms.service: azure-devops-boards
ms.assetid: 
ms.author: chcomley
author: chcomley
ms.topic: tutorial
monikerRange: '<= azure-devops'
ms.date: 09/20/2021
---

# Adjust work to fit sprint capacity

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)] 

<a id="adjust-work">  </a>

Check your team's capacity after you've defined all the tasks for all the sprint backlog items. You can consider adding more items onto the sprint if your team is under capacity. If over capacity, you'll want to remove items out of the backlog.  

Next, check whether any team member is under, at, or over capacity. Or, if someone hasn't even been assigned any work. Use the capacity bars to make these determinations. If you haven't yet [set capacity for your team](set-capacity.md), do that now.

![Over capacity](media/IC795969.png)  

Use this article to learn how to:
> [!div class="checklist"]   
> * Adjust your sprint plan if your team is over or under capacity    
> * Load balance work across your team 
> * Quickly reassign tasks to another team member    

## Prerequisites

[!INCLUDE [temp](../includes/prerequisites.md)]

## Open a Sprint backlog for a team 

::: moniker range=">= azure-devops-2020"

1. From your web browser, open your team's sprint backlog. (1) Check that you've selected the right project, (2) choose **Boards>Sprints**, (3) select the correct team from the team selector menu, and lastly (4), choose **Backlog**. 

    > [!div class="mx-imgBorder"]  
    > ![Open Work, Sprints, for a team](media/add-tasks/open-sprint-backlog-s155-co.png)

    To choose another team, open the selector and select a different team or choose the :::image type="icon" source="../../media/icons/home-icon.png" border="false"::: **Browse all sprints** option. Or, you can enter a keyword in the search box to filter the list of team backlogs for the project.

    > [!div class="mx-imgBorder"]  
    > ![Choose another team](media/add-tasks/team-selector-sprints-agile.png) 

2. To choose a different sprint than the one shown, open the sprint selector and choose the sprint you want. 

    > [!div class="mx-imgBorder"]  
    > ![Choose another sprint](media/add-tasks/select-specific-sprint-agile.png)

    The system lists only those sprints that have been selected for the current team focus. If you don't see the sprints you want listed, then choose **New Sprint** from the menu, and then choose **Select existing iteration**. For more information, see [Define iteration (sprint) paths](../../organizations/settings/set-iteration-paths-sprints.md). 

::: moniker-end

## Check your team capacity 

To view capacity charts, you'll want to turn **Work details** on for a sprint.

::: moniker range="<=azure-devops"

> [!div class="mx-imgBorder"]  
> ![Turn work details on](media/adjust-work/work-details-on.png)

::: moniker-end

## Move items out of a sprint

Move items from the sprint backlog back to the product backlog if your team is over capacity. This action resets the Iteration Path to the default set for your team. Or, you can move the item into the next sprint your team works in. All the tasks that you've defined for that item move with the backlog items.   

::: moniker range="<=azure-devops"

Here we select two items at the bottom of the sprint backlog, open the  :::image type="icon" source="../../media/icons/actions-icon.png" border="false"::: action icon for one of the items, choose **Move to iteration**, and then select **Backlog**. 

> [!div class="mx-imgBorder"]  
> ![Move work items to backlog](media/adjust-work/move-items-to-backlog-agile.png)

> [!TIP]    
> Optionally, you can open the **Planning** pane and drag a work item to the backlog or another sprint which reassigns all child tasks to the same iteration path. See [Assign work to a sprint](assign-work-sprint.md#drag-drop). Also, you can multi-select several items and drag them to the backlog or another sprint. Users with **Stakeholder** access can't drag-and-drop work items.

::: moniker-end

## Balance work across the team

To quickly reassign tasks, drag the task onto the new assignee's capacity bar. 

::: moniker range="<=azure-devops"

For example, here we reassign work from Raisa Pokrovskaya to Christie Church. 

> [!div class="mx-imgBorder"]  
> ![Reassign work, drag and drop task onto an assignee](media/adjust-work/load-balance-work.png)   

As you reassign tasks, capacity bars automatically update.  

> [!div class="mx-imgBorder"]  
> ![Capacity bars adjusted](media/adjust-work/adjusted-work.png)   

::: moniker-end

## Next step
> [!div class="nextstepaction"]
> [5. Share your sprint plan](share-plan.md) 