Creare un file di testo denominato `azureauth.json`. Incollare l'output JSON ottenuto con la creazione dell'entità servizio.

Salvare questo file nel sistema in una posizione sicura e leggibile dal codice. Usare PowerShell per impostare una variabile di ambiente denominata `AZURE_AUTH_LOCATION` con il percorso completo del file, ad esempio:

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
