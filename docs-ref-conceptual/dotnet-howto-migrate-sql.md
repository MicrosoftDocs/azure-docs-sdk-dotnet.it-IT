---
title: Eseguire la migrazione di un database SQL Server ad Azure
description: Informazioni su come eseguire la migrazione di un database SQL Server da SQL Server locale ad Azure.
keywords: Azure .NET, ASP.NET, SQL, SQL Server, database SQL, eseguire la migrazione, migrazione
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: sql-database
ms.custom: devcenter
ms.openlocfilehash: d118d39e2168686c851f0daa6cb611f0a0c9d2fc
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2018
ms.locfileid: "29728492"
---
## <a name="migrate-a-sql-server-database-to-azure"></a>Eseguire la migrazione di un database SQL Server ad Azure

Questo breve articolo descrive sinteticamente due opzioni per la migrazione di un database SQL Server ad Azure.

Azure offre due opzioni principali per la migrazione di un database SQL Server di produzione:

1. [SQL Server in VM di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview):un'istanza di SQL Server installata e ospitata in una macchina virtuale Windows in esecuzione in Azure, definita anche infrastruttura distribuita come servizio (IaaS).
2. [Database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview): un servizio completamente gestito di Azure per il database SQL, definito anche piattaforma distribuita come servizio (PaaS).

Entrambi presentano vantaggi e svantaggi che sarà necessario esaminare prima di eseguire la migrazione.

## <a name="get-started"></a>Attività iniziali

Le seguenti sono guide utili per la migrazione, a seconda del servizio usato:

* [Eseguire la migrazione di un database di SQL Server a SQL Server in una VM di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)
* [Eseguire la migrazione di un database SQL Server a un database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-migrate-your-sql-server-database)

I collegamenti seguenti per contenuti concettuali consentono di comprendere meglio le VM:

* [Disponibilità elevata e ripristino di emergenza di SQL Server in Macchine virtuali di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)
* [Performance best practices for SQL Server in Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance) (Procedure consigliate sulle prestazioni per SQL Server nelle macchine virtuali di Azure)
* [Modelli di applicazione e strategie di sviluppo per SQL Server in Macchine virtuali di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-app-patterns-dev-strategies)

I collegamenti seguenti invece offrono utili informazioni sul database SQL di Azure:

* [Creare e gestire database e server di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases)
* [Unità di transazione di database (DTU) e unità di transazione di database elastico (eDTU)](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu)
* [Limiti delle risorse del database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits)

## <a name="choosing-iaas-or-paas"></a>Scelta di IaaS o di PaaS

Quando si valuta la destinazione della migrazione del database, è opportuno determinare se la scelta ottimale sia IaaS o PaaS.

**È consigliabile scegliere SQL Server nelle macchine virtuali di Azure se:**

* Si prevede di trasferire in modalità lift-and-shift il database e le applicazioni con pochissime o nessuna modifica.
* Si preferisce avere il controllo completo sul server di database e sulla VM in cui viene eseguito.
* Si hanno già licenze SQL Server e Windows Server che si intende usare.

**È consigliabile scegliere il database SQL di Azure se:**

* Si prevede di modernizzare le applicazioni e di eseguire la migrazione per usare altri servizi PaaS in Azure.
* Non si vogliono gestire il server di database e la VM in cui viene eseguito.
* Non si hanno licenze SQL Server o Windows Server o si intende lasciar scadere le licenze disponibili.

La tabella seguente descrive le differenze tra ogni servizio in base a un set di scenari.

| Scenario | SQL Server in VM di Azure | database SQL di Azure |
|----------|-------------------------|--------------------|
| Migrazione | Richiede modifiche minime al database. | Può richiedere modifiche al database se si usano funzionalità non disponibili in Azure SQL, come stabilito da [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595), o se si hanno altre dipendenze, ad esempio eseguibili installati in locale.|
| Gestione di disponibilità, ripristino e aggiornamenti | La disponibilità e il ripristino vengono configurati manualmente. Gli aggiornamenti possono essere automatizzati con i [set di scalabilità di macchine virtuali](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade). | Gestita automaticamente. |
| Configurazione del sistema operativo sottostante | Configurazione manuale. | Gestita automaticamente. |
| Gestione delle dimensioni del database | Supporta fino a 64 TB di spazio di archiviazione per ogni istanza di SQL Server. | Supporta 4 TB di spazio di archiviazione prima che sia necessaria una partizione orizzontale. |
| Gestione dei costi | È necessario gestire i costi delle licenze SQL Server, i costi delle licenze Windows Server e i costi delle VM (in base a core, RAM e spazio di archiviazione). | È necessario gestire i costi dei servizi (in base a [eDTU o DTU](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu), spazio di archiviazione e numero di database se si usa un pool elastico).  È anche necessario gestire il costo dei contratti di servizio. |

Per altre informazioni sulle differenze tra le due opzioni, vedere [Scegliere un'opzione di SQL Server cloud: database SQL di Azure o SQL Server in VM di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas).

## <a name="faq"></a>Domande frequenti

* **È ancora possibile usare strumenti come SQL Server Management Studio e SQL Server Reporting Services (SSRS) con SQL Server in VM di Azure o il database SQL di Azure?**

    Sì. Tutti gli strumenti di Microsoft SQL funzionano con entrambi i servizi. SSRS tuttavia non fa parte del database SQL di Azure ed è consigliabile eseguirlo in una VM di Azure e quindi fare in modo che punti all'istanza del database.
    
* **Si vuole passare a PaaS, ma non si è certi che il database sia compatibile. Sono disponibili strumenti adatti?**

    Sì. [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) è uno strumento usato durante la migrazione al database SQL di Azure.  Il [servizio Migrazione del database di Azure](https://azure.microsoft.com/campaigns/database-migration/) è un servizio in anteprima che è possibile usare per IaaS o PaaS.

* **È possibile stimare i costi?**

    Sì.  Il [calcolatore prezzi di Azure](https://azure.microsoft.com/pricing/calculator/) può essere usato per stimare i costi per tutti i servizi di Azure, inclusi servizi di database e VM.
    
## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Scegliere l'opzione di hosting di Azure più adatta](dotnet-howto-choose-migration.md)
