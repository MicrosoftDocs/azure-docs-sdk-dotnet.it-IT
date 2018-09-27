---
title: Librerie di Cache Redis di Azure per .NET
description: Informazioni di riferimento sulle librerie di Cache Redis di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: redis-cache
ms.openlocfilehash: cc043bbc6ea5915f7b6c2265b606210efb72d9d0
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190524"
---
# <a name="azure-redis-cache-libraries-for-net"></a>Librerie di Cache Redis di Azure per .NET

## <a name="overview"></a>Panoramica

Cache Redis di Azure è una cache di dati sicura e un broker di messaggistica che offre velocità effettiva elevata e accesso ai dati a bassa latenza per le applicazioni.  Per altre informazioni, vedere [Come usare Cache Redis di Azure](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).

## <a name="client-library"></a>Libreria client

Cache Redis di Azure è compatibile con tutte le API client Redis, incluso `StackExchange.Redis`.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/StackExchange.Redis) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a>Esempio

Questo esempio mostra come connettersi a un'istanza del database Cache Redis, aggiungere alcune stringhe alla cache in base al nome e quindi recupera di nuovo le stringhe.

```csharp
/* Include this "using" directive.
using StackExchange.Redis;
*/

ConnectionMultiplexer connection = 
    ConnectionMultiplexer.Connect("contoso.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    IDatabase cache = connection.GetDatabase();

// Perform cache operations using the cache object...
// Simple put of integral data types into the cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from the cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

## <a name="management-library"></a>Libreria di gestione

La libreria di gestione di Cache Redis consente di gestire le risorse Cache Redis e le chiavi di accesso.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a>Esempio

Questo esempio mostra la creazione di una nuova Cache Redis.

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.Redis.Fluent;
*/

IRedisCache redisCache1 = azure.RedisCaches.Define("RedisCacheName")
    .WithRegion(Region.USCentral)
    .WithNewResourceGroup("ResourceGroupName")
    .WithBasicSku()
    .Create();
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a>Esempi

* [Getting Started with Redis - Manage Redis - in .NET](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache) (Introduzione a Redis: Gestire Redis in .NET)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
