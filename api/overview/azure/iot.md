---
title: Librerie di Azure IoT per .NET
description: Informazioni di riferimento sulle librerie di Azure IoT per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: iot-hub
ms.openlocfilehash: 667663c5f5e3452fcc5ec0c4f3ded997370c5852
ms.sourcegitcommit: 7f1a1bf275d8489f8df266b746baa33d66fcb2c8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2018
ms.locfileid: "53737076"
---
# <a name="azure-iot-libraries-for-net"></a><span data-ttu-id="6036d-103">Librerie di Azure IoT per .NET</span><span class="sxs-lookup"><span data-stu-id="6036d-103">Azure IoT libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6036d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6036d-104">Overview</span></span>

<span data-ttu-id="6036d-105">L'[hub IoT di Azure](https://azure.microsoft.com/services/iot-hub/) è un servizio completamente gestito che consente comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="6036d-105">[Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="6036d-106">I dispositivi e le origini dati in una soluzione IoT possono variare da un semplice sensore connesso a una rete a un potente dispositivo di elaborazione autonomo.</span><span class="sxs-lookup"><span data-stu-id="6036d-106">Devices and data sources in an IoT solution can range from a simple network-connected sensor to a powerful, standalone computing device.</span></span> <span data-ttu-id="6036d-107">I dispositivi possono avere capacità di elaborazione, memoria, larghezza di banda e supporto dei protocolli di comunicazione limitati.</span><span class="sxs-lookup"><span data-stu-id="6036d-107">Devices may have limited processing capability, memory, communication bandwidth, and communication protocol support.</span></span> <span data-ttu-id="6036d-108">Gli [SDK per dispositivi](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) IoT consentono di implementare applicazioni client per un'ampia gamma di dispositivi e applicazioni back-end.</span><span class="sxs-lookup"><span data-stu-id="6036d-108">The IoT [device SDKs](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) enable you to implement client applications for a wide variety of devices and back-end applications.</span></span>

<span data-ttu-id="6036d-109">L'SDK per dispositivi per .NET semplifica la creazione di dispositivi .NET che si connettono all'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="6036d-109">The device SDK for .NET facilitates building devices running .NET that connect to Azure IoT Hub.</span></span>

<span data-ttu-id="6036d-110">L'SDK per servizi per .NET semplifica la creazione di applicazioni back-end .NET per la gestione e il controllo dei dispositivi dal cloud.</span><span class="sxs-lookup"><span data-stu-id="6036d-110">The service SDK for .NET facilitates building back-end applications using .NET that manage and allow controlling devices from the Cloud.</span></span>

<span data-ttu-id="6036d-111">[Altre informazioni su Azure IoT](https://docs.microsoft.com/azure/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="6036d-111">[Learn more about Azure IoT](https://docs.microsoft.com/azure/iot-hub/).</span></span>


## <a name="client-library"></a><span data-ttu-id="6036d-112">Libreria client</span><span class="sxs-lookup"><span data-stu-id="6036d-112">Client library</span></span>

<span data-ttu-id="6036d-113">Usare il client per dispositivi IoT .NET per connettersi all'hub IoT e inviare messaggi.</span><span class="sxs-lookup"><span data-stu-id="6036d-113">Use the .NET IoT devices client to connect and send messages to your IoT Hub.</span></span>

<span data-ttu-id="6036d-114">Installare il [pacchetto NuGet]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6036d-114">Install the [NuGet package]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6036d-115">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="6036d-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Devices.Client
```

```bash
dotnet add package Microsoft.Azure.Devices.Client
```
### <a name="code-examples"></a><span data-ttu-id="6036d-116">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="6036d-116">Code Examples</span></span> 

<span data-ttu-id="6036d-117">Questo esempio mostra come connettersi all'hub IoT e inviare un messaggio al secondo.</span><span class="sxs-lookup"><span data-stu-id="6036d-117">This example connects to the IoT Hub and sends one message per second.</span></span>

```csharp
string deviceKey = "<deviceKey>";
string deviceId = "<deviceId>";
string iotHubHostName = "<IoTHubHostname>";
var deviceAuthentication = new DeviceAuthenticationWithRegistrySymmetricKey(deviceId, deviceKey);

DeviceClient deviceClient = DeviceClient.Create(iotHubHostName, deviceAuthentication, TransportType.Mqtt);

while (true)
{
    double currentTemperature = 20 + Rand.NextDouble() * 15;
    double currentHumidity = 60 + Rand.NextDouble() * 20;

    var telemetryDataPoint = new
    {
        messageId = _messageId++,
        deviceId = deviceId,
        temperature = currentTemperature,
        humidity = currentHumidity
    };
    string messageString = JsonConvert.SerializeObject(telemetryDataPoint);
    Message message = new Message(Encoding.ASCII.GetBytes(messageString));
    message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

    await deviceClient.SendEventAsync(message);
    Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

    await Task.Delay(1000);
}
```


> [!div class="nextstepaction"]
> [<span data-ttu-id="6036d-118">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="6036d-118">Explore the client APIs</span></span>](/dotnet/api/overview/azure/iot/client)

## <a name="samples"></a><span data-ttu-id="6036d-119">Esempi</span><span class="sxs-lookup"><span data-stu-id="6036d-119">Samples</span></span>

- <span data-ttu-id="6036d-120">[Generic Web Service to Event Hub scenario](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/) (Scenario di invio dei dati da un servizio Web generico ad Hub eventi)</span><span class="sxs-lookup"><span data-stu-id="6036d-120">[Generic Web Service to Event Hub scenario](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/)</span></span>

<span data-ttu-id="6036d-121">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) degli esempi di codice per l'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="6036d-121">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) of Azure IoT Upsamples.</span></span>

<span data-ttu-id="6036d-122">Per altre indicazioni, vedere [Guida per gli sviluppatori dell'hub IoT di Azure](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide).</span><span class="sxs-lookup"><span data-stu-id="6036d-122">View the [Azure IoT Hub developer guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide) for more guidance.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
