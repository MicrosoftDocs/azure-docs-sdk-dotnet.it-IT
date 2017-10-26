---
title: Librerie di Servizi multimediali di Azure per .NET
description: Informazioni di riferimento sulle librerie di Servizi multimediali di Azure per .NET
keywords: Azure, .NET, SDK, API, Servizi multimediali
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: media-services
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 872ed60363c0c886e9844d0cb0bef07cf41a0242
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2017
---
# <a name="azure-media-services-libraries-for-net"></a>Librerie di Servizi multimediali di Azure per .NET

## <a name="overview"></a>Panoramica

Servizi multimediali di Microsoft Azure costituisce una piattaforma estensibile basata sul cloud che consente agli sviluppatori di creare applicazioni di distribuzione e gestione di contenuti multimediali altamente scalabili. Servizi multimediali si basa su API REST che consentono di caricare, archiviare e codificare contenuti video o audio in modo sicuro, nonché creare pacchetti di tali contenuti per la distribuzione in streaming live e on demand a vari client (ad esempio, TV, PC e dispositivi mobili). 

Per altre informazioni, vedere [Panoramica](/azure/media-services/media-services-overview) e [Introduzione a .NET](/azure/media-services/media-services-dotnet-how-to-use). 

## <a name="client-library"></a>Libreria client

La libreria Azure Media Services .NET SDK consente di programmare per Servizi multimediali usando .NET. Usare la libreria client di Servizi multimediali di Azure per la connessione, l'autenticazione e lo sviluppo nelle API di Servizi multimediali.  

Per altre informazioni, vedere [Introduzione alla distribuzione di contenuti su richiesta utilizzando .NET SDK](/azure/media-services/media-services-dotnet-get-started).

Installare il [pacchetto NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package windowsazure.mediaservices
```

### <a name="code-example"></a>Esempio di codice

Il seguente codice usa l'SDK .NET di Servizi multimediali per eseguire le seguenti attività: 

- Creare un processo di codifica.
- Ottenere un riferimento al codificatore Media Encoder Standard.
- Specificare l'uso del set di impostazioni Flusso adattivo.
- Aggiungere una singola attività di codifica al processo.
- Specificare l’asset di input da codificare.
- Creare un asset di output per la ricezione dell'asset codificato.
- Inviare il processo.


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
> [Esplorare le API client](/dotnet/api/overview/azure/mediaservices/client)

## <a name="samples"></a>Esempi

- [Trasmettere i contenuti HLS in modo protetto con Apple FairPlay](https://azure.microsoft.com/resources/samples/media-services-dotnet-dynamic-encryption-with-fairplay/)
- [Copy blob into an Azure Media Services asset using .NET SDK Extensions](https://azure.microsoft.com/resources/samples/media-services-dotnet-copy-blob-into-asset/) (Copiare un BLOB in un asset di Servizi multimediali di Azure usando le estensioni di .NET SDK)
- [Encode and Deliver a Live Stream with Azure Media Services using .NET SDK](https://azure.microsoft.com/resources/samples/media-services-dotnet-encode-live-stream-with-ams-clear/) (Codificare e distribuire un flusso live con Servizi multimediali di Azure tramite .NET SDK)

Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services) degli esempi di codice per Servizi multimediali di Azure.


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
