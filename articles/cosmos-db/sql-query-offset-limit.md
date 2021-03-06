---
title: Clause OFFSET LIMIT dans Azure Cosmos DB
description: Découvrez comment utiliser la clause OFFSET LIMIT pour ignorer et prendre certaines valeurs lors d’un requête dans Azure Cosmos DB.
author: timsander1
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 06/10/2019
ms.author: mjbrown
ms.openlocfilehash: 3d23676885323e370cee1e9cc9e98c7128faf2e0
ms.sourcegitcommit: 984c5b53851be35c7c3148dcd4dfd2a93cebe49f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76771567"
---
# <a name="offset-limit-clause-in-azure-cosmos-db"></a>Clause OFFSET LIMIT dans Azure Cosmos DB

La clause OFFSET LIMIT est une clause facultative qui indique à la requête de récupérer un certain nombre de valeurs après en avoir ignorées. Le nombre OFFSET et le nombre LIMIT sont obligatoires dans la clause OFFSET LIMIT.

Quand OFFSET LIMIT est utilisé conjointement avec une clause ORDER BY, la requête génère le jeu de résultats en ignorant certaines valeurs, puis en récupérant certaines valeurs en les classant. Si aucune clause ORDER BY n’est utilisée, l’ordre des valeurs est déterministe.

## <a name="syntax"></a>Syntaxe
  
```sql  
OFFSET <offset_amount> LIMIT <limit_amount>
```  
  
## <a name="arguments"></a>Arguments

- `<offset_amount>`

   Spécifie le nombre entier d’éléments que doivent ignorer les résultats de la requête.

- `<limit_amount>`
  
   Spécifie le nombre entier d’éléments que doivent inclure les résultats de la requête

## <a name="remarks"></a>Notes
  
  Le nombre `OFFSET` et le nombre `LIMIT` sont requis dans la clause `OFFSET LIMIT`. Si une clause `ORDER BY` facultative est utilisée, la requête génère le jeu de résultats en classant d’abord les valeurs avant d’en ignorer et conserver les nombres indiqués. Sinon, la requête retourne un ordre fixe de valeurs.

  Les frais d’unité de requête pour une requête avec `OFFSET LIMIT` augmente au fur et à mesure que le nombre de termes Offset augmente. Pour les requêtes affichant plusieurs pages de résultats, nous recommandons généralement d’utiliser des jetons de continuation. Les jetons de continuation sont un « signet » indiquant l’endroit où la requête pourra reprendre. Si vous utilisez `OFFSET LIMIT`, il n’y a aucun « signet ». Si vous souhaitez retourner à la page suivante de la requête, il vous faudrait commencer au début.
  
  Vous devez utiliser `OFFSET LIMIT` lorsque vous souhaitez ignorer des documents entiers et enregistrer des ressources du client. Par exemple, utilisez `OFFSET LIMIT` si vous souhaitez passer au millième résultat de la requête et que vous n’avez pas besoin d’afficher les résultats compris entre 1 et 999. Sur le serveur principal, `OFFSET LIMIT` charge toujours chaque document, y compris ceux qui sont ignorés. L’avantage, pour ce qui est de la performance, est que cela permet d’économiser les ressources du client en évitant de traiter des documents qui ne sont pas nécessaires.

## <a name="examples"></a>Exemples

Par exemple, voici une requête qui ignore la première valeur et retourne la deuxième valeur (dans l’ordre du nom de la ville de résidence) :

```sql
    SELECT f.id, f.address.city
    FROM Families f
    ORDER BY f.address.city
    OFFSET 1 LIMIT 1
```

Les résultats sont :

```json
    [
      {
        "id": "AndersenFamily",
        "city": "Seattle"
      }
    ]
```

Voici une requête qui ignore la première valeur et retourne la deuxième valeur (sans classement) :

```sql
   SELECT f.id, f.address.city
    FROM Families f
    OFFSET 1 LIMIT 1
```

Les résultats sont :

```json
    [
      {
        "id": "WakefieldFamily",
        "city": "Seattle"
      }
    ]
```

## <a name="next-steps"></a>Étapes suivantes

- [Bien démarrer](sql-query-getting-started.md)
- [Clause SELECT](sql-query-select.md)
- [Clause ORDER BY](sql-query-order-by.md)
