---
title: Série NV – Machines virtuelles Microsoft Azure
description: Spécifications pour les machines virtuelles de la série NV.
services: virtual-machines
author: vikancha
ms.service: virtual-machines
ms.topic: article
ms.date: 02/03/2020
ms.author: lahugh
ms.openlocfilehash: 7fd9fff87564b790915acf01373c078c2012371e
ms.sourcegitcommit: d45fd299815ee29ce65fd68fd5e0ecf774546a47
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2020
ms.locfileid: "78273868"
---
# <a name="nv-series"></a>Série NV

Les machines virtuelles de la série NV sont optimisées par des GPU [NVIDIA Tesla M60](https://images.nvidia.com/content/tesla/pdf/188417-Tesla-M60-DS-A4-fnl-Web.pdf) et la technologie NVIDIA GRID pour les applications de bureautique accélérées et les bureaux virtuels où les clients peuvent visualiser leurs données ou simulations. Les utilisateurs peuvent visualiser leurs flux de travail nécessitant beaucoup de graphismes sur les instances NV afin d’obtenir des fonctionnalités graphiques de qualité supérieure et exécuter par ailleurs des charges de travail simple précision comme le codage et le rendu. Les machines virtuelles de la série NV sont également dotées de processeurs Intel Xeon E5-2690 v3 (Haswell).

Chaque GPU dans les instances NV est fourni avec une licence GRID. Cette licence vous donne la possibilité d’utiliser une instance NV comme station de travail virtuelle pour un seul utilisateur. 25 utilisateurs simultanés peuvent aussi se connecter à la machine virtuelle pour un scénario d’application virtuelle.

Premium Storage :  Non pris en charge

Mise en cache du Stockage Premium :  Non pris en charge

Migration dynamique : Non pris en charge

Mises à jour avec préservation de la mémoire : Non pris en charge

| Taille | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | GPU | Mémoire GPU : Gio | Disques de données max. | Nombre max de cartes réseau | Stations de travail virtuelles | Applications virtuelles |
|---|---|---|---|---|---|---|---|---|---|
| Standard_NV6  | 6  | 56  | 340  | 1 | 8  | 24 | 1 | 1 | 25  |
| Standard_NV12 | 12 | 112 | 680  | 2 | 16 | 48 | 2 | 2 | 50  |
| Standard_NV24 | 24 | 224 | 1440 | 4 | 32 | 64 | 4 | 4 | 100 |

1 GPU = une moitié de carte M60.

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

## <a name="supported-operating-systems-and-drivers"></a>Systèmes d’exploitation et pilotes pris en charge

Pour tirer parti des fonctionnalités GPU de machines virtuelles de la série N Azure, installez des pilotes GPU NVIDIA.

[L’extension du pilote GPU NVIDIA](./extensions/hpccompute-gpu-windows.md) installe les pilotes CUDA ou GRID NVIDIA appropriés sur une machine virtuelle de série N. Installez ou gérez l’extension à l’aide du portail Azure ou d’outils tels qu’Azure PowerShell ou les modèles Azure Resource Manager. Consultez la [documentation sur l’extension du pilote GPU NVIDIA](./extensions/hpccompute-gpu-windows.md) pour connaître les systèmes d’exploitation pris en charge et les étapes de déploiement. Pour des informations générales sur les extensions de machine virtuelle, consultez [Extensions et fonctionnalités des machines virtuelles Azure](./extensions/overview.md).

Si vous choisissez d’installer manuellement les pilotes GPU NVIDIA, voir [Configuration des pilotes GPU de série N pour Windows](./windows/n-series-driver-setup.md) ou [Configuration des pilotes GPU de série N pour Linux](./linux/n-series-driver-setup.md) pour connaître les systèmes d’exploitation et pilotes pris en charge, ainsi que les étapes d’installation et de vérification.

## <a name="other-sizes"></a>Autres tailles

- [Usage général](sizes-general.md)
- [Mémoire optimisée](sizes-memory.md)
- [Optimisé pour le stockage](sizes-storage.md)
- [Optimisé pour le GPU](sizes-gpu.md)
- [Calcul haute performance](sizes-hpc.md)
- [Générations précédentes](sizes-previous-gen.md)

## <a name="next-steps"></a>Étapes suivantes

Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.
