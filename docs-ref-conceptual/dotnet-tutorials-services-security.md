---
title: Esercitazioni .NET per la protezione delle app di Azure
description: Esercitazioni relative alla sicurezza delle applicazioni e alla gestione delle identità nelle app .NET in esecuzione in Azure.
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 88ecfc69fbd57becf1adf1163a063c0d2bb086a8
ms.sourcegitcommit: 61638b504b6c4d96b357894835c80c2680a99fe6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750589"
---
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a><span data-ttu-id="140c6-103">Esercitazioni per l'autenticazione di utenti nelle app .NET in esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="140c6-103">Tutorials for authenticating users in your .NET apps running on Azure</span></span>

<span data-ttu-id="140c6-104">La tabella seguente include collegamenti a esercitazioni dettagliate per l'autenticazione di utenti e la protezione delle applicazioni .NET in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="140c6-104">The following table links to in-depth tutorials for authenticating users and securing .NET applications running on Azure.</span></span>

<span data-ttu-id="140c6-105">Per esempi del codice sorgente, vedere l'elenco di [esempi di codice per i servizi di Azure](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span><span class="sxs-lookup"><span data-stu-id="140c6-105">For sample source code, see the list of [Azure service samples](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span></span>

| | |
|---|---|
|<span data-ttu-id="140c6-106">**Active Directory**</span><span class="sxs-lookup"><span data-stu-id="140c6-106">**Active Directory**</span></span>||
| <span data-ttu-id="140c6-107">[Aggiungere Azure Active Directory all'applicazione Web usando Servizi connessi di Visual Studio][5]</span><span class="sxs-lookup"><span data-stu-id="140c6-107">[Add Azure Active Directory to your web application by using Visual Studio Connected Services][5]</span></span> | <span data-ttu-id="140c6-108">Connettere un'app Web ad Azure AD in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="140c6-108">Connect a web app to Azure AD in Visual Studio</span></span> |
| <span data-ttu-id="140c6-109">[Accesso e disconnessione all'app Web con Azure AD][1]</span><span class="sxs-lookup"><span data-stu-id="140c6-109">[Web app sign-in and sign-out with Azure AD][1]</span></span> | <span data-ttu-id="140c6-110">Connettere e disconnettere utenti da ASP.NET con la libreria ADAL.</span><span class="sxs-lookup"><span data-stu-id="140c6-110">Sign users in and out of your ASP.NET with the ADAL library.</span></span> |
| <span data-ttu-id="140c6-111">[Autenticazione delle applicazioni desktop con Azure AD][2]</span><span class="sxs-lookup"><span data-stu-id="140c6-111">[Desktop application authentication with Azure AD][2]</span></span>| <span data-ttu-id="140c6-112">Integrare Azure AD in un'app WPF desktop di Windows con ADAL.</span><span class="sxs-lookup"><span data-stu-id="140c6-112">Integrate Azure AD into a Windows Desktop WPF app using ADAL.</span></span> | 
| <span data-ttu-id="140c6-113">[Autenticazione delle API Web con Azure AD][3]</span><span class="sxs-lookup"><span data-stu-id="140c6-113">[Web API authentication with Azure AD][3]</span></span> | <span data-ttu-id="140c6-114">Proteggere un'API Web usando token di connessione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="140c6-114">Protect a web API using bearer tokens from Azure AD.</span></span> |
|<span data-ttu-id="140c6-115">**Insieme di credenziali di chiave**</span><span class="sxs-lookup"><span data-stu-id="140c6-115">**Key Vault**</span></span>||
| <span data-ttu-id="140c6-116">[Aggiungere Key Vault all'applicazione Web usando Servizi connessi di Visual Studio][6]</span><span class="sxs-lookup"><span data-stu-id="140c6-116">[Add Key Vault to your web application by using Visual Studio Connected Services][6]</span></span> | <span data-ttu-id="140c6-117">Connettere un'app Web ad Azure Key Vault in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="140c6-117">Connect a web app to Azure Key Vault in Visual Studio</span></span> |
| <span data-ttu-id="140c6-118">[Usare Azure Key Vault da un'applicazione Web][4]</span><span class="sxs-lookup"><span data-stu-id="140c6-118">[Use Azure Key Vault from a Web Application][4]</span></span> | <span data-ttu-id="140c6-119">Accedere a un segreto da un'istanza di Azure Key Vault, in modo da poterlo usare nell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="140c6-119">Access a secret from an Azure Key Vault so that it can be used in your web application.</span></span> | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application
[5]: /azure/active-directory/develop/vs-active-directory-add-connected-service
[6]: /azure/key-vault/vs-key-vault-add-connected-service