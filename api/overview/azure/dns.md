---
title: Librerie di DNS di Azure per .NET
description: Informazioni di riferimento sulle librerie di DNS di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: dns
ms.openlocfilehash: b9ab6359aaa1e4e9b6e99e7a7b007928d18f3453
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190194"
---
# <a name="azure-dns-libraries-for-net"></a><span data-ttu-id="ac1e9-103">Librerie di DNS di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="ac1e9-103">Azure DNS libraries for .NET</span></span>

<span data-ttu-id="ac1e9-104">Usare le librerie di DNS Microsoft Azure per .NET per creare e modificare le zone e i record DNS ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="ac1e9-104">Use the Microsoft Azure DNS libraries for .NET to create and modify DNS zones and records hosted within Azure.</span></span> <span data-ttu-id="ac1e9-105">Le zone e i record vengono gestiti come risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac1e9-105">Zones and records are managed as Azure Resources.</span></span> <span data-ttu-id="ac1e9-106">Per altre informazioni, vedere [Panoramica di DNS di Azure](/azure/dns/dns-overview).</span><span class="sxs-lookup"><span data-stu-id="ac1e9-106">Learn more by reading the [Azure DNS overview](/azure/dns/dns-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="ac1e9-107">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="ac1e9-107">Management library</span></span>

<span data-ttu-id="ac1e9-108">Usare la libreria di gestione per creare e modificare le zone e i record DNS ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="ac1e9-108">Use the management library to create and modify DNS zones and records that are hosted in Azure.</span></span>

<span data-ttu-id="ac1e9-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="ac1e9-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ac1e9-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="ac1e9-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a><span data-ttu-id="ac1e9-111">Esempio</span><span class="sxs-lookup"><span data-stu-id="ac1e9-111">Example</span></span>

<span data-ttu-id="ac1e9-112">L'esempio seguente crea una nuova zona DNS.</span><span class="sxs-lookup"><span data-stu-id="ac1e9-112">The following example creates a new DNS zone.</span></span>

```csharp
/*
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
*/
Microsoft.Rest.ServiceClientCredentials serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
DnsManagementClient dnsClient = new DnsManagementClient(serviceCreds);            
Zone dnsZoneParams = new Zone("global");
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");
Zone dnsZone =
    await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac1e9-113">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="ac1e9-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a><span data-ttu-id="ac1e9-114">Esempi</span><span class="sxs-lookup"><span data-stu-id="ac1e9-114">Samples</span></span>

* [<span data-ttu-id="ac1e9-115">Progetto di esempio di Azure DNS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ac1e9-115">Azure DNS .NET SDK Sample Project</span></span>](https://www.microsoft.com/download/details.aspx?id=47268)

<span data-ttu-id="ac1e9-116">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="ac1e9-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
