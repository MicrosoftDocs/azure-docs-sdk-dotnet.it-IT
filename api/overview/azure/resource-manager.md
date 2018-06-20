---
title: Librerie di Azure Resource Manager per .NET
description: Informazioni di riferimento sulle librerie di Azure Resource Manager per .NET
keywords: Azure, .NET, SDK, API, Resource Manager
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f9fe96fcdc94d3d27445f462c5220def9f2966da
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566372"
---
# <a name="azure-resource-manager-libraries-for-net"></a><span data-ttu-id="765c5-104">Librerie di Azure Resource Manager per .NET</span><span class="sxs-lookup"><span data-stu-id="765c5-104">Azure Resource Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="765c5-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="765c5-105">Overview</span></span>

<span data-ttu-id="765c5-106">Gestione risorse di Azure consente di usare le risorse incluse nella soluzione come un gruppo.</span><span class="sxs-lookup"><span data-stu-id="765c5-106">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span>  <span data-ttu-id="765c5-107">Per altre informazioni su Resource Manager, vedere [Panoramica di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="765c5-107">For more information about Resource Manager, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="765c5-108">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="765c5-108">Management library</span></span>

<span data-ttu-id="765c5-109">La libreria di Azure Resource Manager per .NET consente di creare, aggiornare, eliminare ed elencare le risorse e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="765c5-109">The Azure Resource Manager library for .NET enables you to create, update, delete, and list resources and resource groups.</span></span>

<span data-ttu-id="765c5-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="765c5-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="765c5-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="765c5-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a><span data-ttu-id="765c5-112">Esempio</span><span class="sxs-lookup"><span data-stu-id="765c5-112">Example</span></span>

<span data-ttu-id="765c5-113">Questo esempio crea un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="765c5-113">This example creates a new resource group.</span></span>

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.ResourceManager.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IResourceGroup resourceGroup = azure.ResourceGroups
    .Define("ResourceGroupName")
    .WithRegion(Region.USWest)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="765c5-114">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="765c5-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a><span data-ttu-id="765c5-115">Esempi</span><span class="sxs-lookup"><span data-stu-id="765c5-115">Samples</span></span>

* [<span data-ttu-id="765c5-116">Gestire gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="765c5-116">Manage resource groups</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [<span data-ttu-id="765c5-117">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="765c5-117">Manage resources</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [<span data-ttu-id="765c5-118">Distribuire risorse con modelli ARM</span><span class="sxs-lookup"><span data-stu-id="765c5-118">Deploy resources with ARM templates</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [<span data-ttu-id="765c5-119">Distribuire risorse con modelli ARM (con stato di avanzamento)</span><span class="sxs-lookup"><span data-stu-id="765c5-119">Deploy resources with ARM templates (with progress)</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
