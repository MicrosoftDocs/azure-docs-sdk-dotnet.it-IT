---
title: Librerie di Azure Application Insights per .NET
description: Informazioni di riferimento sulle librerie di Azure Application Insights per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: application-insights
ms.openlocfilehash: 10b65f536c6461959b0be9b8f9bd3ec56a307bea
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190836"
---
# <a name="azure-application-insights-libraries-for-net"></a><span data-ttu-id="72e55-103">Librerie di Azure Application Insights per .NET</span><span class="sxs-lookup"><span data-stu-id="72e55-103">Azure Application Insights libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="72e55-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="72e55-104">Overview</span></span>

<span data-ttu-id="72e55-105">Application Insights è un servizio estendibile di monitoraggio e diagnostica per gli sviluppatori Web che offre funzionalità avanzate di analisi ad-hoc.</span><span class="sxs-lookup"><span data-stu-id="72e55-105">Application Insights is an extensible monitoring & diagnostics service for web developers with powerful ad-hoc analytics capabilities.</span></span> <span data-ttu-id="72e55-106">È possibile usare le classi dello spazio dei nomi ApplicationInsights per configurare la raccolta di dati di telemetria e inviare eventuali dati di telemetria personalizzati dalle applicazioni da monitorare.</span><span class="sxs-lookup"><span data-stu-id="72e55-106">You can use the classes in the ApplicationInsights namespace to configure telemetry collection and send any custom telemetry from your applications that you want to monitor.</span></span>

## <a name="client-library"></a><span data-ttu-id="72e55-107">Libreria client</span><span class="sxs-lookup"><span data-stu-id="72e55-107">Client library</span></span>

<span data-ttu-id="72e55-108">L'SDK client di Application Insights per .NET consente di registrare eventi, dati aggregati, eccezioni, dipendenze e metriche in Azure per analisi future.</span><span class="sxs-lookup"><span data-stu-id="72e55-108">The Application Insights client SDK for .NET allows you to log event, aggregated data, exceptions, dependency, and metrics to Azure for future analysis.</span></span>

<span data-ttu-id="72e55-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="72e55-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="72e55-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="72e55-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a><span data-ttu-id="72e55-111">Esempio</span><span class="sxs-lookup"><span data-stu-id="72e55-111">Example</span></span>

<span data-ttu-id="72e55-112">Questo esempio tiene traccia di un evento personalizzato in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="72e55-112">This example tracks a custom event to Application Insights.</span></span>

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="72e55-113">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="72e55-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a><span data-ttu-id="72e55-114">Esempi</span><span class="sxs-lookup"><span data-stu-id="72e55-114">Samples</span></span>

- <span data-ttu-id="72e55-115">[Application Insights Analytics with OpenSchema](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/) (Analisi di Application Insights con OpenSchema)</span><span class="sxs-lookup"><span data-stu-id="72e55-115">[Application Insights Analytics with OpenSchema](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)</span></span>

<span data-ttu-id="72e55-116">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) degli esempi di codice per Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="72e55-116">View the [complete list](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) of Azure Application Insights samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
