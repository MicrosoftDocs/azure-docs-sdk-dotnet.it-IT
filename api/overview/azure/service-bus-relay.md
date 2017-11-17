---
title: Librerie di Inoltro del bus di servizio di Azure per .NET
description: Informazioni di riferimento sulle librerie di Inoltro del bus di servizio di Azure per .NET
keywords: Azure, .NET, SDK, API, Inoltro del bus di servizio
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: service-bus
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 1a869d5939e357c98ec417e6474f711b9ac8c466
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2017
---
# <a name="azure-service-bus-relay-libraries-for-net"></a><span data-ttu-id="bb906-104">Librerie di Inoltro del bus di servizio di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="bb906-104">Azure Service Bus Relay libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="bb906-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="bb906-105">Overview</span></span>

<span data-ttu-id="bb906-106">Il servizio di inoltro di Azure crea applicazioni ibride consentendo di esporre in modo sicuro nel cloud pubblico i servizi che risiedono in una rete aziendale, senza dover aprire una connessione firewall o richiedere modifiche di notevole impatto a un'infrastruttura di rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="bb906-106">The Azure Relay service creates hybrid applications by enabling you to securely expose services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or require intrusive changes to a corporate network infrastructure.</span></span> <span data-ttu-id="bb906-107">Il servizio di inoltro supporta un'ampia gamma di protocolli di trasporto e standard dei servizi Web.</span><span class="sxs-lookup"><span data-stu-id="bb906-107">Relay supports a variety of different transport protocols and web services standards.</span></span>
          
<span data-ttu-id="bb906-108">Altre informazioni sul [servizio di inoltro di Azure](/azure/service-bus-relay/relay-what-is-it).</span><span class="sxs-lookup"><span data-stu-id="bb906-108">Learn more about [Azure Relay](/azure/service-bus-relay/relay-what-is-it).</span></span>

## <a name="client-library"></a><span data-ttu-id="bb906-109">Libreria client</span><span class="sxs-lookup"><span data-stu-id="bb906-109">Client library</span></span>

<span data-ttu-id="bb906-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Relay) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="bb906-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Relay) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="bb906-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="bb906-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb906-112">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="bb906-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a><span data-ttu-id="bb906-113">Esempi</span><span class="sxs-lookup"><span data-stu-id="bb906-113">Samples</span></span>

<span data-ttu-id="bb906-114">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="bb906-114">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package