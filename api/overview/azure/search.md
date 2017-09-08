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
# <a name="azure-search-libraries-for-net"></a><span data-ttu-id="68543-104">Librerie di Ricerca di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="68543-104">Azure Search libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="68543-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="68543-105">Overview</span></span>

<span data-ttu-id="68543-106">[Ricerca di Azure](https://docs.microsoft.com/azure/search/search-what-is-azure-search) è un servizio di ricerca cloud completamente gestito che fornisce un'esperienza di ricerca avanzata sui dati in applicazioni Web, per dispositivi mobili e aziendali.</span><span class="sxs-lookup"><span data-stu-id="68543-106">[Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) is a fully managed cloud search service that provides a rich search experience over data in web, mobile, and enterprise applications.</span></span>

## <a name="client-library"></a><span data-ttu-id="68543-107">Libreria client</span><span class="sxs-lookup"><span data-stu-id="68543-107">Client library</span></span>

<span data-ttu-id="68543-108">Usare la libreria client di Ricerca di Azure per accedere ed eseguire operazioni di indicizzazione e di ricerca in un servizio di ricerca, negli indici, nei documenti o in altri oggetti.</span><span class="sxs-lookup"><span data-stu-id="68543-108">Use the Azure Search client library to access and execute indexing and search operations on a search service, index, documents, or other object.</span></span> <span data-ttu-id="68543-109">Per un'introduzione dettagliata, vedere [Come usare Ricerca di Azure da un'applicazione .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="68543-109">For a step-by-step introduction, see [How to use Azure Search from a .NET application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

<span data-ttu-id="68543-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Search) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="68543-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="68543-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="68543-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a><span data-ttu-id="68543-112">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="68543-112">Code Example</span></span>

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
> [<span data-ttu-id="68543-113">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="68543-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a><span data-ttu-id="68543-114">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="68543-114">Management library</span></span>

<span data-ttu-id="68543-115">Usare la libreria di gestione di Ricerca di Azure per effettuare il provisioning di un servizio, gestire le chiavi API e modificare le risorse.</span><span class="sxs-lookup"><span data-stu-id="68543-115">Use the Azure Search management library to provision a service, manage api-keys, and adjust resources.</span></span> <span data-ttu-id="68543-116">La gestione dei servizi dipende da Azure Resource Manager per l'identificazione di sottoscrittori e tenant.</span><span class="sxs-lookup"><span data-stu-id="68543-116">Service management has a dependency on Azure Resource Manager for subscriber and tenant identification.</span></span> <span data-ttu-id="68543-117">Sono in genere necessarie anche l'autenticazione e la registrazione dell'applicazione in Azure Active Directory per supportare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="68543-117">Typically, authentication and application registration with Azure Active Directory is also necessary to support the workflow.</span></span> <span data-ttu-id="68543-118">Per un'introduzione al provisioning dei servizi di Ricerca di Azure, vedere [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api) (Come usare l'API REST Gestione).</span><span class="sxs-lookup"><span data-stu-id="68543-118">For an introduction to Azure Search service provisioning, see [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api).</span></span>

<span data-ttu-id="68543-119">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="68543-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="68543-120">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="68543-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="68543-121">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="68543-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a><span data-ttu-id="68543-122">Esempi</span><span class="sxs-lookup"><span data-stu-id="68543-122">Samples</span></span>

 + [<span data-ttu-id="68543-123">Azure Samples / search-dotnet-getting-started</span><span class="sxs-lookup"><span data-stu-id="68543-123">Azure Samples / search-dotnet-getting-started</span></span>](https://github.com/Azure-Samples/search-dotnet-getting-started) (Esempi di Azure / search-dotnet-getting-started)
 + [<span data-ttu-id="68543-124">Azure Samples / search-dotnet-management-api</span><span class="sxs-lookup"><span data-stu-id="68543-124">Azure Samples / search-dotnet-management-api</span></span>](https://github.com/Azure-Samples/search-dotnet-management-api) (Esempi di Azure / search-dotnet-management-api)

<span data-ttu-id="68543-125">Per altri esempi di ricerca, vedere il [repository di esempi di Azure](https://github.com/Azure-Samples/) in Github.</span><span class="sxs-lookup"><span data-stu-id="68543-125">Find more search samples in the [Azure samples repository](https://github.com/Azure-Samples/) on Github.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
