---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 7f7c24957d2bc0574fc0b1bf2a8ae8fe8b4dfc64
ms.sourcegitcommit: e534dad2d96b72ab6a9bc4b5567508962bd7e05c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58343340"
---
Creare un file di testo denominato `azureauth.json`. Incollare l'output JSON ottenuto con la creazione dell'entità servizio.

Salvare questo file nel sistema in una posizione sicura e leggibile dal codice. Usare PowerShell per impostare una variabile di ambiente denominata `AZURE_AUTH_LOCATION` con il percorso completo del file, ad esempio:

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
