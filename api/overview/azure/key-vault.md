---
title: Librerie di Azure Key Vault per .NET
description: Informazioni di riferimento sulle librerie di Azure Key Vault per .NET
keywords: Azure, .NET, SDK, API, Key Vault
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: key-vault
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 3b8bcb9135794592f493db679e60fd40116d05e6
ms.sourcegitcommit: 4114b8821f20e02f4185fcea7549d716f29b9c90
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/24/2017
---
# <a name="azure-key-vault-libraries-for-net"></a><span data-ttu-id="0195e-104">Librerie di Azure Key Vault per .NET</span><span class="sxs-lookup"><span data-stu-id="0195e-104">Azure Key Vault libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="0195e-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0195e-105">Overview</span></span>

<span data-ttu-id="0195e-106">L'insieme di credenziali chiave di Azure consente di proteggere le chiavi e i segreti di crittografia usati da servizi e applicazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="0195e-106">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>

<span data-ttu-id="0195e-107">Per altre informazioni, vedere [Informazioni su Key Vault](/azure/key-vault/key-vault-whatis), quindi [Introduzione ad Azure Key Vault](/azure/key-vault/key-vault-get-started) o [Usare Key Vault da un'app Web](/azure/key-vault/key-vault-use-from-web-application).</span><span class="sxs-lookup"><span data-stu-id="0195e-107">Read more about [What is Key Vault?](/azure/key-vault/key-vault-whatis) then [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started) or learn how to [Use Key Vault from a web app](/azure/key-vault/key-vault-use-from-web-application).</span></span>

## <a name="client-library"></a><span data-ttu-id="0195e-108">Libreria client</span><span class="sxs-lookup"><span data-stu-id="0195e-108">Client library</span></span>

<span data-ttu-id="0195e-109">Usare la libreria client per gestire le chiavi e gli asset correlati, ad esempio i certificati e i segreti.</span><span class="sxs-lookup"><span data-stu-id="0195e-109">Use the client library to manage keys and related assets such as certificates and secrets.</span></span>

<span data-ttu-id="0195e-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="0195e-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0195e-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="0195e-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a><span data-ttu-id="0195e-112">Esempio</span><span class="sxs-lookup"><span data-stu-id="0195e-112">Example</span></span>

<span data-ttu-id="0195e-113">L'esempio seguente recupera il segreto per una chiave specifica identificata nelle impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0195e-113">The following example retrieves the secret for a specific key that is identified in the application settings.</span></span>

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0195e-114">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="0195e-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a><span data-ttu-id="0195e-115">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="0195e-115">Management library</span></span>

<span data-ttu-id="0195e-116">Usare la libreria di gestione per creare ed eliminare insiemi di credenziali delle chiavi ed eseguirvi query.</span><span class="sxs-lookup"><span data-stu-id="0195e-116">Use the management library to create, delete, and query key vaults.</span></span>

<span data-ttu-id="0195e-117">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="0195e-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0195e-118">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="0195e-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a><span data-ttu-id="0195e-119">Esempio</span><span class="sxs-lookup"><span data-stu-id="0195e-119">Example</span></span>

<span data-ttu-id="0195e-120">L'esempio seguente illustra come creare un nuovo insieme di credenziali delle chiavi per un gruppo di risorse specifico e una posizione specifica.</span><span class="sxs-lookup"><span data-stu-id="0195e-120">The following example demonstrates how to create a new key vault for a given resource group and location.</span></span>

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
> [<span data-ttu-id="0195e-121">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="0195e-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="0195e-122">Esempi</span><span class="sxs-lookup"><span data-stu-id="0195e-122">Samples</span></span>

* [<span data-ttu-id="0195e-123">Scaricare gli esempi client di Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="0195e-123">Download the Azure Key Vault client samples</span></span>](https://www.microsoft.com/download/details.aspx?id=45343)
* [<span data-ttu-id="0195e-124">Introduzione alla crittografia lato client di Azure in .NET</span><span class="sxs-lookup"><span data-stu-id="0195e-124">Getting Started with Azure Client Side Encryption in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)


<span data-ttu-id="0195e-125">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="0195e-125">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
