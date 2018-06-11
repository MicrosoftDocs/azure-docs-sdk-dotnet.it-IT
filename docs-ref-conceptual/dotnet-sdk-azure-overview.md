---
title: API .NET di Azure
description: Panoramica delle API di Azure per .NET
keywords: Azure, .NET, SDK, API, NuGet, librerie, pacchetti
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 26360a516220ca9d3e8901e60cb23ecbd02863cd
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2018
ms.locfileid: "29752693"
---
# <a name="azure-net-apis"></a><span data-ttu-id="eab14-104">API .NET di Azure</span><span class="sxs-lookup"><span data-stu-id="eab14-104">Azure .NET APIs</span></span>

<span data-ttu-id="eab14-105">Le API .NET di Azure consentono di usare i servizi di Azure e di gestire le risorse di Azure dal codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eab14-105">The Azure .NET APIs let you use Azure services and manage Azure resources from your application code.</span></span> <span data-ttu-id="eab14-106">Le API sono disponibili come [pacchetti NuGet](/dotnet/api/overview/azure/) per l'uso nei progetti .NET.</span><span class="sxs-lookup"><span data-stu-id="eab14-106">The APIs are available as [NuGet packages](/dotnet/api/overview/azure/) for use in your .NET projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="eab14-107">Gestire le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="eab14-107">Manage Azure resources</span></span>

<span data-ttu-id="eab14-108">Le librerie di Azure per .NET consentono di creare e gestire le risorse di Azure dalle applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="eab14-108">The Azure libraries for .NET let you create and manage Azure resources from your .NET applications.</span></span>

<span data-ttu-id="eab14-109">Molti dei pacchetti per la gestione di risorse di Azure hanno un'interfaccia [Fluent](dotnet-sdk-azure-concepts.md) per configurare le risorse esattamente in base alle specifiche.</span><span class="sxs-lookup"><span data-stu-id="eab14-109">Many of the packages for managing Azure resources have a [fluent](dotnet-sdk-azure-concepts.md) interface to configure resources exactly to your specifications.</span></span> <span data-ttu-id="eab14-110">Ad esempio, per creare una VM Windows, scrivere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="eab14-110">For example, to create a Windows VM you would write the following code:</span></span>

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

<span data-ttu-id="eab14-111">Verificare l'[elenco di servizi .NET](/dotnet/api/overview/azure/) per iniziare a usare immediatamente le librerie con i progetti.</span><span class="sxs-lookup"><span data-stu-id="eab14-111">Review the [.NET service list](/dotnet/api/overview/azure/) to start using the libraries immediately with your projects.</span></span> <span data-ttu-id="eab14-112">Leggere quindi l'[articolo introduttivo](dotnet-sdk-azure-get-started.md) per configurare l'autenticazione ed eseguire codice di esempio nella propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eab14-112">Then read the [get started article](dotnet-sdk-azure-get-started.md) to set up authentication and run sample code against your own Azure subscription.</span></span>  <span data-ttu-id="eab14-113">L'[articolo relativo ai concetti](dotnet-sdk-azure-concepts.md) esamina le convenzioni usate da SDK e illustra come sfruttarle per semplificare il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eab14-113">The [concepts article](dotnet-sdk-azure-concepts.md) goes into the conventions the SDK uses and how to leverage them to simplify your application code.</span></span> <span data-ttu-id="eab14-114">Le nuove funzionalità, le modifiche di rilievo e le istruzioni per la migrazione sono disponibili nelle [note sulla versione](dotnet-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="eab14-114">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

## <a name="consume-azure-services"></a><span data-ttu-id="eab14-115">Utilizzare i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="eab14-115">Consume Azure services</span></span>

<span data-ttu-id="eab14-116">Oltre a usare le API .NET per creare e gestire a livello di codice le risorse in Azure, è quindi possibile usare le API .NET anche per connettere le applicazioni a queste risorse e usarle in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="eab14-116">In addition to using .NET APIs to create and programmatically manage resources within Azure, you can also then use .NET APIs to connect your applications to these resources and use them at runtime.</span></span>  <span data-ttu-id="eab14-117">È ad esempio possibile connettersi a un database SQL o archiviare i dati in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eab14-117">For example, you might connect to a SQL Database or store data within Azure Storage.</span></span>  <span data-ttu-id="eab14-118">È possibile identificare il pacchetto NuGet da usare per un servizio di Azure specifico esplorando l'[elenco completo di API del servizio](/dotnet/api/overview/azure/).</span><span class="sxs-lookup"><span data-stu-id="eab14-118">You can identify which NuGet package to use for a particular Azure service by browsing our [full list of service APIs](/dotnet/api/overview/azure/).</span></span>  

## <a name="samples"></a><span data-ttu-id="eab14-119">Esempi</span><span class="sxs-lookup"><span data-stu-id="eab14-119">Samples</span></span>

<span data-ttu-id="eab14-120">Gli esempi seguenti sono relativi ad attività di automazione comuni con le librerie di Azure per .NET:</span><span class="sxs-lookup"><span data-stu-id="eab14-120">The following samples cover common automation tasks with the Azure libraries for .NET:</span></span>

- [<span data-ttu-id="eab14-121">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="eab14-121">Virtual machines</span></span>](dotnet-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="eab14-122">App Web</span><span class="sxs-lookup"><span data-stu-id="eab14-122">Web apps</span></span>](dotnet-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="eab14-123">Database SQL</span><span class="sxs-lookup"><span data-stu-id="eab14-123">SQL Database</span></span>](dotnet-sdk-azure-sql-database-samples.md)

<span data-ttu-id="eab14-124">Le [informazioni di riferimento](/dotnet/api/overview/azure/?view=azure-dotnet) unificate sono disponibili per tutti i pacchetti nelle librerie di gestione e di servizi.</span><span class="sxs-lookup"><span data-stu-id="eab14-124">A unified [reference](/dotnet/api/overview/azure/?view=azure-dotnet) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="eab14-125">Le nuove funzionalità, le modifiche di rilievo e le istruzioni per la migrazione sono disponibili nelle [note sulla versione](dotnet-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="eab14-125">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

[!include[Contribute and community](includes/contribute.md)]