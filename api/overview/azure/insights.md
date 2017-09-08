---
title: Librerie di Azure Application Insights per .NET
description: Informazioni di riferimento sulle librerie di Azure Application Insights per .NET
keywords: Azure, .NET, SDK, API, Application AppInsights
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/24/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 2eef8d322d905679e8aceaed77ba44726c14dd94
ms.sourcegitcommit: fa02d34afbf981f809661ab842b3b93242a38f68
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2017
---
# <a name="azure-application-insights-libraries-for-net"></a>Librerie di Azure Application Insights per .NET

## <a name="overview"></a>Panoramica

Application Insights è un servizio estendibile di monitoraggio e diagnostica per gli sviluppatori Web che offre funzionalità avanzate di analisi ad-hoc. È possibile usare le classi dello spazio dei nomi ApplicationInsights per configurare la raccolta di dati di telemetria e inviare eventuali dati di telemetria personalizzati dalle applicazioni da monitorare.

## <a name="client-library"></a>Libreria client

L'SDK client di Application Insights per .NET consente di registrare eventi, dati aggregati, eccezioni, dipendenze e metriche in Azure per analisi future.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a>Esempio

Questo esempio tiene traccia di un evento personalizzato in Application Insights.

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a>Esempi

- [Application Insights Analytics with OpenSchema](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/) (Analisi di Application Insights con OpenSchema)

Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) degli esempi di codice per Azure Application Insights.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
