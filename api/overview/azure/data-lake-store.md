---
title: Librerie di Azure Data Lake Store per .NET
description: Informazioni di riferimento sulle librerie di Azure Data Lake Store per .NET
keywords: Azure, .NET, SDK, API, Data Lake Store
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/18/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 18746d745d64065a3d92215e704bce575130bdb0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-lake-store-libraries-for-net"></a>Librerie di Azure Data Lake Store per .NET

## <a name="overview"></a>Panoramica

Azure Data Lake Store è un repository su vasta scala a livello aziendale per carichi di lavoro di analisi di Big Data. Azure Data Lake consente di acquisire dati di qualsiasi dimensione, tipo e velocità di inserimento in un'unica posizione per le analisi esplorative e operative.

Per altre informazioni, vedere [Panoramica di Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).

## <a name="management-library"></a>Libreria di gestione

Usare la libreria di gestione per connettersi ai repository di Big Data e gestirli.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

### <a name="code-example"></a>Esempio di codice

Questo esempio esegue l'autenticazione di un account e un archivio di analisi e crea i client necessari per la gestione.

```csharp
/*
using AdlClient
using AdlClient.Models 
*/

// Setup authentication 
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
StoreAccountRef adls_account = new StoreAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
StoreClient adls = new StoreClient(auth, adls_account);
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/datalakestore/management)

## <a name="samples"></a>Esempi

* [Azure Data Lake .NET Client Example](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/) (Esempio di client di Azure Data Lake per .NET)

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
