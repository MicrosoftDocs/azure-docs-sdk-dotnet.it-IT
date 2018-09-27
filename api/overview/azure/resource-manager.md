---
title: Librerie di Azure Resource Manager per .NET
description: Informazioni di riferimento sulle librerie di Azure Resource Manager per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: 6d3a27c5f7ba94f5579723cc4f798826c8bdefd6
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190840"
---
# <a name="azure-resource-manager-libraries-for-net"></a><span data-ttu-id="2a607-103">Librerie di Azure Resource Manager per .NET</span><span class="sxs-lookup"><span data-stu-id="2a607-103">Azure Resource Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="2a607-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2a607-104">Overview</span></span>

<span data-ttu-id="2a607-105">Gestione risorse di Azure consente di usare le risorse incluse nella soluzione come un gruppo.</span><span class="sxs-lookup"><span data-stu-id="2a607-105">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span>  <span data-ttu-id="2a607-106">Per altre informazioni su Resource Manager, vedere [Panoramica di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="2a607-106">For more information about Resource Manager, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="2a607-107">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="2a607-107">Management library</span></span>

<span data-ttu-id="2a607-108">La libreria di Azure Resource Manager per .NET consente di creare, aggiornare, eliminare ed elencare le risorse e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="2a607-108">The Azure Resource Manager library for .NET enables you to create, update, delete, and list resources and resource groups.</span></span>

<span data-ttu-id="2a607-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="2a607-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2a607-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="2a607-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a><span data-ttu-id="2a607-111">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a607-111">Example</span></span>

<span data-ttu-id="2a607-112">Questo esempio crea un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2a607-112">This example creates a new resource group.</span></span>

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
> [<span data-ttu-id="2a607-113">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="2a607-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a><span data-ttu-id="2a607-114">Esempi</span><span class="sxs-lookup"><span data-stu-id="2a607-114">Samples</span></span>

* [<span data-ttu-id="2a607-115">Gestire gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="2a607-115">Manage resource groups</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [<span data-ttu-id="2a607-116">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="2a607-116">Manage resources</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [<span data-ttu-id="2a607-117">Distribuire risorse con modelli ARM</span><span class="sxs-lookup"><span data-stu-id="2a607-117">Deploy resources with ARM templates</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [<span data-ttu-id="2a607-118">Distribuire risorse con modelli ARM (con stato di avanzamento)</span><span class="sxs-lookup"><span data-stu-id="2a607-118">Deploy resources with ARM templates (with progress)</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
