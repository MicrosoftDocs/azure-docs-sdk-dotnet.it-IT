---
title: Eseguire la migrazione di un'applicazione Web ASP.NET al servizio app di Azure
description: Informazioni su come eseguire la migrazione di un'applicazione Web ASP.NET da locale al servizio app di Azure.
keywords: Azure .NET, ASP.NET, servizio app, app Web, eseguire la migrazione, migrazione
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter
ms.openlocfilehash: 050782871c3fe4ccb0d15bf9933c3b11c88ce661
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2018
ms.locfileid: "29728422"
---
# <a name="migrate-an-aspnet-web-application-to-azure-app-service"></a>Eseguire la migrazione di un'applicazione Web ASP.NET al servizio app di Azure

Il [servizio app](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps) è un servizio della piattaforma di calcolo completamente gestito, ottimizzato per l'hosting di siti Web e applicazioni Web scalabili. Questo documento contiene informazioni su come trasferire in modalità lift-and-shift nel servizio app di Azure un'applicazione esistente, sulle modifiche da considerare e su altre risorse per il passaggio al cloud.

Informazioni introduttive [Pubblicare l'applicazione ASP.NET + SQL nel servizio app di Azure](https://go.microsoft.com/fwlink/?linkid=863214).

# <a name="preparation"></a>Operazioni preliminari   
* [Come determinare se l'app è qualificata per il servizio app](https://azure.microsoft.com/downloads/migration-assistant/)
* [Passaggio del database al cloud](https://go.microsoft.com/fwlink/?linkid=863217)

# <a name="considerations"></a>Considerazioni
È necessario prendere in considerazione diversi fattori prima di eseguire la migrazione dell'applicazione. Di seguito è riportato un elenco delle potenziali modifiche da apportare all'applicazione e viene illustrato come eseguirle.

## <a name="sql-database-configuration"></a>Configurazione del database SQL
Se l'applicazione usa un database locale, sono disponibili diverse opzioni per l'app Web. [Altre informazioni sulla migrazione di database SQL ad Azure](https://go.microsoft.com/fwlink/?linkid=863217).

## <a name="iis"></a>IIS
Tutti gli elementi che normalmente vengono configurati tramite applicationHost.config nell'applicazione ora possono essere configurati tramite il portale di Azure. Ciò si applica al numero di bit del pool di applicazioni, all'abilitazione o alla disabilitazione dei WebSocket, alla versione della pipeline gestita, alla versione di .NET Framework (2.0/4.0) e così via. Per modificare le [impostazioni applicazione](https://docs.microsoft.com/azure/app-service/web-sites-configure), passare al [portale di Azure](https://portal.azure.com), aprire il pannello dell'app Web e quindi selezionare la scheda **Impostazioni applicazione**.

## <a name="authentication"></a>Authentication
Se l'applicazione autentica gli utenti in qualsiasi momento, sarà necessario modificare questa funzionalità in modo che funzioni dopo la distribuzione dell'applicazione nelle app Web di Azure. Una possibilità è usare Azure AD Connect per integrare le directory locali con Azure Active Directory. [Altre informazioni su come integrare le directory locali con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="virtual-network-modification"></a>Modifica della rete virtuale
Se si usa più di un servizio di Azure, è possibile prendere in considerazione l'uso di una rete virtuale per consentire a questi servizi di comunicare in modo sicuro. È possibile configurare una connessione dalla rete locale a una [rete virtuale di Azure](https://docs.microsoft.com/azure/app-service/web-sites-integrate-with-vnet) usando la VPN o ExpressRoute.

## <a name="monitoring-and-diagnostics"></a>Monitoraggio e diagnostica
È improbabile che le soluzioni locali correnti per il monitoraggio e la diagnostica funzionino nel cloud. Azure fornisce tuttavia strumenti per la registrazione, il monitoraggio e la diagnostica per poter identificare i problemi delle app Web ed eseguirne il debug. È anche possibile abilitare la diagnostica per l'app Web nella configurazione e visualizzare i log registrati in Azure Application Insights. [Altre informazioni sull'abilitazione della registrazione diagnostica per le app Web](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log).

## <a name="connection-strings-and-application-settings"></a>Stringhe di connessione e impostazioni applicazione
Un'opzione che consente di tenere le informazioni al sicuro è l'uso di [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/), un servizio che archivia in modo sicuro le informazioni riservate usate nell'applicazione. In alternativa, è possibile archiviare questi dati come impostazione del servizio app.

## <a name="dns"></a>DNS
Potrebbe essere necessario aggiornare le configurazioni DNS in base ai requisiti dell'applicazione. Queste impostazioni DNS possono essere configurate nelle [impostazioni del dominio personalizzato](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain) del servizio app. Un altro fattore da considerare è l'[associazione di un certificato SSL personalizzato esistente](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl).

## <a name="file-system-and-storage"></a>Archiviazione e file system
Se l'applicazione salva in modo permanente i dati, sarà necessario aggiornarla per usare invece Archiviazione di Azure. Archiviazione di Azure è un servizio che fornisce condivisioni file per la condivisione tramite protocollo SMB, archivio BLOB, code semplici e tabelle non relazionali. [Altre informazioni sulle condivisioni file di Archiviazione di Azure](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Eseguire la migrazione di un'applicazione Web ASP.NET al servizio app di Azure](https://aka.ms/azure-webapp-migrate)
