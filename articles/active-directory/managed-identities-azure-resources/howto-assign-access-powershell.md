---
title: Affecter à une identité managée l’accès à une ressource à l’aide de PowerShell - Azure AD
description: Instructions détaillées pour affecter à une identité managée sur une ressource l’accès à une autre ressource à l’aide de PowerShell.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: daveba
editor: ''
ms.service: active-directory
ms.subservice: msi
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/06/2018
ms.author: markvi
ms.collection: M365-identity-device-management
ms.openlocfilehash: a2283ac076ef761fd098d75e7120e6557a959574
ms.sourcegitcommit: a678f00c020f50efa9178392cd0f1ac34a86b767
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74547249"
---
# <a name="assign-a-managed-identity-access-to-a-resource-using-powershell"></a>Affecter à une identité managée l’accès à une ressource à l’aide de PowerShell

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

Après avoir configuré une ressource Azure avec une identité managée, vous pouvez accorder à cette dernière un accès à une autre ressource, tout comme n’importe quel principal de sécurité. Cet exemple montre comment accorder à l’identité managée d’une machine virtuelle Azure l’accès à un compte de stockage Azure, à l’aide de PowerShell.

[!INCLUDE [az-powershell-update](../../../includes/updated-for-az.md)]

## <a name="prerequisites"></a>Prérequis

- Si vous n’êtes pas familiarisé avec les identités managées pour ressources Azure, voir la [section Vue d’ensemble](overview.md). **Veillez à lire [la différence entre les identités managées affectées par le système et celles affectées par l’utilisateur](overview.md#how-does-the-managed-identities-for-azure-resources-work)** .
- Si vous n’avez pas encore de compte Azure, [inscrivez-vous à un essai gratuit](https://azure.microsoft.com/free/) avant de continuer.
- Installez [la dernière version d’Azure PowerShell](/powershell/azure/install-az-ps) si ce n’est déjà fait.

## <a name="use-rbac-to-assign-a-managed-identity-access-to-another-resource"></a>Utiliser RBAC pour affecter à une identité managée l’accès à une autre ressource

Après avoir activé l’identité managée sur une ressource Azure, telle qu’une [machine virtuelle Azure](qs-configure-powershell-windows-vm.md) :

1. Connectez-vous à Azure à l’aide du cmdlet `Connect-AzAccount`. Utilisez un compte associé à l’abonnement Azure sous lequel vous avez configuré l’identité managée :

   ```powershell
   Connect-AzAccount
   ```
2. Dans cet exemple, nous accordons à une machine virtuelle Azure l’accès à un compte de stockage. Tout d’abord, nous utilisons [Get-AzVM](/powershell/module/az.compute/get-azvm) pour obtenir le principal de service pour la machine virtuelle nommée `myVM`, qui a été créé lorsque nous avons activé l’identité managée. Ensuite, utilisez [New-AzRoleAssignment](/powershell/module/Az.Resources/New-AzRoleAssignment) pour accorder à la machine virtuelle un accès de type **Lecteur** vers un compte de stockage appelé `myStorageAcct` :

    ```powershell
    $spID = (Get-AzVM -ResourceGroupName myRG -Name myVM).identity.principalid
    New-AzRoleAssignment -ObjectId $spID -RoleDefinitionName "Reader" -Scope "/subscriptions/<mySubscriptionID>/resourceGroups/<myResourceGroup>/providers/Microsoft.Storage/storageAccounts/<myStorageAcct>"
    ```

## <a name="next-steps"></a>Étapes suivantes

- [Vue d’ensemble de l’identité managée pour les ressources Azure](overview.md)
- Pour activer l’identité managée sur une machine virtuelle Azure, consultez [Configurer des identités managées pour ressources Azure sur une machine virtuelle Azure à l’aide de PowerShell](qs-configure-powershell-windows-vm.md).
