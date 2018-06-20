---
title: Librerie di Azure Batch per .NET
description: Informazioni di riferimento sulle librerie di Azure Batch per .NET
keywords: Azure, .NET, SDK, API, Batch
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: batch
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 79ca70e5d0f3d5555c8a691da6dbcc1e6a55ab0b
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487264"
---
# <a name="azure-batch-libraries-for-net"></a>Librerie di Azure Batch per .NET

Azure Batch è un servizio di piattaforma per eseguire in modo efficiente applicazioni parallele e HPC (High Performance Computing) su larga scala nel cloud. Azure Batch pianifica l'esecuzione del lavoro a elevato utilizzo di calcolo su una raccolta gestita di macchine virtuali e può ridimensionare automaticamente le risorse di calcolo in base alle esigenze dei processi.

Con Azure Batch, è possibile definire facilmente le risorse di calcolo di Azure per eseguire le applicazioni in parallelo e su larga scala. Non è necessario creare, configurare e gestire manualmente un cluster HPC, singole macchine virtuali, reti virtuali o un'infrastruttura complessa di pianificazione di processi e attività. Azure Batch automatizza o semplifica queste attività.

Sono disponibili altre informazioni su come [Eseguire carichi di lavoro intrinsecamente paralleli con Batch](/azure/batch/batch-technical-overview), informazioni su come [Iniziare a creare soluzioni con la libreria di client Batch per .NET](/azure/batch/batch-dotnet-get-started) e informazioni su come [Gestire le quote e gli account Batch con la libreria di gestione Batch per .NET](/azure/batch/batch-management-dotnet).

## <a name="client-library"></a>Libreria client

Usare la libreria client per eseguire carichi di lavoro paralleli con Batch.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Azure.Batch) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Azure.Batch
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Azure.Batch
```

### <a name="example"></a>Esempio

L'esempio seguente usa l'SDK client per creare un processo per l'esecuzione in Azure Batch.

```csharp
/*
using Microsoft.Azure.Batch.Auth;
using Microsoft.Azure.Batch;
*/
BatchSharedKeyCredentials credentials = new BatchSharedKeyCredentials(batchUrl, accountName, accountKey);
using (BatchClient batchClient = await BatchClient.OpenAsync(credentials))
{
    //set up pool specification and information along with resource files here
    JobManagerTask jobManagerTask = new JobManagerTask()
    {
        ResourceFiles = jobManagerResourceFiles,
        CommandLine = Constants.JobManagerExecutable,

        //Determines if the job should terminate when the job manager process exits.
        KillJobOnCompletion = true,
        Id = jobManagerTaskId
    };

    string jobId = Environment.GetEnvironmentVariable("USERNAME") + DateTime.UtcNow.ToString("yyyyMMdd-HHmmss");

    CloudJob unboundJob = batchClient.JobOperations.CreateJob(jobId, poolInformation);
    unboundJob.JobManagerTask = jobManagerTask;

    // now interact with the job ...
}
```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/batch/client)

## <a name="management-library"></a>Libreria di gestione

Usare la libreria di gestione per gestire account, quote e pacchetti dell'applicazione di Batch a livello di codice.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.Batch
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Batch
```

### <a name="example"></a>Esempio

L'esempio seguente recupera la quota per la sottoscrizione, crea un account e rigenera la chiave dell'account primario.

```csharp
/*
using Microsoft.Azure.Management.Batch;
using Microsoft.Azure.Management.Batch.Models;
using Microsoft.Rest;
*/
using (BatchManagementClient batchManagementClient = new BatchManagementClient(new TokenCredentials(accessToken)))
{
    batchManagementClient.SubscriptionId = subscriptionId;

    // Get the account quota for the subscription
    BatchLocationQuota quotaResponse = await batchManagementClient.Location.GetQuotasAsync(location);
    Console.WriteLine("Your subscription can create {0} account(s) in the {1} region.", quotaResponse.AccountQuota, location);

    // Create account
    await batchManagementClient.BatchAccount.CreateAsync(ResourceGroupName, accountName, 
        new BatchAccountCreateParameters() { Location = location });

    // Regenerate primary account key
    BatchAccountKeys newKeys = await batchManagementClient.BatchAccount.RegenerateKeyAsync(
        ResourceGroupName, account.Name, AccountKeyType.Primary);
}
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/batch/management)

## <a name="samples"></a>Esempi

* [Azure Batch Client and Management SDK for .NET Samples](https://github.com/Azure/azure-batch-samples/tree/master/CSharp) (Esempi del client di Azure Batch e di Management SDK per .NET)

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
