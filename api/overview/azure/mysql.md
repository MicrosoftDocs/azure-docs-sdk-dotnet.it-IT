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
# <a name="azure-database-for-mysql-libraries-for-net"></a><span data-ttu-id="17f6a-104">Librerie del database di Azure per MySQL per .NET</span><span class="sxs-lookup"><span data-stu-id="17f6a-104">Azure Database for MySQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="17f6a-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="17f6a-105">Overview</span></span>

<span data-ttu-id="17f6a-106">Usare i dati e le risorse archiviati nel [database di Azure per MySQL](/azure/mysql/overview).</span><span class="sxs-lookup"><span data-stu-id="17f6a-106">Work with data and resources stored in [Azure Database for MySQL](/azure/mysql/overview).</span></span>

## <a name="client-apis"></a><span data-ttu-id="17f6a-107">API client</span><span class="sxs-lookup"><span data-stu-id="17f6a-107">Client APIs</span></span>

<span data-ttu-id="17f6a-108">La libreria client consigliata per accedere al database di Azure per MySQL è [Connector/Net](https://dev.mysql.com/doc/connector-net/en) di MySQL.</span><span class="sxs-lookup"><span data-stu-id="17f6a-108">The recommended client library for accessing Azure Database for MySQL is MySQL's [Connector/Net](https://dev.mysql.com/doc/connector-net/en).</span></span> <span data-ttu-id="17f6a-109">Usare il pacchetto per connettersi al database ed eseguire direttamente le istruzioni SQL.</span><span class="sxs-lookup"><span data-stu-id="17f6a-109">Use the package to connect to the database and execute SQL statements directly.</span></span> 

<span data-ttu-id="17f6a-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/MySql.Data) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="17f6a-110">Install the [NuGet package](https://www.nuget.org/packages/MySql.Data) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="17f6a-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="17f6a-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package MySql.Data
```

#### <a name="net-core-cli"></a><span data-ttu-id="17f6a-112">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="17f6a-112">.NET Core CLI</span></span>

```bash
dotnet add package MySql.Data
```

### <a name="code-example"></a><span data-ttu-id="17f6a-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="17f6a-113">Code Example</span></span>

<span data-ttu-id="17f6a-114">Connettersi a un database MySQL ed eseguire una query:</span><span class="sxs-lookup"><span data-stu-id="17f6a-114">Connect to a MySQL database and execute a query:</span></span>

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

## <a name="samples"></a><span data-ttu-id="17f6a-115">Esempi</span><span class="sxs-lookup"><span data-stu-id="17f6a-115">Samples</span></span>

- [<span data-ttu-id="17f6a-116">Esempi di codice ADO.NET</span><span class="sxs-lookup"><span data-stu-id="17f6a-116">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="17f6a-117">Progettare un database MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="17f6a-117">Design a MySQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/mysql/tutorial-design-database-using-cli) 

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
