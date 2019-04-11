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
# <a name="azure-hdinsight-net-sdk"></a>Azure HDInsight .NET SDK

## <a name="azure-hdinsight-libraries-for-net-2x"></a>Librerie di Azure HDInsight per .NET 2.X

## <a name="overview"></a>Panoramica

HDInsight .NET SDK fornisce le classi necessarie per la creazione, la configurazione, l'invio e il monitoraggio dei processi Hadoop gestiti da un servizio HDInsight di Azure. Fornisce inoltre le classi per gestire le sottoscrizioni di Azure tramite il servizio HDInsight e per configurare cluster, account di archiviazione e altri asset associati al cluster HDInsight gestiti da una sottoscrizione di Azure.

## <a name="management-libraries"></a>Librerie di gestione

### <a name="jobs"></a>Processi

Usare Azure HDInsight Client SDK per creare, gestire e monitorare i processi in un cluster Hadoop. 

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a>Esempio di codice

Questo esempio mostra l'esecuzione di un processo Hive in un cluster Hadoop.

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

### <a name="hdinsight"></a>HDInsight

Usare Azure HDInsight Management SDK per creare, gestire, avviare, arrestare e ridimensionare i cluster Hadoop.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a>Esempio di codice

Questo esempio mostra la creazione di un cluster Hadoop Linux a due nodi in HDInsight con una risorsa di archiviazione BLOB di Azure esistente.

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
> [Esplorare le API di gestione](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a>Esempi

- [Creazione del cluster](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [Gestione dei cluster](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [Eseguire processi Hive](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [Eseguire processi Pig](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [Altri processi](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

Visualizzare l'[elenco completo](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) degli esempi di codice per il database SQL di Azure.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

## <a name="hdinsight-net-management-sdk-3x-preview"></a>Anteprima di HDInsight .NET Management SDK 3.X

## <a name="overview"></a>Panoramica

HDInsight .NET SDK fornisce classi e metodi che consentono di gestire i cluster HDInsight. Include operazioni per creare, eliminare, aggiornare, elencare, ridimensionare, eseguire azioni di script, monitorare, ottenere le proprietà dei cluster di HDInsight e altro ancora.

## <a name="prerequisites"></a>Prerequisiti

* Un account Azure. Se non è disponibile, [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/free/).
* [Visual Studio](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a>Installazione dell'SDK

Dal progetto Visual Studio, aprire la console di Gestione pacchetti facendo clic su **Strumenti**, **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.

In Console di Gestione pacchetti eseguire questi comandi:

```
  Install-Package Microsoft.Azure.Management.HDInsight -Version 3.1.0-preview
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a>Authentication

L'SDK deve essere prima autenticato con la sottoscrizione di Azure.  Seguire questo esempio per creare un'entità servizio e usarla per l'autenticazione. Al termine si avrà un'istanza di un `HDInsightManagementClient` che contiene molti metodi, descritti nelle sezioni seguenti, che possono essere usati per operazioni di gestione.

> [!NOTE]
> Oltre all'esempio seguente esistono altre modalità di autenticazione che possono essere più adatte alle proprie esigenze. Tutti i metodi sono descritti qui: [Eseguire l'autenticazione con le librerie di Azure per .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)

### <a name="authentication-example-using-a-service-principal"></a>Esempio di autenticazione con un'entità servizio

Per prima cosa, accedere ad [Azure Cloud Shell](https://shell.azure.com/bash). Verificare che si stia attualmente usando la sottoscrizione in cui si vuole creare l'entità servizio. 

```azurecli-interactive
az account show
```

Le informazioni sulla sottoscrizione vengono visualizzate in formato JSON.

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

Se non si è eseguito l'accesso alla sottoscrizione corretta, selezionare quella corretta eseguendo: 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Se il provider di risorse HDInsight non è già stato registrato con un altro metodo, ad esempio creando un cluster HDInsight tramite il portale di Azure, è necessario eseguire questa operazione una volta prima di poter eseguire l'autenticazione. La registrazione può essere eseguita da [Azure Cloud Shell](https://shell.azure.com/bash) eseguendo questo comando:
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

Scegliere quindi un nome per l'entità servizio e crearla con il comando seguente:

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

Verranno visualizzate le informazioni relative all'entità servizio in formato JSON.

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
Copiare il frammento di codice seguente e compilare `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` e `SUBSCRIPTION_ID` con le stringhe JSON restituite dopo aver eseguito il comando per creare l'entità servizio.

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


## <a name="cluster-management"></a>Gestione dei cluster

> [!NOTE]
> Questa sezione presuppone che l'utente abbia già eseguito l'autenticazione e abbia creato un'istanza `HDInsightManagementClient` che ha poi archiviato in una variabile chiamata `client`. Le istruzioni per l'autenticazione e l'ottenimento di un `HDInsightManagementClient` sono disponibili nella sezione Autenticazione precedente.

### <a name="create-a-cluster"></a>Creare un cluster

Un nuovo cluster può essere creato chiamando `client.Clusters.Create()`. 

#### <a name="example"></a>Esempio

Questo esempio illustra come creare un cluster Spark con 2 nodi head e 1 nodo del ruolo di lavoro.

> [!NOTE]
> È prima necessario creare un gruppo di risorse e un account di archiviazione, come spiegato di seguito. Se sono già stati creati, è possibile ignorare questi passaggi.

##### <a name="creating-a-resource-group"></a>Creazione di un gruppo di risorse

È possibile creare un gruppo di risorse con [Azure Cloud Shell](https://shell.azure.com/bash) eseguendo
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Creazione di un account di archiviazione

È possibile creare un account di archiviazione con [Azure Cloud Shell](https://shell.azure.com/bash) eseguendo:
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Eseguire ora questo comando per ottenere la chiave per l'account di archiviazione. Questa chiave sarà necessaria per creare un cluster:
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
Il frammento di codice .NET seguente crea un cluster Spark con 2 nodi head e 1 nodo del ruolo di lavoro. Inserire le variabili vuote come spiegato nei commenti. È possibile modificare altri parametri in base alle proprie esigenze.

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

### <a name="get-cluster-details"></a>Ottenere i dettagli del cluster

Per ottenere le proprietà di un dato cluster:

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Esempio

È possibile usare `get` per verificare che il cluster sia stato creato correttamente.

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

L'output sarà simile al seguente:

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> Il valore restituito di `get`, archiviato nella variabile `myCluster`, è di tipo `Microsoft.Azure.Management.HDInsight.ModelsCluster`. Un elenco completo delle proprietà di questo oggetto è disponibile [qui](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).


### <a name="list-clusters"></a>Elencare cluster

#### <a name="list-clusters-under-the-subscription"></a>Elencare i cluster nella sottoscrizione

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a>Elencare i cluster per gruppo di risorse

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> Sia `List()` che `ListByResourceGroup()` restituiscono un oggetto `IPage<Cluster>`. Per ottenere la pagina successiva è possibile chiamare `client.Clusters.ListNext("Next Page Link")`. Questa operazione può essere ripetuta fino a quando `NextPageLink` non diventa `null`, come illustrato nell'esempio seguente.

#### <a name="example"></a>Esempio
L'esempio seguente mostra le proprietà di tutti i cluster per la sottoscrizione corrente:

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

### <a name="delete-a-cluster"></a>Eliminare un cluster

Per eliminare un cluster:

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a>Aggiornare i tag del cluster

È possibile aggiornare i tag di un dato cluster nel modo seguente:

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a>Esempio

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="resize-cluster"></a>Ridimensionare un cluster

È possibile ridimensionare il numero di nodi di ruolo di lavoro di un dato cluster specificando una nuova dimensione nel modo seguente:

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a>Monitoraggio del cluster

HDInsight Management SDK può essere usato anche per gestire il monitoraggio dei cluster tramite Operations Management Suite (OMS).

### <a name="enable-oms-monitoring"></a>Abilitare il monitoraggio di OMS

> [!NOTE]
> Per abilitare il monitoraggio di OMS è necessaria un'area di lavoro Log Analytics esistente. Se l'area non è stata ancora creata, vedere [Creare un'area di lavoro Log Analytics nel portale di Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace) per informazioni su come crearla.

Per abilitare il monitoraggio di OMS nel cluster:

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a>Visualizzare lo stato del monitoraggio di OMS

Per ottenere lo stato di OMS nel cluster:

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a>Disabilitare il monitoraggio di OMS

Per disabilitare OMS nel cluster:

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a>Azioni script

HDInsight offre un metodo di configurazione denominato "azioni script" che richiama script personalizzati per il cluster.
> [!NOTE]
> Per altre informazioni sulle azioni script, vedere [Personalizzare i cluster HDInsight basati su Linux tramite azioni script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)

### <a name="execute-script-actions"></a>Eseguire azioni script

È possibile eseguire azioni script in un dato cluster nel modo seguente:

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>Eliminare un'azione script

Per eliminare una determinata azione script persistente in un dato cluster:

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a>Elencare le azioni script persistenti

> [!NOTE]
> `ListPersistedScripts()` e `List()` restituiscono un oggetto `IPage<RuntimeScriptActionDetail>`. Per ottenere la pagina successiva è possibile chiamare `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` o `client.ScriptExecutionHistory.ListNext("Next Page Link")`. Questa operazione può essere ripetuta fino a quando `NextPageLink` non diventa `null`, come illustrato negli esempi seguenti.

Per elencare tutte le azioni script persistenti per il cluster specificato:
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Esempio

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

### <a name="list-all-scripts-execution-history"></a>Elencare la cronologia di esecuzione di tutti gli script

Per elencare la cronologia di esecuzione di tutti gli script per il cluster specificato:

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Esempio

Questo esempio visualizza tutti i dettagli di tutte le precedenti esecuzioni di script.

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
