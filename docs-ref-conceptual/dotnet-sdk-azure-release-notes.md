---
title: Note sulla versione delle librerie di gestione di Azure per .NET | Microsoft Docs
description: Informazioni sulle novità e sulle modifiche di rilievo nelle librerie di gestione di Azure per .NET.
ms.date: 10/19/2017
ms.openlocfilehash: dac9dee9c25fc349dedd50d6007f25c7d15b0928
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190674"
---
# <a name="release-notes"></a><span data-ttu-id="b5acc-103">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="b5acc-103">Release Notes</span></span> 

## <a name="feature-availability-and-road-map-as-of-version-100"></a><span data-ttu-id="b5acc-104">Disponibilità delle funzionalità e roadmap a partire dalla versione 1.0.0</span><span class="sxs-lookup"><span data-stu-id="b5acc-104">Feature Availability and Road Map as of Version 1.0.0</span></span> ##
### <a name="april-26-2017"></a><span data-ttu-id="b5acc-105">26 aprile 2017</span><span class="sxs-lookup"><span data-stu-id="b5acc-105">April 26, 2017</span></span>

<table>
  <tr>
    <th align="left"><span data-ttu-id="b5acc-106">Servizio | Funzionalità</span><span class="sxs-lookup"><span data-stu-id="b5acc-106">Service | feature</span></span></th>
    <th align="left"><span data-ttu-id="b5acc-107">Disponibile a livello generale</span><span class="sxs-lookup"><span data-stu-id="b5acc-107">Available as GA</span></span></th>
    <th align="left"><span data-ttu-id="b5acc-108">Disponibile come anteprima</span><span class="sxs-lookup"><span data-stu-id="b5acc-108">Available as Preview</span></span></th>
    <th align="left"><span data-ttu-id="b5acc-109">Presto disponibile</span><span class="sxs-lookup"><span data-stu-id="b5acc-109">Coming soon</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="b5acc-110">Calcolo</span><span class="sxs-lookup"><span data-stu-id="b5acc-110">Compute</span></span></td>
    <td><span data-ttu-id="b5acc-111">Macchine virtuali ed estensioni di VM</span><span class="sxs-lookup"><span data-stu-id="b5acc-111">Virtual machines and VM extensions</span></span><br><span data-ttu-id="b5acc-112">set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="b5acc-112">Virtual machine scale sets</span></span><br><span data-ttu-id="b5acc-113">Dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="b5acc-113">Managed disks</span></span></td>
    <td></td>
    <td valign="top"><span data-ttu-id="b5acc-114">Servizi contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="b5acc-114">Azure container services</span></span><br><span data-ttu-id="b5acc-115">Registro Azure Container</span><span class="sxs-lookup"><span data-stu-id="b5acc-115">Azure container registry</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b5acc-116">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="b5acc-116">Storage</span></span></td>
    <td><span data-ttu-id="b5acc-117">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="b5acc-117">Storage accounts</span></span></td>
    <td></td>
    <td><span data-ttu-id="b5acc-118">Crittografia</span><span class="sxs-lookup"><span data-stu-id="b5acc-118">Encryption</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b5acc-119">Database SQL</span><span class="sxs-lookup"><span data-stu-id="b5acc-119">SQL Database</span></span></td>
    <td><span data-ttu-id="b5acc-120">Database</span><span class="sxs-lookup"><span data-stu-id="b5acc-120">Databases</span></span><br><span data-ttu-id="b5acc-121">Firewall</span><span class="sxs-lookup"><span data-stu-id="b5acc-121">Firewalls</span></span><br><span data-ttu-id="b5acc-122">Pool elastici</span><span class="sxs-lookup"><span data-stu-id="b5acc-122">Elastic pools</span></span></td>
    <td></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b5acc-123">Rete</span><span class="sxs-lookup"><span data-stu-id="b5acc-123">Networking</span></span></td>
    <td><span data-ttu-id="b5acc-124">Reti virtuali</span><span class="sxs-lookup"><span data-stu-id="b5acc-124">Virtual networks</span></span><br><span data-ttu-id="b5acc-125">Interfacce di rete</span><span class="sxs-lookup"><span data-stu-id="b5acc-125">Network interfaces</span></span><br><span data-ttu-id="b5acc-126">Indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="b5acc-126">IP addresses</span></span><br><span data-ttu-id="b5acc-127">Tabella di routing</span><span class="sxs-lookup"><span data-stu-id="b5acc-127">Routing table</span></span><br><span data-ttu-id="b5acc-128">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="b5acc-128">Network security groups</span></span><br><span data-ttu-id="b5acc-129">DNS</span><span class="sxs-lookup"><span data-stu-id="b5acc-129">DNS</span></span><br><span data-ttu-id="b5acc-130">Strumenti di gestione traffico</span><span class="sxs-lookup"><span data-stu-id="b5acc-130">Traffic managers</span></span></td>
    <td valign="top"><span data-ttu-id="b5acc-131">Servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="b5acc-131">Load balancers</span></span><br><span data-ttu-id="b5acc-132">Gateway di applicazione</span><span class="sxs-lookup"><span data-stu-id="b5acc-132">Application gateways</span></span></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b5acc-133">Altri servizi</span><span class="sxs-lookup"><span data-stu-id="b5acc-133">More services</span></span></td>
    <td><span data-ttu-id="b5acc-134">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="b5acc-134">Resource Manager</span></span><br><span data-ttu-id="b5acc-135">Key Vault</span><span class="sxs-lookup"><span data-stu-id="b5acc-135">Key Vault</span></span><br><span data-ttu-id="b5acc-136">Redis</span><span class="sxs-lookup"><span data-stu-id="b5acc-136">Redis</span></span><br><span data-ttu-id="b5acc-137">RETE CDN</span><span class="sxs-lookup"><span data-stu-id="b5acc-137">CDN</span></span><br><span data-ttu-id="b5acc-138">Batch</span><span class="sxs-lookup"><span data-stu-id="b5acc-138">Batch</span></span></td>
    <td valign="top"><span data-ttu-id="b5acc-139">App Web del servizio app</span><span class="sxs-lookup"><span data-stu-id="b5acc-139">App service - Web apps</span></span><br><span data-ttu-id="b5acc-140">Funzioni</span><span class="sxs-lookup"><span data-stu-id="b5acc-140">Functions</span></span><br><span data-ttu-id="b5acc-141">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="b5acc-141">Service bus</span></span></td>
    <td valign="top"><span data-ttu-id="b5acc-142">Monitorare</span><span class="sxs-lookup"><span data-stu-id="b5acc-142">Monitor</span></span><br><span data-ttu-id="b5acc-143">Controllo degli accessi in base al ruolo per Graph</span><span class="sxs-lookup"><span data-stu-id="b5acc-143">Graph RBAC</span></span><br><span data-ttu-id="b5acc-144">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b5acc-144">Azure Cosmos DB</span></span><br><span data-ttu-id="b5acc-145">Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="b5acc-145">Scheduler</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b5acc-146">Nozioni fondamentali</span><span class="sxs-lookup"><span data-stu-id="b5acc-146">Fundamentals</span></span></td>
    <td><span data-ttu-id="b5acc-147">Autenticazione - Core</span><span class="sxs-lookup"><span data-stu-id="b5acc-147">Authentication - core</span></span></td>
    <td><span data-ttu-id="b5acc-148">Metodi asincroni</span><span class="sxs-lookup"><span data-stu-id="b5acc-148">Async methods</span></span></td>
    <td valign="top"></td>
  </tr>
</table>

> [!WARNING] 
> <span data-ttu-id="b5acc-149">Le funzionalità in *anteprima* sono contrassegnate nei commenti della documentazione nelle librerie.</span><span class="sxs-lookup"><span data-stu-id="b5acc-149">*Preview* features are flagged in documentation comments in libraries.</span></span> <span data-ttu-id="b5acc-150">Queste funzionalità sono soggette a modifiche.</span><span class="sxs-lookup"><span data-stu-id="b5acc-150">These features are subject to change.</span></span> <span data-ttu-id="b5acc-151">È possibile che vengano modificate o addirittura rimosse in futuro.</span><span class="sxs-lookup"><span data-stu-id="b5acc-151">They can be modified in any way (or even removed) in the future.</span></span>

[!include[Contribute and community](includes/contribute.md)]
