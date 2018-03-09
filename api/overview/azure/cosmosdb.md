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
# <a name="azure-cosmosdb-libraries-for-net"></a>Librerie di Azure Cosmos DB per .NET

## <a name="overview"></a>Panoramica

[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) è un archivio dati distribuito e scalabile che supporta vari tipi diversi di database.

[Introduzione a Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-documentdb-dotnet).

## <a name="client-library"></a>Libreria client

Usare la libreria client di Cosmos DB per .NET per accedere ai dati e archiviarli in un archivio dati Cosmos DB esistente.  Per automatizzare la creazione di un nuovo account CosmosDB, usare il portale di Azure, l'interfaccia della riga di comando o PowerShell.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a>Esempio di codice

Questo esempio mostra come connettersi a un database dell'API DocumentDB di Cosmos DB, eseguire la lettura di un documento da una raccolta e deserializzare il documento come un oggetto `Item`.   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>Esempi

* [Develop a Java app using Azure Cosmos DB MongoDB API](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/) (Sviluppare un'app Java con l'API MongoDB di Azure Cosmos DB)

Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) degli esempi di codice per Azure Cosmos DB.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
