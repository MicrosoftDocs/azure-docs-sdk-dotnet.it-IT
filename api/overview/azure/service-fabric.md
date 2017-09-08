---
title: Librerie di Azure Service Fabric per .NET
description: Informazioni di riferimento sulle librerie di Azure Service Fabric per .NET
keywords: Azure, .NET, SDK, API, Service Fabric
author: spboyer
ms.author: casoper
manager: douge
ms.date: 07/07/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: c708ae06fa4b5165e3f615abf636b11bfd95cd3b
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-service-fabric-libraries-for-net"></a><span data-ttu-id="26161-104">Librerie di Azure Service Fabric per .NET</span><span class="sxs-lookup"><span data-stu-id="26161-104">Azure Service Fabric libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="26161-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="26161-105">Overview</span></span>

<span data-ttu-id="26161-106">Azure Service Fabric è una piattaforma di sistemi distribuiti che semplifica la disposizione in pacchetti, la distribuzione e la gestione di microservizi e contenitori scalabili e affidabili.</span><span class="sxs-lookup"><span data-stu-id="26161-106">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span>

## <a name="client-library"></a><span data-ttu-id="26161-107">Libreria client</span><span class="sxs-lookup"><span data-stu-id="26161-107">Client library</span></span>

<span data-ttu-id="26161-108">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.ServiceFabric) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="26161-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="26161-109">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="26161-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-example"></a><span data-ttu-id="26161-110">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="26161-110">Code Example</span></span>

<span data-ttu-id="26161-111">L'esempio seguente mostra come copiare un pacchetto dell'applicazione nell'archivio immagini, eseguire il provisioning del tipo di applicazione e creare un'istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="26161-111">The following example copies an application package to the image store, provisions the application type, and creates an application instance.</span></span>

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
> [<span data-ttu-id="26161-112">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="26161-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicefabric/client)

## <a name="samples"></a><span data-ttu-id="26161-113">Esempi</span><span class="sxs-lookup"><span data-stu-id="26161-113">Samples</span></span>

* [<span data-ttu-id="26161-114">Distribuire e rimuovere applicazioni con il client Fabric</span><span class="sxs-lookup"><span data-stu-id="26161-114">Deploy and remove applications using FabricClient</span></span>](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
