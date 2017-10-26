---
title: .NET per sviluppatori di Azure
description: .NET per sviluppatori di Azure
keywords: Azure .NET, SDK, informazioni di riferimento sulle API .NET di Azure, libreria di classi .NET di Azure
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.assetid: 
ms.openlocfilehash: eb7aa364cae9deea4ed2052eefdbd51c85379afa
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/26/2017
---
# <a name="get-started-with-net-for-azure-developers"></a>Introduzione a .NET per sviluppatori di Azure

Questa esercitazione illustrerà in modo dettagliato la creazione e la distribuzione di un'applicazione Microsoft Azure con Visual Studio e .NET.  Al termine, sarà disponibile un'applicazione di tipo "elenco attività" basata sul Web, compilata in ASP.NET MVC Core, ospitata come app Web di Azure e con Azure CosmosDB per l'archiviazione dei dati.

## <a name="prerequisites"></a>Prerequisiti

* [Visual Studio 2017](https://www.visualstudio.com/downloads/)
* Una [sottoscrizione di Microsoft Azure](https://azure.microsoft.com/free/).

## <a name="create-a-cosmosdb-account"></a>Creare un account CosmosDB

CosmosDB viene usato per l'archiviazione dei dati in questa esercitazione, quindi sarà necessario creare un account.  Eseguire questo script localmente o in Cloud Shell per creare un account per l'API DocumentDB di Azure CosmosDB.  Fare clic sul pulsante **Prova** nel blocco di codice seguente per avviare [Azure Cloud Shell](/azure/cloud-shell/) e copiare/incollare il blocco di script nella shell.

```azurecli-interactive
# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Generate a unique name for the account
let randomNum=$RANDOM*$RANDOM
cosmosdbname=dotnettutorial$randomNum

# Create the CosmosDB account
az cosmosdb create --name $cosmosdbname --resource-group DotNetAzureTutorial

# Retrieve the endpoint and key (you'll need these later)
cosmosEndpoint=$(az cosmosdb show -n $cosmosdbname -g DotNetAzureTutorial --query [documentEndpoint] -o tsv)
cosmosAuthKey=$(az cosmosdb list-keys -n $cosmosdbname -g DotNetAzureTutorial --query [primaryMasterKey] -o tsv)
printf "\n\nauthKey: $cosmosAuthKey\nendpoint: $cosmosEndpoint\n\n"

# Done!

```

Prendere nota dei valori visualizzati per **authKey** ed **endpoint** 

## <a name="downloading-and-running-the-application"></a>Download ed esecuzione dell'applicazione

È necessario ottenere il codice di esempio per questa procedura dettagliata e associarlo all'account CosmosDB.

1. Scaricare il codice di esempio.  È possibile [scaricarlo da GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) oppure, se si ha il [client della riga di comando git](https://git-scm.com/), clonarlo nel computer locale con il comando seguente:

    ```cmd
    git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart
    ```

2. Aprire il file **todo.csproj** in Visual Studio.

3. Aprire **appsettings.json** nel progetto Web.  Cercare le righe seguenti:

    ```json
    "authKey": "AUTHKEYVALUE",
    "endpoint": "ENDPOINTVALUE",
    ```
    Sostituire i valori di **AUTHKEYVALUE** ed **ENDPOINTVALUE** con i valori annotati in precedenza.

4. Premere **F5** per ripristinare i pacchetti NuGet del progetto, compilare il progetto ed eseguire in locale.

L'applicazione Web verrà eseguita in locale nel browser.  È possibile aggiungere nuovi elementi all'elenco attività facendo clic su **Crea nuovo**.  I dati immessi nell'applicazione vengono archiviati nell'account CosmosDB.  È possibile [visualizzare i dati nel portale di Azure](/azure/documentdb/documentdb-view-json-document-explorer).

## <a name="deploying-the-application-as-an-azure-web-app"></a>Distribuzione dell'applicazione come app Web di Azure

È stata creata un'applicazione che usa servizi di Azure come DocumentDB.  A questo punto, l'applicazione Web verrà distribuita nel cloud.

> [!IMPORTANT]
> Assicurarsi di aver eseguito l'accesso a Visual Studio con lo stesso account a cui è associata la sottoscrizione di Azure.

1. In Visual Studio fare clic con il pulsante destro del mouse sul nome del progetto in Esplora soluzioni e scegliere **Pubblica...**

2. Nella finestra di dialogo Pubblica selezionare **Servizio app di Microsoft Azure**, quindi **Crea nuovo** e infine fare clic su **Pubblica**

3. Nella finestra di dialogo Crea servizio app immettere le informazioni seguenti:

    * Immettere un nome univoco in **Nome app Web**.  Questo nome costituirà parte dell'URL per l'app.
    * Selezionare la **Sottoscrizione** di Azure in cui verrà effettuata la distribuzione.  Usare la stessa sottoscrizione utilizzata per l'accesso a Cloud Shell in precedenza.
    * Selezionare *DotNetAzureTutorial* per il **Gruppo di risorse** dell'applicazione Web.
    * Selezionare o creare un **Piano di servizio app** per determinare il piano tariffario dell'applicazione.  Vedere qui per [altre informazioni sui Piani di servizio app](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).

4. Fare clic su **Crea** per distribuire l'applicazione.  Al termine della distribuzione, verrà visualizzata una finestra del browser con l'applicazione distribuita.

![App completata](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a>Eseguire la pulizia

Al termine del test dell'app e della verifica del codice e delle risorse, è possibile eliminare l'app Web e l'account CosmosDB tramite l'eliminazione del gruppo di risorse. in Cloud Shell.

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a>Passaggi successivi

* [Usare Azure Active Directory per l'autenticazione in un'applicazione Web ASP.NET](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [Creare un'app Web di Azure usando il database SQL di Azure](/azure/app-service-web/web-sites-dotnet-get-started)
* [Try a .NET sample application with Azure Storage](/azure/storage/storage-samples-dotnet) (Provare un'applicazione .NET di esempio con Archiviazione di Azure)


