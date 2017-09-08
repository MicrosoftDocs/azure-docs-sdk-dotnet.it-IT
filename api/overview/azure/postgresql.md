---
title: Librerie del Database di Azure per PostgreSQL per .NET
description: Documentazione di riferimento per le librerie client .NET per il Database di Azure per PostgreSQL
keywords: Azure, .NET ODBC, SDK, API, SQL, ADO.NET, database, PostGres, PostgreSQL
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: postgresql
ms.openlocfilehash: 899002b12dd36e6b23a05c8516670ff841abed79
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a>Librerie del Database di Azure per PostgreSQL per .NET

## <a name="overview"></a>Panoramica

Usare i dati e le risorse archiviati nel [Database di Azure per PostgreSQL](https://docs.microsoft.com/azure/postgresql/).

## <a name="client-api"></a>API client

La libreria client consigliata per l'accesso al Database di Azure per PostgreSQL è il [provider di dati ADO.NET Npgsql](http://www.npgsql.org/) open source. Usare il provider ADO.NET per connettersi al database ed eseguire istruzioni SQL direttamente o tramite Entity Framework con i provider [Entity Framework 6](http://www.npgsql.org/ef6/index.html) o [Entity Framework Core](http://www.npgsql.org/efcore/index.html) di Npgsql.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Npgsql) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di.NET Core CLI][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a>Esempio di codice

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

### <a name="samples"></a>Esempi

- [Esempi di codice ADO.NET](/dotnet/framework/data/adonet/ado-net-code-examples)
- [Progettare un database PostgreSQL usando l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) [PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console [DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package