---
title: Librerie di calcolo di Azure per .NET
description: Informazioni di riferimento sulle librerie di calcolo di Azure per .NET
keywords: Azure, .NET, SDK, API, VM, macchine virtuali, calcolo
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: virtual-machines
ms.custom: devcenter, svc-overview
ms.openlocfilehash: d3bad2e94ec8b08bad2a014fb25d400625a3590d
ms.sourcegitcommit: 2d08f2815fa7fab55e09d294fc4d74897df7951d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2017
---
# <a name="azure-virtual-machine-libraries-for-net"></a><span data-ttu-id="30a95-104">Librerie delle macchine virtuali di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="30a95-104">Azure virtual machine libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="30a95-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="30a95-105">Overview</span></span>

<span data-ttu-id="30a95-106">Risorse di calcolo su richiesta e scalabili in esecuzione su Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="30a95-106">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="30a95-107">Per iniziare a usare le macchine virtuali di Azure, vedere [Creare una macchina virtuale Linux con il portale di Azure](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="30a95-107">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="30a95-108">API di gestione</span><span class="sxs-lookup"><span data-stu-id="30a95-108">Management APIs</span></span>

<span data-ttu-id="30a95-109">Creare, configurare e aumentare le macchine virtuali Windows e Linux in Azure dal codice con l'API di gestione.</span><span class="sxs-lookup"><span data-stu-id="30a95-109">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="30a95-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="30a95-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="30a95-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="30a95-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="30a95-112">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="30a95-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a><span data-ttu-id="30a95-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="30a95-113">Code Example</span></span>

<span data-ttu-id="30a95-114">Creare una VM Windows.</span><span class="sxs-lookup"><span data-stu-id="30a95-114">Create a Windows VM.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.Compute.Fluent;
using Microsoft.Azure.Management.Compute.Fluent.Models;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IVirtualMachine windowsVM = azure.VirtualMachines.Define("MyVirtualMachine")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewPrimaryNetwork("10.0.0.0/28")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithNewPrimaryPublicIPAddress("MyIPAddressLabel")
    .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
    .WithAdminUsername("UserName")
    .WithAdminPassword("Password")
    .WithSize(VirtualMachineSizeTypes.StandardD3V2)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="30a95-115">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="30a95-115">Explore the management APIs</span></span>](https://docs.microsoft.com/en-us/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a><span data-ttu-id="30a95-116">Esempi</span><span class="sxs-lookup"><span data-stu-id="30a95-116">Samples</span></span>

* [<span data-ttu-id="30a95-117">Creare e gestire macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="30a95-117">Create and manage virtual machines</span></span>](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* <span data-ttu-id="30a95-118">[Deploy an SSH-enabled VM with a Template with .NET](https://azure.microsoft.com/en-us/resources/samples/resource-manager-dotnet-template-deployment/) (Distribuire una macchina virtuale abilitata per SSH con un modello con .NET)</span><span class="sxs-lookup"><span data-stu-id="30a95-118">[Deploy an SSH-enabled VM with a Template with .NET](https://azure.microsoft.com/en-us/resources/samples/resource-manager-dotnet-template-deployment/)</span></span>

<span data-ttu-id="30a95-119">Visualizzare l'[elenco completo](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM) di esempi di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="30a95-119">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM) of virtual machine samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
