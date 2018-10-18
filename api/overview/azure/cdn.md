---
title: Librerie della rete CDN di Azure per .NET
description: Informazioni di riferimento sulle librerie della rete CDN di Azure per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: azure-cdn
ms.openlocfilehash: b06b886531510d442c415fdc483d8083b6622c8e
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348063"
---
# <a name="azure-cdn-libraries-for-net"></a>Librerie della rete CDN di Azure per .NET

## <a name="overview"></a>Panoramica

La rete per la distribuzione di contenuti (rete CDN) di Azure memorizza nella cache il contenuto Web statico in località strategiche per offrire la massima velocità effettiva per la distribuzione del contenuto agli utenti. La rete CDN offre agli sviluppatori una soluzione globale per distribuire contenuto con esigenze di larghezza di banda elevata tramite la memorizzazione di tale contenuto nella cache in nodi fisici ubicati in tutto il mondo.

Per altre informazioni sulla rete CDN di Azure, vedere [Panoramica della rete per la distribuzione di contenuti (rete CDN) di Azure](https://docs.microsoft.com/azure/cdn/cdn-overview).


## <a name="management-library"></a>Libreria di gestione

È possibile usare la libreria della rete CDN di Azure per .NET per automatizzare la creazione e la gestione di profili ed endpoint di una rete CDN. 

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a>Esempio

Questo esempio crea un nuovo profilo della rete CDN con un nuovo endpoint che fa riferimento a `www.contoso.com`.

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.Cdn.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

ICdnProfile profileDefinition = azure.CdnProfiles.Define("CdnProfileName")
    .WithRegion(Region.USCentral)
    .WithExistingResourceGroup("ResourceGroupName")
    .WithStandardVerizonSku()
    .WithNewEndpoint("www.contoso.com")
    .Create();

```

> [!div class="nextstepaction"]
> [Esplorare le API di gestione](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a>Esempi

* [Introduzione alla rete CDN - Gestire la rete CDN - in .NET](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
