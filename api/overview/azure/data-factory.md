---
title: Librerie di Azure Data Factory per .NET
description: Informazioni di riferimento sulle librerie di Azure Data Factory per .NET
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: e0b85d7d3988febca6dce7f4038825d74e4b8d2e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-factory-libraries-for-net"></a>Librerie di Azure Data Factory per .NET

## <a name="overview"></a>Panoramica

Azure Data Factory è un servizio di integrazione di dati basato sul cloud. Consente di creare flussi di lavoro basati sui dati nel cloud per orchestrare e automatizzare lo spostamento dei dati e la trasformazione dei dati.

Per altre informazioni, vedere [Introduzione ad Azure Data Factory](/azure/data-factory/data-factory-introduction).

## <a name="management-library"></a>Libreria di gestione

Usare la libreria di gestione per creare e pianificare i flussi di lavoro basati sui dati (pipeline).

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
