---
title: Librerie di Azure Application Insights per .NET
description: Informazioni di riferimento sulle librerie di Azure Application Insights per .NET
keywords: Azure, .NET, SDK, API, Application AppInsights
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: application-insights
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 081143eafaeea2954703c337609a67fd5a7941c6
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2017
---
# <a name="azure-application-insights-libraries-for-net"></a><span data-ttu-id="acfda-104">Librerie di Azure Application Insights per .NET</span><span class="sxs-lookup"><span data-stu-id="acfda-104">Azure Application Insights libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="acfda-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="acfda-105">Overview</span></span>

<span data-ttu-id="acfda-106">Application Insights è un servizio estendibile di monitoraggio e diagnostica per gli sviluppatori Web che offre funzionalità avanzate di analisi ad-hoc.</span><span class="sxs-lookup"><span data-stu-id="acfda-106">Application Insights is an extensible monitoring & diagnostics service for web developers with powerful ad-hoc analytics capabilities.</span></span> <span data-ttu-id="acfda-107">È possibile usare le classi dello spazio dei nomi ApplicationInsights per configurare la raccolta di dati di telemetria e inviare eventuali dati di telemetria personalizzati dalle applicazioni da monitorare.</span><span class="sxs-lookup"><span data-stu-id="acfda-107">You can use the classes in the ApplicationInsights namespace to configure telemetry collection and send any custom telemetry from your applications that you want to monitor.</span></span>

## <a name="client-library"></a><span data-ttu-id="acfda-108">Libreria client</span><span class="sxs-lookup"><span data-stu-id="acfda-108">Client library</span></span>

<span data-ttu-id="acfda-109">L'SDK client di Application Insights per .NET consente di registrare eventi, dati aggregati, eccezioni, dipendenze e metriche in Azure per analisi future.</span><span class="sxs-lookup"><span data-stu-id="acfda-109">The Application Insights client SDK for .NET allows you to log event, aggregated data, exceptions, dependency, and metrics to Azure for future analysis.</span></span>

<span data-ttu-id="acfda-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="acfda-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="acfda-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="acfda-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a><span data-ttu-id="acfda-112">Esempio</span><span class="sxs-lookup"><span data-stu-id="acfda-112">Example</span></span>

<span data-ttu-id="acfda-113">Questo esempio tiene traccia di un evento personalizzato in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="acfda-113">This example tracks a custom event to Application Insights.</span></span>

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="acfda-114">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="acfda-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a><span data-ttu-id="acfda-115">Esempi</span><span class="sxs-lookup"><span data-stu-id="acfda-115">Samples</span></span>

- <span data-ttu-id="acfda-116">[Application Insights Analytics with OpenSchema](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/) (Analisi di Application Insights con OpenSchema)</span><span class="sxs-lookup"><span data-stu-id="acfda-116">[Application Insights Analytics with OpenSchema](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)</span></span>

<span data-ttu-id="acfda-117">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) degli esempi di codice per Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="acfda-117">View the [complete list](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) of Azure Application Insights samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
