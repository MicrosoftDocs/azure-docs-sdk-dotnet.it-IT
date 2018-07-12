---
title: Concetti e modelli di utilizzo delle librerie di gestione di Azure per .NET
description: ''
keywords: Azure, .NET, SDK, API, modelli, concetti, Fluent, registrazione
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: b817216e114e5ab3ff22c1c5adb0f892c7874147
ms.sourcegitcommit: 1c2e1fd031ad012d6888fcde3cd325f7e8e49e0f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2018
ms.locfileid: "29752863"
---
# <a name="azure-management-library-for-net-fluent-concepts"></a><span data-ttu-id="8a626-103">Concetti relativi alla libreria di gestione per .NET Fluent</span><span class="sxs-lookup"><span data-stu-id="8a626-103">Azure management library for .NET fluent concepts</span></span>

<span data-ttu-id="8a626-104">Questo articolo fornisce informazioni su come usare efficacemente l'interfaccia Fluent nelle librerie di gestione di Azure per .NET.</span><span class="sxs-lookup"><span data-stu-id="8a626-104">This article will help you understand how to effectively use the fluent interface in the Azure management libraries for .NET.</span></span>

## <a name="building-resources-using-a-fluent-interface"></a><span data-ttu-id="8a626-105">Creazione di risorse tramite un'interfaccia Fluent</span><span class="sxs-lookup"><span data-stu-id="8a626-105">Building resources using a fluent interface</span></span>

<span data-ttu-id="8a626-106">Un'interfaccia Fluent è una forma specifica del modello di generatore che crea oggetti tramite una catena di metodi che impone la corretta configurazione di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="8a626-106">A fluent interface is a specific form of the builder pattern that creates objects through a method chain that enforces correct configuration of a resource.</span></span> <span data-ttu-id="8a626-107">Ad esempio, l'oggetto Azure per il punto di ingresso è creato usando un'interfaccia Fluent:</span><span class="sxs-lookup"><span data-stu-id="8a626-107">For example, the entry-point Azure object is created using a fluent interface:</span></span>

```csharp
var azure = Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

## <a name="resource-collections"></a><span data-ttu-id="8a626-108">Raccolte di risorse</span><span class="sxs-lookup"><span data-stu-id="8a626-108">Resource collections</span></span>

<span data-ttu-id="8a626-109">L'oggetto `Microsoft.Azure.Management.Fluent.Azure` mostrato sopra rappresenta il punto di ingresso per la creazione di tutte le risorse nelle librerie di gestione Fluent.</span><span class="sxs-lookup"><span data-stu-id="8a626-109">The `Microsoft.Azure.Management.Fluent.Azure` object shown above is the entry point for all resource creation in the fluent management libraries.</span></span> <span data-ttu-id="8a626-110">Selezionare i tipi di risorse da usare tramite la raccolta di risorse nell'oggetto `Azure`.</span><span class="sxs-lookup"><span data-stu-id="8a626-110">Select which type of resources to work with using the resource collections in the `Azure` object.</span></span> <span data-ttu-id="8a626-111">Ad esempio, per il database SQL:</span><span class="sxs-lookup"><span data-stu-id="8a626-111">For example, for SQL Database:</span></span>

```csharp
var sql = azure.SqlServers.Define(sqlServerName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithAdministratorLogin(administratorLogin)
    .WithAdministratorPassword(administratorPassword)
    .Create();
```

<span data-ttu-id="8a626-112">Come illustrato sopra, le "conversazioni" più Fluent instaurate con l'API iniziano con la selezione della raccolta di risorse appropriata per le risorse di Azure che è necessario usare.</span><span class="sxs-lookup"><span data-stu-id="8a626-112">As seen above, most fluent "conversations" you have with the API start with selecting the appropriate resource collection for the Azure resources you need to work with.</span></span>  <span data-ttu-id="8a626-113">L'utente viene guidato attraverso la conversazione tramite IntelliSense in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8a626-113">Intellisense in Visual Studio then guides you through the conversation.</span></span> 

![GIF della conversazione Fluent gestita da IntelliSense in Visual Studio](media/dotnet-sdk-azure-concepts/vs-fluent.gif)   

## <a name="lists-and-iterations"></a><span data-ttu-id="8a626-115">Elenchi e iterazioni</span><span class="sxs-lookup"><span data-stu-id="8a626-115">Lists and iterations</span></span>

<span data-ttu-id="8a626-116">Ogni raccolta di risorse include un metodo `List()` per restituire ogni istanza di tale risorsa nella sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="8a626-116">Every resource collection has a `List()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="8a626-117">Ad esempio, `Azure.SqlServers.List()` restituisce tutti i server SQL nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8a626-117">For example, `Azure.SqlServers.List()` returns all SQL servers in the subscription.</span></span>

<span data-ttu-id="8a626-118">Usare il metodo `ListByResourceGroup()` per definire un [gruppo di risorse di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) specifico come ambito dell'elenco restituito.</span><span class="sxs-lookup"><span data-stu-id="8a626-118">Use the `ListByResourceGroup()` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="8a626-119">Eseguire l'iterazione della raccolta restituita, in modo analogo a un oggetto `List<T>` normale:</span><span class="sxs-lookup"><span data-stu-id="8a626-119">Iterate over the returned collection just as you would a normal `List<T>`:</span></span>

```csharp
var vmList = azure.VirtualMachines.List();
foreach(var vm in vmList)
{
    Console.WriteLine("VM Name: {0}", vm.Name);
}
```   

## <a name="actionable-verbs"></a><span data-ttu-id="8a626-120">Verbi su cui è possibile eseguire azioni</span><span class="sxs-lookup"><span data-stu-id="8a626-120">Actionable verbs</span></span>

<span data-ttu-id="8a626-121">I metodi della raccolta di risorse i cui nomi includono verbi consentono di eseguire azioni immediate in Azure.</span><span class="sxs-lookup"><span data-stu-id="8a626-121">Resource collection methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="8a626-122">Questi metodi funzionano in modo sincrono e bloccano l'esecuzione nel thread corrente fino al completamento.</span><span class="sxs-lookup"><span data-stu-id="8a626-122">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="8a626-123">Verbo</span><span class="sxs-lookup"><span data-stu-id="8a626-123">Verb</span></span>   |  <span data-ttu-id="8a626-124">Esempio di utilizzo</span><span class="sxs-lookup"><span data-stu-id="8a626-124">Sample usage</span></span> |
|--------|---------------|
| <span data-ttu-id="8a626-125">Create</span><span class="sxs-lookup"><span data-stu-id="8a626-125">Create</span></span> | `azure.VirtualMachines.Create(listOfVMCreatables)` |
| <span data-ttu-id="8a626-126">Applica</span><span class="sxs-lookup"><span data-stu-id="8a626-126">Apply</span></span>  | `virtualMachineScaleSet.Update().WithCapacity(6).Apply()` |
| <span data-ttu-id="8a626-127">Delete</span><span class="sxs-lookup"><span data-stu-id="8a626-127">Delete</span></span> | `azure.Disks.DeleteById(id)` | 
| <span data-ttu-id="8a626-128">Elenco</span><span class="sxs-lookup"><span data-stu-id="8a626-128">List</span></span>   | `azure.SqlServers.List()` | 
| <span data-ttu-id="8a626-129">Get</span><span class="sxs-lookup"><span data-stu-id="8a626-129">Get</span></span>    | `var vm  = azure.VirtualMachines.GetByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="8a626-130">`Define()` e `Update()` sono verbi ma non bloccano l'esecuzione, a meno che non siano seguiti da `Create()` o `Apply()`.</span><span class="sxs-lookup"><span data-stu-id="8a626-130">`Define()` and `Update()` are verbs but do not block unless followed by a `Create()` or `Apply()`.</span></span>
 
<span data-ttu-id="8a626-131">Alcuni oggetti di risorse specifici includono verbi che consentono di modificare lo stato della risorsa in Azure.</span><span class="sxs-lookup"><span data-stu-id="8a626-131">Specific resource objects have verbs that change the state of the resource in Azure.</span></span> <span data-ttu-id="8a626-132">Ad esempio: </span><span class="sxs-lookup"><span data-stu-id="8a626-132">For example:</span></span>

```csharp
var vmToRestart = azure.VirtualMachines.GetById(id);
vmToRestart.Restart();
```

<span data-ttu-id="8a626-133">Per la maggior parte dei metodi descritti in questa sezione è disponibile anche una versione asincrona, indicata dal suffisso `Async`.</span><span class="sxs-lookup"><span data-stu-id="8a626-133">Most of the methods described in this section have an asynchronous version as well, denoted by the suffix `Async`.</span></span>

```csharp
Task restartTask = azure.VirtualMachines.GetById(id).RestartAsync();
```

## <a name="lazy-resource-creation"></a><span data-ttu-id="8a626-134">Creazione differita delle risorse</span><span class="sxs-lookup"><span data-stu-id="8a626-134">Lazy resource creation</span></span>

<span data-ttu-id="8a626-135">La creazione di risorse di Azure può presentare alcune difficoltà, ad esempio nel caso in cui una nuova risorsa dipenda da un'altra risorsa che non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="8a626-135">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="8a626-136">Un esempio di questo scenario è costituito dalla necessità di riservare un indirizzo IP pubblico e di configurare un disco quando si crea una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8a626-136">An example is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="8a626-137">Non si vuole verificare di avere riservato l'indirizzo o di avere creato il disco. Si vuole solo configurare la macchina virtuale con tali risorse.</span><span class="sxs-lookup"><span data-stu-id="8a626-137">You don't want to verify reserving the address or the creating the disk, you just want to configure the virtual machine with those resources.</span></span>

<span data-ttu-id="8a626-138">Usare oggetti generabili per definire le risorse di Azure da usare nel codice ma crearli solo quando necessario in Azure.</span><span class="sxs-lookup"><span data-stu-id="8a626-138">Use creatable objects to define Azure resources for use in your code but only create them when needed in Azure.</span></span> <span data-ttu-id="8a626-139">Il codice scritto con oggetti generabili trasferisce la creazione di risorse nell'ambiente di Azure all'API di gestione, aumentando così le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="8a626-139">Code written with creatable objects offloads resource creation in the Azure environment to the management API, boosting performance.</span></span> 

<span data-ttu-id="8a626-140">Creare gli oggetti generabili usando il verbo `Define()` della raccolta di risorse senza un verbo `Create()`:</span><span class="sxs-lookup"><span data-stu-id="8a626-140">Generate creatable objects through the resource collections' `Define()` verb without a `Create()` verb:</span></span>

```csharp
// Init a creatable Public IP Address
var publicIpAddressCreatable = azure.PublicIPAddresses.Define("publicIPAddressName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName);
```

<span data-ttu-id="8a626-141">La risorsa di Azure definita dall'oggetto generabile non esiste ancora nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8a626-141">The Azure resource defined by the creatable object does not yet exist in your subscription.</span></span> <span data-ttu-id="8a626-142">Un oggetto generabile è una rappresentazione locale di una risorsa che verrà creata dall'API di gestione al momento opportuno, ovvero quando viene chiamato il metodo `.Create()`.</span><span class="sxs-lookup"><span data-stu-id="8a626-142">A creatable object is a local representation of a resource that the management API will create when it's needed (when `.Create()` is called).</span></span> <span data-ttu-id="8a626-143">Usare questo oggetto generabile nella definizione di altre risorse di Azure che richiedono questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="8a626-143">Use this creatable object in the definition of other Azure resources that need this resource.</span></span> 

```csharp
// Init a creatable VM using the creatable Public IP Address
var vmCreatable = azure.VirtualMachines.Define("creatableVM")
    // ...
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
    // ...
```

<span data-ttu-id="8a626-144">Creare le risorse nella sottoscrizione di Azure usando il metodo `Create()` per la raccolta di risorse.</span><span class="sxs-lookup"><span data-stu-id="8a626-144">Create the resources in your Azure subscription using the `Create()` method for the resource collection.</span></span> 

```csharp
// Create the VM and its Public IP Address
var virtualMachine = azure.VirtualMachines.Create(vmCreatable);
```

<span data-ttu-id="8a626-145">Se passano gli oggetti generabili a `Create()`, viene restituito un oggetto `ICreatedResources` invece di un singolo oggetto risorsa.</span><span class="sxs-lookup"><span data-stu-id="8a626-145">Passing creatable objects to `Create()` returns a `ICreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="8a626-146">L'oggetto `CreatedRelatedResource` consente di accedere a tutte le risorse create dalla chiamata `Create()`, non solo al tipo della raccolta di risorse.</span><span class="sxs-lookup"><span data-stu-id="8a626-146">The `CreatedRelatedResource` object lets you access all resources created by the `Create()` call, not just the type from the resource collection.</span></span> <span data-ttu-id="8a626-147">Per accedere all'indirizzo IP pubblico creato in Azure per la macchina virtuale creata nell'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="8a626-147">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```csharp
var pip = virtualMachine.CreatedRelatedResource(publicIPAddressCreatable.Key()) as PublicIPAddress;;
```    

## <a name="exception-handling"></a><span data-ttu-id="8a626-148">Gestione delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="8a626-148">Exception handling</span></span>

<span data-ttu-id="8a626-149">L'API di gestione definisce classi di eccezioni che estendono `Microsoft.Rest.RestException`.</span><span class="sxs-lookup"><span data-stu-id="8a626-149">The management API defines exception classes that extend `Microsoft.Rest.RestException`.</span></span> <span data-ttu-id="8a626-150">È possibile intercettare le eccezioni generate dall'API di gestione con un blocco `catch (RestException exception)` dopo l'istruzione `try` pertinente.</span><span class="sxs-lookup"><span data-stu-id="8a626-150">Catch exceptions generated by management API, with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-tracing"></a><span data-ttu-id="8a626-151">Log e traccia</span><span class="sxs-lookup"><span data-stu-id="8a626-151">Logs and tracing</span></span>

<span data-ttu-id="8a626-152">La registrazione nelle librerie di gestione di Azure Fluent per .NET sfruttano la traccia dei client del servizio [AutoRest](https://github.com/Azure/AutoRest) sottostante.</span><span class="sxs-lookup"><span data-stu-id="8a626-152">Logging in the fluent Azure management libraries for .NET leverages the underlying [AutoRest](https://github.com/Azure/AutoRest) service client tracing.</span></span>

<span data-ttu-id="8a626-153">Creare una classe che implementi `Microsoft.Rest.IServiceClientTracingInterceptor`.</span><span class="sxs-lookup"><span data-stu-id="8a626-153">Create a class that implements `Microsoft.Rest.IServiceClientTracingInterceptor`.</span></span>  <span data-ttu-id="8a626-154">Questa classe sarà responsabile dell'intercettazione dei messaggi di log e li passerà al meccanismo di generazione in uso.</span><span class="sxs-lookup"><span data-stu-id="8a626-154">This class will be responsible for intercepting log messages and passing them to whatever logging mechanism you're using.</span></span>  <span data-ttu-id="8a626-155">In questo esempio i messaggi vengono scritti nella console, ma è anche possibile passarli a Log4Net, `Microsoft.Extensions.Logging` o qualsiasi altro framework di registrazione.</span><span class="sxs-lookup"><span data-stu-id="8a626-155">In this example, we're just writing messages to the console, but you could also pass them to Log4Net, `Microsoft.Extensions.Logging`, or any other logging framework.</span></span>

```csharp
class ConsoleTracer : IServiceClientTracingInterceptor
{
    public void Information(string message)
    {
        Console.WriteLine(message);
    }

    public void TraceError(string invocationId, Exception exception)
    {
        Console.WriteLine("Exception in {0}: {1}", invocationId, exception);
    }

    public void ReceiveResponse(string invocationId, HttpResponseMessage response) { }

    public void SendRequest(string invocationId, HttpRequestMessage request) { }

    public void Configuration(string source, string name, string value) { }

    public void EnterMethod(string invocationId, object instance, string method, IDictionary<string, object> parameters) { }

    public void ExitMethod(string invocationId, object returnValue) { }
}
```

<span data-ttu-id="8a626-156">Prima di creare l'oggetto `Microsoft.Azure.Management.Fluent.Azure`, inizializzare l'interfaccia `IServiceClientTracingInterceptor` creata in precedenza chiamando il metodo `ServiceClientTracing.AddTracingInterceptor()` e impostare `ServiceClientTracing.IsEnabled` su *true*.</span><span class="sxs-lookup"><span data-stu-id="8a626-156">Before creating the `Microsoft.Azure.Management.Fluent.Azure` object, initialize the `IServiceClientTracingInterceptor` you created above by calling `ServiceClientTracing.AddTracingInterceptor()` and set `ServiceClientTracing.IsEnabled` to *true*.</span></span>  <span data-ttu-id="8a626-157">Quando si crea l'oggetto `Azure`, includere i metodi `.WithDelegatingHandler()` e `.WithLogLevel()` per associare il client alla traccia dei client del servizio AutoRest.</span><span class="sxs-lookup"><span data-stu-id="8a626-157">When you create the `Azure` object, include the `.WithDelegatingHandler()` and `.WithLogLevel()` methods to wire up the client to AutoRest's service client tracing.</span></span>

```csharp
ServiceClientTracing.AddTracingInterceptor(new ConsoleTracer());
ServiceClientTracing.IsEnabled = true;

var azure = Azure
    .Configure()
    .WithDelegatingHandler(new HttpLoggingDelegatingHandler())
    .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

<span data-ttu-id="8a626-158">I livelli del log `HttpLoggingDelegatingHandler` sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="8a626-158">The `HttpLoggingDelegatingHandler` log levels are defined as follows:</span></span>

| <span data-ttu-id="8a626-159">Livello di traccia</span><span class="sxs-lookup"><span data-stu-id="8a626-159">Trace level</span></span> | <span data-ttu-id="8a626-160">Registrazione abilitata</span><span class="sxs-lookup"><span data-stu-id="8a626-160">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="8a626-161">HttpLoggingDelegatingHandler.Level.None</span><span class="sxs-lookup"><span data-stu-id="8a626-161">HttpLoggingDelegatingHandler.Level.None</span></span> | <span data-ttu-id="8a626-162">Nessun output</span><span class="sxs-lookup"><span data-stu-id="8a626-162">No output</span></span>
| <span data-ttu-id="8a626-163">HttpLoggingDelegatingHandler.Level.Basic</span><span class="sxs-lookup"><span data-stu-id="8a626-163">HttpLoggingDelegatingHandler.Level.Basic</span></span> | <span data-ttu-id="8a626-164">Registra gli URL delle chiamate REST sottostanti, i codici di risposta e gli orari</span><span class="sxs-lookup"><span data-stu-id="8a626-164">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="8a626-165">HttpLoggingDelegatingHandler.Level.Body</span><span class="sxs-lookup"><span data-stu-id="8a626-165">HttpLoggingDelegatingHandler.Level.Body</span></span> | <span data-ttu-id="8a626-166">Tutti gli elementi del livello Basic e i corpi di richiesta e risposta per le chiamate REST</span><span class="sxs-lookup"><span data-stu-id="8a626-166">Everything in Basic plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="8a626-167">HttpLoggingDelegatingHandler.Level.Headers</span><span class="sxs-lookup"><span data-stu-id="8a626-167">HttpLoggingDelegatingHandler.Level.Headers</span></span> | <span data-ttu-id="8a626-168">Tutti gli elementi del livello Basic e le intestazioni di richiesta e risposta per le chiamate REST</span><span class="sxs-lookup"><span data-stu-id="8a626-168">Everything in Basic plus the request and response headers REST calls</span></span>
| <span data-ttu-id="8a626-169">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span><span class="sxs-lookup"><span data-stu-id="8a626-169">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span></span> | <span data-ttu-id="8a626-170">Tutti gli elementi dei livelli di registrazione Body e Headers</span><span class="sxs-lookup"><span data-stu-id="8a626-170">Everything in both Body and Headers log level</span></span>
