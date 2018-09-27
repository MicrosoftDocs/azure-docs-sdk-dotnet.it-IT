---
title: Eseguire l'autenticazione con le librerie di Azure per .NET
description: Eseguire l'autenticazione per le librerie di Azure per .NET
ms.date: 08/22/2018
ms.openlocfilehash: d0d8db89816a887fa23490a213917a3c554ecdb4
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190860"
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a><span data-ttu-id="157d2-103">Eseguire l'autenticazione con le librerie di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="157d2-103">Authenticate with the Azure Libraries for .NET</span></span>

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="157d2-104">Connettersi ai servizi con le stringhe di connessione</span><span class="sxs-lookup"><span data-stu-id="157d2-104">Connect to services with connection strings</span></span>

<span data-ttu-id="157d2-105">La maggior parte delle librerie di servizi di Azure richiede una stringa di connessione o chiavi per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="157d2-105">Most Azure service libraries require a connection string or keys for authentication.</span></span> <span data-ttu-id="157d2-106">Ad esempio, il database SQL usa una stringa di connessione SQL standard:</span><span class="sxs-lookup"><span data-stu-id="157d2-106">For example, SQL Database uses a standard SQL connection string:</span></span>

```csharp
var builder = new SqlConnectionStringBuilder();
builder.DataSource = "example.database.windows.net";
builder.InitialCatalog = "MyDatabase";
builder.UserID = "sampleuser@example"; // Format user ID as "user@server"
builder.Password = password;
builder.Encrypt = true;
builder.TrustServerCertificate = true;
                
using (var conn = new SqlConnection(builder.ConnectionString))
{
    conn.Open();
    // Do things with the connection...
    // ...
}
```

<span data-ttu-id="157d2-107">Archiviazione di Azure usa una chiave di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="157d2-107">Azure Storage uses a storage key:</span></span>

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

<span data-ttu-id="157d2-108">Le stringhe di connessione dei servizi vengono usate anche in altri servizi di Azure, come [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Cache Redis](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache) e [bus di servizio](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues), ed è possibile ottenere queste stringhe usando il portale di Azure, l'interfaccia della riga di comando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="157d2-108">Service connection strings are used in other Azure services like [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Redis Cache](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache), and [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues) and you can get those strings using the Azure portal, CLI, or PowerShell.</span></span>  <span data-ttu-id="157d2-109">È anche possibile usare le librerie di gestione di Azure per .NET per eseguire query nelle risorse per creare stringhe di connessione nel codice.</span><span class="sxs-lookup"><span data-stu-id="157d2-109">You can also use the Azure management libraries for .NET to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="157d2-110">Questo frammento di codice usa le librerie di gestione per creare una stringa di connessione dell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="157d2-110">This snippet uses the management libraries to create a storage account connection string:</span></span>

```csharp
// Get a storage account
var storage = azure.StorageAccounts.GetByResourceGroup("myResourceGroup", "myStorageAccount");

// Extract the keys
var storageKeys = storage.GetKeys();

// Build the connection string
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.Name
        + ";AccountKey=" + storageKeys[0].Value
        + ";EndpointSuffix=core.windows.net";

// Connect
var account = CloudStorageAccount.Parse(storageConnectionString);

// Do things with the account here...
```

<span data-ttu-id="157d2-111">Altre librerie richiedono che l'applicazione venga eseguita con un'[entità servizio](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) che autorizza l'esecuzione dell'applicazione con le credenziali concesse.</span><span class="sxs-lookup"><span data-stu-id="157d2-111">Other libraries require your application to run with a [service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="157d2-112">Questa configurazione è simile alla procedura di autenticazione basata su oggetti per le librerie di gestione illustrata di seguito.</span><span class="sxs-lookup"><span data-stu-id="157d2-112">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

## <a name="mgmt-auth"></a><span data-ttu-id="157d2-113">Autenticazione delle librerie di gestione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="157d2-113">Azure management libraries for .NET authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

<span data-ttu-id="157d2-114">Dopo la creazione dell'entità servizio, sono disponibili due opzioni per l'autenticazione nell'entità servizio per la creazione e la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="157d2-114">Now that the service principal is created, two options are available to authenticate to the service principal to create and manage resources.</span></span>

<span data-ttu-id="157d2-115">Per entrambe le opzioni sarà necessario aggiungere i pacchetti NuGet seguenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="157d2-115">For both options you will need to add the following nuget packages to your project.</span></span>

```
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a><span data-ttu-id="157d2-116">Eseguire l'autenticazione con le credenziali del token</span><span class="sxs-lookup"><span data-stu-id="157d2-116">Authenticate with token credentials</span></span>

<span data-ttu-id="157d2-117">Il primo metodo consiste nel creare l'oggetto credenziali del token nel codice.</span><span class="sxs-lookup"><span data-stu-id="157d2-117">The first method is to build the token credential object in code.</span></span>  <span data-ttu-id="157d2-118">È necessario archiviare le credenziali in modo sicuro nel file di configurazione, nel Registro di sistema o in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="157d2-118">You should store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId, 
    AzureEnvironment.AzureGlobalCloud);
```

<span data-ttu-id="157d2-119">Usare i valori di *clientId*, *clientSecret* e *tenantId* dell'output JSON della creazione dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="157d2-119">Use the *clientId*, *clientSecret*, and *tenantId* values from the JSON output when you created the service principal.</span></span>

<span data-ttu-id="157d2-120">Creare quindi l'oggetto `Azure` del punto di ingresso per iniziare a usare l'API:</span><span class="sxs-lookup"><span data-stu-id="157d2-120">Then create the entry point `Azure` object to start working with the API:</span></span>

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <a name="mgmt-file"></a><span data-ttu-id="157d2-121">Autenticazione basata su file</span><span class="sxs-lookup"><span data-stu-id="157d2-121">File-based authentication</span></span>

<span data-ttu-id="157d2-122">L'autenticazione basata su file consente di inserire le credenziali dell'entità servizio in un file di testo normale e di proteggerlo nel file system.</span><span class="sxs-lookup"><span data-stu-id="157d2-122">File-based authentication allows you to put the service principal credentials in a plain text file and secure it within the file system.</span></span>

[!include[File-based authentication](includes/file-based-auth.md)]

<span data-ttu-id="157d2-123">Leggere i contenuti del file e creare l'oggetto `Azure` del punto di ingresso per iniziare a usare l'API:</span><span class="sxs-lookup"><span data-stu-id="157d2-123">Read the contents of the file and create the entry point `Azure` object to start working with the API:</span></span>

```csharp
// pull in the location of the authentication properties file from the environment 
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
