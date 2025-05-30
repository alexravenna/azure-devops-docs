---
title: Docker Content Trust in Azure Pipelines
description: Use Azure Pipelines to sign and push trusted images to container registries
ms.topic: quickstart
ms.assetid: b66517e3-85de-4847-82f6-b1b0431d2915
ms.author: ericvan
author: geekzter
ms.date: 05/21/2025
monikerRange: 'azure-devops'
---
# Docker Content Trust

[!INCLUDE [version-eq-azure-devops](../../../includes/version-eq-azure-devops.md)]

Docker Content Trust (DCT) lets you use digital signatures for data sent to and received from remote Docker registries. These signatures let you verify the integrity and publisher of specific image tags on the client side or at runtime.

> [!NOTE]
> To sign an image, you need a Docker Registry with an attached Notary server (examples include [Docker Hub](https://docs.docker.com/engine/security/trust/content_trust/) or [Azure Container Registry](/azure/container-registry/container-registry-content-trust)).

## Signing images in Azure Pipelines

### Prerequisites on the development machine

1. Use Docker trust's built-in generator or manually generate delegation key pair. If the [built-in generator](https://docs.docker.com/engine/security/trust/trust_delegation/#using-docker-trust-to-generate-keys) is used, the delegation private key is imported into the local Docker trust store. Otherwise, you need to manually import the private key into the local Docker trust store. See [Manually Generating Keys](https://docs.docker.com/engine/security/trust/trust_delegation/#manually-generating-keys) for details.
1. Use the delegation key generated in the previous step to upload the first key to a delegation and [initiate the repository](https://docs.docker.com/engine/security/trust/trust_delegation/#initiating-the-repository).

> [!Tip]
> To view the list of local Delegation keys, use the Notary CLI to run the following command: `$ notary key list`.

### Set up pipeline for signing images

1. Get the delegation private key from the local Docker trust store on your development machine, and add it as a [secure file](../../library/secure-files.md) in Pipelines.
2. [Authorize this secure file](../../library/secure-files.md#secure-file-authorization) for use in all pipelines.
3. The service principal associated with `containerRegistryServiceConnection` must have the AcrImageSigner role in the target container registry.
4. Create a pipeline based on the following YAML snippet:

   ```yaml
   pool:
     vmImage: 'ubuntu-latest'

   variables:
     system.debug: true
     containerRegistryServiceConnection: serviceConnectionName
     imageRepository: foobar/content-trust
     tag: test
    
   steps:
   - task: Docker@2
     inputs:
       command: login
       containerRegistry: $(containerRegistryServiceConnection)
    
   - task: DownloadSecureFile@1
     name: privateKey
     inputs:
       secureFile: cc8f3c6f998bee63fefaaabc5a2202eab06867b83f491813326481f56a95466f.key
   - script: |
       mkdir -p $(DOCKER_CONFIG)/trust/private
       cp $(privateKey.secureFilePath) $(DOCKER_CONFIG)/trust/private
    
   - task: Docker@2
     inputs:
       command: build
       Dockerfile: '**/Dockerfile'
       containerRegistry: $(containerRegistryServiceConnection)
       repository: $(imageRepository)
       tags: |
         $(tag)
    
    - task: Docker@2
      inputs:
        command: push
        containerRegistry: $(containerRegistryServiceConnection)
        repository: $(imageRepository)
        tags: |
          $(tag)
      env:
        DOCKER_CONTENT_TRUST_REPOSITORY_PASSPHRASE: $(DOCKER_CONTENT_TRUST_REPOSITORY_PASSPHRASE)
        DOCKER_CONTENT_TRUST_ROOT_PASSPHRASE: $(rootPassphrase)
   ```

   In the previous example, the `DOCKER_CONFIG` variable is set by the `login` command in the Docker task. Set up `DOCKER_CONTENT_TRUST_REPOSITORY_PASSPHRASE` and `DOCKER_CONTENT_TRUST_ROOT_PASSPHRASE` as [secret variables](../../process/variables.md#secret-variables) for your pipeline. 

    `DOCKER_CONTENT_TRUST_REPOSITORY_PASSPHRASE` in this example refers to the private key's passphrase (not the repository passphrase). We only need the private key's passphrase in this example because the repository has been initiated already (prerequisites).
