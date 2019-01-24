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
# <a name="azure-cosmos-db-libraries-for-net"></a>Librerie di Azure Cosmos DB per .NET

## <a name="overview"></a>Panoramica

[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) è un servizio di database multimodello e distribuito a livello globale. È progettato per ridimensionare in modo elastico e indipendente velocità effettiva e memoria tra più aree geografiche con un contratto di servizio completo. Azure Cosmos DB consente di archiviare e accedere a database di documenti, con coppie chiave-valore, con colonna ampia e con elementi grafici mediante API e modelli di programmazione. 

[Introduzione a Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).

## <a name="client-library"></a>Libreria client

Usare la libreria client di Azure Cosmos DB per .NET per accedere ai dati e archiviarli in un archivio dati Azure Cosmos DB esistente. Per automatizzare la creazione di un nuovo account Azure Cosmos DB, usare il portale di Azure, l'interfaccia della riga di comando o PowerShell.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

Per installare la versione 2.x:

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

Per installare l'anteprima della versione 3.0 per lo standard .NET: 

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Cosmos -prerelease
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Microsoft.Azure.Cosmos
```


### <a name="code-example"></a>Esempio di codice

Questo esempio mostra come connettersi a un database dell'API SQL Azure Cosmos DB, leggere un documento da una raccolta e deserializzare il documento come oggetto `TodoItem`. Questo esempio usa la versione 2.x di .NET SDK.   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
var todoItem = client.ReadDocumentAsync<TodoItem>(documentUri);
```

Questo esempio si collega a un database API SQL di Azure Cosmos DB esistente, crea un nuovo database e contenitore, legge un elemento dal contenitore e lo deserializza in un oggetto `TodoItem`. Questo esempio usa la versione 3.x di .NET SDK.   

```csharp
using (CosmosClient cosmosClient = new CosmosClient("endpoint", "primaryKey"))
{
    // Read item from container
    CosmosItemResponse<TodoItem> todoItemResponse = await cosmosClient.Databases["DatabaseId"].Containers["ContainerId"].Items.ReadItemAsync<TodoItem>("partitionKeyValue", "ItemId");
}
```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>Esempi

* [Sviluppo di un'app .NET usando l'API SQL di Azure Cosmos DB (versione 2.x)](https://github.com/Azure-Samples/documentdb-dotnet-todo-app/)
* [Sviluppo di un'app .NET usando l'API SQL di Azure Cosmos DB (versione 3.x di anteprima)](https://github.com/Azure-Samples/cosmos-dotnet-todo-app/)
* [Sviluppo di un'app .NET Core usando l'API SQL di Azure Cosmos DB (versione 3.x di anteprima)](https://github.com/Azure-Samples/cosmos-dotnet-core-getting-started)

Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) degli esempi di codice per Azure Cosmos DB.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
