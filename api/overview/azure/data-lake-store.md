---
title: Librerie di Azure Data Lake Store per .NET
description: Informazioni di riferimento sulle librerie di Azure Data Lake Store per .NET
keywords: Azure, .NET, SDK, API, Data Lake Store
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/18/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 18746d745d64065a3d92215e704bce575130bdb0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-lake-store-libraries-for-net"></a><span data-ttu-id="d30d1-104">Librerie di Azure Data Lake Store per .NET</span><span class="sxs-lookup"><span data-stu-id="d30d1-104">Azure Data Lake Store libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="d30d1-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d30d1-105">Overview</span></span>

<span data-ttu-id="d30d1-106">Azure Data Lake Store è un repository su vasta scala a livello aziendale per carichi di lavoro di analisi di Big Data.</span><span class="sxs-lookup"><span data-stu-id="d30d1-106">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="d30d1-107">Azure Data Lake consente di acquisire dati di qualsiasi dimensione, tipo e velocità di inserimento in un'unica posizione per le analisi esplorative e operative.</span><span class="sxs-lookup"><span data-stu-id="d30d1-107">Azure Data Lake enables you to capture data of any size, type, and ingestion speed in one single place for operational and exploratory analytics.</span></span>

<span data-ttu-id="d30d1-108">Per altre informazioni, vedere [Panoramica di Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span><span class="sxs-lookup"><span data-stu-id="d30d1-108">To learn more, see [Overview of Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="d30d1-109">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="d30d1-109">Management library</span></span>

<span data-ttu-id="d30d1-110">Usare la libreria di gestione per connettersi ai repository di Big Data e gestirli.</span><span class="sxs-lookup"><span data-stu-id="d30d1-110">Use the management library to connect to and manage your big data repositories.</span></span>

<span data-ttu-id="d30d1-111">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="d30d1-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d30d1-112">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="d30d1-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

### <a name="code-example"></a><span data-ttu-id="d30d1-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="d30d1-113">Code Example</span></span>

<span data-ttu-id="d30d1-114">Questo esempio esegue l'autenticazione di un account e un archivio di analisi e crea i client necessari per la gestione.</span><span class="sxs-lookup"><span data-stu-id="d30d1-114">This example authenticates to an analytics account and store and creates the clients necessary for management.</span></span>

```csharp
/*
using AdlClient
using AdlClient.Models 
*/

// Setup authentication 
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
StoreAccountRef adls_account = new StoreAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
StoreClient adls = new StoreClient(auth, adls_account);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d30d1-115">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="d30d1-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datalakestore/management)

## <a name="samples"></a><span data-ttu-id="d30d1-116">Esempi</span><span class="sxs-lookup"><span data-stu-id="d30d1-116">Samples</span></span>

* [<span data-ttu-id="d30d1-117">Azure Data Lake .NET Client Example</span><span class="sxs-lookup"><span data-stu-id="d30d1-117">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/) (Esempio di client di Azure Data Lake per .NET)

<span data-ttu-id="d30d1-118">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="d30d1-118">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
