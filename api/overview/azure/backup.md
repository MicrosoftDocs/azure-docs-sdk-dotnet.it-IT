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
# <a name="azure-backup-libraries-for-net"></a>Librerie di Backup di Azure per .NET

## <a name="overview"></a>Panoramica

Backup di Azure è il servizio cloud che consente di eseguire il backup, proteggere e ripristinare i dati.

Per altre informazioni su Backup di Azure, vedere [Informazioni su Backup di Azure](/azure/backup/backup-introduction-to-azure-backup).

## <a name="management-library"></a>Libreria di gestione

Usare la libreria di gestione di Backup per gestire i backup e configurare gli insiemi di credenziali di Servizi di ripristino.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices.Backup) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

L'esempio di codice seguente usa la libreria di gestione per attivare un backup.

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/backup/management)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
