---
title: Eseguire l'autenticazione con le librerie di Azure per .NET
description: Eseguire l'autenticazione per le librerie di Azure per .NET
keywords: Azure, .NET, SDK, API, autenticazione, active directory, entità servizio
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 783b5ebf14abad992c18726df7232e4f3a68b72b
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2018
ms.locfileid: "29752773"
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a>Eseguire l'autenticazione con le librerie di Azure per .NET

## <a name="connect-to-services-with-connection-strings"></a>Connettersi ai servizi con le stringhe di connessione

La maggior parte delle librerie di servizi di Azure richiede una stringa di connessione o chiavi per l'autenticazione. Ad esempio, il database SQL usa una stringa di connessione SQL standard:

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

Archiviazione di Azure usa una chiave di archiviazione:

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

Le stringhe di connessione dei servizi vengono usate anche in altri servizi di Azure, come [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Cache Redis](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache) e [bus di servizio](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues), ed è possibile ottenere queste stringhe usando il portale di Azure, l'interfaccia della riga di comando o PowerShell.  È anche possibile usare le librerie di gestione di Azure per .NET per eseguire query nelle risorse per creare stringhe di connessione nel codice. 

Questo frammento di codice usa le librerie di gestione per creare una stringa di connessione dell'account di archiviazione:

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

Altre librerie richiedono che l'applicazione venga eseguita con un'[entità servizio](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) che autorizza l'esecuzione dell'applicazione con le credenziali concesse. Questa configurazione è simile alla procedura di autenticazione basata su oggetti per le librerie di gestione illustrata di seguito.

## <a name="mgmt-auth"></a>Autenticazione delle librerie di gestione di Azure per .NET

[!include[Create service principal](includes/create-sp.md)]

Dopo la creazione dell'entità servizio, sono disponibili due opzioni per l'autenticazione nell'entità servizio per la creazione e la gestione delle risorse.

Per entrambe le opzioni sarà necessario aggiungere i pacchetti NuGet seguenti al progetto.

```
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a>Eseguire l'autenticazione con le credenziali del token

Il primo metodo consiste nel creare l'oggetto credenziali del token nel codice.  È necessario archiviare le credenziali in modo sicuro nel file di configurazione, nel Registro di sistema o in Azure Key Vault.

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId, 
    AzureEnvironment.AzureGlobalCloud);
```

- clientId: usare il valore *ApplicationId* dall'output dell'entità servizio.
- clientSecret: usare il parametro *-Password* assegnato durante l'esecuzione di `New-AzureRmADServicePrincipal` (senza virgolette).
- tenantId: usare il valore *TenantId* specificato durante l'esecuzione di `Login-AzureRmAccount`.

Creare quindi l'oggetto `Azure` del punto di ingresso per iniziare a usare l'API:

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <a name="mgmt-file"></a>Autenticazione basata su file

L'autenticazione basata su file consente di inserire le credenziali dell'entità servizio in un file di testo normale e di proteggerlo nel file system.

[!include[File-based authentication](includes/file-based-auth.md)]

Leggere i contenuti del file e creare l'oggetto `Azure` del punto di ingresso per iniziare a usare l'API:

```csharp
// pull in the location of the authentication properties file from the environment 
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
