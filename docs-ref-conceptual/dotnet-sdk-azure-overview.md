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
# <a name="azure-net-apis"></a><span data-ttu-id="b5f13-103">API .NET di Azure</span><span class="sxs-lookup"><span data-stu-id="b5f13-103">Azure .NET APIs</span></span>

<span data-ttu-id="b5f13-104">Le API .NET di Azure consentono di usare i servizi di Azure e di gestire le risorse di Azure dal codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b5f13-104">The Azure .NET APIs let you use Azure services and manage Azure resources from your application code.</span></span> <span data-ttu-id="b5f13-105">Le API sono disponibili come [pacchetti NuGet](/dotnet/api/overview/azure/) per l'uso nei progetti .NET.</span><span class="sxs-lookup"><span data-stu-id="b5f13-105">The APIs are available as [NuGet packages](/dotnet/api/overview/azure/) for use in your .NET projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="b5f13-106">Gestire le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="b5f13-106">Manage Azure resources</span></span>

<span data-ttu-id="b5f13-107">Le librerie di Azure per .NET consentono di creare e gestire le risorse di Azure dalle applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="b5f13-107">The Azure libraries for .NET let you create and manage Azure resources from your .NET applications.</span></span>

<span data-ttu-id="b5f13-108">Molti dei pacchetti per la gestione di risorse di Azure hanno un'interfaccia [Fluent](dotnet-sdk-azure-concepts.md) per configurare le risorse esattamente in base alle specifiche.</span><span class="sxs-lookup"><span data-stu-id="b5f13-108">Many of the packages for managing Azure resources have a [fluent](dotnet-sdk-azure-concepts.md) interface to configure resources exactly to your specifications.</span></span> <span data-ttu-id="b5f13-109">Ad esempio, per creare una VM Windows, scrivere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="b5f13-109">For example, to create a Windows VM you would write the following code:</span></span>

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

<span data-ttu-id="b5f13-110">Verificare l'[elenco di servizi .NET](/dotnet/api/overview/azure/) per iniziare a usare immediatamente le librerie con i progetti.</span><span class="sxs-lookup"><span data-stu-id="b5f13-110">Review the [.NET service list](/dotnet/api/overview/azure/) to start using the libraries immediately with your projects.</span></span> <span data-ttu-id="b5f13-111">Leggere quindi l'[articolo introduttivo](dotnet-sdk-azure-get-started.md) per configurare l'autenticazione ed eseguire codice di esempio nella propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5f13-111">Then read the [get started article](dotnet-sdk-azure-get-started.md) to set up authentication and run sample code against your own Azure subscription.</span></span>  <span data-ttu-id="b5f13-112">L'[articolo relativo ai concetti](dotnet-sdk-azure-concepts.md) esamina le convenzioni usate da SDK e illustra come sfruttarle per semplificare il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b5f13-112">The [concepts article](dotnet-sdk-azure-concepts.md) goes into the conventions the SDK uses and how to leverage them to simplify your application code.</span></span> <span data-ttu-id="b5f13-113">Le nuove funzionalità, le modifiche di rilievo e le istruzioni per la migrazione sono disponibili nelle [note sulla versione](dotnet-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="b5f13-113">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

## <a name="consume-azure-services"></a><span data-ttu-id="b5f13-114">Utilizzare i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="b5f13-114">Consume Azure services</span></span>

<span data-ttu-id="b5f13-115">Oltre a usare le API .NET per creare e gestire a livello di codice le risorse in Azure, è quindi possibile usare le API .NET anche per connettere le applicazioni a queste risorse e usarle in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b5f13-115">In addition to using .NET APIs to create and programmatically manage resources within Azure, you can also then use .NET APIs to connect your applications to these resources and use them at runtime.</span></span>  <span data-ttu-id="b5f13-116">È ad esempio possibile connettersi a un database SQL o archiviare i dati in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5f13-116">For example, you might connect to a SQL Database or store data within Azure Storage.</span></span>  <span data-ttu-id="b5f13-117">È possibile identificare il pacchetto NuGet da usare per un servizio di Azure specifico esplorando l'[elenco completo di API del servizio](/dotnet/api/overview/azure/).</span><span class="sxs-lookup"><span data-stu-id="b5f13-117">You can identify which NuGet package to use for a particular Azure service by browsing our [full list of service APIs](/dotnet/api/overview/azure/).</span></span>  

## <a name="samples"></a><span data-ttu-id="b5f13-118">Esempi</span><span class="sxs-lookup"><span data-stu-id="b5f13-118">Samples</span></span>

<span data-ttu-id="b5f13-119">Gli esempi seguenti sono relativi ad attività di automazione comuni con le librerie di Azure per .NET:</span><span class="sxs-lookup"><span data-stu-id="b5f13-119">The following samples cover common automation tasks with the Azure libraries for .NET:</span></span>

- [<span data-ttu-id="b5f13-120">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="b5f13-120">Virtual machines</span></span>](dotnet-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="b5f13-121">App Web</span><span class="sxs-lookup"><span data-stu-id="b5f13-121">Web apps</span></span>](dotnet-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="b5f13-122">Database SQL</span><span class="sxs-lookup"><span data-stu-id="b5f13-122">SQL Database</span></span>](dotnet-sdk-azure-sql-database-samples.md)

<span data-ttu-id="b5f13-123">Le [informazioni di riferimento](/dotnet/api/overview/azure/?view=azure-dotnet) unificate sono disponibili per tutti i pacchetti nelle librerie di gestione e di servizi.</span><span class="sxs-lookup"><span data-stu-id="b5f13-123">A unified [reference](/dotnet/api/overview/azure/?view=azure-dotnet) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="b5f13-124">Le nuove funzionalità, le modifiche di rilievo e le istruzioni per la migrazione sono disponibili nelle [note sulla versione](dotnet-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="b5f13-124">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

[!include[Contribute and community](includes/contribute.md)]