---
title: "集合必要條件 | Microsoft Docs"
description: "取得在 System Center Configuration Manager 中使用集合的必要條件。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: 7
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 81342ab0d064e3f2da19126819bdd048270a4320


---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager 中集合的必要條件

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的集合只包含產品內的相依性。  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  

|相依性|詳細資訊|  
|----------------|----------------------|  
|Reporting Services 點|必須先安裝 Reporting Services 點站台系統角色，才能執行集合的報告。 如需詳細資訊，請參閱 [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md) (System Center Configuration Manager 中的報告)。|  
|若要管理集合，必須授與特定的安全性權限。|您必須具備下列安全性權限，才能管理相容性設定：<br /><br /> - 建立和管理集合：[集合] 物件的 [建立]、[刪除]、[修改]、[修改資料夾]、[移動物件]、[讀取] 和 [讀取資源]。<br /><br /> - 管理集合設定：[集合] 物件的 [修改集合設定]。<br /><br /> 需要所有集合資料夾 (包括根資料夾) 的 [修改資料夾]  權限。|  



<!--HONumber=Dec16_HO3-->


