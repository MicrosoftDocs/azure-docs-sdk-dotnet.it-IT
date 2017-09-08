---
title: API del database SQL di Azure per .NET
description: Informazioni di riferimento sulle librerie di archiviazione del database SQL di Azure per .NET
keywords: Azure, .NET, SDK, API, SQL, database
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: sql
ms.openlocfilehash: 110b7e554666a4fa6386d6715919684e121441a3
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-sql-database-apis-for-net"></a>API del database SQL di Azure per .NET

## <a name="overview"></a>Panoramica

Il [database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) è un database come servizio che usa il motore Microsoft SQL Server che supporta i dati relazionali, JSON, i dati spaziali e i dati XML. 

Per altre informazioni sull'uso del database SQL con .NET, vedere [Usare .NET con Visual Studio per connettersi a un database SQL di Azure ed eseguire query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).

## <a name="client-library"></a>Libreria client

Usare la libreria client SQL .NET per connettersi ed eseguire l'autenticazione nel database ed eseguire istruzioni T-SQL ad-hoc e stored procedure.

Installare il [pacchetto NuGet]( https://www.nuget.org/packages/System.Data.SqlClient) direttamente dalla [Console di Gestione pacchetti](https://docs.microsoft.com/nuget/tools/package-manager-console) di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package).

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package System.Data.SqlClient
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package System.Data.SqlClient
```

### <a name="code-example"></a>Esempio di codice

Questo esempio si connette a un database e legge righe da una tabella.

```csharp
/* Include this 'using' directive...
using System.Data.SqlClient;
*/

// Always store connection strings securely. 
string connectionString = "Server=tcp:[serverName].database.windows.net;" 
    + "Database=myDataBase;User ID=[loginname]@[serverName];Password=myPassword;"
    + "Trusted_Connection=False;Encrypt=True;";

// Best practice is to scope the SqlConnection to a "using" block
using (SqlConnection conn = new SqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    SqlCommand selectCommand = new SqlCommand("SELECT * FROM MyTable", conn);
    SqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/sql/client)

## <a name="management-library"></a>Libreria di gestione

Usare la libreria di gestione del database SQL di Azure per creare, gestire e ridimensionare le istanze del server del database SQL di Azure.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) direttamente dalla [Console di Gestione pacchetti](https://docs.microsoft.com/nuget/tools/package-manager-console) di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.Sql.Fluent
``` 

#### <a name="net-core-command-line"></a>Riga di comando di .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Sql.Fluent
```

### <a name="code-example"></a>Esempio di codice

Questo esempio crea una nuova istanza del server del database SQL e quindi crea un nuovo database in tale istanza.

```csharp
/* Include these 'using' directives...
using Microsoft.Azure.Management.Sql.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

string startAddress = "0.0.0.0";
string endAddress = "255.255.255.255";

// Create the SQL server instance
ISqlServer sqlServer = azure.SqlServers.Define("UniqueServerName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup("ResourceGroupName")
    .WithAdministratorLogin("UserName")
    .WithAdministratorPassword("Password")
    .WithNewFirewallRule(startAddress, endAddress)
    .Create();

// Create the database
ISqlDatabase sqlDb = sqlServer.Databases.Define("DatabaseName").Create();
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/sql/management)

## <a name="samples"></a>Esempi

- [Esempi di codice ADO.NET](/dotnet/framework/data/adonet/ado-net-code-examples)
- [Esempi di librerie di gestione di Azure per .NET per il database SQL](/dotnet/azure/dotnet-sdk-azure-sql-database-samples)

Visualizzare l'[elenco completo](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=sql+database) degli esempi di codice per il database SQL di Azure.

