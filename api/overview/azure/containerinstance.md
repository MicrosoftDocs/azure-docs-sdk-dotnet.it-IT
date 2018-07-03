---
title: Librerie di Istanze di contenitore di Azure per .NET
description: Informazioni di riferimento per le librerie di Istanze di contenitore di Azure per .NET
keywords: Azure, .NET, SDK, API, Istanze di contenitore, Istanze di contenitore di Azure
author: mmacy
ms.author: marsma
manager: jeconnoc
ms.date: 06/11/2018
ms.topic: reference
ms.devlang: dotnet
ms.service: dcontainer-instances
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 85fe5485c04193b336d10e8c387719e2ad1e6910
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37066145"
---
# <a name="azure-container-instances-libraries-for-net"></a><span data-ttu-id="5fe03-104">Librerie di Istanze di contenitore di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="5fe03-104">Azure Container Instances libraries for .NET</span></span>

<span data-ttu-id="5fe03-105">È possibile usare le librerie di Istanze di contenitore di Microsoft Azure per .NET per creare e gestire istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe03-105">Use the Microsoft Azure Container Instances libraries for .NET to create and manage Azure container instances.</span></span> <span data-ttu-id="5fe03-106">Per altre informazioni, vedere [Panoramica di Istanze di contenitore di Azure](/azure/container-instances/container-instances-overview).</span><span class="sxs-lookup"><span data-stu-id="5fe03-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="5fe03-107">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="5fe03-107">Management library</span></span>

<span data-ttu-id="5fe03-108">Usare la libreria di gestione per creare e gestire istanze di contenitore di Azure in Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe03-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="5fe03-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="5fe03-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

### <a name="visual-studio-package-manager"></a><span data-ttu-id="5fe03-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="5fe03-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="example-source"></a><span data-ttu-id="5fe03-111">Codice sorgente di esempio</span><span class="sxs-lookup"><span data-stu-id="5fe03-111">Example source</span></span>

<span data-ttu-id="5fe03-112">Se si preferisce visualizzarli nel contesto, gli esempi di codice riportati di seguito sono disponibili nel repository GitHub seguente:</span><span class="sxs-lookup"><span data-stu-id="5fe03-112">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="5fe03-113">Azure-Samples/aci-docs-sample-dotnet</span><span class="sxs-lookup"><span data-stu-id="5fe03-113">Azure-Samples/aci-docs-sample-dotnet</span></span>](https://github.com/Azure-Samples/aci-docs-sample-dotnet)

## <a name="authentication"></a><span data-ttu-id="5fe03-114">Authentication</span><span class="sxs-lookup"><span data-stu-id="5fe03-114">Authentication</span></span>

<span data-ttu-id="5fe03-115">Uno dei modi più semplici per autenticare i client SDK è l'[autenticazione basata su file][sdk-auth].</span><span class="sxs-lookup"><span data-stu-id="5fe03-115">One of the easiest ways to authenticate SDK clients is with [file-based authentication][sdk-auth].</span></span> <span data-ttu-id="5fe03-116">L'autenticazione basata su file analizza un file di credenziali quando si creano istanze dell'oggetto client [IAzure][iazure], che quindi usa tali credenziali per l'autenticazione con Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe03-116">File-based authentication parses a credentials file when instantiating the [IAzure][iazure] client object, which then uses those credentials when authenticating with Azure.</span></span> <span data-ttu-id="5fe03-117">Per usare l'autenticazione basata su file:</span><span class="sxs-lookup"><span data-stu-id="5fe03-117">To use file-based authentication:</span></span>

1. <span data-ttu-id="5fe03-118">Creare un file delle credenziali con l'[interfaccia della riga di comando di Azure](/cli/azure) o [Cloud Shell](https://shell.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="5fe03-118">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="5fe03-119">Se si usa [Cloud Shell](https://shell.azure.com/) per generare il file delle credenziali, copiarne il contenuto in un file locale a cui l'applicazione .NET può accedere.</span><span class="sxs-lookup"><span data-stu-id="5fe03-119">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your .NET application can access.</span></span>

2. <span data-ttu-id="5fe03-120">Impostare la variabile di ambiente `AZURE_AUTH_LOCATION` sul percorso completo del file delle credenziali generato.</span><span class="sxs-lookup"><span data-stu-id="5fe03-120">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="5fe03-121">Ad esempio (nella shell di Bash):</span><span class="sxs-lookup"><span data-stu-id="5fe03-121">For example (in the Bash shell):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="5fe03-122">Dopo aver creato il file delle credenziali e popolato la variabile di ambiente `AZURE_AUTH_LOCATION`, usare il metodo [Azure.Authenticate][iazure-authenticate] per inizializzare l'oggetto client [IAzure][iazure].</span><span class="sxs-lookup"><span data-stu-id="5fe03-122">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the [Azure.Authenticate][iazure-authenticate] method to initialize the [IAzure][iazure] client object.</span></span> <span data-ttu-id="5fe03-123">Il progetto di esempio ottiene prima il valore `AZURE_AUTH_LOCATION`, quindi chiama un metodo che restituisce un oggetto client `IAzure` inizializzato:</span><span class="sxs-lookup"><span data-stu-id="5fe03-123">The example project first obtains the `AZURE_AUTH_LOCATION` value, then calls a method that returns an initialized `IAzure` client object:</span></span>

<span data-ttu-id="5fe03-124"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]</span><span class="sxs-lookup"><span data-stu-id="5fe03-124"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]</span></span>

<span data-ttu-id="5fe03-125">Questo metodo dell'applicazione di esempio restituisce l'istanza di [IAzure][iazure] inizializzata, che viene quindi passata come primo parametro a tutti gli altri metodi dell'esempio:</span><span class="sxs-lookup"><span data-stu-id="5fe03-125">This method from the sample application returns the initialized [IAzure][iazure] instance, which is then passed as the first parameter to all other methods in the sample:</span></span>

<span data-ttu-id="5fe03-126"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]</span><span class="sxs-lookup"><span data-stu-id="5fe03-126"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]</span></span>

<span data-ttu-id="5fe03-127">Per altri dettagli sui metodi di autenticazione disponibili nelle librerie di gestione .NET per Azure, vedere [Authentication in Azure Management Libraries for .NET][sdk-auth] (Eseguire l'autenticazione con le librerie di gestione di Azure per .NET).</span><span class="sxs-lookup"><span data-stu-id="5fe03-127">For more details about the available authentication methods in the .NET management libraries for Azure, see [Authentication in Azure Management Libraries for .NET][sdk-auth].</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="5fe03-128">Creare un gruppo di contenitori: singolo contenitore</span><span class="sxs-lookup"><span data-stu-id="5fe03-128">Create container group - single container</span></span>

<span data-ttu-id="5fe03-129">Questo esempio crea un gruppo di contenitori con un singolo contenitore.</span><span class="sxs-lookup"><span data-stu-id="5fe03-129">This example creates a container group with a single container.</span></span>

<span data-ttu-id="5fe03-130"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]</span><span class="sxs-lookup"><span data-stu-id="5fe03-130"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]</span></span>

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="5fe03-131">Creare un gruppo di contenitori: più contenitori</span><span class="sxs-lookup"><span data-stu-id="5fe03-131">Create container group - multiple containers</span></span>

<span data-ttu-id="5fe03-132">Questo esempio crea un gruppo di contenitori con due contenitori: un contenitore di applicazioni e un contenitore collaterale.</span><span class="sxs-lookup"><span data-stu-id="5fe03-132">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<span data-ttu-id="5fe03-133"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]</span><span class="sxs-lookup"><span data-stu-id="5fe03-133"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]</span></span>

## <a name="asynchronous-container-create-with-polling"></a><span data-ttu-id="5fe03-134">Creazione asincrona di contenitori con polling</span><span class="sxs-lookup"><span data-stu-id="5fe03-134">Asynchronous container create with polling</span></span>

<span data-ttu-id="5fe03-135">Questo esempio crea un gruppo di contenitori con un singolo contenitore usando il metodo di creazione asincrona.</span><span class="sxs-lookup"><span data-stu-id="5fe03-135">This example creates a container group with a single container using the async create method.</span></span> <span data-ttu-id="5fe03-136">Viene quindi eseguito il polling di Azure per il gruppo di contenitori e viene restituito lo stato del gruppo di contenitori fino a lo stato non è "In esecuzione".</span><span class="sxs-lookup"><span data-stu-id="5fe03-136">It then polls Azure for the container group, and outputs the container group's status until its state is "Running."</span></span>

<span data-ttu-id="5fe03-137"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]</span><span class="sxs-lookup"><span data-stu-id="5fe03-137"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]</span></span>

## <a name="create-task-based-container-group"></a><span data-ttu-id="5fe03-138">Creare un gruppo di contenitori basato su attività</span><span class="sxs-lookup"><span data-stu-id="5fe03-138">Create task-based container group</span></span>

<span data-ttu-id="5fe03-139">Questo esempio crea un gruppo di contenitori con un singolo contenitore basato su attività.</span><span class="sxs-lookup"><span data-stu-id="5fe03-139">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="5fe03-140">Il contenitore viene configurato con un [criterio di riavvio](/azure/container-instances/container-instances-restart-policy) impostato su "Mai" e una [riga di comando personalizzata](/azure/container-instances/container-instances-restart-policy#command-line-override).</span><span class="sxs-lookup"><span data-stu-id="5fe03-140">The container is configured with a [restart policy](/azure/container-instances/container-instances-restart-policy) of "Never" and a [custom command line](/azure/container-instances/container-instances-restart-policy#command-line-override).</span></span>

<span data-ttu-id="5fe03-141">Se si vuole eseguire un singolo comando con diversi argomenti della riga di comando, ad esempio `echo FOO BAR`, è necessario fornirli come matrice di stringa al metodo `WithStartingCommandLines`.</span><span class="sxs-lookup"><span data-stu-id="5fe03-141">If you want to run a single command with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string array to the `WithStartingCommandLines` method.</span></span> <span data-ttu-id="5fe03-142">Ad esempio: </span><span class="sxs-lookup"><span data-stu-id="5fe03-142">For example:</span></span>

`WithStartingCommandLines("echo", "FOO", "BAR")`

<span data-ttu-id="5fe03-143">Se tuttavia si vogliono eseguire più comandi con (potenzialmente) più argomenti, è necessario eseguire una shell e passare i comandi concatenati come argomento.</span><span class="sxs-lookup"><span data-stu-id="5fe03-143">If, however, you want to run multiple commands with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="5fe03-144">Questo codice, ad esempio, esegue i comandi `echo` e `tail`:</span><span class="sxs-lookup"><span data-stu-id="5fe03-144">For example, this executes both an `echo` and a `tail` command:</span></span>

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<span data-ttu-id="5fe03-145"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]</span><span class="sxs-lookup"><span data-stu-id="5fe03-145"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]</span></span>

## <a name="list-container-groups"></a><span data-ttu-id="5fe03-146">Elencare i gruppi di contenitori</span><span class="sxs-lookup"><span data-stu-id="5fe03-146">List container groups</span></span>

<span data-ttu-id="5fe03-147">Questo esempio elenca i gruppi di contenitori in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5fe03-147">This example lists the container groups in a resource group.</span></span>

<span data-ttu-id="5fe03-148"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]</span><span class="sxs-lookup"><span data-stu-id="5fe03-148"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]</span></span>

## <a name="get-an-existing-container-group"></a><span data-ttu-id="5fe03-149">Ottenere un gruppo di contenitori esistente</span><span class="sxs-lookup"><span data-stu-id="5fe03-149">Get an existing container group</span></span>

<span data-ttu-id="5fe03-150">Questo esempio ottiene un gruppo di contenitori specifico che si trova in un gruppo di risorse e quindi stampa alcune proprietà e i rispettivi valori.</span><span class="sxs-lookup"><span data-stu-id="5fe03-150">This example gets a specific container group residing in a resource group and then prints a few of its properties and their values.</span></span>

<span data-ttu-id="5fe03-151"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]</span><span class="sxs-lookup"><span data-stu-id="5fe03-151"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]</span></span>

## <a name="delete-a-container-group"></a><span data-ttu-id="5fe03-152">Eliminare un gruppo di contenitori</span><span class="sxs-lookup"><span data-stu-id="5fe03-152">Delete a container group</span></span>

<span data-ttu-id="5fe03-153">Questo esempio elimina un gruppo di contenitori da un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5fe03-153">This example deletes a container group from a resource group.</span></span>

<span data-ttu-id="5fe03-154"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]</span><span class="sxs-lookup"><span data-stu-id="5fe03-154"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]</span></span>

## <a name="api-reference"></a><span data-ttu-id="5fe03-155">Informazioni di riferimento sulle API</span><span class="sxs-lookup"><span data-stu-id="5fe03-155">API reference</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5fe03-156">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="5fe03-156">Explore the management APIs</span></span>](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a><span data-ttu-id="5fe03-157">Esempi</span><span class="sxs-lookup"><span data-stu-id="5fe03-157">Samples</span></span>

* <span data-ttu-id="5fe03-158">Il codice sorgente per gli esempi precedenti è disponibile in GitHub:</span><span class="sxs-lookup"><span data-stu-id="5fe03-158">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="5fe03-159">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span><span class="sxs-lookup"><span data-stu-id="5fe03-159">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span></span>

* <span data-ttu-id="5fe03-160">Altri esempi di codice per Istanze di contenitore di Azure:</span><span class="sxs-lookup"><span data-stu-id="5fe03-160">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="5fe03-161">[Esempi di codice per Azure][samples]</span><span class="sxs-lookup"><span data-stu-id="5fe03-161">[Azure Code Samples][samples]</span></span>

<span data-ttu-id="5fe03-162">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="5fe03-162">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

<!-- LINKS - External -->
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[sdk-auth]: https://github.com/Azure/azure-libraries-for-net/blob/master/AUTH.md

<!-- LINKS - Internal -->
[DotNetCLI]: /dotnet/core/tools/dotnet-add-package
[PackageManager]: /nuget/tools/package-manager-console
[iazure]: /dotnet/api/microsoft.azure.management.fluent.azure
[iazure-authenticate]: /dotnet/api/microsoft.azure.management.fluent.azure.authenticate
