---
title: Librerie di Automazione di Azure per .NET
description: Informazioni di riferimento sulle librerie di Automazione di Azure per .NET
keywords: Azure, .NET, SDK, API, Automazione
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 1e1b5a662947503ff71f3e4a9b67f20a1e2d5f87
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-automation-libraries-for-net"></a><span data-ttu-id="2ea08-104">Librerie di Automazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="2ea08-104">Azure Automation libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="2ea08-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2ea08-105">Overview</span></span>

<span data-ttu-id="2ea08-106">Automazione di Microsoft Azure offre agli utenti la possibilità di automatizzare le attività comunemente eseguite negli ambienti cloud e aziendali.</span><span class="sxs-lookup"><span data-stu-id="2ea08-106">Microsoft Azure Automation provides a way for users to automate the tasks that are commonly performed in a cloud and enterprise environment.</span></span> 

<span data-ttu-id="2ea08-107">Per altre informazioni, vedere [Panoramica di Automazione di Azure](/azure/automation/automation-intro).</span><span class="sxs-lookup"><span data-stu-id="2ea08-107">Learn more by reading the [Azure Automation Overview](/azure/automation/automation-intro).</span></span>

## <a name="management-library"></a><span data-ttu-id="2ea08-108">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="2ea08-108">Management library</span></span>

<span data-ttu-id="2ea08-109">Utilizzo della libreria di gestione per gestire runbook e processi, nonché le impostazioni DSC (Desired State Configuration).</span><span class="sxs-lookup"><span data-stu-id="2ea08-109">Using the management library to manage runbooks and jobs and manage Desired State Configuration settings.</span></span>

<span data-ttu-id="2ea08-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="2ea08-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2ea08-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="2ea08-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a><span data-ttu-id="2ea08-112">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="2ea08-112">Code Example</span></span>

<span data-ttu-id="2ea08-113">L'esempio seguente mostra come avviare un nuovo processo in base a un runbook esistente.</span><span class="sxs-lookup"><span data-stu-id="2ea08-113">The following example illustrates how to start a new job based on an existing runbook.</span></span>

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
> [<span data-ttu-id="2ea08-114">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="2ea08-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a><span data-ttu-id="2ea08-115">Esempi</span><span class="sxs-lookup"><span data-stu-id="2ea08-115">Samples</span></span>

* <span data-ttu-id="2ea08-116">[AzureBot](https://github.com/Microsoft/AzureBot) usa la libreria di automazione con [Bot Framework](https://docs.microsoft.com/bot-framework/) e [Servizi cognitivi](/cognitive-services) per migliorare la produttività degli sviluppatori in Azure</span><span class="sxs-lookup"><span data-stu-id="2ea08-116">[AzureBot](https://github.com/Microsoft/AzureBot) uses the automation library with the [Bot Framework](https://docs.microsoft.com/bot-framework/) and [Cognitive Services](/cognitive-services) to improve developer productivity on Azure</span></span>

<span data-ttu-id="2ea08-117">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="2ea08-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
