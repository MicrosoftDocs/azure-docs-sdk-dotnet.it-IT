---
title: Librerie di fatturazione di Azure per .NET
description: Informazioni di riferimento sulle librerie di fatturazione di Azure per .NET
keywords: Azure, .NET, SDK, API, fatturazione
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 8df15d55a80991f29b694f4af06a20514bf20b32
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566082"
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="a4972-104">Librerie di fatturazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="a4972-104">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="a4972-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a4972-105">Overview</span></span>

<span data-ttu-id="a4972-106">L'API Fatturazione di Azure (anteprima) fornisce l'accesso a livello di codice alle informazioni di fatturazione e alle fatture di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4972-106">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="a4972-107">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="a4972-107">Management library</span></span>

<span data-ttu-id="a4972-108">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="a4972-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a4972-109">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="a4972-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="a4972-110">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="a4972-110">Code Example</span></span>

<span data-ttu-id="a4972-111">Connettersi ad Azure e ottenere un elenco di fatture.</span><span class="sxs-lookup"><span data-stu-id="a4972-111">Connect to Azure and get a list of invoices.</span></span>

```csharp
/* Include these directives
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Billing;
using Microsoft.Azure.Management.Billing.Models;
*/

// Log into Azure
var serviceCreds = ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var billingClient = new BillingClient(serviceCreds);
billingClient.SubscriptionId = subscriptionId;

// Get list of invoices
billingClient.Invoices.List();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a4972-112">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="a4972-112">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="a4972-113">Esempi</span><span class="sxs-lookup"><span data-stu-id="a4972-113">Samples</span></span>

* [<span data-ttu-id="a4972-114">API di utilizzo</span><span class="sxs-lookup"><span data-stu-id="a4972-114">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="a4972-115">API RateCard</span><span class="sxs-lookup"><span data-stu-id="a4972-115">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="a4972-116">Applicazione Web multi-tenant</span><span class="sxs-lookup"><span data-stu-id="a4972-116">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
