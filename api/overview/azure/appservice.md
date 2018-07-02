---
title: Librerie del servizio app di Azure per .NET
description: Informazioni di riferimento sulle librerie del servizio app di Azure per .NET
keywords: Azure, .NET, SDK, API, app Web, servizio app, dispositivi mobili, asp.net
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 0fee28930dff5075cdd84fe3cb88850e07bc6ccb
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065801"
---
# <a name="azure-app-service-libraries-for-net"></a><span data-ttu-id="31515-104">Librerie del servizio app di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="31515-104">Azure App Service libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="31515-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="31515-105">Overview</span></span>

<span data-ttu-id="31515-106">Il [Servizio app di Azure](/azure/app-service/app-service-value-prop-what-is) consente di distribuire e ridimensionare siti Web, applicazioni Web, servizi e API REST.</span><span class="sxs-lookup"><span data-stu-id="31515-106">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) allows you to deploy and scale websites, web applications, services, and REST APIs.</span></span>

## <a name="management-api"></a><span data-ttu-id="31515-107">API di gestione</span><span class="sxs-lookup"><span data-stu-id="31515-107">Management API</span></span>

<span data-ttu-id="31515-108">Distribuire, gestire e ridimensionare gli elementi ospitati nel servizio app di Azure con l'API di gestione.</span><span class="sxs-lookup"><span data-stu-id="31515-108">Deploy, manage, and scale elements hosted in Azure App Service with the management API.</span></span>

<span data-ttu-id="31515-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="31515-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="31515-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="31515-110">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="31515-111">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="31515-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a><span data-ttu-id="31515-112">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="31515-112">Code Example</span></span>

<span data-ttu-id="31515-113">Creare una nuova app Web.</span><span class="sxs-lookup"><span data-stu-id="31515-113">Create a new web app.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.AppService.Fluent;
*/

IWebApp app1 = azure.WebApps
    .Define("MyUniqueWebAddress")
    .WithRegion(Region.USWest)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewWindowsPlan(PricingTier.StandardS1)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="31515-114">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="31515-114">Explore the Management APIs</span></span>](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a><span data-ttu-id="31515-115">Esempi</span><span class="sxs-lookup"><span data-stu-id="31515-115">Samples</span></span>

* <span data-ttu-id="31515-116">[Manage your web apps with the .NET SDK for Azure](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-manage/) (Gestire le app Web con .NET SDK per Azure)</span><span class="sxs-lookup"><span data-stu-id="31515-116">[Manage your web apps with the .NET SDK for Azure](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-manage/)</span></span>
* <span data-ttu-id="31515-117">[ASP.NET sample for Azure App Service](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-get-started/) (Esempio di ASP.NET per il Servizio app di Azure)</span><span class="sxs-lookup"><span data-stu-id="31515-117">[ASP.NET sample for Azure App Service](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-get-started/)</span></span>

<span data-ttu-id="31515-118">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) degli esempi di codice per il Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="31515-118">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) of Azure App Service samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package