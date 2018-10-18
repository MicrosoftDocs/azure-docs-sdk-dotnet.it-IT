---
title: Librerie di Inoltro del bus di servizio di Azure per .NET
description: Informazioni di riferimento sulle librerie di Inoltro del bus di servizio di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-bus-relay
ms.openlocfilehash: 9190e8efdebe1c352b4fb2c98be189089b0975d2
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348123"
---
# <a name="azure-service-bus-relay-libraries-for-net"></a><span data-ttu-id="979c0-103">Librerie di Inoltro del bus di servizio di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="979c0-103">Azure Service Bus Relay libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="979c0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="979c0-104">Overview</span></span>

<span data-ttu-id="979c0-105">Il servizio di inoltro di Azure crea applicazioni ibride consentendo di esporre in modo sicuro nel cloud pubblico i servizi che risiedono in una rete aziendale, senza dover aprire una connessione firewall o richiedere modifiche di notevole impatto a un'infrastruttura di rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="979c0-105">The Azure Relay service creates hybrid applications by enabling you to securely expose services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or require intrusive changes to a corporate network infrastructure.</span></span> <span data-ttu-id="979c0-106">Il servizio di inoltro supporta un'ampia gamma di protocolli di trasporto e standard dei servizi Web.</span><span class="sxs-lookup"><span data-stu-id="979c0-106">Relay supports a variety of different transport protocols and web services standards.</span></span>
          
<span data-ttu-id="979c0-107">Altre informazioni sul [servizio di inoltro di Azure](/azure/service-bus-relay/relay-what-is-it).</span><span class="sxs-lookup"><span data-stu-id="979c0-107">Learn more about [Azure Relay](/azure/service-bus-relay/relay-what-is-it).</span></span>

## <a name="client-library"></a><span data-ttu-id="979c0-108">Libreria client</span><span class="sxs-lookup"><span data-stu-id="979c0-108">Client library</span></span>

<span data-ttu-id="979c0-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Relay) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="979c0-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Relay) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="979c0-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="979c0-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="979c0-111">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="979c0-111">Explore the client APIs</span></span>](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a><span data-ttu-id="979c0-112">Esempi</span><span class="sxs-lookup"><span data-stu-id="979c0-112">Samples</span></span>

<span data-ttu-id="979c0-113">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="979c0-113">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package