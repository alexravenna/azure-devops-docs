---
title: Extend the Work Item Form | Azure DevOps Extensions
description: Learn how to extend work item tracking, including adding an action, an observer, a group, or a page to the work item form in Azure DevOps.
ms.assetid: bffc76b7-f6ba-41f0-8460-ccb44d45d670
ms.subservice: azure-devops-ecosystem
ms.topic: conceptual
monikerRange: '<= azure-devops'
ms.author: chcomley
author: chcomley
ms.date: 04/11/2025
---

# Extend the work item form

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)]

This article explains how to use extensions to customize how the work item form gets presented to users. You can extend work item tracking, including adding an action, an observer, a group, or a page to the work item form in Azure DevOps.

* [Add a group to the main page](#addagroup)
* [Add a page (tab)](#addapage) 
* [Add an action to the context menu](#addmenuaction)
* [Add a custom control](./custom-control.md)
* [Listen for events on the form](#listenforevents)
* [Configure contributions in work item form](#showcontributions)

For the full source code, see the **UI** example in the [Azure DevOps extension samples](https://github.com/Microsoft/vso-extension-samples/tree/master/ui) on GitHub.

<a name="addagroup"></a>

## Add a group

:::image type="content" source="media/add-workitem-extension-group.png" alt-text="Screenshot that shows the toolbar item in work item form.":::

To add a group to the main page, add a contribution to your extension manifest. The type of this contribution should be `ms.vss-work-web.work-item-form-group` and it should target the `ms.vss-work-web.work-item-form` contribution. 

 ```json
"contributions": [
    {  
        "id": "sample-work-item-form-group",
        "type": "ms.vss-work-web.work-item-form-group",
        "description": "Custom work item form group",
        "targets": [
            "ms.vss-work-web.work-item-form"
        ],
        "properties": {
            "name": "My Group",
            "uri": "workItemGroup.html",
            "height": 600
        }
    }
]
```

### Properties

| Property     | Description           |
|--------------|-----------------------|
| `name`       | Text that appears on the group.   |
| `uri`        | URI to a page that hosts the html that shows on the work item form and its scripts. |
| `height`     | (Optional) Defines the height of the group. When omitted, it's 100%. |

### JavaScript sample

This example shows how to register an object that's called when events occur on the work item form that might affect your contributed group.

```js
import { IWorkItemFormService, WorkItemTrackingServiceIds } from "azure-devops-extension-api/WorkItemTracking";
import * as SDK from "azure-devops-extension-sdk";

// Get the WorkItemFormService.  This service allows you to get/set fields/links on the 'active' work item (the work item
// that currently is displayed in the UI).
async function getWorkItemFormService()
{
    const workItemFormService = await SDK.getService<IWorkItemFormService>(WorkItemTrackingServiceIds.WorkItemFormService);
    return workItemFormService;
}

// Register a listener for the work item group contribution after initializing the SDK.
SDK.register(SDK.getContributionId(), function () {
    return {
        // Called when the active work item is modified
        onFieldChanged: function(args) {
            $(".events").append($("<div/>").text("onFieldChanged - " + JSON.stringify(args)));
        },
        
        // Called when a new work item is being loaded in the UI
        onLoaded: function (args) {

            getWorkItemFormService().then(function(service) {            
                // Get the current values for a few of the common fields
                service.getFieldValues(["System.Id", "System.Title", "System.State", "System.CreatedDate"]).then(
                    function (value) {
                        $(".events").append($("<div/>").text("onLoaded - " + JSON.stringify(value)));
                    });
            });
        },
        
        // Called when the active work item is being unloaded in the UI
        onUnloaded: function (args) {
            $(".events").empty();
            $(".events").append($("<div/>").text("onUnloaded - " + JSON.stringify(args)));
        },
        
        // Called after the work item has been saved
        onSaved: function (args) {
            $(".events").append($("<div/>").text("onSaved - " + JSON.stringify(args)));
        },
        
        // Called when the work item is reset to its unmodified state (undo)
        onReset: function (args) {
            $(".events").append($("<div/>").text("onReset - " + JSON.stringify(args)));
        },
        
        // Called when the work item has been refreshed from the server
        onRefreshed: function (args) {
            $(".events").append($("<div/>").text("onRefreshed - " + JSON.stringify(args)));
        }
    }
});
```

[!INCLUDE [Events](../includes/add-workitem-extension-sharedevents.md)]

<a name="addapage"></a>

## Add a page

A new page is rendered as a tab on the work item form. New pages appear next to the **Details** tab.

:::image type="content" source="media/add-workitem-extension-page.png" alt-text="Screenshot that shows the new page as a tab on the work item form.":::

To add a page to the work item form, add a contribution to your extension manifest. The type of this contribution should be `ms.vss-work-web.work-item-form-page` and it should target the `ms.vss-work-web.work-item-form` contribution. 

```json
"contributions": [
    {  
        "id": "sample-work-item-form-page",
        "type": "ms.vss-work-web.work-item-form-page",
        "description": "Custom work item form page",
        "targets": [
            "ms.vss-work-web.work-item-form"
        ],
        "properties": {
            "name": "My Page",
            "uri": "workItemPage.html"
        } 
    }
]
```

### Properties

| Property     | Description           |
|--------------|-----------------------|
| name         | Text that appears on the tab page.   |
| uri          | URI to a page that hosts the html that shows on the work item form and its scripts. |

### JavaScript sample

See the JavaScript sample in the form group section. The name of the registered object should match the `id` of the contribution.

[!INCLUDE [Events](../includes/add-workitem-extension-sharedevents.md)]

<a name="showcontributions"></a>

## Configure contributions in work item form

In Azure DevOps Services, by default, the group extensions appear in the end of the second column of the form, and page contributions appear after all the work item form pages as a tab. Control contributions aren't shown in the form by default, so users have to manually add them to the form. In Azure DevOps Server, to show/hide or move the control, group and page contributions in work item form, see [Configure work item form extensions](./configure-workitemform-extensions.md).

<a name="addmenuaction"></a>

## Add menu action

:::image type="content" source="media/add-workitem-extension-toolbar.png" alt-text="Screenshot that shows how to add an item to the work item toolbar.":::

To add an item to the work item toolbar, add this contribution to your extension manifest. Select the vertical ellipsis in the work item form to see the dropdown menu.

 ```json
"contributions": [
    {  
       "id": "sample-work-item-menu",  
       "type": "ms.vss-web.action",  
       "description": "Sample toolbar item which updates the title of a work item",  
       "targets": [  
           "ms.vss-work-web.work-item-context-menu"  
       ],  
       "properties": {  
           "text": "Try me!",  
           "title": "Updates the title of the work item from the extension",  
           "toolbarText": "Try me!",  
           "icon": "images/show-properties.png",  
           "uri": "menu-workItemToolbarButton.html"  
       }  
    }
]
```

### Properties

| Property     | Description           |
|--------------|-----------------------|
| `text`         | Text that appears on the toolbar item. |
| `title`        | Tooltip text that appears on the menu item. |
| `toolbarText`  | Text that appears when the item is being hovered over. |
| `uri`          | URI to a page that registers the toolbar action handler. |
| `icon`         | URL to an icon that appears on the menu item. Relative URLs are resolved using `baseUri`. |
| `group`        | Determines where the menu item appears, related to others. Toolbar items with the same group name are grouped and divided by a separator from the rest of the items. |
| `registeredObjectId` | (Optional) Name of the registered menu action handler. Defaults to the contribution ID. |

<a name="listenforevents"></a>  

## Listen for events

To add an observer to the work item, which listens to the work item events, add this contribution to your extension manifest. There's no visualization for observers on the work item form. This is the best way to listen to work item form *onSaved* event since the observer lives outside of the form and doesn't get destroyed when form closes, which might happen right after save.

 ```json
"contributions": [
    {  
        "id": "sample-work-item-form-observer",
        "type": "ms.vss-work-web.work-item-notifications",
        "description": "Gets events about the current work item form for the 'Try Me!' toolbar button",
        "targets": [
            "ms.vss-work-web.work-item-form"
        ],
        "properties": {
            "uri": "myformobserver.html"
        }
    }
]
```

### Properties

| Property     | Description           |
|--------------|-----------------------|
| `uri`        | URI to a page that hosts the scripts listening to events. |

[!INCLUDE [Events](../includes/add-workitem-extension-sharedevents.md)]

### HTML/JavaScript sample

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Work item extension page sample</title>
</head>

<body>
    <script src="sdk/scripts/SDK.js"></script>

    <script>
        SDK.init({
            usePlatformScripts: true
        });
        
        SDK.ready(function () {
             // Register a listener for the work item page contribution.
            SDK.register(SDK.getContributionId(), function () {
                return {
                    // Called when the active work item is modified
                    onFieldChanged: function(args) {
                        
                    },
                    
                    // Called when a new work item is being loaded in the UI
                    onLoaded: function (args) {
            
                    },
                    
                    // Called when the active work item is being unloaded in the UI
                    onUnloaded: function (args) {
            
                    },
                    
                    // Called after the work item has been saved
                    onSaved: function (args) {
            
                    },
                    
                    // Called when the work item is reset to its unmodified state (undo)
                    onReset: function (args) {
            
                    },
                    
                    // Called when the work item has been refreshed from the server
                    onRefreshed: function (args) {
            
                    }
                }
            });    
        });
     </script>
</body>
</html>    
```

## Changes with New Boards Hub

> [!NOTE]
> The New Boards Hub feature is enabled by default. We strongly suggest that you test your internal extensions with the New Boards Hub to ensure compatibility.

### Use the latest SDKs

Make sure your extension is using the latest version of [azure-devops-extension-sdk](https://www.npmjs.com/package/azure-devops-extension-sdk)

When using the new SDK, you should also be using the [azure-devops-extension-api](https://www.npmjs.com/package/azure-devops-extension-api) package for REST APIs. We update the methods and interfaces every sprint to ensure it includes all of the latest features.

### When to use action or action-provider

Use `ms.vss-web.action-provider` when dynamically loading menu items using `getMenuItems` on the menu handler. Avoid using `ms.vss-web.action-provider` when your menu items are static and defined in your manifest. Instead `ms.vss-web.action` should be used.

### Package `require("VSS/Events/Document")` is no longer supported

`require("VSS/Events/Document")` import is no longer supported with the New Boards Hub.
