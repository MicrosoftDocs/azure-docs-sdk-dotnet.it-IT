---
title: Esercitazioni per la messaggistica e IoT con .NET in Azure | Microsoft Docs
description: Inviare messaggi tra applicazioni cloud e tra dispositivi e il cloud usando .NET e i servizi di Azure.
author: camsoper
manager: douge
ms.assetid: 2ce6ea06-7b0b-45e6-8ca0-44e4e4030b82
ms.devlang: dotnet
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: casoper
ms.openlocfilehash: 0c3e81231ac88b2418778b83ecabcbb553608e24
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="net-tutorials-for-enterprise-messaging-and-internet-of-things-iot"></a><span data-ttu-id="59a1e-103">Esercitazioni .NET per la messaggistica aziendale e Internet delle cose</span><span class="sxs-lookup"><span data-stu-id="59a1e-103">.NET tutorials for enterprise messaging and Internet of Things (IoT)</span></span>

<span data-ttu-id="59a1e-104">La tabella seguente include collegamenti a esercitazioni dettagliate per l'invio e la lettura di messaggi tra applicazioni e dispositivi nel codice .NET tramite i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="59a1e-104">The following table links to in-depth tutorials for sending and reading messages between applications and devices in from your .NET code using Azure services.</span></span>

<span data-ttu-id="59a1e-105">Per esempi del codice sorgente, vedere l'elenco di [esempi di codice per i servizi di Azure](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span><span class="sxs-lookup"><span data-stu-id="59a1e-105">For sample source code, see the list of [Azure service samples](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span></span>


| | |
|---|---|
| <span data-ttu-id="59a1e-106">**Bus di servizio**</span><span class="sxs-lookup"><span data-stu-id="59a1e-106">**Service Bus**</span></span> | |
| <span data-ttu-id="59a1e-107">[Come usare le code del bus di servizio][1]</span><span class="sxs-lookup"><span data-stu-id="59a1e-107">[How to use Service Bus queues][1]</span></span> | <span data-ttu-id="59a1e-108">Creare code, inviare e ricevere messaggi ed eliminare code.</span><span class="sxs-lookup"><span data-stu-id="59a1e-108">Create queues, send and receive messages, and delete queues.</span></span> | 
| <span data-ttu-id="59a1e-109">[Come usare gli argomenti e le sottoscrizioni del bus di servizio][2]</span><span class="sxs-lookup"><span data-stu-id="59a1e-109">[How to use Service Bus topics and subscriptions][2]</span></span> | <span data-ttu-id="59a1e-110">Informazioni su come usare il modello di comunicazione pubblicazione/sottoscrizione con il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="59a1e-110">Learn how to use publish/subscribe communication model with Service Bus.</span></span>
| <span data-ttu-id="59a1e-111">[Uso del bus di servizio da .NET con AMQP 1.0][3]</span><span class="sxs-lookup"><span data-stu-id="59a1e-111">[Using Service Bus from .NET with AMQP 1.0][3]</span></span> | <span data-ttu-id="59a1e-112">Informazioni su come usare AMQP nelle applicazioni del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="59a1e-112">Learn how to use AMQP in you Service Bus applications.</span></span>
|<span data-ttu-id="59a1e-113">**Hub IoT**</span><span class="sxs-lookup"><span data-stu-id="59a1e-113">**IoT Hub**</span></span>|
| <span data-ttu-id="59a1e-114">[Connettere un dispositivo simulato all'hub IoT][4]</span><span class="sxs-lookup"><span data-stu-id="59a1e-114">[Connect a simulated device to your IoT Hub][4]</span></span> | <span data-ttu-id="59a1e-115">Creare un'identità del dispositivo, inviare messaggi ed elaborare i dati di telemetria dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="59a1e-115">Create a device identity, send messages, and process telemetry from your IoT Hub.</span></span> |   
| <span data-ttu-id="59a1e-116">[Elaborare i messaggi da dispositivo a cloud][5]</span><span class="sxs-lookup"><span data-stu-id="59a1e-116">[Process device-to-cloud messages][5]</span></span> | <span data-ttu-id="59a1e-117">Inviare messaggi da un dispositivo simulato ed elaborarli nel cloud.</span><span class="sxs-lookup"><span data-stu-id="59a1e-117">Send messages from a simulated device and process them in the cloud.</span></span> |
|<span data-ttu-id="59a1e-118">**Hub eventi**</span><span class="sxs-lookup"><span data-stu-id="59a1e-118">**Event Hub**</span></span>|
| <span data-ttu-id="59a1e-119">[Inviare eventi a un hub eventi][6]</span><span class="sxs-lookup"><span data-stu-id="59a1e-119">[Send events to an Event Hub][6]</span></span> | <span data-ttu-id="59a1e-120">Inviare eventi all'hub eventi da un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="59a1e-120">Send events to Event hub from a console application.</span></span>
| <span data-ttu-id="59a1e-121">[Ricevere eventi dall'hub eventi][7]</span><span class="sxs-lookup"><span data-stu-id="59a1e-121">[Receive events from Event Hubs][7]</span></span> | <span data-ttu-id="59a1e-122">Ricevere messaggi ed elaborarli in parallelo.</span><span class="sxs-lookup"><span data-stu-id="59a1e-122">Receive messages and process them in parallel.</span></span>


[1]: /azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues
[2]: /azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions
[3]: /azure/service-bus-messaging/service-bus-amqp-dotnet
[4]: /azure/iot-hub/iot-hub-csharp-csharp-getstarted
[5]: /azure/iot-hub/iot-hub-csharp-csharp-process-d2c
[6]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-send
[7]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph


