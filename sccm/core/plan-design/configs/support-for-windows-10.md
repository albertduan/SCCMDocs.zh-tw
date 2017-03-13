---
title: "Windows 10 的支援 | Microsoft Docs"
description: "了解哪些 Windows 10 版本支援執行 System Center Configuration Manager 用戶端。"
ms.custom: na
ms.date: 2/10/2017
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
translationtype: Human Translation
ms.sourcegitcommit: 3702993d6cf9644d5aebaadd168749668fbcb62c
ms.openlocfilehash: 4b90384621dd20475ab9ea33ea062c24f5ecf5fa
ms.lasthandoff: 02/22/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>將 Windows 10 作為 System Center Configuration Manager 用戶端的支援

*適用對象：System Center Configuration Manager (最新分支)*


 本主題識別您可用作不同 System Center Configuration Manager 最新分支版本用戶端的 Windows 10 版本。

- 這會補充[用戶端和裝置的支援作業系統](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)。
- 如果您使用 Configuration Manager 長期維護分支，請參閱[支援的長期維護分支設定](/sccm/core/understand/supported-configurations-for-ltsb)。

Configuration Manager 嘗試在該 Windows 版本發行之後盡快支援每個新 Windows 10 版本。 因為產品具有個別的開發和發行排程，所以 Configuration Manager 提供的支援取決於每個產品的版本和分支發行時。  



|Windows 10 版本 |Configuration Manager 1602|Configuration Manager 1606|Configuration Manager 1610|
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB |![支援](media/green_check.png) |![支援](media/green_check.png) |![支援](media/green_check.png) |
|1507 <br />Enterprise、Pro | ![支援](media/green_check.png)| ![支援](media/green_check.png)|![支援](media/green_check.png) |
|1511 <br />Enterprise、Pro <br />(CB)、(CBB) |![支援](media/green_check.png) |![支援](media/green_check.png) |![支援](media/green_check.png) |
|Enterprise 2016 LTSB    |![不支援](media/Red_X.png) |![支援](media/green_check.png) | ![支援](media/green_check.png)|
|1607 <br />Enterprise、Pro<br /> (CB)    |![不支援](media/Red_X.png) |![回溯相容](media/blue_compat.png) |![支援](media/green_check.png) |
|1607 <br />Enterprise、Pro <br />(CBB)    |![不支援](media/Red_X.png) |![回溯相容](media/Red_X.png) |![支援](media/green_check.png) |


|機碼|
|--|
|![支援](media/green_check.png) = **支援**  |
|![不支援](media/blue_compat.png)  = **回溯相容** - 這表示現有用戶端管理功能 (硬體清查、軟體清查、軟體更新等) 應該使用新的 Windows 10 最新分支組建。 將會記載任何已知問題或警示。 <br><br>這種方法可讓您能夠在第一天部署和管理具有應用程式相容性支援的新 Windows 10 CB 組建，而不需要新的 Configuration Manager 更新版本。 |
|![支援](media/Red_X.png) = **不支援**|
