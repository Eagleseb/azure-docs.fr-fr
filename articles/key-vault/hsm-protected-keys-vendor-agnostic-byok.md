---
title: Génération et transfert de clés protégées par HSM pour Azure Key Vault - Azure Key Vault | Microsoft Docs
description: Utilisez les informations de cet article pour planifier, générer, puis transférer vos propres clés protégées par HSM à utiliser avec Azure Key Vault. Cette méthode est également appelée BYOK (Bring Your Own Key, ou apportez votre propre clé).
services: key-vault
author: amitbapat
manager: devtiw
tags: azure-resource-manager
ms.service: key-vault
ms.topic: conceptual
ms.date: 02/17/2020
ms.author: ambapat
ms.openlocfilehash: 0e3246f9da202b54cc0d1285795c25cfafb678d8
ms.sourcegitcommit: 1fa2bf6d3d91d9eaff4d083015e2175984c686da
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/01/2020
ms.locfileid: "78207028"
---
# <a name="import-hsm-protected-keys-to-key-vault-preview"></a>Importer des clés protégées par HSM dans Key Vault (préversion)

> [!NOTE]
> Cette fonctionnalité est en préversion et n’est disponible que dans les régions Azure *EUAP USA Est 2* et *EUAP USA Centre*. 

Pour une meilleure garantie, lorsque vous utilisez Azure Key Vault, vous pouvez importer ou générer une clé dans un module de sécurité matériel (HSM), qui ne franchit jamais les limites de celui-ci. Il est souvent fait référence à ce scénario sous le terme *BYOK* (Bring Your Own Key, ou apportez votre propre clé). Azure Key Vault utilise la famille nShield de HSM (FIPS 140-2 niveau 2 validé) de nCipher pour protéger vos clés.

Les informations de cet article vous aident à planifier, à générer puis à transférer vos propres clés protégées par HSM à utiliser avec Azure Key Vault.

> [!NOTE]
> Cette fonctionnalité n’est pas disponible pour Azure Chine 21Vianet. 
> 
> Cette méthode d’importation n’est disponible que pour les [HSM pris en charge](#supported-hsms). 

Pour plus d’informations et pour accéder à un tutoriel sur la prise en main de Key Vault (y compris la création d’un coffre de clés pour des clés protégées par HSM), voir [Qu’est-ce qu’Azure Key Vault ?](key-vault-overview.md).

## <a name="overview"></a>Vue d’ensemble

Voici une vue d’ensemble du processus. Les étapes spécifiques à effectuer sont décrites plus loin dans cet article.

* Dans Azure Key Vault, générez une clé (*Key Exchange Key*, KEK). Cette KEK doit être une clé RSA-HSM qui n’a que l’opération de clé `import`. Seule la référence SKU Premium d’Azure Key Vault prend en charge les clés RSA-HSM.
* Téléchargez la clé publique KEK en tant que fichier. pem.
* Transférez la clé publique KEK sur un ordinateur hors connexion connecté à un HSM local.
* Sur l’ordinateur hors connexion, utilisez l’outil BYOK fourni par votre fournisseur de HSM pour créer un fichier BYOK. 
* La clé cible est chiffrée à l’aide d’une clé KEK qui reste chiffrée jusqu’à ce qu’elle soit transférée vers le HSM d’Azure Key Vault. Seule la version chiffrée de la clé quitte le HSM local.
* Une clé KEK générée à l’intérieur d’un HSM de Key Vault n’est pas exportable. Les HSM appliquent la règle en vertu de laquelle aucune version claire d’une clé KEK n’existe en dehors d’un HSM de Key Vault.
* La clé KEK doit se trouver dans le coffre de clés dans lequel la clé cible doit être importée.
* Lors du chargement du fichier BYOK sur le coffre de clés, un HSM de Key Vault utilise la clé KEK privée pour déchiffrer le matériel de la clé cible et l’importer comme clé HSM. Cette opération se produit entièrement à l’intérieur d’un HSM de Key Vault. La clé cible reste toujours dans la limite de protection du HSM.

## <a name="prerequisites"></a>Prérequis

Le tableau suivant répertorie les conditions préalables à l’utilisation de BYOK dans Azure Key Vault :

| Condition requise | Informations complémentaires |
| --- | --- |
| Abonnement Azure |Pour créer un coffre de clés dans Azure Key Vault, vous avez besoin d’un abonnement Azure. [Inscrivez-vous pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial/). |
| SKU Premium Key Vault pour l’importation de clés protégées par HSM |Pour plus d’informations sur les niveaux de service et les capacités d’Azure Key Vault, voir [Tarification d’Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/). |
| HSM figurant dans la liste des HSM pris en charge, avec un outil BYOK et des instructions fournies par votre fournisseur de HSM | Vous devez disposer d’autorisations pour un HSM et d’une connaissance de base de l’utilisation de votre HSM. Consultez [Modules HSM pris en charge](#supported-hsms). |
| Azure CLI version 2.1.0 ou ultérieure | Voir [Installer l’interface de ligne de commande Azure](/cli/azure/install-azure-cli?view=azure-cli-latest).|

## <a name="supported-hsms"></a>Modules HSM pris en charge

|Nom du fournisseur de HSM|Modèles HSM pris en charge|Informations complémentaires|
|---|---|---|
|Thales|Famille SafeNet Luna HSM 7 avec la version de microprogramme 7.3 ou une version ultérieure| [Outil BYOK SafeNet Luna et documentation](https://supportportal.thalesgroup.com/csm?id=kb_article_view&sys_kb_id=3892db6ddb8fc45005c9143b0b961987&sysparm_article=KB0021016)|

> [!NOTE]
> Pour importer des clés protégées par HSM à partir de la famille nShield de HSM de nCipher, suivez la [procédure BYOK héritée](hsm-protected-keys-legacy.md).

## <a name="supported-key-types"></a>Types de clés pris en charge

|Nom de clé|Type de clé|Taille de la clé|Origine|Description|
|---|---|---|---|---|
|Key Exchange Key (KEK)|RSA| 2 048 bits<br />3 072 bits<br />4 096 bits|HSM Azure Key Vault|Paire de clés RSA sauvegardée par HSM générée dans Azure Key Vault|
|Clé cible|RSA|2 048 bits<br />3 072 bits<br />4 096 bits|HSM du fournisseur|Clé à transférer au HSM d’Azure Key Vault|

## <a name="generate-and-transfer-your-key-to-the-key-vault-hsm"></a>Générer et transférer votre clé vers le HSM du Key Vault

Pour générer et transférer votre clé vers un HDM de Key Vault :

* [Étape 1 : Générer une clé KEK](#step-1-generate-a-kek)
* [Étape 2 : Télécharger la clé publique KEK](#step-2-download-the-kek-public-key)
* [Étape 3 : Générer votre clé et la préparer pour le transfert](#step-3-generate-and-prepare-your-key-for-transfer)
* [Étape 4 : Transférer votre clé vers Azure Key Vault](#step-4-transfer-your-key-to-azure-key-vault)

### <a name="step-1-generate-a-kek"></a>Étape 1 : Générer une clé KEK

Une KEK est une clé RSA générée dans un HSM de Key Vault. La KEK est utilisée pour chiffrer la clé que vous souhaitez importer (clé *cible*).

La clé KEK doit être :
- une clé RSA-HSM (2 048 bits, 3 072 bits ou 4 096 bits)
- Générée dans le coffre de clés dans lequel vous envisagez d’importer la clé cible
- Créée avec les opérations de clé autorisées définies sur `import`

> [!NOTE]
> La clé KEK doit avoir « Importer » comme seule opération de clé autorisée. « Importer » est incompatible avec toutes les autres opérations de clé.

Pour créer une clé KEK avec les opérations de clé définies sur `import`, utilisez la commande [az keyvault key create](/cli/azure/keyvault/key?view=azure-cli-latest#az-keyvault-key-create). Enregistrez l’identificateur de clé (`kid`) qui est retourné par la commande suivante. (Vous allez utiliser la valeur `kid` à l’[étape 3](#step-3-generate-and-prepare-your-key-for-transfer).)

```azurecli
az keyvault key create --kty RSA-HSM --size 4096 --name KEKforBYOK --ops import --vault-name ContosoKeyVaultHSM
```

### <a name="step-2-download-the-kek-public-key"></a>Étape 2 : Télécharger la clé publique KEK

Utilisez la commande [az keyvault key download](/cli/azure/keyvault/key?view=azure-cli-latest#az-keyvault-key-download) pour télécharger la clé publique KEK dans un fichier .pem. La clé cible que vous importez est chiffrée à l’aide de la clé publique KEK.

```azurecli
az keyvault key download --name KEKforBYOK --vault-name ContosoKeyVaultHSM --file KEKforBYOK.publickey.pem
```

Transférez le fichier KEKforBYOK.publickey.pem sur votre ordiateur hors connexion. Vous en aurez besoin à l’étape suivante.

### <a name="step-3-generate-and-prepare-your-key-for-transfer"></a>Étape 3 : Générer votre clé et la préparer pour le transfert

Reportez-vous à la documentation de votre fournisseur de HSM pour télécharger et installer l’outil BYOK. Suivez les instructions de votre fournisseur de HSM pour générer une clé cible, puis créez un package de transfert de clé (fichier BYOK). L’outil BYOK utilise le `kid` de l’[étape 1](#step-1-generate-a-kek) et le fichier KEKforBYOK.publickey.pem que vous avez téléchargé à l’[étape 2](#step-2-download-the-kek-public-key) pour générer une clé cible chiffrée dans un fichier BYOK.

Transférez le fichier BYOK sur votre ordinateur connecté.

> [!NOTE] 
> L’importation de clés RSA 1 024 bits n’est pas prise en charge. Actuellement, l’importation d’une clé Elliptic Curve (EC) n’est pas prise en charge.
> 
> **Problème connu** : L’importation d’une clé cible RSA 4K à partir de modules HSM SafeNet Luna est uniquement prise en charge avec le microprogramme 7.4.0 ou une version plus récente.

### <a name="step-4-transfer-your-key-to-azure-key-vault"></a>Étape 4 : Transférer votre clé vers Azure Key Vault

Pour terminer l’importation de la clé, transférez le package de transfert de clé (fichier BYOK) de votre ordinateur déconnecté vers l’ordinateur connecté à Internet. Pour charger le fichier BYOK dans le HSM de Key Vault, utilisez la commande [az keyvault key import](/cli/azure/keyvault/key?view=azure-cli-latest#az-keyvault-key-import).

```azurecli
az keyvault key import --vault-name ContosoKeyVaultHSM --name ContosoFirstHSMkey --byok-file KeyTransferPackage-ContosoFirstHSMkey.byok
```

Si le chargement réussit, Azure CLI affiche les propriétés de la clé importée.

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez maintenant utiliser cette clé protégée HSM dans votre coffre de clés. Pour plus d’informations, voir cette [comparaison de prix et de fonctionnalité](https://azure.microsoft.com/pricing/details/key-vault/).



