Creare un file di testo denominato `azureauth.properties` usando le credenziali dell'entità servizio:

```plaintext
# sample management library properties file
subscription=15dbcfa8-4b93-4c9a-881c-6189d39f04d4
client=a2ab11af-01aa-4759-8345-7803287dbd39
key=password
tenant=43413cc1-5886-4711-9804-8cfea3d1c3ee
managementURI=https://management.core.windows.net/
baseURL=https://management.azure.com/
authURL=https://login.windows.net/
graphURL=https://graph.windows.net/
```

- subscription: usare il valore *SubscriptionId* specificato durante l'esecuzione di `Login-AzureRmAccount`.
- client: usare il valore *ApplicationId* dall'output dell'entità servizio.
- key: usare il parametro *-Password* assegnato durante l'esecuzione di `New-AzureRmADServicePrincipal` (senza virgolette).
- tenant: usare il valore *TenantId* specificato durante l'esecuzione di `Login-AzureRmAccount`.

Salvare questo file nel sistema in una posizione sicura e leggibile dal codice. Usare PowerShell per impostare una variabile di ambiente denominata `AZURE_AUTH_LOCATION` con il percorso completo del file, ad esempio:

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.properties", "User")
```
