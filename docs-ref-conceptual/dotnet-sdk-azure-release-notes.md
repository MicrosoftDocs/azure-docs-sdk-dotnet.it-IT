---
title: Note sulla versione delle librerie di gestione di Azure per .NET | Microsoft Docs
description: "Informazioni sulle novità e sulle modifiche di rilievo nelle librerie di gestione di Azure per .NET."
keywords: Azure, .NET, API, informazioni di riferimento, note, aggiornamenti, deprecare
author: camsoper
ms.author: casoper
manager: douge
ms.assetid: 
ms.service: Azure
ms.devlang: dotnet
ms.topic: reference
ms.technology: Azure
ms.date: 06/20/2017
ms.openlocfilehash: b4a66eb2860673f63a0d11c3cf31486337f36131
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="release-notes"></a><span data-ttu-id="1ebc2-104">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="1ebc2-104">Release Notes</span></span> 

## <a name="feature-availability-and-road-map-as-of-version-100"></a><span data-ttu-id="1ebc2-105">Disponibilità delle funzionalità e roadmap a partire dalla versione 1.0.0</span><span class="sxs-lookup"><span data-stu-id="1ebc2-105">Feature Availability and Road Map as of Version 1.0.0</span></span> ##
### <a name="april-26-2017"></a><span data-ttu-id="1ebc2-106">26 aprile 2017</span><span class="sxs-lookup"><span data-stu-id="1ebc2-106">April 26, 2017</span></span>

<table>
  <tr>
    <th align="left"><span data-ttu-id="1ebc2-107">Servizio | Funzionalità</span><span class="sxs-lookup"><span data-stu-id="1ebc2-107">Service | feature</span></span></th>
    <th align="left"><span data-ttu-id="1ebc2-108">Disponibile a livello generale</span><span class="sxs-lookup"><span data-stu-id="1ebc2-108">Available as GA</span></span></th>
    <th align="left"><span data-ttu-id="1ebc2-109">Disponibile come anteprima</span><span class="sxs-lookup"><span data-stu-id="1ebc2-109">Available as Preview</span></span></th>
    <th align="left"><span data-ttu-id="1ebc2-110">Presto disponibile</span><span class="sxs-lookup"><span data-stu-id="1ebc2-110">Coming soon</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="1ebc2-111">Calcolo</span><span class="sxs-lookup"><span data-stu-id="1ebc2-111">Compute</span></span></td>
    <td><span data-ttu-id="1ebc2-112">Macchine virtuali ed estensioni di VM</span><span class="sxs-lookup"><span data-stu-id="1ebc2-112">Virtual machines and VM extensions</span></span><br><span data-ttu-id="1ebc2-113">set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1ebc2-113">Virtual machine scale sets</span></span><br><span data-ttu-id="1ebc2-114">Dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="1ebc2-114">Managed disks</span></span></td>
    <td></td>
    <td valign="top"><span data-ttu-id="1ebc2-115">Servizi contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="1ebc2-115">Azure container services</span></span><br><span data-ttu-id="1ebc2-116">Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="1ebc2-116">Azure container registry</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1ebc2-117">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="1ebc2-117">Storage</span></span></td>
    <td><span data-ttu-id="1ebc2-118">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1ebc2-118">Storage accounts</span></span></td>
    <td></td>
    <td><span data-ttu-id="1ebc2-119">Crittografia</span><span class="sxs-lookup"><span data-stu-id="1ebc2-119">Encryption</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1ebc2-120">Database SQL</span><span class="sxs-lookup"><span data-stu-id="1ebc2-120">SQL Database</span></span></td>
    <td><span data-ttu-id="1ebc2-121">Database</span><span class="sxs-lookup"><span data-stu-id="1ebc2-121">Databases</span></span><br><span data-ttu-id="1ebc2-122">Firewall</span><span class="sxs-lookup"><span data-stu-id="1ebc2-122">Firewalls</span></span><br><span data-ttu-id="1ebc2-123">Pool elastici</span><span class="sxs-lookup"><span data-stu-id="1ebc2-123">Elastic pools</span></span></td>
    <td></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1ebc2-124">Rete</span><span class="sxs-lookup"><span data-stu-id="1ebc2-124">Networking</span></span></td>
    <td><span data-ttu-id="1ebc2-125">Reti virtuali</span><span class="sxs-lookup"><span data-stu-id="1ebc2-125">Virtual networks</span></span><br><span data-ttu-id="1ebc2-126">Interfacce di rete</span><span class="sxs-lookup"><span data-stu-id="1ebc2-126">Network interfaces</span></span><br><span data-ttu-id="1ebc2-127">Indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="1ebc2-127">IP addresses</span></span><br><span data-ttu-id="1ebc2-128">Tabella di routing</span><span class="sxs-lookup"><span data-stu-id="1ebc2-128">Routing table</span></span><br><span data-ttu-id="1ebc2-129">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="1ebc2-129">Network security groups</span></span><br><span data-ttu-id="1ebc2-130">DNS</span><span class="sxs-lookup"><span data-stu-id="1ebc2-130">DNS</span></span><br><span data-ttu-id="1ebc2-131">Strumenti di gestione traffico</span><span class="sxs-lookup"><span data-stu-id="1ebc2-131">Traffic managers</span></span></td>
    <td valign="top"><span data-ttu-id="1ebc2-132">Servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="1ebc2-132">Load balancers</span></span><br><span data-ttu-id="1ebc2-133">Gateway di applicazione</span><span class="sxs-lookup"><span data-stu-id="1ebc2-133">Application gateways</span></span></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1ebc2-134">Altri servizi</span><span class="sxs-lookup"><span data-stu-id="1ebc2-134">More services</span></span></td>
    <td><span data-ttu-id="1ebc2-135">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="1ebc2-135">Resource Manager</span></span><br><span data-ttu-id="1ebc2-136">Insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="1ebc2-136">Key Vault</span></span><br><span data-ttu-id="1ebc2-137">Redis</span><span class="sxs-lookup"><span data-stu-id="1ebc2-137">Redis</span></span><br><span data-ttu-id="1ebc2-138">RETE CDN</span><span class="sxs-lookup"><span data-stu-id="1ebc2-138">CDN</span></span><br><span data-ttu-id="1ebc2-139">Batch</span><span class="sxs-lookup"><span data-stu-id="1ebc2-139">Batch</span></span></td>
    <td valign="top"><span data-ttu-id="1ebc2-140">App Web del servizio app</span><span class="sxs-lookup"><span data-stu-id="1ebc2-140">App service - Web apps</span></span><br><span data-ttu-id="1ebc2-141">Funzioni</span><span class="sxs-lookup"><span data-stu-id="1ebc2-141">Functions</span></span><br><span data-ttu-id="1ebc2-142">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="1ebc2-142">Service bus</span></span></td>
    <td valign="top"><span data-ttu-id="1ebc2-143">Monitorare</span><span class="sxs-lookup"><span data-stu-id="1ebc2-143">Monitor</span></span><br><span data-ttu-id="1ebc2-144">Controllo degli accessi in base al ruolo per Graph</span><span class="sxs-lookup"><span data-stu-id="1ebc2-144">Graph RBAC</span></span><br><span data-ttu-id="1ebc2-145">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="1ebc2-145">DocumentDB</span></span><br><span data-ttu-id="1ebc2-146">Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="1ebc2-146">Scheduler</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="1ebc2-147">Nozioni fondamentali</span><span class="sxs-lookup"><span data-stu-id="1ebc2-147">Fundamentals</span></span></td>
    <td><span data-ttu-id="1ebc2-148">Autenticazione - Core</span><span class="sxs-lookup"><span data-stu-id="1ebc2-148">Authentication - core</span></span></td>
    <td><span data-ttu-id="1ebc2-149">Metodi asincroni</span><span class="sxs-lookup"><span data-stu-id="1ebc2-149">Async methods</span></span></td>
    <td valign="top"></td>
  </tr>
</table>

> [!WARNING] 
> <span data-ttu-id="1ebc2-150">Le funzionalità in *anteprima* sono contrassegnate nei commenti della documentazione nelle librerie.</span><span class="sxs-lookup"><span data-stu-id="1ebc2-150">*Preview* features are flagged in documentation comments in libraries.</span></span> <span data-ttu-id="1ebc2-151">Queste funzionalità sono soggette a modifiche.</span><span class="sxs-lookup"><span data-stu-id="1ebc2-151">These features are subject to change.</span></span> <span data-ttu-id="1ebc2-152">È possibile che vengano modificate o addirittura rimosse in futuro.</span><span class="sxs-lookup"><span data-stu-id="1ebc2-152">They can be modified in any way (or even removed) in the future.</span></span>

[!include[Contribute and community](includes/contribute.md)]
