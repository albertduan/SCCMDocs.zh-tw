---
title: "診斷和使用方式資料 | System Center Configuration Manager"
description: "了解 System Center Configuration Manager 所收集關於本身的診斷及使用方式資料。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 996efaeb89926b04d2f071cf600dcf45bd2edc89


---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>System Center Configuration Manager 的診斷和使用方式資料

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 會收集與其本身相關的診斷和使用方式資料，Microsoft 會使用這些資料來改進未來版本的安裝體驗、品質及安全性。  

 診斷和使用方式資料已針對每個 System Center Configuration Manager 階層啟用。 它是由每週在每個主要站台和管理中心網站上執行的 SQL Server 查詢所組成。 當階層使用管理中心網站時，系統會從主要站台將資料複寫到該站台。 在您階層的頂層站台，服務連接點會在檢查更新時提交此資訊。 如果服務連接點處於離線模式，則會使用服務連線工具來傳送此資訊。  

> [!NOTE]  
>  Configuration Manager 只會從站台的 SQL Server 資料庫收集資料，而不會直接從用戶端或站台伺服器收集資料。  

 如需詳細資訊，請參閱 [System Center Configuration Manager 隱私權聲明](http://go.microsoft.com/fwlink/?LinkID=626527)。  

 請透過下列主題深入了解 System Center Configuration Manager 的診斷和使用方式資料：  

-   [診斷和使用方式資料如何用於 System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   診斷使用方式資料收集層級：
    - [1511 的診斷資料](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
    - [1602 的診斷資料](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [1606 的診斷資料](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)  
    

-   [System Center Configuration Manager 如何收集診斷和使用方式資料](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [如何檢視 System Center Configuration Manager 的診斷和使用方式資料](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [適用於 System Center Configuration Manager 的客戶經驗改進計畫 (CEIP)](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

-   [與 System Center Configuration Manager 的診斷和使用方式資料有關的常見問題集](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>另請參閱  
 [關於 System Center Configuration Manager 中的服務連線點](../../../core/servers/deploy/configure/about-the-service-connection-point.md)



<!--HONumber=Nov16_HO1-->

