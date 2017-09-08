---
title: Librerie di Ricerca di Azure per .NET
description: Informazioni di riferimento sulle librerie di Ricerca di Azure per .NET
keywords: Azure, .NET, SDK, API, Ricerca
author: spboyer
ms.author: casoper
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 5330e0642bc27c97c4acc0857d4b92e6fc2a027c
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-search-libraries-for-net"></a>Librerie di Ricerca di Azure per .NET

## <a name="overview"></a>Panoramica

[Ricerca di Azure](https://docs.microsoft.com/azure/search/search-what-is-azure-search) è un servizio di ricerca cloud completamente gestito che fornisce un'esperienza di ricerca avanzata sui dati in applicazioni Web, per dispositivi mobili e aziendali.

## <a name="client-library"></a>Libreria client

Usare la libreria client di Ricerca di Azure per accedere ed eseguire operazioni di indicizzazione e di ricerca in un servizio di ricerca, negli indici, nei documenti o in altri oggetti. Per un'introduzione dettagliata, vedere [Come usare Ricerca di Azure da un'applicazione .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Search) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a>Esempio di codice

```csharp
/* Include these 'using' directives:
   using Microsoft.Azure.Search;
   using Microsoft.Azure.Search.Models;
*/

// A service endpoint and an api-key are required on a connection.
// Set them in a config file (not shown) and then connect to the client.
IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
IConfigurationRoot configuration = builder.Build();

SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

// Create an index named hotels
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a>Libreria di gestione

Usare la libreria di gestione di Ricerca di Azure per effettuare il provisioning di un servizio, gestire le chiavi API e modificare le risorse. La gestione dei servizi dipende da Azure Resource Manager per l'identificazione di sottoscrittori e tenant. Sono in genere necessarie anche l'autenticazione e la registrazione dell'applicazione in Azure Active Directory per supportare il flusso di lavoro. Per un'introduzione al provisioning dei servizi di Ricerca di Azure, vedere [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api) (Come usare l'API REST Gestione).

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a>Esempi

 + [Azure Samples / search-dotnet-getting-started](https://github.com/Azure-Samples/search-dotnet-getting-started) (Esempi di Azure / search-dotnet-getting-started)
 + [Azure Samples / search-dotnet-management-api](https://github.com/Azure-Samples/search-dotnet-management-api) (Esempi di Azure / search-dotnet-management-api)

Per altri esempi di ricerca, vedere il [repository di esempi di Azure](https://github.com/Azure-Samples/) in Github.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
