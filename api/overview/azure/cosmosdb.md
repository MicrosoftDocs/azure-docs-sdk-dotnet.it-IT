---
title: Librerie di Azure Cosmos DB per .NET
description: Informazioni di riferimento sulle librerie di Azure Cosmos DB per .NET
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 21a2f2168259528a0d27103783e34aa532d7e17a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190795"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="baa86-103">Librerie di Azure Cosmos DB per .NET</span><span class="sxs-lookup"><span data-stu-id="baa86-103">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="baa86-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="baa86-104">Overview</span></span>

<span data-ttu-id="baa86-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) è un servizio di database multimodello e distribuito a livello globale.</span><span class="sxs-lookup"><span data-stu-id="baa86-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="baa86-106">È progettato per ridimensionare in modo elastico e indipendente velocità effettiva e memoria tra più aree geografiche con un contratto di servizio completo.</span><span class="sxs-lookup"><span data-stu-id="baa86-106">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="baa86-107">Azure Cosmos DB consente di archiviare e accedere a database di documenti, con coppie chiave-valore, con colonna ampia e con elementi grafici mediante API e modelli di programmazione.</span><span class="sxs-lookup"><span data-stu-id="baa86-107">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="baa86-108">[Introduzione a Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span><span class="sxs-lookup"><span data-stu-id="baa86-108">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="baa86-109">Libreria client</span><span class="sxs-lookup"><span data-stu-id="baa86-109">Client library</span></span>

<span data-ttu-id="baa86-110">Usare la libreria client di Azure Cosmos DB per .NET per accedere ai dati e archiviarli in un archivio dati Azure Cosmos DB esistente.</span><span class="sxs-lookup"><span data-stu-id="baa86-110">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="baa86-111">Per automatizzare la creazione di un nuovo account Azure Cosmos DB, usare il portale di Azure, l'interfaccia della riga di comando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="baa86-111">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="baa86-112">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="baa86-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="baa86-113">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="baa86-113">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="baa86-114">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="baa86-114">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="baa86-115">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="baa86-115">Code Example</span></span>

<span data-ttu-id="baa86-116">Questo esempio mostra come connettersi a un database dell'API SQL Azure Cosmos DB, leggere un documento da una raccolta e deserializzare il documento come oggetto `Item`.</span><span class="sxs-lookup"><span data-stu-id="baa86-116">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="baa86-117">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="baa86-117">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="baa86-118">Esempi</span><span class="sxs-lookup"><span data-stu-id="baa86-118">Samples</span></span>

* <span data-ttu-id="baa86-119">[Develop a Java app using Azure Cosmos DB MongoDB API](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/) (Sviluppare un'app Java con l'API MongoDB di Azure Cosmos DB)</span><span class="sxs-lookup"><span data-stu-id="baa86-119">[Developing a .NET app using Azure Cosmos DB's MongoDB API](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)</span></span>

<span data-ttu-id="baa86-120">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) degli esempi di codice per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="baa86-120">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
