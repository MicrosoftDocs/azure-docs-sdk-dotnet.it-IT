---
title: Librerie di Azure Key Vault per .NET
description: Informazioni di riferimento sulle librerie di Azure Key Vault per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: key-vault
ms.openlocfilehash: a42eb9684bcfb8e8d2209235f61bbf6962cf5e9e
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190554"
---
# <a name="azure-key-vault-libraries-for-net"></a><span data-ttu-id="b040f-103">Librerie di Azure Key Vault per .NET</span><span class="sxs-lookup"><span data-stu-id="b040f-103">Azure Key Vault libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="b040f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b040f-104">Overview</span></span>

<span data-ttu-id="b040f-105">L'insieme di credenziali delle chiavi di Azure consente di proteggere le chiavi e i segreti di crittografia usati da servizi e applicazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="b040f-105">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>

<span data-ttu-id="b040f-106">Per altre informazioni, vedere [Informazioni su Key Vault](/azure/key-vault/key-vault-whatis), quindi [Introduzione ad Azure Key Vault](/azure/key-vault/key-vault-get-started) o [Usare Key Vault da un'app Web](/azure/key-vault/key-vault-use-from-web-application).</span><span class="sxs-lookup"><span data-stu-id="b040f-106">Read more about [What is Key Vault?](/azure/key-vault/key-vault-whatis) then [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started) or learn how to [Use Key Vault from a web app](/azure/key-vault/key-vault-use-from-web-application).</span></span>

## <a name="client-library"></a><span data-ttu-id="b040f-107">Libreria client</span><span class="sxs-lookup"><span data-stu-id="b040f-107">Client library</span></span>

<span data-ttu-id="b040f-108">Usare la libreria client per gestire le chiavi e gli asset correlati, ad esempio i certificati e i segreti.</span><span class="sxs-lookup"><span data-stu-id="b040f-108">Use the client library to manage keys and related assets such as certificates and secrets.</span></span>

<span data-ttu-id="b040f-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="b040f-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="b040f-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="b040f-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a><span data-ttu-id="b040f-111">Esempio</span><span class="sxs-lookup"><span data-stu-id="b040f-111">Example</span></span>

<span data-ttu-id="b040f-112">L'esempio seguente recupera il segreto per una chiave specifica identificata nelle impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b040f-112">The following example retrieves the secret for a specific key that is identified in the application settings.</span></span>

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="b040f-113">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="b040f-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a><span data-ttu-id="b040f-114">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="b040f-114">Management library</span></span>

<span data-ttu-id="b040f-115">Usare la libreria di gestione per creare ed eliminare insiemi di credenziali delle chiavi ed eseguirvi query.</span><span class="sxs-lookup"><span data-stu-id="b040f-115">Use the management library to create, delete, and query key vaults.</span></span>

<span data-ttu-id="b040f-116">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="b040f-116">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="b040f-117">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="b040f-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a><span data-ttu-id="b040f-118">Esempio</span><span class="sxs-lookup"><span data-stu-id="b040f-118">Example</span></span>

<span data-ttu-id="b040f-119">L'esempio seguente illustra come creare un nuovo insieme di credenziali delle chiavi per un gruppo di risorse specifico e una posizione specifica.</span><span class="sxs-lookup"><span data-stu-id="b040f-119">The following example demonstrates how to create a new key vault for a given resource group and location.</span></span>

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
> [<span data-ttu-id="b040f-120">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="b040f-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="b040f-121">Esempi</span><span class="sxs-lookup"><span data-stu-id="b040f-121">Samples</span></span>

* [<span data-ttu-id="b040f-122">Scaricare gli esempi client di Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="b040f-122">Download the Azure Key Vault client samples</span></span>](https://www.microsoft.com/download/details.aspx?id=45343)
* [<span data-ttu-id="b040f-123">Introduzione alla crittografia lato client di Azure in .NET</span><span class="sxs-lookup"><span data-stu-id="b040f-123">Getting Started with Azure Client Side Encryption in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)


<span data-ttu-id="b040f-124">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="b040f-124">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
