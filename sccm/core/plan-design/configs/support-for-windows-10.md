---
title: "Windows 10 的支援 | Microsoft Docs"
description: "針對搭配 System Center Configuration Manager 做為用戶端或用於 OSD 的狀況，了解支援的 Windows 10 版本。"
ms.custom: na
ms.date: 05/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: f809c9327db9f298168674add2d09820fdecd1b8
ms.openlocfilehash: ed5efcf7b305f8bee6e99e00c5285f6ae7033d82
ms.contentlocale: zh-tw
ms.lasthandoff: 05/17/2017

---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>System Center Configuration Manager 的 Windows 10 支援  

*適用於：System Center Configuration Manager (最新分支)*


 本主題詳細說明您可搭配不同 System Center Configuration Manager 最新分支版本使用的 Windows 10 版本。 這包括：
 -  做為 Configuration Manager 用戶端的 Windows 10。
 -  Windows 10 Windows 評定及部署套件 (ADK)。

## <a name="windows-10-as-a-client"></a>做為用戶端的 Windows 10
Configuration Manager 會在每個新 Windows 10 版本發行之後，盡快支援新版本做為用戶端。 因為產品具有個別的開發和發行排程，所以 Configuration Manager 提供的支援取決於每個產品的版本和分支發行時。

例如，當某個 Configuration Manager 版本的[版本支援終止](/sccm/core/servers/manage/current-branch-versions-supported)之後，該版本將會從矩陣中卸除。 同樣地，當 Windows 10 版本的支援 (例如企業版 2015 長期維護分支或 1607 (CBB)) 從 Configuration Manager 支援組態清單中移除時，這些版本將會從矩陣中卸除。 如需詳細資訊，請參閱[已淘汰的作業系統](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems)。

-   以下資訊會補充說明[用戶端和裝置的支援作業系統](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)。
-   如果您使用 Configuration Manager 長期維護分支，請參閱[支援的長期維護分支設定](/sccm/core/understand/supported-configurations-for-ltsb)。

|Windows 10 版本                    |Configuration Manager 1606          |Configuration Manager 1610          |    Configuration Manager 1702 |
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB                   |![支援](media/green_check.png) |![支援](media/green_check.png) |![支援](media/green_check.png) |
|1507 <br />(請參閱版本)            |![支援](media/green_check.png) |![支援](media/green_check.png) |![支援](media/green_check.png) |
|1511 (CB)、(CBB)<br />(請參閱版本) |![支援](media/green_check.png) |![支援](media/green_check.png) |![支援](media/green_check.png) |
|Enterprise 2016 LTSB                   |![支援](media/green_check.png) |![支援](media/green_check.png) |![支援](media/green_check.png) |
|1607 (CB)    <br />年度更新版<br />(請參閱版本)      |![回溯相容](media/blue_compat.png) |![支援](media/green_check.png) |![支援](media/green_check.png) |
|1607 (CBB)    <br />年度更新版<br />(請參閱版本)      |![不支援](media/Red_X.png)   |![支援](media/green_check.png) |![支援](media/green_check.png) |
|1703 (CB)    <br />Creators Update<br />(請參閱版本)      |![不支援](media/Red_X.png)   |![不支援](media/Red_X.png) |![回溯相容](media/blue_compat.png) |


**版本：**企業版、專業版、教育版、專業教育版   

|機碼|
|--|
|![支援](media/green_check.png) = **支援**  |
|![不支援](media/blue_compat.png)  = **回溯相容** - 這表示現有用戶端管理功能 (硬體清查、軟體清查、軟體更新等) 應該使用新的 Windows 10 最新分支組建。 將會記載任何已知問題或警示。 <br><br>這種方法可讓您能夠在第一天部署和管理具有應用程式相容性支援的新 Windows 10 CB 組建，而不需要新的 Configuration Manager 更新版本。 |
|![支援](media/Red_X.png) = **不支援**|


## <a name="windows-10-adk"></a>Windows 10 ADK
當您使用 Configuration Manager 部署作業系統時，[Windows ADK 是必要的外部相依性](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。

下表列出可搭配不同 Configuration Manager 版本使用的 Windows 10 ADK 版本。

|Windows 10 ADK 版本 |Configuration Manager 1606 |Configuration Manager 1610  |Configuration Manager 1702 |
|--------------------|-----|-----|-----|
|1507  |![不支援](media/Red_X.png)         |![不支援](media/Red_X.png)  |![不支援](media/Red_X.png)|
|1511  |![回溯相容](media/blue_compat.png)|![不支援](media/Red_X.png)  |![不支援](media/Red_X.png)|
|1607  |![支援](media/green_check.png)       |![支援](media/green_check.png)|![回溯相容](media/blue_compat.png) |
|1703  |![不支援](media/Red_X.png)         |![不支援](media/Red_X.png)  |![支援](media/green_check.png) |  

|機碼|
|--|
|![支援](media/green_check.png) = **支援** - Windows 建議使用符合您要部署之 Windows 版本的 Windows ADK。 例如，部署 Windows 10 1703 版時，使用適用於 Windows 10 1703 版的 Windows ADK。  |
|![回溯相容](media/blue_compat.png)  = **回溯相容** - 此組合未經測試，但應可運作。 將會記載任何已知問題或警示。 |
|![支援](media/Red_X.png) = **不支援**|

