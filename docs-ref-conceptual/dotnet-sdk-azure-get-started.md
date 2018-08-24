---
title: Introduzione alle API di Azure .NET e .NET Core
description: Introduzione all'uso di base delle librerie di Azure per .NET e .NET Core con la propria sottoscrizione di Azure.
keywords: Azure, .NET, .NET Core, ASP.NET, ASP.NET Core SDK, API, autenticazione, introduzione
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 08/22/2018
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: ad894e47704fcccc83f7d02acb8e418b167993f9
ms.sourcegitcommit: b2a53a3aea9de6720bd975fb7fe4e722e9d182a3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703054"
---
# <a name="get-started-with-the-azure-net-and-net-core-apis"></a><span data-ttu-id="478a2-104">Introduzione alle API di Azure .NET e .NET Core</span><span class="sxs-lookup"><span data-stu-id="478a2-104">Get started with the Azure .NET and .NET Core APIs</span></span>

<span data-ttu-id="478a2-105">Questa esercitazione illustra l'utilizzo di alcune [API di Azure per .NET](/dotnet/api/overview/azure/).</span><span class="sxs-lookup"><span data-stu-id="478a2-105">This tutorial demonstrates the usage of several [Azure APIs for .NET](/dotnet/api/overview/azure/).</span></span>  <span data-ttu-id="478a2-106">Verranno eseguite operazioni per la configurazione dell'autenticazione, la creazione e l'uso di un account di archiviazione di Azure, la creazione e l'uso di un database SQL di Azure, la distribuzione di alcune macchine virtuali e la distribuzione di un'app Web del Servizio app di Azure da GitHub.</span><span class="sxs-lookup"><span data-stu-id="478a2-106">You will set up authentication, create and use an Azure Storage account, create and use an Azure SQL Database, deploy some virtual machines, and deploy an Azure App Service Web App from GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="478a2-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="478a2-107">Prerequisites</span></span>

- <span data-ttu-id="478a2-108">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="478a2-108">An Azure account.</span></span> <span data-ttu-id="478a2-109">Se non è disponibile, [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="478a2-109">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="478a2-110">Configurare l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="478a2-110">Set up authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="create-a-new-project"></a><span data-ttu-id="478a2-111">Creare un nuovo progetto</span><span class="sxs-lookup"><span data-stu-id="478a2-111">Create a new project</span></span> 

<span data-ttu-id="478a2-112">Creare un nuovo progetto di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="478a2-112">Create a new console application project.</span></span>  <span data-ttu-id="478a2-113">In Visual Studio eseguire questa operazione facendo clic su **File**, **Nuovo** e quindi su **Progetto**.  Nei modelli di Visual C# selezionare **App console (.NET Core)**, assegnare un nome al progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="478a2-113">In Visual Studio, do this by clicking **File**, **New**, and then clicking **Project...**.  Under the Visual C# templates, select **Console App (.NET Core)**, name your project, and then click **OK**.</span></span>

![Finestra di dialogo Nuovo progetto](media/dotnet-sdk-azure-get-started/new-project.png)

<span data-ttu-id="478a2-115">Dopo la creazione della nuova app console, aprire la console di Gestione pacchetti facendo clic su **Strumenti**, **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="478a2-115">When the new console app is created, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>  <span data-ttu-id="478a2-116">Nella console ottenere i pacchetti necessari eseguendo i tre comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="478a2-116">In the console, get the packages you'll need by executing the following three commands:</span></span>

```powershell
# Azure Management Libraries for .NET (Fluent)
Install-Package Microsoft.Azure.Management.Fluent

# Azure Store client libraries
Install-Package WindowsAzure.Storage

# SQL Database client libraries
Install-Package System.Data.SqlClient
```

## <a name="directives"></a><span data-ttu-id="478a2-117">Direttive</span><span class="sxs-lookup"><span data-stu-id="478a2-117">Directives</span></span>

<span data-ttu-id="478a2-118">Modificare il file `Program.cs` dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="478a2-118">Edit your application's `Program.cs` file.</span></span>  <span data-ttu-id="478a2-119">Sostituire le direttive `using` all'inizio del file con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="478a2-119">Replace the `using` directives at the top with the following:</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="478a2-120">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="478a2-120">Create a virtual machine</span></span>

<span data-ttu-id="478a2-121">Questo esempio distribuisce una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="478a2-121">This example deploys a virtual machine.</span></span> 

<span data-ttu-id="478a2-122">Sostituire il metodo `Main` con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="478a2-122">Replace the `Main` method with the following.</span></span>  <span data-ttu-id="478a2-123">Assicurarsi di specificare valori effettivi per `username` e `password` per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="478a2-123">Be sure to provide an actual `username` and `password` for the virtual machine.</span></span>

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string username = "MY_USERNAME";
    string password = "MY_PASSWORD";
    string rgName = "sampleResourceGroup";
    string windowsVmName = "sampleWindowsVM";
    string publicIpDnsLabel = "samplePublicIP" + (new Random().Next(0,100000)).ToString();

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

<span data-ttu-id="478a2-124">Premere **F5** per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="478a2-124">Press **F5** to run the sample.</span></span>

<span data-ttu-id="478a2-125">Dopo alcuni minuti il programma verrà completato e verrà richiesto di premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="478a2-125">After several minutes, the program will finish, prompting you to press enter.</span></span> <span data-ttu-id="478a2-126">Dopo avere premuto INVIO, verificare la macchina virtuale nella sottoscrizione con Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="478a2-126">After pressing enter, verify the virtual machine in your subscription with the Cloud Shell:</span></span>

```azurecli-interactive
az vm list
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="478a2-127">Distribuire un'app Web da un repository di GitHub</span><span class="sxs-lookup"><span data-stu-id="478a2-127">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="478a2-128">Verranno ora apportate modifiche al codice per creare e distribuire una nuova app Web da un repository esistente di GitHub.</span><span class="sxs-lookup"><span data-stu-id="478a2-128">Now you'll modify your code to create a deploy a new web app from an existing GitHub repository.</span></span> <span data-ttu-id="478a2-129">Sostituire il metodo `Main` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="478a2-129">Replace the `Main` method with the following code:</span></span>

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

<span data-ttu-id="478a2-130">Eseguire il codice come indicato in precedenza premendo **F5**.</span><span class="sxs-lookup"><span data-stu-id="478a2-130">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="478a2-131">Verificare la distribuzione aprendo un browser e passando all'URL visualizzato nella console.</span><span class="sxs-lookup"><span data-stu-id="478a2-131">Verify the deployment by opening a browser and navigating to URL displayed in the console.</span></span>

## <a name="connect-to-a-sql-database"></a><span data-ttu-id="478a2-132">Connettersi al database SQL</span><span class="sxs-lookup"><span data-stu-id="478a2-132">Connect to a SQL database</span></span>

<span data-ttu-id="478a2-133">Questo esempio crea un nuovo database SQL di Azure ed esegue alcune operazioni SQL.</span><span class="sxs-lookup"><span data-stu-id="478a2-133">This example creates a new Azure SQL Database and performs a few SQL operations.</span></span>

<span data-ttu-id="478a2-134">Sostituire il metodo `Main` con il codice seguente, assicurandosi di assegnare una password complessa per `dbPassword`:</span><span class="sxs-lookup"><span data-stu-id="478a2-134">Replace the `Main` method with the following, making sure to assign a strong password for `dbPassword`:</span></span>

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

<span data-ttu-id="478a2-135">Eseguire il codice come indicato in precedenza premendo **F5**.</span><span class="sxs-lookup"><span data-stu-id="478a2-135">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="478a2-136">L'output della console dovrebbe confermare che il server è stato creato e che funziona come previsto, ma è possibile connettersi direttamente al server con uno strumento come SQL Server Management Studio, se si preferisce.</span><span class="sxs-lookup"><span data-stu-id="478a2-136">The console output should validate that the server was created and works as expected, but you can connect to it directly with a tool like SQL Server Management Studio if you like.</span></span>

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="478a2-137">Scrivere un BLOB in un nuovo account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="478a2-137">Write a blob into a new storage account</span></span>

<span data-ttu-id="478a2-138">Questo esempio consente di creare un account di archiviazione e di caricare un BLOB.</span><span class="sxs-lookup"><span data-stu-id="478a2-138">This example creates a storage account and upload a blob.</span></span>  

<span data-ttu-id="478a2-139">Sostituire il metodo `Main` con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="478a2-139">Replace the `Main` method with the following.</span></span>

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

<span data-ttu-id="478a2-140">Premere **F5** per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="478a2-140">Press **F5** to run the sample.</span></span>

<span data-ttu-id="478a2-141">Dopo alcuni minuti il programma termina.</span><span class="sxs-lookup"><span data-stu-id="478a2-141">After several minutes, the program finishes.</span></span> <span data-ttu-id="478a2-142">Verificare che il BLOB sia stato caricato passando all'URL visualizzato nella console.</span><span class="sxs-lookup"><span data-stu-id="478a2-142">Verify the blob was uploaded by browsing to the URL displayed in the console.</span></span>  <span data-ttu-id="478a2-143">Dovrebbe essere visualizzato il testo "Hello, Azure!"</span><span class="sxs-lookup"><span data-stu-id="478a2-143">You should see the text "Hello, Azure!"</span></span> <span data-ttu-id="478a2-144">nel browser.</span><span class="sxs-lookup"><span data-stu-id="478a2-144">in your browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="478a2-145">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="478a2-145">Clean up</span></span>

> [!IMPORTANT]
> <span data-ttu-id="478a2-146">Se non si esegue la pulizia delle risorse usate in questa esercitazione, si continueranno a ricevere addebiti per tali risorse.</span><span class="sxs-lookup"><span data-stu-id="478a2-146">If you don't clean up your resources from this tutorial, you will continue to be charged for them.</span></span>  <span data-ttu-id="478a2-147">Assicurarsi di eseguire questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="478a2-147">Be sure to do this step.</span></span>

<span data-ttu-id="478a2-148">Eliminare tutte le risorse create immettendo il comando seguente in Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="478a2-148">Delete all the resources you created by entering the following in the Cloud Shell:</span></span>

```azurecli-interactive
az group delete --name sampleResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="478a2-149">Esplorare altri esempi</span><span class="sxs-lookup"><span data-stu-id="478a2-149">Explore more samples</span></span>

<span data-ttu-id="478a2-150">Per altre informazioni su come usare le librerie di Azure per .NET per la gestione delle risorse e l'automazione delle attività, vedere il codice di esempio per [macchine virtuali](dotnet-sdk-azure-virtual-machine-samples.md), [app Web](dotnet-sdk-azure-web-apps-samples.md) e [database SQL](dotnet-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="478a2-150">To learn more about how to use the Azure libraries for .NET to manage resources and automate tasks, see our sample code for [virtual machines](dotnet-sdk-azure-virtual-machine-samples.md), [web apps](dotnet-sdk-azure-web-apps-samples.md) and [SQL database](dotnet-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference"></a><span data-ttu-id="478a2-151">riferimento</span><span class="sxs-lookup"><span data-stu-id="478a2-151">Reference</span></span>

<span data-ttu-id="478a2-152">Le [informazioni di riferimento](http://docs.microsoft.com/dotnet/api) sono disponibili per tutti i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="478a2-152">A [reference](http://docs.microsoft.com/dotnet/api) is available for all packages.</span></span>

[!include[Contribute and community](includes/contribute.md)]
