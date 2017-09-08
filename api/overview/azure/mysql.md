---
title: Librerie del database di Azure per MySQL per .NET
description: Documentazione di riferimento per le librerie client .NET per il database di Azure per MySQL
keywords: Azure, .NET, SDK, API, SQL, database, MySQL
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: mysql
ms.openlocfilehash: 1bc373d63b0172fd554277a6ef30fa09772a395b
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-database-for-mysql-libraries-for-net"></a>Librerie del database di Azure per MySQL per .NET

## <a name="overview"></a>Panoramica

Usare i dati e le risorse archiviati nel [database di Azure per MySQL](/azure/mysql/overview).

## <a name="client-apis"></a>API client

La libreria client consigliata per accedere al database di Azure per MySQL è [Connector/Net](https://dev.mysql.com/doc/connector-net/en) di MySQL. Usare il pacchetto per connettersi al database ed eseguire direttamente le istruzioni SQL. 

Installare il [pacchetto NuGet](https://www.nuget.org/packages/MySql.Data) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package MySql.Data
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package MySql.Data
```

### <a name="code-example"></a>Esempio di codice

Connettersi a un database MySQL ed eseguire una query:

```csharp
/* Include this "using" directive...
using MySql.Data.MySqlClient;
*/

string connectionString = "Server=[servername].mysql.database.azure.com; " +
    "Database=myDataBase; Uid=[userid]@[servername]; Pwd=myPassword;";

// Best practice is to scope the MySqlConnection to a "using" block
using (MySqlConnection conn = new MySqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    MySqlCommand selectCommand = new MySqlCommand("SELECT * FROM MyTable", conn);
    MySqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

## <a name="samples"></a>Esempi

- [Esempi di codice ADO.NET](/dotnet/framework/data/adonet/ado-net-code-examples)
- [Progettare un database MySQL tramite l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/azure/mysql/tutorial-design-database-using-cli) 

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
