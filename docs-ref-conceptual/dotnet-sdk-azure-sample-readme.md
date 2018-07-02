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
ms.sourcegitcommit: 9dd801d659803f5efb16d65454cd09258e1cc7d6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2018
ms.locfileid: "29752473"
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a><span data-ttu-id="82e8c-104">Istruzioni per gli esempi di librerie di gestione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="82e8c-104">Azure management libraries for .NET sample instructions</span></span>

<span data-ttu-id="82e8c-105">Questo articolo illustra i prerequisiti e l'autenticazione necessari per l'esecuzione degli esempi per le librerie di gestione di Azure per .NET.</span><span class="sxs-lookup"><span data-stu-id="82e8c-105">This article describes the prerequisites and authentication required for running the samples for the Azure management libraries for .NET.</span></span>

## <a name="prerequisties"></a><span data-ttu-id="82e8c-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="82e8c-106">Prerequisties</span></span> 

* <span data-ttu-id="82e8c-107">[Visual Studio 2017](https://www.visualstudio.com/vs/) o [.NET Core SDK](https://www.microsoft.com/net/download/core)</span><span class="sxs-lookup"><span data-stu-id="82e8c-107">[Visual Studio 2017](https://www.visualstudio.com/vs/) or [.NET Core SDK](https://www.microsoft.com/net/download/core)</span></span>
* <span data-ttu-id="82e8c-108">Una [sottoscrizione di Microsoft Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="82e8c-108">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* [<span data-ttu-id="82e8c-109">Client della riga di comando Git</span><span class="sxs-lookup"><span data-stu-id="82e8c-109">Git command line client</span></span>](https://git-scm.com/)
* [<span data-ttu-id="82e8c-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="82e8c-110">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

## <a name="authentication-for-all-samples"></a><span data-ttu-id="82e8c-111">Autenticazione per tutti gli esempi</span><span class="sxs-lookup"><span data-stu-id="82e8c-111">Authentication for all samples</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="running-the-samples"></a><span data-ttu-id="82e8c-112">Esecuzione degli esempi</span><span class="sxs-lookup"><span data-stu-id="82e8c-112">Running the samples</span></span>

<span data-ttu-id="82e8c-113">Dopo avere usato Git per clonare l'esempio, è possibile aprire l'esempio in Visual Studio ed eseguirlo tramite l'IDE.</span><span class="sxs-lookup"><span data-stu-id="82e8c-113">Once you have used Git to clone the sample, you can open the sample in Visual Studio and run the sample using the IDE.</span></span>  <span data-ttu-id="82e8c-114">In alternativa, usare .NET Core SDK per compilare ed eseguire l'esempio dalla riga di comando, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="82e8c-114">Alternatively, use the .NET Core SDK to build and run the sample from the command line, like this:</span></span>

```cmd
git clone https://github.com/Azure-Samples/app-service-dotnet-configure-deployment-sources-for-web-apps.git
cd app-service-dotnet-configure-deployment-sources-for-web-apps
dotnet restore
dotnet run
```