---
title: Introduzione alle API di Azure .NET e .NET Core
description: Introduzione all'uso di base delle librerie di Azure per .NET e .NET Core con la propria sottoscrizione di Azure.
keywords: Azure, .NET, .NET Core, ASP.NET, ASP.NET Core SDK, API, autenticazione, introduzione
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 07/17/2018
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: a8775993e71566b7659a8ae8ceb2c376ece14e45
ms.sourcegitcommit: 779c1b202d3670cfa0b9428c89f830cad9ec7e9d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2018
ms.locfileid: "39135779"
---
# <a name="get-started-with-the-azure-net-and-net-core-apis"></a>Introduzione alle API di Azure .NET e .NET Core

Questa esercitazione illustra l'utilizzo di alcune [API di Azure per .NET](/dotnet/api/overview/azure/).  Verranno eseguite operazioni per la configurazione dell'autenticazione, la creazione e l'uso di un account di archiviazione di Azure, la creazione e l'uso di un database SQL di Azure, la distribuzione di alcune macchine virtuali e la distribuzione di un'app Web del Servizio app di Azure da GitHub.

## <a name="prerequisites"></a>Prerequisiti

- Un account Azure. Se non è disponibile, [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/free/)
- [Azure PowerShell](/powershell/azure/install-azurerm-ps)

## <a name="set-up-authentication"></a>Configurare l'autenticazione

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="create-a-new-project"></a>Creare un nuovo progetto 

Creare un nuovo progetto di applicazione console.  In Visual Studio eseguire questa operazione facendo clic su **File**, **Nuovo** e quindi su **Progetto**.  Nei modelli di Visual C# selezionare **App console (.NET Core)**, assegnare un nome al progetto e quindi fare clic su **OK**.

![Finestra di dialogo Nuovo progetto](media/dotnet-sdk-azure-get-started/new-project.png)

Dopo la creazione della nuova app console, aprire la console di Gestione pacchetti facendo clic su **Strumenti**, **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.  Nella console ottenere i pacchetti necessari eseguendo i tre comandi seguenti:

```powershell
# Azure Management Libraries for .NET (Fluent)
Install-Package Microsoft.Azure.Management.Fluent

# Azure Store client libraries
Install-Package WindowsAzure.Storage

# SQL Database client libraries
Install-Package System.Data.SqlClient
```

## <a name="directives"></a>Direttive

Modificare il file `Program.cs` dell'applicazione.  Sostituire le direttive `using` all'inizio del file con il codice seguente:

```csharp
using System;
using System.Linq;
using Microsoft.Azure.Management.Compute.Fluent;
using Microsoft.Azure.Management.Compute.Fluent.Models;
using Microsoft.Azure.Management.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Data.SqlClient;
```

## <a name="create-a-virtual-machine"></a>Creare una macchina virtuale

Questo esempio distribuisce una macchina virtuale. 

Sostituire il metodo `Main` con il codice seguente.  Assicurarsi di specificare valori effettivi per `username` e `password` per la macchina virtuale.

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string username = "MY_USERNAME";
    string password = "MY_PASSWORD";
    string rgName = "sampleResourceGroup";
    string windowsVmName = "sampleWindowsVM";
    string publicIpDnsLabel = "samplePublicIP";

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the VM
    Console.WriteLine("Creating VM...");
    var windowsVM = azure.VirtualMachines.Define(windowsVmName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithNewPrimaryNetwork("10.0.0.0/28")
        .WithPrimaryPrivateIPAddressDynamic()
        .WithNewPrimaryPublicIPAddress(publicIpDnsLabel)
        .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
        .WithAdminUsername(username)
        .WithAdminPassword(password)
        .WithSize(VirtualMachineSizeTypes.StandardD2V2)
        .Create();

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

Premere **F5** per eseguire l'esempio.

Dopo alcuni minuti il programma verrà completato e verrà richiesto di premere INVIO. Dopo avere premuto INVIO, verificare la macchina virtuale nella sottoscrizione con PowerShell:

```powershell
Get-AzureRmVm -ResourceGroupName sampleResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>Distribuire un'app Web da un repository di GitHub

Verranno ora apportate modifiche al codice per creare e distribuire una nuova app Web da un repository esistente di GitHub. Sostituire il metodo `Main` con il codice seguente:

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string appName = SdkContext.RandomResourceName("WebApp", 20);

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the web app
    Console.WriteLine("Creating Web App...");
    var app = azure.WebApps.Define(appName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithNewFreeAppServicePlan()
        .DefineSourceControl()
        .WithPublicGitRepository("https://github.com/Azure-Samples/app-service-web-dotnet-get-started")
        .WithBranch("master")
        .Attach()
        .Create();
    Console.WriteLine("Your web app is live at: https://{0}", app.HostNames.First());

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

Eseguire il codice come indicato in precedenza premendo **F5**.  Verificare la distribuzione aprendo un browser e passando all'URL visualizzato nella console.

## <a name="connect-to-a-sql-database"></a>Connettersi al database SQL

Questo esempio crea un nuovo database SQL di Azure ed esegue alcune operazioni SQL.

Sostituire il metodo `Main` con il codice seguente, assicurandosi di assegnare una password complessa per `dbPassword`:

```csharp
 static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string adminUser = SdkContext.RandomResourceName("db", 8);
    string sqlServerName = SdkContext.RandomResourceName("sql", 10);
    string sqlDbName = SdkContext.RandomResourceName("dbname", 8);
    string dbPassword = "YOUR_PASSWORD_HERE";

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the SQL server and database
    Console.WriteLine("Creating server...");
    var sqlServer = azure.SqlServers.Define(sqlServerName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithAdministratorLogin(adminUser)
        .WithAdministratorPassword(dbPassword)
        .WithNewFirewallRule("0.0.0.0", "255.255.255.255")
        .Create();

    Console.WriteLine("Creating database...");
    var sqlDb = sqlServer.Databases.Define(sqlDbName).Create();

    // Display information for connecting later...
    Console.WriteLine("Created database {0} in server {1}.", sqlDbName, sqlServer.FullyQualifiedDomainName);
    Console.WriteLine("Your user name is {0}.", adminUser + "@" + sqlServer.Name);

    // Build the connection string
    var builder = new SqlConnectionStringBuilder();
    builder.DataSource = sqlServer.FullyQualifiedDomainName;
    builder.InitialCatalog = sqlDbName;
    builder.UserID = adminUser + "@" + sqlServer.Name; // Format user ID as "user@server"
    builder.Password = dbPassword;
    builder.Encrypt = true;
    builder.TrustServerCertificate = true;

    // connect to the database, create a table and insert an entry into it
    using (var conn = new SqlConnection(builder.ConnectionString))
    {
        conn.Open();

        Console.WriteLine("Populating database...");
        var createCommand = new SqlCommand("CREATE TABLE CLOUD (name varchar(255), code int);", conn);
        createCommand.ExecuteNonQuery();

        var insertCommand = new SqlCommand("INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);", conn);
        insertCommand.ExecuteNonQuery();

        Console.WriteLine("Reading from database...");
        var selectCommand = new SqlCommand("SELECT * FROM CLOUD", conn);
        var results = selectCommand.ExecuteReader();
        while(results.Read())
        {
            Console.WriteLine("Name: {0} Code: {1}", results[0], results[1]);
        }
    }

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

Eseguire il codice come indicato in precedenza premendo **F5**.  L'output della console dovrebbe confermare che il server è stato creato e che funziona come previsto, ma è possibile connettersi direttamente al server con uno strumento come SQL Server Management Studio, se si preferisce.

## <a name="write-a-blob-into-a-new-storage-account"></a>Scrivere un BLOB in un nuovo account di archiviazione

Questo esempio consente di creare un account di archiviazione e di caricare un BLOB.  

Sostituire il metodo `Main` con il codice seguente.

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string storageAccountName = SdkContext.RandomResourceName("st", 10);

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the storage account
    Console.WriteLine("Creating storage account...");
    var storage = azure.StorageAccounts.Define(storageAccountName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .Create();

    var storageKeys = storage.GetKeys();
    string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.Name
        + ";AccountKey=" + storageKeys[0].Value
        + ";EndpointSuffix=core.windows.net";

    var account = CloudStorageAccount.Parse(storageConnectionString);
    var serviceClient = account.CreateCloudBlobClient();

    // Create container. Name must be lower case.
    Console.WriteLine("Creating container...");
    var container = serviceClient.GetContainerReference("helloazure");
    container.CreateIfNotExistsAsync().Wait();

    // Make the container public
    var containerPermissions = new BlobContainerPermissions()
        { PublicAccess = BlobContainerPublicAccessType.Container };
    container.SetPermissionsAsync(containerPermissions).Wait();

    // write a blob to the container
    Console.WriteLine("Uploading blob...");
    var blob = container.GetBlockBlobReference("helloazure.txt");
    blob.UploadTextAsync("Hello, Azure!").Wait();
    Console.WriteLine("Your blob is located at {0}", blob.StorageUri.PrimaryUri);

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

Premere **F5** per eseguire l'esempio.

Dopo alcuni minuti il programma termina. Verificare che il BLOB sia stato caricato passando all'URL visualizzato nella console.  Dovrebbe essere visualizzato il testo "Hello, Azure!" nel browser.

## <a name="clean-up"></a>Eseguire la pulizia

> [!IMPORTANT]
> Se non si esegue la pulizia delle risorse usate in questa esercitazione, si continueranno a ricevere addebiti per tali risorse.  Assicurarsi di eseguire questo passaggio.

Eliminare tutte le risorse create immettendo il codice seguente in PowerShell:

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName sampleResourceGroup
```

## <a name="explore-more-samples"></a>Esplorare altri esempi

Per altre informazioni su come usare le librerie di Azure per .NET per la gestione delle risorse e l'automazione delle attività, vedere il codice di esempio per [macchine virtuali](dotnet-sdk-azure-virtual-machine-samples.md), [app Web](dotnet-sdk-azure-web-apps-samples.md) e [database SQL](dotnet-sdk-azure-sql-database-samples.md).

## <a name="reference"></a>riferimento

Le [informazioni di riferimento](http://docs.microsoft.com/dotnet/api) sono disponibili per tutti i pacchetti.

[!include[Contribute and community](includes/contribute.md)]
