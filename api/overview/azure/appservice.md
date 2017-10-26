---
title: Librerie del servizio app di Azure per .NET
description: Informazioni di riferimento sulle librerie del servizio app di Azure per .NET
keywords: Azure, .NET, SDK, API, app Web, servizio app, dispositivi mobili, asp.net
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 9f54fb6aca934f07c6ae23a4ae40dc29fa48ec8b
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2017
---
# <a name="azure-app-service-libraries-for-net"></a>Librerie del servizio app di Azure per .NET

## <a name="overview"></a>Panoramica

Il [Servizio app di Azure](/azure/app-service/app-service-value-prop-what-is) consente di distribuire e ridimensionare siti Web, applicazioni Web, servizi e API REST.

## <a name="management-api"></a>API di gestione

Distribuire, gestire e ridimensionare gli elementi ospitati nel servizio app di Azure con l'API di gestione.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].


#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a>Esempio di codice

Creare una nuova app Web.

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
> [Esplorare le API di gestione](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a>Esempi

* [Manage your web apps with the .NET SDK for Azure](https://azure.microsoft.com/en-us/resources/samples/app-service-web-dotnet-manage/) (Gestire le app Web con .NET SDK per Azure)
* [ASP.NET sample for Azure App Service](https://azure.microsoft.com/en-us/resources/samples/app-service-web-dotnet-get-started/) (Esempio di ASP.NET per il Servizio app di Azure)

Visualizzare l'[elenco completo](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=app%20service) degli esempi di codice per il Servizio app di Azure.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package