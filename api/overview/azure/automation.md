---
title: Librerie di Automazione di Azure per .NET
description: Informazioni di riferimento sulle librerie di Automazione di Azure per .NET
keywords: Azure, .NET, SDK, API, Automazione
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: automation
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2055a5e24d445468763c049c34a5055cea108688
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2017
ms.locfileid: "23486694"
---
# <a name="azure-automation-libraries-for-net"></a>Librerie di Automazione di Azure per .NET

## <a name="overview"></a>Panoramica

Automazione di Microsoft Azure offre agli utenti la possibilità di automatizzare le attività comunemente eseguite negli ambienti cloud e aziendali. 

Per altre informazioni, vedere [Panoramica di Automazione di Azure](/azure/automation/automation-intro).

## <a name="management-library"></a>Libreria di gestione

Utilizzo della libreria di gestione per gestire runbook e processi, nonché le impostazioni DSC (Desired State Configuration).

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a>Esempio di codice

L'esempio seguente mostra come avviare un nuovo processo in base a un runbook esistente.

```csharp
/*
  using Microsoft.Azure.Management.Automation;
*/
AutomationManagementClient client =
    new AutomationManagementClient(new CertificateCloudCredentials(subscriptionId, cert));

// Create job create parameters
JobCreateParameters jcParam = new JobCreateParameters
{
    Properties = new JobCreateProperties
    {
        Runbook = new RunbookAssociationProperty
        {
            Name = runbookName
        },
        Parameters = null // optional parameters here
    }
};

// create runbook job. This gives back the Job
Job job = automationManagementClient.Jobs.Create(automationAccountName, jcParam).Job;
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a>Esempi

* [AzureBot](https://github.com/Microsoft/AzureBot) usa la libreria di automazione con [Bot Framework](https://docs.microsoft.com/bot-framework/) e [Servizi cognitivi](/cognitive-services) per migliorare la produttività degli sviluppatori in Azure

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
