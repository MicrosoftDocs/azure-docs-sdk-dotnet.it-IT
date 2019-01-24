---
title: Librerie di Azure Cosmos DB per .NET
description: Informazioni di riferimento sulle librerie di Azure Cosmos DB per .NET
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 95fcd8468c3d472cfcadeaae3b56ae789c3b1e7a
ms.sourcegitcommit: 55ee51501678d1575e5159f0ac0e475b5bf9daf3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/22/2019
ms.locfileid: "54453995"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="9461c-103">Librerie di Azure Cosmos DB per .NET</span><span class="sxs-lookup"><span data-stu-id="9461c-103">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="9461c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9461c-104">Overview</span></span>

<span data-ttu-id="9461c-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) è un servizio di database multimodello e distribuito a livello globale.</span><span class="sxs-lookup"><span data-stu-id="9461c-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="9461c-106">È progettato per ridimensionare in modo elastico e indipendente velocità effettiva e memoria tra più aree geografiche con un contratto di servizio completo.</span><span class="sxs-lookup"><span data-stu-id="9461c-106">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="9461c-107">Azure Cosmos DB consente di archiviare e accedere a database di documenti, con coppie chiave-valore, con colonna ampia e con elementi grafici mediante API e modelli di programmazione.</span><span class="sxs-lookup"><span data-stu-id="9461c-107">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="9461c-108">[Introduzione a Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span><span class="sxs-lookup"><span data-stu-id="9461c-108">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="9461c-109">Libreria client</span><span class="sxs-lookup"><span data-stu-id="9461c-109">Client library</span></span>

<span data-ttu-id="9461c-110">Usare la libreria client di Azure Cosmos DB per .NET per accedere ai dati e archiviarli in un archivio dati Azure Cosmos DB esistente.</span><span class="sxs-lookup"><span data-stu-id="9461c-110">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="9461c-111">Per automatizzare la creazione di un nuovo account Azure Cosmos DB, usare il portale di Azure, l'interfaccia della riga di comando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9461c-111">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="9461c-112">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="9461c-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

<span data-ttu-id="9461c-113">Per installare la versione 2.x:</span><span class="sxs-lookup"><span data-stu-id="9461c-113">To install version 2.x:</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9461c-114">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="9461c-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="9461c-115">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="9461c-115">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

<span data-ttu-id="9461c-116">Per installare l'anteprima della versione 3.0 per lo standard .NET:</span><span class="sxs-lookup"><span data-stu-id="9461c-116">To install the preview of version 3.0, which targets .NET standard:</span></span> 

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9461c-117">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="9461c-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Cosmos -prerelease
```

#### <a name="net-core-cli"></a><span data-ttu-id="9461c-118">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="9461c-118">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Cosmos
```


### <a name="code-example"></a><span data-ttu-id="9461c-119">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="9461c-119">Code Example</span></span>

<span data-ttu-id="9461c-120">Questo esempio mostra come connettersi a un database dell'API SQL Azure Cosmos DB, leggere un documento da una raccolta e deserializzare il documento come oggetto `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="9461c-120">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `TodoItem` object.</span></span> <span data-ttu-id="9461c-121">Questo esempio usa la versione 2.x di .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="9461c-121">This example uses version 2.x of the .NET SDK.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
var todoItem = client.ReadDocumentAsync<TodoItem>(documentUri);
```

<span data-ttu-id="9461c-122">Questo esempio si collega a un database API SQL di Azure Cosmos DB esistente, crea un nuovo database e contenitore, legge un elemento dal contenitore e lo deserializza in un oggetto `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="9461c-122">This example connects to an existing Azure Cosmos DB SQL API database, creates a new database and container, reads an item from the container, and deserializes it to a `TodoItem` object.</span></span> <span data-ttu-id="9461c-123">Questo esempio usa la versione 3.x di .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="9461c-123">This example uses version 3.x of the .NET SDK.</span></span>   

```csharp
using (CosmosClient cosmosClient = new CosmosClient("endpoint", "primaryKey"))
{
    // Read item from container
    CosmosItemResponse<TodoItem> todoItemResponse = await cosmosClient.Databases["DatabaseId"].Containers["ContainerId"].Items.ReadItemAsync<TodoItem>("partitionKeyValue", "ItemId");
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9461c-124">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="9461c-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="9461c-125">Esempi</span><span class="sxs-lookup"><span data-stu-id="9461c-125">Samples</span></span>

* [<span data-ttu-id="9461c-126">Sviluppo di un'app .NET usando l'API SQL di Azure Cosmos DB (versione 2.x)</span><span class="sxs-lookup"><span data-stu-id="9461c-126">Developing a .NET app using Azure Cosmos DB's SQL API (Version 2.x)</span></span>](https://github.com/Azure-Samples/documentdb-dotnet-todo-app/)
* [<span data-ttu-id="9461c-127">Sviluppo di un'app .NET usando l'API SQL di Azure Cosmos DB (versione 3.x di anteprima)</span><span class="sxs-lookup"><span data-stu-id="9461c-127">Developing a .NET app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-todo-app/)
* [<span data-ttu-id="9461c-128">Sviluppo di un'app .NET Core usando l'API SQL di Azure Cosmos DB (versione 3.x di anteprima)</span><span class="sxs-lookup"><span data-stu-id="9461c-128">Developing a .NET Core app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-core-getting-started)

<span data-ttu-id="9461c-129">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) degli esempi di codice per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9461c-129">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
