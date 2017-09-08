---
title: Librerie di Azure Batch per .NET
description: Informazioni di riferimento sulle librerie di Azure Batch per .NET
keywords: Azure, .NET, SDK, API, Batch
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/01/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 753721d430de0577c0bc1dd3774d728783a3bfee
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-batch-libraries-for-net"></a><span data-ttu-id="3a737-104">Librerie di Azure Batch per .NET</span><span class="sxs-lookup"><span data-stu-id="3a737-104">Azure Batch libraries for .NET</span></span>

<span data-ttu-id="3a737-105">Azure Batch è un servizio di piattaforma per eseguire in modo efficiente applicazioni parallele e HPC (High Performance Computing) su larga scala nel cloud.</span><span class="sxs-lookup"><span data-stu-id="3a737-105">Azure Batch is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="3a737-106">Azure Batch pianifica l'esecuzione del lavoro a elevato utilizzo di calcolo su una raccolta gestita di macchine virtuali e può ridimensionare automaticamente le risorse di calcolo in base alle esigenze dei processi.</span><span class="sxs-lookup"><span data-stu-id="3a737-106">Azure Batch schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="3a737-107">Con Azure Batch, è possibile definire facilmente le risorse di calcolo di Azure per eseguire le applicazioni in parallelo e su larga scala.</span><span class="sxs-lookup"><span data-stu-id="3a737-107">With Azure Batch, you can easily define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="3a737-108">Non è necessario creare, configurare e gestire manualmente un cluster HPC, singole macchine virtuali, reti virtuali o un'infrastruttura complessa di pianificazione di processi e attività.</span><span class="sxs-lookup"><span data-stu-id="3a737-108">There's no need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span> <span data-ttu-id="3a737-109">Azure Batch automatizza o semplifica queste attività.</span><span class="sxs-lookup"><span data-stu-id="3a737-109">Azure Batch automates or simplifies these tasks for you.</span></span>

<span data-ttu-id="3a737-110">Sono disponibili altre informazioni su come [Eseguire carichi di lavoro intrinsecamente paralleli con Batch](/azure/batch/batch-technical-overview),</span><span class="sxs-lookup"><span data-stu-id="3a737-110">Read more about how to [run intrinsically parallel workloads with Batch](/azure/batch/batch-technical-overview).</span></span> <span data-ttu-id="3a737-111">informazioni su come [Iniziare a creare soluzioni con la libreria di client Batch per .NET](/azure/batch/batch-dotnet-get-started) e</span><span class="sxs-lookup"><span data-stu-id="3a737-111">You can also learn how to [get started building solutions with the Batch client library for .NET](/azure/batch/batch-dotnet-get-started).</span></span> <span data-ttu-id="3a737-112">informazioni su come [Gestire le quote e gli account Batch con la libreria di gestione Batch per .NET](/azure/batch/batch-management-dotnet).</span><span class="sxs-lookup"><span data-stu-id="3a737-112">Discover how to [manage Batch accounts and quotas with the Batch Management library for .NET](/azure/batch/batch-management-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="3a737-113">Libreria client</span><span class="sxs-lookup"><span data-stu-id="3a737-113">Client library</span></span>

<span data-ttu-id="3a737-114">Usare la libreria client per eseguire carichi di lavoro paralleli con Batch.</span><span class="sxs-lookup"><span data-stu-id="3a737-114">Use the client library to run parallel workloads with Batch.</span></span>

<span data-ttu-id="3a737-115">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Azure.Batch) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="3a737-115">Install the [NuGet package](https://www.nuget.org/packages/Azure.Batch) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3a737-116">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="3a737-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Azure.Batch
```

#### <a name="net-core-cli"></a><span data-ttu-id="3a737-117">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="3a737-117">.NET Core CLI</span></span>

```bash
dotnet add package Azure.Batch
```

### <a name="example"></a><span data-ttu-id="3a737-118">Esempio</span><span class="sxs-lookup"><span data-stu-id="3a737-118">Example</span></span>

<span data-ttu-id="3a737-119">L'esempio seguente usa l'SDK client per creare un processo per l'esecuzione in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="3a737-119">The following example uses the client SDK to create a job to run in Azure Batch.</span></span>

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
> [<span data-ttu-id="3a737-120">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="3a737-120">Explore the client APIs</span></span>](/dotnet/api/overview/azure/batch/client)

## <a name="management-library"></a><span data-ttu-id="3a737-121">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="3a737-121">Management library</span></span>

<span data-ttu-id="3a737-122">Usare la libreria di gestione per gestire account, quote e pacchetti dell'applicazione di Batch a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="3a737-122">Use the management library to programmatically manage Batch accounts, quotas, and application packages.</span></span>

<span data-ttu-id="3a737-123">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="3a737-123">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3a737-124">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="3a737-124">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Batch
```

#### <a name="net-core-cli"></a><span data-ttu-id="3a737-125">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="3a737-125">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Batch
```

### <a name="example"></a><span data-ttu-id="3a737-126">Esempio</span><span class="sxs-lookup"><span data-stu-id="3a737-126">Example</span></span>

<span data-ttu-id="3a737-127">L'esempio seguente recupera la quota per la sottoscrizione, crea un account e rigenera la chiave dell'account primario.</span><span class="sxs-lookup"><span data-stu-id="3a737-127">The following example retrieves the quota for the subscription, creates an account, and regenerates the primary account key.</span></span>

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
> [<span data-ttu-id="3a737-128">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="3a737-128">Explore the management APIs</span></span>](/dotnet/api/overview/azure/batch/management)

## <a name="samples"></a><span data-ttu-id="3a737-129">Esempi</span><span class="sxs-lookup"><span data-stu-id="3a737-129">Samples</span></span>

* [<span data-ttu-id="3a737-130">Azure Batch Client and Management SDK for .NET Samples</span><span class="sxs-lookup"><span data-stu-id="3a737-130">Azure Batch Client and Management SDK for .NET Samples</span></span>](https://github.com/Azure/azure-batch-samples/tree/master/CSharp) (Esempi del client di Azure Batch e di Management SDK per .NET)

<span data-ttu-id="3a737-131">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="3a737-131">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
