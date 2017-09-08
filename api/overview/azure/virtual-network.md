---
title: Librerie della Rete virtuale di Azure per .NET
description: Informazioni di riferimento sulle librerie della Rete virtuale di Azure per .NET
keywords: Azure, .NET, SDK, API, rete virtuale
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/01/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: ea605dbd632ef4deb9c97c8de3474246dd4be30d
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-virtual-network-libraries-for-net"></a>Librerie della Rete virtuale di Azure per .NET

## <a name="overview"></a>Panoramica
Il servizio [Rete virtuale di Azure](/azure/virtual-network/virtual-networks-overview) consente di connettere tra loro le risorse di Azure in modo sicuro con reti virtuali. Una rete virtuale è una rappresentazione della propria rete nel cloud. È anche possibile connettere tra loro le reti virtuali in modo che le risorse connesse a una di esse possano comunicare tra loro. 

## <a name="management-library"></a>Libreria di gestione

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.Network.Fluent
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Network.Fluent
```

### <a name="code-example"></a>Esempio di codice
Questo esempio illustra come creare una rete virtuale.

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
> [Esplorare le API di gestione](/dotnet/api/overview/azure/network/management)

## <a name="samples"></a>Esempi
- [Gestire le reti virtuali con subnet](https://github.com/Azure-Samples/network-dotnet-manage-virtual-network)

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console 
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package 

