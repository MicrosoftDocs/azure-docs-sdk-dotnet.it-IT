---
title: Librerie di Istanze di contenitore di Azure per .NET
description: Informazioni di riferimento per le librerie di Istanze di contenitore di Azure per .NET
keywords: Azure, .NET, SDK, API, Istanze di contenitore, Istanze di contenitore di Azure
author: mmacy
ms.author: marsma
manager: jeconnoc
ms.date: 05/25/2018
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: dcontainer-instances
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 033f67a989b0ed6cfcb67a6212c0d5c46c485afa
ms.sourcegitcommit: 4ae9f77a9300a4fe54d0179055ae61191078f207
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2018
ms.locfileid: "34567183"
---
# <a name="azure-container-instances-libraries-for-net"></a><span data-ttu-id="641c8-104">Librerie di Istanze di contenitore di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="641c8-104">Azure Container Instances libraries for .NET</span></span>

<span data-ttu-id="641c8-105">È possibile usare le librerie di Istanze di contenitore di Microsoft Azure per .NET per creare e gestire istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="641c8-105">Use the Microsoft Azure Container Instances libraries for .NET to create and manage Azure container instances.</span></span> <span data-ttu-id="641c8-106">Per altre informazioni, vedere [Panoramica di Istanze di contenitore di Azure](/azure/container-instances/container-instances-overview).</span><span class="sxs-lookup"><span data-stu-id="641c8-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="641c8-107">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="641c8-107">Management library</span></span>

<span data-ttu-id="641c8-108">È possibile usare la libreria di gestione per creare e gestire istanze di contenitore di Azure in Azure.</span><span class="sxs-lookup"><span data-stu-id="641c8-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="641c8-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="641c8-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

### <a name="visual-studio-package-manager"></a><span data-ttu-id="641c8-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="641c8-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="examples"></a><span data-ttu-id="641c8-111">Esempi</span><span class="sxs-lookup"><span data-stu-id="641c8-111">Examples</span></span>

### <a name="create-container-group---single-container"></a><span data-ttu-id="641c8-112">Creare un gruppo di contenitori - Singolo contenitore</span><span class="sxs-lookup"><span data-stu-id="641c8-112">Create container group - single container</span></span>

<span data-ttu-id="641c8-113">Questo esempio crea un gruppo di contenitori con un singolo contenitore.</span><span class="sxs-lookup"><span data-stu-id="641c8-113">This example creates a container group with a single container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

### <a name="create-container-group---multiple-containers"></a><span data-ttu-id="641c8-114">Creare un gruppo di contenitori - Più contenitori</span><span class="sxs-lookup"><span data-stu-id="641c8-114">Create container group - multiple containers</span></span>

<span data-ttu-id="641c8-115">Questo esempio crea un gruppo di contenitori con due contenitori, ovvero un contenitore di applicazioni e un contenitore collaterale.</span><span class="sxs-lookup"><span data-stu-id="641c8-115">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

### <a name="asynchronous-container-create-with-polling"></a><span data-ttu-id="641c8-116">Creazione asincrona di contenitori con polling</span><span class="sxs-lookup"><span data-stu-id="641c8-116">Asynchronous container create with polling</span></span>

<span data-ttu-id="641c8-117">Questo esempio crea un gruppo di contenitori con un singolo contenitore usando il metodo di creazione asincrona.</span><span class="sxs-lookup"><span data-stu-id="641c8-117">This example creates a container group with a single container using the async create method.</span></span> <span data-ttu-id="641c8-118">Viene quindi eseguito il polling di Azure per il gruppo di contenitori e viene restituito lo stato del gruppo di contenitori fino a lo stato non è "In esecuzione".</span><span class="sxs-lookup"><span data-stu-id="641c8-118">It then polls Azure for the container group, and outputs the container group's status until its state is "Running."</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

### <a name="create-task-based-container-group"></a><span data-ttu-id="641c8-119">Creare un gruppo di contenitori basato su attività</span><span class="sxs-lookup"><span data-stu-id="641c8-119">Create task-based container group</span></span>

<span data-ttu-id="641c8-120">Questo esempio crea un gruppo di contenitori con un singolo contenitore basato su attività.</span><span class="sxs-lookup"><span data-stu-id="641c8-120">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="641c8-121">Il contenitore viene configurato con un [criterio di riavvio](/azure/container-instances/container-instances-restart-policy) impostato su "Mai" e una [riga di comando personalizzata](/azure/container-instances/container-instances-restart-policy#command-line-override).</span><span class="sxs-lookup"><span data-stu-id="641c8-121">The container is configured with a [restart policy](/azure/container-instances/container-instances-restart-policy) of "Never" and a [custom command line](/azure/container-instances/container-instances-restart-policy#command-line-override).</span></span>

<span data-ttu-id="641c8-122">Se si vuole eseguire un singolo comando con diversi argomenti della riga di comando, ad esempio `echo FOO BAR`, è necessario fornirli come matrice di stringa al metodo `WithStartingCommandLines`.</span><span class="sxs-lookup"><span data-stu-id="641c8-122">If you want to run a single command with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string array to the `WithStartingCommandLines` method.</span></span> <span data-ttu-id="641c8-123">Ad esempio: </span><span class="sxs-lookup"><span data-stu-id="641c8-123">For example:</span></span>

`WithStartingCommandLines("echo", "FOO", "BAR")`

<span data-ttu-id="641c8-124">Se tuttavia si vogliono eseguire più comandi con (potenzialmente) più argomenti, è necessario eseguire una shell e passare i comandi concatenati come argomento.</span><span class="sxs-lookup"><span data-stu-id="641c8-124">If, however, you want to run multiple commands with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="641c8-125">Il codice seguente, ad esempio, esegue i comandi `echo` e `tail`:</span><span class="sxs-lookup"><span data-stu-id="641c8-125">For example, this executes both an `echo` and a `tail` command:</span></span>

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

### <a name="list-container-groups"></a><span data-ttu-id="641c8-126">Elencare gruppi di contenitori</span><span class="sxs-lookup"><span data-stu-id="641c8-126">List container groups</span></span>

<span data-ttu-id="641c8-127">Questo esempio elenca i gruppi di contenitori in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="641c8-127">This example lists the container groups in a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

### <a name="get-an-existing-container-group"></a><span data-ttu-id="641c8-128">Ottenere un gruppo di contenitori esistente</span><span class="sxs-lookup"><span data-stu-id="641c8-128">Get an existing container group</span></span>

<span data-ttu-id="641c8-129">Questo esempio ottiene un gruppo di contenitori specifico che si trova in un gruppo di risorse e quindi stampa alcune proprietà e i rispettivi valori.</span><span class="sxs-lookup"><span data-stu-id="641c8-129">This example gets a specific container group residing in a resource group and then prints a few of its properties and their values.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

### <a name="delete-a-container-group"></a><span data-ttu-id="641c8-130">Eliminare un gruppo di contenitori</span><span class="sxs-lookup"><span data-stu-id="641c8-130">Delete a container group</span></span>

<span data-ttu-id="641c8-131">Questo esempio elimina un gruppo di contenitori da un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="641c8-131">This example deletes a container group from a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a><span data-ttu-id="641c8-132">Informazioni di riferimento sulle API</span><span class="sxs-lookup"><span data-stu-id="641c8-132">API reference</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="641c8-133">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="641c8-133">Explore the management APIs</span></span>](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a><span data-ttu-id="641c8-134">Esempi</span><span class="sxs-lookup"><span data-stu-id="641c8-134">Samples</span></span>

* <span data-ttu-id="641c8-135">Il codice sorgente per gli esempi seguenti è disponibile in GitHub:</span><span class="sxs-lookup"><span data-stu-id="641c8-135">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="641c8-136">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span><span class="sxs-lookup"><span data-stu-id="641c8-136">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span></span>

* <span data-ttu-id="641c8-137">Altri esempi di codice per Istanze di contenitore di Azure:</span><span class="sxs-lookup"><span data-stu-id="641c8-137">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="641c8-138">[Esempi di codice per Azure][samples]</span><span class="sxs-lookup"><span data-stu-id="641c8-138">[Azure Code Samples][samples]</span></span>

<span data-ttu-id="641c8-139">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="641c8-139">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
