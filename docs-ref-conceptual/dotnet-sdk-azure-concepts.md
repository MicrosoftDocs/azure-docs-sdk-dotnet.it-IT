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
# <a name="azure-management-library-for-net-fluent-concepts"></a>Concetti relativi alla libreria di gestione per .NET Fluent

Questo articolo fornisce informazioni su come usare efficacemente l'interfaccia Fluent nelle librerie di gestione di Azure per .NET.

## <a name="building-resources-using-a-fluent-interface"></a>Creazione di risorse tramite un'interfaccia Fluent

Un'interfaccia Fluent è una forma specifica del modello di generatore che crea oggetti tramite una catena di metodi che impone la corretta configurazione di una risorsa. Ad esempio, l'oggetto Azure per il punto di ingresso è creato usando un'interfaccia Fluent:

```csharp
var azure = Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

## <a name="resource-collections"></a>Raccolte di risorse

L'oggetto `Microsoft.Azure.Management.Fluent.Azure` mostrato sopra rappresenta il punto di ingresso per la creazione di tutte le risorse nelle librerie di gestione Fluent. Selezionare i tipi di risorse da usare tramite la raccolta di risorse nell'oggetto `Azure`. Ad esempio, per il database SQL:

```csharp
var sql = azure.SqlServers.Define(sqlServerName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithAdministratorLogin(administratorLogin)
    .WithAdministratorPassword(administratorPassword)
    .Create();
```

Come illustrato sopra, le "conversazioni" più Fluent instaurate con l'API iniziano con la selezione della raccolta di risorse appropriata per le risorse di Azure che è necessario usare.  L'utente viene guidato attraverso la conversazione tramite IntelliSense in Visual Studio. 

![GIF della conversazione Fluent gestita da IntelliSense in Visual Studio](media/dotnet-sdk-azure-concepts/vs-fluent.gif)   

## <a name="lists-and-iterations"></a>Elenchi e iterazioni

Ogni raccolta di risorse include un metodo `List()` per restituire ogni istanza di tale risorsa nella sottoscrizione corrente. Ad esempio, `Azure.SqlServers.List()` restituisce tutti i server SQL nella sottoscrizione.

Usare il metodo `ListByResourceGroup()` per definire un [gruppo di risorse di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) specifico come ambito dell'elenco restituito.  

Eseguire l'iterazione della raccolta restituita, in modo analogo a un oggetto `List<T>` normale:

```csharp
var vmList = azure.VirtualMachines.List();
foreach(var vm in vmList)
{
    Console.WriteLine("VM Name: {0}", vm.Name);
}
```   

## <a name="actionable-verbs"></a>Verbi su cui è possibile eseguire azioni

I metodi della raccolta di risorse i cui nomi includono verbi consentono di eseguire azioni immediate in Azure. Questi metodi funzionano in modo sincrono e bloccano l'esecuzione nel thread corrente fino al completamento. 

| Verbo   |  Esempio di utilizzo |
|--------|---------------|
| Create | `azure.VirtualMachines.Create(listOfVMCreatables)` |
| Applica  | `virtualMachineScaleSet.Update().WithCapacity(6).Apply()` |
| Delete | `azure.Disks.DeleteById(id)` | 
| Elenco   | `azure.SqlServers.List()` | 
| Get    | `var vm  = azure.VirtualMachines.GetByResourceGroup(group, vmName)` |

>[!NOTE]
> `Define()` e `Update()` sono verbi ma non bloccano l'esecuzione, a meno che non siano seguiti da `Create()` o `Apply()`.
 
Alcuni oggetti di risorse specifici includono verbi che consentono di modificare lo stato della risorsa in Azure. Ad esempio: 

```csharp
var vmToRestart = azure.VirtualMachines.GetById(id);
vmToRestart.Restart();
```

Per la maggior parte dei metodi descritti in questa sezione è disponibile anche una versione asincrona, indicata dal suffisso `Async`.

```csharp
Task restartTask = azure.VirtualMachines.GetById(id).RestartAsync();
```

## <a name="lazy-resource-creation"></a>Creazione differita delle risorse

La creazione di risorse di Azure può presentare alcune difficoltà, ad esempio nel caso in cui una nuova risorsa dipenda da un'altra risorsa che non esiste ancora. Un esempio di questo scenario è costituito dalla necessità di riservare un indirizzo IP pubblico e di configurare un disco quando si crea una nuova macchina virtuale. Non si vuole verificare di avere riservato l'indirizzo o di avere creato il disco. Si vuole solo configurare la macchina virtuale con tali risorse.

Usare oggetti generabili per definire le risorse di Azure da usare nel codice ma crearli solo quando necessario in Azure. Il codice scritto con oggetti generabili trasferisce la creazione di risorse nell'ambiente di Azure all'API di gestione, aumentando così le prestazioni. 

Creare gli oggetti generabili usando il verbo `Define()` della raccolta di risorse senza un verbo `Create()`:

```csharp
// Init a creatable Public IP Address
var publicIpAddressCreatable = azure.PublicIPAddresses.Define("publicIPAddressName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName);
```

La risorsa di Azure definita dall'oggetto generabile non esiste ancora nella sottoscrizione. Un oggetto generabile è una rappresentazione locale di una risorsa che verrà creata dall'API di gestione al momento opportuno, ovvero quando viene chiamato il metodo `.Create()`. Usare questo oggetto generabile nella definizione di altre risorse di Azure che richiedono questa risorsa. 

```csharp
// Init a creatable VM using the creatable Public IP Address
var vmCreatable = azure.VirtualMachines.Define("creatableVM")
    // ...
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
    // ...
```

Creare le risorse nella sottoscrizione di Azure usando il metodo `Create()` per la raccolta di risorse. 

```csharp
// Create the VM and its Public IP Address
var virtualMachine = azure.VirtualMachines.Create(vmCreatable);
```

Se passano gli oggetti generabili a `Create()`, viene restituito un oggetto `ICreatedResources` invece di un singolo oggetto risorsa.  L'oggetto `CreatedRelatedResource` consente di accedere a tutte le risorse create dalla chiamata `Create()`, non solo al tipo della raccolta di risorse. Per accedere all'indirizzo IP pubblico creato in Azure per la macchina virtuale creata nell'esempio precedente:

```csharp
var pip = virtualMachine.CreatedRelatedResource(publicIPAddressCreatable.Key()) as PublicIPAddress;;
```    

## <a name="exception-handling"></a>Gestione delle eccezioni

L'API di gestione definisce classi di eccezioni che estendono `Microsoft.Rest.RestException`. È possibile intercettare le eccezioni generate dall'API di gestione con un blocco `catch (RestException exception)` dopo l'istruzione `try` pertinente.

## <a name="logs-and-tracing"></a>Log e traccia

La registrazione nelle librerie di gestione di Azure Fluent per .NET sfruttano la traccia dei client del servizio [AutoRest](https://github.com/Azure/AutoRest) sottostante.

Creare una classe che implementi `Microsoft.Rest.IServiceClientTracingInterceptor`.  Questa classe sarà responsabile dell'intercettazione dei messaggi di log e li passerà al meccanismo di generazione in uso.  In questo esempio i messaggi vengono scritti nella console, ma è anche possibile passarli a Log4Net, `Microsoft.Extensions.Logging` o qualsiasi altro framework di registrazione.

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

Prima di creare l'oggetto `Microsoft.Azure.Management.Fluent.Azure`, inizializzare l'interfaccia `IServiceClientTracingInterceptor` creata in precedenza chiamando il metodo `ServiceClientTracing.AddTracingInterceptor()` e impostare `ServiceClientTracing.IsEnabled` su *true*.  Quando si crea l'oggetto `Azure`, includere i metodi `.WithDelegatingHandler()` e `.WithLogLevel()` per associare il client alla traccia dei client del servizio AutoRest.

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

I livelli del log `HttpLoggingDelegatingHandler` sono definiti come segue:

| Livello di traccia | Registrazione abilitata 
| ------------ | ---------------
| HttpLoggingDelegatingHandler.Level.None | Nessun output
| HttpLoggingDelegatingHandler.Level.Basic | Registra gli URL delle chiamate REST sottostanti, i codici di risposta e gli orari
| HttpLoggingDelegatingHandler.Level.Body | Tutti gli elementi del livello Basic e i corpi di richiesta e risposta per le chiamate REST
| HttpLoggingDelegatingHandler.Level.Headers | Tutti gli elementi del livello Basic e le intestazioni di richiesta e risposta per le chiamate REST
| HttpLoggingDelegatingHandler.Level.BodyAndHeaders | Tutti gli elementi dei livelli di registrazione Body e Headers
