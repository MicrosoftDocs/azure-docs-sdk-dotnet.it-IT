---
title: Librerie di Hub eventi di Azure per .NET
description: Informazioni di riferimento sulle librerie di Hub eventi di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: event-hubs
ms.openlocfilehash: 74c533bef598b90369009d68a759d35d122a368d
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190274"
---
# <a name="azure-event-hubs-libraries-for-net"></a><span data-ttu-id="0eda4-103">Librerie di Hub eventi di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="0eda4-103">Azure Event Hubs libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="0eda4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0eda4-104">Overview</span></span>

<span data-ttu-id="0eda4-105">Hub eventi di Azure è un servizio di inserimento di eventi e una piattaforma di streaming dei dati altamente scalabile.</span><span class="sxs-lookup"><span data-stu-id="0eda4-105">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service.</span></span>

<span data-ttu-id="0eda4-106">Per altre informazioni su Hub eventi di Azure, vedere [Che cos'è Hub eventi?](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="0eda4-106">To learn more about Azure Event Hubs, read the article [What is Event Hubs?](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>  <span data-ttu-id="0eda4-107">Per iniziare, vedere la [Guida alla programmazione per Hub eventi](/azure/event-hubs/event-hubs-programming-guide).</span><span class="sxs-lookup"><span data-stu-id="0eda4-107">To get started, check out the [Event Hubs Programming Guide](/azure/event-hubs/event-hubs-programming-guide).</span></span>

## <a name="client-library"></a><span data-ttu-id="0eda4-108">Libreria client</span><span class="sxs-lookup"><span data-stu-id="0eda4-108">Client library</span></span>

<span data-ttu-id="0eda4-109">Usare il client di Hub eventi per inviare e ricevere messaggi da e verso Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="0eda4-109">Use the Event Hubs client to send and receive messages to and from Event Hubs.</span></span>

<span data-ttu-id="0eda4-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="0eda4-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0eda4-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="0eda4-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventHubs
```

```bash
dotnet add package Microsoft.Azure.EventHubs
```

### <a name="code-example"></a><span data-ttu-id="0eda4-112">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="0eda4-112">Code Example</span></span>

<span data-ttu-id="0eda4-113">Il codice seguente mostra come creare un client di Hub eventi e inviare un messaggio all'hub.</span><span class="sxs-lookup"><span data-stu-id="0eda4-113">The following code creates an Event Hubs client and sends a message to the hub.</span></span>

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
> [<span data-ttu-id="0eda4-114">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="0eda4-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/eventhub/client)

## <a name="management-library"></a><span data-ttu-id="0eda4-115">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="0eda4-115">Management library</span></span>

<span data-ttu-id="0eda4-116">Usare la libreria di gestione di Hub eventi per creare, aggiornare e rimuovere hub e gruppi di consumer.</span><span class="sxs-lookup"><span data-stu-id="0eda4-116">Use the Event Hubs management library to create, update, and remove hubs and consumer groups.</span></span>

<span data-ttu-id="0eda4-117">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="0eda4-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0eda4-118">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="0eda4-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventHub
```

```bash
dotnet add package Microsoft.Azure.Management.EventHub
```

### <a name="code-example"></a><span data-ttu-id="0eda4-119">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="0eda4-119">Code Example</span></span>

<span data-ttu-id="0eda4-120">Il codice seguente crea un nuovo hub eventi.</span><span class="sxs-lookup"><span data-stu-id="0eda4-120">The following code creates a new event hub.</span></span>

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
> [<span data-ttu-id="0eda4-121">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="0eda4-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventhub/management)

## <a name="tutorials"></a><span data-ttu-id="0eda4-122">Esercitazioni</span><span class="sxs-lookup"><span data-stu-id="0eda4-122">Tutorials</span></span>

* [<span data-ttu-id="0eda4-123">Inviare eventi a Hub eventi di Azure usando .NET Framework</span><span class="sxs-lookup"><span data-stu-id="0eda4-123">Send events to Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-send)

* [<span data-ttu-id="0eda4-124">Ricevere eventi da Hub eventi di Azure usando .NET Framework</span><span class="sxs-lookup"><span data-stu-id="0eda4-124">Receive events from Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-receive-eph)

## <a name="samples"></a><span data-ttu-id="0eda4-125">Esempi</span><span class="sxs-lookup"><span data-stu-id="0eda4-125">Samples</span></span>

* [<span data-ttu-id="0eda4-126">Esempi di Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="0eda4-126">Azure Event Hubs Samples</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="0eda4-127">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="0eda4-127">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
