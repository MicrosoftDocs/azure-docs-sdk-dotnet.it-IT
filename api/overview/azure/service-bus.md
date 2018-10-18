---
title: Librerie del bus di servizio di Azure per .NET
description: Informazioni di riferimento sulle librerie del bus di servizio di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-bus-messaging
ms.openlocfilehash: a7a42b8ec788b944cb519218b0e5b201e5d6ac4f
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348043"
---
# <a name="azure-service-bus-libraries-for-net"></a><span data-ttu-id="dc82b-103">Librerie del bus di servizio di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="dc82b-103">Azure Service Bus libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="dc82b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="dc82b-104">Overview</span></span>

<span data-ttu-id="dc82b-105">Il [bus di servizio di Azure](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) è un'infrastruttura di messaggistica che risiede tra le applicazioni e permette loro di scambiare messaggi offrendo scalabilità e resilienza migliori.</span><span class="sxs-lookup"><span data-stu-id="dc82b-105">[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) is a messaging infrastructure that sits between applications allowing them to exchange messages for improved scale and resiliency.</span></span>

## <a name="client-library"></a><span data-ttu-id="dc82b-106">Libreria client</span><span class="sxs-lookup"><span data-stu-id="dc82b-106">Client library</span></span>

<span data-ttu-id="dc82b-107">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc82b-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="dc82b-108">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="dc82b-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.ServiceBus
```

### <a name="code-example"></a><span data-ttu-id="dc82b-109">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="dc82b-109">Code Example</span></span>

<span data-ttu-id="dc82b-110">Questo esempio invia un messaggio a una coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="dc82b-110">This example sends a message to a Service Bus queue.</span></span>

```csharp
// using Microsoft.Azure.ServiceBus;
// Microsoft.Azure.ServiceBus 2.0.0 (stable)

byte[] messageBody = System.Text.Encoding.Unicode.GetBytes("Hello, world!");
ServiceBusConnectionStringBuilder builder = new ServiceBusConnectionStringBuilder(connectionString);
QueueClient client = new QueueClient(builder, ReceiveMode.PeekLock);
client.SendAsync(new Message(messageBody));
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc82b-111">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="dc82b-111">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a><span data-ttu-id="dc82b-112">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="dc82b-112">Management library</span></span>

<span data-ttu-id="dc82b-113">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="dc82b-113">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="dc82b-114">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="dc82b-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="dc82b-115">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="dc82b-115">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a><span data-ttu-id="dc82b-116">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="dc82b-116">Code Example</span></span>

<span data-ttu-id="dc82b-117">Questo esempio crea una coda del bus di servizio con dimensioni massime di 1024 MB.</span><span class="sxs-lookup"><span data-stu-id="dc82b-117">This example creates a Service Bus queue with a maximum size of 1024 MB.</span></span>

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
> [<span data-ttu-id="dc82b-118">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="dc82b-118">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a><span data-ttu-id="dc82b-119">Esempi</span><span class="sxs-lookup"><span data-stu-id="dc82b-119">Samples</span></span>

- <span data-ttu-id="dc82b-120">[Service Bus Queue Basics - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/) (Nozioni fondamentali sulle code del bus di servizio - .NET)</span><span class="sxs-lookup"><span data-stu-id="dc82b-120">[Service Bus Queue Basics - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)</span></span>
- <span data-ttu-id="dc82b-121">[Service Bus Queue Advanced Features - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/) (Funzionalità avanzate delle code del bus di servizio - .NET)</span><span class="sxs-lookup"><span data-stu-id="dc82b-121">[Service Bus Queue Advanced Features - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)</span></span>
- <span data-ttu-id="dc82b-122">[Service Bus Publish/Subscribe Basics - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/) (Nozioni fondamentali su pubblicazione/sottoscrizione del bus di servizio - .NET)</span><span class="sxs-lookup"><span data-stu-id="dc82b-122">[Service Bus Publish/Subscribe Basics - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)</span></span>
- <span data-ttu-id="dc82b-123">[Service Bus Publish/Subscribe Advanced Features - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/) (Funzionalità avanzate di pubblicazione/sottoscrizione del bus di servizio - .NET)</span><span class="sxs-lookup"><span data-stu-id="dc82b-123">[Service Bus Publish/Subscribe Advanced Features - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)</span></span>
- <span data-ttu-id="dc82b-124">[Service Bus with Claims-Based Authorization - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/) (Autenticazione basata sulle attestazioni del bus di servizio - .NET)</span><span class="sxs-lookup"><span data-stu-id="dc82b-124">[Service Bus with Claims-Based Authorization - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)</span></span>

<span data-ttu-id="dc82b-125">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?term=service+bus) degli esempi di codice per il bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc82b-125">View the [complete list](https://azure.microsoft.com/resources/samples/?term=service+bus) of Azure Service Bus samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
