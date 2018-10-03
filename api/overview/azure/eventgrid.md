---
title: Librerie di Griglia di eventi di Azure per .NET
description: Informazioni di riferimento sulle librerie di Griglia di eventi di Azure per .NET
ms.date: 04/16/2018
ms.topic: reference
ms.service: event-grid
ms.openlocfilehash: 5b19f8aa8b28b3e4aef528da051b6e7d177f1a2f
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190394"
---
# <a name="azure-event-grid-libraries-for-net"></a><span data-ttu-id="febeb-103">Librerie di Griglia di eventi di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="febeb-103">Azure Event Grid libraries for .NET</span></span>

<span data-ttu-id="febeb-104">È possibile creare applicazioni basate su eventi che rimangono in ascolto e reagiscono a eventi dai servizi di Azure e da origini personalizzate usando la gestione semplice di eventi basati su HTTP con Griglia di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="febeb-104">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="febeb-105">[Altre informazioni](/azure/event-grid/overview) su Griglia di eventi di Azure e introduzione all'[esercitazione sugli eventi di archiviazione BLOB di Azure](/azure/storage/blobs/storage-blob-event-quickstart-powershell).</span><span class="sxs-lookup"><span data-stu-id="febeb-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart-powershell).</span></span> 

## <a name="client-sdk"></a><span data-ttu-id="febeb-106">Client SDK</span><span class="sxs-lookup"><span data-stu-id="febeb-106">Client SDK</span></span>

<span data-ttu-id="febeb-107">Creare eventi, eseguire l'autenticazione e inserire commenti negli argomenti usando Client SDK per Griglia di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="febeb-107">Create events, authenticate, and post to topics using the Azure Event Grid Client SDK.</span></span>

<span data-ttu-id="febeb-108">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="febeb-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="febeb-109">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="febeb-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="febeb-110">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="febeb-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.EventGrid 
```

### <a name="publish-events"></a><span data-ttu-id="febeb-111">Pubblicare eventi</span><span class="sxs-lookup"><span data-stu-id="febeb-111">Publish events</span></span>

<span data-ttu-id="febeb-112">Il codice seguente esegue l'autenticazione con Azure e pubblica un oggetto `List` di eventi di `EventGridEvent` di tipo personalizzato, in questo esempio `Contoso.Items.ItemsReceivedEvent`, in un argomento.</span><span class="sxs-lookup"><span data-stu-id="febeb-112">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceivedEvent` ) to a topic.</span></span> <span data-ttu-id="febeb-113">La chiave e l'indirizzo dell'endpoint dell'argomento usati nell'esempio possono essere recuperati da Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="febeb-113">The topic key and endpoint address used in the sample can be retrieved from Azure PowerShell:</span></span>

```powershell
$endpoint = (Get-AzureRmEventGridTopic -ResourceGroupName gridResourceGroup -Name <topic-name>).Endpoint
$keys = Get-AzureRmEventGridTopicKey -ResourceGroupName gridResourceGroup -Name <topic-name>
```

```csharp
string topicEndpoint = "https://<topic-name>.<region>-1.eventgrid.azure.net/api/events";
string topicKey = "<topic-key>";
string topicHostname = new Uri(topicEndpoint).Host;

TopicCredentials topicCredentials = new TopicCredentials(topicKey);
EventGridClient client = new EventGridClient(topicCredentials);

client.PublishEventsAsync(topicHostname, GetEventsList()).GetAwaiter().GetResult();
Console.Write("Published events to Event Grid.");

static IList<EventGridEvent> GetEventsList()
{
    List<EventGridEvent> eventsList = new List<EventGridEvent>();
    for (int i = 0; i < 1; i++)
    {
        eventsList.Add(new EventGridEvent()
        {
            Id = Guid.NewGuid().ToString(),
            EventType = "Contoso.Items.ItemReceivedEvent",
            Data = new ContosoItemReceivedEventData()
            {
                ItemUri = "ContosoSuperItemUri"
            },

            EventTime = DateTime.Now,
            Subject = "Door1",
            DataVersion = "2.0"
        });
    }
    return eventsList;
}
```

### <a name="consume-events"></a><span data-ttu-id="febeb-114">Utilizzare gli eventi</span><span class="sxs-lookup"><span data-stu-id="febeb-114">Consume events</span></span>

<span data-ttu-id="febeb-115">Questo frammento di codice utilizza eventi, tra cui un evento personalizzato `Contoso.Items.ItemsReceived`, nonché eventi attivati da altri servizi di Azure, ad esempio Archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="febeb-115">This snippet consumes events, including a custom event `Contoso.Items.ItemsReceived` as well as events triggered from other Azure services, such as Blob Storage.</span></span>

```csharp
string response = string.Empty;
string requestContent = await req.Content.ReadAsStringAsync();

EventGridSubscriber eventGridSubscriber = new EventGridSubscriber();

// Optionally add one or more custom event type mappings
eventGridSubscriber.AddOrUpdateCustomEventMapping("Contoso.Items.ItemReceived", typeof(ContosoItemReceivedEventData));

var events = eventGridSubscriber.DeserializeEventGridEvents(requestContent);            
 
foreach (EventGridEvent receivedEvent in events)
{
    if (receivedEvent.Data is SubscriptionValidationEventData)
    {
        SubscriptionValidationEventData eventData = (SubscriptionValidationEventData)receivedEvent.Data;
        log.Info($"Got SubscriptionValidation event data, validationCode: {eventData.ValidationCode},  validationUrl: {eventData.ValidationUrl}, topic: {eventGridEvent.Topic}");
        // Handle subscription validation
    }
    else if (receivedEvent.Data is StorageBlobCreatedEventData)
    {
        StorageBlobCreatedEventData eventData = (StorageBlobCreatedEventData)receivedEvent.Data;
        log.Info($"Got BlobCreated event data, blob URI {eventData.Url}");
        // Handle StorageBlobCreatedEventData
    }
    else if (receivedEvent.Data is ContosoItemReceivedEventData)
    {
        ContosoItemReceivedEventData eventData = (ContosoItemReceivedEventData)receivedEvent.Data;
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="febeb-116">Esplorare le API di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="febeb-116">Explore the publishing APIs</span></span>](/dotnet/api/overview/azure/eventgrid/publish)

## <a name="management-sdk"></a><span data-ttu-id="febeb-117">SDK di gestione</span><span class="sxs-lookup"><span data-stu-id="febeb-117">Management SDK</span></span>

<span data-ttu-id="febeb-118">Creare, aggiornare o eliminare istanze, argomenti e sottoscrizioni di Griglia di eventi con l'SDK di gestione.</span><span class="sxs-lookup"><span data-stu-id="febeb-118">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

<span data-ttu-id="febeb-119">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="febeb-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="febeb-120">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="febeb-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="febeb-121">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="febeb-121">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.EventGrid
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="febeb-122">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="febeb-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="febeb-123">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="febeb-123">Learn more</span></span>

- <span data-ttu-id="febeb-124">[Receive events using the Event Grid SDK](/azure/event-grid/receive-events) (Ricevere eventi tramite l'SDK di Griglia di eventi)</span><span class="sxs-lookup"><span data-stu-id="febeb-124">[Receive events using the Event Grid SDK](/azure/event-grid/receive-events)</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
