---
title: Librerie di Azure Active Directory per .NET
description: Informazioni di riferimento sulle librerie di Azure Active Directory per .NET
keywords: Azure, .NET, SDK, API, AAD, Active Directory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: adbe907888e49066b6d67a4fb26410a6f6b3b095
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2017
---
# <a name="azure-active-directory-libraries-for-net"></a><span data-ttu-id="ee048-104">Librerie di Azure Active Directory per .NET</span><span class="sxs-lookup"><span data-stu-id="ee048-104">Azure Active Directory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="ee048-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ee048-105">Overview</span></span>

<span data-ttu-id="ee048-106">Con Azure Active Directory è possibile gestire l'accesso degli utenti e controllare l'accesso ad applicazioni e API.</span><span class="sxs-lookup"><span data-stu-id="ee048-106">Sign-on users and manage access to applications and APIs with Azure Active Directory.</span></span>

<span data-ttu-id="ee048-107">Per iniziare a usare Azure Active Directory, vedere [Accesso e disconnessione all'app Web ASP.NET con Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).</span><span class="sxs-lookup"><span data-stu-id="ee048-107">To get started with Azure Active Directory, see [ASP.NET web app sign-in and sign-out with Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="ee048-108">Libreria client</span><span class="sxs-lookup"><span data-stu-id="ee048-108">Client library</span></span>

<span data-ttu-id="ee048-109">Connettersi e autenticare utenti o applicazioni tramite OAuth2, OpenID Connect, autenticazione con API Graph di Active Directory o [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span><span class="sxs-lookup"><span data-stu-id="ee048-109">Connect and authenticate users or applications over OAuth2, OpenID Connect, Active Directory Graph API authentication or [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span></span>

<span data-ttu-id="ee048-110">Installare il [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) direttamente dalla [Console di Gestione pacchetti][PackageManager] di Visual Studio o tramite l'[interfaccia della riga di comando di .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="ee048-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ee048-111">Visual Studio - Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="ee048-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="net-core-cli"></a><span data-ttu-id="ee048-112">Interfaccia della riga di comando di .NET Core</span><span class="sxs-lookup"><span data-stu-id="ee048-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory
```

### <a name="code-example"></a><span data-ttu-id="ee048-113">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="ee048-113">Code Example</span></span>

<span data-ttu-id="ee048-114">Recuperare un token di accesso per un'applicazione desktop.</span><span class="sxs-lookup"><span data-stu-id="ee048-114">Retrieve an access token for a desktop application.</span></span>

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
> [<span data-ttu-id="ee048-115">Esplorare le API client</span><span class="sxs-lookup"><span data-stu-id="ee048-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/activedirectory/client)

### <a name="samples"></a><span data-ttu-id="ee048-116">Esempi</span><span class="sxs-lookup"><span data-stu-id="ee048-116">Samples</span></span>

* [<span data-ttu-id="ee048-117">Use OpenID Connect to authenticate users from an Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="ee048-117">Use OpenID Connect to authenticate users from an Azure AD tenant</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) (Usare OpenID Connect per autenticare utenti da un tenant di Azure AD)
* [<span data-ttu-id="ee048-118">Use Oauth2 to call a web API with application permissions</span><span class="sxs-lookup"><span data-stu-id="ee048-118">Use Oauth2 to call a web API with application permissions</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) (Usare Oauth2 per chiamare un'API Web con autorizzazioni dell'applicazione)
* [<span data-ttu-id="ee048-119">Use role-based access control (RBAC) in an application</span><span class="sxs-lookup"><span data-stu-id="ee048-119">Use role-based access control (RBAC) in an application</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) (Usare il controllo degli accessi in base al ruolo in un'applicazione)

<span data-ttu-id="ee048-120">Esplorare la raccolta completa di [Esempi di codice di Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-code-samples).</span><span class="sxs-lookup"><span data-stu-id="ee048-120">Explore the full collection of [Azure Active Directory code samples](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-code-samples).</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
