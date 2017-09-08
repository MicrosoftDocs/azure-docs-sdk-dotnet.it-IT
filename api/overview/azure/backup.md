---
title: Librerie di Backup di Azure per .NET
description: Informazioni di riferimento sulle librerie di Backup di Azure per .NET
keywords: Azure, .NET, SDK, API, Backup
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/24/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 93eeaeda1860e3b7190dfb0ae917b4b85b5a3609
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-backup-libraries-for-net"></a><span data-ttu-id="93ce4-104">Librerie di Backup di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="93ce4-104">Azure Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="93ce4-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="93ce4-105">Overview</span></span>

<span data-ttu-id="93ce4-106">Backup di Azure è il servizio cloud che consente di eseguire il backup, proteggere e ripristinare i dati.</span><span class="sxs-lookup"><span data-stu-id="93ce4-106">Azure Backup is the cloud service you can use to back up, protect, and restore your data.</span></span>

<span data-ttu-id="93ce4-107">Per altre informazioni su Backup di Azure, vedere [Informazioni su Backup di Azure](/azure/backup/backup-introduction-to-azure-backup).</span><span class="sxs-lookup"><span data-stu-id="93ce4-107">Learn more about Azure Backup by reading [What is Azure Backup?](/azure/backup/backup-introduction-to-azure-backup).</span></span>

## <a name="management-library"></a><span data-ttu-id="93ce4-108">Libreria di gestione</span><span class="sxs-lookup"><span data-stu-id="93ce4-108">Management library</span></span>

<span data-ttu-id="93ce4-109">Usare la libreria di gestione di Backup per gestire i backup e configurare gli insiemi di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="93ce4-109">Use the backup management library to manage backups and set up Recovery Services vaults.</span></span>

<span data-ttu-id="93ce4-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices.Backup) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="93ce4-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices.Backup) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="93ce4-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="93ce4-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

<span data-ttu-id="93ce4-112">L'esempio di codice seguente usa la libreria di gestione per attivare un backup.</span><span class="sxs-lookup"><span data-stu-id="93ce4-112">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="93ce4-113">Esplorare le API di gestione</span><span class="sxs-lookup"><span data-stu-id="93ce4-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/backup/management)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
