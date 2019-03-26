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
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="c7824-103">Librerie di Hub di notifica di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="c7824-103">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="c7824-104">Hub di notifica di Azure offre un motore di push di facile uso, multipiattaforma e con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="c7824-104">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="c7824-105">Con una sola chiamata all'API multipiattaforma, è possibile inviare facilmente notifiche push mirate e personalizzate a qualsiasi piattaforma mobile da qualsiasi cloud o back-end locale.</span><span class="sxs-lookup"><span data-stu-id="c7824-105">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="c7824-106">Libreria client</span><span class="sxs-lookup"><span data-stu-id="c7824-106">Client library</span></span>

<span data-ttu-id="c7824-107">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c7824-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

> [!NOTE]
> <span data-ttu-id="c7824-108">Il [pacchetto NuGet di Hub di notifica di Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) supporta ora .NET Standard, che consente di usare .NET Core per il back-end di Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="c7824-108">The [Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) now supports .NET Standard, which allows using .NET core for backend use of Notifications Hubs</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c7824-109">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="c7824-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="c7824-110">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="c7824-110">Code Example</span></span>

<span data-ttu-id="c7824-111">Questo esempio illustra come connettersi a un hub di notifica e inviare un messaggio di Servizi notifica Push Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="c7824-111">This example connects to a Notification Hub and sends a Windows Push Notification Service (WNS) message.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7824-112">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="c7824-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)

## <a name="management-library"></a><span data-ttu-id="c7824-113">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="c7824-113">Management library</span></span>

<span data-ttu-id="c7824-114">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c7824-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c7824-115">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="c7824-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7824-116">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="c7824-116">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="c7824-117">Esempi</span><span class="sxs-lookup"><span data-stu-id="c7824-117">Samples</span></span>

- [<span data-ttu-id="c7824-118">Introduzione a Universale di Windows</span><span class="sxs-lookup"><span data-stu-id="c7824-118">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
