---
title: Esercitazioni .NET per la protezione delle app di Azure
description: Esercitazioni relative alla sicurezza delle applicazioni e alla gestione delle identità nelle app .NET in esecuzione in Azure.
ms.date: 10/19/2017
ms.openlocfilehash: 19960efa8faa762f0cde657d702f09a8dcb66e99
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190644"
---
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a>Esercitazioni per l'autenticazione di utenti nelle app .NET in esecuzione in Azure

La tabella seguente include collegamenti a esercitazioni dettagliate per l'autenticazione di utenti e la protezione delle applicazioni .NET in esecuzione in Azure.

Per esempi del codice sorgente, vedere l'elenco di [esempi di codice per i servizi di Azure](https://azure.microsoft.com/resources/samples/?platform=dotnet).

| | |
|---|---|
|**Active Directory**||
| [Aggiungere Azure Active Directory all'applicazione Web usando Servizi connessi di Visual Studio][5] | Connettere un'app Web ad Azure AD in Visual Studio |
| [Accesso e disconnessione all'app Web con Azure AD][1] | Connettere e disconnettere utenti da ASP.NET con la libreria ADAL. |
| [Autenticazione delle applicazioni desktop con Azure AD][2]| Integrare Azure AD in un'app WPF desktop di Windows con ADAL. | 
| [Autenticazione delle API Web con Azure AD][3] | Proteggere un'API Web usando token di connessione di Azure AD. |
|**Insieme di credenziali di chiave**||
| [Aggiungere Key Vault all'applicazione Web usando Servizi connessi di Visual Studio][6] | Connettere un'app Web ad Azure Key Vault in Visual Studio |
| [Usare Azure Key Vault da un'applicazione Web][4] | Accedere a un segreto da un'istanza di Azure Key Vault, in modo da poterlo usare nell'applicazione Web. | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application
[5]: /azure/active-directory/develop/vs-active-directory-add-connected-service
[6]: /azure/key-vault/vs-key-vault-add-connected-service