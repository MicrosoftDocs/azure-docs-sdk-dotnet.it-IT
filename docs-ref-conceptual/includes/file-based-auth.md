---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 7f7c24957d2bc0574fc0b1bf2a8ae8fe8b4dfc64
ms.sourcegitcommit: 70982e900bd4adfbc121eba55d94544f17c6b495
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2018
ms.locfileid: "51196047"
---
<span data-ttu-id="d91c0-101">Creare un file di testo denominato `azureauth.json`.</span><span class="sxs-lookup"><span data-stu-id="d91c0-101">Create a text file named `azureauth.json`.</span></span> <span data-ttu-id="d91c0-102">Incollare l'output JSON ottenuto con la creazione dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="d91c0-102">Paste the JSON output from when you created the service principal.</span></span>

<span data-ttu-id="d91c0-103">Salvare questo file nel sistema in una posizione sicura e leggibile dal codice.</span><span class="sxs-lookup"><span data-stu-id="d91c0-103">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="d91c0-104">Usare PowerShell per impostare una variabile di ambiente denominata `AZURE_AUTH_LOCATION` con il percorso completo del file, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d91c0-104">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
