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
ms.openlocfilehash: cac6dde85a7b0db2c98d0888cb0ee5c60ee31836
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2018
---
# <a name="azure-virtual-machine-libraries-for-net"></a>Librerie delle macchine virtuali di Azure per .NET

## <a name="overview"></a>Panoramica

Risorse di calcolo su richiesta e scalabili in esecuzione su Linux o Windows.

Per iniziare a usare le macchine virtuali di Azure, vedere [Creare una macchina virtuale Linux con il portale di Azure](https://review.docs.microsoft.com/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-apis"></a>API di gestione

Creare, configurare e aumentare le macchine virtuali Windows e Linux in Azure dal codice con l'API di gestione.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a>Esempio di codice

Creare una VM Windows.

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
> [Esplorare le API di gestione](https://docs.microsoft.com/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a>Esempi

* [Creare e gestire macchine virtuali](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* [Deploy an SSH-enabled VM with a Template with .NET](https://azure.microsoft.com/resources/samples/resource-manager-dotnet-template-deployment/) (Distribuire una macchina virtuale abilitata per SSH con un modello con .NET)

Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=VM) di esempi di macchine virtuali.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
