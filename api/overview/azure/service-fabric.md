---
title: Librerie di Azure Service Fabric per .NET
description: Informazioni di riferimento sulle librerie di Azure Service Fabric per .NET
keywords: Azure, .NET, SDK, API, Service Fabric
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: service-fabric
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f4b54933d31a4e1fc4c390baa57469cc1c02783a
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566094"
---
# <a name="azure-service-fabric-libraries-for-net"></a>Librerie di Azure Service Fabric per .NET

## <a name="overview"></a>Panoramica

Azure Service Fabric è una piattaforma di sistemi distribuiti che semplifica la disposizione in pacchetti, la distribuzione e la gestione di microservizi e contenitori scalabili e affidabili.  Per altre informazioni, vedere la [documentazione di Azure Service Fabric](/azure/service-fabric/).

## <a name="client-library"></a>Libreria client

Usare la libreria del client di Service Fabric per interagire con un cluster di Service Fabric esistente.  La libreria contiene tre categorie di API:

* Le API **client** vengono usate per gestire, ridimensionare e riciclare il cluster, oltre a distribuire pacchetti dell'applicazione.
* Le API di **runtime** vengono usate per consentire all'applicazione in esecuzione di interagire con rispettivo cluster di hosting.
* Le API **comuni** contengono tipi usati nelle API **client** e di **runtime**.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.ServiceFabric) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-examples"></a>Esempi di codice

L'esempio seguente usa le API **client** di Service Fabric per copiare un pacchetto dell'applicazione nell'archivio immagini, effettuare il provisioning del tipo di applicazione e creare un'istanza dell'applicazione.

```csharp
/* Include these dependencies
using System.Fabric;
using System.Fabric.Description;
*/

// Connect to the cluster.
FabricClient fabricClient = new FabricClient(clusterConnection);

// Copy the application package to a location in the image store
fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);

// Provision the application.
fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

//  Create the application instance.
ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/servicefabric/client)

Questo esempio usa le API di **runtime** e **common** di Service Fabric da un'applicazione ospitata per aggiornare una raccolta [Reliable Collections](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) in fase di runtime.

```csharp
using System.Fabric;
using Microsoft.ServiceFabric.Data.Collections;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

/// <summary>
/// This is the main entry point for your service replica.
/// This method executes when this replica of your service becomes primary and has write status.
/// </summary>
/// <param name="cancellationToken">Canceled when Service Fabric needs to shut down this service replica.</param>
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();
        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }
        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

> [!div class="nextstepaction"]
> [Esplora le API di runtime](/dotnet/api/overview/azure/servicefabric/runtime)

> [!div class="nextstepaction"]
> [Esplora le API comuni](/dotnet/api/overview/azure/servicefabric/common)

## <a name="management-library"></a>Libreria di gestione

La libreria di gestione viene usata per creare, aggiornare ed eliminare cluster di Service Fabric.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.ServiceFabric
```

```bash
dotnet add package Microsoft.Azure.Management.ServiceFabric
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/servicefabric/management)

## <a name="samples"></a>Esempi

* [Distribuire e rimuovere applicazioni con il client Fabric](/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
