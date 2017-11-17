---
title: Eseguire l'autenticazione con le librerie di Azure per .NET
description: Eseguire l'autenticazione per le librerie di Azure per .NET
keywords: "Azure, .NET, SDK, API, autenticazione, active directory, entità servizio"
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
ms.openlocfilehash: c9755d7e9c20186c7677b4bfe69d4033f9852607
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2017
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a><span data-ttu-id="8c70d-104">Eseguire l'autenticazione con le librerie di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="8c70d-104">Authenticate with the Azure Libraries for .NET</span></span>

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="8c70d-105">Connettersi ai servizi con le stringhe di connessione</span><span class="sxs-lookup"><span data-stu-id="8c70d-105">Connect to services with connection strings</span></span>

<span data-ttu-id="8c70d-106">La maggior parte delle librerie di servizi di Azure richiede una stringa di connessione o chiavi per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="8c70d-106">Most Azure service libraries require a connection string or keys for authentication.</span></span> <span data-ttu-id="8c70d-107">Ad esempio, il database SQL usa una stringa di connessione SQL standard:</span><span class="sxs-lookup"><span data-stu-id="8c70d-107">For example, SQL Database uses a standard SQL connection string:</span></span>

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

<span data-ttu-id="8c70d-108">Archiviazione di Azure usa una chiave di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="8c70d-108">Azure Storage uses a storage key:</span></span>

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

<span data-ttu-id="8c70d-109">Le stringhe di connessione dei servizi vengono usate anche in altri servizi di Azure, come [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Cache Redis](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache) e [bus di servizio](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues), ed è possibile ottenere queste stringhe usando il portale di Azure, l'interfaccia della riga di comando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c70d-109">Service connection strings are used in other Azure services like [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Redis Cache](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache), and [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues) and you can get those strings using the Azure portal, CLI, or PowerShell.</span></span>  <span data-ttu-id="8c70d-110">È anche possibile usare le librerie di gestione di Azure per .NET per eseguire query nelle risorse per creare stringhe di connessione nel codice.</span><span class="sxs-lookup"><span data-stu-id="8c70d-110">You can also use the Azure management libraries for .NET to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="8c70d-111">Questo frammento di codice usa le librerie di gestione per creare una stringa di connessione dell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="8c70d-111">This snippet uses the management libraries to create a storage account connection string:</span></span>

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

<span data-ttu-id="8c70d-112">Altre librerie richiedono che l'applicazione venga eseguita con un'[entità servizio](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) che autorizza l'esecuzione dell'applicazione con le credenziali concesse.</span><span class="sxs-lookup"><span data-stu-id="8c70d-112">Other libraries require your application to run with a [service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="8c70d-113">Questa configurazione è simile alla procedura di autenticazione basata su oggetti per le librerie di gestione illustrata di seguito.</span><span class="sxs-lookup"><span data-stu-id="8c70d-113">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

## <span data-ttu-id="8c70d-114"><a name="mgmt-auth"></a>Autenticazione delle librerie di gestione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="8c70d-114"><a name="mgmt-auth"></a>Azure management libraries for .NET authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

<span data-ttu-id="8c70d-115">Dopo la creazione dell'entità servizio, sono disponibili due opzioni per l'autenticazione nell'entità servizio per la creazione e la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="8c70d-115">Now that the service principal is created, two options are available to authenticate to the service principal to create and manage resources.</span></span>

<span data-ttu-id="8c70d-116">Per entrambe le opzioni sarà necessario aggiungere i pacchetti NuGet seguenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="8c70d-116">For both options you will need to add the following nuget packages to your project.</span></span>

```
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a><span data-ttu-id="8c70d-117">Eseguire l'autenticazione con le credenziali del token</span><span class="sxs-lookup"><span data-stu-id="8c70d-117">Authenticate with token credentials</span></span>

<span data-ttu-id="8c70d-118">Il primo metodo consiste nel creare l'oggetto credenziali del token nel codice.</span><span class="sxs-lookup"><span data-stu-id="8c70d-118">The first method is to build the token credential object in code.</span></span>  <span data-ttu-id="8c70d-119">È necessario archiviare le credenziali in modo sicuro nel file di configurazione, nel Registro di sistema o in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8c70d-119">You should store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId, 
    AzureEnvironment.AzureGlobalCloud);
```

- <span data-ttu-id="8c70d-120">clientId: usare il valore *ApplicationId* dall'output dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="8c70d-120">clientId: use the *ApplicationId* value from the service principal output.</span></span>
- <span data-ttu-id="8c70d-121">clientSecret: usare il parametro *-Password* assegnato durante l'esecuzione di `New-AzureRmADServicePrincipal` (senza virgolette).</span><span class="sxs-lookup"><span data-stu-id="8c70d-121">clientSecret: use the *-Password* parameter you assigned when you ran `New-AzureRmADServicePrincipal` (without quotes).</span></span>
- <span data-ttu-id="8c70d-122">tenantId: usare il valore *TenantId* specificato durante l'esecuzione di `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="8c70d-122">tenantId: use the *TenantId* value from when you ran `Login-AzureRmAccount`.</span></span>

<span data-ttu-id="8c70d-123">Creare quindi l'oggetto `Azure` del punto di ingresso per iniziare a usare l'API:</span><span class="sxs-lookup"><span data-stu-id="8c70d-123">Then create the entry point `Azure` object to start working with the API:</span></span>

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <span data-ttu-id="8c70d-124"><a name="mgmt-file"></a>Autenticazione basata su file</span><span class="sxs-lookup"><span data-stu-id="8c70d-124"><a name="mgmt-file"></a>File-based authentication</span></span>

<span data-ttu-id="8c70d-125">L'autenticazione basata su file consente di inserire le credenziali dell'entità servizio in un file di testo normale e di proteggerlo nel file system.</span><span class="sxs-lookup"><span data-stu-id="8c70d-125">File-based authentication allows you to put the service principal credentials in a plain text file and secure it within the file system.</span></span>

[!include[File-based authentication](includes/file-based-auth.md)]

<span data-ttu-id="8c70d-126">Leggere i contenuti del file e creare l'oggetto `Azure` del punto di ingresso per iniziare a usare l'API:</span><span class="sxs-lookup"><span data-stu-id="8c70d-126">Read the contents of the file and create the entry point `Azure` object to start working with the API:</span></span>

```csharp
// pull in the location of the authentication properties file from the environment 
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
