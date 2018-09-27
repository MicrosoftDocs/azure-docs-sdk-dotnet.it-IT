---
title: Librerie del Database di Azure per PostgreSQL per .NET
description: Documentazione di riferimento per le librerie client .NET per il Database di Azure per PostgreSQL
ms.date: 10/19/2017
ms.topic: reference
ms.service: postgresql
ms.openlocfilehash: 4137e024eadba93c9cb3e94c1e7478d0816f8370
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190746"
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a><span data-ttu-id="fab81-103">Librerie del Database di Azure per PostgreSQL per .NET</span><span class="sxs-lookup"><span data-stu-id="fab81-103">Azure Database for PostgreSQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="fab81-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="fab81-104">Overview</span></span>

<span data-ttu-id="fab81-105">Usare i dati e le risorse archiviati nel [Database di Azure per PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span><span class="sxs-lookup"><span data-stu-id="fab81-105">Work with data and resources stored in [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-api"></a><span data-ttu-id="fab81-106">API client</span><span class="sxs-lookup"><span data-stu-id="fab81-106">Client API</span></span>

<span data-ttu-id="fab81-107">La libreria client consigliata per l'accesso al Database di Azure per PostgreSQL è il [provider di dati ADO.NET Npgsql](http://www.npgsql.org/) open source.</span><span class="sxs-lookup"><span data-stu-id="fab81-107">The recommended client library for accessing Azure Database for PostgreSQL is the open-source [Npgsql ADO.NET data provider](http://www.npgsql.org/).</span></span> <span data-ttu-id="fab81-108">Usare il provider ADO.NET per connettersi al database ed eseguire istruzioni SQL direttamente o tramite Entity Framework con i provider [Entity Framework 6](http://www.npgsql.org/ef6/index.html) o [Entity Framework Core](http://www.npgsql.org/efcore/index.html) di Npgsql.</span><span class="sxs-lookup"><span data-stu-id="fab81-108">Use the ADO.NET provider to connect to the database and execute SQL statements directly or through Entity Framework with the Npgsql's [Entity Framework 6](http://www.npgsql.org/ef6/index.html) or [Entity Framework Core](http://www.npgsql.org/efcore/index.html) providers.</span></span>

<span data-ttu-id="fab81-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Npgsql) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="fab81-109">Install the [NuGet package](https://www.nuget.org/packages/Npgsql) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="fab81-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="fab81-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a><span data-ttu-id="fab81-111">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="fab81-111">.NET Core CLI</span></span>

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a><span data-ttu-id="fab81-112">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="fab81-112">Code Example</span></span>

```csharp
/* Include this 'using' directive...
using Npgsql;
*/

// Always store connection strings securely. 
string connectionString = "Server=[servername].postgres.database.azure.com; " +
    "Port=5432; Database=myDataBase; User Id=[userid]@[servername]; Password=password;";

// Best practice is to scope the NpgsqlConnection to a "using" block
using (NpgsqlConnection conn = new NpgsqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    NpgsqlCommand selectCommand = new NpgsqlCommand("SELECT * FROM MyTable", conn);
    NpgsqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

### <a name="samples"></a><span data-ttu-id="fab81-113">Esempi</span><span class="sxs-lookup"><span data-stu-id="fab81-113">Samples</span></span>

- [<span data-ttu-id="fab81-114">Esempi di codice ADO.NET</span><span class="sxs-lookup"><span data-stu-id="fab81-114">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="fab81-115">Progettare un database PostgreSQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="fab81-115">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
