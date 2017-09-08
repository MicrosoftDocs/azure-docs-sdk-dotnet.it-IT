---
title: Istruzioni per gli esempi di librerie di gestione di Azure per .NET
description: Ottenere codice di esempio per creare e aggiornare le risorse con le librerie di gestione di Azure management per .NET.
keywords: Azure, .NET, SDK, API, esempi, esempio
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: ffda7cca724962e6f953432c5cab04485ddabb03
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a>Istruzioni per gli esempi di librerie di gestione di Azure per .NET

Questo articolo illustra i prerequisiti e l'autenticazione necessari per l'esecuzione degli esempi per le librerie di gestione di Azure per .NET.

## <a name="prerequisties"></a>Prerequisiti 

* [Visual Studio 2017](https://www.visualstudio.com/vs/) o [.NET Core SDK](https://www.microsoft.com/net/download/core)
* Una [sottoscrizione di Microsoft Azure](https://azure.microsoft.com/free/).
* [Client della riga di comando Git](https://git-scm.com/)
* [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)

## <a name="authentication-for-all-samples"></a>Autenticazione per tutti gli esempi

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="running-the-samples"></a>Esecuzione degli esempi

Dopo avere usato Git per clonare l'esempio, è possibile aprire l'esempio in Visual Studio ed eseguirlo tramite l'IDE.  In alternativa, usare .NET Core SDK per compilare ed eseguire l'esempio dalla riga di comando, come illustrato di seguito:

```cmd
git clone https://github.com/Azure-Samples/app-service-dotnet-configure-deployment-sources-for-web-apps.git
cd app-service-dotnet-configure-deployment-sources-for-web-apps
dotnet restore
dotnet run
```