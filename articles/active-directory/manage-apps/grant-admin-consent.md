---
title: Accorder le consentement administrateur au niveau locataire à une application - Azure AD
description: Découvrez comment accorder un consentement au niveau locataire à une application afin d’éviter que les utilisateurs finaux donnent leur consentement lors de la connexion à une application.
services: active-directory
author: psignoret
manager: CelesteDG
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: conceptual
ms.date: 11/04/2019
ms.author: mimart
ms.reviewer: phsignor
ms.collection: M365-identity-device-management
ms.openlocfilehash: c515fef4997720435c64bd5f3ae7b18f8921fc5d
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75475271"
---
# <a name="grant-tenant-wide-admin-consent-to-an-application"></a>Accorder le consentement administrateur au niveau locataire à une application

Découvrez comment simplifier l’expérience utilisateur en accordant un consentement administrateur au niveau locataire à une application. Cet article présente les différentes façons d’y parvenir. Les méthodes s’appliquent à tous les utilisateurs finaux de votre client Azure Active Directory (Azure AD).

Pour plus d’informations sur le consentement des applications, consultez [Infrastructure de consentement d’Azure Active Directory](../develop/consent-framework.md).

## <a name="prerequisites"></a>Conditions préalables requises

L’octroi du consentement administrateur au niveau locataire vous oblige à vous connecter en tant qu’[administrateur général](../users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator), [administrateur d’application](../users-groups-roles/directory-assign-admin-roles.md#application-administrator) ou [administrateur d’application cloud](../users-groups-roles/directory-assign-admin-roles.md#cloud-application-administrator).

> [!IMPORTANT]
> Lorsqu’une application a reçu le consentement administrateur au niveau locataire, tous les utilisateurs peuvent se connecter à l’application, sauf si elle a été configurée pour exiger l’attribution de l’utilisateur. Pour restreindre à des utilisateurs spécifiques l’accès à une application, demandez l’affectation d’utilisateurs, puis affectez des utilisateurs ou des groupes à l’application. Pour plus d'informations, voir [Méthodes d'affectation d'utilisateurs et de groupes](methods-for-assigning-users-and-groups.md).

> [!WARNING]
> Le fait d’accorder le consentement administrateur au niveau locataire à une application permettra à l’application et à l’éditeur de l'application d’accéder aux données de votre organisation. Examinez attentivement les autorisations demandées par l’application avant d’accorder le consentement.

## <a name="grant-admin-consent-from-the-azure-portal"></a>Accorder le consentement administrateur à partir du Portail Azure

### <a name="grant-admin-consent-in-enterprise-apps"></a>Accorder le consentement administrateur dans des applications d’entreprise

Vous pouvez accorder le consentement administrateur au niveau locataire via *Applications d’entreprise* si l’application a déjà été approvisionnée dans votre locataire. Par exemple, une application peut être approvisionnée dans votre locataire si au moins un utilisateur a déjà donné son consentement à l’application. Pour plus d’informations, consultez [Comment et pourquoi les applications sont ajoutées à Azure Active Directory](../develop/active-directory-how-applications-are-added.md).

Pour accorder le consentement administrateur au niveau locataire à une application figurant dans **Applications d’entreprise** :

1. Connectez-vous au [Portail Azure](https://portal.azure.com) en tant qu’[administrateur général](../users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator), [administrateur d’application](../users-groups-roles/directory-assign-admin-roles.md#application-administrator) ou [administrateur d’application cloud](../users-groups-roles/directory-assign-admin-roles.md#cloud-application-administrator).
2. Sélectionnez **Azure Active Directory** puis **Applications d’entreprise**.
3. Sélectionnez l’application à laquelle vous souhaitez accorder le consentement administrateur au niveau locataire.
4. Sélectionnez **Autorisations**, puis cliquez sur **Accorder le consentement administrateur**.
5. Examinez attentivement les autorisations requises par l’application.
6. Si vous acceptez les autorisations requises par l’application, accordez le consentement. Si ce n’est pas le cas, cliquez sur **Annuler** ou fermez la fenêtre.

### <a name="grant-admin-consent-in-app-registrations"></a>Accorder le consentement administrateur dans les inscriptions d’applications

Pour les applications développées par votre organisation ou inscrites directement dans votre locataire Azure AD, vous pouvez également accorder le consentement administrateur au niveau locataire à partir de **Inscriptions d’applications** dans le Portail Azure.

Pour accorder le consentement administrateur au niveau locataire dans **Inscriptions d'applications** :

1. Connectez-vous au [Portail Azure](https://portal.azure.com) en tant qu’[administrateur général](../users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator), [administrateur d’application](../users-groups-roles/directory-assign-admin-roles.md#application-administrator) ou [administrateur d’application cloud](../users-groups-roles/directory-assign-admin-roles.md#cloud-application-administrator).
2. Sélectionnez **Azure Active Directory**, puis **Inscription d’applications**.
3. Sélectionnez l’application à laquelle vous souhaitez accorder le consentement administrateur au niveau locataire.
4. Sélectionnez **Autorisations d’API**, puis cliquez sur **Accorder le consentement administrateur**.
5. Examinez attentivement les autorisations requises par l’application.
6. Si vous acceptez les autorisations requises par l’application, accordez le consentement. Si ce n’est pas le cas, cliquez sur **Annuler** ou fermez la fenêtre.

## <a name="construct-the-url-for-granting-tenant-wide-admin-consent"></a>Construire l’URL pour accorder le consentement de l’administrateur au niveau du locataire

Lorsque vous accordez le consentement administrateur au niveau du locataire à l’aide de l’une des méthodes décrites ci-dessus, une fenêtre s’ouvre à partir du Portail Azure pour demander le consentement administrateur au niveau locataire. Si vous connaissez l’ID client (également appelé ID d’application) de l’application, vous pouvez générer la même URL pour accorder le consentement administrateur au niveau locataire.

L’URL de consentement administrateur au niveau locataire suit le format suivant :

    https://login.microsoftonline.com/{tenant-id}/adminconsent?client_id={client-id}

où :

* `{client-id}` est l’ID client de l’application (également appelé ID d’application).
* `{tenant-id}` est l’ID de locataire de votre organisation ou un nom de domaine vérifié.

Comme toujours, examinez attentivement les autorisations demandées par une application avant d’accorder le consentement.

## <a name="next-steps"></a>Étapes suivantes

[Configurer le consentement de l’utilisateur final pour une application](configure-user-consent.md)

[Configurer le workflow du consentement administrateur](configure-admin-consent-workflow.md)

[Autorisations et consentement dans la plateforme d’identités Microsoft](../develop/active-directory-v2-scopes.md)

[Azure AD sur StackOverflow](https://stackoverflow.com/questions/tagged/azure-active-directory)
