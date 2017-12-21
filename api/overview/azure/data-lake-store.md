---
title: Librerie di Azure Data Lake Store per .NET
description: Informazioni di riferimento sulle librerie di Azure Data Lake Store per .NET
keywords: Azure, .NET, SDK, API, Data Lake Store
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-lake-store
ms.custom: devcenter, svc-overview
ms.openlocfilehash: e8380c4a9ebf86f03fe87fc800dffda10e48e60a
ms.sourcegitcommit: 3e904e6e4f04f1c92d729459434c85faff32e386
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/09/2017
---
# <a name="azure-data-lake-store-libraries-for-net"></a><span data-ttu-id="07867-104">Librerie di Azure Data Lake Store per .NET</span><span class="sxs-lookup"><span data-stu-id="07867-104">Azure Data Lake Store libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="07867-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="07867-105">Overview</span></span>

<span data-ttu-id="07867-106">Azure Data Lake Store è un repository su vasta scala a livello aziendale per carichi di lavoro di analisi di Big Data.</span><span class="sxs-lookup"><span data-stu-id="07867-106">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="07867-107">Azure Data Lake consente di acquisire dati di qualsiasi dimensione, tipo e velocità di inserimento in un'unica posizione per le analisi esplorative e operative.</span><span class="sxs-lookup"><span data-stu-id="07867-107">Azure Data Lake enables you to capture data of any size, type, and ingestion speed in one single place for operational and exploratory analytics.</span></span>

<span data-ttu-id="07867-108">Per altre informazioni, vedere [Panoramica di Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span><span class="sxs-lookup"><span data-stu-id="07867-108">To learn more, see [Overview of Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

## <a name="client-library"></a><span data-ttu-id="07867-109">Libreria client</span><span class="sxs-lookup"><span data-stu-id="07867-109">Client library</span></span>

<span data-ttu-id="07867-110">Usare la libreria client per eseguire operazioni del file system in Data Lake Store, ad esempio la creazione di cartelle in un account Data Lake Store, il caricamento di file e il download di file.</span><span class="sxs-lookup"><span data-stu-id="07867-110">Use the client library to perform filesystem operations on Data Lake Store, such as creating folders in a Data Lake Store account, uploading files, and downloading files.</span></span>  <span data-ttu-id="07867-111">Per un'esercitazione completa sull'uso di Data Lake Store con .NET, vedere [Operazioni del file system in Azure Data Lake Store con .NET SDK](/azure/data-lake-store/data-lake-store-data-operations-net-sdk).</span><span class="sxs-lookup"><span data-stu-id="07867-111">For a full tutorial on using Data Lake Store with .NET, see [Filesystem operations on Azure Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-data-operations-net-sdk).</span></span>

<span data-ttu-id="07867-112">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="07867-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="07867-113">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="07867-113">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.DataLake.Store
```
### <a name="authentication"></a><span data-ttu-id="07867-114">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="07867-114">Authentication</span></span>

* <span data-ttu-id="07867-115">Per l'autenticazione dell'utente finale per l'applicazione, vedere [End-user authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk) (Autenticazione dell'utente finale con Data Lake Store tramite .NET SDK).</span><span class="sxs-lookup"><span data-stu-id="07867-115">For end-user authentication for your application, see [End-user authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk).</span></span>
* <span data-ttu-id="07867-116">Per l'autenticazione da servizio a servizio per l'applicazione, vedere [Service-to-service authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk) (Autenticazione da servizio a servizio con Data Lake Store tramite .NET SDK).</span><span class="sxs-lookup"><span data-stu-id="07867-116">For service-to-service authentication for your application, see [Service-to-service authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk).</span></span>

### <a name="code-example"></a><span data-ttu-id="07867-117">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="07867-117">Code Example</span></span>

<span data-ttu-id="07867-118">Il frammento di codice seguente crea l'oggetto client del file system di Data Lake Store, usato per inviare richieste al servizio.</span><span class="sxs-lookup"><span data-stu-id="07867-118">The following snippet creates the Data Lake Store filesystem client object, which is used to issue requests to the service.</span></span>

```csharp
// Create client objects
AdlsClient client = AdlsClient.CreateClient(_adlsAccountName, adlCreds);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="07867-119">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="07867-119">Explore the client APIs</span></span>](/dotnet/api/overview/azure/datalakestore/client)


## <a name="management-library"></a><span data-ttu-id="07867-120">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="07867-120">Management library</span></span>

<span data-ttu-id="07867-121">Usare la libreria di gestione per connettersi ai repository di Big Data e gestirli.</span><span class="sxs-lookup"><span data-stu-id="07867-121">Use the management library to connect to and manage your big data repositories.</span></span>

<span data-ttu-id="07867-122">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="07867-122">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="07867-123">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="07867-123">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="07867-124">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="07867-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/datalakestore/management)


## <a name="samples"></a><span data-ttu-id="07867-125">Esempi</span><span class="sxs-lookup"><span data-stu-id="07867-125">Samples</span></span>

* <span data-ttu-id="07867-126">[Azure Data Lake .NET Client Example](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/) (Esempio di client di Azure Data Lake per .NET)</span><span class="sxs-lookup"><span data-stu-id="07867-126">[Azure Data Lake .NET Client Example](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)</span></span>

<span data-ttu-id="07867-127">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="07867-127">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
