---
title: API .NET di Azure
description: Panoramica delle API di Azure per .NET
ms.date: 10/19/2017
ms.openlocfilehash: 04997caa99ed60db6ad98cabbc72b36bfbf99f4d
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190134"
---
# <a name="azure-net-apis"></a>API .NET di Azure

Le API .NET di Azure consentono di usare i servizi di Azure e di gestire le risorse di Azure dal codice dell'applicazione. Le API sono disponibili come [pacchetti NuGet](/dotnet/api/overview/azure/) per l'uso nei progetti .NET. 

## <a name="manage-azure-resources"></a>Gestire le risorse di Azure

Le librerie di Azure per .NET consentono di creare e gestire le risorse di Azure dalle applicazioni .NET.

Molti dei pacchetti per la gestione di risorse di Azure hanno un'interfaccia [Fluent](dotnet-sdk-azure-concepts.md) per configurare le risorse esattamente in base alle specifiche. Ad esempio, per creare una VM Windows, scrivere il codice seguente:

```csharp
var windowsVM = azure.VirtualMachines.Define(windowsVmName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithNewPrimaryNetwork("10.0.0.0/28")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithNewPrimaryPublicIPAddress(publicIpDnsLabel)
    .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
    .WithAdminUsername(username)
    .WithAdminPassword(password)
    .WithSize(VirtualMachineSizeTypes.StandardD3V2)
    .Create();
 ```

Verificare l'[elenco di servizi .NET](/dotnet/api/overview/azure/) per iniziare a usare immediatamente le librerie con i progetti. Leggere quindi l'[articolo introduttivo](dotnet-sdk-azure-get-started.md) per configurare l'autenticazione ed eseguire codice di esempio nella propria sottoscrizione di Azure.  L'[articolo relativo ai concetti](dotnet-sdk-azure-concepts.md) esamina le convenzioni usate da SDK e illustra come sfruttarle per semplificare il codice dell'applicazione. Le nuove funzionalità, le modifiche di rilievo e le istruzioni per la migrazione sono disponibili nelle [note sulla versione](dotnet-sdk-azure-release-notes.md).

## <a name="consume-azure-services"></a>Utilizzare i servizi di Azure

Oltre a usare le API .NET per creare e gestire a livello di codice le risorse in Azure, è quindi possibile usare le API .NET anche per connettere le applicazioni a queste risorse e usarle in fase di esecuzione.  È ad esempio possibile connettersi a un database SQL o archiviare i dati in Archiviazione di Azure.  È possibile identificare il pacchetto NuGet da usare per un servizio di Azure specifico esplorando l'[elenco completo di API del servizio](/dotnet/api/overview/azure/).  

## <a name="samples"></a>Esempi

Gli esempi seguenti sono relativi ad attività di automazione comuni con le librerie di Azure per .NET:

- [Macchine virtuali](dotnet-sdk-azure-virtual-machine-samples.md)
- [App Web](dotnet-sdk-azure-web-apps-samples.md)
- [Database SQL](dotnet-sdk-azure-sql-database-samples.md)

Le [informazioni di riferimento](/dotnet/api/overview/azure/?view=azure-dotnet) unificate sono disponibili per tutti i pacchetti nelle librerie di gestione e di servizi. Le nuove funzionalità, le modifiche di rilievo e le istruzioni per la migrazione sono disponibili nelle [note sulla versione](dotnet-sdk-azure-release-notes.md).

[!include[Contribute and community](includes/contribute.md)]