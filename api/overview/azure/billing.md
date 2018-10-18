---
title: Librerie di fatturazione di Azure per .NET
description: Informazioni di riferimento sulle librerie di fatturazione di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: billing
ms.openlocfilehash: 196b9b4ed5f1f5f6794d86a43d26827355800d7b
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348083"
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="e38c3-103">Librerie di fatturazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="e38c3-103">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="e38c3-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e38c3-104">Overview</span></span>

<span data-ttu-id="e38c3-105">L'API Fatturazione di Azure (anteprima) fornisce l'accesso a livello di codice alle informazioni di fatturazione e alle fatture di Azure.</span><span class="sxs-lookup"><span data-stu-id="e38c3-105">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="e38c3-106">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="e38c3-106">Management library</span></span>

<span data-ttu-id="e38c3-107">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="e38c3-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e38c3-108">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="e38c3-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="e38c3-109">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="e38c3-109">Code Example</span></span>

<span data-ttu-id="e38c3-110">Connettersi ad Azure e ottenere un elenco di fatture.</span><span class="sxs-lookup"><span data-stu-id="e38c3-110">Connect to Azure and get a list of invoices.</span></span>

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
> [<span data-ttu-id="e38c3-111">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="e38c3-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="e38c3-112">Esempi</span><span class="sxs-lookup"><span data-stu-id="e38c3-112">Samples</span></span>

* [<span data-ttu-id="e38c3-113">API di utilizzo</span><span class="sxs-lookup"><span data-stu-id="e38c3-113">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="e38c3-114">API RateCard</span><span class="sxs-lookup"><span data-stu-id="e38c3-114">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="e38c3-115">Applicazione Web multi-tenant</span><span class="sxs-lookup"><span data-stu-id="e38c3-115">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
