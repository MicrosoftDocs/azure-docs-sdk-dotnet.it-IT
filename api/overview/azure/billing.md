---
title: Librerie di fatturazione di Azure per .NET
description: Informazioni di riferimento sulle librerie di fatturazione di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: 88b90c71d29eacf61e4da2099f8a054d74df4a83
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190254"
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="c921d-103">Librerie di fatturazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="c921d-103">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c921d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c921d-104">Overview</span></span>

<span data-ttu-id="c921d-105">L'API Fatturazione di Azure (anteprima) fornisce l'accesso a livello di codice alle informazioni di fatturazione e alle fatture di Azure.</span><span class="sxs-lookup"><span data-stu-id="c921d-105">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="c921d-106">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="c921d-106">Management library</span></span>

<span data-ttu-id="c921d-107">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c921d-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c921d-108">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="c921d-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="c921d-109">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="c921d-109">Code Example</span></span>

<span data-ttu-id="c921d-110">Connettersi ad Azure e ottenere un elenco di fatture.</span><span class="sxs-lookup"><span data-stu-id="c921d-110">Connect to Azure and get a list of invoices.</span></span>

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
> [<span data-ttu-id="c921d-111">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="c921d-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="c921d-112">Esempi</span><span class="sxs-lookup"><span data-stu-id="c921d-112">Samples</span></span>

* [<span data-ttu-id="c921d-113">API di utilizzo</span><span class="sxs-lookup"><span data-stu-id="c921d-113">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="c921d-114">API RateCard</span><span class="sxs-lookup"><span data-stu-id="c921d-114">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="c921d-115">Applicazione Web multi-tenant</span><span class="sxs-lookup"><span data-stu-id="c921d-115">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
