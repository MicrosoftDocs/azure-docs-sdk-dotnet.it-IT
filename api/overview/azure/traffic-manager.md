---
title: Librerie di Gestione traffico di Azure per .NET
description: Informazioni di riferimento sulle librerie di Gestione traffico di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: traffic-manager
ms.openlocfilehash: a75b5c566496f73475d24d62288a00c7d5775168
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190817"
---
# <a name="azure-traffic-manager-libraries-for-net"></a><span data-ttu-id="2ea60-103">Librerie di Gestione traffico di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="2ea60-103">Azure Traffic Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="2ea60-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2ea60-104">Overview</span></span>

<span data-ttu-id="2ea60-105">Gestione traffico di Microsoft Azure consente di controllare la distribuzione del traffico utente per gli endpoint di servizio in diversi data center.</span><span class="sxs-lookup"><span data-stu-id="2ea60-105">Microsoft Azure Traffic Manager allows you to control the distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="2ea60-106">Gli endpoint di servizio supportati da Gestione traffico includono servizi cloud, app Web e macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ea60-106">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="2ea60-107">È anche possibile usare Gestione traffico con endpoint esterni, non di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ea60-107">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="2ea60-108">Altre informazioni su [Gestione traffico di Azure](/azure/traffic-manager/traffic-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="2ea60-108">Learn more about [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>  

## <a name="management-library"></a><span data-ttu-id="2ea60-109">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="2ea60-109">Management library</span></span>

<span data-ttu-id="2ea60-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="2ea60-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2ea60-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="2ea60-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ea60-112">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="2ea60-112">Explore the management APIs</span></span>](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="2ea60-113">Esempi</span><span class="sxs-lookup"><span data-stu-id="2ea60-113">Samples</span></span>

<span data-ttu-id="2ea60-114">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="2ea60-114">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package