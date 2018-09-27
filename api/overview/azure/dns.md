---
title: Librerie di DNS di Azure per .NET
description: Informazioni di riferimento sulle librerie di DNS di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: dns
ms.openlocfilehash: b9ab6359aaa1e4e9b6e99e7a7b007928d18f3453
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190194"
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
