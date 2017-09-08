---
title: Librerie di Azure Data Factory per .NET
description: Informazioni di riferimento sulle librerie di Azure Data Factory per .NET
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: e0b85d7d3988febca6dce7f4038825d74e4b8d2e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="c2ad2-104">Librerie di Azure Data Factory per .NET</span><span class="sxs-lookup"><span data-stu-id="c2ad2-104">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c2ad2-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c2ad2-105">Overview</span></span>

<span data-ttu-id="c2ad2-106">Azure Data Factory è un servizio di integrazione di dati basato sul cloud.</span><span class="sxs-lookup"><span data-stu-id="c2ad2-106">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="c2ad2-107">Consente di creare flussi di lavoro basati sui dati nel cloud per orchestrare e automatizzare lo spostamento dei dati e la trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="c2ad2-107">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="c2ad2-108">Per altre informazioni, vedere [Introduzione ad Azure Data Factory](/azure/data-factory/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="c2ad2-108">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library"></a><span data-ttu-id="c2ad2-109">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="c2ad2-109">Management library</span></span>

<span data-ttu-id="c2ad2-110">Usare la libreria di gestione per creare e pianificare i flussi di lavoro basati sui dati (pipeline).</span><span class="sxs-lookup"><span data-stu-id="c2ad2-110">Use the management library to create and schedule data-driven workflows (pipelines).</span></span>

<span data-ttu-id="c2ad2-111">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c2ad2-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c2ad2-112">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="c2ad2-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="c2ad2-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="c2ad2-113">Code Example</span></span>

<span data-ttu-id="c2ad2-114">L'esempio seguente usa la libreria di gestione per creare una data factory.</span><span class="sxs-lookup"><span data-stu-id="c2ad2-114">The following example uses the management library to create a data factory.</span></span>

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
> [<span data-ttu-id="c2ad2-115">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="c2ad2-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="c2ad2-116">Esempi</span><span class="sxs-lookup"><span data-stu-id="c2ad2-116">Samples</span></span>

* <span data-ttu-id="c2ad2-117">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) (MyDriving - Applicazione di esempio di Azure IOT e per dispositivi mobili) che usa Data Factory per ottenere informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="c2ad2-117">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="c2ad2-118">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="c2ad2-118">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
