---
title: Transformation d’union des flux de données de mappage
description: Transformation de nouvelle branche de mappage de flux de données pour Azure Data Factory
author: kromerm
ms.author: makromer
ms.reviewer: douglasl
ms.service: data-factory
ms.topic: conceptual
ms.custom: seo-lt-2019; seo-dt-2019
ms.date: 02/12/2019
ms.openlocfilehash: adba1eb61676dbebcb356490b14b279ebe69c644
ms.sourcegitcommit: a5ebf5026d9967c4c4f92432698cb1f8651c03bb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2019
ms.locfileid: "74930162"
---
# <a name="azure-data-factory-mapping-data-flow-union-transformation"></a>Transformation d’union de flux de données de mappage Azure Data Factory

L'union combinera plusieurs flux de données en un, avec l'union SQL de ces flux en tant que nouvelle sortie de la transformation d’union. Tous les schémas de chaque flux d’entrée sont combinés à l’intérieur de votre flux de données, sans avoir à disposer d’une clé de jointure.

Vous pouvez combiner des n flux dans le tableau de paramètres en sélectionnant l’icône « + » en regard de chaque ligne configurée, notamment la source de données et des flux de transformations existantes dans votre flux de données.

![Transformation d’union](media/data-flow/union.png "Union")

Dans ce cas, vous pouvez associer des métadonnées disparates provenant de plusieurs sources (dans cet exemple, trois fichiers sources différents) et les combiner en un seul flux :

![Vue d’ensemble de la transformation d’union](media/data-flow/union111.png "Union 1")

Pour ce faire, ajoutez des lignes supplémentaires dans les paramètres d’union, en incluant toutes les sources que vous souhaitez ajouter. Il n’est pas nécessaire d’avoir une clé de recherche ou de jointure commune :

![Paramètres de transformation d’union](media/data-flow/unionsettings.png "Paramètres d’union")

Si vous définissez une transformation Sélectionner après l’union, vous ne pourrez pas renommer des champs qui se chevauchent ou ceux qui n’étaient pas nommés à partir de sources sans en-tête. Cliquez sur « Inspecter » pour afficher les métadonnées combinées avec les 132 colonnes de cet exemple à partir de trois sources différentes :

![Transformation d’union finale](media/data-flow/union333.png "Union 3")

## <a name="name-and-position"></a>Nom et position

Lorsque vous choisissez une « union par nom », chaque valeur de colonne est supprimée dans la colonne correspondante de chaque source, avec un nouveau schéma de métadonnées concaténées.

Si vous choisissez une « union par position », chaque valeur de colonne est supprimée à la position d’origine de chaque source correspondante, ce qui entraîne un nouveau flux combiné de données où les données de chaque source sont ajoutées au même flux :

![Sortie d’union](media/data-flow/unionoutput.png "Sortie d’union")

## <a name="next-steps"></a>Étapes suivantes

Explorez les transformations similaires, y compris [Joindre](data-flow-join.md) et [Existe](data-flow-exists.md).
