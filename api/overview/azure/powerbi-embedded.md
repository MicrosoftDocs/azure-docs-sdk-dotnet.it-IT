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
# <a name="power-bi-embedded-libraries-for-net"></a><span data-ttu-id="4d9c3-103">Librerie di Power BI Embedded per .NET</span><span class="sxs-lookup"><span data-stu-id="4d9c3-103">Power BI Embedded libraries for .NET</span></span>

<span data-ttu-id="4d9c3-104">[Power BI](https://powerbi.microsoft.com/) è un servizio di analisi business basato sul cloud che offre una visualizzazione centralizzata sui dati aziendali più strategici.</span><span class="sxs-lookup"><span data-stu-id="4d9c3-104">[Power BI](https://powerbi.microsoft.com/) is a cloud-based business analytics service that gives you a single view of your most critical business data.</span></span>

<span data-ttu-id="4d9c3-105">Per altre informazioni su come usare Power BI con .NET, vedere [Incorporamento con Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span><span class="sxs-lookup"><span data-stu-id="4d9c3-105">To learn more about using Power BI with .NET, see [Embedding with Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span></span>

## <a name="client-library"></a><span data-ttu-id="4d9c3-106">Libreria client</span><span class="sxs-lookup"><span data-stu-id="4d9c3-106">Client library</span></span>

<span data-ttu-id="4d9c3-107">Usare la libreria client per connettersi alle API Power BI e accedere e interagire con report e set di dati.</span><span class="sxs-lookup"><span data-stu-id="4d9c3-107">Use the client library to connect with Power BI APIs to access and interact with data sets and reports.</span></span>

<span data-ttu-id="4d9c3-108">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.PowerBI.Api) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d9c3-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="4d9c3-109">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="4d9c3-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a><span data-ttu-id="4d9c3-110">Esempio</span><span class="sxs-lookup"><span data-stu-id="4d9c3-110">Example</span></span>

<span data-ttu-id="4d9c3-111">L'esempio seguente mostra come recuperare e visualizzare un elenco di report e set di dati.</span><span class="sxs-lookup"><span data-stu-id="4d9c3-111">The following example retrieves and displays a list of datasets and reports.</span></span>

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
> [<span data-ttu-id="4d9c3-112">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="4d9c3-112">Explore the client APIs</span></span>](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a><span data-ttu-id="4d9c3-113">Esempi</span><span class="sxs-lookup"><span data-stu-id="4d9c3-113">Samples</span></span>

* [<span data-ttu-id="4d9c3-114">Esempi di Power BI per gli sviluppatori</span><span class="sxs-lookup"><span data-stu-id="4d9c3-114">Power BI Developer Samples</span></span>](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [<span data-ttu-id="4d9c3-115">Repository GitHub di Power BI per .NET</span><span class="sxs-lookup"><span data-stu-id="4d9c3-115">Power BI .NET GitHub repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)

<span data-ttu-id="4d9c3-116">Esplorare altro [codice .NET di esempio](https://azure.microsoft.com/resources/samples/?platform=dotnet) da usare nelle app.</span><span class="sxs-lookup"><span data-stu-id="4d9c3-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
