---
title: Configurer une application monopage - Plateforme d’identités Microsoft | Azure
description: Apprendre à créer une application monopage (configuration du code de l’application)
services: active-directory
documentationcenter: dev-center-name
author: navyasric
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/11/2020
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f1e0bf44515aab18019b19b4f0a6f84183e5aac3
ms.sourcegitcommit: 76bc196464334a99510e33d836669d95d7f57643
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2020
ms.locfileid: "77160081"
---
# <a name="single-page-application-code-configuration"></a>Application monopage : Configuration de code

En savoir plus sur la configuration du code de votre application monopage (SPA).

## <a name="msal-libraries-that-support-implicit-flow"></a>Bibliothèques MSAL qui prennent en charge le flux implicite

La plateforme d’identités Microsoft fournit les bibliothèques MSAL (Microsoft Authentication Library) suivantes pour prendre en charge le flux implicite à l’aide des pratiques de sécurité recommandées par le secteur :  

| Bibliothèque MSAL | Description |
|--------------|--------------|
| ![MSAL.js](media/sample-v2-code/logo_js.png) <br/> [MSAL.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)  | Bibliothèque JavaScript brute à utiliser dans n’importe quelle application web côté client qui est créée par l’intermédiaire de frameworks JavaScript ou SPA, tels que Angular, Vue.js and React.js. |
| ![MSAL Angular](media/sample-v2-code/logo_angular.png) <br/> [MSAL Angular](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) | Wrapper de la bibliothèque MSAL.js principale pour simplifier l’utilisation dans les applications monopages qui sont créées à l’aide du framework Angular. Cette bibliothèque est disponible en préversion et comporte des [problèmes connus](https://github.com/AzureAD/microsoft-authentication-library-for-js/issues?q=is%3Aopen+is%3Aissue+label%3Aangular) avec certaines versions d’Angular et navigateurs. |

## <a name="application-code-configuration"></a>Configuration du code de l’application

Dans une bibliothèque MSAL, les informations d’inscription d’application sont transmises en tant que configuration pendant l’initialisation de la bibliothèque.

# <a name="javascripttabjavascript"></a>[JavaScript](#tab/javascript)

```javascript
// Configuration object constructed.
const config = {
    auth: {
        clientId: 'your_app_id',
        redirectUri: "your_app_redirect_uri" //defaults to application start page
    }
}

// create UserAgentApplication instance
const userAgentApplication = new UserAgentApplication(config);
```

Pour plus d’informations sur les options configurables, consultez [Initialisation d’application avec MSAL.js](msal-js-initializing-client-applications.md).

# <a name="angulartabangular"></a>[Angular](#tab/angular)

```javascript
//In app.module.ts
import { MsalModule } from '@azure/msal-angular';

@NgModule({
  imports: [ MsalModule.forRoot({
                clientID: 'your_app_id'
            })]
         })

  export class AppModule { }
```

---

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Se connecter et se déconnecter](scenario-spa-sign-in.md)
