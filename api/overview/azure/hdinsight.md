---
title: Azure HDInsight SDK per .NET
description: Informazioni di riferimento per Azure HDInsight SDK per .NET
ms.date: 04/10/2019
ms.topic: reference
ms.service: hdinsight
ms.openlocfilehash: 2282a302b269a52c71ed88c26e021344cdca4382
ms.sourcegitcommit: 4328168172ac1b1a448e16988f75199262bc5c2d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2019
ms.locfileid: "59700259"
---
# <a name="azure-hdinsight-sdk-for-net"></a><span data-ttu-id="07c4d-103">Azure HDInsight SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="07c4d-103">Azure HDInsight SDK for .NET</span></span>

<span data-ttu-id="07c4d-104">Azure HDInsight offre SDK di gestione e processi per .NET che forniscono classi per la gestione del cluster HDInsight e per l'invio e il monitoraggio di processi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="07c4d-104">Azure HDInsight offers management and job SDKs for .NET that provide classes for managing your HDInsight cluster and submitting and monitoring Hadoop jobs.</span></span>

## <a name="management"></a><span data-ttu-id="07c4d-105">Gestione</span><span class="sxs-lookup"><span data-stu-id="07c4d-105">Management</span></span>

<span data-ttu-id="07c4d-106">L'SDK HDInsight di gestione per .NET fornisce classi e metodi che consentono di gestire i cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="07c4d-106">The HDInsight management SDK for .NET provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="07c4d-107">Include operazioni per creare, eliminare, aggiornare, elencare, ridimensionare, eseguire azioni di script, monitorare, ottenere le proprietà dei cluster di HDInsight e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="07c4d-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07c4d-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="07c4d-108">Prerequisites</span></span>

* <span data-ttu-id="07c4d-109">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="07c4d-109">An Azure account.</span></span> <span data-ttu-id="07c4d-110">Se non è disponibile, [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="07c4d-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="07c4d-111">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07c4d-111">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a><span data-ttu-id="07c4d-112">Installazione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="07c4d-112">SDK Installation</span></span>

<span data-ttu-id="07c4d-113">Dal progetto Visual Studio, aprire la console di Gestione pacchetti facendo clic su **Strumenti**, **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="07c4d-113">From your Visual Studio project, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>

<span data-ttu-id="07c4d-114">In Console di Gestione pacchetti eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="07c4d-114">In the Package Manager Console, execute the following commands:</span></span>

```
  Install-Package Microsoft.Azure.Management.HDInsight
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a><span data-ttu-id="07c4d-115">Authentication</span><span class="sxs-lookup"><span data-stu-id="07c4d-115">Authentication</span></span>

<span data-ttu-id="07c4d-116">L'SDK deve essere prima autenticato con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="07c4d-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="07c4d-117">Seguire questo esempio per creare un'entità servizio e usarla per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="07c4d-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="07c4d-118">Al termine si avrà un'istanza di un `HDInsightManagementClient` che contiene molti metodi, descritti nelle sezioni seguenti, che possono essere usati per operazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="07c4d-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="07c4d-119">Oltre all'esempio seguente esistono altre modalità di autenticazione che possono essere più adatte alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="07c4d-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="07c4d-120">Tutti i metodi sono descritti di seguito: [Eseguire l'autenticazione con le librerie di Azure per .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span><span class="sxs-lookup"><span data-stu-id="07c4d-120">All methods are outlined here: [Authenticate with the Azure Libraries for .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="07c4d-121">Esempio di autenticazione con un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="07c4d-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="07c4d-122">Per prima cosa, accedere ad [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="07c4d-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="07c4d-123">Verificare che si stia attualmente usando la sottoscrizione in cui si vuole creare l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="07c4d-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="07c4d-124">Le informazioni sulla sottoscrizione vengono visualizzate in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="07c4d-124">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="07c4d-125">Se non si è eseguito l'accesso alla sottoscrizione corretta, selezionare quella corretta eseguendo:</span><span class="sxs-lookup"><span data-stu-id="07c4d-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="07c4d-126">Se il provider di risorse HDInsight non è già stato registrato con un altro metodo, ad esempio creando un cluster HDInsight tramite il portale di Azure, è necessario eseguire questa operazione una volta prima di poter eseguire l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="07c4d-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="07c4d-127">La registrazione può essere eseguita da [Azure Cloud Shell](https://shell.azure.com/bash) eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="07c4d-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="07c4d-128">Scegliere quindi un nome per l'entità servizio e crearla con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="07c4d-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="07c4d-129">Verranno visualizzate le informazioni relative all'entità servizio in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="07c4d-129">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="07c4d-130">Copiare il frammento di codice seguente e compilare `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` e `SUBSCRIPTION_ID` con le stringhe JSON restituite dopo aver eseguito il comando per creare l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="07c4d-130">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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

## <a name="cluster-management"></a><span data-ttu-id="07c4d-131">Gestione dei cluster</span><span class="sxs-lookup"><span data-stu-id="07c4d-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="07c4d-132">Questa sezione presuppone che l'utente abbia già eseguito l'autenticazione e abbia creato un'istanza `HDInsightManagementClient` che ha poi archiviato in una variabile chiamata `client`.</span><span class="sxs-lookup"><span data-stu-id="07c4d-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="07c4d-133">Le istruzioni per l'autenticazione e l'ottenimento di un `HDInsightManagementClient` sono disponibili nella sezione Autenticazione precedente.</span><span class="sxs-lookup"><span data-stu-id="07c4d-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="07c4d-134">Creare un cluster</span><span class="sxs-lookup"><span data-stu-id="07c4d-134">Create a Cluster</span></span>

<span data-ttu-id="07c4d-135">Un nuovo cluster può essere creato chiamando `client.Clusters.Create()`.</span><span class="sxs-lookup"><span data-stu-id="07c4d-135">A new cluster can be created by calling `client.Clusters.Create()`.</span></span>

#### <a name="samples"></a><span data-ttu-id="07c4d-136">Esempi</span><span class="sxs-lookup"><span data-stu-id="07c4d-136">Samples</span></span>

<span data-ttu-id="07c4d-137">Sono disponibili esempi di codice per la creazione di diversi tipi comuni di cluster HDInsight: [Esempi HDInsight .NET](https://github.com/Azure-Samples/hdinsight-dotnet-sdk-samples).</span><span class="sxs-lookup"><span data-stu-id="07c4d-137">Code samples for creating several common types of HDInsight clusters are available: [HDInsight .NET Samples](https://github.com/Azure-Samples/hdinsight-dotnet-sdk-samples).</span></span>

#### <a name="example"></a><span data-ttu-id="07c4d-138">Esempio</span><span class="sxs-lookup"><span data-stu-id="07c4d-138">Example</span></span>

<span data-ttu-id="07c4d-139">Questo esempio illustra come creare un cluster Spark con 2 nodi head e 1 nodo del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="07c4d-139">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="07c4d-140">È prima necessario creare un gruppo di risorse e un account di archiviazione, come spiegato di seguito.</span><span class="sxs-lookup"><span data-stu-id="07c4d-140">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="07c4d-141">Se sono già stati creati, è possibile ignorare questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="07c4d-141">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="07c4d-142">Creazione di un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="07c4d-142">Creating a Resource Group</span></span>

<span data-ttu-id="07c4d-143">È possibile creare un gruppo di risorse con [Azure Cloud Shell](https://shell.azure.com/bash) eseguendo</span><span class="sxs-lookup"><span data-stu-id="07c4d-143">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="07c4d-144">Creazione di un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="07c4d-144">Creating a Storage Account</span></span>

<span data-ttu-id="07c4d-145">È possibile creare un account di archiviazione con [Azure Cloud Shell](https://shell.azure.com/bash) eseguendo:</span><span class="sxs-lookup"><span data-stu-id="07c4d-145">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="07c4d-146">Eseguire ora questo comando per ottenere la chiave per l'account di archiviazione. Questa chiave sarà necessaria per creare un cluster:</span><span class="sxs-lookup"><span data-stu-id="07c4d-146">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="07c4d-147">Il frammento di codice .NET seguente crea un cluster Spark con 2 nodi head e 1 nodo del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="07c4d-147">The below .NET snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="07c4d-148">Inserire le variabili vuote come spiegato nei commenti. È possibile modificare altri parametri in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="07c4d-148">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="07c4d-149">Ottenere i dettagli del cluster</span><span class="sxs-lookup"><span data-stu-id="07c4d-149">Get Cluster Details</span></span>

<span data-ttu-id="07c4d-150">Per ottenere le proprietà di un dato cluster:</span><span class="sxs-lookup"><span data-stu-id="07c4d-150">To get properties for a given cluster:</span></span>

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="07c4d-151">Esempio</span><span class="sxs-lookup"><span data-stu-id="07c4d-151">Example</span></span>

<span data-ttu-id="07c4d-152">È possibile usare `get` per verificare che il cluster sia stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="07c4d-152">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

<span data-ttu-id="07c4d-153">L'output sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="07c4d-153">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> <span data-ttu-id="07c4d-154">Il valore restituito di `get`, archiviato nella variabile `myCluster`, è di tipo `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span><span class="sxs-lookup"><span data-stu-id="07c4d-154">The return value of `get`, stored in variable `myCluster`, is of type `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span></span> <span data-ttu-id="07c4d-155">Un elenco completo delle proprietà di questo oggetto è disponibile [qui](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span><span class="sxs-lookup"><span data-stu-id="07c4d-155">A full list of this object's properties can be found [here](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span></span>


### <a name="list-clusters"></a><span data-ttu-id="07c4d-156">Elencare cluster</span><span class="sxs-lookup"><span data-stu-id="07c4d-156">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="07c4d-157">Elencare i cluster nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="07c4d-157">List Clusters Under The Subscription</span></span>

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="07c4d-158">Elencare i cluster per gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="07c4d-158">List Clusters By Resource Group</span></span>

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="07c4d-159">Sia `List()` che `ListByResourceGroup()` restituiscono un oggetto `IPage<Cluster>`.</span><span class="sxs-lookup"><span data-stu-id="07c4d-159">Both `List()` and `ListByResourceGroup()` return an `IPage<Cluster>` object.</span></span> <span data-ttu-id="07c4d-160">Per ottenere la pagina successiva è possibile chiamare `client.Clusters.ListNext("Next Page Link")`.</span><span class="sxs-lookup"><span data-stu-id="07c4d-160">To get the next page, you can call `client.Clusters.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="07c4d-161">Questa operazione può essere ripetuta fino a quando `NextPageLink` non diventa `null`, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="07c4d-161">This can be repeated until `NextPageLink` is `null`, as shown in the example below.</span></span>

#### <a name="example"></a><span data-ttu-id="07c4d-162">Esempio</span><span class="sxs-lookup"><span data-stu-id="07c4d-162">Example</span></span>
<span data-ttu-id="07c4d-163">L'esempio seguente mostra le proprietà di tutti i cluster per la sottoscrizione corrente:</span><span class="sxs-lookup"><span data-stu-id="07c4d-163">The following example prints the properties of all clusters for the current subscription:</span></span>

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

### <a name="delete-a-cluster"></a><span data-ttu-id="07c4d-164">Eliminare un cluster</span><span class="sxs-lookup"><span data-stu-id="07c4d-164">Delete a Cluster</span></span>

<span data-ttu-id="07c4d-165">Per eliminare un cluster:</span><span class="sxs-lookup"><span data-stu-id="07c4d-165">To delete a cluster:</span></span>

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="07c4d-166">Aggiornare i tag del cluster</span><span class="sxs-lookup"><span data-stu-id="07c4d-166">Update Cluster Tags</span></span>

<span data-ttu-id="07c4d-167">È possibile aggiornare i tag di un dato cluster nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="07c4d-167">You can update the tags of a given cluster like so:</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a><span data-ttu-id="07c4d-168">Esempio</span><span class="sxs-lookup"><span data-stu-id="07c4d-168">Example</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="resize-cluster"></a><span data-ttu-id="07c4d-169">Ridimensionare un cluster</span><span class="sxs-lookup"><span data-stu-id="07c4d-169">Resize Cluster</span></span>

<span data-ttu-id="07c4d-170">È possibile ridimensionare il numero di nodi di ruolo di lavoro di un dato cluster specificando una nuova dimensione nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="07c4d-170">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="07c4d-171">Monitoraggio del cluster</span><span class="sxs-lookup"><span data-stu-id="07c4d-171">Cluster Monitoring</span></span>

<span data-ttu-id="07c4d-172">HDInsight Management SDK può essere usato anche per gestire il monitoraggio dei cluster tramite Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="07c4d-172">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="07c4d-173">Abilitare il monitoraggio di OMS</span><span class="sxs-lookup"><span data-stu-id="07c4d-173">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="07c4d-174">Per abilitare il monitoraggio di OMS è necessaria un'area di lavoro Log Analytics esistente.</span><span class="sxs-lookup"><span data-stu-id="07c4d-174">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="07c4d-175">Se non è già stata creata una, è possibile ottenere informazioni su come farlo qui: [Creare un'area di lavoro Log Analytics nel portale di Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="07c4d-175">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="07c4d-176">Per abilitare il monitoraggio di OMS nel cluster:</span><span class="sxs-lookup"><span data-stu-id="07c4d-176">To enable OMS Monitoring on your cluster:</span></span>

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="07c4d-177">Visualizzare lo stato del monitoraggio di OMS</span><span class="sxs-lookup"><span data-stu-id="07c4d-177">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="07c4d-178">Per ottenere lo stato di OMS nel cluster:</span><span class="sxs-lookup"><span data-stu-id="07c4d-178">To get the status of OMS on your cluster:</span></span>

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="07c4d-179">Disabilitare il monitoraggio di OMS</span><span class="sxs-lookup"><span data-stu-id="07c4d-179">Disable OMS Monitoring</span></span>

<span data-ttu-id="07c4d-180">Per disabilitare OMS nel cluster:</span><span class="sxs-lookup"><span data-stu-id="07c4d-180">To disable OMS on your cluster:</span></span>

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="07c4d-181">Azioni script</span><span class="sxs-lookup"><span data-stu-id="07c4d-181">Script Actions</span></span>

<span data-ttu-id="07c4d-182">HDInsight offre un metodo di configurazione denominato "azioni script" che richiama script personalizzati per il cluster.</span><span class="sxs-lookup"><span data-stu-id="07c4d-182">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="07c4d-183">Altre informazioni su come usare le azioni dello script sono disponibili qui: [Personalizzare i cluster HDInsight basati su Linux tramite azioni script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="07c4d-183">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="07c4d-184">Eseguire azioni script</span><span class="sxs-lookup"><span data-stu-id="07c4d-184">Execute Script Actions</span></span>

<span data-ttu-id="07c4d-185">È possibile eseguire azioni script in un dato cluster nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="07c4d-185">You can execute script actions on a given cluster like so:</span></span>

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="07c4d-186">Eliminare un'azione script</span><span class="sxs-lookup"><span data-stu-id="07c4d-186">Delete Script Action</span></span>

<span data-ttu-id="07c4d-187">Per eliminare una determinata azione script persistente in un dato cluster:</span><span class="sxs-lookup"><span data-stu-id="07c4d-187">To delete a specified persisted script action on a given cluster:</span></span>

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="07c4d-188">Elencare le azioni script persistenti</span><span class="sxs-lookup"><span data-stu-id="07c4d-188">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="07c4d-189">`ListPersistedScripts()` e `List()` restituiscono un oggetto `IPage<RuntimeScriptActionDetail>`.</span><span class="sxs-lookup"><span data-stu-id="07c4d-189">`ListPersistedScripts()` and `List()` return an `IPage<RuntimeScriptActionDetail>` object.</span></span> <span data-ttu-id="07c4d-190">Per ottenere la pagina successiva è possibile chiamare `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` o `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span><span class="sxs-lookup"><span data-stu-id="07c4d-190">To get the next page, you can call `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` or `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="07c4d-191">Questa operazione può essere ripetuta fino a quando `NextPageLink` non diventa `null`, come illustrato negli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="07c4d-191">This can be repeated until `NextPageLink` is `null`, as shown in the examples below.</span></span>

<span data-ttu-id="07c4d-192">Per elencare tutte le azioni script persistenti per il cluster specificato:</span><span class="sxs-lookup"><span data-stu-id="07c4d-192">To list all persisted script actions for the specified cluster:</span></span>
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="07c4d-193">Esempio</span><span class="sxs-lookup"><span data-stu-id="07c4d-193">Example</span></span>

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

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="07c4d-194">Elencare la cronologia di esecuzione di tutti gli script</span><span class="sxs-lookup"><span data-stu-id="07c4d-194">List All Scripts' Execution History</span></span>

<span data-ttu-id="07c4d-195">Per elencare la cronologia di esecuzione di tutti gli script per il cluster specificato:</span><span class="sxs-lookup"><span data-stu-id="07c4d-195">To list all scripts' execution history for the specified cluster:</span></span>

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="07c4d-196">Esempio</span><span class="sxs-lookup"><span data-stu-id="07c4d-196">Example</span></span>

<span data-ttu-id="07c4d-197">Questo esempio visualizza tutti i dettagli di tutte le precedenti esecuzioni di script.</span><span class="sxs-lookup"><span data-stu-id="07c4d-197">This example prints all the details for all past script executions.</span></span>

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

## <a name="jobs"></a><span data-ttu-id="07c4d-198">Processi</span><span class="sxs-lookup"><span data-stu-id="07c4d-198">Jobs</span></span>

<span data-ttu-id="07c4d-199">Usare l'SDK Azure HDInsight per i processi per .NET per creare, gestire e monitorare i processi in un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="07c4d-199">Use the Azure HDInsight job SDK for .NET to create, manage, and monitor jobs on a Hadoop cluster.</span></span>

### <a name="sdk-installation"></a><span data-ttu-id="07c4d-200">Installazione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="07c4d-200">SDK Installation</span></span>

<span data-ttu-id="07c4d-201">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di.NET Core CLI][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="07c4d-201">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="07c4d-202">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="07c4d-202">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

### <a name="code-example"></a><span data-ttu-id="07c4d-203">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="07c4d-203">Code Example</span></span>

<span data-ttu-id="07c4d-204">Questo esempio mostra l'esecuzione di un processo Hive in un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="07c4d-204">This example runs a Hive job in a Hadoop cluster.</span></span>

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

### <a name="samples"></a><span data-ttu-id="07c4d-205">Esempi</span><span class="sxs-lookup"><span data-stu-id="07c4d-205">Samples</span></span>

- [<span data-ttu-id="07c4d-206">Eseguire processi Hive</span><span class="sxs-lookup"><span data-stu-id="07c4d-206">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="07c4d-207">Eseguire processi Pig</span><span class="sxs-lookup"><span data-stu-id="07c4d-207">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="07c4d-208">Altri processi</span><span class="sxs-lookup"><span data-stu-id="07c4d-208">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)
