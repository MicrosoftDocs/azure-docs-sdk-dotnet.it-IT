---
title: Librerie di Hub di notifica di Azure per .NET
description: Informazioni di riferimento sulle librerie di Hub di notifica di Azure per .NET
keywords: Azure, .NET, SDK, API, Hub di notifica
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 630cdd465fdf6c77ad5d46d9f231c3f331467587
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="701ef-104">Librerie di Hub di notifica di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="701ef-104">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="701ef-105">Hub di notifica di Azure offre un motore di push di facile uso, multipiattaforma e con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="701ef-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="701ef-106">Con una sola chiamata all'API multipiattaforma, è possibile inviare facilmente notifiche push mirate e personalizzate a qualsiasi piattaforma mobile da qualsiasi cloud o back-end locale.</span><span class="sxs-lookup"><span data-stu-id="701ef-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="701ef-107">Libreria client</span><span class="sxs-lookup"><span data-stu-id="701ef-107">Client library</span></span>

<span data-ttu-id="701ef-108">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="701ef-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="701ef-109">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="701ef-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="701ef-110">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="701ef-110">Code Example</span></span>

<span data-ttu-id="701ef-111">Questo esempio si connette a un database e legge righe da una tabella.</span><span class="sxs-lookup"><span data-stu-id="701ef-111">This example connects to a database and reads rows from a table.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="701ef-112">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="701ef-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a><span data-ttu-id="701ef-113">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="701ef-113">Management library</span></span>

<span data-ttu-id="701ef-114">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="701ef-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="701ef-115">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="701ef-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="701ef-116">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="701ef-116">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="701ef-117">Esempi</span><span class="sxs-lookup"><span data-stu-id="701ef-117">Samples</span></span>

- [<span data-ttu-id="701ef-118">Introduzione a Universale di Windows</span><span class="sxs-lookup"><span data-stu-id="701ef-118">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
