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
# <a name="azure-iot-libraries-for-net"></a>Librerie di Azure IoT per .NET

## <a name="overview"></a>Panoramica

L'[hub IoT di Azure](https://azure.microsoft.com/services/iot-hub/) è un servizio completamente gestito che consente comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione.

I dispositivi e le origini dati in una soluzione IoT possono variare da un semplice sensore connesso a una rete a un potente dispositivo di elaborazione autonomo. I dispositivi possono avere capacità di elaborazione, memoria, larghezza di banda e supporto dei protocolli di comunicazione limitati. Gli [SDK per dispositivi](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) IoT consentono di implementare applicazioni client per un'ampia gamma di dispositivi e applicazioni back-end.

L'SDK per dispositivi per .NET semplifica la creazione di dispositivi .NET che si connettono all'hub IoT di Azure.

L'SDK per servizi per .NET semplifica la creazione di applicazioni back-end .NET per la gestione e il controllo dei dispositivi dal cloud.

[Altre informazioni su Azure IoT](https://docs.microsoft.com/azure/iot-hub/).


## <a name="client-library"></a>Libreria client

Usare il client per dispositivi IoT .NET per connettersi all'hub IoT e inviare messaggi.

Installare il [pacchetto NuGet]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Devices.Client
```

```bash
dotnet add package Microsoft.Azure.Devices.Client
```
### <a name="code-examples"></a>Esempi di codice 

Questo esempio mostra come connettersi all'hub IoT e inviare un messaggio al secondo.

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
> [Esplorare le API client](/dotnet/api/overview/azure/iot/client)

## <a name="samples"></a>Esempi

- [Generic Web Service to Event Hub scenario](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/) (Scenario di invio dei dati da un servizio Web generico ad Hub eventi)

Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) degli esempi di codice per l'hub IoT di Azure.

Per altre indicazioni, vedere [Guida per gli sviluppatori dell'hub IoT di Azure](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide).

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
