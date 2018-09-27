---
title: Librerie di Azure Service Fabric per .NET
description: Informazioni di riferimento sulle librerie di Azure Service Fabric per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-fabric
ms.openlocfilehash: 064f95a4eae3182c4ac5b31779a5d22b592a75b2
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190764"
---
# <a name="azure-service-fabric-libraries-for-net"></a><span data-ttu-id="d073d-103">Librerie di Azure Service Fabric per .NET</span><span class="sxs-lookup"><span data-stu-id="d073d-103">Azure Service Fabric libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="d073d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d073d-104">Overview</span></span>

<span data-ttu-id="d073d-105">Azure Service Fabric è una piattaforma di sistemi distribuiti che semplifica la disposizione in pacchetti, la distribuzione e la gestione di microservizi e contenitori scalabili e affidabili.</span><span class="sxs-lookup"><span data-stu-id="d073d-105">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span>  <span data-ttu-id="d073d-106">Per altre informazioni, vedere la [documentazione di Azure Service Fabric](/azure/service-fabric/).</span><span class="sxs-lookup"><span data-stu-id="d073d-106">For more information, see the [Azure Service Fabric Documentation](/azure/service-fabric/).</span></span>

## <a name="client-library"></a><span data-ttu-id="d073d-107">Libreria client</span><span class="sxs-lookup"><span data-stu-id="d073d-107">Client library</span></span>

<span data-ttu-id="d073d-108">Usare la libreria del client di Service Fabric per interagire con un cluster di Service Fabric esistente.</span><span class="sxs-lookup"><span data-stu-id="d073d-108">Use the Service Fabric client library to interact with an existing Service Fabric cluster.</span></span>  <span data-ttu-id="d073d-109">La libreria contiene tre categorie di API:</span><span class="sxs-lookup"><span data-stu-id="d073d-109">The library contains three categories of APIs:</span></span>

* <span data-ttu-id="d073d-110">Le API **client** vengono usate per gestire, ridimensionare e riciclare il cluster, oltre a distribuire pacchetti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d073d-110">**Client** APIs are used to manage, scale, and recycle the cluster, as well as deploy application packages.</span></span>
* <span data-ttu-id="d073d-111">Le API di **runtime** vengono usate per consentire all'applicazione in esecuzione di interagire con rispettivo cluster di hosting.</span><span class="sxs-lookup"><span data-stu-id="d073d-111">**Runtime** APIs are used for the running application to interact with its hosting cluster.</span></span>
* <span data-ttu-id="d073d-112">Le API **comuni** contengono tipi usati nelle API **client** e di **runtime**.</span><span class="sxs-lookup"><span data-stu-id="d073d-112">**Common** APIs contain types used in both **client** and **runtime** APIs.</span></span>

<span data-ttu-id="d073d-113">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.ServiceFabric) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="d073d-113">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d073d-114">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="d073d-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-examples"></a><span data-ttu-id="d073d-115">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="d073d-115">Code Examples</span></span>

<span data-ttu-id="d073d-116">L'esempio seguente usa le API **client** di Service Fabric per copiare un pacchetto dell'applicazione nell'archivio immagini, effettuare il provisioning del tipo di applicazione e creare un'istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d073d-116">The following example uses the Service Fabric **client** APIs to copy an application package to the image store, provisions the application type, and create an application instance.</span></span>

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
> [<span data-ttu-id="d073d-117">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="d073d-117">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicefabric/client)

<span data-ttu-id="d073d-118">Questo esempio usa le API di **runtime** e **common** di Service Fabric da un'applicazione ospitata per aggiornare una raccolta [Reliable Collections](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) in fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="d073d-118">This example uses the Service Fabric **runtime** and **common** APIs from within a hosted application to update a [Reliable Collection](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) at runtime.</span></span>

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
> [<span data-ttu-id="d073d-119">Esplora le API di runtime</span><span class="sxs-lookup"><span data-stu-id="d073d-119">Explore the runtime APIs</span></span>](/dotnet/api/overview/azure/servicefabric/runtime)

> [!div class="nextstepaction"]
> [<span data-ttu-id="d073d-120">Esplora le API comuni</span><span class="sxs-lookup"><span data-stu-id="d073d-120">Explore the common APIs</span></span>](/dotnet/api/overview/azure/servicefabric/common)

## <a name="management-library"></a><span data-ttu-id="d073d-121">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="d073d-121">Management Library</span></span>

<span data-ttu-id="d073d-122">La libreria di gestione viene usata per creare, aggiornare ed eliminare cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d073d-122">The management library is used to create, update, and delete Service Fabric clusters.</span></span>

<span data-ttu-id="d073d-123">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="d073d-123">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d073d-124">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="d073d-124">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceFabric
```

```bash
dotnet add package Microsoft.Azure.Management.ServiceFabric
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d073d-125">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="d073d-125">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicefabric/management)

## <a name="samples"></a><span data-ttu-id="d073d-126">Esempi</span><span class="sxs-lookup"><span data-stu-id="d073d-126">Samples</span></span>

* [<span data-ttu-id="d073d-127">Distribuire e rimuovere applicazioni con il client Fabric</span><span class="sxs-lookup"><span data-stu-id="d073d-127">Deploy and remove applications using FabricClient</span></span>](/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
