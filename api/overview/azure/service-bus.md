---
title: Librerie del bus di servizio di Azure per .NET
description: Informazioni di riferimento sulle librerie del bus di servizio di Azure per .NET
keywords: Azure, .NET, SDK, API, bus di servizio
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: service-bus
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f2795a123a7b92237b0aea672298ce9339fd0830
ms.sourcegitcommit: e1a0e91988bb849c75e9583a80e3e6d712083785
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2018
ms.locfileid: "31005938"
---
# <a name="azure-service-bus-libraries-for-net"></a><span data-ttu-id="99a85-104">Librerie del bus di servizio di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="99a85-104">Azure Service Bus libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="99a85-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="99a85-105">Overview</span></span>

<span data-ttu-id="99a85-106">Il [bus di servizio di Azure](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) è un'infrastruttura di messaggistica che risiede tra le applicazioni e permette loro di scambiare messaggi offrendo scalabilità e resilienza migliori.</span><span class="sxs-lookup"><span data-stu-id="99a85-106">[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) is a messaging infrastructure that sits between applications allowing them to exchange messages for improved scale and resiliency.</span></span>

## <a name="client-library"></a><span data-ttu-id="99a85-107">Libreria client</span><span class="sxs-lookup"><span data-stu-id="99a85-107">Client library</span></span>

<span data-ttu-id="99a85-108">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99a85-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="99a85-109">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="99a85-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.ServiceBus
```

### <a name="code-example"></a><span data-ttu-id="99a85-110">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="99a85-110">Code Example</span></span>

<span data-ttu-id="99a85-111">Questo esempio invia un messaggio a una coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="99a85-111">This example sends a message to a Service Bus queue.</span></span>

```csharp
// using Microsoft.Azure.ServiceBus;
// Microsoft.Azure.ServiceBus 2.0.0 (stable)

byte[] messageBody = System.Text.Encoding.Unicode.GetBytes("Hello, world!");
ServiceBusConnectionStringBuilder builder = new ServiceBusConnectionStringBuilder(connectionString);
QueueClient client = new QueueClient(builder, ReceiveMode.PeekLock);
client.SendAsync(new Message(messageBody));
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="99a85-112">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="99a85-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a><span data-ttu-id="99a85-113">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="99a85-113">Management library</span></span>

<span data-ttu-id="99a85-114">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="99a85-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="99a85-115">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="99a85-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="99a85-116">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="99a85-116">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a><span data-ttu-id="99a85-117">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="99a85-117">Code Example</span></span>

<span data-ttu-id="99a85-118">Questo esempio crea una coda del bus di servizio con dimensioni massime di 1024 MB.</span><span class="sxs-lookup"><span data-stu-id="99a85-118">This example creates a Service Bus queue with a maximum size of 1024 MB.</span></span>

```csharp
// using Microsoft.Azure.Management.ServiceBus.Fluent;
// using Microsoft.Azure.Management.ServiceBus.Fluent.Models;

using (ServiceBusManagementClient client = new ServiceBusManagementClient(credentials))
{
    client.SubscriptionId = subscriptionId;
    QueueInner parameters = new QueueInner
    {
        MaxSizeInMegabytes = 1024
    };
    await client.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, queueName, parameters);
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="99a85-119">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="99a85-119">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a><span data-ttu-id="99a85-120">Esempi</span><span class="sxs-lookup"><span data-stu-id="99a85-120">Samples</span></span>

- <span data-ttu-id="99a85-121">[Service Bus Queue Basics - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/) (Nozioni fondamentali sulle code del bus di servizio - .NET)</span><span class="sxs-lookup"><span data-stu-id="99a85-121">[Service Bus Queue Basics - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)</span></span>
- <span data-ttu-id="99a85-122">[Service Bus Queue Advanced Features - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/) (Funzionalità avanzate delle code del bus di servizio - .NET)</span><span class="sxs-lookup"><span data-stu-id="99a85-122">[Service Bus Queue Advanced Features - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)</span></span>
- <span data-ttu-id="99a85-123">[Service Bus Publish/Subscribe Basics - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/) (Nozioni fondamentali su pubblicazione/sottoscrizione del bus di servizio - .NET)</span><span class="sxs-lookup"><span data-stu-id="99a85-123">[Service Bus Publish/Subscribe Basics - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)</span></span>
- <span data-ttu-id="99a85-124">[Service Bus Publish/Subscribe Advanced Features - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/) (Funzionalità avanzate di pubblicazione/sottoscrizione del bus di servizio - .NET)</span><span class="sxs-lookup"><span data-stu-id="99a85-124">[Service Bus Publish/Subscribe Advanced Features - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)</span></span>
- <span data-ttu-id="99a85-125">[Service Bus with Claims-Based Authorization - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/) (Autenticazione basata sulle attestazioni del bus di servizio - .NET)</span><span class="sxs-lookup"><span data-stu-id="99a85-125">[Service Bus with Claims-Based Authorization - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)</span></span>

<span data-ttu-id="99a85-126">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?term=service+bus) degli esempi di codice per il bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="99a85-126">View the [complete list](https://azure.microsoft.com/resources/samples/?term=service+bus) of Azure Service Bus samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
