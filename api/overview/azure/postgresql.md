---
title: Librerie del Database di Azure per PostgreSQL per .NET
description: Documentazione di riferimento per le librerie client .NET per il Database di Azure per PostgreSQL
keywords: Azure, .NET ODBC, SDK, API, SQL, ADO.NET, database, PostGres, PostgreSQL
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: postgresql
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 7a8c1965432d5cca36665bce3963c30cdaee9205
ms.sourcegitcommit: 4dba7cd869bddff3dee7315d258522dc4879abce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2017
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a><span data-ttu-id="bf585-104">Librerie del Database di Azure per PostgreSQL per .NET</span><span class="sxs-lookup"><span data-stu-id="bf585-104">Azure Database for PostgreSQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="bf585-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="bf585-105">Overview</span></span>

<span data-ttu-id="bf585-106">Usare i dati e le risorse archiviati nel [Database di Azure per PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span><span class="sxs-lookup"><span data-stu-id="bf585-106">Work with data and resources stored in [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-api"></a><span data-ttu-id="bf585-107">API client</span><span class="sxs-lookup"><span data-stu-id="bf585-107">Client API</span></span>

<span data-ttu-id="bf585-108">La libreria client consigliata per l'accesso al Database di Azure per PostgreSQL è il [provider di dati ADO.NET Npgsql](http://www.npgsql.org/) open source.</span><span class="sxs-lookup"><span data-stu-id="bf585-108">The recommended client library for accessing Azure Database for PostgreSQL is the open-source [Npgsql ADO.NET data provider](http://www.npgsql.org/).</span></span> <span data-ttu-id="bf585-109">Usare il provider ADO.NET per connettersi al database ed eseguire istruzioni SQL direttamente o tramite Entity Framework con i provider [Entity Framework 6](http://www.npgsql.org/ef6/index.html) o [Entity Framework Core](http://www.npgsql.org/efcore/index.html) di Npgsql.</span><span class="sxs-lookup"><span data-stu-id="bf585-109">Use the ADO.NET provider to connect to the database and execute SQL statements directly or through Entity Framework with the Npgsql's [Entity Framework 6](http://www.npgsql.org/ef6/index.html) or [Entity Framework Core](http://www.npgsql.org/efcore/index.html) providers.</span></span>

<span data-ttu-id="bf585-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Npgsql) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="bf585-110">Install the [NuGet package](https://www.nuget.org/packages/Npgsql) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="bf585-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="bf585-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a><span data-ttu-id="bf585-112">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="bf585-112">.NET Core CLI</span></span>

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a><span data-ttu-id="bf585-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="bf585-113">Code Example</span></span>

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

### <a name="samples"></a><span data-ttu-id="bf585-114">Esempi</span><span class="sxs-lookup"><span data-stu-id="bf585-114">Samples</span></span>

- [<span data-ttu-id="bf585-115">Esempi di codice ADO.NET</span><span class="sxs-lookup"><span data-stu-id="bf585-115">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="bf585-116">Progettare un database PostgreSQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="bf585-116">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
