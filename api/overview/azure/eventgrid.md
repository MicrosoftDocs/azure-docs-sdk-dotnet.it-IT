---
title: Librerie di Griglia di eventi di Azure per .NET
description: Informazioni di riferimento sulle librerie di Griglia di eventi di Azure per .NET
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/16/2018
ms.topic: reference
ms.devlang: dotnet
ms.service: event-grid
ms.custom: devcenter
ms.openlocfilehash: 894b8a5beaf0507ab50e8eed6a5ab20d10a71ba6
ms.sourcegitcommit: 61638b504b6c4d96b357894835c80c2680a99fe6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750599"
---
# <a name="azure-event-grid-libraries-for-net"></a>Librerie di Griglia di eventi di Azure per .NET

È possibile creare applicazioni basate su eventi che rimangono in ascolto e reagiscono a eventi dai servizi di Azure e da origini personalizzate usando la gestione semplice di eventi basati su HTTP con Griglia di eventi di Azure.

[Altre informazioni](/azure/event-grid/overview) su Griglia di eventi di Azure e introduzione all'[esercitazione sugli eventi di archiviazione BLOB di Azure](/azure/storage/blobs/storage-blob-event-quickstart-powershell). 

## <a name="client-sdk"></a>Client SDK

Creare eventi, eseguire l'autenticazione e inserire commenti negli argomenti usando Client SDK per Griglia di eventi di Azure.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.EventGrid
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Microsoft.Azure.EventGrid 
```

### <a name="publish-events"></a>Pubblicare eventi

Il codice seguente esegue l'autenticazione con Azure e pubblica un oggetto `List` di eventi di `EventGridEvent` di tipo personalizzato, in questo esempio `Contoso.Items.ItemsReceivedEvent`, in un argomento. La chiave e l'indirizzo dell'endpoint dell'argomento usati nell'esempio possono essere recuperati da Azure PowerShell:

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

### <a name="consume-events"></a>Utilizzare gli eventi

Questo frammento di codice utilizza eventi, tra cui un evento personalizzato `Contoso.Items.ItemsReceived`, nonché eventi attivati da altri servizi di Azure, ad esempio Archiviazione BLOB.

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
> [Esplorare le API client](/dotnet/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>SDK di gestione

Creare, aggiornare o eliminare istanze, argomenti e sottoscrizioni di Griglia di eventi con l'SDK di gestione.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].


#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.EventGrid
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Microsoft.Azure.Management.EventGrid
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a>Altre informazioni

- [Receive events using the Event Grid SDK](/azure/event-grid/receive-events) (Ricevere eventi tramite l'SDK di Griglia di eventi)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
