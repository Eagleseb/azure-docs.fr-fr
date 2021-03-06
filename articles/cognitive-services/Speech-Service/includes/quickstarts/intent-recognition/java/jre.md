---
author: IEvangelist
ms.service: cognitive-services
ms.subservice: speech-service
ms.date: 01/27/2020
ms.topic: include
ms.author: dapine
zone_pivot_groups: programming-languages-set-two
ms.openlocfilehash: bd15a19a352120e01da04aeca0f3b27d3fce092f
ms.sourcegitcommit: dfa543fad47cb2df5a574931ba57d40d6a47daef
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/18/2020
ms.locfileid: "77445900"
---
## <a name="prerequisites"></a>Prérequis

Avant de commencer :

* S’il s’agit de votre premier projet Java (JRE), utilisez ce guide pour <a href="~/articles/cognitive-services/Speech-Service/quickstarts/create-project.md?tabs=jre" target="_blank">créer un exemple de projet vide<span class="docon docon-navigate-external x-hidden-focus"></span></a>.
* <a href="~/articles/cognitive-services/Speech-Service/quickstarts/setup-platform.md?tabs=jre" target="_blank">Installez le SDK Speech pour votre environnement de développement<span class="docon docon-navigate-external x-hidden-focus"></span></a>.

## <a name="create-a-luis-app-for-intent-recognition"></a>Créer une application LUIS pour la reconnaissance de l’intention

[!INCLUDE [Create a LUIS app for intent recognition](../luis-sign-up.md)]

## <a name="open-your-project"></a>Ouvrir votre projet

1. Ouvrez l’IDE de votre choix.
2. Chargez votre projet et ouvrez `Main.java`.

## <a name="start-with-some-boilerplate-code"></a>Commencer avec du code réutilisable

Nous allons ajouter du code qui servira de squelette à notre projet

[!code-java[](~/samples-cognitive-services-speech-sdk/quickstart/java/jre/intent-recognition/src/speechsdk/quickstart/Main.java?range=6-20,68-75)]

## <a name="create-a-speech-configuration"></a>Créer une configuration Speech

Pour pouvoir initialiser un objet `IntentRecognizer`, vous devez au préalable créer une configuration qui utilise la clé et la localisation de votre ressource de prédiction LUIS.  

Insérez ce code dans le bloc try/catch dans `main()`. Veillez à mettre à jour ces valeurs :

* Remplacez `"YourLanguageUnderstandingSubscriptionKey"` par votre clé de prédiction LUIS.
* Remplacez `"YourLanguageUnderstandingServiceRegion"` par votre localisation LUIS. Utilisez l’**identificateur Région** de la [région](https://aka.ms/speech/sdkregion).

>[!TIP]
> Si vous avez besoin d’aide pour trouver ces valeurs, consultez [Créer une application LUIS pour la reconnaissance de l’intention](#create-a-luis-app-for-intent-recognition).

[!code-java[](~/samples-cognitive-services-speech-sdk/quickstart/java/jre/intent-recognition/src/speechsdk/quickstart/Main.java?range=27)]

Cet exemple utilise la méthode `FromSubscription()` pour générer la `SpeechConfig`. Pour obtenir la liste complète des méthodes disponibles, consultez la rubrique [Classe SpeechConfig](https://docs.microsoft.com/dotnet/api/microsoft.cognitiveservices.speech.speechconfig?view=azure-dotnet).

Le SDK Speech reconnaît par défaut l’utilisation de la langue en-US. Consultez [Spécifier la langue source pour la reconnaissance vocale](../../../../how-to-specify-source-language.md) pour plus d’informations sur le choix de la langue source.

## <a name="initialize-an-intentrecognizer"></a>Initialiser IntentRecognizer

Créons maintenant un `IntentRecognizer`. Insérez ce code juste en dessous de votre configuration Speech.

[!code-java[](~/samples-cognitive-services-speech-sdk/quickstart/java/jre/intent-recognition/src/speechsdk/quickstart/Main.java?range=30)]

## <a name="add-a-languageunderstandingmodel-and-intents"></a>Ajouter un LanguageUnderstandingModel et des intentions

Vous devez associer un `LanguageUnderstandingModel` au module de reconnaissance de l’intention et ajouter les intentions que vous souhaitez reconnaître. Nous allons utiliser les intentions du domaine prédéfini pour la domotique.

Insérez ce code en dessous de votre `IntentRecognizer`. Veillez à remplacer `"YourLanguageUnderstandingAppId"` par votre ID d’application LUIS.

>[!TIP]
> Si vous avez besoin d’aide pour trouver cette valeur, consultez [Créer une application LUIS pour la reconnaissance de l’intention](#create-a-luis-app-for-intent-recognition).

[!code-java[](~/samples-cognitive-services-speech-sdk/quickstart/java/jre/intent-recognition/src/speechsdk/quickstart/Main.java?range=33-35)]

## <a name="recognize-an-intent"></a>Reconnaître une intention

À partir de l’objet `IntentRecognizer`, vous devez appeler la méthode `recognizeOnceAsync()`. Cette méthode permet au service Speech de savoir que vous envoyez une seule expression pour reconnaissance, et d’arrêter la reconnaissance une fois que l’expression a été identifiée.

Insérez ce code en dessous de votre modèle :

[!code-java[](~/samples-cognitive-services-speech-sdk/quickstart/java/jre/intent-recognition/src/speechsdk/quickstart/Main.java?range=40)]

## <a name="display-the-recognition-results-or-errors"></a>Afficher les résultats de la reconnaissance (ou les erreurs)

Lorsque le résultat de la reconnaissance est retourné par le service de reconnaissance vocale, vous pouvez effectuer une opération avec celui-ci. Nous allons faire simple et imprimer le résultat dans la console.

Insérez ce code en dessous de votre appel à `recognizeOnceAsync()` : [!code-java[](~/samples-cognitive-services-speech-sdk/quickstart/java/jre/intent-recognition/src/speechsdk/quickstart/Main.java?range=43-64)]

## <a name="release-resources"></a>Libérer des ressources

Il est important de libérer les ressources lorsque vous avez fini de les utiliser. Insérez ce code à la fin du bloc try/catch :

[!code-java[](~/samples-cognitive-services-speech-sdk/quickstart/java/jre/intent-recognition/src/speechsdk/quickstart/Main.java?range=66-67)]

## <a name="check-your-code"></a>Vérifier votre code

À ce stade, votre code doit ressembler à ceci :

> [!NOTE]
> Nous avons ajouté des commentaires à cette version.

[!code-java[](~/samples-cognitive-services-speech-sdk/quickstart/java/jre/intent-recognition/src/speechsdk/quickstart/Main.java?range=6-75)]

## <a name="build-and-run-your-app"></a>Générer et exécuter votre application

Appuyez sur <kbd>F11</kbd> ou sélectionnez **Run** (Exécuter) > **Debug** (Déboguer).
Les 15 secondes suivantes de saisie vocale provenant de votre microphone seront reconnues et enregistrées dans la fenêtre console.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [footer](./footer.md)]
