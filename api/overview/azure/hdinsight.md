---
title: Azure HDInsight .NET SDK
description: Informazioni di riferimento per Azure HDInsight .NET SDK
ms.date: 9/19/2018
ms.topic: reference
ms.service: hdinsight
ms.openlocfilehash: 35e2c8c07fb2b86b2d0ae9be4f855e369c1aa86d
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348203"
---
# <a name="azure-hdinsight-net-sdk"></a><span data-ttu-id="7aa1b-103">Azure HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7aa1b-103">Azure HDInsight .NET SDK</span></span>

## <a name="azure-hdinsight-libraries-for-net-2x"></a><span data-ttu-id="7aa1b-104">Librerie di Azure HDInsight per .NET 2.X</span><span class="sxs-lookup"><span data-stu-id="7aa1b-104">Azure HDInsight libraries for .NET 2.X</span></span>

## <a name="overview"></a><span data-ttu-id="7aa1b-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7aa1b-105">Overview</span></span>

<span data-ttu-id="7aa1b-106">HDInsight .NET SDK fornisce le classi necessarie per la creazione, la configurazione, l'invio e il monitoraggio dei processi Hadoop gestiti da un servizio HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-106">The HDInsight Service .NET SDK provides classes that relate to the creation, configuration, submission, and monitoring of Hadoop jobs managed by an Azure HDInsight Service.</span></span> <span data-ttu-id="7aa1b-107">Fornisce inoltre le classi per gestire le sottoscrizioni di Azure tramite il servizio HDInsight e per configurare cluster, account di archiviazione e altri asset associati al cluster HDInsight gestiti da una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-107">In addition, it provides classes to manage Azure subscriptions using the HDInsight Service and to configure the clusters, storage accounts, and other assets associated with the HDInsight clusters that are managed by an Azure subscription.</span></span>

## <a name="management-libraries"></a><span data-ttu-id="7aa1b-108">Librerie di gestione</span><span class="sxs-lookup"><span data-stu-id="7aa1b-108">Management libraries</span></span>

### <a name="jobs"></a><span data-ttu-id="7aa1b-109">Processi</span><span class="sxs-lookup"><span data-stu-id="7aa1b-109">Jobs</span></span>

<span data-ttu-id="7aa1b-110">Usare Azure HDInsight Client SDK per creare, gestire e monitorare i processi in un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-110">Use the Azure HDInsight client SDK to create, manage, and monitor jobs on a Hadoop cluster.</span></span> 

<span data-ttu-id="7aa1b-111">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="7aa1b-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7aa1b-112">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="7aa1b-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a><span data-ttu-id="7aa1b-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="7aa1b-113">Code Example</span></span>

<span data-ttu-id="7aa1b-114">Questo esempio mostra l'esecuzione di un processo Hive in un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-114">This example runs a Hive job in a Hadoop cluster.</span></span>

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

### <a name="hdinsight"></a><span data-ttu-id="7aa1b-115">HDInsight</span><span class="sxs-lookup"><span data-stu-id="7aa1b-115">HDInsight</span></span>

<span data-ttu-id="7aa1b-116">Usare Azure HDInsight Management SDK per creare, gestire, avviare, arrestare e ridimensionare i cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-116">Use the Azure HDInsight management SDK to create, manage, start, stop, and scale Hadoop clusters.</span></span>

<span data-ttu-id="7aa1b-117">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="7aa1b-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7aa1b-118">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="7aa1b-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a><span data-ttu-id="7aa1b-119">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="7aa1b-119">Code Example</span></span>

<span data-ttu-id="7aa1b-120">Questo esempio mostra la creazione di un cluster Hadoop Linux a due nodi in HDInsight con una risorsa di archiviazione BLOB di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-120">This example creates an HDInsight two node Linux Hadoop cluster with an existing Azure Blob Storage.</span></span>

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
> [<span data-ttu-id="7aa1b-121">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="7aa1b-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a><span data-ttu-id="7aa1b-122">Esempi</span><span class="sxs-lookup"><span data-stu-id="7aa1b-122">Samples</span></span>

- [<span data-ttu-id="7aa1b-123">Creazione del cluster</span><span class="sxs-lookup"><span data-stu-id="7aa1b-123">Cluster creation</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [<span data-ttu-id="7aa1b-124">Gestione dei cluster</span><span class="sxs-lookup"><span data-stu-id="7aa1b-124">Cluster management</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [<span data-ttu-id="7aa1b-125">Eseguire processi Hive</span><span class="sxs-lookup"><span data-stu-id="7aa1b-125">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="7aa1b-126">Eseguire processi Pig</span><span class="sxs-lookup"><span data-stu-id="7aa1b-126">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="7aa1b-127">Altri processi</span><span class="sxs-lookup"><span data-stu-id="7aa1b-127">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

<span data-ttu-id="7aa1b-128">Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) degli esempi di codice per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-128">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) of Azure SQL Database samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

## <a name="hdinsight-net-management-sdk-3x-preview"></a><span data-ttu-id="7aa1b-129">Anteprima di HDInsight .NET Management SDK 3.X</span><span class="sxs-lookup"><span data-stu-id="7aa1b-129">HDInsight .NET Management SDK 3.X Preview</span></span>

## <a name="overview"></a><span data-ttu-id="7aa1b-130">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7aa1b-130">Overview</span></span>

<span data-ttu-id="7aa1b-131">HDInsight .NET SDK fornisce classi e metodi che consentono di gestire i cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-131">The HDInsight .NET SDK provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="7aa1b-132">Include operazioni per creare, eliminare, aggiornare, elencare, ridimensionare, eseguire azioni di script, monitorare, ottenere le proprietà dei cluster di HDInsight e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-132">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7aa1b-133">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7aa1b-133">Prerequisites</span></span>

* <span data-ttu-id="7aa1b-134">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-134">An Azure account.</span></span> <span data-ttu-id="7aa1b-135">Se non è disponibile, [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7aa1b-135">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="7aa1b-136">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7aa1b-136">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a><span data-ttu-id="7aa1b-137">Installazione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="7aa1b-137">SDK Installation</span></span>

<span data-ttu-id="7aa1b-138">Dal progetto Visual Studio, aprire la console di Gestione pacchetti facendo clic su **Strumenti**, **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-138">From your Visual Studio project, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>

<span data-ttu-id="7aa1b-139">In Console di Gestione pacchetti eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-139">In the Package Manager Console, execute the following commands:</span></span>

```
  Install-Package Microsoft.Azure.Management.HDInsight -Version 3.1.0-preview
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a><span data-ttu-id="7aa1b-140">Authentication</span><span class="sxs-lookup"><span data-stu-id="7aa1b-140">Authentication</span></span>

<span data-ttu-id="7aa1b-141">L'SDK deve essere prima autenticato con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-141">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="7aa1b-142">Seguire questo esempio per creare un'entità servizio e usarla per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-142">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="7aa1b-143">Al termine si avrà un'istanza di un `HDInsightManagementClient` che contiene molti metodi, descritti nelle sezioni seguenti, che possono essere usati per operazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-143">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="7aa1b-144">Oltre all'esempio seguente esistono altre modalità di autenticazione che possono essere più adatte alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-144">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="7aa1b-145">Tutti i metodi sono descritti qui: [Eseguire l'autenticazione con le librerie di Azure per .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span><span class="sxs-lookup"><span data-stu-id="7aa1b-145">All methods are outlined here: [Authenticate with the Azure Libraries for .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="7aa1b-146">Esempio di autenticazione con un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="7aa1b-146">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="7aa1b-147">Per prima cosa, accedere ad [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="7aa1b-147">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="7aa1b-148">Verificare che si stia attualmente usando la sottoscrizione in cui si vuole creare l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-148">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="7aa1b-149">Le informazioni sulla sottoscrizione vengono visualizzate in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-149">Your subscription information is displayed as JSON.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

<span data-ttu-id="7aa1b-150">Se non si è eseguito l'accesso alla sottoscrizione corretta, selezionare quella corretta eseguendo:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-150">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="7aa1b-151">Se il provider di risorse HDInsight non è già stato registrato con un altro metodo, ad esempio creando un cluster HDInsight tramite il portale di Azure, è necessario eseguire questa operazione una volta prima di poter eseguire l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-151">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="7aa1b-152">La registrazione può essere eseguita da [Azure Cloud Shell](https://shell.azure.com/bash) eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-152">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="7aa1b-153">Scegliere quindi un nome per l'entità servizio e crearla con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-153">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="7aa1b-154">Verranno visualizzate le informazioni relative all'entità servizio in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-154">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
<span data-ttu-id="7aa1b-155">Copiare il frammento di codice seguente e compilare `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` e `SUBSCRIPTION_ID` con le stringhe JSON restituite dopo aver eseguito il comando per creare l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-155">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

```csharp
using Microsoft.Azure.Management.HDInsight;
using Microsoft.Azure.Management.HDInsight.Models;
using Microsoft.Azure.Management.ResourceManager.Fluent;

namespace HDI_SDK_Test
{
    class Program
    {
        static void Main(string[] args)
        {
            // Tenant ID for your Azure Subscription
            var TENANT_ID = "";
            // Your Service Principal App Client ID
            var CLIENT_ID = "";
            // Your Service Principal Client Secret
            var CLIENT_SECRET = "";
            // Azure Subscription ID
            var SUBSCRIPTION_ID = "";

            var credentials = SdkContext.AzureCredentialsFactory
                .FromServicePrincipal(
                CLIENT_ID,
                CLIENT_SECRET,
                TENANT_ID,
                AzureEnvironment.AzureGlobalCloud);

            var client = new HDInsightManagementClient(credentials);
            client.SubscriptionId = SUBSCRIPTION_ID;
        }
    }
}
```


## <a name="cluster-management"></a><span data-ttu-id="7aa1b-156">Gestione dei cluster</span><span class="sxs-lookup"><span data-stu-id="7aa1b-156">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="7aa1b-157">Questa sezione presuppone che l'utente abbia già eseguito l'autenticazione e abbia creato un'istanza `HDInsightManagementClient` che ha poi archiviato in una variabile chiamata `client`.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-157">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="7aa1b-158">Le istruzioni per l'autenticazione e l'ottenimento di un `HDInsightManagementClient` sono disponibili nella sezione Autenticazione precedente.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-158">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="7aa1b-159">Creare un cluster</span><span class="sxs-lookup"><span data-stu-id="7aa1b-159">Create a Cluster</span></span>

<span data-ttu-id="7aa1b-160">Un nuovo cluster può essere creato chiamando `client.Clusters.Create()`.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-160">A new cluster can be created by calling `client.Clusters.Create()`.</span></span> 

#### <a name="example"></a><span data-ttu-id="7aa1b-161">Esempio</span><span class="sxs-lookup"><span data-stu-id="7aa1b-161">Example</span></span>

<span data-ttu-id="7aa1b-162">Questo esempio illustra come creare un cluster Spark con 2 nodi head e 1 nodo del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-162">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="7aa1b-163">È prima necessario creare un gruppo di risorse e un account di archiviazione, come spiegato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-163">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="7aa1b-164">Se sono già stati creati, è possibile ignorare questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-164">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="7aa1b-165">Creazione di un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="7aa1b-165">Creating a Resource Group</span></span>

<span data-ttu-id="7aa1b-166">È possibile creare un gruppo di risorse con [Azure Cloud Shell](https://shell.azure.com/bash) eseguendo</span><span class="sxs-lookup"><span data-stu-id="7aa1b-166">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="7aa1b-167">Creazione di un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="7aa1b-167">Creating a Storage Account</span></span>

<span data-ttu-id="7aa1b-168">È possibile creare un account di archiviazione con [Azure Cloud Shell](https://shell.azure.com/bash) eseguendo:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-168">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="7aa1b-169">Eseguire ora questo comando per ottenere la chiave per l'account di archiviazione. Questa chiave sarà necessaria per creare un cluster:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-169">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="7aa1b-170">Il frammento di codice .NET seguente crea un cluster Spark con 2 nodi head e 1 nodo del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-170">The below .NET snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="7aa1b-171">Inserire le variabili vuote come spiegato nei commenti. È possibile modificare altri parametri in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-171">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

```csharp
// The name for the cluster you are creating
var clusterName = "";
// The name of your existing Resource Group
var resourceGroupName = "";
// Choose a username
var username = "";
// Choose a password
var password = "";
// Replace <> with the name of your storage account
var storageAccount = "<>.blob.core.windows.net";
// Storage account key you obtained above
var storageAccountKey = "";
// Choose a region
var location = "";
var container = "default";

var parameters = new ClusterCreateParametersExtended
{
    Location = location,
    Tags = new Dictionary<string, string>(),
    Properties = new ClusterCreateProperties
    {
        ClusterVersion = "3.6",
        OsType = OSType.Linux,
        ClusterDefinition = new ClusterDefinition
        {
            Kind = "Hadoop",            
            Configurations = new Dictionary<string, Dictionary<string, string>>()
            {                
                { "gateway", new Dictionary<string, string>
                    {
                        { "restAuthCredential.isEnabled", "true" },
                        { "restAuthCredential.username", username},
                        { "restAuthCredential.password", password}
                    }
                }
            }
        },
        Tier = Tier.Standard,
        ComputeProfile = new ComputeProfile
        {
            Roles = new List<Role>{
                new Role
                {
                    Name = "headnode",
                    TargetInstanceCount = 2,
                    HardwareProfile = new HardwareProfile
                    {
                        VmSize = "Large"
                    },
                    OsProfile = new OsProfile
                    {
                        LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
                        {
                            Username = username,
                            Password = password
                        }
                    }
                },
                new Role
                {
                    Name = "workernode",
                    TargetInstanceCount = 1,
                    HardwareProfile = new HardwareProfile
                    {
                        VmSize = "Large"
                    },
                    OsProfile = new OsProfile
                    {
                        LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
                        {
                            Username = username,
                            Password = password
                        }
                    }
                },
            }
        },
        StorageProfile = new StorageProfile
        {
            Storageaccounts = new[]
            {
                new StorageAccount
                {
                    Name = storageAccount,
                    Key = storageAccountKey,
                    Container = container,
                    IsDefault = true
                }
            }
        }
    }
};
client.Clusters.Create(
    resourceGroupName,
    clusterName,
    parameters
);
```

### <a name="get-cluster-details"></a><span data-ttu-id="7aa1b-172">Ottenere i dettagli del cluster</span><span class="sxs-lookup"><span data-stu-id="7aa1b-172">Get Cluster Details</span></span>

<span data-ttu-id="7aa1b-173">Per ottenere le proprietà di un dato cluster:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-173">To get properties for a given cluster:</span></span>

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="7aa1b-174">Esempio</span><span class="sxs-lookup"><span data-stu-id="7aa1b-174">Example</span></span>

<span data-ttu-id="7aa1b-175">È possibile usare `get` per verificare che il cluster sia stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-175">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

<span data-ttu-id="7aa1b-176">L'output sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-176">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> <span data-ttu-id="7aa1b-177">Il valore restituito di `get`, archiviato nella variabile `myCluster`, è di tipo `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-177">The return value of `get`, stored in variable `myCluster`, is of type `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span></span> <span data-ttu-id="7aa1b-178">Un elenco completo delle proprietà di questo oggetto è disponibile [qui](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span><span class="sxs-lookup"><span data-stu-id="7aa1b-178">A full list of this object's properties can be found [here](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span></span>


### <a name="list-clusters"></a><span data-ttu-id="7aa1b-179">Elencare cluster</span><span class="sxs-lookup"><span data-stu-id="7aa1b-179">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="7aa1b-180">Elencare i cluster nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="7aa1b-180">List Clusters Under The Subscription</span></span>

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="7aa1b-181">Elencare i cluster per gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="7aa1b-181">List Clusters By Resource Group</span></span>

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="7aa1b-182">Sia `List()` che `ListByResourceGroup()` restituiscono un oggetto `IPage<Cluster>`.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-182">Both `List()` and `ListByResourceGroup()` return an `IPage<Cluster>` object.</span></span> <span data-ttu-id="7aa1b-183">Per ottenere la pagina successiva è possibile chiamare `client.Clusters.ListNext("Next Page Link")`.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-183">To get the next page, you can call `client.Clusters.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="7aa1b-184">Questa operazione può essere ripetuta fino a quando `NextPageLink` non diventa `null`, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-184">This can be repeated until `NextPageLink` is `null`, as shown in the example below.</span></span>

#### <a name="example"></a><span data-ttu-id="7aa1b-185">Esempio</span><span class="sxs-lookup"><span data-stu-id="7aa1b-185">Example</span></span>
<span data-ttu-id="7aa1b-186">L'esempio seguente mostra le proprietà di tutti i cluster per la sottoscrizione corrente:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-186">The following example prints the properties of all clusters for the current subscription:</span></span>

```csharp
var clustersPaged = client.Clusters.List();
while (true)
{
  foreach (var cluster in clustersPaged)
  {
    Debug.WriteLine(cluster.Name);
  
}  if (clustersPaged.NextPageLink == null)
  {
    break;
  }
  clustersPaged = client.Clusters.ListNext(clustersPaged.NextPageLink);
}
```

### <a name="delete-a-cluster"></a><span data-ttu-id="7aa1b-187">Eliminare un cluster</span><span class="sxs-lookup"><span data-stu-id="7aa1b-187">Delete a Cluster</span></span>

<span data-ttu-id="7aa1b-188">Per eliminare un cluster:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-188">To delete a cluster:</span></span>

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="7aa1b-189">Aggiornare i tag del cluster</span><span class="sxs-lookup"><span data-stu-id="7aa1b-189">Update Cluster Tags</span></span>

<span data-ttu-id="7aa1b-190">È possibile aggiornare i tag di un dato cluster nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-190">You can update the tags of a given cluster like so:</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a><span data-ttu-id="7aa1b-191">Esempio</span><span class="sxs-lookup"><span data-stu-id="7aa1b-191">Example</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="resize-cluster"></a><span data-ttu-id="7aa1b-192">Ridimensionare un cluster</span><span class="sxs-lookup"><span data-stu-id="7aa1b-192">Resize Cluster</span></span>

<span data-ttu-id="7aa1b-193">È possibile ridimensionare il numero di nodi di ruolo di lavoro di un dato cluster specificando una nuova dimensione nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-193">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="7aa1b-194">Monitoraggio del cluster</span><span class="sxs-lookup"><span data-stu-id="7aa1b-194">Cluster Monitoring</span></span>

<span data-ttu-id="7aa1b-195">HDInsight Management SDK può essere usato anche per gestire il monitoraggio dei cluster tramite Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="7aa1b-195">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="7aa1b-196">Abilitare il monitoraggio di OMS</span><span class="sxs-lookup"><span data-stu-id="7aa1b-196">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="7aa1b-197">Per abilitare il monitoraggio di OMS è necessaria un'area di lavoro Log Analytics esistente.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-197">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="7aa1b-198">Se l'area non è stata ancora creata, vedere [Creare un'area di lavoro Log Analytics nel portale di Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace) per informazioni su come crearla.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-198">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="7aa1b-199">Per abilitare il monitoraggio di OMS nel cluster:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-199">To enable OMS Monitoring on your cluster:</span></span>

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="7aa1b-200">Visualizzare lo stato del monitoraggio di OMS</span><span class="sxs-lookup"><span data-stu-id="7aa1b-200">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="7aa1b-201">Per ottenere lo stato di OMS nel cluster:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-201">To get the status of OMS on your cluster:</span></span>

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="7aa1b-202">Disabilitare il monitoraggio di OMS</span><span class="sxs-lookup"><span data-stu-id="7aa1b-202">Disable OMS Monitoring</span></span>

<span data-ttu-id="7aa1b-203">Per disabilitare OMS nel cluster:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-203">To disable OMS on your cluster:</span></span>

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="7aa1b-204">Azioni script</span><span class="sxs-lookup"><span data-stu-id="7aa1b-204">Script Actions</span></span>

<span data-ttu-id="7aa1b-205">HDInsight offre un metodo di configurazione denominato "azioni script" che richiama script personalizzati per il cluster.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-205">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="7aa1b-206">Per altre informazioni sulle azioni script, vedere [Personalizzare i cluster HDInsight basati su Linux tramite azioni script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="7aa1b-206">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="7aa1b-207">Eseguire azioni script</span><span class="sxs-lookup"><span data-stu-id="7aa1b-207">Execute Script Actions</span></span>

<span data-ttu-id="7aa1b-208">È possibile eseguire azioni script in un dato cluster nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-208">You can execute script actions on a given cluster like so:</span></span>

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="7aa1b-209">Eliminare un'azione script</span><span class="sxs-lookup"><span data-stu-id="7aa1b-209">Delete Script Action</span></span>

<span data-ttu-id="7aa1b-210">Per eliminare una determinata azione script persistente in un dato cluster:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-210">To delete a specified persisted script action on a given cluster:</span></span>

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="7aa1b-211">Elencare le azioni script persistenti</span><span class="sxs-lookup"><span data-stu-id="7aa1b-211">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="7aa1b-212">`ListPersistedScripts()` e `List()` restituiscono un oggetto `IPage<RuntimeScriptActionDetail>`.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-212">`ListPersistedScripts()` and `List()` return an `IPage<RuntimeScriptActionDetail>` object.</span></span> <span data-ttu-id="7aa1b-213">Per ottenere la pagina successiva è possibile chiamare `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` o `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-213">To get the next page, you can call `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` or `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="7aa1b-214">Questa operazione può essere ripetuta fino a quando `NextPageLink` non diventa `null`, come illustrato negli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-214">This can be repeated until `NextPageLink` is `null`, as shown in the examples below.</span></span>

<span data-ttu-id="7aa1b-215">Per elencare tutte le azioni script persistenti per il cluster specificato:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-215">To list all persisted script actions for the specified cluster:</span></span>
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="7aa1b-216">Esempio</span><span class="sxs-lookup"><span data-stu-id="7aa1b-216">Example</span></span>

```csharp
var scriptsPaged = client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
while (true)
{
    foreach (var script in scriptsPaged)
    {
        Debug.WriteLine(script.Name); //There are other properties of RuntimeScriptActionDetail besides Name, such as Status, Operation, StartTime, EndTime, etc. See reference documentation.
    }
    if (scriptsPaged.NextPageLink == null)
    {
        break;
    }
    scriptsPaged = client.ScriptActions.ListPersistedScriptsNext(scriptsPaged.NextPageLink);
}
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="7aa1b-217">Elencare la cronologia di esecuzione di tutti gli script</span><span class="sxs-lookup"><span data-stu-id="7aa1b-217">List All Scripts' Execution History</span></span>

<span data-ttu-id="7aa1b-218">Per elencare la cronologia di esecuzione di tutti gli script per il cluster specificato:</span><span class="sxs-lookup"><span data-stu-id="7aa1b-218">To list all scripts' execution history for the specified cluster:</span></span>

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="7aa1b-219">Esempio</span><span class="sxs-lookup"><span data-stu-id="7aa1b-219">Example</span></span>

<span data-ttu-id="7aa1b-220">Questo esempio visualizza tutti i dettagli di tutte le precedenti esecuzioni di script.</span><span class="sxs-lookup"><span data-stu-id="7aa1b-220">This example prints all the details for all past script executions.</span></span>

```csharp
var scriptExecutionsPaged = client.ScriptExecutionHistory.List("<Resource Group Name>", "<Cluster Name>");
while (true)
{
    foreach (var script in scriptExecutionsPaged)
    {
        Debug.WriteLine(script.Name); //There are other properties of RuntimeScriptActionDetail besides Name, such as Status, Operation, StartTime, EndTime, etc. See reference documentation.

    }
    if (scriptExecutionsPaged.NextPageLink == null)
    {
        break;
    }
    scriptExecutionsPaged = client.ScriptExecutionHistory.ListNext(scriptExecutionsPaged.NextPageLink);
}
```
