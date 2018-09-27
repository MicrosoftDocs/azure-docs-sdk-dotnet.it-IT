---
title: Distribuire in Azure da Visual Studio
description: Questa esercitazione illustrerà in modo dettagliato la creazione e la distribuzione di un'applicazione Microsoft Azure con Visual Studio e .NET.
ms.date: 06/20/2017
ms.openlocfilehash: a4ddaa0dbf1cd71a0de031cc89b299baa381992c
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190424"
---
# <a name="deploy-to-azure-from-visual-studio"></a><span data-ttu-id="6c4a5-103">Distribuire in Azure da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6c4a5-103">Deploy to Azure from Visual Studio</span></span>

<span data-ttu-id="6c4a5-104">Questa esercitazione illustrerà in modo dettagliato la creazione e la distribuzione di un'applicazione Microsoft Azure con Visual Studio e .NET.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-104">This tutorial will walk you through building and deploying a Microsoft Azure application using Visual Studio and .NET.</span></span>  <span data-ttu-id="6c4a5-105">Al termine, sarà disponibile un'applicazione di tipo "elenco attività" basata sul Web, compilata in ASP.NET MVC Core, ospitata come app Web di Azure e con Azure Cosmos DB per l'archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-105">When finished, you'll have a web-based to-do application built in ASP.NET MVC Core, hosted as an Azure Web App, and using Azure Cosmos DB for data storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c4a5-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6c4a5-106">Prerequisites</span></span>

* [<span data-ttu-id="6c4a5-107">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6c4a5-107">Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="6c4a5-108">Una [sottoscrizione di Microsoft Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="6c4a5-108">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="6c4a5-109">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6c4a5-109">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="6c4a5-110">Azure Cosmos DB viene usato per l'archiviazione dei dati in questa esercitazione, quindi sarà necessario creare un account.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-110">Azure Cosmos DB is used for data storage in this tutorial, so you'll need to create an account.</span></span>  <span data-ttu-id="6c4a5-111">Eseguire questo script localmente o in Cloud Shell per creare un account per l'API SQL Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-111">Run this script locally or in the Cloud Shell to create an Azure Cosmos DB SQL API account.</span></span>  <span data-ttu-id="6c4a5-112">Fare clic sul pulsante **Prova** nel blocco di codice seguente per avviare [Azure Cloud Shell](/azure/cloud-shell/) e copiare/incollare il blocco di script nella shell.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-112">Click the **Try it** button on the code block below to launch the [Azure Cloud Shell](/azure/cloud-shell/) and copy/paste the script block into the shell.</span></span>

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
printf "\n\nauthKey: $cosmosAuthKey\nendpoint: $cosmosEndpoint\n\n"

# Done!

```

<span data-ttu-id="6c4a5-113">Prendere nota dei valori visualizzati per **authKey** ed **endpoint**</span><span class="sxs-lookup"><span data-stu-id="6c4a5-113">Make a note of the displayed **authKey** and **endpoint**</span></span> 

## <a name="downloading-and-running-the-application"></a><span data-ttu-id="6c4a5-114">Download ed esecuzione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="6c4a5-114">Downloading and running the application</span></span>

<span data-ttu-id="6c4a5-115">È necessario ottenere il codice di esempio per questa procedura dettagliata e associarlo all'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-115">Let's get the sample code for this walkthrough and hook it up to your Azure Cosmos DB account.</span></span>

1. <span data-ttu-id="6c4a5-116">Scaricare il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-116">Download the sample code.</span></span>  <span data-ttu-id="6c4a5-117">È possibile [scaricarlo da GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) oppure, se si ha il [client della riga di comando git](https://git-scm.com/), clonarlo nel computer locale con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c4a5-117">You can [get it from GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/), or if you have the [git command line client](https://git-scm.com/), clone it to your local machine with the following command:</span></span>

    ```cmd
    git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart
    ```

2. <span data-ttu-id="6c4a5-118">Aprire il file **todo.csproj** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-118">Open **todo.csproj** in Visual Studio.</span></span>

3. <span data-ttu-id="6c4a5-119">Aprire **appsettings.json** nel progetto Web.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-119">Open **appsettings.json** in the web project.</span></span>  <span data-ttu-id="6c4a5-120">Cercare le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="6c4a5-120">Look for the following lines:</span></span>

    ```json
    "authKey": "AUTHKEYVALUE",
    "endpoint": "ENDPOINTVALUE",
    ```
    <span data-ttu-id="6c4a5-121">Sostituire i valori di **AUTHKEYVALUE** ed **ENDPOINTVALUE** con i valori annotati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-121">Replace **AUTHKEYVALUE** and **ENDPOINTVALUE** with the values you noted earlier.</span></span>

4. <span data-ttu-id="6c4a5-122">Premere **F5** per ripristinare i pacchetti NuGet del progetto, compilare il progetto ed eseguire in locale.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-122">Press **F5** to restore the project's NuGet packages, build the project, and run it locally.</span></span>

<span data-ttu-id="6c4a5-123">L'applicazione Web verrà eseguita in locale nel browser.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-123">The web application should run locally in your browser.</span></span>  <span data-ttu-id="6c4a5-124">È possibile aggiungere nuovi elementi all'elenco attività facendo clic su **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-124">You can add new items to the to-do list by clicking **Create New**.</span></span>  <span data-ttu-id="6c4a5-125">I dati immessi nell'applicazione vengono archiviati nell'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-125">Note the data you enter in the application is being stored in your Azure Cosmos DB account.</span></span>  <span data-ttu-id="6c4a5-126">È possibile visualizzare i dati nel [portale di Azure](https://portal.azure.com) selezionando Azure Cosmos DB dal menu a sinistra, quindi selezionando l'account e infine **Esplora dati**.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-126">You can view your data in the [Azure portal](https://portal.azure.com) by selecting Azure Cosmos DB from the left menu, selecting your account, and then selecting **Data Explorer**.</span></span>

## <a name="deploying-the-application-as-an-azure-web-app"></a><span data-ttu-id="6c4a5-127">Distribuzione dell'applicazione come app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="6c4a5-127">Deploying the application as an Azure Web App</span></span>

<span data-ttu-id="6c4a5-128">È stata compilata un'applicazione che usa servizi di Azure come Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-128">You've successfully built an application that uses Azure services like Azure Cosmos DB.</span></span>  <span data-ttu-id="6c4a5-129">A questo punto, l'applicazione Web verrà distribuita nel cloud.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-129">Next, we'll deploy our web application to the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c4a5-130">Assicurarsi di aver eseguito l'accesso a Visual Studio con lo stesso account a cui è associata la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-130">Be sure you're signed into Visual Studio with the same account your Azure subscription is associated with.</span></span>

1. <span data-ttu-id="6c4a5-131">In Visual Studio fare clic con il pulsante destro del mouse sul nome del progetto in Esplora soluzioni e scegliere **Pubblica...**</span><span class="sxs-lookup"><span data-stu-id="6c4a5-131">In Visual Studio Solution Explorer, right-click on the project name and select **Publish...**</span></span>

2. <span data-ttu-id="6c4a5-132">Nella finestra di dialogo Pubblica selezionare **Servizio app di Microsoft Azure**, quindi **Crea nuovo** e infine fare clic su **Pubblica**</span><span class="sxs-lookup"><span data-stu-id="6c4a5-132">Using the Publish dialog, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**</span></span>

3. <span data-ttu-id="6c4a5-133">Nella finestra di dialogo Crea servizio app immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6c4a5-133">Complete the Create App Service dialog as follows:</span></span>

    * <span data-ttu-id="6c4a5-134">Immettere un nome univoco in **Nome app Web**.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-134">Enter a unique **Web App Name**.</span></span>  <span data-ttu-id="6c4a5-135">Questo nome costituirà parte dell'URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-135">This will be part of the URL for your app.</span></span>
    * <span data-ttu-id="6c4a5-136">Selezionare la **Sottoscrizione** di Azure in cui verrà effettuata la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-136">Select the Azure **Subscription** you're deploying to.</span></span>  <span data-ttu-id="6c4a5-137">Usare la stessa sottoscrizione utilizzata per l'accesso a Cloud Shell in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-137">Use same subscription with which you were logged into Cloud Shell earlier.</span></span>
    * <span data-ttu-id="6c4a5-138">Selezionare *DotNetAzureTutorial* per il **Gruppo di risorse** dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-138">Select *DotNetAzureTutorial* for the **Resource Group** for your web application.</span></span>
    * <span data-ttu-id="6c4a5-139">Selezionare o creare un **Piano di servizio app** per determinare il piano tariffario dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-139">Select or create an **App Service Plan** to determine the pricing your your application.</span></span>  <span data-ttu-id="6c4a5-140">Vedere qui per [altre informazioni sui Piani di servizio app](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span><span class="sxs-lookup"><span data-stu-id="6c4a5-140">Here's [more information about App Service Plans](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span></span>

4. <span data-ttu-id="6c4a5-141">Fare clic su **Crea** per distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-141">Click **Create** to deploy the application.</span></span>  <span data-ttu-id="6c4a5-142">Al termine della distribuzione, verrà visualizzata una finestra del browser con l'applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-142">When deployment is complete, a browser will open with your deployed application.</span></span>

![App completata](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a><span data-ttu-id="6c4a5-144">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="6c4a5-144">Clean up</span></span>

<span data-ttu-id="6c4a5-145">Al termine del test dell'app e della verifica del codice e delle risorse, è possibile eliminare l'app Web e l'account Azure Cosmos DB tramite l'eliminazione del gruppo di risorse in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="6c4a5-145">When you're done testing the app and inspecting the code and resources, you can delete the Web App and Azure Cosmos DB account by deleting the resource group in the Cloud Shell.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="6c4a5-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c4a5-146">Next steps</span></span>

* [<span data-ttu-id="6c4a5-147">Usare Azure Active Directory per l'autenticazione in un'applicazione Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6c4a5-147">Use Azure Active Directory for authentication in an ASP.NET web application</span></span>](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [<span data-ttu-id="6c4a5-148">Creare un'app Web di Azure usando il database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="6c4a5-148">Build an Azure Web App using Azure SQL Database</span></span>](/azure/app-service-web/web-sites-dotnet-get-started)
* <span data-ttu-id="6c4a5-149">[Try a .NET sample application with Azure Storage](/azure/storage/storage-samples-dotnet) (Provare un'applicazione .NET di esempio con Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="6c4a5-149">[Try a .NET sample application with Azure Storage](/azure/storage/storage-samples-dotnet)</span></span>


