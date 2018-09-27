---
title: Librerie di Automazione di Azure per .NET
description: Informazioni di riferimento sulle librerie di Automazione di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: automation
ms.openlocfilehash: 4890faab86d1319fe802a30e3735419ac65e8d64
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190284"
---
# <a name="azure-automation-libraries-for-net"></a><span data-ttu-id="6bb85-103">Librerie di Automazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="6bb85-103">Azure Automation libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6bb85-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6bb85-104">Overview</span></span>

<span data-ttu-id="6bb85-105">Automazione di Microsoft Azure offre agli utenti la possibilità di automatizzare le attività comunemente eseguite negli ambienti cloud e aziendali.</span><span class="sxs-lookup"><span data-stu-id="6bb85-105">Microsoft Azure Automation provides a way for users to automate the tasks that are commonly performed in a cloud and enterprise environment.</span></span> 

<span data-ttu-id="6bb85-106">Per altre informazioni, vedere [Panoramica di Automazione di Azure](/azure/automation/automation-intro).</span><span class="sxs-lookup"><span data-stu-id="6bb85-106">Learn more by reading the [Azure Automation Overview](/azure/automation/automation-intro).</span></span>

## <a name="management-library"></a><span data-ttu-id="6bb85-107">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="6bb85-107">Management library</span></span>

<span data-ttu-id="6bb85-108">Utilizzo della libreria di gestione per gestire runbook e processi, nonché le impostazioni DSC (Desired State Configuration).</span><span class="sxs-lookup"><span data-stu-id="6bb85-108">Using the management library to manage runbooks and jobs and manage Desired State Configuration settings.</span></span>

<span data-ttu-id="6bb85-109">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6bb85-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6bb85-110">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="6bb85-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a><span data-ttu-id="6bb85-111">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="6bb85-111">Code Example</span></span>

<span data-ttu-id="6bb85-112">L'esempio seguente mostra come avviare un nuovo processo in base a un runbook esistente.</span><span class="sxs-lookup"><span data-stu-id="6bb85-112">The following example illustrates how to start a new job based on an existing runbook.</span></span>

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
> [<span data-ttu-id="6bb85-113">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="6bb85-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a><span data-ttu-id="6bb85-114">Esempi</span><span class="sxs-lookup"><span data-stu-id="6bb85-114">Samples</span></span>

* <span data-ttu-id="6bb85-115">[AzureBot](https://github.com/Microsoft/AzureBot) usa la libreria di automazione con [Bot Framework](https://docs.microsoft.com/bot-framework/) e [Servizi cognitivi](/cognitive-services) per migliorare la produttività degli sviluppatori in Azure</span><span class="sxs-lookup"><span data-stu-id="6bb85-115">[AzureBot](https://github.com/Microsoft/AzureBot) uses the automation library with the [Bot Framework](https://docs.microsoft.com/bot-framework/) and [Cognitive Services](/cognitive-services) to improve developer productivity on Azure</span></span>

<span data-ttu-id="6bb85-116">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="6bb85-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
