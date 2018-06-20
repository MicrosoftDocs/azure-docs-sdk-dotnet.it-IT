---
title: Scegliere l'opzione di hosting di Azure più adatta
description: Informazioni sul percorso di migrazione ad Azure più adatto per l'applicazione Web ASP.NET.
keywords: Azure .NET, ASP.NET, servizio app, VM, macchina virtuale, app Web, eseguire la migrazione, migrazione
author: CESARDELATORRE
manager: wpickett
ms.author: cesardl
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, casoper
ms.openlocfilehash: dbf54bb1a6e3d612ef8363a6b30e06b388b4490f
ms.sourcegitcommit: 3e904e6e4f04f1c92d729459434c85faff32e386
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/09/2017
ms.locfileid: "26588464"
---
# <a name="choose-the-right-azure-hosting-option"></a>Scegliere l'opzione di hosting di Azure più adatta

Questo documento offre diverse considerazioni e confronti tra le scelte disponibili in Azure quando si esegue la migrazione delle applicazioni .NET Framework esistenti da locale ad Azure.

Gli aspetti fondamentali da tenere presenti quando si esegue la migrazione ad Azure di applicazioni .NET esistenti sono:

1.  Opzioni di calcolo
2.  Opzioni di database
3.  Considerazioni relative alla rete e alla sicurezza
4.  Considerazioni relative all'autenticazione e all'autorizzazione

## <a name="compute-choices"></a>Opzioni di calcolo

Quando si esegue la migrazione ad Azure di applicazioni .NET Framework esistenti, sono possibili più scelte.  Poiché tuttavia .NET Framework dipende da Windows, le scelte seguenti sono limitate ai servizi di calcolo basati su Windows.

La tabella seguente include diversi confronti e suggerimenti per scegliere il percorso di migrazione di calcolo adatto per l'applicazione .NET esistente.

|                 | Macchine virtuali di Azure | Servizio app di Azure | Contenitori Windows |
|-----------------|-----------|-------------------|--------------------|
|Quando usare le autorizzazioni      |<ul><li>L'applicazione dipende fortemente dal server e dalle installazioni MSI locali.</li><li>Si vuole semplificare il più possibile il percorso di migrazione dell'applicazione</li></ul>|L'app non dipende in alcun modo dal server, è solo un'app Web ASP.NET pulita (MVC, WebForm) o un'app a più livelli (API Web, WCF) che accede a un server di database. |<ul><li>L'applicazione ha dipendenze dal server originale, ma tali dipendenze possono essere incluse nell'immagine Windows di Docker.</li><li>Si vuole modernizzare l'app in modo che sia [pronta per DevOps cloud](https://docs.microsoft.com/dotnet/standard/modernize-with-azure-and-containers/lift-and-shift-existing-apps-devops/reasons-to-lift-and-shift-existing-net-apps-to-cloud-devops-ready-applications).</li></ul>|
|Vantaggi  |<ul><li>Percorso di migrazione molto semplice</li><li>Ambiente familiare. L'ambiente di distribuzione è una VM e quindi molto simile ai server locali.</li></ul> |Manutenzione PaaS continua, massima semplicità di gestione e ridimensionamento delle app in Azure. |<ul><li>Pronti per il futuro e per DevOps cloud con dipendenze incluse nei contenitori dell'app.</li><li>Quasi nessuna necessità di effettuare il refactoring del codice .NET /C#.</li></ul> |
|Svantaggi             |Si tratta di IaaS. La manutenzione è costosa. È necessario gestire l'infrastruttura di VM a livello di rete, servizio di bilanciamento del carico, aumento del numero di istanze, gestione IIS e così via. |<ul><li>Non tutte le app sono [supportate](http://www.migratetoazure.net/ReadinessAssessment)</li><li>Potrebbe essere necessario effettuare il refactoring e modificare leggermente l'architettura di alcune app, in modo che supportino il servizio app di Azure.</li></ul> |<ul><li>Curva di apprendimento delle competenze di Docker</li><li>Alcune impostazioni del codice e di configurazione dell'app vengono modificate</li></ul>|
|Requisiti |VM Windows Server con gli stessi requisiti dell'app per l'ambiente locale | Requisiti del servizio app di Azure specificati nell'[analisi della compatibilità per il servizio app di Azure](https://www.migratetoazure.net/Resources). |<ul><li>[Windows Server 2016 with Containers - VM di Azure](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WindowsServer?tab=Overview)<br />oppure</li><li>[Servizio contenitore di Azure](https://azure.microsoft.com/services/container-service/) (agente di orchestrazione Kubernetes)<br />oppure<li>[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)</li></ul> |
|Come eseguire la migrazione |Vedere [Eseguire la migrazione a macchine virtuali di Azure](https://go.microsoft.com/fwlink/?linkid=862531) | Vedere [Eseguire la migrazione al servizio app di Azure](https://go.microsoft.com/fwlink/?linkid=862532) | Seguire le considerazioni, gli scenari e le procedure dettagliate illustrati in [Modernizing existing .NET apps with Azure and Windows Containers eBook](https://aka.ms/liftandshiftwithcontainersebook) (eBook sulla modernizzazione di app .NET esistenti con contenitori di Azure e Windows) |

 Il diagramma di flusso seguente illustra un albero delle decisioni quando si pianifica una migrazione ad Azure per le applicazioni .NET Framework esistenti, dove l'opzione A è la prima opzione da provare ed eseguire se possibile, ma l'opzione B è il percorso più facile da eseguire.

![Diagramma di flusso che illustra l'albero delle decisioni relativo all'hosting](media/dotnet-howto-choose-migration/decision-tree.png)

## <a name="database-choices"></a>Opzioni di database

Quando si esegue la migrazione di database relazionali ad Azure sono disponibili più opzioni. Per scegliere il percorso di migrazione del database adatto all'applicazione .NET esistente, vedere [Eseguire la migrazione del database SQL Server ad Azure](https://go.microsoft.com/fwlink/?linkid=862533).

## <a name="networking-and-security-considerations"></a>Considerazioni relative alla rete e alla sicurezza

Quando si distribuiscono le applicazioni in un cloud pubblico come Microsoft Azure, potrebbe essere necessario isolare e proteggere determinate reti [creando reti perimetrali](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/), ad esempio una [rete perimetrale tra Azure e l'ambiente locale](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) o una [rete perimetrale tra Azure e Internet](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz). Le reti perimetrali possono essere implementate con [Rete virtuale di Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).
Le reti virtuali di Azure consentono di:

- Creare un'infrastruttura ibrida facile da controllare
- Usare indirizzi IP e server DNS personali
- Proteggere le connessioni con una VPN IPSec o ExpressRoute
- Ottenere il controllo granulare del traffico tra subnet
- Creare topologie di rete sofisticate con appliance virtuali
- Ottenere un ambiente isolato con sicurezza elevata per le applicazioni
 
Per iniziare a creare la rete virtuale, vedere la [documentazione di Rete virtuale di Azure](https://docs.microsoft.com/azure/virtual-network/).

## <a name="authentication-and-authorization-considerations-when-migrating-to-azure"></a>Considerazioni relative all'autenticazione e all'autorizzazione quando si esegue la migrazione ad Azure

Una delle preoccupazioni principali delle organizzazioni che passano al cloud è la sicurezza. La maggior parte delle società ha investito una considerevole quantità di tempo, denaro e risorse tecniche nella progettazione e nello sviluppo di un modello di sicurezza ed è importante che possano sfruttare gli investimenti esistenti, ad esempio gli archivi identità e le soluzioni Single Sign-On.

Molte applicazioni .NET B2E aziendali esistenti in esecuzione in locale usano Active Directory per l'autenticazione e la gestione delle identità.  Azure AD Connect consente di integrare le directory locali con Azure Active Directory.  Per iniziare, vedere [Integrare le directory locali con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

Per una maggiore pianificazione relativa ad Azure Active Directory, vedere [Requisiti per la soluzione ibrida di gestione delle identità](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-business-needs).

Le altre opzioni per il protocollo di autenticazione sono [OAuth](https://en.wikipedia.org/wiki/OAuth) e [OpenID](https://en.wikipedia.org/wiki/OpenID), che sono comuni nelle applicazioni rivolte agli utenti.  Quando si usano database di identità autonomi, ad esempio un database SQL di identità ASP.NET di cui viene eseguito il wrapping con IdentityServer4 tramite OAuth, in genere non è necessaria la connettività ai database o alle directory locali.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Eseguire la migrazione di un'applicazione Web ASP.NET al servizio app di Azure](dotnet-howto-migrate-app-service.md)