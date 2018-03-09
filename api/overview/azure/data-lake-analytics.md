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
ms.openlocfilehash: 063513d8c523330276cdfc222d3ca00a9629f63a
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2018
---
# <a name="azure-data-lake-analytics-libraries-for-net"></a><span data-ttu-id="c7318-104">Librerie di Azure Data Lake Analytics per .NET</span><span class="sxs-lookup"><span data-stu-id="c7318-104">Azure Data Lake Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c7318-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c7318-105">Overview</span></span>

<span data-ttu-id="c7318-106">Azure Data Lake Analytics è un servizio per processi di analisi su richiesta che semplifica l'analisi dei Big Data.</span><span class="sxs-lookup"><span data-stu-id="c7318-106">Azure Data Lake Analytics is an on-demand analytics job service to simplify big data analytics.</span></span>

<span data-ttu-id="c7318-107">Per altre informazioni, vedere [Panoramica di Microsoft Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview)</span><span class="sxs-lookup"><span data-stu-id="c7318-107">To learn more, see [Overview of Microsoft Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="c7318-108">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="c7318-108">Management library</span></span>

<span data-ttu-id="c7318-109">Usare la libreria di gestione per connettersi al servizio e gestire i processi di analisi.</span><span class="sxs-lookup"><span data-stu-id="c7318-109">Use the management library to connect to the service and manage analytics jobs.</span></span>

<span data-ttu-id="c7318-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c7318-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c7318-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="c7318-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Analytics
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Analytics
```

### <a name="code-example"></a><span data-ttu-id="c7318-112">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="c7318-112">Code Example</span></span>

<span data-ttu-id="c7318-113">Questo esempio crea i client per la connessione e la gestione dell'account di analisi.</span><span class="sxs-lookup"><span data-stu-id="c7318-113">This example creates the clients to connect with and manage the analytics account.</span></span>

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
> [<span data-ttu-id="c7318-114">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="c7318-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a><span data-ttu-id="c7318-115">Esempi</span><span class="sxs-lookup"><span data-stu-id="c7318-115">Samples</span></span>
* <span data-ttu-id="c7318-116">[Azure Data Lake .NET Client Example](https://azure.microsoft.com/resources/samples/data-lake-dotnet-client/) (Esempio di client di Azure Data Lake per .NET)</span><span class="sxs-lookup"><span data-stu-id="c7318-116">[Azure Data Lake .NET Client Example](https://azure.microsoft.com/resources/samples/data-lake-dotnet-client/)</span></span>

<span data-ttu-id="c7318-117">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="c7318-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
