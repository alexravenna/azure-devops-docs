---
title: Connect to your Git repos using credential managers
titleSuffix: Azure Repos
description: Authenticate to Azure Repos using credential managers.
ms.assetid: 7779af87-460c-4078-bc2b-ceb4b758c24e
ms.service: azure-devops-repos
ms.topic: how-to
monikerRange: '<= azure-devops'
ms.subservice: azure-devops-repos-git
ms.date: 07/02/2025
ms.custom: sfi-image-nochange
---

# Use Git Credential Manager to authenticate to Azure Repos

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)]
[!INCLUDE [version-vs-gt-eq-2019](../../includes/version-vs-gt-eq-2019.md)]

Git Credential Manager simplifies authentication with your Azure Repos Git repositories. Credential managers let you use the same credentials that you use for the Azure DevOps web portal, supporting secure authentication through Microsoft account or Microsoft Entra ID with built-in multifactor authentication. Git Credential Manager also supports [two-factor authentication](https://help.github.com/articles/about-two-factor-authentication/) with GitHub repositories.

## Authentication options

Git Credential Manager supports multiple authentication methods, with Microsoft Entra ID tokens being the recommended approach for enhanced security:

- **Microsoft Entra ID tokens (recommended)**: Provides enhanced security with shorter token lifespans and better integration with organizational policies.
- **Microsoft account authentication**: Personal Microsoft accounts with multifactor authentication support.
- **Personal Access Tokens**: Available as an alternative, though we recommend using Microsoft Entra ID tokens when possible.

## IDE integration

Azure Repos provides IDE support for Microsoft account and Microsoft Entra authentication through the following clients:

- [Team Explorer in Visual Studio](../../organizations/projects/connect-to-projects.md)
- [IntelliJ and Android Studio with the Azure Repos Plugin for IntelliJ](/previous-versions/azure/devops/all/java/download-intellij-plug-in) 

If your environment doesn't have an integration available, you can configure your IDE with [Microsoft Entra ID tokens](../../integrate/get-started/authentication/entra.md) (recommended), [Personal Access Tokens](../../organizations/accounts/use-personal-access-tokens-to-authenticate.md), or [SSH](use-ssh-keys-to-authenticate.md) to connect to your repositories.

[!INCLUDE [use-microsoft-entra-reduce-pats](../../includes/use-microsoft-entra-reduce-pats.md)]

## Install Git Credential Manager

### Windows

Download and run the latest [Git for Windows installer](https://git-scm.com/download/win), which includes Git Credential Manager. Make sure to enable the Git Credential Manager installation option.

   ![Screenshot shows selection, Enable Git Credential Manager during Git for Windows install.](media/install-git-with-git-credential-manager.png) 

### macOS and Linux

You can [use SSH keys](use-ssh-keys-to-authenticate.md) to authenticate to Azure Repos, or use [Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager).

Installation instructions are included in the GitHub repository for GCM.
On Mac, we recommend using [Homebrew](https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/install.md#macos).
On Linux, you can install from a [.deb](https://github.com/GitCredentialManager/git-credential-manager#ubuntudebian-distributions) or a [tarball](https://github.com/GitCredentialManager/git-credential-manager#other-distributions).

## Using the Git Credential Manager

When you connect to a Git repository from your Git client for the first time, the credential manager prompts for credentials. Provide your Microsoft account or Microsoft Entra credentials. If your account has multifactor authentication enabled, the credential manager prompts you to go through that process as well.

![Git Credential Manager prompting during Git pull](media/gcm_login_prompt.gif)

Once authenticated, the credential manager creates and caches a token for future connections to the repo. Git commands that connect to this account don't prompt for user credentials until the token expires. A token can be revoked through Azure Repos.

### Configure Microsoft Entra ID authentication (recommended)

By default, GCM can request different types of authentication tokens from Azure Repos. You can [configure the default Git authentication](https://github.com/git-ecosystem/git-credential-manager/blob/main/docs/configuration.md#credentialazreposcredentialtype) to use [Microsoft Entra ID tokens](../../integrate/get-started/authentication/entra.md), which provide enhanced security through OAuth protocols. We recommend this approach for better security and integration with organizational policies. Learn more about [using GCM with Azure Repos](https://github.com/git-ecosystem/git-credential-manager/blob/main/docs/azrepos-users-and-tokens.md#set-default-credential-type).

```
git config --global credential.azreposCredentialType oauth
```

### Use service principal as authentication
You can also provide a [service principal](../../integrate/get-started/authentication/service-principal-managed-identity.md) for [authentication with GCM](https://github.com/git-ecosystem/git-credential-manager/blob/main/docs/configuration.md#credentialazreposserviceprincipal). Specify the client and tenant IDs of a service principal in this format: `{tenantId}/{clientId}`.

```
git config --global credential.azreposServicePrincipal "11111111-1111-1111-1111-111111111111/22222222-2222-2222-2222-222222222222"
```

You must also set at least one authentication mechanism if you set this value:
* [credential.azreposServicePrincipalSecret](https://github.com/git-ecosystem/git-credential-manager/blob/main/docs/configuration.md#credentialazreposserviceprincipalsecret)
* [credential.azreposServicePrincipalCertificateThumbprint](https://github.com/git-ecosystem/git-credential-manager/blob/main/docs/configuration.md#credentialazreposserviceprincipalcertificatethumbprint)
* [credential.azreposServicePrincipalCertificateSendX5C](https://github.com/git-ecosystem/git-credential-manager/blob/main/docs/configuration.md#credentialazreposserviceprincipalcertificatesendx5c)

## Get help

You can open and report issues with Git Credential Manager on the [project GitHub](https://github.com/GitCredentialManager/Git-Credential-Manager/issues).
