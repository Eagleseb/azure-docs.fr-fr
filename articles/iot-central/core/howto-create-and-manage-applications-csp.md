---
title: Créer et gérer des applications Azure IoT Central sur le portail des CSP | Microsoft Docs
description: En tant que fournisseur de solutions cloud, comment créer une application Azure IoT Central pour le compte de votre client.
services: iot-central
ms.service: iot-central
author: dominicbetts
ms.author: dobett
ms.date: 08/23/2019
ms.topic: conceptual
manager: philmea
ms.openlocfilehash: 40c5f612b5b1571bb3d39f452d64a7005701f7c1
ms.sourcegitcommit: 21e33a0f3fda25c91e7670666c601ae3d422fb9c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/05/2020
ms.locfileid: "77023801"
---
# <a name="create-and-manage-an-azure-iot-central-application-from-the-csp-portal"></a>Créer et gérer une application Azure IoT Central sur le portail des CSP

Le programme Fournisseur de solutions cloud Microsoft est un programme Revendeur Microsoft. Son objectif est de fournir à nos partenaires un programme clé en main pour revendre tous les services en ligne commerciaux de Microsoft. Découvrez plus d’informations sur le [programme Fournisseur de solutions cloud](https://partner.microsoft.com/cloud-solution-provider).

En tant que fournisseur de solutions cloud, vous pouvez créer et gérer des applications Microsoft Azure IoT Central pour le compte de vos clients via le [Microsoft Partner Center](https://partnercenter.microsoft.com/partner/home). Quand des applications Azure IoT Central sont créées pour le compte de clients par des fournisseurs de solutions cloud, tout comme avec d’autres services gérés par ceux-ci, les fournisseurs de solutions cloud gèrent la facturation des clients. Le coût d’Azure IoT Central apparaît dans le total de votre facture sur l’Espace partenaires Microsoft.

Pour commencer, connectez-vous à votre compte sur le portail des partenaires Microsoft et sélectionnez un client pour lequel vous voulez créer une application Azure IoT Central. Accédez à Gestion des services pour le client dans la barre de navigation de gauche.

![Microsoft Partner Center, vue Client](media/howto-create-and-manage-applications-csp/image1.png)

Azure IoT Central apparaît en tant que service pouvant être administré. Sélectionnez le lien Azure IoT Central sur la page pour créer des applications ou pour gérer des applications existantes pour ce client.

![Azure IoT Central disponible pour la gestion](media/howto-create-and-manage-applications-csp/image2.png)

Vous êtes dirigé vers la page Gestionnaire d’applications d’Azure IoT Central. Azure IoT Central conserve le contexte indiquant que vous venez du Microsoft Partner Center et que vous voulez gérer ce client particulier. Vous pouvez le constater d’après l’en-tête de la page Gestionnaire d’applications. Vous pouvez soit accéder à une application que vous avez déjà créée pour que ce client la gère, soit lui en créer une nouvelle.

![Gestionnaire de création pour les fournisseurs de services cloud](media/howto-create-and-manage-applications-csp/image3.png)

Pour créer une application Azure IoT Central, sélectionnez **Créer** dans le menu de gauche. Choisissez l’un des modèles sectoriels ou **Application héritée** pour créer une application à partir de zéro. Ceci charge la page de création d’application. Vous devez renseigner tous les champs de cette page, puis choisir **Créer**. Vous pouvez trouver plus d’informations sur chacun des champs ci-dessous.

![Page Créer une application pour les fournisseurs de solutions cloud](media/howto-create-and-manage-applications-csp/image4.png)

![Page Créer une application pour les fournisseurs de solutions cloud](media/howto-create-and-manage-applications-csp/image4-1.png)

![Page Créer une application pour les fournisseurs de solutions cloud - Informations de facturation](media/howto-create-and-manage-applications-csp/image4-2.png)

## <a name="pricing-plan"></a>Plan tarifaire

En tant que fournisseur de solutions cloud, vous pouvez uniquement créer des applications qui utilisent un plan tarifaire Standard. Pour faire une démonstration d’Azure IoT Central à votre client, vous pouvez créer séparément une application qui utilise le plan tarifaire Gratuit. Découvrez plus en détail les plans tarifaires Gratuit et Standard dans la [page des prix Azure IoT Central](https://azure.microsoft.com/pricing/details/iot-central/).

En tant que fournisseur de solutions cloud, vous pouvez uniquement créer des applications qui utilisent un plan tarifaire Standard. Pour faire une démonstration d’Azure IoT Central à votre client, vous pouvez créer séparément une application qui utilise le plan tarifaire Gratuit. Découvrez plus en détail les plans tarifaires Gratuit et Standard dans la [page des prix Azure IoT Central](https://azure.microsoft.com/pricing/details/iot-central/).

## <a name="application-name"></a>Nom de l'application

Le nom de votre application est affiché sur la page **Gestionnaire d’application** et dans chaque application Azure IoT Central. Vous pouvez choisir n’importe quel nom pour votre application Azure IoT Central. Choisissez un nom évocateur pour vous et les autres personnes de votre organisation.

## <a name="application-url"></a>URL de l’application

L’URL de l’application est le lien vers votre application. Vous pouvez enregistrer un signet vers cette URL dans votre navigateur ou le partager avec d’autres utilisateurs.

Quand vous entrez le nom de votre application, l’URL de l’application est générée automatiquement. Si vous préférez, vous pouvez choisir une autre URL pour votre application. Chaque URL d’Azure IoT Central doit y être unique. Vous voyez un message d’erreur si l’URL que vous choisissez a déjà été utilisée.

## <a name="directory"></a>Répertoire

Dans la mesure où Azure IoT Central dispose du contexte indiquant que vous êtes là pour gérer le client sélectionné dans le portail des partenaires Microsoft, vous voyez seulement le locataire Azure Active Directory pour ce client dans le champ Annuaire. 

Un locataire Azure Active Directory contient les identités des utilisateurs, les informations d’identification et d’autres informations de l’organisation. Vous pouvez associer plusieurs abonnements Azure à un même locataire Azure Active Directory.

Pour plus d’informations, consultez [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).

## <a name="azure-subscription"></a>Abonnement Azure

Un abonnement Azure vous permet de créer des instances de services Azure. Azure IoT Central recherche automatiquement tous les abonnements Azure du client auquel vous avez accès et les affiche dans une liste déroulante dans la page **Créer une application**. Choisissez un abonnement Azure pour créer une application Azure IoT Central.

Si vous n’avez pas d’abonnement Azure, vous pouvez en créer un dans le Microsoft Partner Center. Après avoir créé l’abonnement Azure, revenez à la page **Créer une application**. Votre nouvel abonnement apparaît dans la liste déroulante **Abonnement Azure**.

Pour plus d’informations, consultez [Abonnements Azure](https://docs.microsoft.com/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing).

## <a name="region"></a>Région

Choisissez la région ou la [zone géographique](https://azure.microsoft.com/global-infrastructure/geographies/) où vous voulez créer votre application Azure IoT Central. D’une façon générale, pour bénéficier de performances optimales, il est recommandé de choisir la région qui est physiquement la plus proche de vos appareils.

Pour plus d’informations, voir [Régions Azure](https://azure.microsoft.com/global-infrastructure/regions/) et [Zones géographiques Azure](https://azure.microsoft.com/global-infrastructure/geographies/).

Vous pouvez voir les régions dans lesquelles Azure IoT Central est disponible dans la page [Disponibilité des produits par région](https://azure.microsoft.com/global-infrastructure/services/?products=iot-central).

> [!Note]
> Une fois que vous avez choisi une région, vous ne pouvez plus déplacer votre application dans une autre région.

## <a name="application-template"></a>Modèle d’application

Choisissez le modèle d’application que vous souhaitez utiliser pour votre application.


## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez découvert comment créer une application Azure IoT Central en tant que fournisseur de solutions cloud, voici l’étape suivante suggérée :

> [!div class="nextstepaction"]
> [Administrer votre application](howto-administer.md)
