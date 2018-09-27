---
title: Librerie di Ricerca di Azure per .NET
description: Informazioni di riferimento sulle librerie di Ricerca di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: search
ms.openlocfilehash: cf622ccb59f10a5270c02fa76d7396345fbb1a9b
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190244"
---
# <a name="azure-search-libraries-for-net"></a><span data-ttu-id="6a1d1-103">Librerie di Ricerca di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="6a1d1-103">Azure Search libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6a1d1-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6a1d1-104">Overview</span></span>

<span data-ttu-id="6a1d1-105">[Ricerca di Azure](https://docs.microsoft.com/azure/search/search-what-is-azure-search) è un servizio di ricerca cloud completamente gestito che fornisce un'esperienza di ricerca avanzata sui dati in applicazioni Web, per dispositivi mobili e aziendali.</span><span class="sxs-lookup"><span data-stu-id="6a1d1-105">[Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) is a fully managed cloud search service that provides a rich search experience over data in web, mobile, and enterprise applications.</span></span>

## <a name="client-library"></a><span data-ttu-id="6a1d1-106">Libreria client</span><span class="sxs-lookup"><span data-stu-id="6a1d1-106">Client library</span></span>

<span data-ttu-id="6a1d1-107">Usare la libreria client di Ricerca di Azure per accedere ed eseguire operazioni di indicizzazione e di ricerca in un servizio di ricerca, negli indici, nei documenti o in altri oggetti.</span><span class="sxs-lookup"><span data-stu-id="6a1d1-107">Use the Azure Search client library to access and execute indexing and search operations on a search service, index, documents, or other object.</span></span> <span data-ttu-id="6a1d1-108">Per un'introduzione dettagliata, vedere [Come usare Ricerca di Azure da un'applicazione .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="6a1d1-108">For a step-by-step introduction, see [How to use Azure Search from a .NET application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

<span data-ttu-id="6a1d1-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Search) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6a1d1-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6a1d1-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="6a1d1-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a><span data-ttu-id="6a1d1-111">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="6a1d1-111">Code Example</span></span>

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
> [<span data-ttu-id="6a1d1-112">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="6a1d1-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a><span data-ttu-id="6a1d1-113">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="6a1d1-113">Management library</span></span>

<span data-ttu-id="6a1d1-114">Usare la libreria di gestione di Ricerca di Azure per effettuare il provisioning di un servizio, gestire le chiavi API e modificare le risorse.</span><span class="sxs-lookup"><span data-stu-id="6a1d1-114">Use the Azure Search management library to provision a service, manage api-keys, and adjust resources.</span></span> <span data-ttu-id="6a1d1-115">La gestione dei servizi dipende da Azure Resource Manager per l'identificazione di sottoscrittori e tenant.</span><span class="sxs-lookup"><span data-stu-id="6a1d1-115">Service management has a dependency on Azure Resource Manager for subscriber and tenant identification.</span></span> <span data-ttu-id="6a1d1-116">Sono in genere necessarie anche l'autenticazione e la registrazione dell'applicazione in Azure Active Directory per supportare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6a1d1-116">Typically, authentication and application registration with Azure Active Directory is also necessary to support the workflow.</span></span> <span data-ttu-id="6a1d1-117">Per un'introduzione al provisioning dei servizi di Ricerca di Azure, vedere [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api) (Come usare l'API REST Gestione).</span><span class="sxs-lookup"><span data-stu-id="6a1d1-117">For an introduction to Azure Search service provisioning, see [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api).</span></span>

<span data-ttu-id="6a1d1-118">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6a1d1-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6a1d1-119">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="6a1d1-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a1d1-120">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="6a1d1-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a><span data-ttu-id="6a1d1-121">Esempi</span><span class="sxs-lookup"><span data-stu-id="6a1d1-121">Samples</span></span>

 + <span data-ttu-id="6a1d1-122">[Azure Samples / search-dotnet-getting-started](https://github.com/Azure-Samples/search-dotnet-getting-started) (Esempi di Azure / search-dotnet-getting-started)</span><span class="sxs-lookup"><span data-stu-id="6a1d1-122">[Azure Samples / search-dotnet-getting-started](https://github.com/Azure-Samples/search-dotnet-getting-started)</span></span>
 + <span data-ttu-id="6a1d1-123">[Azure Samples / search-dotnet-management-api](https://github.com/Azure-Samples/search-dotnet-management-api) (Esempi di Azure / search-dotnet-management-api)</span><span class="sxs-lookup"><span data-stu-id="6a1d1-123">[Azure Samples / search-dotnet-management-api](https://github.com/Azure-Samples/search-dotnet-management-api)</span></span>

<span data-ttu-id="6a1d1-124">Per altri esempi di ricerca, vedere il [repository di esempi di Azure](https://github.com/Azure-Samples/) in Github.</span><span class="sxs-lookup"><span data-stu-id="6a1d1-124">Find more search samples in the [Azure samples repository](https://github.com/Azure-Samples/) on Github.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
