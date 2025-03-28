---
ms.subservice: azure-devops-security
ms.author: chcomley
author: chcomley
ms.topic: include
ms.date: 02/28/2022
---

 
The following table lists the permissions assigned at the organization or collection level. All permissions, except for **Make requests on behalf of others**, are granted to members of the **Project Collection Administrators** group. For more information, see [Permissions and groups reference, Groups](../permissions.md#collection-level).
 
:::row:::
   :::column span="":::
      **General**  
      - Alter trace settings  
      - Create new projects  
      - Delete team project  
      - Edit instance-level information
      - View instance-level information  

      **Service Account**
      - Make requests on behalf of others
      - Trigger events
      - View system synchronization information  

      **Boards**  
   :::column span="":::
      ::: moniker range="<=azure-devops"
      - Administer process permissions
      - Create process
      - Delete field from organization or account  
      - Delete process
      - Edit process
      ::: moniker-end
      
      
      **Repos** (TFVC)  
      - Administer shelved changes  
      - Administer workspaces  
      - Create a workspace  
   :::column-end:::
   :::column span="":::
      **Pipelines**  
      ::: moniker range="<=azure-devops"
      - Administer build resource permissions  
      - Manage build resources
      - Manage pipeline policies
      - Use build resources
      - View build resources
      ::: moniker-end
      
      **Test Plans**  
      - Manage test controllers  
      ::: moniker range="azure-devops"
      **Auditing**
      - Delete audit streams
      - Manage audit streams
      - View audit log
      ::: moniker-end
      ::: moniker range="<=azure-devops"
      **Policies**  
      - Manage enterprise policies
      ::: moniker-end
   :::column-end:::
:::row-end:::
 
