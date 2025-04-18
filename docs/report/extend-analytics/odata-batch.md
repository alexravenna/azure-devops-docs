---
title: OData batch support 
titleSuffix: Azure DevOps 
description: Learn how to write good OData queries for Analytics for Azure DevOps.
ms.subservice: azure-devops-analytics
ms.reviewer: desalg
ms.author: chcomley
author: chcomley
ms.topic: conceptual
monikerRange: "<=azure-devops"
ms.date: 09/30/2020
---

# OData batch support

[!INCLUDE [version-gt-eq-2019](../../includes/version-gt-eq-2019.md)]

Batch requests are part of the OData spec. Analytics for Azure DevOps provides limited support, as a means to submit large requests. For more information about batch operations in OData, see section [11.7 Batch Requests](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752313) of the OData spec.

[!INCLUDE [temp](../includes/analytics-preview.md)]

## The Analytics $batch endpoint

The $batch endpoint is located at:

::: moniker range="azure-devops"

> [!div class="tabbedCodeSnippets"]
> ```OData
>  https://analytics.dev.azure.com/{OrganizationName}/_odata/{version}/$batch
> ``` 
> 
> [!NOTE]
> The $batch endpoint is not available with a project scope, but the queries within a batch can contain project scoping.

::: moniker-end

::: moniker range="<azure-devops"

> [!div class="tabbedCodeSnippets"]
> ```OData
> https://{servername}:{port}/tfs/{OrganizationName}/_odata/{version}/$batch
> ```
> 
> [!NOTE]
> The examples shown in this document are based on an Azure DevOps Services URL, you will need to substitute in your Azure DevOps Server URL.
> The $batch endpoint is not available with a project scope, but the queries within a batch can contain project scoping.

::: moniker-end

### Supported $batch operations

The OData spec allows for many operations per $batch request, however Analytics limits each $batch request to a single query. The Analytics $batch endpoint is also read-only, no change sets may be published to it.

### When to use $batch queries

Use $batch requests when you are in danger of exceeding the browser's limit on URL length. Many modern browsers have these limits and exceeding them can result in undesirable behavior. Using a $batch request allows long queries to be issued against Analytics as the OData query is delivered in a POST body. You may use $batch requests for all your queries, though GET requests are slightly faster.

## $batch example

### Request

URL: ```https://analytics.dev.azure.com/{OrganizationName}/_odata/{version}/$batch```  
Content-Type: ```multipart/mixed; boundary=batch_2af9a11e-9dec-4266-a3ab-0db9d10fb55a```  
Request payload:
```
--batch_1af9a11e-9dec-4266-a3ab-0db9d10fb55a
Content-Type: application/http
Content-Transfer-Encoding: binary

GET https://{OrganizationName}.analytics.vsts.me/_odata/{version}/Users?$filter=UserEmail eq 'john.smith@contoso.com'&$select=UserId,UserSK,UserName HTTP/1.1
Accept: application/json

--batch_1af9a11e-9dec-4266-a3ab-0db9d10fb55a
```

### Response

Status code: ```200```  
Response body:  
```
--batchresponse_0cc7749e-dcec-4b5e-9380-eb05859fe733
Content-Type: application/http
Content-Transfer-Encoding: binary

HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
OData-Version: 4.0

{"@odata.context":"https://{OrganizationName}.analytics.vsts.me/_odata/{version}/$metadata#Users(UserId,UserSK,UserName)","value":[{"UserId":"00aa00aa-bb11-cc22-dd33-44ee44ee44ee","UserSK":"00aa00aa-bb11-cc22-dd33-44ee44ee44ee","UserName":"John Smith"}]}
--batchresponse_0cc7749e-dcec-4b5e-9380-eb05859fe733--
```
