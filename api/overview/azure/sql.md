---
title: API del database SQL di Azure per .NET
description: Informazioni di riferimento sulle librerie di archiviazione del database SQL di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: sql-database
ms.openlocfilehash: e4c1620ddf488952c6720b9bedf2521c6512b9a3
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190634"
---
# <a name="azure-sql-database-apis-for-net"></a><span data-ttu-id="57f30-103">API del database SQL di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="57f30-103">Azure SQL Database APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="57f30-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="57f30-104">Overview</span></span>

<span data-ttu-id="57f30-105">Il [database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) è un database come servizio che usa il motore Microsoft SQL Server che supporta i dati relazionali, JSON, i dati spaziali e i dati XML.</span><span class="sxs-lookup"><span data-stu-id="57f30-105">[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) is a database service using the Microsoft SQL Server engine that supports relational, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="57f30-106">Per altre informazioni sull'uso del database SQL con .NET, vedere [Usare .NET con Visual Studio per connettersi a un database SQL di Azure ed eseguire query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="57f30-106">To learn more about the using SQL Database with .NET, see [Use .NET with Visual Studio to connect and query an Azure SQL database](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).</span></span>

## <a name="client-library"></a><span data-ttu-id="57f30-107">Libreria client</span><span class="sxs-lookup"><span data-stu-id="57f30-107">Client library</span></span>

<span data-ttu-id="57f30-108">Usare la libreria client SQL .NET per connettersi ed eseguire l'autenticazione nel database ed eseguire istruzioni T-SQL ad-hoc e stored procedure.</span><span class="sxs-lookup"><span data-stu-id="57f30-108">Use the .NET SQL client library to connect and authenticate with your database and execute ad-hoc T-SQL statements and stored procedures.</span></span>

<span data-ttu-id="57f30-109">Installare il [pacchetto NuGet]( https://www.nuget.org/packages/System.Data.SqlClient) direttamente dalla [Console di Gestione pacchetti](https://docs.microsoft.com/nuget/tools/package-manager-console) di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span><span class="sxs-lookup"><span data-stu-id="57f30-109">Install the [NuGet package]( https://www.nuget.org/packages/System.Data.SqlClient) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="57f30-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="57f30-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package System.Data.SqlClient
```

#### <a name="net-core-cli"></a><span data-ttu-id="57f30-111">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="57f30-111">.NET Core CLI</span></span>

```bash
dotnet add package System.Data.SqlClient
```

### <a name="code-example"></a><span data-ttu-id="57f30-112">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="57f30-112">Code Example</span></span>

<span data-ttu-id="57f30-113">Questo esempio si connette a un database e legge righe da una tabella.</span><span class="sxs-lookup"><span data-stu-id="57f30-113">This example connects to a database and reads rows from a table.</span></span>

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
> [<span data-ttu-id="57f30-114">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="57f30-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/sql/client)

## <a name="management-library"></a><span data-ttu-id="57f30-115">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="57f30-115">Management library</span></span>

<span data-ttu-id="57f30-116">Usare la libreria di gestione del database SQL di Azure per creare, gestire e ridimensionare le istanze del server di database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="57f30-116">Use the Azure SQL Database management library to create, manage, and scale Azure SQL Database server instances.</span></span>

<span data-ttu-id="57f30-117">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) direttamente dalla [Console di Gestione pacchetti](https://docs.microsoft.com/nuget/tools/package-manager-console) di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span><span class="sxs-lookup"><span data-stu-id="57f30-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="57f30-118">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="57f30-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Sql.Fluent
``` 

#### <a name="net-core-command-line"></a><span data-ttu-id="57f30-119">Riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="57f30-119">.NET Core command line</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Sql.Fluent
```

### <a name="code-example"></a><span data-ttu-id="57f30-120">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="57f30-120">Code Example</span></span>

<span data-ttu-id="57f30-121">Questo esempio crea una nuova istanza del server di database SQL e quindi crea un nuovo database in tale istanza.</span><span class="sxs-lookup"><span data-stu-id="57f30-121">This example creates a new SQL Database server instance and then creates a new database on that instance.</span></span>

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
> [<span data-ttu-id="57f30-122">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="57f30-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/sql/management)

## <a name="samples"></a><span data-ttu-id="57f30-123">Esempi</span><span class="sxs-lookup"><span data-stu-id="57f30-123">Samples</span></span>

- [<span data-ttu-id="57f30-124">Esempi di codice ADO.NET</span><span class="sxs-lookup"><span data-stu-id="57f30-124">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="57f30-125">Esempi di librerie di gestione di Azure per .NET per il database SQL</span><span class="sxs-lookup"><span data-stu-id="57f30-125">Azure management libraries for .NET samples for SQL Database</span></span>](/dotnet/azure/dotnet-sdk-azure-sql-database-samples)

<span data-ttu-id="57f30-126">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=sql+database) degli esempi di codice per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="57f30-126">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=sql+database) of Azure SQL Database samples.</span></span>

