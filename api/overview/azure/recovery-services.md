---
title: Librerie di Servizi di ripristino di Azure e di Backup per .NET
description: Informazioni di riferimento sulle librerie di Servizi di ripristino di Azure e di Backup per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: backup
ms.openlocfilehash: c2faef5c83f28cb35158609b92f0334671161d1d
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348173"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a>Librerie di Servizi di ripristino di Azure e di Backup per .NET

## <a name="overview"></a>Panoramica

Servizi di ripristino di Azure è una famiglia di servizi per il ripristino dei dati che include [Backup di Azure](/azure/backup/) e [Azure Site Recovery](/azure/site-recovery/).

## <a name="management-library"></a>Libreria di gestione

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a>Esempio di codice

L'esempio di codice seguente usa la libreria di gestione per attivare un backup.

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
