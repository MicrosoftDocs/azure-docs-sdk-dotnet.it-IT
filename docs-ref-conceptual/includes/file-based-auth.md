<span data-ttu-id="76c32-101">Creare un file di testo denominato `azureauth.properties` usando le credenziali dell'entità servizio:</span><span class="sxs-lookup"><span data-stu-id="76c32-101">Create a text file named `azureauth.properties` using the service principal credentials:</span></span>

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

- <span data-ttu-id="76c32-102">subscription: usare il valore *SubscriptionId* specificato durante l'esecuzione di `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="76c32-102">subscription: use the *SubscriptionId* value from when you ran `Login-AzureRmAccount`.</span></span>
- <span data-ttu-id="76c32-103">client: usare il valore *ApplicationId* dall'output dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="76c32-103">client: use the *ApplicationId* value from the service principal output.</span></span>
- <span data-ttu-id="76c32-104">key: usare il parametro *-Password* assegnato durante l'esecuzione di `New-AzureRmADServicePrincipal` (senza virgolette).</span><span class="sxs-lookup"><span data-stu-id="76c32-104">key: use the *-Password* parameter you assigned when you ran `New-AzureRmADServicePrincipal` (without quotes).</span></span>
- <span data-ttu-id="76c32-105">tenant: usare il valore *TenantId* specificato durante l'esecuzione di `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="76c32-105">tenant: use the *TenantId* value from when you ran `Login-AzureRmAccount`.</span></span>

<span data-ttu-id="76c32-106">Salvare questo file nel sistema in una posizione sicura e leggibile dal codice.</span><span class="sxs-lookup"><span data-stu-id="76c32-106">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="76c32-107">Usare PowerShell per impostare una variabile di ambiente denominata `AZURE_AUTH_LOCATION` con il percorso completo del file, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="76c32-107">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.properties", "User")
```
