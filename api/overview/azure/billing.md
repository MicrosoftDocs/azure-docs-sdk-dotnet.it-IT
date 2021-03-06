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
# <a name="azure-billing-libraries-for-net"></a>Librerie di fatturazione di Azure per .NET

## <a name="overview"></a>Panoramica

L'API Fatturazione di Azure (anteprima) fornisce l'accesso a livello di codice alle informazioni di fatturazione e alle fatture di Azure.

## <a name="management-library"></a>Libreria di gestione

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a>Esempio di codice

Connettersi ad Azure e ottenere un elenco di fatture.

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
> [Esplorare le API di gestione](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a>Esempi

* [API di utilizzo](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [API RateCard](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [Applicazione Web multi-tenant](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
