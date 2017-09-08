---
title: Librerie di DNS di Azure per .NET
description: Informazioni di riferimento sulle librerie di DNS di Azure per .NET
keywords: Azure, .NET, SDK, API, DNS
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 57c578f12ea426dc5784658338473f0044d21e5c
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-dns-libraries-for-net"></a>Librerie di DNS di Azure per .NET

Usare le librerie di DNS Microsoft Azure per .NET per creare e modificare le zone e i record DNS ospitati in Azure. Le zone e i record vengono gestiti come risorse di Azure. Per altre informazioni, vedere [Panoramica di DNS di Azure](/azure/dns/dns-overview).

## <a name="management-library"></a>Libreria di gestione

Usare la libreria di gestione per creare e modificare le zone e i record DNS ospitati in Azure.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a>Esempio

L'esempio seguente crea una nuova zona DNS.

```csharp
/*
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
*/
Microsoft.Rest.ServiceClientCredentials serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
DnsManagementClient dnsClient = new DnsManagementClient(serviceCreds);            
Zone dnsZoneParams = new Zone("global");
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");
Zone dnsZone =
    await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a>Esempi

* [Progetto di esempio di Azure DNS .NET SDK](https://www.microsoft.com/download/details.aspx?id=47268)

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
