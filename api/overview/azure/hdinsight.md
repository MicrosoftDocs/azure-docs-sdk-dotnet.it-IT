---
title: Librerie di Azure HDInsight per .NET
description: Informazioni di riferimento sulle librerie di Azure HDInsight per .NET
keywords: Azure, .NET, SDK, API, HDInsight
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 3f0b6f48d89d582180193f52ce85c328e6bdf8e0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-hdinsight-libraries-for-net"></a><span data-ttu-id="8caa8-104">Librerie di Azure HDInsight per .NET</span><span class="sxs-lookup"><span data-stu-id="8caa8-104">Azure HDInsight libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="8caa8-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8caa8-105">Overview</span></span>

<span data-ttu-id="8caa8-106">HDInsight .NET SDK fornisce le classi necessarie per la creazione, la configurazione, l'invio e il monitoraggio dei processi Hadoop gestiti da un servizio HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="8caa8-106">The HDInsight Service .NET SDK provides classes that relate to the creation, configuration, submission, and monitoring of Hadoop jobs managed by an Azure HDInsight Service.</span></span> <span data-ttu-id="8caa8-107">Fornisce inoltre le classi per gestire le sottoscrizioni di Azure tramite il servizio HDInsight e per configurare cluster, account di archiviazione e altri asset associati al cluster HDInsight gestiti da una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8caa8-107">In addition, it provides classes to manage Azure subscriptions using the HDInsight Service and to configure the clusters, storage accounts, and other assets associated with the HDInsight clusters that are managed by an Azure subscription.</span></span>

## <a name="management-libraries"></a><span data-ttu-id="8caa8-108">Librerie di gestione</span><span class="sxs-lookup"><span data-stu-id="8caa8-108">Management libraries</span></span>

### <a name="jobs"></a><span data-ttu-id="8caa8-109">Processi</span><span class="sxs-lookup"><span data-stu-id="8caa8-109">Jobs</span></span>

<span data-ttu-id="8caa8-110">Usare Azure HDInsight Client SDK per creare, gestire e monitorare i processi in un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="8caa8-110">Use the Azure HDInsight client SDK to create, manage, and monitor jobs on a Hadoop cluster.</span></span> 

<span data-ttu-id="8caa8-111">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="8caa8-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="8caa8-112">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="8caa8-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a><span data-ttu-id="8caa8-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="8caa8-113">Code Example</span></span>

<span data-ttu-id="8caa8-114">Questo esempio mostra l'esecuzione di un processo Hive in un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="8caa8-114">This example runs a Hive job in a Hadoop cluster.</span></span>

```csharp
HDInsightJobManagementClient managementClient = new HDInsightJobManagementClient(clusterUri, credentials);

Dictionary<string, string> defines = new Dictionary<string, string> {
    { "hive.execution.engine", "tez" },
    { "hive.exec.reducers.max", "1" }
};
List<string> arguments = new List<string> { { "argA" }, { "argB" } };
HiveJobSubmissionParameters parameters = new HiveJobSubmissionParameters
{
    Query = "SHOW TABLES",
    Defines = defines,
    Arguments = arguments
};

JobSubmissionResponse jobResponse = managementClient.JobManagement.SubmitHiveJob(parameters);
```

### <a name="hdinsight"></a><span data-ttu-id="8caa8-115">HDInsight</span><span class="sxs-lookup"><span data-stu-id="8caa8-115">HDInsight</span></span>

<span data-ttu-id="8caa8-116">Usare Azure HDInsight Management SDK per creare, gestire, avviare, arrestare e ridimensionare i cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="8caa8-116">Use the Azure HDInsight management SDK to create, manage, start, stop, and scale Hadoop clusters.</span></span>

<span data-ttu-id="8caa8-117">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="8caa8-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="8caa8-118">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="8caa8-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a><span data-ttu-id="8caa8-119">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="8caa8-119">Code Example</span></span>

<span data-ttu-id="8caa8-120">Questo esempio mostra la creazione di un cluster Hadoop Linux a due nodi in HDInsight con una risorsa di archiviazione BLOB di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="8caa8-120">This example creates an HDInsight two node Linux Hadoop cluster with an existing Azure Blob Storage.</span></span>

```csharp
HDInsightManagementClient managementClient = new HDInsightManagementClient(authToken);
// Set parameters for the new cluster
ClusterCreateParameters parameters = new ClusterCreateParameters
{
    ClusterSizeInNodes = 2,
    UserName = "admin",
    Password = "<Enter HTTP User Password>",
    ClusterType = "Hadoop",
    OSType = OSType.Linux,
    Version = "3.5",
    // Use an Azure storage account as the default storage
    DefaultStorageInfo = new AzureStorageInfo("<StorageAccount>", "<StorageKey>", "<BlobContainerName>"),
    Location = "EAST US 2",
    SshUserName = "sshuser",
    SshPassword = "<Enter SSH User Password>",
};

// Create the cluster
managementClient.Clusters.Create("<ExistingResourceGroupName>", "<NewClusterName>", parameters);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8caa8-121">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="8caa8-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a><span data-ttu-id="8caa8-122">Esempi</span><span class="sxs-lookup"><span data-stu-id="8caa8-122">Samples</span></span>

- [<span data-ttu-id="8caa8-123">Creazione del cluster</span><span class="sxs-lookup"><span data-stu-id="8caa8-123">Cluster creation</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [<span data-ttu-id="8caa8-124">Gestione dei cluster</span><span class="sxs-lookup"><span data-stu-id="8caa8-124">Cluster management</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [<span data-ttu-id="8caa8-125">Eseguire processi Hive</span><span class="sxs-lookup"><span data-stu-id="8caa8-125">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="8caa8-126">Eseguire processi Pig</span><span class="sxs-lookup"><span data-stu-id="8caa8-126">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="8caa8-127">Altri processi</span><span class="sxs-lookup"><span data-stu-id="8caa8-127">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

<span data-ttu-id="8caa8-128">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) degli esempi di codice per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="8caa8-128">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) of Azure SQL Database samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
