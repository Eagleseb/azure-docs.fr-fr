---
title: Versions prises en charge – Azure Database pour MySQL
description: Découvrez les versions du serveur MySQL qui sont prises en charge dans le service Azure Database pour MySQL.
author: ajlam
ms.author: andrela
ms.service: mysql
ms.topic: conceptual
ms.date: 12/12/2019
ms.openlocfilehash: 05d4ecd58f6febff75212f1ad88b60be4f23c2a7
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75454330"
---
# <a name="supported-azure-database-for-mysql-server-versions"></a>Versions prises en charge du serveur de base de données Azure pour MySQL

Azure Database for MySQL a été développé à partir de [MySQL Community Edition](https://www.mysql.com/products/community/), avec le moteur InnoDB.

MySQL utilise le schéma de nommage X.Y.Z. X correspond à la version majeure, Y à la version mineure et Z à la version du correctif de bogue. Pour plus d’informations sur ce schéma, reportez-vous à la [documentation MySQL](https://dev.mysql.com/doc/refman/5.7/en/which-version.html).

> [!NOTE]
> Dans le service, une passerelle est utilisée pour rediriger les connexions vers des instances de serveur. Une fois la connexion établie, le client de MySQL affiche la version de MySQL définie dans la passerelle, et non la version en cours d’exécution sur votre instance de serveur MySQL. Pour déterminer la version de votre instance de serveur MySQL, utilisez la commande `SELECT VERSION();` à l’invite de MySQL.

Azure Database pour MySQL prend actuellement en charge les versions suivantes :

## <a name="mysql-version-56"></a>MySQL version 5.6

Version du correctif de bogue : 5.6.45

Pour plus d’informations sur les améliorations et les correctifs de cette version, consultez les [notes de publication](https://dev.mysql.com/doc/relnotes/mysql/5.6/en/news-5-6-45.html) MySQL.

## <a name="mysql-version-57"></a>MySQL version 5.7

Version du correctif de bogue : 5.7.27

Pour plus d’informations sur les améliorations et les correctifs de cette version, consultez les [notes de publication](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-27.html) MySQL.

## <a name="mysql-version-80"></a>MySQL Version 8.0

Version du correctif de bogue : 8.0.15

Pour plus d’informations sur les améliorations et les correctifs de cette version, consultez les [notes de publication](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-15.html) MySQL.

## <a name="managing-updates-and-upgrades"></a>Gestion des mises à jour et des mises à niveau
Le service gère automatiquement les correctifs pour les mises à jour des versions des correctifs de bogues. Par exemple, 5.7.20 à 5.7.21.  

Les mises à niveau des versions majeures et mineures ne sont pas prises en charge. Par exemple, il n’est pas possible de mettre à niveau MySQL 5.6 vers MySQL 5.7. Si vous voulez effectuer une mise à niveau de 5.6 vers 5.7, prenez une [image mémoire et restaurez-la](./concepts-migrate-dump-restore.md) sur un serveur créé avec la nouvelle version du moteur.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les quotas de ressources et les limitations associés à votre **niveau de service**, consultez la page [Niveaux de service](./concepts-pricing-tiers.md).
