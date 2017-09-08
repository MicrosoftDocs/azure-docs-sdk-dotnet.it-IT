---
title: Librerie di fatturazione di Azure per .NET
description: Informazioni di riferimento sulle librerie di fatturazione di Azure per .NET
keywords: Azure, .NET, SDK, API, fatturazione
author: spboyer
ms.author: casoper
manager: douge
ms.date: 07/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 0a401bf9ccc345d3c6e99a010c74f9c7f6f5914e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="17fc2-104">Librerie di fatturazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="17fc2-104">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="17fc2-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="17fc2-105">Overview</span></span>

<span data-ttu-id="17fc2-106">L'API Fatturazione di Azure (anteprima) fornisce l'accesso a livello di codice alle informazioni di fatturazione e alle fatture di Azure.</span><span class="sxs-lookup"><span data-stu-id="17fc2-106">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="17fc2-107">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="17fc2-107">Management library</span></span>

<span data-ttu-id="17fc2-108">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="17fc2-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="17fc2-109">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="17fc2-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="17fc2-110">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="17fc2-110">Code Example</span></span>

<span data-ttu-id="17fc2-111">Connettersi ad Azure e ottenere un elenco di fatture.</span><span class="sxs-lookup"><span data-stu-id="17fc2-111">Connect to Azure and get a list of invoices.</span></span>

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
> [<span data-ttu-id="17fc2-112">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="17fc2-112">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="17fc2-113">Esempi</span><span class="sxs-lookup"><span data-stu-id="17fc2-113">Samples</span></span>

* [<span data-ttu-id="17fc2-114">API di utilizzo</span><span class="sxs-lookup"><span data-stu-id="17fc2-114">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="17fc2-115">API RateCard</span><span class="sxs-lookup"><span data-stu-id="17fc2-115">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="17fc2-116">Applicazione Web multi-tenant</span><span class="sxs-lookup"><span data-stu-id="17fc2-116">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
