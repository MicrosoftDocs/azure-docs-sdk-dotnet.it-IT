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
# <a name="azure-management-libraries-for-net-sample-instructions"></a><span data-ttu-id="cb41a-104">Istruzioni per gli esempi di librerie di gestione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="cb41a-104">Azure management libraries for .NET sample instructions</span></span>

<span data-ttu-id="cb41a-105">Questo articolo illustra i prerequisiti e l'autenticazione necessari per l'esecuzione degli esempi per le librerie di gestione di Azure per .NET.</span><span class="sxs-lookup"><span data-stu-id="cb41a-105">This article describes the prerequisites and authentication required for running the samples for the Azure management libraries for .NET.</span></span>

## <a name="prerequisties"></a><span data-ttu-id="cb41a-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cb41a-106">Prerequisties</span></span> 

* [<span data-ttu-id="cb41a-107">Visual Studio 2017](https://www.visualstudio.com/vs/) o [.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="cb41a-107">Visual Studio 2017](https://www.visualstudio.com/vs/) or [.NET Core SDK</span></span>](https://www.microsoft.com/net/download/core)
* <span data-ttu-id="cb41a-108">Una [sottoscrizione di Microsoft Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="cb41a-108">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* [<span data-ttu-id="cb41a-109">Client della riga di comando Git</span><span class="sxs-lookup"><span data-stu-id="cb41a-109">Git command line client</span></span>](https://git-scm.com/)
* [<span data-ttu-id="cb41a-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb41a-110">Azure PowerShell</span></span>](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)

## <a name="authentication-for-all-samples"></a><span data-ttu-id="cb41a-111">Autenticazione per tutti gli esempi</span><span class="sxs-lookup"><span data-stu-id="cb41a-111">Authentication for all samples</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="running-the-samples"></a><span data-ttu-id="cb41a-112">Esecuzione degli esempi</span><span class="sxs-lookup"><span data-stu-id="cb41a-112">Running the samples</span></span>

<span data-ttu-id="cb41a-113">Dopo avere usato Git per clonare l'esempio, è possibile aprire l'esempio in Visual Studio ed eseguirlo tramite l'IDE.</span><span class="sxs-lookup"><span data-stu-id="cb41a-113">Once you have used Git to clone the sample, you can open the sample in Visual Studio and run the sample using the IDE.</span></span>  <span data-ttu-id="cb41a-114">In alternativa, usare .NET Core SDK per compilare ed eseguire l'esempio dalla riga di comando, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cb41a-114">Alternatively, use the .NET Core SDK to build and run the sample from the command line, like this:</span></span>

```cmd
git clone https://github.com/Azure-Samples/app-service-dotnet-configure-deployment-sources-for-web-apps.git
cd app-service-dotnet-configure-deployment-sources-for-web-apps
dotnet restore
dotnet run
```