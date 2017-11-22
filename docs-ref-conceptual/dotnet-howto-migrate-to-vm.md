---
title: Eseguire la migrazione di un'applicazione Web ASP.NET a una macchina virtuale di Azure
description: Informazioni su come eseguire la migrazione di un'applicazione Web ASP.NET da locale a una macchina virtuale di Azure.
keywords: Azure .NET, ASP.NET, VM, macchina virtuale, eseguire la migrazione, migrazione
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: virtual-machines
ms.custom: devcenter
ms.openlocfilehash: 718d91b98180a7584f78a2383d430c4700743306
ms.sourcegitcommit: c360a22d5bff6eedd714b28b847d2f26b06665f4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/15/2017
---
# <a name="migrate-an-aspnet-web-application-to-an-azure-virtual-machine"></a><span data-ttu-id="ab7ef-104">Eseguire la migrazione di un'applicazione Web ASP.NET a una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="ab7ef-104">Migrate an ASP.NET Web application to an Azure Virtual Machine</span></span>

<span data-ttu-id="ab7ef-105">Questo documento offre una panoramica su come eseguire la migrazione di un'applicazione Web ASP.NET da locale a una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-105">This document provides an overview of how to migrate an ASP.NET web application from on-premises to an Azure Virtual Machine.</span></span>

## <a name="get-started"></a><span data-ttu-id="ab7ef-106">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="ab7ef-106">Get Started</span></span>

<span data-ttu-id="ab7ef-107">Queste esercitazioni illustrano i passaggi per creare una macchina virtuale (o eseguirne la migrazione), pubblicarvi l'applicazione Web e altre attività che potrebbero essere necessarie per supportare l'applicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-107">These tutorials demonstrate the steps to create (or migrate) a virtual machine, publish your web application to it, and other tasks that may be required to support your application in Azure.</span></span>

- <span data-ttu-id="ab7ef-108">Creare una macchina virtuale per l'applicazione ASP.NET in Azure usando una delle due opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab7ef-108">Create a virtual machine for your ASP.NET application in Azure using one of the following two options:</span></span>
    - [<span data-ttu-id="ab7ef-109">Creare una nuova macchina virtuale per le applicazioni ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ab7ef-109">Create a new virtual machine for ASP.NET Applications</span></span>](https://go.microsoft.com/fwlink/?linkid=863237)
    - [<span data-ttu-id="ab7ef-110">Eseguire la migrazione di una macchina virtuale locale esistente</span><span class="sxs-lookup"><span data-stu-id="ab7ef-110">Migrate an existing on-premises virtual machine</span></span>](https://docs.microsoft.com/azure/site-recovery/tutorial-migrate-on-premises-to-azure)
- [<span data-ttu-id="ab7ef-111">Pubblicare l'app usando Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ab7ef-111">Publish your app using Visual Studio</span></span>](https://go.microsoft.com/fwlink/?linkid=863240)
- [<span data-ttu-id="ab7ef-112">Creare una rete virtuale sicura per le VM</span><span class="sxs-lookup"><span data-stu-id="ab7ef-112">Create a secure virtual network for your VMs</span></span>](https://docs.microsoft.com/azure/virtual-network/virtual-network-get-started-vnet-subnet)
- [<span data-ttu-id="ab7ef-113">Creare una pipeline di integrazione continua/distribuzione continua per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="ab7ef-113">Create a CI/CD pipeline for your application</span></span>](https://docs.microsoft.com/vsts/build-release/apps/cd/deploy-webdeploy-iis-deploygroups)
- [<span data-ttu-id="ab7ef-114">Passare a un set di scalabilità di macchine virtuali per la scalabilità e la disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="ab7ef-114">Move to a VM scale set for high availability and scalability</span></span>](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app)

## <a name="considerations"></a><span data-ttu-id="ab7ef-115">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="ab7ef-115">Considerations</span></span>

### <a name="benefits"></a><span data-ttu-id="ab7ef-116">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="ab7ef-116">Benefits</span></span>

<span data-ttu-id="ab7ef-117">Le macchine virtuali sono il modo più semplice per eseguire la migrazione di un'applicazione da locale al cloud.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-117">Virtual machines offer the easiest path to migrate an application from on-premises to the cloud.</span></span>  <span data-ttu-id="ab7ef-118">Consentono di replicare lo stesso ambiente usato dall'applicazione in locale, eliminando la necessità di mantenere i data center.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-118">They enable you to replicate the same environment your application uses on-premises, while removing the need to maintain your own data centers.</span></span>  <span data-ttu-id="ab7ef-119">I set di scalabilità di macchine virtuali forniscono scalabilità e disponibilità elevata per le applicazioni in esecuzione nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-119">Virtual Machine Scale Sets provide high availability and scalability for applications running in Virtual Machines.</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="ab7ef-120">Dimensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ab7ef-120">Virtual Machine Size</span></span>

<span data-ttu-id="ab7ef-121">Scegliere per la macchina virtuale le dimensioni e il tipo ottimale per il carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-121">Choose the virtual machine size and type that is best optimized for your workload.</span></span>  <span data-ttu-id="ab7ef-122">Per altre informazioni, vedere [Dimensioni per le macchine virtuali Windows in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes).</span><span class="sxs-lookup"><span data-stu-id="ab7ef-122">See [sizes for Windows virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) for more information.</span></span>

### <a name="maintenance"></a><span data-ttu-id="ab7ef-123">Manutenzione </span><span class="sxs-lookup"><span data-stu-id="ab7ef-123">Maintenance</span></span>

<span data-ttu-id="ab7ef-124">Come per un computer locale, l'utente è responsabile della manutenzione e dell'aggiornamento della macchina virtuale<sup>&#42;</sup>,</span><span class="sxs-lookup"><span data-stu-id="ab7ef-124">Just like an on-premises machine, you are responsible for maintaining and updating the virtual machine<sup>&#42;</sup>.</span></span>  <span data-ttu-id="ab7ef-125">ma, se l'applicazione può essere eseguita in un ambiente di piattaforma distribuita come servizio (PaaS), ad esempio il [Servizio app di Azure](https://docs.microsoft.com/azure/app-service/), o in un [contenitore](https://docs.microsoft.com/azure/app-service/containers/), non sarà più necessario.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-125">If your application can run in a Platform as a Service (PaaS) environment such as [Azure App Service](https://docs.microsoft.com/azure/app-service/) or in a [container](https://docs.microsoft.com/azure/app-service/containers/), that will remove this need.</span></span>

<span data-ttu-id="ab7ef-126">*<sup>&#42;</sup>Gli [aggiornamenti automatici del sistema operativo per un set di scalabilità di macchine virtuali di Azure](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) sono attualmente disponibili come servizio in anteprima.*</span><span class="sxs-lookup"><span data-stu-id="ab7ef-126">*<sup>&#42;</sup>[Automatic OS upgrades for virtual machine scale sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) is currently available as a Preview service.*</span></span>

### <a name="virtual-networks"></a><span data-ttu-id="ab7ef-127">Reti virtuali</span><span class="sxs-lookup"><span data-stu-id="ab7ef-127">Virtual Networks</span></span>

<span data-ttu-id="ab7ef-128">Le reti virtuali di Azure consentono di:</span><span class="sxs-lookup"><span data-stu-id="ab7ef-128">Azure Virtual Networks enable you to:</span></span>
- <span data-ttu-id="ab7ef-129">Creare un'infrastruttura ibrida facile da controllare</span><span class="sxs-lookup"><span data-stu-id="ab7ef-129">Build a hybrid infrastructure that you control</span></span>
- <span data-ttu-id="ab7ef-130">Usare indirizzi IP e server DNS personali</span><span class="sxs-lookup"><span data-stu-id="ab7ef-130">Bring your own IP addresses and DNS servers</span></span>
- <span data-ttu-id="ab7ef-131">Creare un ambiente isolato con sicurezza elevata per le applicazioni</span><span class="sxs-lookup"><span data-stu-id="ab7ef-131">Create an isolated and highly-secure environment for your applications</span></span>
- <span data-ttu-id="ab7ef-132">Connettere la VM alla rete locale usando una delle diverse [opzioni di connettività](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)</span><span class="sxs-lookup"><span data-stu-id="ab7ef-132">Connect your VM to your on-premises network using one of several [connectivity options](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)</span></span>
- <span data-ttu-id="ab7ef-133">Integrare la macchina virtuale nella rete locale usando [ExpressRoute](https://azure.microsoft.com/services/expressroute/)</span><span class="sxs-lookup"><span data-stu-id="ab7ef-133">Integrate your virtual machine into your on-premises network using [ExpressRoute](https://azure.microsoft.com/services/expressroute/)</span></span>

<span data-ttu-id="ab7ef-134">Per iniziare, vedere la [documentazione sulla rete virtuale](https://docs.microsoft.com/azure/virtual-network/)</span><span class="sxs-lookup"><span data-stu-id="ab7ef-134">To get started, see the [Virtual Network documentation](https://docs.microsoft.com/azure/virtual-network/)</span></span>

### <a name="active-directory"></a><span data-ttu-id="ab7ef-135">Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab7ef-135">Active Directory</span></span>
<span data-ttu-id="ab7ef-136">Molte applicazioni usano Active Directory per l'autenticazione e la gestione delle identità.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-136">Many applications use Active Directory for authentication and identity management.</span></span>  
- <span data-ttu-id="ab7ef-137">Azure AD Connect consente di integrare le directory locali con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-137">Azure AD Connect enables you to integrate your on-premises directories with Azure Active Directory.</span></span>  <span data-ttu-id="ab7ef-138">Per iniziare, vedere [Integrare le directory locali con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span><span class="sxs-lookup"><span data-stu-id="ab7ef-138">To get started, see [Integrate your on-premises directories with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>  
- <span data-ttu-id="ab7ef-139">In alternativa, [ExpressRoute](https://azure.microsoft.com/services/expressroute/) consente alle applicazioni di accedere all'istanza di Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-139">Alternatively, [ExpressRoute](https://azure.microsoft.com/services/expressroute/) enables your application to access your on-premises Active Directory.</span></span>

### <a name="sql-databases"></a><span data-ttu-id="ab7ef-140">DATABASE SQL</span><span class="sxs-lookup"><span data-stu-id="ab7ef-140">SQL Databases</span></span>

<span data-ttu-id="ab7ef-141">Se l'applicazione usa un database locale, l'app non potrà comunicare con il database per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-141">If your application is using an on-premises database, your app will not be able to talk to it by default.</span></span> <span data-ttu-id="ab7ef-142">È possibile:</span><span class="sxs-lookup"><span data-stu-id="ab7ef-142">You can either:</span></span>
- <span data-ttu-id="ab7ef-143">Configurare una rete ibrida che consente all'applicazione di accedere al database in esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-143">Configure a hybrid network that enables your application to access your database running on-premises.</span></span>  
- <span data-ttu-id="ab7ef-144">Eseguire la migrazione del database ad Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-144">Migrate your database to the Azure.</span></span>  <span data-ttu-id="ab7ef-145">Per altre informazioni, vedere [Eseguire la migrazione del database SQL Server ad Azure](dotnet-howto-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ab7ef-145">See [Migrate your SQL Server database to Azure](dotnet-howto-migrate-sql.md) for more information.</span></span>

### <a name="high-availability-and-scalability"></a><span data-ttu-id="ab7ef-146">Disponibilità e scalabilità elevate</span><span class="sxs-lookup"><span data-stu-id="ab7ef-146">High Availability and Scalability</span></span>

#### <a name="virtual-machine-scale-sets"></a><span data-ttu-id="ab7ef-147">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ab7ef-147">Virtual Machine Scale Sets</span></span>
<span data-ttu-id="ab7ef-148">Per fare in modo che l'applicazione sia a disponibilità elevata e scalabile, eseguire la migrazione dell'immagine della VM a un set di scalabilità di macchine virtuali di Azure per migliorare la disponibilità e la scalabilità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-148">You want to make sure that your application is highly available and can scale, migrate your VM image to an Azure Virtual Machine Scale Set to improve the availability and scalability of your application.</span></span>  <span data-ttu-id="ab7ef-149">I set di scalabilità di macchine virtuali consentono di usare una VM esistente già configurata o di configurare una pipeline di compilazione per compilare un'immagine con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ab7ef-149">VM Scale Sets provide the ability to use an existing VM you’ve already configured or set up a build pipeline to build an image with your application.</span></span>  

<span data-ttu-id="ab7ef-150">Per iniziare, vedere [Distribuire l'applicazione nei set di scalabilità di macchine virtuali](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).</span><span class="sxs-lookup"><span data-stu-id="ab7ef-150">To get started, see [Deploy your application on virtual machine scale sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).</span></span>

#### <a name="centralized-logging"></a><span data-ttu-id="ab7ef-151">Registrazione centralizzata</span><span class="sxs-lookup"><span data-stu-id="ab7ef-151">Centralized Logging</span></span>
<span data-ttu-id="ab7ef-152">Quando si esegue l'applicazione in più istanze, prendere in considerazione la possibilità di archiviare i log in una posizione centralizzata, ad esempio [Archiviazione di Azure](https://docs.microsoft.com/azure/storage/).</span><span class="sxs-lookup"><span data-stu-id="ab7ef-152">When running your application across multiple instances, consider storing your logs in a centralized location such as [Azure Storage](https://docs.microsoft.com/azure/storage/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab7ef-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab7ef-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab7ef-154">Eseguire la migrazione di un database SQL Server ad Azure</span><span class="sxs-lookup"><span data-stu-id="ab7ef-154">Migrate a SQL Server database to Azure</span></span>](dotnet-howto-migrate-sql.md)