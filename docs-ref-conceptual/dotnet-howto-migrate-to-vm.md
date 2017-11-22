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
# <a name="migrate-an-aspnet-web-application-to-an-azure-virtual-machine"></a>Eseguire la migrazione di un'applicazione Web ASP.NET a una macchina virtuale di Azure

Questo documento offre una panoramica su come eseguire la migrazione di un'applicazione Web ASP.NET da locale a una macchina virtuale di Azure.

## <a name="get-started"></a>Attività iniziali

Queste esercitazioni illustrano i passaggi per creare una macchina virtuale (o eseguirne la migrazione), pubblicarvi l'applicazione Web e altre attività che potrebbero essere necessarie per supportare l'applicazione in Azure.

- Creare una macchina virtuale per l'applicazione ASP.NET in Azure usando una delle due opzioni seguenti:
    - [Creare una nuova macchina virtuale per le applicazioni ASP.NET](https://go.microsoft.com/fwlink/?linkid=863237)
    - [Eseguire la migrazione di una macchina virtuale locale esistente](https://docs.microsoft.com/azure/site-recovery/tutorial-migrate-on-premises-to-azure)
- [Pubblicare l'app usando Visual Studio](https://go.microsoft.com/fwlink/?linkid=863240)
- [Creare una rete virtuale sicura per le VM](https://docs.microsoft.com/azure/virtual-network/virtual-network-get-started-vnet-subnet)
- [Creare una pipeline di integrazione continua/distribuzione continua per l'applicazione](https://docs.microsoft.com/vsts/build-release/apps/cd/deploy-webdeploy-iis-deploygroups)
- [Passare a un set di scalabilità di macchine virtuali per la scalabilità e la disponibilità elevata](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app)

## <a name="considerations"></a>Considerazioni

### <a name="benefits"></a>Vantaggi

Le macchine virtuali sono il modo più semplice per eseguire la migrazione di un'applicazione da locale al cloud.  Consentono di replicare lo stesso ambiente usato dall'applicazione in locale, eliminando la necessità di mantenere i data center.  I set di scalabilità di macchine virtuali forniscono scalabilità e disponibilità elevata per le applicazioni in esecuzione nelle macchine virtuali.

### <a name="virtual-machine-size"></a>Dimensioni della macchina virtuale

Scegliere per la macchina virtuale le dimensioni e il tipo ottimale per il carico di lavoro.  Per altre informazioni, vedere [Dimensioni per le macchine virtuali Windows in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes).

### <a name="maintenance"></a>Manutenzione 

Come per un computer locale, l'utente è responsabile della manutenzione e dell'aggiornamento della macchina virtuale<sup>&#42;</sup>,  ma, se l'applicazione può essere eseguita in un ambiente di piattaforma distribuita come servizio (PaaS), ad esempio il [Servizio app di Azure](https://docs.microsoft.com/azure/app-service/), o in un [contenitore](https://docs.microsoft.com/azure/app-service/containers/), non sarà più necessario.

*<sup>&#42;</sup>Gli [aggiornamenti automatici del sistema operativo per un set di scalabilità di macchine virtuali di Azure](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) sono attualmente disponibili come servizio in anteprima.*

### <a name="virtual-networks"></a>Reti virtuali

Le reti virtuali di Azure consentono di:
- Creare un'infrastruttura ibrida facile da controllare
- Usare indirizzi IP e server DNS personali
- Creare un ambiente isolato con sicurezza elevata per le applicazioni
- Connettere la VM alla rete locale usando una delle diverse [opzioni di connettività](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)
- Integrare la macchina virtuale nella rete locale usando [ExpressRoute](https://azure.microsoft.com/services/expressroute/)

Per iniziare, vedere la [documentazione sulla rete virtuale](https://docs.microsoft.com/azure/virtual-network/)

### <a name="active-directory"></a>Active Directory
Molte applicazioni usano Active Directory per l'autenticazione e la gestione delle identità.  
- Azure AD Connect consente di integrare le directory locali con Azure Active Directory.  Per iniziare, vedere [Integrare le directory locali con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).  
- In alternativa, [ExpressRoute](https://azure.microsoft.com/services/expressroute/) consente alle applicazioni di accedere all'istanza di Active Directory locale.

### <a name="sql-databases"></a>DATABASE SQL

Se l'applicazione usa un database locale, l'app non potrà comunicare con il database per impostazione predefinita. È possibile:
- Configurare una rete ibrida che consente all'applicazione di accedere al database in esecuzione in locale.  
- Eseguire la migrazione del database ad Azure.  Per altre informazioni, vedere [Eseguire la migrazione del database SQL Server ad Azure](dotnet-howto-migrate-sql.md).

### <a name="high-availability-and-scalability"></a>Disponibilità e scalabilità elevate

#### <a name="virtual-machine-scale-sets"></a>Set di scalabilità di macchine virtuali
Per fare in modo che l'applicazione sia a disponibilità elevata e scalabile, eseguire la migrazione dell'immagine della VM a un set di scalabilità di macchine virtuali di Azure per migliorare la disponibilità e la scalabilità dell'applicazione.  I set di scalabilità di macchine virtuali consentono di usare una VM esistente già configurata o di configurare una pipeline di compilazione per compilare un'immagine con l'applicazione.  

Per iniziare, vedere [Distribuire l'applicazione nei set di scalabilità di macchine virtuali](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).

#### <a name="centralized-logging"></a>Registrazione centralizzata
Quando si esegue l'applicazione in più istanze, prendere in considerazione la possibilità di archiviare i log in una posizione centralizzata, ad esempio [Archiviazione di Azure](https://docs.microsoft.com/azure/storage/).

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Eseguire la migrazione di un database SQL Server ad Azure](dotnet-howto-migrate-sql.md)