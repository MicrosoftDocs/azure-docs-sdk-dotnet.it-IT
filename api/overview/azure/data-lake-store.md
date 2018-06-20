---
title: Librerie di Azure Data Lake Store per .NET
description: Informazioni di riferimento sulle librerie di Azure Data Lake Store per .NET
keywords: Azure, .NET, SDK, API, Data Lake Store
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-lake-store
ms.custom: devcenter, svc-overview
ms.openlocfilehash: e8380c4a9ebf86f03fe87fc800dffda10e48e60a
ms.sourcegitcommit: 3e904e6e4f04f1c92d729459434c85faff32e386
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/09/2017
ms.locfileid: "26588474"
---
# <a name="azure-data-lake-store-libraries-for-net"></a>Librerie di Azure Data Lake Store per .NET

## <a name="overview"></a>Panoramica

Azure Data Lake Store è un repository su vasta scala a livello aziendale per carichi di lavoro di analisi di Big Data. Azure Data Lake consente di acquisire dati di qualsiasi dimensione, tipo e velocità di inserimento in un'unica posizione per le analisi esplorative e operative.

Per altre informazioni, vedere [Panoramica di Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).

## <a name="client-library"></a>Libreria client

Usare la libreria client per eseguire operazioni del file system in Data Lake Store, ad esempio la creazione di cartelle in un account Data Lake Store, il caricamento di file e il download di file.  Per un'esercitazione completa sull'uso di Data Lake Store con .NET, vedere [Operazioni del file system in Azure Data Lake Store con .NET SDK](/azure/data-lake-store/data-lake-store-data-operations-net-sdk).

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.DataLake.Store
```
### <a name="authentication"></a>Autenticazione

* Per l'autenticazione dell'utente finale per l'applicazione, vedere [End-user authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk) (Autenticazione dell'utente finale con Data Lake Store tramite .NET SDK).
* Per l'autenticazione da servizio a servizio per l'applicazione, vedere [Service-to-service authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk) (Autenticazione da servizio a servizio con Data Lake Store tramite .NET SDK).

### <a name="code-example"></a>Esempio di codice

Il frammento di codice seguente crea l'oggetto client del file system di Data Lake Store, usato per inviare richieste al servizio.

```csharp
// Create client objects
AdlsClient client = AdlsClient.CreateClient(_adlsAccountName, adlCreds);
```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/datalakestore/client)


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

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/datalakestore/management)


## <a name="samples"></a>Esempi

* [Azure Data Lake .NET Client Example](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/) (Esempio di client di Azure Data Lake per .NET)

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
