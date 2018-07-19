---
title: API del database SQL di Azure per .NET
description: Informazioni di riferimento sulle librerie di archiviazione del database SQL di Azure per .NET
keywords: Azure, .NET, SDK, API, SQL, database SQL
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: sql-database
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 8096e66be1263bc50648ef5b9b16f3fc2bd08ac8
ms.sourcegitcommit: 512e031ead61a578ac96835c8ea01829842740bf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2018
ms.locfileid: "39116677"
---
# <a name="azure-sql-database-apis-for-net"></a><span data-ttu-id="b5f13-104">API del database SQL di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="b5f13-104">Azure SQL Database APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="b5f13-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b5f13-105">Overview</span></span>

<span data-ttu-id="b5f13-106">Il [database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) è un database come servizio che usa il motore Microsoft SQL Server che supporta i dati relazionali, JSON, i dati spaziali e i dati XML.</span><span class="sxs-lookup"><span data-stu-id="b5f13-106">[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) is a database service using the Microsoft SQL Server engine that supports relational, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="b5f13-107">Per altre informazioni sull'uso del database SQL con .NET, vedere [Usare .NET con Visual Studio per connettersi a un database SQL di Azure ed eseguire query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="b5f13-107">To learn more about the using SQL Database with .NET, see [Use .NET with Visual Studio to connect and query an Azure SQL database](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).</span></span>

## <a name="client-library"></a><span data-ttu-id="b5f13-108">Libreria client</span><span class="sxs-lookup"><span data-stu-id="b5f13-108">Client library</span></span>

<span data-ttu-id="b5f13-109">Usare la libreria client SQL .NET per connettersi ed eseguire l'autenticazione nel database ed eseguire istruzioni T-SQL ad-hoc e stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5f13-109">Use the .NET SQL client library to connect and authenticate with your database and execute ad-hoc T-SQL statements and stored procedures.</span></span>

<span data-ttu-id="b5f13-110">Installare il [pacchetto NuGet]( https://www.nuget.org/packages/System.Data.SqlClient) direttamente dalla [Console di Gestione pacchetti](https://docs.microsoft.com/nuget/tools/package-manager-console) di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span><span class="sxs-lookup"><span data-stu-id="b5f13-110">Install the [NuGet package]( https://www.nuget.org/packages/System.Data.SqlClient) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="b5f13-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="b5f13-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package System.Data.SqlClient
```

#### <a name="net-core-cli"></a><span data-ttu-id="b5f13-112">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="b5f13-112">.NET Core CLI</span></span>

```bash
dotnet add package System.Data.SqlClient
```

### <a name="code-example"></a><span data-ttu-id="b5f13-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="b5f13-113">Code Example</span></span>

<span data-ttu-id="b5f13-114">Questo esempio si connette a un database e legge righe da una tabella.</span><span class="sxs-lookup"><span data-stu-id="b5f13-114">This example connects to a database and reads rows from a table.</span></span>

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
> [<span data-ttu-id="b5f13-115">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="b5f13-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/sql/client)

## <a name="management-library"></a><span data-ttu-id="b5f13-116">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="b5f13-116">Management library</span></span>

<span data-ttu-id="b5f13-117">Usare la libreria di gestione del database SQL di Azure per creare, gestire e ridimensionare le istanze del server del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5f13-117">Use the Azure SQL Database management library to create, manage, and scale Azure SQL Database server instances.</span></span>

<span data-ttu-id="b5f13-118">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) direttamente dalla [Console di Gestione pacchetti](https://docs.microsoft.com/nuget/tools/package-manager-console) di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span><span class="sxs-lookup"><span data-stu-id="b5f13-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="b5f13-119">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="b5f13-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Sql.Fluent
``` 

#### <a name="net-core-command-line"></a><span data-ttu-id="b5f13-120">Riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="b5f13-120">.NET Core command line</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Sql.Fluent
```

### <a name="code-example"></a><span data-ttu-id="b5f13-121">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="b5f13-121">Code Example</span></span>

<span data-ttu-id="b5f13-122">Questo esempio crea una nuova istanza del server del database SQL e quindi crea un nuovo database in tale istanza.</span><span class="sxs-lookup"><span data-stu-id="b5f13-122">This example creates a new SQL Database server instance and then creates a new database on that instance.</span></span>

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
> [<span data-ttu-id="b5f13-123">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="b5f13-123">Explore the management APIs</span></span>](/dotnet/api/overview/azure/sql/management)

## <a name="samples"></a><span data-ttu-id="b5f13-124">Esempi</span><span class="sxs-lookup"><span data-stu-id="b5f13-124">Samples</span></span>

- [<span data-ttu-id="b5f13-125">Esempi di codice ADO.NET</span><span class="sxs-lookup"><span data-stu-id="b5f13-125">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="b5f13-126">Esempi di librerie di gestione di Azure per .NET per il database SQL</span><span class="sxs-lookup"><span data-stu-id="b5f13-126">Azure management libraries for .NET samples for SQL Database</span></span>](/dotnet/azure/dotnet-sdk-azure-sql-database-samples)

<span data-ttu-id="b5f13-127">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=sql+database) degli esempi di codice per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5f13-127">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=sql+database) of Azure SQL Database samples.</span></span>

