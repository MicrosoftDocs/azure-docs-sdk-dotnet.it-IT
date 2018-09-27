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
# <a name="azure-redis-cache-libraries-for-net"></a><span data-ttu-id="04372-103">Librerie di Cache Redis di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="04372-103">Azure Redis Cache libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="04372-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="04372-104">Overview</span></span>

<span data-ttu-id="04372-105">Cache Redis di Azure è una cache di dati sicura e un broker di messaggistica che offre velocità effettiva elevata e accesso ai dati a bassa latenza per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="04372-105">Azure Redis Cache is a secure data cache and messaging broker that provides high throughput and low-latency access to data for applications.</span></span>  <span data-ttu-id="04372-106">Per altre informazioni, vedere [Come usare Cache Redis di Azure](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="04372-106">For more information, see [How to Use Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span></span>

## <a name="client-library"></a><span data-ttu-id="04372-107">Libreria client</span><span class="sxs-lookup"><span data-stu-id="04372-107">Client library</span></span>

<span data-ttu-id="04372-108">Cache Redis di Azure è compatibile con tutte le API client Redis, incluso `StackExchange.Redis`.</span><span class="sxs-lookup"><span data-stu-id="04372-108">Azure Redis Cache is compatible with any Redis client API, including `StackExchange.Redis`.</span></span>

<span data-ttu-id="04372-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/StackExchange.Redis) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="04372-109">Install the [NuGet package](https://www.nuget.org/packages/StackExchange.Redis) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="04372-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="04372-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a><span data-ttu-id="04372-111">Esempio</span><span class="sxs-lookup"><span data-stu-id="04372-111">Example</span></span>

<span data-ttu-id="04372-112">Questo esempio mostra come connettersi a un'istanza del database Cache Redis, aggiungere alcune stringhe alla cache in base al nome e quindi recupera di nuovo le stringhe.</span><span class="sxs-lookup"><span data-stu-id="04372-112">This example connects to a Redis Cache database instance, adds some strings to the cache by name, and then retrieves them again.</span></span>

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

## <a name="management-library"></a><span data-ttu-id="04372-113">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="04372-113">Management library</span></span>

<span data-ttu-id="04372-114">La libreria di gestione di Cache Redis consente di gestire le risorse Cache Redis e le chiavi di accesso.</span><span class="sxs-lookup"><span data-stu-id="04372-114">The Redis Cache management library allows you to manage Redis Cache resources and access keys.</span></span>

<span data-ttu-id="04372-115">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="04372-115">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="04372-116">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="04372-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a><span data-ttu-id="04372-117">Esempio</span><span class="sxs-lookup"><span data-stu-id="04372-117">Example</span></span>

<span data-ttu-id="04372-118">Questo esempio mostra la creazione di una nuova Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="04372-118">This example creates a new Redis Cache.</span></span>

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
> [<span data-ttu-id="04372-119">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="04372-119">Explore the management APIs</span></span>](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a><span data-ttu-id="04372-120">Esempi</span><span class="sxs-lookup"><span data-stu-id="04372-120">Samples</span></span>

* <span data-ttu-id="04372-121">[Getting Started with Redis - Manage Redis - in .NET](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache) (Introduzione a Redis: Gestire Redis in .NET)</span><span class="sxs-lookup"><span data-stu-id="04372-121">[Getting Started with Redis - Manage Redis - in .NET](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache)</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
