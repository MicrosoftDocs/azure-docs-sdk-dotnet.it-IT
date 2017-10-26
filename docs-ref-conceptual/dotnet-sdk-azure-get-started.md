---
title: Introduzione alle API .NET di Azure
description: Introduzione all'uso di base delle librerie di Azure per .NET con la propria sottoscrizione di Azure.
keywords: Azure, .NET, SDK, API, autenticare, introduzione
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 80f796493362a84474f5913a26ad6802f68a4906
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2017
---
# <a name="get-started-with-the-azure-net-apis"></a><span data-ttu-id="2f96e-104">Introduzione alle API .NET di Azure</span><span class="sxs-lookup"><span data-stu-id="2f96e-104">Get started with the Azure .NET APIs</span></span>

<span data-ttu-id="2f96e-105">Questa esercitazione illustra l'utilizzo di alcune [API di Azure per .NET](/dotnet/api/overview/azure/).</span><span class="sxs-lookup"><span data-stu-id="2f96e-105">This tutorial demonstrates the usage of several [Azure APIs for .NET](/dotnet/api/overview/azure/).</span></span>  <span data-ttu-id="2f96e-106">Verranno eseguite operazioni per la configurazione dell'autenticazione, la creazione e l'uso di un account di archiviazione di Azure, la creazione e l'uso di un database SQL di Azure, la distribuzione di alcune macchine virtuali e la distribuzione di un'app Web del Servizio app di Azure da GitHub.</span><span class="sxs-lookup"><span data-stu-id="2f96e-106">You will set up authentication, create and use an Azure Storage account, create and use an Azure SQL Database, deploy some virtual machines, and deploy an Azure App Service Web App from GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f96e-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2f96e-107">Prerequisites</span></span>

- <span data-ttu-id="2f96e-108">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="2f96e-108">An Azure account.</span></span> <span data-ttu-id="2f96e-109">Se non è disponibile, [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="2f96e-109">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- [<span data-ttu-id="2f96e-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f96e-110">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

## <a name="set-up-authentication"></a><span data-ttu-id="2f96e-111">Configurare l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="2f96e-111">Set up authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="create-a-new-project"></a><span data-ttu-id="2f96e-112">Creare un nuovo progetto</span><span class="sxs-lookup"><span data-stu-id="2f96e-112">Create a new project</span></span> 

<span data-ttu-id="2f96e-113">Creare un nuovo progetto di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="2f96e-113">Create a new console application project.</span></span>  <span data-ttu-id="2f96e-114">In Visual Studio eseguire questa operazione facendo clic su **File**, **Nuovo** e quindi su **Progetto**.  Nei modelli di Visual C# selezionare **App console (.NET Core)**, assegnare un nome al progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f96e-114">In Visual Studio, do this by clicking **File**, **New**, and then clicking **Project...**.  Under the Visual C# templates, select **Console App (.NET Core)**, name your project, and then click **OK**.</span></span>

![Finestra di dialogo Nuovo progetto](media/dotnet-sdk-azure-get-started/new-project.png)

<span data-ttu-id="2f96e-116">Dopo la creazione della nuova app console, aprire la console di Gestione pacchetti facendo clic su **Strumenti**, **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="2f96e-116">When the new console app is created, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>  <span data-ttu-id="2f96e-117">Nella console ottenere i pacchetti necessari eseguendo i tre comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f96e-117">In the console, get the packages you'll need by executing the following three commands:</span></span>

```powershell
# Azure Management Libraries for .NET (Fluent)
Install-Package Microsoft.Azure.Management.Fluent

# Azure Store client libraries
Install-Package WindowsAzure.Storage

# SQL Database client libraries
Install-Package System.Data.SqlClient
```

## <a name="directives"></a><span data-ttu-id="2f96e-118">Direttive</span><span class="sxs-lookup"><span data-stu-id="2f96e-118">Directives</span></span>

<span data-ttu-id="2f96e-119">Modificare il file `Program.cs` dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f96e-119">Edit your application's `Program.cs` file.</span></span>  <span data-ttu-id="2f96e-120">Sostituire le direttive `using` all'inizio del file con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2f96e-120">Replace the `using` directives at the top with the following:</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="2f96e-121">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2f96e-121">Create a virtual machine</span></span>

<span data-ttu-id="2f96e-122">Questo esempio distribuisce una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2f96e-122">This example deploys a virtual machine.</span></span> 

<span data-ttu-id="2f96e-123">Sostituire il metodo `Main` con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="2f96e-123">Replace the `Main` method with the following.</span></span>  <span data-ttu-id="2f96e-124">Assicurarsi di specificare valori effettivi per `username` e `password` per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2f96e-124">Be sure to provide an actual `username` and `password` for the virtual machine.</span></span>

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

<span data-ttu-id="2f96e-125">Premere **F5** per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="2f96e-125">Press **F5** to run the sample.</span></span>

<span data-ttu-id="2f96e-126">Dopo alcuni minuti il programma verrà completato e verrà richiesto di premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="2f96e-126">After several minutes, the program will finish, prompting you to press enter.</span></span> <span data-ttu-id="2f96e-127">Dopo avere premuto INVIO, verificare la macchina virtuale nella sottoscrizione con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2f96e-127">After pressing enter, verify the virtual machine in your subscription with PowerShell:</span></span>

```powershell
Get-AzureRmVm -ResourceGroupName sampleResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="2f96e-128">Distribuire un'app Web da un repository di GitHub</span><span class="sxs-lookup"><span data-stu-id="2f96e-128">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="2f96e-129">Verranno ora apportate modifiche al codice per creare e distribuire una nuova app Web da un repository esistente di GitHub.</span><span class="sxs-lookup"><span data-stu-id="2f96e-129">Now you'll modify your code to create a deploy a new web app from an existing GitHub repository.</span></span> <span data-ttu-id="2f96e-130">Sostituire il metodo `Main` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2f96e-130">Replace the `Main` method with the following code:</span></span>

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

<span data-ttu-id="2f96e-131">Eseguire il codice come indicato in precedenza premendo **F5**.</span><span class="sxs-lookup"><span data-stu-id="2f96e-131">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="2f96e-132">Verificare la distribuzione aprendo un browser e passando all'URL visualizzato nella console.</span><span class="sxs-lookup"><span data-stu-id="2f96e-132">Verify the deployment by opening a browser and navigating to URL displayed in the console.</span></span>

## <a name="connect-to-a-sql-database"></a><span data-ttu-id="2f96e-133">Connettersi al database SQL</span><span class="sxs-lookup"><span data-stu-id="2f96e-133">Connect to a SQL database</span></span>

<span data-ttu-id="2f96e-134">Questo esempio crea un nuovo database SQL di Azure ed esegue alcune operazioni SQL.</span><span class="sxs-lookup"><span data-stu-id="2f96e-134">This example creates a new Azure SQL Database and performs a few SQL operations.</span></span>

<span data-ttu-id="2f96e-135">Sostituire il metodo `Main` con il codice seguente, assicurandosi di assegnare una password complessa per `dbPassword`:</span><span class="sxs-lookup"><span data-stu-id="2f96e-135">Replace the `Main` method with the following, making sure to assign a strong password for `dbPassword`:</span></span>

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
<span data-ttu-id="2f96e-136">Eseguire il codice come indicato in precedenza premendo **F5**.</span><span class="sxs-lookup"><span data-stu-id="2f96e-136">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="2f96e-137">L'output della console dovrebbe confermare che il server è stato creato e che funziona come previsto, ma è possibile connettersi direttamente al server con uno strumento come SQL Server Management Studio, se si preferisce.</span><span class="sxs-lookup"><span data-stu-id="2f96e-137">The console output should validate that the server was created and works as expected, but you can connect to it directly with a tool like SQL Server Management Studio if you like.</span></span>

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="2f96e-138">Scrivere un BLOB in un nuovo account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="2f96e-138">Write a blob into a new storage account</span></span>

<span data-ttu-id="2f96e-139">Questo esempio consentirà di creare un account di archiviazione e di caricare un BLOB.</span><span class="sxs-lookup"><span data-stu-id="2f96e-139">This example will create a storage account and upload a blob.</span></span>  

<span data-ttu-id="2f96e-140">Sostituire il metodo `Main` con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="2f96e-140">Replace the `Main` method with the following.</span></span>

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

<span data-ttu-id="2f96e-141">Premere **F5** per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="2f96e-141">Press **F5** to run the sample.</span></span>

<span data-ttu-id="2f96e-142">Dopo alcuni minuti il programma verrà completato.</span><span class="sxs-lookup"><span data-stu-id="2f96e-142">After several minutes, the program will finish.</span></span> <span data-ttu-id="2f96e-143">Verificare che il BLOB sia stato caricato passando all'URL visualizzato nella console.</span><span class="sxs-lookup"><span data-stu-id="2f96e-143">Verify the blob was uploaded by browsing to the URL displayed in the console.</span></span>  <span data-ttu-id="2f96e-144">Dovrebbe essere visualizzato il testo "Hello, Azure!"</span><span class="sxs-lookup"><span data-stu-id="2f96e-144">You should see the text "Hello, Azure!"</span></span> <span data-ttu-id="2f96e-145">nel browser.</span><span class="sxs-lookup"><span data-stu-id="2f96e-145">in your browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="2f96e-146">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="2f96e-146">Clean up</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f96e-147">Se non si esegue la pulizia delle risorse usate in questa esercitazione, si continueranno a ricevere addebiti per tali risorse.</span><span class="sxs-lookup"><span data-stu-id="2f96e-147">If you don't clean up your resources from this tutorial, you will continue to be charged for them.</span></span>  <span data-ttu-id="2f96e-148">Assicurarsi di eseguire questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="2f96e-148">Be sure to do this step.</span></span>

<span data-ttu-id="2f96e-149">Eliminare tutte le risorse create immettendo il codice seguente in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2f96e-149">Delete all the resources you created by entering the following in PowerShell:</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName sampleResourceGroup
```
## <a name="explore-more-samples"></a><span data-ttu-id="2f96e-150">Esplorare altri esempi</span><span class="sxs-lookup"><span data-stu-id="2f96e-150">Explore more samples</span></span>

<span data-ttu-id="2f96e-151">Per altre informazioni su come usare le librerie di Azure per .NET per la gestione delle risorse e l'automazione delle attività, vedere il codice di esempio per [macchine virtuali](dotnet-sdk-azure-virtual-machine-samples.md), [app Web](dotnet-sdk-azure-web-apps-samples.md) e [database SQL](dotnet-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2f96e-151">To learn more about how to use the Azure libraries for .NET to manage resources and automate tasks, see our sample code for [virtual machines](dotnet-sdk-azure-virtual-machine-samples.md), [web apps](dotnet-sdk-azure-web-apps-samples.md) and [SQL database](dotnet-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference"></a><span data-ttu-id="2f96e-152">riferimento</span><span class="sxs-lookup"><span data-stu-id="2f96e-152">Reference</span></span>

<span data-ttu-id="2f96e-153">Le [informazioni di riferimento](http://docs.microsoft.com/dotnet/api) sono disponibili per tutti i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2f96e-153">A [reference](http://docs.microsoft.com/dotnet/api) is available for all packages.</span></span>

[!include[Contribute and community](includes/contribute.md)]
