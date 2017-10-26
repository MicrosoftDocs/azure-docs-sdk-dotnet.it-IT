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
ms.openlocfilehash: b8caa9a46b858c2ea1f14e83880bd69d83f6a5e9
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2017
---
# <a name="azure-virtual-machine-libraries-for-net"></a><span data-ttu-id="a5c98-104">Librerie delle macchine virtuali di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="a5c98-104">Azure virtual machine libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="a5c98-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a5c98-105">Overview</span></span>

<span data-ttu-id="a5c98-106">Risorse di calcolo su richiesta e scalabili in esecuzione su Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="a5c98-106">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="a5c98-107">Per iniziare a usare le macchine virtuali di Azure, vedere [Creare una macchina virtuale Linux con il portale di Azure](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="a5c98-107">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="a5c98-108">API di gestione</span><span class="sxs-lookup"><span data-stu-id="a5c98-108">Management APIs</span></span>

<span data-ttu-id="a5c98-109">Creare, configurare e aumentare le macchine virtuali Windows e Linux in Azure dal codice con l'API di gestione.</span><span class="sxs-lookup"><span data-stu-id="a5c98-109">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="a5c98-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="a5c98-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a5c98-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="a5c98-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="a5c98-112">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="a5c98-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a><span data-ttu-id="a5c98-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="a5c98-113">Code Example</span></span>

<span data-ttu-id="a5c98-114">Creare una VM Windows.</span><span class="sxs-lookup"><span data-stu-id="a5c98-114">Create a Windows VM.</span></span>

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
> [<span data-ttu-id="a5c98-115">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="a5c98-115">Explore the management APIs</span></span>](https://review.docs.microsoft.com/en-us/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a><span data-ttu-id="a5c98-116">Esempi</span><span class="sxs-lookup"><span data-stu-id="a5c98-116">Samples</span></span>

* [<span data-ttu-id="a5c98-117">Creare e gestire macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="a5c98-117">Create and manage virtual machines</span></span>](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* <span data-ttu-id="a5c98-118">[Deploy an SSH-enabled VM with a Template with .NET](https://azure.microsoft.com/en-us/resources/samples/resource-manager-dotnet-template-deployment/) (Distribuire una macchina virtuale abilitata per SSH con un modello con .NET)</span><span class="sxs-lookup"><span data-stu-id="a5c98-118">[Deploy an SSH-enabled VM with a Template with .NET](https://azure.microsoft.com/en-us/resources/samples/resource-manager-dotnet-template-deployment/)</span></span>

<span data-ttu-id="a5c98-119">Visualizzare l'[elenco completo](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM) di esempi di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a5c98-119">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM) of virtual machine samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
