---
title: Série NDv2 – Machines virtuelles Azure
description: Spécifications pour les machines virtuelles de la série NDv2.
services: virtual-machines
author: vikancha
ms.service: virtual-machines
ms.topic: article
ms.date: 02/03/2020
ms.author: lahugh
ms.openlocfilehash: 1aa2a6402a58ba69a7b5999803bb10d48169a035
ms.sourcegitcommit: d45fd299815ee29ce65fd68fd5e0ecf774546a47
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2020
ms.locfileid: "78267437"
---
# <a name="updated-ndv2-series-preview"></a>Série NDv2 mise à jour (préversion)

Les machines virtuelles de la série NDv2 rejoignent la famille des processeurs graphiques (GPU) pour répondre aux besoins de l’IA accélérée par GPU, de l’apprentissage automatique, de la simulation et des charges de travail HPC les plus exigeantes.

NDv2 est alimenté par 8 GPU NVIDIA Tesla V100 NVLINK, doté chacun de 32 Go de mémoire. Chaque machine virtuelle NDv2 possède également 40 cœurs Intel Xeon Platinum 8168 (Skylake) non hyperthread et 672 Gio de mémoire système.

Les instances NDv2 offrent d’excellentes performances pour les charges de travail HPC et IA à l’aide de noyaux de calcul optimisés pour le GPU CUDA, ainsi que de nombreux outils d’intelligence artificielle et d’analyse prenant en charge l’accélération GPU prêts à l’emploi, tels que TensorFlow, Pytorch, Caffe, Digital et autres infrastructures.

Il est essentiel que NDv2 soit conçu pour répondre à la fois à des charges de travail de scale-up (8 GPU par machine virtuelle) et de scale-out (plusieurs machines virtuelles travaillant ensemble) qui sont gourmandes en calcul. La série NDv2 prend désormais en charge le réseau back-end EDR InfiniBand 100 Gigabits, similaire à celui disponible dans la série HB de HPC VM, afin de permettre un clustering haute performance pour les scénarios parallèles, notamment l’entraînement distribué pour l’IA et le ML. Ce réseau principal prend en charge tous les principaux protocoles InfiniBand, y compris ceux utilisés par les bibliothèques NCCL2 de NVIDIA, ce qui permet une mise en grappe transparente des GPU.


> [!NOTE]
> Lors de l’[activation d’InfiniBand](https://docs.microsoft.com/azure/virtual-machines/workloads/hpc/enable-infiniband) sur la machine virtuelle ND40rs_v2, utilisez le pilote OFED 4.7-1.0.0.1.
>
> En raison de l’augmentation de la mémoire GPU, la nouvelle machine virtuelle ND40rs_v2 nécessite l’utilisation de [deux machines virtuelles Generation](https://docs.microsoft.com/azure/virtual-machines/windows/generation-2) et d’images marketplace. 
>
> [Inscrivez-vous pour demander un accès anticipé à la préversion de l’ordinateur virtuel NDv2.](https://aka.ms/AzureNDrv2Preview)
>
> Notez ce qui suit : Le modèle ND40s_v2 doté de 16 Go de mémoire par GPU n’est plus disponible en préversion et a été remplacé par le modèle ND40rs_v2 mis à jour.

<br>

Premium Storage :  Prise en charge

Mise en cache du Stockage Premium :  Prise en charge

Migration dynamique : Non pris en charge

Mises à jour avec préservation de la mémoire : Non pris en charge

Infiniband Prise en charge

| Taille | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) : Gio | GPU | Mémoire GPU : Gio | Disques de données max. | Débit du disque non mis en cache max. : IOPS / MBps | Bande passante réseau maximale | Nombre max de cartes réseau |
|---|---|---|---|---|---|---|---|---|---|
| Standard_ND40rs_v2 | 40 | 672 | 2948 | 8 V100 32 Go (NVLink) | 16 | 32 | 80000/800 | 24 000 Mbits/s | 8 |

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
