---
title: Intégrer Splunk à l’aide d’Azure Monitor | Microsoft Docs
description: Découvrez comment intégrer des journaux d’activité Azure Active Directory avec SumoLogic à l’aide d’Azure Monitor
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: daveba
editor: ''
ms.assetid: 2c3db9a8-50fa-475a-97d8-f31082af6593
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.subservice: report-monitor
ms.date: 03/10/2020
ms.author: markvi
ms.reviewer: dhanyahk
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2eda3643a7b1a341c7ed664dbfea933145f1f927
ms.sourcegitcommit: 5f39f60c4ae33b20156529a765b8f8c04f181143
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "78968706"
---
# <a name="how-to-integrate-azure-active-directory-logs-with-splunk-using-azure-monitor"></a>Procédure : Intégrer des journaux d’activité Azure Active Directory à Splunk à l’aide d’Azure Monitor

Cet article explique comment intégrer des journaux d’activité Azure Active Directory (Azure AD) avec Splunk à l’aide d’Azure Monitor. Vous commencez pas router les journaux d’activité vers un hub d’événements Azure, puis vous intégrez le hub d’événements avec Splunk.

## <a name="prerequisites"></a>Prérequis

Pour utiliser cette fonctionnalité, vous avez besoin des éléments suivants :

- Un hub d’événements Azure contenant les journaux d’activité d’Azure AD. Découvrez comment [diffuser en continu vos journaux d’activité sur un hub d’événements](quickstart-azure-monitor-stream-logs-to-event-hub.md). 

-  [Module complémentaire Microsoft Azure pour Splunk](https://splunkbase.splunk.com/app/3757/) 

## <a name="integrate-azure-active-directory-logs"></a>Intégrer des journaux d’activité Azure Active Directory 

1. Ouvrez votre instance Splunk, puis sélectionnez **Data Summary** (Synthèse des données).

    ![Bouton « Synthèse des données »](./media/howto-integrate-activity-logs-with-splunk/DataSummary.png)

2. Sélectionnez l’onglet **Sourcetypes**, puis **amal: aadal:audit**

    ![Onglet Sourcetypes de Synthèse des données](./media/howto-integrate-activity-logs-with-splunk/sourcetypeaadal.png)

    Les journaux d’activité d’Azure AD sont présentés dans la figure suivante :

    ![Journaux d’activité](./media/howto-integrate-activity-logs-with-splunk/activitylogs.png)

> [!NOTE]
> Si vous ne pouvez pas installer de module complémentaire dans votre instance Splunk (par exemple, si vous utilisez un proxy ou exécutez sur un cloud Splunk), vous pouvez transférer ces événements au collecteur d’événements HTTP Splunk. Pour ce faire, utilisez cette [fonction Azure](https://github.com/Microsoft/AzureFunctionforSplunkVS) déclenchée par de nouveaux messages dans le hub d’événements. 
>

## <a name="next-steps"></a>Étapes suivantes

* [Interpréter le schéma des journaux d’audit dans Azure Monitor](reference-azure-monitor-audit-log-schema.md)
* [Interpréter le schéma des journaux d’activité de connexion dans Azure Monitor](reference-azure-monitor-sign-ins-log-schema.md)
* [Questions fréquentes et problèmes connus](concept-activity-logs-azure-monitor.md#frequently-asked-questions)