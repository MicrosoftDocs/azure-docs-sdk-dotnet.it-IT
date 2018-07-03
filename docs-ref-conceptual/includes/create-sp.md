<span data-ttu-id="1f7ee-101">L'applicazione .NET necessita delle autorizzazioni per la lettura e la creazione di risorse nella sottoscrizione di Azure per potere usare le librerie di gestione di Azure per .NET.</span><span class="sxs-lookup"><span data-stu-id="1f7ee-101">Your .NET application needs permissions to read and create resources in your Azure subscription in order to use the Azure Management Libraries for .NET.</span></span> <span data-ttu-id="1f7ee-102">Creare un'entità servizio e configurare l'app per l'esecuzione con le rispettive credenziali per concedere questo accesso.</span><span class="sxs-lookup"><span data-stu-id="1f7ee-102">Create a service principal and configure your app to run with its credentials to grant this access.</span></span> <span data-ttu-id="1f7ee-103">Le entità servizio consentono di creare un account non interattivo associato all'identità a cui vengono concessi solo i privilegi necessari per l'esecuzione dell'app.</span><span class="sxs-lookup"><span data-stu-id="1f7ee-103">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="1f7ee-104">Accedere prima di tutto ad Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1f7ee-104">First, login to Azure PowerShell:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="1f7ee-105">Annotare le informazioni visualizzate sul tenant e sulla sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="1f7ee-105">Note the information displayed about your tenant and subscription:</span></span>

```plaintext
Environment           : AzureCloud
Account               : jane@contoso.com
TenantId              : 43413cc1-5886-4711-9804-8cfea3d1c3ee
SubscriptionId        : 15dbcfa8-4b93-4c9a-881c-6189d39f04d4
SubscriptionName      : my-subscription
CurrentStorageAccount : 
```

<span data-ttu-id="1f7ee-106">[Creare un'entità servizio usando PowerShell](/powershell/azure/create-azure-service-principal-azureps), come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1f7ee-106">[Create a service principal using PowerShell](/powershell/azure/create-azure-service-principal-azureps) as shown below.</span></span> 

> [!NOTE]
> <span data-ttu-id="1f7ee-107">Se il cmdlet `New-AzureRmADServicePrincipal` seguente restituisce "Another object with the same value for property identifierUris already exists" (Esiste già un oggetto con lo stesso valore per la proprietà identifierUris), è già presente un'entità servizio con tale nome nel tenant.</span><span class="sxs-lookup"><span data-stu-id="1f7ee-107">If the `New-AzureRmADServicePrincipal` cmdlet below returns "Another object with the same value for property identifierUris already exists," there is already a service principal by that name in your tenant.</span></span> <span data-ttu-id="1f7ee-108">Usare un valore diverso per il parametro **DisplayName**.</span><span class="sxs-lookup"><span data-stu-id="1f7ee-108">Use a different value for the **DisplayName** parameter.</span></span> 

```powershell
# Create the service principal (use a strong password)
$cred = Get-Credential
$sp = New-AzureRmADServicePrincipal -DisplayName "AzureDotNetTest" -Password $cred.Password

# Give it the permissions it needs...
New-AzureRmRoleAssignment -ServicePrincipalName $sp.ApplicationId -RoleDefinitionName Contributor

# Display the Application ID, because we'll need it later.
$sp | Select DisplayName, ApplicationId
```

<span data-ttu-id="1f7ee-109">Assicurarsi di annotare il valore di ApplicationId:</span><span class="sxs-lookup"><span data-stu-id="1f7ee-109">Make sure to note the ApplicationId:</span></span>

```plaintext
DisplayName     ApplicationId
-----------     -------------
AzureDotNetTest a2ab11af-01aa-4759-8345-7803287dbd39
```
