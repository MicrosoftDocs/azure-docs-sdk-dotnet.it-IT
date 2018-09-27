---
title: Librerie di Analisi di flusso di Azure per .NET
description: Informazioni di riferimento sulle librerie di Analisi di flusso di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: stream-analytics
ms.openlocfilehash: c04a5c8a7b1d7e0f283d4fb81bd772de24f195eb
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190454"
---
# <a name="azure-stream-analytics-libraries-for-net"></a><span data-ttu-id="dba16-103">Librerie di Analisi di flusso di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="dba16-103">Azure Stream Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="dba16-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="dba16-104">Overview</span></span>

<span data-ttu-id="dba16-105">[Analisi di flusso di Azure](/azure/stream-analytics/stream-analytics-introduction) è un motore di elaborazione di eventi completamente gestito che consente di configurare calcoli di analisi in tempo reale sui dati di streaming.</span><span class="sxs-lookup"><span data-stu-id="dba16-105">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) is a fully managed event-processing engine that lets you set up real-time analytic computations on streaming data.</span></span> <span data-ttu-id="dba16-106">I dati possono provenire da dispositivi, sensori, siti Web, feed di social media, applicazioni, sistemi di infrastruttura e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="dba16-106">The data can come from devices, sensors, web sites, social media feeds, applications, infrastructure systems, and more.</span></span> 

<span data-ttu-id="dba16-107">Per altre informazioni su Analisi di flusso di Azure, vedere [Introduzione al rilevamento di illeciti in tempo reale con Analisi di flusso di Azure](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).</span><span class="sxs-lookup"><span data-stu-id="dba16-107">To learn more about Azure Stream Analytics, see [Get started with Azure Stream Analytics Real-time fraud detection](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).</span></span>


## <a name="management-library"></a><span data-ttu-id="dba16-108">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="dba16-108">Management library</span></span>

<span data-ttu-id="dba16-109">Usare la libreria di gestione di Analisi di flusso di Azure per creare, avviare e arrestare processi di Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="dba16-109">Use the Azure Stream Analytics management library to create, start, and stop Azure Stream Analytics jobs.</span></span>

<span data-ttu-id="dba16-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="dba16-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="dba16-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="dba16-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.StreamAnalytics
```

```bash
dotnet add package Microsoft.Azure.Management.StreamAnalytics
```

### <a name="code-example"></a><span data-ttu-id="dba16-112">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="dba16-112">Code Example</span></span>

<span data-ttu-id="dba16-113">Questo esempio crea istanze di un client di Analisi di flusso e crea un processo di streaming.</span><span class="sxs-lookup"><span data-stu-id="dba16-113">This example instantiates a Stream Analytics client and creates a streaming job.</span></span>

```csharp
/* Include these 'using' directives:
using Microsoft.Azure.Management.StreamAnalytics;
*/
SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

// Get credentials
ServiceClientCredentials credentials = GetCredentials().Result;

// Create Stream Analytics management client
StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
{
    SubscriptionId = subscriptionId
};

// Create a streaming job
StreamingJob streamingJob = new StreamingJob()
{
    Tags = new Dictionary<string, string>()
    {
        { "Origin", ".NET SDK" },
        { "ReasonCreated", "Getting started tutorial" }
    },
    Location = "West US",
    EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
    EventsOutOfOrderMaxDelayInSeconds = 5,
    EventsLateArrivalMaxDelayInSeconds = 16,
    OutputErrorPolicy = OutputErrorPolicy.Drop,
    DataLocale = "en-US",
    CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
    Sku = new Sku()
    {
        Name = SkuName.Standard
    }
};
StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="dba16-114">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="dba16-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/streamanalytics/management)


## <a name="samples"></a><span data-ttu-id="dba16-115">Esempi</span><span class="sxs-lookup"><span data-stu-id="dba16-115">Samples</span></span>

- [<span data-ttu-id="dba16-116">Management .NET SDK: impostare ed eseguire processi di analisi tramite l'API di Analisi di flusso di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="dba16-116">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

<span data-ttu-id="dba16-117">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) degli esempi di codice per Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="dba16-117">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) of Azure Stream Analytics samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
