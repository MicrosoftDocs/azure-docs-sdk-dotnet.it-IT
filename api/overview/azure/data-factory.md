---
title: Librerie di Azure Data Factory per .NET
description: Informazioni di riferimento sulle librerie di Azure Data Factory per .NET
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-factory
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 20e94fa687a3008ac7112d1a6511f8cec92b544c
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2017
---
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="2d800-104">Librerie di Azure Data Factory per .NET</span><span class="sxs-lookup"><span data-stu-id="2d800-104">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="2d800-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2d800-105">Overview</span></span>

<span data-ttu-id="2d800-106">Azure Data Factory è un servizio di integrazione di dati basato sul cloud.</span><span class="sxs-lookup"><span data-stu-id="2d800-106">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="2d800-107">Consente di creare flussi di lavoro basati sui dati nel cloud per orchestrare e automatizzare lo spostamento dei dati e la trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="2d800-107">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="2d800-108">Per altre informazioni, vedere [Introduzione ad Azure Data Factory](/azure/data-factory/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="2d800-108">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library---data-factory-v2-preview"></a><span data-ttu-id="2d800-109">Libreria di gestione - Data Factory V2 (anteprima)</span><span class="sxs-lookup"><span data-stu-id="2d800-109">Management library - Data Factory V2 (Preview)</span></span>

<span data-ttu-id="2d800-110">Usare la libreria di gestione per creare e pianificare i flussi di lavoro basati sui dati (pipeline) in Data Factory V2 (anteprima).</span><span class="sxs-lookup"><span data-stu-id="2d800-110">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory V2 (Preview).</span></span>  <span data-ttu-id="2d800-111">Per altre informazioni, vedere [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net) (Creare una data factory e una pipeline con .NET SDK).</span><span class="sxs-lookup"><span data-stu-id="2d800-111">For more information, see [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net).</span></span>

<span data-ttu-id="2d800-112">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="2d800-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2d800-113">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="2d800-113">Visual Studio Package Manager</span></span>

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a><span data-ttu-id="2d800-114">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="2d800-114">Code Example</span></span>

<span data-ttu-id="2d800-115">L'esempio seguente usa la libreria di gestione per creare una data factory.</span><span class="sxs-lookup"><span data-stu-id="2d800-115">The following example uses the management library to create a data factory.</span></span>

```csharp
/*
using Microsoft.Azure.Management.ResourceManager;
using Microsoft.Azure.Management.DataFactory;
using Microsoft.Azure.Management.DataFactory.Models;
*/

DataFactoryManagementClient client = new DataFactoryManagementClient(tokenCredentials) { SubscriptionId = subscriptionId };
Factory dataFactory = new Factory
{
    Location = region,
    Identity = new FactoryIdentity()
};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d800-116">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="2d800-116">Explore the management APIs</span></span>](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a><span data-ttu-id="2d800-117">Libreria di gestione - Data Factory V1</span><span class="sxs-lookup"><span data-stu-id="2d800-117">Management library - Data Factory V1</span></span>

<span data-ttu-id="2d800-118">Usare la libreria di gestione per creare e pianificare i flussi di lavoro basati sui dati (pipeline) in Data Factory versione 1.</span><span class="sxs-lookup"><span data-stu-id="2d800-118">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory Version 1.</span></span>  <span data-ttu-id="2d800-119">Per altre informazioni, vedere la documentazione per [Data Factory versione 1](/azure/data-factory/v1/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="2d800-119">For more information, review the documentation for [Data Factory Version 1](/azure/data-factory/v1/data-factory-introduction).</span></span>

<span data-ttu-id="2d800-120">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="2d800-120">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2d800-121">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="2d800-121">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="2d800-122">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="2d800-122">Code Example</span></span>

<span data-ttu-id="2d800-123">L'esempio seguente usa la libreria di gestione per creare una data factory.</span><span class="sxs-lookup"><span data-stu-id="2d800-123">The following example uses the management library to create a data factory.</span></span>

```csharp
DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
client.DataFactories.CreateOrUpdate(resourceGroupName,
    new DataFactoryCreateOrUpdateParameters()
    {
        DataFactory = new DataFactory()
        {
            Name = dataFactoryName,
            Location = "westus",
            Properties = new DataFactoryProperties()
        }
    }
);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d800-124">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="2d800-124">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="2d800-125">Esempi</span><span class="sxs-lookup"><span data-stu-id="2d800-125">Samples</span></span>

* <span data-ttu-id="2d800-126">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) (MyDriving - Applicazione di esempio di Azure IOT e per dispositivi mobili) che usa Data Factory per ottenere informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="2d800-126">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="2d800-127">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="2d800-127">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
