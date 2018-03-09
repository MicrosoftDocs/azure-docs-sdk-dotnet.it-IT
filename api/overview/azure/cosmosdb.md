---
title: Librerie di Azure Cosmos DB per .NET
description: Informazioni di riferimento sulle librerie di Azure Cosmos DB per .NET
keywords: Azure, .NET, SDK, API, Cosmos DB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 11/17/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4791e00c18d00fbed13bdf2c626a24fed2ff2863
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2018
---
# <a name="azure-cosmosdb-libraries-for-net"></a><span data-ttu-id="bf132-104">Librerie di Azure Cosmos DB per .NET</span><span class="sxs-lookup"><span data-stu-id="bf132-104">Azure CosmosDB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="bf132-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="bf132-105">Overview</span></span>

<span data-ttu-id="bf132-106">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) è un archivio dati distribuito e scalabile che supporta vari tipi diversi di database.</span><span class="sxs-lookup"><span data-stu-id="bf132-106">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a distributed and scalable data store, supporting multiple different types of databases.</span></span>

<span data-ttu-id="bf132-107">[Introduzione a Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-documentdb-dotnet).</span><span class="sxs-lookup"><span data-stu-id="bf132-107">[Get started with CosmosDB](https://docs.microsoft.com/azure/cosmos-db/create-documentdb-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="bf132-108">Libreria client</span><span class="sxs-lookup"><span data-stu-id="bf132-108">Client library</span></span>

<span data-ttu-id="bf132-109">Usare la libreria client di Cosmos DB per .NET per accedere ai dati e archiviarli in un archivio dati Cosmos DB esistente.</span><span class="sxs-lookup"><span data-stu-id="bf132-109">Use the CosmosDB .NET client library to access and store data in an existing CosmosDB data store.</span></span>  <span data-ttu-id="bf132-110">Per automatizzare la creazione di un nuovo account CosmosDB, usare il portale di Azure, l'interfaccia della riga di comando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf132-110">To automate creation of a new CosmosDB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="bf132-111">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="bf132-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="bf132-112">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="bf132-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="bf132-113">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="bf132-113">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="bf132-114">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="bf132-114">Code Example</span></span>

<span data-ttu-id="bf132-115">Questo esempio mostra come connettersi a un database dell'API DocumentDB di Cosmos DB, eseguire la lettura di un documento da una raccolta e deserializzare il documento come un oggetto `Item`.</span><span class="sxs-lookup"><span data-stu-id="bf132-115">This example connects to an existing CosmosDB DocumentDB API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bf132-116">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="bf132-116">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="bf132-117">Esempi</span><span class="sxs-lookup"><span data-stu-id="bf132-117">Samples</span></span>

* <span data-ttu-id="bf132-118">[Develop a Java app using Azure Cosmos DB MongoDB API](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/) (Sviluppare un'app Java con l'API MongoDB di Azure Cosmos DB)</span><span class="sxs-lookup"><span data-stu-id="bf132-118">[Developing a .NET app using Azure Cosmos DB's MongoDB API](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)</span></span>

<span data-ttu-id="bf132-119">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) degli esempi di codice per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bf132-119">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
