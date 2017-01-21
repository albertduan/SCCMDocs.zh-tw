---
title: "使用維護期間 | System Center Configuration Manager"
description: "使用集合和維護期間，在 System Center Configuration Manager 中有效率地管理用戶端。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c29d8a1bc0d224113a1c906893308d5582894a01


---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>如何使用 System Center Configuration Manager 的維護視窗

*適用於：System Center Configuration Manager (最新分支)*

對裝置集合成員執行各種 Configuration Manager 作業時，Configuration Manager 的維護期間提供系統管理使用者一種定義時段的方法。 您可以藉助維護視窗，確保用戶端組態變更發生的時段不會影響組織的產能。  

 下列 Configuration Manager 作業支援維護期間：  

-   軟體部署  

-   軟體更新部署  

-   相容性設定部署和評估  

-   作業系統部署  

-   工作順序部署  

 維護期間的設定包含開始日期、開始和結束時間，以及定期模式。 每一個維護期間的持續時間都必須少於 24 小時。 根據預設，部署造成電腦重新啟動的行為不允許出現在維護視窗之外，但是您可以在每個部署的設定中覆寫預設值。 維護視窗只會影響部署程式執行的時間，而設定在本機上下載及執行的應用程式可以在維護視窗之外下載內容。  

 如果用戶端電腦是已設定維護視窗的裝置集合成員，則部署程式只會在允許的執行時間上限未超過針對維護視窗設定的持續時間時執行。 如果程式執行失敗，將會產生警示，且部署將會在下一次排程的維護視窗有可用時間時重新執行。  

## <a name="using-multiple-maintenance-windows"></a>使用多個維護視窗  
 如果用戶端電腦是已設定維護期間的多個裝置集合的成員，則適用下列規則：  

-   如果維護期間未重疊，則會視為兩個獨立的維護期間。  

-   如果維護期間重疊，則會視為包含兩個維護期間所涵蓋時段的單一維護期間。 例如，如果兩個維護期間的持續時間各為一小時，其中有 30 分鐘重疊，則維護期間的有效持續時間會是 90 分鐘。  

 當使用者從軟體中心起始應用程式安裝時，應用程式將會立即安裝，而不理會任何已設定的維護視窗。  

 如果在軟體中心使用者設定的非營業時間裡，有 **必要** 目的的應用程式部署面臨安裝期限，就會安裝應用程式。  

### <a name="how-to-configure-maintenance-windows"></a>如何設定維護視窗  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [裝置集合] 。  

3.  在 [裝置集合]  清單中，選取要設定維護期間的集合。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  在 [&lt;集合名稱\> 內容] 對話方塊的 [維護期間] 索引標籤中，按一下 [新增] 圖示。  

    > [!NOTE]  
    >  您無法為 [所有系統]  集合建立維護期間。  

6.  在 [&lt;新增\> 排程] 對話方塊中，指定維護期間的名稱、排程及定期模式。 您也可以啟用選項只對工作順序套用排程。  

7.  從 [將此排程套用至]  下拉式清單中，選取將這個維護視窗套用至所有部署、僅套用至軟體更新，或僅套用至工作順序。  

8.  按一下 [確定] 關閉 [&lt;新增\> 排程] 對話方塊，並建立新的維護期間。  

9. 關閉 [&lt;集合名稱\> 內容] 對話方塊。  



<!--HONumber=Nov16_HO1-->


