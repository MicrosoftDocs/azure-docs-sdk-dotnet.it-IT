---
title: Librerie di Hub di notifica di Azure per .NET
description: Informazioni di riferimento sulle librerie di Hub di notifica di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: notification-hubs
ms.openlocfilehash: 750a51e8dfa7323f6afb54735b4bfc517f9ec15f
ms.sourcegitcommit: 4b68c73652cb7e44cf4db36f70cb33a17dd863ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/19/2019
ms.locfileid: "58085838"
---
# <a name="azure-notification-hubs-libraries-for-net"></a>Librerie di Hub di notifica di Azure per .NET

Hub di notifica di Azure offre un motore di push di facile uso, multipiattaforma e con scalabilità orizzontale. Con una sola chiamata all'API multipiattaforma, è possibile inviare facilmente notifiche push mirate e personalizzate a qualsiasi piattaforma mobile da qualsiasi cloud o back-end locale.

## <a name="client-library"></a>Libreria client

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

> [!NOTE]
> Il [pacchetto NuGet di Hub di notifica di Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) supporta ora .NET Standard, che consente di usare .NET Core per il back-end di Hub di notifica

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a>Esempio di codice

Questo esempio illustra come connettersi a un hub di notifica e inviare un messaggio di Servizi notifica Push Windows (WNS).

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/notificationhubs/client)

## <a name="management-library"></a>Libreria di gestione

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a>Esempi

- [Introduzione a Universale di Windows](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
