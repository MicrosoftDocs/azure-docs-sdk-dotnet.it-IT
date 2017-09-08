---
title: Librerie di Gestione traffico di Azure per .NET
description: Informazioni di riferimento sulle librerie di Gestione traffico di Azure per .NET
keywords: Azure, .NET, SDK, API, Gestione traffico
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 0fc747c25fe368b5d67f70af1e2b9afc5e07f615
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-traffic-manager-libraries-for-net"></a>Librerie di Gestione traffico di Azure per .NET

## <a name="overview"></a>Panoramica

Gestione traffico di Microsoft Azure consente di controllare la distribuzione del traffico utente per gli endpoint di servizio in diversi data center. Gli endpoint di servizio supportati da Gestione traffico includono servizi cloud, app Web e macchine virtuali di Azure. È anche possibile usare Gestione traffico con endpoint esterni, non di Azure.

Altre informazioni su [Gestione traffico di Azure](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-overview).  

## <a name="management-library"></a>Libreria di gestione

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a>Esempi

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package