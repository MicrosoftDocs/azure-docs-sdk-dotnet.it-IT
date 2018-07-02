---
title: Librerie di Servizi multimediali di Azure per .NET
description: Informazioni di riferimento sulle librerie di Servizi multimediali di Azure per .NET
keywords: Azure, .NET, SDK, API, Servizi multimediali
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: media-services
ms.custom: devcenter, svc-overview
ms.openlocfilehash: ec6a7ec7f8f0c416d93aad5c91ece4d3b499fd7a
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065401"
---
# <a name="azure-media-services-libraries-for-net"></a><span data-ttu-id="d2dc1-104">Librerie di Servizi multimediali di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="d2dc1-104">Azure Media Services libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="d2dc1-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d2dc1-105">Overview</span></span>

<span data-ttu-id="d2dc1-106">Servizi multimediali di Microsoft Azure costituisce una piattaforma estensibile basata sul cloud che consente agli sviluppatori di creare applicazioni di distribuzione e gestione di contenuti multimediali altamente scalabili.</span><span class="sxs-lookup"><span data-stu-id="d2dc1-106">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers to build scalable media management and delivery applications.</span></span> <span data-ttu-id="d2dc1-107">Servizi multimediali si basa su API REST che consentono di caricare, archiviare e codificare contenuti video o audio in modo sicuro, nonché creare pacchetti di tali contenuti per la distribuzione in streaming live e on demand a vari client (ad esempio, TV, PC e dispositivi mobili).</span><span class="sxs-lookup"><span data-stu-id="d2dc1-107">Media Services is based on REST APIs that enable you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span> 

<span data-ttu-id="d2dc1-108">Per altre informazioni, vedere [Panoramica](/azure/media-services/media-services-overview) e [Introduzione a .NET](/azure/media-services/media-services-dotnet-how-to-use).</span><span class="sxs-lookup"><span data-stu-id="d2dc1-108">To learn more, see [Overview](/azure/media-services/media-services-overview) and [Getting started with .NET](/azure/media-services/media-services-dotnet-how-to-use).</span></span> 

## <a name="client-library"></a><span data-ttu-id="d2dc1-109">Libreria client</span><span class="sxs-lookup"><span data-stu-id="d2dc1-109">Client library</span></span>

<span data-ttu-id="d2dc1-110">La libreria Azure Media Services .NET SDK consente di programmare per Servizi multimediali usando .NET.</span><span class="sxs-lookup"><span data-stu-id="d2dc1-110">The Azure Media Services .NET SDK library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="d2dc1-111">Usare la libreria client di Servizi multimediali di Azure per la connessione, l'autenticazione e lo sviluppo nelle API di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="d2dc1-111">Use the Azure Media Services client library to connect, authenticate, and develop against Media Services APIs.</span></span>  

<span data-ttu-id="d2dc1-112">Per altre informazioni, vedere [Introduzione alla distribuzione di contenuti su richiesta utilizzando .NET SDK](/azure/media-services/media-services-dotnet-get-started).</span><span class="sxs-lookup"><span data-stu-id="d2dc1-112">For more information, see [Get started with delivering content on demand using .NET SDK](/azure/media-services/media-services-dotnet-get-started).</span></span>

<span data-ttu-id="d2dc1-113">Installare il [pacchetto NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="d2dc1-113">Install the [NuGet package](https://www.nuget.org/packages/windowsazure.mediaservices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d2dc1-114">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="d2dc1-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package windowsazure.mediaservices
```

### <a name="code-example"></a><span data-ttu-id="d2dc1-115">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="d2dc1-115">Code Example</span></span>

<span data-ttu-id="d2dc1-116">Il seguente codice usa l'SDK .NET di Servizi multimediali per eseguire le seguenti attività: </span><span class="sxs-lookup"><span data-stu-id="d2dc1-116">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="d2dc1-117">Creare un processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="d2dc1-117">Create an encoding job.</span></span>
- <span data-ttu-id="d2dc1-118">Ottenere un riferimento al codificatore Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="d2dc1-118">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="d2dc1-119">Specificare l'uso del set di impostazioni Flusso adattivo.</span><span class="sxs-lookup"><span data-stu-id="d2dc1-119">Specify to use the Adaptive Streaming preset.</span></span>
- <span data-ttu-id="d2dc1-120">Aggiungere una singola attività di codifica al processo.</span><span class="sxs-lookup"><span data-stu-id="d2dc1-120">Add a single encoding task to the job.</span></span>
- <span data-ttu-id="d2dc1-121">Specificare l’asset di input da codificare.</span><span class="sxs-lookup"><span data-stu-id="d2dc1-121">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="d2dc1-122">Creare un asset di output per la ricezione dell'asset codificato.</span><span class="sxs-lookup"><span data-stu-id="d2dc1-122">Create an output asset to receive the encoded asset.</span></span>
- <span data-ttu-id="d2dc1-123">Inviare il processo.</span><span class="sxs-lookup"><span data-stu-id="d2dc1-123">Submit the job.</span></span>


```csharp
/* Include this 'using' directive:
using Microsoft.WindowsAzure.MediaServices.Client;
*/

CloudMediaContext context = new CloudMediaContext(new Uri(mediaServiceRESTAPIEndpoint), tokenProvider);

// Get an uploaded asset.
IAsset asset = context.Assets.FirstOrDefault();

// Encode and generate the output using the "Adaptive Streaming" preset.
// Declare a new job.
IJob job = context.Jobs.Create("Media Encoder Standard Job");
// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = context.MediaProcessors.Where(p => p.Name == mediaProcessorName)
    .ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();
if (processor == null) 
{
    throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));
}

// Create a task with the encoding details, using a string preset.
// In this case "Adaptive Streaming" preset is used.
ITask task = job.Tasks.AddNew("My encoding task", processor, "Adaptive Streaming", TaskOptions.None);

// Specify the input asset to be encoded.
task.InputAssets.Add(asset);
// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);

job.Submit();
job.GetExecutionProgressTask(CancellationToken.None).Wait();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2dc1-124">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="d2dc1-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/mediaservices/client)

## <a name="samples"></a><span data-ttu-id="d2dc1-125">Esempi</span><span class="sxs-lookup"><span data-stu-id="d2dc1-125">Samples</span></span>

- [<span data-ttu-id="d2dc1-126">Trasmettere i contenuti HLS in modo protetto con Apple FairPlay</span><span class="sxs-lookup"><span data-stu-id="d2dc1-126">Stream your HLS content Protected with Apple FairPlay</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-dynamic-encryption-with-fairplay/)
- <span data-ttu-id="d2dc1-127">[Copy blob into an Azure Media Services asset using .NET SDK Extensions](https://azure.microsoft.com/resources/samples/media-services-dotnet-copy-blob-into-asset/) (Copiare un BLOB in un asset di Servizi multimediali di Azure usando le estensioni di .NET SDK)</span><span class="sxs-lookup"><span data-stu-id="d2dc1-127">[Copy blob into an Azure Media Services asset using .NET SDK Extensions](https://azure.microsoft.com/resources/samples/media-services-dotnet-copy-blob-into-asset/)</span></span>
- <span data-ttu-id="d2dc1-128">[Encode and Deliver a Live Stream with Azure Media Services using .NET SDK](https://azure.microsoft.com/resources/samples/media-services-dotnet-encode-live-stream-with-ams-clear/) (Codificare e distribuire un flusso live con Servizi multimediali di Azure tramite .NET SDK)</span><span class="sxs-lookup"><span data-stu-id="d2dc1-128">[Encode and Deliver a Live Stream with Azure Media Services using .NET SDK](https://azure.microsoft.com/resources/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)</span></span>

<span data-ttu-id="d2dc1-129">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services) degli esempi di codice per Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2dc1-129">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services) of Azure Media Services samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
