---
title: Librerie di Inoltro del bus di servizio di Azure per .NET
description: Informazioni di riferimento sulle librerie di Inoltro del bus di servizio di Azure per .NET
keywords: Azure, .NET, SDK, API, Inoltro del bus di servizio
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/14/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 13a875b837648a05401453e975c9cd70d5e203a1
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-service-bus-relay-libraries-for-net"></a><span data-ttu-id="9549b-104">Librerie di Inoltro del bus di servizio di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="9549b-104">Azure Service Bus Relay libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="9549b-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9549b-105">Overview</span></span>

<span data-ttu-id="9549b-106">Il servizio di inoltro di Azure crea applicazioni ibride consentendo di esporre in modo sicuro nel cloud pubblico i servizi che risiedono in una rete aziendale, senza dover aprire una connessione firewall o richiedere modifiche di notevole impatto a un'infrastruttura di rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="9549b-106">The Azure Relay service creates hybrid applications by enabling you to securely expose services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or require intrusive changes to a corporate network infrastructure.</span></span> <span data-ttu-id="9549b-107">Il servizio di inoltro supporta un'ampia gamma di protocolli di trasporto e standard dei servizi Web.</span><span class="sxs-lookup"><span data-stu-id="9549b-107">Relay supports a variety of different transport protocols and web services standards.</span></span>
          
<span data-ttu-id="9549b-108">Altre informazioni sul [servizio di inoltro di Azure](https://docs.microsoft.com/en-us/azure/service-bus-relay/relay-what-is-it).</span><span class="sxs-lookup"><span data-stu-id="9549b-108">Learn more about [Azure Relay](https://docs.microsoft.com/en-us/azure/service-bus-relay/relay-what-is-it).</span></span>

## <a name="client-library"></a><span data-ttu-id="9549b-109">Libreria client</span><span class="sxs-lookup"><span data-stu-id="9549b-109">Client library</span></span>

<span data-ttu-id="9549b-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Relay) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="9549b-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Relay) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9549b-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="9549b-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9549b-112">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="9549b-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a><span data-ttu-id="9549b-113">Esempi</span><span class="sxs-lookup"><span data-stu-id="9549b-113">Samples</span></span>

<span data-ttu-id="9549b-114">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="9549b-114">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package