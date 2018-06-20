---
title: Distribuire in Azure dalla riga di comando con .NET Core
description: Questo articolo descrive come distribuire un'applicazione ASP.NET Core in un servizio app di Azure tramite gli strumenti da riga di comando.
keywords: Azure .NET, SDK, informazioni di riferimento sulle API .NET di Azure, libreria di classi .NET di Azure
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.openlocfilehash: 8371c304681ff88cba6f1cc3ba0d1caef836d609
ms.sourcegitcommit: e1a0e91988bb849c75e9583a80e3e6d712083785
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2018
ms.locfileid: "31005878"
---
# <a name="deploy-to-azure-from-the-command-line-with-net-core"></a><span data-ttu-id="e10f5-104">Distribuire in Azure dalla riga di comando con .NET Core</span><span class="sxs-lookup"><span data-stu-id="e10f5-104">Deploy to Azure from the command line with .NET Core</span></span>

<span data-ttu-id="e10f5-105">Questa esercitazione illustrerà in modo dettagliato la creazione e la distribuzione di un'applicazione di Microsoft Azure con .NET Core.</span><span class="sxs-lookup"><span data-stu-id="e10f5-105">This tutorial will walk you through building and deploying a Microsoft Azure application using .NET Core.</span></span>  <span data-ttu-id="e10f5-106">Al termine, sarà disponibile un'applicazione di tipo "elenco attività" basata sul Web, compilata in ASP.NET MVC Core, ospitata come app Web di Azure e con Azure Cosmos DB per l'archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="e10f5-106">When finished, you'll have a web-based to-do application built in ASP.NET MVC Core, hosted as an Azure Web App, and using Azure Cosmos DB for data storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e10f5-107">prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e10f5-107">Prerequisites</span></span>

* <span data-ttu-id="e10f5-108">Una [sottoscrizione di Microsoft Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e10f5-108">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* <span data-ttu-id="e10f5-109">[.NET Core](https://www.microsoft.com/net/download/core) (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="e10f5-109">[.NET Core](https://www.microsoft.com/net/download/core) (optional)</span></span>
* <span data-ttu-id="e10f5-110">[Interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="e10f5-110">[Azure CLI 2.0](/cli/azure/install-az-cli2) (optional)</span></span>
* <span data-ttu-id="e10f5-111">Client della riga di comando [Git](https://www.git-scm.com/) (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="e10f5-111">[Git](https://www.git-scm.com/) command line client (optional)</span></span>

<span data-ttu-id="e10f5-112">In [Azure Cloud Shell](/azure/cloud-shell/) sono preinstallati tutti i prerequisiti facoltativi per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e10f5-112">The [Azure Cloud Shell](/azure/cloud-shell/) has all of the optional prerequisites for this tutorial preinstalled.</span></span>  <span data-ttu-id="e10f5-113">È necessario installare i componenti facoltativi indicati solo se si vuole eseguire l'esercitazione in locale.</span><span class="sxs-lookup"><span data-stu-id="e10f5-113">You only need to install the optional components above if you wish to run the tutorial locally.</span></span>  <span data-ttu-id="e10f5-114">Per avviare rapidamente Cloud Shell, fare clic sul pulsante **Prova** in alto a destra nei blocchi di codice seguenti.</span><span class="sxs-lookup"><span data-stu-id="e10f5-114">To quickly launch the Cloud Shell, just click the **Try it** button in the top-right of any of the below code blocks.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="e10f5-115">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e10f5-115">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="e10f5-116">Azure Cosmos DB viene usato per l'archiviazione dei dati in questa esercitazione, quindi sarà necessario creare un account.</span><span class="sxs-lookup"><span data-stu-id="e10f5-116">Azure Cosmos DB is used for data storage in this tutorial, so you'll need to create an account.</span></span>  <span data-ttu-id="e10f5-117">Eseguire questo script localmente o in Cloud Shell per creare un account per l'API SQL Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e10f5-117">Run this script locally or in the Cloud Shell to create an Azure Cosmos DB SQL API account.</span></span>

```azurecli-interactive
# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Generate a unique name for the account
let randomNum=$RANDOM*$RANDOM
cosmosdbname=dotnettutorial$randomNum

# Create the Azure Cosmos DB account
az cosmosdb create --name $cosmosdbname --resource-group DotNetAzureTutorial

# Retrieve the endpoint and key (you'll need these later)
cosmosEndpoint=$(az cosmosdb show -n $cosmosdbname -g DotNetAzureTutorial --query [documentEndpoint] -o tsv)
cosmosAuthKey=$(az cosmosdb list-keys -n $cosmosdbname -g DotNetAzureTutorial --query [primaryMasterKey] -o tsv)

```

## <a name="download-and-configure-the-application"></a><span data-ttu-id="e10f5-118">Scaricare e configurare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="e10f5-118">Download and configure the application</span></span>

<span data-ttu-id="e10f5-119">L'applicazione da distribuire è una [semplice app di tipo "elenco attività"](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) scritta in ASP.NET MVC Core con le librerie client di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e10f5-119">The application you're going to deploy is a [simple to-do app](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) written using ASP.NET MVC Core using the Azure Cosmos DB client libraries.</span></span>  <span data-ttu-id="e10f5-120">Verrà ora reso disponibile il codice per l'esercitazione, che verrà configurato con le informazioni specifiche per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e10f5-120">Now you'll get the code for this tutorial and configure it with your Azure Cosmos DB information.</span></span>

```azurecli-interactive
# Get the code from GitHub
git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart

# Change the working directory
cd dotnet-cosmosdb-quickstart

# Replace authKey and endpoint values in appsettings.json
sed -i "s|AUTHKEYVALUE|$cosmosAuthKey|g" appsettings.json
sed -i "s|ENDPOINTVALUE|$cosmosEndpoint|g" appsettings.json

# Now commit your changes to the local Git repository.
git commit -a -m "Modified settings"

```

> [!NOTE]
> <span data-ttu-id="e10f5-121">Se non è mai stato eseguito `git commit` in questo ambiente, è possibile che venga richiesta la configurazione della propria identità.</span><span class="sxs-lookup"><span data-stu-id="e10f5-121">If you've never run `git commit` in this environment before, you may be prompted to set your identity.</span></span> <span data-ttu-id="e10f5-122">Seguire le istruzioni visualizzate sullo schermo e quindi eseguire di nuovo il comando `git commit`.</span><span class="sxs-lookup"><span data-stu-id="e10f5-122">Follow the on-screen instructions and then re-run the `git commit` command.</span></span>

<span data-ttu-id="e10f5-123">Ripristinare i pacchetti NuGet e compilare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e10f5-123">Restore the NuGet packages and build the application.</span></span>

```azurecli-interactive
dotnet restore
dotnet build
```

> [!TIP]
> <span data-ttu-id="e10f5-124">Se si usano gli strumenti nel proprio computer, è possibile testare l'applicazione eseguendo `dotnet run` e passando all'indirizzo `localhost` visualizzato.</span><span class="sxs-lookup"><span data-stu-id="e10f5-124">If you are using the tools on your own machine, you can test the application by running `dotnet run` and browsing to the displayed `localhost` address.</span></span>  <span data-ttu-id="e10f5-125">Non è tuttavia possibile passare a questo indirizzo in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="e10f5-125">You are not able to browse to this address in the Cloud Shell, however.</span></span>  

## <a name="configure-azure-app-service-and-deploy-the-web-app"></a><span data-ttu-id="e10f5-126">Configurare il Servizio app di Azure e distribuire l'app Web</span><span class="sxs-lookup"><span data-stu-id="e10f5-126">Configure Azure App Service and deploy the web app</span></span>

<span data-ttu-id="e10f5-127">L'applicazione Web è stata scaricata e compilata e si è pronti per distribuirla come app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="e10f5-127">You've successfully downloaded and built the web application, and you're ready to deploy it as an Azure Web App.</span></span>  <span data-ttu-id="e10f5-128">Creare prima di tutto la risorsa app Web.</span><span class="sxs-lookup"><span data-stu-id="e10f5-128">You'll start by creating the Web App resource.</span></span>

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=todoApp$randomNum

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname

```

<span data-ttu-id="e10f5-129">Prima della distribuzione è necessario configurare le credenziali di distribuzione a livello di account.</span><span class="sxs-lookup"><span data-stu-id="e10f5-129">Before you deploy, you need to set the account-level deployment credentials.</span></span>  <span data-ttu-id="e10f5-130">Usare lo script seguente, assicurandosi di includere i propri valori per nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="e10f5-130">Use the script below, making sure to include your own values for the user name and password.</span></span>

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

<span data-ttu-id="e10f5-131">Distribuire infine l'applicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="e10f5-131">Finally, deploy the application to Azure.</span></span>  <span data-ttu-id="e10f5-132">Verrà richiesto di specificare la password creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e10f5-132">You will be prompted for the password you created above.</span></span>

```azurecli-interactive
# Get the Git deployment URL
giturl=$(az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv)

# Add the URL as a Git remote repository
git remote add azure $giturl

# Push the local repository to the remote
git push azure master
```

<span data-ttu-id="e10f5-133">L'applicazione verrà compilata in remoto e distribuita.</span><span class="sxs-lookup"><span data-stu-id="e10f5-133">The application will be built remotely and deployed.</span></span>  <span data-ttu-id="e10f5-134">Testare l'applicazione passando a `https://<web app name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e10f5-134">Test the application by browsing to `https://<web app name>.azurewebsites.net`.</span></span>  <span data-ttu-id="e10f5-135">Per visualizzare l'indirizzo nella console, usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e10f5-135">To display the address in the console, use the following:</span></span>

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

<span data-ttu-id="e10f5-136">È possibile aggiungere nuovi elementi all'elenco di attività facendo clic su **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="e10f5-136">You can add new items to the to-do list by clicking **Create New**.</span></span>

![App completata](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a><span data-ttu-id="e10f5-138">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="e10f5-138">Clean up</span></span>

<span data-ttu-id="e10f5-139">Al termine del test dell'app e della verifica del codice e delle risorse, è possibile eliminare l'app Web e l'account Azure Cosmos DB tramite l'eliminazione del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e10f5-139">When you're done testing the app and inspecting the code and resources, you can delete the Web App and Azure Cosmos DB account by deleting the resource group.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="e10f5-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e10f5-140">Next steps</span></span>

* [<span data-ttu-id="e10f5-141">Usare Azure Active Directory per l'autenticazione in un'applicazione Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e10f5-141">Use Azure Active Directory for authentication in an ASP.NET web application</span></span>](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [<span data-ttu-id="e10f5-142">Creare un'app Web di Azure usando il database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="e10f5-142">Build an Azure Web App using Azure SQL Database</span></span>](/azure/app-service-web/web-sites-dotnet-get-started)
* <span data-ttu-id="e10f5-143">[Try a .NET sample application with Azure Storage](/azure/storage/storage-samples-dotnet) (Provare un'applicazione .NET di esempio con Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="e10f5-143">[Try a .NET sample application with Azure Storage](/azure/storage/storage-samples-dotnet)</span></span>


