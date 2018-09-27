---
title: Librerie di Power BI Embedded per .NET
description: Informazioni di riferimento sulle librerie di Power BI Embedded per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: acb327b56e89522142e51016a6a9b279f995a674
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190374"
---
# <a name="power-bi-embedded-libraries-for-net"></a>Librerie di Power BI Embedded per .NET

[Power BI](https://powerbi.microsoft.com/) è un servizio di analisi business basato sul cloud che offre una visualizzazione centralizzata sui dati aziendali più strategici.

Per altre informazioni su come usare Power BI con .NET, vedere [Incorporamento con Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).

## <a name="client-library"></a>Libreria client

Usare la libreria client per connettersi alle API Power BI e accedere e interagire con report e set di dati.

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.PowerBI.Api) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio.

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a>Esempio

L'esempio seguente mostra come recuperare e visualizzare un elenco di report e set di dati.

```csharp
/* Include these'using' directive:
using Microsoft.PowerBI.Api.V2;
using Microsoft.PowerBI.Api.V2.Models;
*/
using (PowerBIClient client = new PowerBIClient(new Uri(apiUrl), tokenCredentials))
{

    Console.WriteLine("\r*** DATASETS ***\r");

    // List of datasets in a group/app workspace
    ODataResponseListDataset datasetList = client.Datasets.GetDatasetsInGroup(groupId);

    foreach(Dataset ds in datasetList.Value)
    {
        Console.WriteLine(ds.Id + " | " + ds.Name);
    }

    Console.WriteLine("\r*** REPORTS ***\r");

    // List of reports in a group/app workspace
    ODataResponseListReport reportList = client.Reports.GetReportsInGroup(groupId);

    foreach (Report rpt in reportList.Value)
    {
        Console.WriteLine(rpt.Id + " | " + rpt.Name +  " | DatasetID = " + rpt.DatasetId);
    }
}
```

> [!div class="nextstepaction"]
> [Esplorare le API client](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a>Esempi

* [Esempi di Power BI per gli sviluppatori](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [Repository GitHub di Power BI per .NET](https://github.com/Microsoft/PowerBI-CSharp)

Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
