---
title: Images et référentiels de conteneurs
services: cognitive-services
author: IEvangelist
manager: nitinme
description: Deux tableaux représentant les registres de conteneurs, les dépôts et les noms d’images pour toutes les offres Cognitive Services.
ms.service: cognitive-services
ms.topic: include
ms.date: 03/10/2020
ms.author: dapine
ms.openlocfilehash: 55a3bb5f894d3ab753cfec64687abc9c7cae53cb
ms.sourcegitcommit: b8d0d72dfe8e26eecc42e0f2dbff9a7dd69d3116
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79082671"
---
### <a name="container-repositories-and-images"></a>Images et référentiels de conteneurs

Les tableaux ci-dessous répertorient les images conteneurs offertes par Azure Cognitive Services. Pour obtenir la liste complète de tous les noms d’image conteneur disponibles et leurs étiquettes utilisables, consultez [Étiquettes des images conteneurs Cognitive Services](../container-image-tags.md). Actuellement, il n’existe pas de conteneurs Cognitive Services en disponibilité générale. Pour le moment, jusqu’à ce que d’autres annonces soient faites, les conteneurs sont disponibles de façon *publique non contrôlée* ou en *préversion publique contrôlée*.

 - *Publique non contrôlée* : les conteneurs sont disponibles publiquement sans mécanisme de contrôle.
 - *Préversion publique contrôlée* : les conteneurs sont disponibles publiquement, mais exigent d’abord une demande formelle pour l’accès au registre des conteneurs.

#### <a name="public-ungated-container-registry-mcrmicrosoftcom"></a>Public « non contrôlé » (registre de conteneurs : `mcr.microsoft.com`)

Le registre de conteneurs Microsoft (MCR) regroupe tous les conteneurs « non contrôlés » disponibles publiquement pour Cognitive Services. Les conteneurs sont également accessibles directement à partir du [Docker Hub](https://hub.docker.com/_/microsoft-azure-cognitive-services).

| Service | Conteneur | Nom de registre de conteneurs / référentiel / image |
|--|--|--|
| [LUIS](../../LUIS/luis-container-howto.md) | LUIS | `mcr.microsoft.com/azure-cognitive-services/luis` |
| [Analyse de texte](../../text-analytics/how-tos/text-analytics-how-to-install-containers.md) | Extraction d’expressions clés | `mcr.microsoft.com/azure-cognitive-services/keyphrase` |
| [Analyse de texte](../../text-analytics/how-tos/text-analytics-how-to-install-containers.md) | Détection de la langue | `mcr.microsoft.com/azure-cognitive-services/language` |
| [Analyse de texte](../../text-analytics/how-tos/text-analytics-how-to-install-containers.md) | Analyse des sentiments | `mcr.microsoft.com/azure-cognitive-services/sentiment` |

#### <a name="public-gated-preview-container-registry-containerpreviewazurecrio"></a>Préversion « contrôlée » publique (registre de conteneurs : `containerpreview.azurecr.io`)

Le registre des conteneurs en préversion héberge tous les conteneurs « contrôlés » disponibles publiquement pour Cognitive Services. L’accès à ces conteneurs nécessite qu’une demande formelle leur soit adressée via leur registre de conteneurs.

| Service | Conteneur | Nom de registre de conteneurs / référentiel / image |
|--|--|--|
| [Détecteur d’anomalies](../../anomaly-detector/anomaly-detector-container-howto.md) | Le détecteur d’anomalies | `containerpreview.azurecr.io/microsoft/cognitive-services-anomaly-detector` |
| [Vision par ordinateur](../../Computer-vision/computer-vision-how-to-install-containers.md) | Lire | `containerpreview.azurecr.io/microsoft/cognitive-services-read` |
| [Visage](../../face/face-how-to-install-containers.md) | Face | `containerpreview.azurecr.io/microsoft/cognitive-services-face` |
| [Form recognizer](https://go.microsoft.com/fwlink/?linkid=2083826&clcid=0x409) | Form Recognizer | `containerpreview.azurecr.io/microsoft/cognitive-services-form-recognizer` |
| [API Speech Service](../../speech-service/speech-container-howto.md?tab=stt) | Reconnaissance vocale | `containerpreview.azurecr.io/microsoft/cognitive-services-speech-to-text` |
| [API Speech Service](../../speech-service/speech-container-howto.md?tab=cstt) | Reconnaissance vocale personnalisée | `containerpreview.azurecr.io/microsoft/cognitive-services-custom-speech-to-text` |
| [API Speech Service](../../speech-service/speech-container-howto.md?tab=tts) | Synthèse vocale | `containerpreview.azurecr.io/microsoft/cognitive-services-text-to-speech` |
| [API Speech Service](../../speech-service/speech-container-howto.md?tab=ctts) | Synthèse vocale personnalisée | `containerpreview.azurecr.io/microsoft/cognitive-services-custom-text-to-speech` |
