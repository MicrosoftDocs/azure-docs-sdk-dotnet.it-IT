---
title: Librerie di DNS di Azure per .NET
description: Informazioni di riferimento sulle librerie di DNS di Azure per .NET
keywords: Azure, .NET, SDK, API, DNS
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 57c578f12ea426dc5784658338473f0044d21e5c
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-dns-libraries-for-net"></a><span data-ttu-id="6b7b4-104">Librerie di DNS di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="6b7b4-104">Azure DNS libraries for .NET</span></span>

<span data-ttu-id="6b7b4-105">Usare le librerie di DNS Microsoft Azure per .NET per creare e modificare le zone e i record DNS ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="6b7b4-105">Use the Microsoft Azure DNS libraries for .NET to create and modify DNS zones and records hosted within Azure.</span></span> <span data-ttu-id="6b7b4-106">Le zone e i record vengono gestiti come risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b7b4-106">Zones and records are managed as Azure Resources.</span></span> <span data-ttu-id="6b7b4-107">Per altre informazioni, vedere [Panoramica di DNS di Azure](/azure/dns/dns-overview).</span><span class="sxs-lookup"><span data-stu-id="6b7b4-107">Learn more by reading the [Azure DNS overview](/azure/dns/dns-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="6b7b4-108">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="6b7b4-108">Management library</span></span>

<span data-ttu-id="6b7b4-109">Usare la libreria di gestione per creare e modificare le zone e i record DNS ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="6b7b4-109">Use the management library to create and modify DNS zones and records that are hosted in Azure.</span></span>

<span data-ttu-id="6b7b4-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6b7b4-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6b7b4-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="6b7b4-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a><span data-ttu-id="6b7b4-112">Esempio</span><span class="sxs-lookup"><span data-stu-id="6b7b4-112">Example</span></span>

<span data-ttu-id="6b7b4-113">L'esempio seguente crea una nuova zona DNS.</span><span class="sxs-lookup"><span data-stu-id="6b7b4-113">The following example creates a new DNS zone.</span></span>

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
> [<span data-ttu-id="6b7b4-114">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="6b7b4-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a><span data-ttu-id="6b7b4-115">Esempi</span><span class="sxs-lookup"><span data-stu-id="6b7b4-115">Samples</span></span>

* [<span data-ttu-id="6b7b4-116">Progetto di esempio di Azure DNS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6b7b4-116">Azure DNS .NET SDK Sample Project</span></span>](https://www.microsoft.com/download/details.aspx?id=47268)

<span data-ttu-id="6b7b4-117">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="6b7b4-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
