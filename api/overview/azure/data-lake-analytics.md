---
title: Librerie di Azure Data Lake Analytics per .NET
description: Informazioni di riferimento sulle librerie di Azure Data Lake Analytics per .NET
keywords: Azure, .NET, SDK, API, Data Lake Analytics
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-lake-analytics
ms.custom: devcenter, svc-overview
ms.openlocfilehash: aa99608ec5568450a90cc2b93c3f1c5d0e38bfb1
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2017
---
# <a name="azure-data-lake-analytics-libraries-for-net"></a>Librerie di Azure Data Lake Analytics per .NET

## <a name="overview"></a>Panoramica

Azure Data Lake Analytics è un servizio per processi di analisi su richiesta che semplifica l'analisi dei Big Data.

Per altre informazioni, vedere [Panoramica di Microsoft Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview)

## <a name="management-library"></a>Libreria di gestione

Usare la libreria di gestione per connettersi al servizio e gestire i processi di analisi.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Analytics
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Analytics
```

### <a name="code-example"></a>Esempio di codice

Questo esempio crea i client per la connessione e la gestione dell'account di analisi.

```csharp
/*
using AdlClient 
*/

// Setup authentication for this demo
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
AnalyticsAccountRef adla_account = new AnalyticsAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
AnalyticsClient adla = new AnalyticsClient(auth, adla_account);
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>Esempi
* [Azure Data Lake .NET Client Example](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/) (Esempio di client di Azure Data Lake per .NET)

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
