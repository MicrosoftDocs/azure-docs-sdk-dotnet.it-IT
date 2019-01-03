---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 5c8cb328802cfb94e944e4241852fb9568e8507f
ms.sourcegitcommit: e25b6ac74033f3b0a7610bf66feb654acb43054c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53430534"
---
L'applicazione .NET necessita delle autorizzazioni per la lettura e la creazione di risorse nella sottoscrizione di Azure per potere usare le librerie di gestione di Azure per .NET. Creare un'entità servizio e configurare l'app per l'esecuzione con le rispettive credenziali per concedere questo accesso. Le entità servizio consentono di creare un account non interattivo associato all'identità a cui vengono concessi solo i privilegi necessari per l'esecuzione dell'app.

Per prima cosa, accedere ad [Azure Cloud Shell](https://shell.azure.com/bash). Verificare che si stia attualmente usando la sottoscrizione in cui si vuole creare l'entità servizio. 

```azurecli-interactive
az account show
```

Verranno visualizzate le informazioni relative alla sottoscrizione.

```json
{
  "environmentName": "AzureCloud",
  "id": "15dbcfa8-4b93-4c9a-881c-6189d39f04d4",
  "isDefault": true,
  "name": "my-subscription",
  "state": "Enabled",
  "tenantId": "43413cc1-5886-4711-9804-8cfea3d1c3ee",
  "user": {
    "cloudShellID": true,
    "name": "jane@contoso.com",
    "type": "user"
  }
}
```

Se non si è eseguito l'accesso alla sottoscrizione corretta, selezionare quella corretta digitando `az account set -s <name or ID of subscription>`.

Creare l'entità servizio con il comando seguente:

```azurecli-interactive
az ad sp create-for-rbac --sdk-auth
```

Verranno visualizzate le informazioni relative all'entità servizio in formato JSON.

```json
{
  "clientId": "b52dd125-9272-4b21-9862-0be667bdf6dc",
  "clientSecret": "ebc6e170-72b2-4b6f-9de2-99410964d2d0",
  "subscriptionId": "ffa52f27-be12-4cad-b1ea-c2c241b6cceb",
  "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```

Copiare e incollare l'output JSON in un editor di testo per usarlo in seguito.
