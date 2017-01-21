---
title: "診斷資料常見問題集 | System Center Configuration Manager"
description: "尋找與 System Center Configuration Manager 的診斷和使用方式資料有關的常見問題集。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f5d0bf6215e827b58dcbc4a64c509c2f07b44815


---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>與 System Center Configuration Manager 的診斷和使用方式資料有關的常見問題集

*適用於：System Center Configuration Manager (最新分支)*

以下是與 System Center Configuration Manager 的診斷和使用方式資料有關的常見問題集：  

###  <a name="a-namebkmkoffa-how-do-i-turn-off-telemetry"></a><a name="bkmk_off"></a> 如何關閉遙測？  
 Configuration Manager 的最新分支需要定期更新，才能支援新版的 Windows 10 和 Microsoft Intune。 Microsoft 至少需要「基本」層級的診斷和使用方式資料，才能確保產品保持在最新狀態、改善更新體驗，以及提升產品的品質和安全性。  

###  <a name="a-namebkmkretentiona-what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> 什麼是資料保留期間？  
 診斷和使用方式資料會保留一年。  

###  <a name="a-namebkmkupdatea-is-diagnostics-and-usage-data-sent-when-installing-or-updating-the-product"></a><a name="bkmk_update"></a> 安裝或更新產品時，是否會傳送診斷和使用方式資料？  
 不會。 只有在安裝完站台並正常運作之後，才會傳送診斷和使用方式資料。  

###  <a name="a-namebkmkfrequencya-how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> 多久傳送一次資料？  
 SQL 預存程序每 7 天執行一次 (從安裝站台的那天算起)。 在線上模式中，服務連接點是設定為在執行查詢之後上傳資料。 在離線模式中，系統管理員會使用服務連線工具來上傳資料。 (注意︰資料一開始並不可供離線使用，必須等到安裝完站台 7 天後，才可供離線使用。)  

###  <a name="a-namebkmknetworka-can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> 是否可以使用資料來形成網路地圖？  
 如 System Center Configuration Manager 的診斷使用方式資料收集層級描述中所示，站台詳細資料包括每個站台的時區資訊。 這可讓您深入了解階層中站台的廣泛地理位置和全球散佈情況。 不過，並不會收集任何網路詳細資料，例如 IP 位址或更詳細的地理資訊。
 - [1511 的診斷資料](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [1602 的診斷資料](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [1606 的診斷資料](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)


###  <a name="a-namebkmktablesa-can-you-see-data-in-custom-tables"></a><a name="bkmk_tables"></a> 您是否可以看到自訂資料表中的資料？  
 不會。 收集診斷和使用方式資料時，是透過 SQL 預存程序依據資料庫中的預設產品資料表 (首碼皆為 **TEL_**) 來收集。 在進行 SQL 結構描述偵測查詢的過程中，所有資料表名稱都會經過雜湊處理，以便與已知的預設值做比較。 這可以判斷自訂資料表存在於資料庫中 (資料庫結構描述延伸自預設值)，但無法判斷這些資料表內包含的任何資料。  

###  <a name="a-namebkmkdatabasesa-can-you-see-names-of-other-databases-or-data-in-other-databases"></a><a name="bkmk_databases"></a> 您是否可以看到其他資料庫的名稱或其他資料庫中的資料？  
 不會。 用來收集資料的預存程序會被限制在站台資料庫。  

## <a name="see-also"></a>另請參閱  
 [System Center Configuration Manager 的診斷和使用方式資料](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)



<!--HONumber=Nov16_HO1-->


