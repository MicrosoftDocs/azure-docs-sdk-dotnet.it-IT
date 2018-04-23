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
---
# <a name="deploy-to-azure-from-the-command-line-with-net-core"></a>Distribuire in Azure dalla riga di comando con .NET Core

Questa esercitazione illustrerà in modo dettagliato la creazione e la distribuzione di un'applicazione di Microsoft Azure con .NET Core.  Al termine, sarà disponibile un'applicazione di tipo "elenco attività" basata sul Web, compilata in ASP.NET MVC Core, ospitata come app Web di Azure e con Azure Cosmos DB per l'archiviazione dei dati.

## <a name="prerequisites"></a>prerequisiti

* Una [sottoscrizione di Microsoft Azure](https://azure.microsoft.com/free/).
* [.NET Core](https://www.microsoft.com/net/download/core) (facoltativo)
* [Interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) (facoltativo)
* Client della riga di comando [Git](https://www.git-scm.com/) (facoltativo)

In [Azure Cloud Shell](/azure/cloud-shell/) sono preinstallati tutti i prerequisiti facoltativi per questa esercitazione.  È necessario installare i componenti facoltativi indicati solo se si vuole eseguire l'esercitazione in locale.  Per avviare rapidamente Cloud Shell, fare clic sul pulsante **Prova** in alto a destra nei blocchi di codice seguenti.

## <a name="create-an-azure-cosmos-db-account"></a>Creare un account Azure Cosmos DB

Azure Cosmos DB viene usato per l'archiviazione dei dati in questa esercitazione, quindi sarà necessario creare un account.  Eseguire questo script localmente o in Cloud Shell per creare un account per l'API SQL Azure Cosmos DB.

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

## <a name="download-and-configure-the-application"></a>Scaricare e configurare l'applicazione

L'applicazione da distribuire è una [semplice app di tipo "elenco attività"](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) scritta in ASP.NET MVC Core con le librerie client di Azure Cosmos DB.  Verrà ora reso disponibile il codice per l'esercitazione, che verrà configurato con le informazioni specifiche per Azure Cosmos DB.

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
> Se non è mai stato eseguito `git commit` in questo ambiente, è possibile che venga richiesta la configurazione della propria identità. Seguire le istruzioni visualizzate sullo schermo e quindi eseguire di nuovo il comando `git commit`.

Ripristinare i pacchetti NuGet e compilare l'applicazione.

```azurecli-interactive
dotnet restore
dotnet build
```

> [!TIP]
> Se si usano gli strumenti nel proprio computer, è possibile testare l'applicazione eseguendo `dotnet run` e passando all'indirizzo `localhost` visualizzato.  Non è tuttavia possibile passare a questo indirizzo in Cloud Shell.  

## <a name="configure-azure-app-service-and-deploy-the-web-app"></a>Configurare il Servizio app di Azure e distribuire l'app Web

L'applicazione Web è stata scaricata e compilata e si è pronti per distribuirla come app Web di Azure.  Creare prima di tutto la risorsa app Web.

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=todoApp$randomNum

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname

```

Prima della distribuzione è necessario configurare le credenziali di distribuzione a livello di account.  Usare lo script seguente, assicurandosi di includere i propri valori per nome utente e password.

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

Distribuire infine l'applicazione in Azure.  Verrà richiesto di specificare la password creata in precedenza.

```azurecli-interactive
# Get the Git deployment URL
giturl=$(az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv)

# Add the URL as a Git remote repository
git remote add azure $giturl

# Push the local repository to the remote
git push azure master
```

L'applicazione verrà compilata in remoto e distribuita.  Testare l'applicazione passando a `https://<web app name>.azurewebsites.net`.  Per visualizzare l'indirizzo nella console, usare il codice seguente:

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

È possibile aggiungere nuovi elementi all'elenco di attività facendo clic su **Crea nuovo**.

![App completata](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a>Eseguire la pulizia

Al termine del test dell'app e della verifica del codice e delle risorse, è possibile eliminare l'app Web e l'account Azure Cosmos DB tramite l'eliminazione del gruppo di risorse.

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a>Passaggi successivi

* [Usare Azure Active Directory per l'autenticazione in un'applicazione Web ASP.NET](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [Creare un'app Web di Azure usando il database SQL di Azure](/azure/app-service-web/web-sites-dotnet-get-started)
* [Try a .NET sample application with Azure Storage](/azure/storage/storage-samples-dotnet) (Provare un'applicazione .NET di esempio con Archiviazione di Azure)


