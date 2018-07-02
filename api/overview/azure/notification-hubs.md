---
title: Librerie di Hub di notifica di Azure per .NET
description: Informazioni di riferimento sulle librerie di Hub di notifica di Azure per .NET
keywords: Azure, .NET, SDK, API, Hub di notifica
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: notification-hubs
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 0cbbfbafd2d1900c00f08fd1ab2e0f1af80ae8ff
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065501"
---
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="f48b0-104">Librerie di Hub di notifica di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="f48b0-104">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="f48b0-105">Hub di notifica di Azure offre un motore di push di facile uso, multipiattaforma e con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="f48b0-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="f48b0-106">Con una sola chiamata all'API multipiattaforma, è possibile inviare facilmente notifiche push mirate e personalizzate a qualsiasi piattaforma mobile da qualsiasi cloud o back-end locale.</span><span class="sxs-lookup"><span data-stu-id="f48b0-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="f48b0-107">Libreria client</span><span class="sxs-lookup"><span data-stu-id="f48b0-107">Client library</span></span>

<span data-ttu-id="f48b0-108">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="f48b0-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

> [!NOTE]
> <span data-ttu-id="f48b0-109">Una [nuova versione di anteprima del pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1) supporta ora .NET Standard, che consente di sfruttare .NET Core per l'uso di Hub di notifica in back-end</span><span class="sxs-lookup"><span data-stu-id="f48b0-109">A [new preview version of the NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1) now supports .NET Standard, which allows using .NET core for backend use of Notifications Hubs</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f48b0-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="f48b0-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="f48b0-111">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="f48b0-111">Code Example</span></span>

<span data-ttu-id="f48b0-112">Questo esempio illustra come connettersi a un hub di notifica e inviare un messaggio di Servizi notifica Push Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="f48b0-112">This example connects to a Notification Hub and sends a Windows Push Notification Service (WNS) message.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f48b0-113">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="f48b0-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a><span data-ttu-id="f48b0-114">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="f48b0-114">Management library</span></span>

<span data-ttu-id="f48b0-115">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="f48b0-115">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f48b0-116">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="f48b0-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f48b0-117">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="f48b0-117">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="f48b0-118">Esempi</span><span class="sxs-lookup"><span data-stu-id="f48b0-118">Samples</span></span>

- [<span data-ttu-id="f48b0-119">Introduzione a Universale di Windows</span><span class="sxs-lookup"><span data-stu-id="f48b0-119">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
