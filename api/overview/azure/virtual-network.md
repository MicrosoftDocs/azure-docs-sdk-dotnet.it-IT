---
title: Librerie della Rete virtuale di Azure per .NET
description: Informazioni di riferimento sulle librerie della Rete virtuale di Azure per .NET
keywords: Azure, .NET, SDK, API, rete virtuale
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: virtual-network
ms.custom: devcenter, svc-overview
ms.openlocfilehash: b67415344ef9cbf8af598a1fd43b6b47023bb071
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2017
---
# <a name="azure-virtual-network-libraries-for-net"></a><span data-ttu-id="f240e-104">Librerie della Rete virtuale di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="f240e-104">Azure Virtual Network libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="f240e-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f240e-105">Overview</span></span>
<span data-ttu-id="f240e-106">Il servizio [Rete virtuale di Azure](/azure/virtual-network/virtual-networks-overview) consente di connettere tra loro le risorse di Azure in modo sicuro con reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="f240e-106">The [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) service enables you to securely connect Azure resources to each other with virtual networks (VNets).</span></span> <span data-ttu-id="f240e-107">Una rete virtuale è una rappresentazione della propria rete nel cloud.</span><span class="sxs-lookup"><span data-stu-id="f240e-107">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="f240e-108">È anche possibile connettere tra loro le reti virtuali in modo che le risorse connesse a una di esse possano comunicare tra loro.</span><span class="sxs-lookup"><span data-stu-id="f240e-108">You can also connect VNets to each other, enabling resources connected to either VNet to communicate with each other.</span></span> 

## <a name="management-library"></a><span data-ttu-id="f240e-109">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="f240e-109">Management library</span></span>

<span data-ttu-id="f240e-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="f240e-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f240e-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="f240e-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Network.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="f240e-112">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="f240e-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Network.Fluent
```

### <a name="code-example"></a><span data-ttu-id="f240e-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="f240e-113">Code Example</span></span>
<span data-ttu-id="f240e-114">Questo esempio illustra come creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="f240e-114">This example shows how you can create a virtual network.</span></span>

```csharp
/* 
  Include these "using" directives...
  
  using Microsoft.Azure.Management.Network.Fluent;
  using Microsoft.Azure.Management.Network.Fluent.Models;
*/
using (NetworkManagementClient client = new NetworkManagementClient(credentials))
{
    // Define VNet
    VirtualNetworkInner vnet = new VirtualNetworkInner()
    {
        Location = "West US",
        AddressSpace = new AddressSpace()
        {
            AddressPrefixes = new List<string>() { "0.0.0.0/16" }
        },

        DhcpOptions = new DhcpOptions()
        {
            DnsServers = new List<string>() { "1.1.1.1", "1.1.2.4" }
        },

        Subnets = new List<Subnet>()
        {
            new Subnet()
            {
                Name = subnet1Name,
                AddressPrefix = "1.0.1.0/24",
            },
            new Subnet()
            {
                Name = subnet2Name,
               AddressPrefix = "1.0.2.0/24",
            }
        }
    };
    
    await client.VirtualNetworks.CreateOrUpdateAsync(resourceGroupName, vNetName, vnet);
}

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f240e-115">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="f240e-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/network/management)

## <a name="samples"></a><span data-ttu-id="f240e-116">Esempi</span><span class="sxs-lookup"><span data-stu-id="f240e-116">Samples</span></span>
- [<span data-ttu-id="f240e-117">Gestire le reti virtuali con subnet</span><span class="sxs-lookup"><span data-stu-id="f240e-117">Managing Virtual Networks with subnets</span></span>](https://github.com/Azure-Samples/network-dotnet-manage-virtual-network)

<span data-ttu-id="f240e-118">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="f240e-118">Explore more [.NET sample code](https://azure.microsoft.com/resources/samples/?platform=dotnet) that you can use in your apps.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console 
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package 

