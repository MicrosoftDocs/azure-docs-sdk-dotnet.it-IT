---
title: Librerie di Hub eventi di Azure per .NET
description: Informazioni di riferimento sulle librerie di Hub eventi di Azure per .NET
keywords: Azure, .NET, SDK, API, Hub eventi
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: event-hubs
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2ec234959ffc46d2399d1c763e05f173a311b0d2
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2017
---
# <a name="azure-event-hubs-libraries-for-net"></a>Librerie di Hub eventi di Azure per .NET

## <a name="overview"></a>Panoramica

Hub eventi di Azure è un servizio di inserimento di eventi e una piattaforma di streaming dei dati altamente scalabile.

Per altre informazioni su Hub eventi di Azure, vedere [Che cos'è Hub eventi?](/azure/event-hubs/event-hubs-what-is-event-hubs).  Per iniziare, vedere la [Guida alla programmazione per Hub eventi](/azure/event-hubs/event-hubs-programming-guide).

## <a name="client-library"></a>Libreria client

Usare il client di Hub eventi per inviare e ricevere messaggi da e verso Hub eventi.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.EventHubs
```

```bash
dotnet add package Microsoft.Azure.EventHubs
```

### <a name="code-example"></a>Esempio di codice

Il codice seguente mostra come creare un client di Hub eventi e inviare un messaggio all'hub.

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
> [Esplorare le API client](/dotnet/api/overview/azure/eventhub/client)

## <a name="management-library"></a>Libreria di gestione

Usare la libreria di gestione di Hub eventi per creare, aggiornare e rimuovere hub e gruppi di consumer.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.EventHub
```

```bash
dotnet add package Microsoft.Azure.Management.EventHub
```

### <a name="code-example"></a>Esempio di codice

Il codice seguente crea un nuovo hub eventi.

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
> [Esplorare le API di gestione](/dotnet/api/overview/azure/eventhub/management)

## <a name="tutorials"></a>Esercitazioni

* [Inviare eventi a Hub eventi di Azure usando .NET Framework](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-send)

* [Ricevere eventi da Hub eventi di Azure usando .NET Framework](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-receive-eph)

## <a name="samples"></a>Esempi

* [Esempi di Hub eventi di Azure](https://github.com/Azure/azure-event-hubs/tree/master/samples)

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
