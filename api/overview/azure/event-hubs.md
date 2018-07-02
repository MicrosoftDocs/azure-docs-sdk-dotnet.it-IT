---
title: Librerie di Hub eventi di Azure per .NET
description: Informazioni di riferimento sulle librerie di Hub eventi di Azure per .NET
keywords: Azure, .NET, SDK, API, Hub eventi
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: event-hubs
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 5502ae24574c7883c34522ae18ca81bb516a33d2
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065311"
---
# <a name="azure-event-hubs-libraries-for-net"></a><span data-ttu-id="7a773-104">Librerie di Hub eventi di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="7a773-104">Azure Event Hubs libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="7a773-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7a773-105">Overview</span></span>

<span data-ttu-id="7a773-106">Hub eventi di Azure è un servizio di inserimento di eventi e una piattaforma di streaming dei dati altamente scalabile.</span><span class="sxs-lookup"><span data-stu-id="7a773-106">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service.</span></span>

<span data-ttu-id="7a773-107">Per altre informazioni su Hub eventi di Azure, vedere [Che cos'è Hub eventi?](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="7a773-107">To learn more about Azure Event Hubs, read the article [What is Event Hubs?](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>  <span data-ttu-id="7a773-108">Per iniziare, vedere la [Guida alla programmazione per Hub eventi](/azure/event-hubs/event-hubs-programming-guide).</span><span class="sxs-lookup"><span data-stu-id="7a773-108">To get started, check out the [Event Hubs Programming Guide](/azure/event-hubs/event-hubs-programming-guide).</span></span>

## <a name="client-library"></a><span data-ttu-id="7a773-109">Libreria client</span><span class="sxs-lookup"><span data-stu-id="7a773-109">Client library</span></span>

<span data-ttu-id="7a773-110">Usare il client di Hub eventi per inviare e ricevere messaggi da e verso Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="7a773-110">Use the Event Hubs client to send and receive messages to and from Event Hubs.</span></span>

<span data-ttu-id="7a773-111">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="7a773-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7a773-112">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="7a773-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventHubs
```

```bash
dotnet add package Microsoft.Azure.EventHubs
```

### <a name="code-example"></a><span data-ttu-id="7a773-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="7a773-113">Code Example</span></span>

<span data-ttu-id="7a773-114">Il codice seguente mostra come creare un client di Hub eventi e inviare un messaggio all'hub.</span><span class="sxs-lookup"><span data-stu-id="7a773-114">The following code creates an Event Hubs client and sends a message to the hub.</span></span>

```csharp
EventHubsConnectionStringBuilder connectionStringBuilder = new EventHubsConnectionStringBuilder(eventHubConnectionString)
{
    EntityPath = eventHubEntityPath
};

EventHubClient eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
string message = $"Message {i}";
Console.WriteLine($"Sending message: {message}");
await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a773-115">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="7a773-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/eventhub/client)

## <a name="management-library"></a><span data-ttu-id="7a773-116">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="7a773-116">Management library</span></span>

<span data-ttu-id="7a773-117">Usare la libreria di gestione di Hub eventi per creare, aggiornare e rimuovere hub e gruppi di consumer.</span><span class="sxs-lookup"><span data-stu-id="7a773-117">Use the Event Hubs management library to create, update, and remove hubs and consumer groups.</span></span>

<span data-ttu-id="7a773-118">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="7a773-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7a773-119">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="7a773-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventHub
```

```bash
dotnet add package Microsoft.Azure.Management.EventHub
```

### <a name="code-example"></a><span data-ttu-id="7a773-120">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="7a773-120">Code Example</span></span>

<span data-ttu-id="7a773-121">Il codice seguente crea un nuovo hub eventi.</span><span class="sxs-lookup"><span data-stu-id="7a773-121">The following code creates a new event hub.</span></span>

```csharp
TokenCredentials creds = new TokenCredentials(token);
EventHubManagementClient ehClient = new EventHubManagementClient(creds)
{
    SubscriptionId = subscriptionId
};

EventHubCreateOrUpdateParameters ehParams = new EventHubCreateOrUpdateParameters()
{
    Location = location
};

Console.WriteLine("Creating Event Hub...");
await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
Console.WriteLine("Created Event Hub successfully.");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a773-122">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="7a773-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventhub/management)

## <a name="tutorials"></a><span data-ttu-id="7a773-123">Esercitazioni</span><span class="sxs-lookup"><span data-stu-id="7a773-123">Tutorials</span></span>

* [<span data-ttu-id="7a773-124">Inviare eventi a Hub eventi di Azure usando .NET Framework</span><span class="sxs-lookup"><span data-stu-id="7a773-124">Send events to Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-send)

* [<span data-ttu-id="7a773-125">Ricevere eventi da Hub eventi di Azure usando .NET Framework</span><span class="sxs-lookup"><span data-stu-id="7a773-125">Receive events from Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-receive-eph)

## <a name="samples"></a><span data-ttu-id="7a773-126">Esempi</span><span class="sxs-lookup"><span data-stu-id="7a773-126">Samples</span></span>

* [<span data-ttu-id="7a773-127">Esempi di Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="7a773-127">Azure Event Hubs Samples</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="7a773-128">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="7a773-128">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
