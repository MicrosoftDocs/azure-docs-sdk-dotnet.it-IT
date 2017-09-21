---
title: Librerie di Azure Key Vault per .NET
description: Informazioni di riferimento sulle librerie di Azure Key Vault per .NET
keywords: Azure, .NET, SDK, API, Key Vault
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 77a4e710e858bbeb98579a7b540b52b4cb9dd7b0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-key-vault-libraries-for-net"></a>Librerie di Azure Key Vault per .NET

## <a name="overview"></a>Panoramica

L'insieme di credenziali chiave di Azure consente di proteggere le chiavi e i segreti di crittografia usati da servizi e applicazioni cloud.

Per altre informazioni, vedere [Informazioni su Key Vault](/azure/key-vault/key-vault-whatis), quindi [Introduzione ad Azure Key Vault](/azure/key-vault/key-vault-get-started) o [Usare Key Vault da un'app Web](/azure/key-vault/key-vault-use-from-web-application).

## <a name="client-library"></a>Libreria client

Usare la libreria client per gestire le chiavi e gli asset correlati, ad esempio i certificati e i segreti.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a>Esempio

L'esempio seguente recupera il segreto per una chiave specifica identificata nelle impostazioni dell'applicazione.

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a>Libreria di gestione

Usare la libreria di gestione per creare ed eliminare insiemi di credenziali delle chiavi ed eseguirvi query.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a>Esempio

L'esempio seguente illustra come creare un nuovo insieme di credenziali delle chiavi per un gruppo di risorse specifico e una posizione specifica.

```csharp
using (KeyVaultManagementClient client = new KeyVaultManagementClient(
    new TokenCloudCredentials(subscriptionId, accessToken)))
{
    client.Vaults.CreateOrUpdate(resourceGroupName, "myKeyVault", new VaultCreateOrUpdateParameters
    {
        Properties = new VaultProperties
        {
            EnabledForDeployment = true,
            EnabledForDiskEncryption = true,
            EnabledForTemplateDeployment = true,
            Location = resourceGroupLocation,
            // SKU level, access policies, tenants, etc.
        }
    });
}
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a>Esempi

* [Scaricare gli esempi client di Azure Key Vault](https://www.microsoft.com/download/details.aspx?id=45343)
* [Introduzione alla crittografia lato client di Azure in .NET](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)


Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package