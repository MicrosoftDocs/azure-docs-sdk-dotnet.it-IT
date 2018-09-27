---
title: Librerie di Istanze di contenitore di Azure per .NET
description: Informazioni di riferimento per le librerie di Istanze di contenitore di Azure per .NET
ms.date: 06/11/2018
ms.topic: reference
ms.service: dcontainer-instances
ms.openlocfilehash: 93f537058e0ed11f51cc6cb6cece01da80559822
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190724"
---
# <a name="azure-container-instances-libraries-for-net"></a><span data-ttu-id="56865-103">Librerie di Istanze di contenitore di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="56865-103">Azure Container Instances libraries for .NET</span></span>

<span data-ttu-id="56865-104">È possibile usare le librerie di Istanze di contenitore di Microsoft Azure per .NET per creare e gestire istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="56865-104">Use the Microsoft Azure Container Instances libraries for .NET to create and manage Azure container instances.</span></span> <span data-ttu-id="56865-105">Per altre informazioni, vedere [Panoramica di Istanze di contenitore di Azure](/azure/container-instances/container-instances-overview).</span><span class="sxs-lookup"><span data-stu-id="56865-105">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="56865-106">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="56865-106">Management library</span></span>

<span data-ttu-id="56865-107">Usare la libreria di gestione per creare e gestire istanze di contenitore di Azure in Azure.</span><span class="sxs-lookup"><span data-stu-id="56865-107">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="56865-108">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="56865-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

### <a name="visual-studio-package-manager"></a><span data-ttu-id="56865-109">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="56865-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="example-source"></a><span data-ttu-id="56865-110">Codice sorgente di esempio</span><span class="sxs-lookup"><span data-stu-id="56865-110">Example source</span></span>

<span data-ttu-id="56865-111">Se si preferisce visualizzarli nel contesto, gli esempi di codice riportati di seguito sono disponibili nel repository GitHub seguente:</span><span class="sxs-lookup"><span data-stu-id="56865-111">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="56865-112">Azure-Samples/aci-docs-sample-dotnet</span><span class="sxs-lookup"><span data-stu-id="56865-112">Azure-Samples/aci-docs-sample-dotnet</span></span>](https://github.com/Azure-Samples/aci-docs-sample-dotnet)

## <a name="authentication"></a><span data-ttu-id="56865-113">Authentication</span><span class="sxs-lookup"><span data-stu-id="56865-113">Authentication</span></span>

<span data-ttu-id="56865-114">Uno dei modi più semplici per autenticare i client SDK è l'[autenticazione basata su file][sdk-auth].</span><span class="sxs-lookup"><span data-stu-id="56865-114">One of the easiest ways to authenticate SDK clients is with [file-based authentication][sdk-auth].</span></span> <span data-ttu-id="56865-115">L'autenticazione basata su file analizza un file di credenziali quando si creano istanze dell'oggetto client [IAzure][iazure], che quindi usa tali credenziali per l'autenticazione con Azure.</span><span class="sxs-lookup"><span data-stu-id="56865-115">File-based authentication parses a credentials file when instantiating the [IAzure][iazure] client object, which then uses those credentials when authenticating with Azure.</span></span> <span data-ttu-id="56865-116">Per usare l'autenticazione basata su file:</span><span class="sxs-lookup"><span data-stu-id="56865-116">To use file-based authentication:</span></span>

1. <span data-ttu-id="56865-117">Creare un file delle credenziali con l'[interfaccia della riga di comando di Azure](/cli/azure) o [Cloud Shell](https://shell.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="56865-117">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="56865-118">Se si usa [Cloud Shell](https://shell.azure.com/) per generare il file delle credenziali, copiarne il contenuto in un file locale a cui l'applicazione .NET può accedere.</span><span class="sxs-lookup"><span data-stu-id="56865-118">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your .NET application can access.</span></span>

2. <span data-ttu-id="56865-119">Impostare la variabile di ambiente `AZURE_AUTH_LOCATION` sul percorso completo del file delle credenziali generato.</span><span class="sxs-lookup"><span data-stu-id="56865-119">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="56865-120">Ad esempio (nella shell di Bash):</span><span class="sxs-lookup"><span data-stu-id="56865-120">For example (in the Bash shell):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="56865-121">Dopo aver creato il file delle credenziali e popolato la variabile di ambiente `AZURE_AUTH_LOCATION`, usare il metodo [Azure.Authenticate][iazure-authenticate] per inizializzare l'oggetto client [IAzure][iazure].</span><span class="sxs-lookup"><span data-stu-id="56865-121">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the [Azure.Authenticate][iazure-authenticate] method to initialize the [IAzure][iazure] client object.</span></span> <span data-ttu-id="56865-122">Il progetto di esempio ottiene prima il valore `AZURE_AUTH_LOCATION`, quindi chiama un metodo che restituisce un oggetto client `IAzure` inizializzato:</span><span class="sxs-lookup"><span data-stu-id="56865-122">The example project first obtains the `AZURE_AUTH_LOCATION` value, then calls a method that returns an initialized `IAzure` client object:</span></span>

<span data-ttu-id="56865-123"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]</span><span class="sxs-lookup"><span data-stu-id="56865-123"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]</span></span>

<span data-ttu-id="56865-124">Questo metodo dell'applicazione di esempio restituisce l'istanza di [IAzure][iazure] inizializzata, che viene quindi passata come primo parametro a tutti gli altri metodi dell'esempio:</span><span class="sxs-lookup"><span data-stu-id="56865-124">This method from the sample application returns the initialized [IAzure][iazure] instance, which is then passed as the first parameter to all other methods in the sample:</span></span>

<span data-ttu-id="56865-125"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]</span><span class="sxs-lookup"><span data-stu-id="56865-125"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]</span></span>

<span data-ttu-id="56865-126">Per altri dettagli sui metodi di autenticazione disponibili nelle librerie di gestione .NET per Azure, vedere [Authentication in Azure Management Libraries for .NET][sdk-auth] (Eseguire l'autenticazione con le librerie di gestione di Azure per .NET).</span><span class="sxs-lookup"><span data-stu-id="56865-126">For more details about the available authentication methods in the .NET management libraries for Azure, see [Authentication in Azure Management Libraries for .NET][sdk-auth].</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="56865-127">Creare un gruppo di contenitori: singolo contenitore</span><span class="sxs-lookup"><span data-stu-id="56865-127">Create container group - single container</span></span>

<span data-ttu-id="56865-128">Questo esempio crea un gruppo di contenitori con un singolo contenitore.</span><span class="sxs-lookup"><span data-stu-id="56865-128">This example creates a container group with a single container.</span></span>

<span data-ttu-id="56865-129"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]</span><span class="sxs-lookup"><span data-stu-id="56865-129"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]</span></span>

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="56865-130">Creare un gruppo di contenitori: più contenitori</span><span class="sxs-lookup"><span data-stu-id="56865-130">Create container group - multiple containers</span></span>

<span data-ttu-id="56865-131">Questo esempio crea un gruppo di contenitori con due contenitori: un contenitore di applicazioni e un contenitore collaterale.</span><span class="sxs-lookup"><span data-stu-id="56865-131">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<span data-ttu-id="56865-132"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]</span><span class="sxs-lookup"><span data-stu-id="56865-132"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]</span></span>

## <a name="asynchronous-container-create-with-polling"></a><span data-ttu-id="56865-133">Creazione asincrona di contenitori con polling</span><span class="sxs-lookup"><span data-stu-id="56865-133">Asynchronous container create with polling</span></span>

<span data-ttu-id="56865-134">Questo esempio crea un gruppo di contenitori con un singolo contenitore usando il metodo di creazione asincrona.</span><span class="sxs-lookup"><span data-stu-id="56865-134">This example creates a container group with a single container using the async create method.</span></span> <span data-ttu-id="56865-135">Viene quindi eseguito il polling di Azure per il gruppo di contenitori e viene restituito lo stato del gruppo di contenitori fino a lo stato non è "In esecuzione".</span><span class="sxs-lookup"><span data-stu-id="56865-135">It then polls Azure for the container group, and outputs the container group's status until its state is "Running."</span></span>

<span data-ttu-id="56865-136"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]</span><span class="sxs-lookup"><span data-stu-id="56865-136"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]</span></span>

## <a name="create-task-based-container-group"></a><span data-ttu-id="56865-137">Creare un gruppo di contenitori basato su attività</span><span class="sxs-lookup"><span data-stu-id="56865-137">Create task-based container group</span></span>

<span data-ttu-id="56865-138">Questo esempio crea un gruppo di contenitori con un singolo contenitore basato su attività.</span><span class="sxs-lookup"><span data-stu-id="56865-138">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="56865-139">Il contenitore viene configurato con un [criterio di riavvio](/azure/container-instances/container-instances-restart-policy) impostato su "Mai" e una [riga di comando personalizzata](/azure/container-instances/container-instances-restart-policy#command-line-override).</span><span class="sxs-lookup"><span data-stu-id="56865-139">The container is configured with a [restart policy](/azure/container-instances/container-instances-restart-policy) of "Never" and a [custom command line](/azure/container-instances/container-instances-restart-policy#command-line-override).</span></span>

<span data-ttu-id="56865-140">Se si vuole eseguire un singolo comando con diversi argomenti della riga di comando, ad esempio `echo FOO BAR`, è necessario fornirli come matrice di stringa al metodo `WithStartingCommandLines`.</span><span class="sxs-lookup"><span data-stu-id="56865-140">If you want to run a single command with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string array to the `WithStartingCommandLines` method.</span></span> <span data-ttu-id="56865-141">Ad esempio: </span><span class="sxs-lookup"><span data-stu-id="56865-141">For example:</span></span>

`WithStartingCommandLines("echo", "FOO", "BAR")`

<span data-ttu-id="56865-142">Se tuttavia si vogliono eseguire più comandi con (potenzialmente) più argomenti, è necessario eseguire una shell e passare i comandi concatenati come argomento.</span><span class="sxs-lookup"><span data-stu-id="56865-142">If, however, you want to run multiple commands with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="56865-143">Questo codice, ad esempio, esegue i comandi `echo` e `tail`:</span><span class="sxs-lookup"><span data-stu-id="56865-143">For example, this executes both an `echo` and a `tail` command:</span></span>

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<span data-ttu-id="56865-144"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]</span><span class="sxs-lookup"><span data-stu-id="56865-144"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]</span></span>

## <a name="list-container-groups"></a><span data-ttu-id="56865-145">Elencare i gruppi di contenitori</span><span class="sxs-lookup"><span data-stu-id="56865-145">List container groups</span></span>

<span data-ttu-id="56865-146">Questo esempio elenca i gruppi di contenitori in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="56865-146">This example lists the container groups in a resource group.</span></span>

<span data-ttu-id="56865-147"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]</span><span class="sxs-lookup"><span data-stu-id="56865-147"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]</span></span>

## <a name="get-an-existing-container-group"></a><span data-ttu-id="56865-148">Ottenere un gruppo di contenitori esistente</span><span class="sxs-lookup"><span data-stu-id="56865-148">Get an existing container group</span></span>

<span data-ttu-id="56865-149">Questo esempio ottiene un gruppo di contenitori specifico che si trova in un gruppo di risorse e quindi stampa alcune proprietà e i rispettivi valori.</span><span class="sxs-lookup"><span data-stu-id="56865-149">This example gets a specific container group residing in a resource group and then prints a few of its properties and their values.</span></span>

<span data-ttu-id="56865-150"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]</span><span class="sxs-lookup"><span data-stu-id="56865-150"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]</span></span>

## <a name="delete-a-container-group"></a><span data-ttu-id="56865-151">Eliminare un gruppo di contenitori</span><span class="sxs-lookup"><span data-stu-id="56865-151">Delete a container group</span></span>

<span data-ttu-id="56865-152">Questo esempio elimina un gruppo di contenitori da un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="56865-152">This example deletes a container group from a resource group.</span></span>

<span data-ttu-id="56865-153"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]</span><span class="sxs-lookup"><span data-stu-id="56865-153"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]</span></span>

## <a name="api-reference"></a><span data-ttu-id="56865-154">Informazioni di riferimento sulle API</span><span class="sxs-lookup"><span data-stu-id="56865-154">API reference</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="56865-155">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="56865-155">Explore the management APIs</span></span>](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a><span data-ttu-id="56865-156">Esempi</span><span class="sxs-lookup"><span data-stu-id="56865-156">Samples</span></span>

* <span data-ttu-id="56865-157">Il codice sorgente per gli esempi precedenti è disponibile in GitHub:</span><span class="sxs-lookup"><span data-stu-id="56865-157">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="56865-158">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span><span class="sxs-lookup"><span data-stu-id="56865-158">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span></span>

* <span data-ttu-id="56865-159">Altri esempi di codice per Istanze di contenitore di Azure:</span><span class="sxs-lookup"><span data-stu-id="56865-159">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="56865-160">[Esempi di codice per Azure][samples]</span><span class="sxs-lookup"><span data-stu-id="56865-160">[Azure Code Samples][samples]</span></span>

<span data-ttu-id="56865-161">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="56865-161">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

<!-- LINKS - External -->
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[sdk-auth]: https://github.com/Azure/azure-libraries-for-net/blob/master/AUTH.md

<!-- LINKS - Internal -->
[DotNetCLI]: /dotnet/core/tools/dotnet-add-package
[PackageManager]: /nuget/tools/package-manager-console
[iazure]: /dotnet/api/microsoft.azure.management.fluent.azure
[iazure-authenticate]: /dotnet/api/microsoft.azure.management.fluent.azure.authenticate
