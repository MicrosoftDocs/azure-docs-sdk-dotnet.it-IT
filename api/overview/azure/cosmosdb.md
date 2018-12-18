---
title: Librerie di Azure Cosmos DB per .NET
description: Informazioni di riferimento sulle librerie di Azure Cosmos DB per .NET
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 8ff565f1cd72eec2f574b45d04ceac526b8c5eb0
ms.sourcegitcommit: 01ec3adba39a6f946015552c28da0a9a6bb57180
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53112019"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="6d390-103">Librerie di Azure Cosmos DB per .NET</span><span class="sxs-lookup"><span data-stu-id="6d390-103">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6d390-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6d390-104">Overview</span></span>

<span data-ttu-id="6d390-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) è un servizio di database multimodello e distribuito a livello globale.</span><span class="sxs-lookup"><span data-stu-id="6d390-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="6d390-106">È progettato per ridimensionare in modo elastico e indipendente velocità effettiva e memoria tra più aree geografiche con un contratto di servizio completo.</span><span class="sxs-lookup"><span data-stu-id="6d390-106">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="6d390-107">Azure Cosmos DB consente di archiviare e accedere a database di documenti, con coppie chiave-valore, con colonna ampia e con elementi grafici mediante API e modelli di programmazione.</span><span class="sxs-lookup"><span data-stu-id="6d390-107">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="6d390-108">[Introduzione a Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span><span class="sxs-lookup"><span data-stu-id="6d390-108">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="6d390-109">Libreria client</span><span class="sxs-lookup"><span data-stu-id="6d390-109">Client library</span></span>

<span data-ttu-id="6d390-110">Usare la libreria client di Azure Cosmos DB per .NET per accedere ai dati e archiviarli in un archivio dati Azure Cosmos DB esistente.</span><span class="sxs-lookup"><span data-stu-id="6d390-110">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="6d390-111">Per automatizzare la creazione di un nuovo account Azure Cosmos DB, usare il portale di Azure, l'interfaccia della riga di comando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d390-111">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="6d390-112">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6d390-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

<span data-ttu-id="6d390-113">Per installare la versione 2.x:</span><span class="sxs-lookup"><span data-stu-id="6d390-113">To install version 2.x:</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6d390-114">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="6d390-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="6d390-115">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="6d390-115">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

<span data-ttu-id="6d390-116">Per installare l'anteprima della versione 3.0 per lo standard .NET:</span><span class="sxs-lookup"><span data-stu-id="6d390-116">To install the preview of version 3.0, which targets .NET standard:</span></span> 

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6d390-117">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="6d390-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Cosmos -prerelease
```

#### <a name="net-core-cli"></a><span data-ttu-id="6d390-118">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="6d390-118">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Cosmos
```


### <a name="code-example"></a><span data-ttu-id="6d390-119">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="6d390-119">Code Example</span></span>

<span data-ttu-id="6d390-120">Questo esempio mostra come connettersi a un database dell'API SQL Azure Cosmos DB, leggere un documento da una raccolta e deserializzare il documento come oggetto `Item`.</span><span class="sxs-lookup"><span data-stu-id="6d390-120">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span> <span data-ttu-id="6d390-121">Questo esempio usa la versione 2.x di .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="6d390-121">This example uses version 2.x of the .NET SDK.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

<span data-ttu-id="6d390-122">Questo esempio si collega a un database API SQL di Azure Cosmos DB esistente, crea un nuovo database e contenitore, legge un elemento dal contenitore e lo deserializza in un oggetto `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="6d390-122">This example connects to an existing Azure Cosmos DB SQL API database, creates a new database and container, reads an item from the container, and deserializes it to a `TodoItem` object.</span></span> <span data-ttu-id="6d390-123">Questo esempio usa la versione 3.x di .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="6d390-123">This example uses version 3.x of the .NET SDK.</span></span>   

```csharp
using (CosmosClient cosmosClient = new CosmosClient("endpoint", "primaryKey"))
{
    // Read item from container
    CosmosItemResponse<TodoItem> todoItemResponse = await cosmosClient.Databases["DatabaseId"].Containers["ContainerId"].Items.ReadItemAsync<TodoItem>("partitionKeyValue", "ItemId");
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6d390-124">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="6d390-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="6d390-125">Esempi</span><span class="sxs-lookup"><span data-stu-id="6d390-125">Samples</span></span>

* [<span data-ttu-id="6d390-126">Sviluppo di un'app .NET usando l'API SQL di Azure Cosmos DB (versione 2.x)</span><span class="sxs-lookup"><span data-stu-id="6d390-126">Developing a .NET app using Azure Cosmos DB's SQL API (Version 2.x)</span></span>](https://github.com/Azure-Samples/documentdb-dotnet-todo-app/)
* [<span data-ttu-id="6d390-127">Sviluppo di un'app .NET usando l'API SQL di Azure Cosmos DB (versione 3.x di anteprima)</span><span class="sxs-lookup"><span data-stu-id="6d390-127">Developing a .NET app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-todo-app/)
* [<span data-ttu-id="6d390-128">Sviluppo di un'app .NET Core usando l'API SQL di Azure Cosmos DB (versione 3.x di anteprima)</span><span class="sxs-lookup"><span data-stu-id="6d390-128">Developing a .NET Core app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-core-getting-started)

<span data-ttu-id="6d390-129">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) degli esempi di codice per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6d390-129">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
