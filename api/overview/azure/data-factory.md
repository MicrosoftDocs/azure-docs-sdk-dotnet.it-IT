---
title: Librerie di Azure Data Factory per .NET
description: Informazioni di riferimento sulle librerie di Azure Data Factory per .NET
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 09/22/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-factory
ms.custom: devcenter
ms.openlocfilehash: 6f1a1cf9ac8189af59ff4e3f42dc1d8fb9620ea2
ms.sourcegitcommit: f35939d37f67485b3667739b02621e317db3e391
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2017
---
# <a name="azure-data-factory-libraries-for-net"></a>Librerie di Azure Data Factory per .NET

## <a name="overview"></a>Panoramica

Azure Data Factory è un servizio di integrazione di dati basato sul cloud. Consente di creare flussi di lavoro basati sui dati nel cloud per orchestrare e automatizzare lo spostamento dei dati e la trasformazione dei dati.

Per altre informazioni, vedere [Introduzione ad Azure Data Factory](/azure/data-factory/data-factory-introduction).

## <a name="management-library---data-factory-v2-preview"></a>Libreria di gestione - Data Factory V2 (anteprima)

Usare la libreria di gestione per creare e pianificare i flussi di lavoro basati sui dati (pipeline) in Data Factory V2 (anteprima).  Per altre informazioni, vedere [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net) (Creare una data factory e una pipeline con .NET SDK).

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a>Esempio di codice

L'esempio seguente usa la libreria di gestione per creare una data factory.

```csharp
/*
using Microsoft.Azure.Management.ResourceManager;
using Microsoft.Azure.Management.DataFactory;
using Microsoft.Azure.Management.DataFactory.Models;
*/

DataFactoryManagementClient client = new DataFactoryManagementClient(tokenCredentials) { SubscriptionId = subscriptionId };
Factory dataFactory = new Factory
{
    Location = region,
    Identity = new FactoryIdentity()
};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a>Libreria di gestione - Data Factory V1

Usare la libreria di gestione per creare e pianificare i flussi di lavoro basati sui dati (pipeline) in Data Factory versione 1.  Per altre informazioni, vedere la documentazione per [Data Factory versione 1](/azure/data-factory/v1/data-factory-introduction).

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a>Esempio di codice

L'esempio seguente usa la libreria di gestione per creare una data factory.

```csharp
DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
client.DataFactories.CreateOrUpdate(resourceGroupName,
    new DataFactoryCreateOrUpdateParameters()
    {
        DataFactory = new DataFactory()
        {
            Name = dataFactoryName,
            Location = "westus",
            Properties = new DataFactoryProperties()
        }
    }
);
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a>Esempi

* [MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) (MyDriving - Applicazione di esempio di Azure IOT e per dispositivi mobili) che usa Data Factory per ottenere informazioni dettagliate.

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
