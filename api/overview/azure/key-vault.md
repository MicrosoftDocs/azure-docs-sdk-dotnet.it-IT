---
title: Librerie di Azure Key Vault per .NET
description: Informazioni di riferimento sulle librerie di Azure Key Vault per .NET
keywords: Azure, .NET, SDK, API, Key Vault
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: key-vault
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 037b80f60616a37665eddb0b7b212d15180700ba
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065451"
---
# <a name="azure-key-vault-libraries-for-net"></a><span data-ttu-id="61b5a-104">Librerie di Azure Key Vault per .NET</span><span class="sxs-lookup"><span data-stu-id="61b5a-104">Azure Key Vault libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="61b5a-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="61b5a-105">Overview</span></span>

<span data-ttu-id="61b5a-106">L'insieme di credenziali delle chiavi di Azure consente di proteggere le chiavi e i segreti di crittografia usati da servizi e applicazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="61b5a-106">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>

<span data-ttu-id="61b5a-107">Per altre informazioni, vedere [Informazioni su Key Vault](/azure/key-vault/key-vault-whatis), quindi [Introduzione ad Azure Key Vault](/azure/key-vault/key-vault-get-started) o [Usare Key Vault da un'app Web](/azure/key-vault/key-vault-use-from-web-application).</span><span class="sxs-lookup"><span data-stu-id="61b5a-107">Read more about [What is Key Vault?](/azure/key-vault/key-vault-whatis) then [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started) or learn how to [Use Key Vault from a web app](/azure/key-vault/key-vault-use-from-web-application).</span></span>

## <a name="client-library"></a><span data-ttu-id="61b5a-108">Libreria client</span><span class="sxs-lookup"><span data-stu-id="61b5a-108">Client library</span></span>

<span data-ttu-id="61b5a-109">Usare la libreria client per gestire le chiavi e gli asset correlati, ad esempio i certificati e i segreti.</span><span class="sxs-lookup"><span data-stu-id="61b5a-109">Use the client library to manage keys and related assets such as certificates and secrets.</span></span>

<span data-ttu-id="61b5a-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="61b5a-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="61b5a-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="61b5a-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a><span data-ttu-id="61b5a-112">Esempio</span><span class="sxs-lookup"><span data-stu-id="61b5a-112">Example</span></span>

<span data-ttu-id="61b5a-113">L'esempio seguente recupera il segreto per una chiave specifica identificata nelle impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="61b5a-113">The following example retrieves the secret for a specific key that is identified in the application settings.</span></span>

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="61b5a-114">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="61b5a-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a><span data-ttu-id="61b5a-115">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="61b5a-115">Management library</span></span>

<span data-ttu-id="61b5a-116">Usare la libreria di gestione per creare ed eliminare insiemi di credenziali delle chiavi ed eseguirvi query.</span><span class="sxs-lookup"><span data-stu-id="61b5a-116">Use the management library to create, delete, and query key vaults.</span></span>

<span data-ttu-id="61b5a-117">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="61b5a-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="61b5a-118">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="61b5a-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a><span data-ttu-id="61b5a-119">Esempio</span><span class="sxs-lookup"><span data-stu-id="61b5a-119">Example</span></span>

<span data-ttu-id="61b5a-120">L'esempio seguente illustra come creare un nuovo insieme di credenziali delle chiavi per un gruppo di risorse specifico e una posizione specifica.</span><span class="sxs-lookup"><span data-stu-id="61b5a-120">The following example demonstrates how to create a new key vault for a given resource group and location.</span></span>

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
> [<span data-ttu-id="61b5a-121">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="61b5a-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="61b5a-122">Esempi</span><span class="sxs-lookup"><span data-stu-id="61b5a-122">Samples</span></span>

* [<span data-ttu-id="61b5a-123">Scaricare gli esempi client di Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="61b5a-123">Download the Azure Key Vault client samples</span></span>](https://www.microsoft.com/download/details.aspx?id=45343)
* [<span data-ttu-id="61b5a-124">Introduzione alla crittografia lato client di Azure in .NET</span><span class="sxs-lookup"><span data-stu-id="61b5a-124">Getting Started with Azure Client Side Encryption in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)


<span data-ttu-id="61b5a-125">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="61b5a-125">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
