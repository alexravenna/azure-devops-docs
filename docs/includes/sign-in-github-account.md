---
ms.topic: include
---

## Sign up with a GitHub account

> [!IMPORTANT]
> If your GitHub email address is associated with a Microsoft Entra ID-backed organization in Azure DevOps, you can't sign in with your GitHub account, rather you must sign in with your Microsoft Entra account.

1. Select the sign-up link for [Azure DevOps](https://azure.microsoft.com/services/devops/), **Start free with GitHub**. If you're already part of an Azure DevOps organization, select **Sign in to Azure DevOps**.

   ![Sign up for Azure DevOps](../media/azure-devops-start-free.png)

2. Select **Sign in with GitHub**.

   ![Select Sign in with GitHub](../media/sign-in-github.png)  

   If you have an account in session already, select **Use another account**. You're taken to GitHub sign-in where you can enter your GitHub user name or email address.

3. Enter your GitHub account credentials, and then select **Sign in**.

   ![Enter GitHub credentials](../media/enter-github-credentials.png)

4. Select **Authorize Microsoft corporation**.

   ![Authorize Microsoft](../media/authorize-Microsoft-corp.png)

5. To get started with Azure DevOps, select **Continue**.

   ![Choose Continue to sign up for Azure DevOps](../media/sign-up-azure-devops.png)

An organization is created based on the account you used to sign in. Sign in to your organization at any time, (`https://dev.azure.com/{yourorganization}`).

You can rename and delete your organization, or change the organization location. For more information, see [Manage organizations](../organizations/accounts/organization-management.md).

### Enable GitHub invitations

Creating a new Azure DevOps organization with your GitHub username turns on the Invite GitHub users policy by default. For existing organizations, your administrator can turn on this capability via **Organization settings** > **Policies** tab. 

Once the setting is changed, sign out of Azure DevOps, and then from a fresh browser session, sign back in to the organization `dev.azure.com/{organizationName}` or `organizationName.visualstudio.com` with your GitHub credentials. You're now recognized as a GitHub user and the GitHub invitation experience is available to you.

![Invite GitHub users policy ](../media/invite-github-users-policy.png)

For more information about GitHub authentication, see [Connect to GitHub/FAQs](../boards/github/connect-to-github.md#faqs).
