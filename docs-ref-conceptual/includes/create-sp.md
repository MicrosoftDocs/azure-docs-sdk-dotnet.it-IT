L'applicazione .NET necessita delle autorizzazioni per la lettura e la creazione di risorse nella sottoscrizione di Azure per potere usare le librerie di gestione di Azure per .NET. Creare un'entità servizio e configurare l'app per l'esecuzione con le rispettive credenziali per concedere questo accesso. Le entità servizio consentono di creare un account non interattivo associato all'identità a cui vengono concessi solo i privilegi necessari per l'esecuzione dell'app.

Accedere prima di tutto ad Azure PowerShell:

```powershell
Login-AzureRmAccount
```

Annotare le informazioni visualizzate sul tenant e sulla sottoscrizione:

```plaintext
Environment           : AzureCloud
Account               : jane@contoso.com
TenantId              : 43413cc1-5886-4711-9804-8cfea3d1c3ee
SubscriptionId        : 15dbcfa8-4b93-4c9a-881c-6189d39f04d4
SubscriptionName      : my-subscription
CurrentStorageAccount : 
```

[Creare un'entità servizio usando PowerShell](/powershell/azure/create-azure-service-principal-azureps), come illustrato di seguito. 

> [!NOTE]
> Se il cmdlet `New-AzureRmADServicePrincipal` seguente restituisce "Another object with the same value for property identifierUris already exists" (Esiste già un oggetto con lo stesso valore per la proprietà identifierUris), è già presente un'entità servizio con tale nome nel tenant. Usare un valore diverso per il parametro **DisplayName**. 

```powershell
# Create the service principal (use a strong password)
$cred = Get-Credential
$sp = New-AzureRmADServicePrincipal -DisplayName "AzureDotNetTest" -Password $cred.Password

# Give it the permissions it needs...
New-AzureRmRoleAssignment -ServicePrincipalName $sp.ApplicationId -RoleDefinitionName Contributor

# Display the Application ID, because we'll need it later.
$sp | Select DisplayName, ApplicationId
```

Assicurarsi di annotare il valore di ApplicationId:

```plaintext
DisplayName     ApplicationId
-----------     -------------
AzureDotNetTest a2ab11af-01aa-4759-8345-7803287dbd39
```
