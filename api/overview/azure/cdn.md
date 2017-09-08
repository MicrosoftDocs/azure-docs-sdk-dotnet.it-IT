---
title: Librerie della rete CDN di Azure per .NET
description: Informazioni di riferimento sulle librerie della rete CDN di Azure per .NET
keywords: Azure, .NET, SDK, API, rete CDN
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cdn
ms.openlocfilehash: 1582f85c6e25a973fdf0294afb4393e6622e92a0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-cdn-libraries-for-net"></a><span data-ttu-id="3558c-104">Librerie della rete CDN di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="3558c-104">Azure CDN libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="3558c-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="3558c-105">Overview</span></span>

<span data-ttu-id="3558c-106">La rete per la distribuzione di contenuti (rete CDN) di Azure memorizza nella cache il contenuto Web statico in località strategiche per offrire la massima velocità effettiva per la distribuzione del contenuto agli utenti.</span><span class="sxs-lookup"><span data-stu-id="3558c-106">The Azure Content Delivery Network (CDN) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="3558c-107">La rete CDN offre agli sviluppatori una soluzione globale per distribuire contenuto con esigenze di larghezza di banda elevata tramite la memorizzazione di tale contenuto nella cache in nodi fisici ubicati in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="3558c-107">The CDN offers developers a global solution for delivering high-bandwidth content by caching the content at physical nodes across the world.</span></span>

<span data-ttu-id="3558c-108">Per altre informazioni sulla rete CDN di Azure, vedere [Panoramica della rete per la distribuzione di contenuti (rete CDN) di Azure](https://docs.microsoft.com/azure/cdn/cdn-overview).</span><span class="sxs-lookup"><span data-stu-id="3558c-108">To learn more about Azure CDN, see [Overview of the Azure Content Delivery Network](https://docs.microsoft.com/azure/cdn/cdn-overview).</span></span>


## <a name="management-library"></a><span data-ttu-id="3558c-109">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="3558c-109">Management library</span></span>

<span data-ttu-id="3558c-110">È possibile usare la libreria della rete CDN di Azure per .NET per automatizzare la creazione e la gestione di profili ed endpoint di una rete CDN.</span><span class="sxs-lookup"><span data-stu-id="3558c-110">You can use the Azure CDN Library for .NET to automate creation and management of CDN profiles and endpoints.</span></span> 

<span data-ttu-id="3558c-111">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="3558c-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3558c-112">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="3558c-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a><span data-ttu-id="3558c-113">Esempio</span><span class="sxs-lookup"><span data-stu-id="3558c-113">Example</span></span>

<span data-ttu-id="3558c-114">Questo esempio crea un nuovo profilo della rete CDN con un nuovo endpoint che fa riferimento a `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="3558c-114">This example creates a new CDN profile with a new endpoint pointed to `www.contoso.com`.</span></span>

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.Cdn.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

ICdnProfile profileDefinition = azure.CdnProfiles.Define("CdnProfileName")
    .WithRegion(Region.USCentral)
    .WithExistingResourceGroup("ResourceGroupName")
    .WithStandardVerizonSku()
    .WithNewEndpoint("www.contoso.com")
    .Create();

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3558c-115">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="3558c-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a><span data-ttu-id="3558c-116">Esempi</span><span class="sxs-lookup"><span data-stu-id="3558c-116">Samples</span></span>

* [<span data-ttu-id="3558c-117">Introduzione alla rete CDN - Gestire la rete CDN - in .NET</span><span class="sxs-lookup"><span data-stu-id="3558c-117">Getting started with CDN - Manage CDN - in .NET</span></span>](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
