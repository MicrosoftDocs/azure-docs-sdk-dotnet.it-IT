---
title: API di archiviazione di Azure per .NET
description: Informazioni di riferimento sulle librerie di archiviazione di Azure per .NET
keywords: Azure, .NET, SDK, API, archiviazione, BLOB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: storage
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 273e7ffc8794ef531e2bd35858b8ad1299755882
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065531"
---
# <a name="azure-storage-apis-for-net"></a><span data-ttu-id="41e86-104">API di archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="41e86-104">Azure Storage APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="41e86-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="41e86-105">Overview</span></span>

<span data-ttu-id="41e86-106">Eseguire la lettura e la scrittura di file, dati di BLOB (oggetto), coppie chiave-valore e messaggi dalle applicazioni .NET con l'[Archiviazione di Azure](https://review.docs.microsoft.com/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="41e86-106">Read and write files, blob (object) data, key-value pairs, and messages from your .NET applications with [Azure Storage](https://review.docs.microsoft.com/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="41e86-107">Per iniziare a usare Archiviazione di Azure, vedere [Introduzione all'archivio BLOB di Azure con .NET](/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="41e86-107">To get started with Azure Storage, see [Get started with Azure Blob storage using .NET](/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

## <a name="client-library"></a><span data-ttu-id="41e86-108">Libreria client</span><span class="sxs-lookup"><span data-stu-id="41e86-108">Client library</span></span>

<span data-ttu-id="41e86-109">Usare le [stringhe di connessione](/azure/storage/storage-create-storage-account#manage-your-storage-account) per connettersi a un account di archiviazione di Azure e quindi usare le classi e i metodi delle librerie client per usare l'archiviazione BLOB, tabelle, file o code.</span><span class="sxs-lookup"><span data-stu-id="41e86-109">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span>

<span data-ttu-id="41e86-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/WindowsAzure.Storage) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="41e86-110">Install the [NuGet package](https://www.nuget.org/packages/WindowsAzure.Storage) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="41e86-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="41e86-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package WindowsAzure.Storage
```

### <a name="net-core-cli"></a><span data-ttu-id="41e86-112">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="41e86-112">.NET Core CLI</span></span>

```bash
dotnet add package WindowsAzure.Storage
```

### <a name="code-example"></a><span data-ttu-id="41e86-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="41e86-113">Code Example</span></span>

<span data-ttu-id="41e86-114">Questo esempio mostra come creare un nuovo BLOB in un nuovo contenitore in un account di archiviazione esistente.</span><span class="sxs-lookup"><span data-stu-id="41e86-114">This example creates a new blob to a new container in an existing storage account.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
*/

string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=[Storage Account Name]"
    + ";AccountKey=[Storage Account Key]"
    + ";EndpointSuffix=core.windows.net";

CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);
CloudBlobClient serviceClient = account.CreateCloudBlobClient();

// Create container. Name must be lower case.
Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("mycontainer");
container.CreateIfNotExistsAsync().Wait();

// write a blob to the container
CloudBlockBlob blob = container.GetBlockBlobReference("helloworld.txt");
blob.UploadTextAsync("Hello, World!").Wait();
```

> [!div class="nextstepactions"]
> [<span data-ttu-id="41e86-115">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="41e86-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/storage/client)

## <a name="management-apis"></a><span data-ttu-id="41e86-116">API di gestione</span><span class="sxs-lookup"><span data-stu-id="41e86-116">Management APIs</span></span>

<span data-ttu-id="41e86-117">Creare e gestire account di archiviazione di Azure e chiavi di connessione con l'API di gestione.</span><span class="sxs-lookup"><span data-stu-id="41e86-117">Create and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="41e86-118">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="41e86-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="41e86-119">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="41e86-119">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Storage.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="41e86-120">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="41e86-120">.NET Core CLI</span></span>

````bash
dotnet add package Microsoft.Azure.Management.Storage.Fluent
````

### <a name="code-example"></a><span data-ttu-id="41e86-121">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="41e86-121">Code Example</span></span>

<span data-ttu-id="41e86-122">Questo esempio mostra come creare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="41e86-122">This example creates a storage account.</span></span>

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Management.Storage.Fluent
*/

IStorageAccount storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .Create();
```

> [!div class="nextstepactions"]
> [<span data-ttu-id="41e86-123">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="41e86-123">Explore the management APIs</span></span>](/dotnet/api/overview/azure/storage/management)

## <a name="samples"></a><span data-ttu-id="41e86-124">Esempi</span><span class="sxs-lookup"><span data-stu-id="41e86-124">Samples</span></span>

* [<span data-ttu-id="41e86-125">Introduzione all'archivio BLOB di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="41e86-125">Get started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/) 
* <span data-ttu-id="41e86-126">[Get started with Azure Queue Storage in .NET](https://azure.microsoft.com/resources/samples/storage-queue-dotnet-getting-started/) (Introduzione all'archiviazione code di Azure con .NET)</span><span class="sxs-lookup"><span data-stu-id="41e86-126">[Get started with Azure Queue Storage in .NET](https://azure.microsoft.com/resources/samples/storage-queue-dotnet-getting-started/)</span></span>

<span data-ttu-id="41e86-127">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) degli esempi di codice per Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="41e86-127">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) of Azure Storage samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package