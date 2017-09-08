---
title: Librerie di Inoltro del bus di servizio di Azure per .NET
description: Informazioni di riferimento sulle librerie di Inoltro del bus di servizio di Azure per .NET
keywords: Azure, .NET, SDK, API, Inoltro del bus di servizio
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/14/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 13a875b837648a05401453e975c9cd70d5e203a1
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-service-bus-relay-libraries-for-net"></a>Librerie di Inoltro del bus di servizio di Azure per .NET

## <a name="overview"></a>Panoramica

Il servizio di inoltro di Azure crea applicazioni ibride consentendo di esporre in modo sicuro nel cloud pubblico i servizi che risiedono in una rete aziendale, senza dover aprire una connessione firewall o richiedere modifiche di notevole impatto a un'infrastruttura di rete aziendale. Il servizio di inoltro supporta un'ampia gamma di protocolli di trasporto e standard dei servizi Web.
          
Altre informazioni sul [servizio di inoltro di Azure](https://docs.microsoft.com/en-us/azure/service-bus-relay/relay-what-is-it).

## <a name="client-library"></a>Libreria client

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Relay) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a>Esempi

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package