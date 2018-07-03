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
# <a name="azure-container-instances-libraries-for-net"></a>Librerie di Istanze di contenitore di Azure per .NET

È possibile usare le librerie di Istanze di contenitore di Microsoft Azure per .NET per creare e gestire istanze di contenitore di Azure. Per altre informazioni, vedere [Panoramica di Istanze di contenitore di Azure](/azure/container-instances/container-instances-overview).

## <a name="management-library"></a>Libreria di gestione

Usare la libreria di gestione per creare e gestire istanze di contenitore di Azure in Azure.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="example-source"></a>Codice sorgente di esempio

Se si preferisce visualizzarli nel contesto, gli esempi di codice riportati di seguito sono disponibili nel repository GitHub seguente:

[Azure-Samples/aci-docs-sample-dotnet](https://github.com/Azure-Samples/aci-docs-sample-dotnet)

## <a name="authentication"></a>Authentication

Uno dei modi più semplici per autenticare i client SDK è l'[autenticazione basata su file][sdk-auth]. L'autenticazione basata su file analizza un file di credenziali quando si creano istanze dell'oggetto client [IAzure][iazure], che quindi usa tali credenziali per l'autenticazione con Azure. Per usare l'autenticazione basata su file:

1. Creare un file delle credenziali con l'[interfaccia della riga di comando di Azure](/cli/azure) o [Cloud Shell](https://shell.azure.com/):

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   Se si usa [Cloud Shell](https://shell.azure.com/) per generare il file delle credenziali, copiarne il contenuto in un file locale a cui l'applicazione .NET può accedere.

2. Impostare la variabile di ambiente `AZURE_AUTH_LOCATION` sul percorso completo del file delle credenziali generato. Ad esempio (nella shell di Bash):

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

Dopo aver creato il file delle credenziali e popolato la variabile di ambiente `AZURE_AUTH_LOCATION`, usare il metodo [Azure.Authenticate][iazure-authenticate] per inizializzare l'oggetto client [IAzure][iazure]. Il progetto di esempio ottiene prima il valore `AZURE_AUTH_LOCATION`, quindi chiama un metodo che restituisce un oggetto client `IAzure` inizializzato:

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]

Questo metodo dell'applicazione di esempio restituisce l'istanza di [IAzure][iazure] inizializzata, che viene quindi passata come primo parametro a tutti gli altri metodi dell'esempio:

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]

Per altri dettagli sui metodi di autenticazione disponibili nelle librerie di gestione .NET per Azure, vedere [Authentication in Azure Management Libraries for .NET][sdk-auth] (Eseguire l'autenticazione con le librerie di gestione di Azure per .NET).

## <a name="create-container-group---single-container"></a>Creare un gruppo di contenitori: singolo contenitore

Questo esempio crea un gruppo di contenitori con un singolo contenitore.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a>Creare un gruppo di contenitori: più contenitori

Questo esempio crea un gruppo di contenitori con due contenitori: un contenitore di applicazioni e un contenitore collaterale.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

## <a name="asynchronous-container-create-with-polling"></a>Creazione asincrona di contenitori con polling

Questo esempio crea un gruppo di contenitori con un singolo contenitore usando il metodo di creazione asincrona. Viene quindi eseguito il polling di Azure per il gruppo di contenitori e viene restituito lo stato del gruppo di contenitori fino a lo stato non è "In esecuzione".

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

## <a name="create-task-based-container-group"></a>Creare un gruppo di contenitori basato su attività

Questo esempio crea un gruppo di contenitori con un singolo contenitore basato su attività. Il contenitore viene configurato con un [criterio di riavvio](/azure/container-instances/container-instances-restart-policy) impostato su "Mai" e una [riga di comando personalizzata](/azure/container-instances/container-instances-restart-policy#command-line-override).

Se si vuole eseguire un singolo comando con diversi argomenti della riga di comando, ad esempio `echo FOO BAR`, è necessario fornirli come matrice di stringa al metodo `WithStartingCommandLines`. Ad esempio: 

`WithStartingCommandLines("echo", "FOO", "BAR")`

Se tuttavia si vogliono eseguire più comandi con (potenzialmente) più argomenti, è necessario eseguire una shell e passare i comandi concatenati come argomento. Questo codice, ad esempio, esegue i comandi `echo` e `tail`:

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

## <a name="list-container-groups"></a>Elencare i gruppi di contenitori

Questo esempio elenca i gruppi di contenitori in un gruppo di risorse.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

## <a name="get-an-existing-container-group"></a>Ottenere un gruppo di contenitori esistente

Questo esempio ottiene un gruppo di contenitori specifico che si trova in un gruppo di risorse e quindi stampa alcune proprietà e i rispettivi valori.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

## <a name="delete-a-container-group"></a>Eliminare un gruppo di contenitori

Questo esempio elimina un gruppo di contenitori da un gruppo di risorse.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a>Informazioni di riferimento sulle API

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a>Esempi

* Il codice sorgente per gli esempi precedenti è disponibile in GitHub:

  [Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]

* Altri esempi di codice per Istanze di contenitore di Azure:

  [Esempi di codice per Azure][samples]

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

<!-- LINKS - External -->
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[sdk-auth]: https://github.com/Azure/azure-libraries-for-net/blob/master/AUTH.md

<!-- LINKS - Internal -->
[DotNetCLI]: /dotnet/core/tools/dotnet-add-package
[PackageManager]: /nuget/tools/package-manager-console
[iazure]: /dotnet/api/microsoft.azure.management.fluent.azure
[iazure-authenticate]: /dotnet/api/microsoft.azure.management.fluent.azure.authenticate
