---
title: Librerie di Azure Active Directory per .NET
description: Informazioni di riferimento sulle librerie di Azure Active Directory per .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: active-directory
ms.openlocfilehash: 0226f06546f7dc14b9ab3392008744754d47a19a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190224"
---
# <a name="azure-active-directory-libraries-for-net"></a>Librerie di Azure Active Directory per .NET

## <a name="overview"></a>Panoramica

Con Azure Active Directory è possibile gestire l'accesso degli utenti e controllare l'accesso ad applicazioni e API.

Per iniziare a usare Azure Active Directory, vedere [Accesso e disconnessione all'app Web ASP.NET con Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).

## <a name="client-library"></a>Libreria client

Connettersi e autenticare utenti o applicazioni tramite OAuth2, OpenID Connect, autenticazione con API Graph di Active Directory o [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).

Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Visual Studio - Gestione pacchetti

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="net-core-cli"></a>Interfaccia della riga di comando di .NET Core

```bash
dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory
```

### <a name="code-example"></a>Esempio di codice

Recuperare un token di accesso per un'applicazione desktop.

```csharp
/* Include this "using" directive...
using Microsoft.IdentityModel.Clients.ActiveDirectory;
*/

AuthenticationResult result = null;
AuthenticationContext authContext = new AuthenticationContext("https://someauthority.com");
try
{
    result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
}
catch (AdalException ex)
{
    // An unexpected error occurred, or user canceled the sign in.
    if (ex.ErrorCode != "access_denied")
        MessageBox.Show(ex.Message);

    return;
}
```

> [!div class="nextstepaction"]
> [Esplorare le API client](/dotnet/api/overview/azure/activedirectory/client)

### <a name="samples"></a>Esempi

* [Use OpenID Connect to authenticate users from an Azure AD tenant](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) (Usare OpenID Connect per autenticare utenti da un tenant di Azure AD)
* [Use Oauth2 to call a web API with application permissions](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) (Usare Oauth2 per chiamare un'API Web con autorizzazioni dell'applicazione)
* [Use role-based access control (RBAC) in an application](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) (Usare il controllo degli accessi in base al ruolo in un'applicazione)

Esplorare la raccolta completa di [Esempi di codice di Azure Active Directory](/azure/active-directory/develop/active-directory-code-samples).

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
