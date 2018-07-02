---
title: Librerie di Servizi di ripristino di Azure e di Backup per .NET
description: Informazioni di riferimento sulle librerie di Servizi di ripristino di Azure e di Backup per .NET
keywords: Azure, .NET, SDK, API, Servizi di ripristino, Backup
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: recovery-services
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 6186411b668d0950328b49bb826e5b05c5ee0304
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065431"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a><span data-ttu-id="595cf-104">Librerie di Servizi di ripristino di Azure e di Backup per .NET</span><span class="sxs-lookup"><span data-stu-id="595cf-104">Azure Recovery Services and Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="595cf-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="595cf-105">Overview</span></span>

<span data-ttu-id="595cf-106">Servizi di ripristino di Azure è una famiglia di servizi per il ripristino dei dati che include [Backup di Azure](/azure/backup/) e [Azure Site Recovery](/azure/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="595cf-106">Azure Recovery Services is a suite of services for data recovery, including [Azure Backup](/azure/backup/) and [Azure Site Recovery](/azure/site-recovery/).</span></span>

## <a name="management-library"></a><span data-ttu-id="595cf-107">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="595cf-107">Management library</span></span>

<span data-ttu-id="595cf-108">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="595cf-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="595cf-109">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="595cf-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a><span data-ttu-id="595cf-110">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="595cf-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="595cf-111">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="595cf-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a><span data-ttu-id="595cf-112">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="595cf-112">Code Example</span></span>

<span data-ttu-id="595cf-113">L'esempio di codice seguente usa la libreria di gestione per attivare un backup.</span><span class="sxs-lookup"><span data-stu-id="595cf-113">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
