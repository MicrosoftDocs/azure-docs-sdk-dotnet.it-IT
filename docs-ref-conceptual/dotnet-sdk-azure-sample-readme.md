---
title: Istruzioni per gli esempi di librerie di gestione di Azure per .NET
description: Ottenere codice di esempio per creare e aggiornare le risorse con le librerie di gestione di Azure management per .NET.
keywords: Azure, .NET, SDK, API, esempi, esempio
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: a931e623768e1fddad263c7da8eb864c37613379
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2018
ms.locfileid: "29752473"
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a>Istruzioni per gli esempi di librerie di gestione di Azure per .NET

Questo articolo illustra i prerequisiti e l'autenticazione necessari per l'esecuzione degli esempi per le librerie di gestione di Azure per .NET.

## <a name="prerequisties"></a>Prerequisiti 

* [Visual Studio 2017](https://www.visualstudio.com/vs/) o [.NET Core SDK](https://www.microsoft.com/net/download/core)
* Una [sottoscrizione di Microsoft Azure](https://azure.microsoft.com/free/).
* [Client della riga di comando Git](https://git-scm.com/)
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

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