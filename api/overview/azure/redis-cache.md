---
title: Librerie di Cache Redis di Azure per .NET
description: Informazioni di riferimento sulle librerie di Cache Redis di Azure per .NET
keywords: Azure, .NET, SDK, API, Cache Redis
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: redis-cache
ms.openlocfilehash: 2316a179712b143b7e099f4592035c489d270bc3
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-redis-cache-libraries-for-net"></a><span data-ttu-id="812f8-104">Librerie di Cache Redis di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="812f8-104">Azure Redis Cache libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="812f8-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="812f8-105">Overview</span></span>

<span data-ttu-id="812f8-106">Cache Redis di Azure è una cache di dati sicura e un broker di messaggistica che offre velocità effettiva elevata e accesso ai dati a bassa latenza per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="812f8-106">Azure Redis Cache is a secure data cache and messaging broker that provides high throughput and low-latency access to data for applications.</span></span>  <span data-ttu-id="812f8-107">Per altre informazioni, vedere [Come usare Cache Redis di Azure](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="812f8-107">For more information, see [How to Use Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span></span>

## <a name="client-library"></a><span data-ttu-id="812f8-108">Libreria client</span><span class="sxs-lookup"><span data-stu-id="812f8-108">Client library</span></span>

<span data-ttu-id="812f8-109">Cache Redis di Azure è compatibile con tutte le API client Redis, incluso `StackExchange.Redis`.</span><span class="sxs-lookup"><span data-stu-id="812f8-109">Azure Redis Cache is compatible with any Redis client API, including `StackExchange.Redis`.</span></span>

<span data-ttu-id="812f8-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/StackExchange.Redis) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="812f8-110">Install the [NuGet package](https://www.nuget.org/packages/StackExchange.Redis) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="812f8-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="812f8-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a><span data-ttu-id="812f8-112">Esempio</span><span class="sxs-lookup"><span data-stu-id="812f8-112">Example</span></span>

<span data-ttu-id="812f8-113">Questo esempio mostra come connettersi a un'istanza del database Cache Redis, aggiungere alcune stringhe alla cache in base al nome e quindi recupera di nuovo le stringhe.</span><span class="sxs-lookup"><span data-stu-id="812f8-113">This example connects to a Redis Cache database instance, adds some strings to the cache by name, and then retrieves them again.</span></span>

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

## <a name="management-library"></a><span data-ttu-id="812f8-114">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="812f8-114">Management library</span></span>

<span data-ttu-id="812f8-115">La libreria di gestione di Cache Redis consente di gestire le risorse Cache Redis e le chiavi di accesso.</span><span class="sxs-lookup"><span data-stu-id="812f8-115">The Redis Cache management library allows you to manage Redis Cache resources and access keys.</span></span>

<span data-ttu-id="812f8-116">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="812f8-116">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="812f8-117">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="812f8-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a><span data-ttu-id="812f8-118">Esempio</span><span class="sxs-lookup"><span data-stu-id="812f8-118">Example</span></span>

<span data-ttu-id="812f8-119">Questo esempio mostra la creazione di una nuova Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="812f8-119">This example creates a new Redis Cache.</span></span>

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
> [<span data-ttu-id="812f8-120">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="812f8-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a><span data-ttu-id="812f8-121">Esempi</span><span class="sxs-lookup"><span data-stu-id="812f8-121">Samples</span></span>

* [<span data-ttu-id="812f8-122">Getting Started with Redis - Manage Redis - in .NET</span><span class="sxs-lookup"><span data-stu-id="812f8-122">Getting Started with Redis - Manage Redis - in .NET</span></span>](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache) (Introduzione a Redis: Gestire Redis in .NET)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
