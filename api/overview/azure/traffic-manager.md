---
title: Librerie di Gestione traffico di Azure per .NET
description: Informazioni di riferimento sulle librerie di Gestione traffico di Azure per .NET
keywords: Azure, .NET, SDK, API, Gestione traffico
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: traffic-manager
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 491a8b12146882b32f7fc6d85ad58cca1d00fd04
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2017
---
# <a name="azure-traffic-manager-libraries-for-net"></a><span data-ttu-id="2ec97-104">Librerie di Gestione traffico di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="2ec97-104">Azure Traffic Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="2ec97-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2ec97-105">Overview</span></span>

<span data-ttu-id="2ec97-106">Gestione traffico di Microsoft Azure consente di controllare la distribuzione del traffico utente per gli endpoint di servizio in diversi data center.</span><span class="sxs-lookup"><span data-stu-id="2ec97-106">Microsoft Azure Traffic Manager allows you to control the distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="2ec97-107">Gli endpoint di servizio supportati da Gestione traffico includono servizi cloud, app Web e macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec97-107">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="2ec97-108">È anche possibile usare Gestione traffico con endpoint esterni, non di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec97-108">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="2ec97-109">Altre informazioni su [Gestione traffico di Azure](/azure/traffic-manager/traffic-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="2ec97-109">Learn more about [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>  

## <a name="management-library"></a><span data-ttu-id="2ec97-110">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="2ec97-110">Management library</span></span>

<span data-ttu-id="2ec97-111">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="2ec97-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2ec97-112">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="2ec97-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ec97-113">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="2ec97-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="2ec97-114">Esempi</span><span class="sxs-lookup"><span data-stu-id="2ec97-114">Samples</span></span>

<span data-ttu-id="2ec97-115">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="2ec97-115">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package