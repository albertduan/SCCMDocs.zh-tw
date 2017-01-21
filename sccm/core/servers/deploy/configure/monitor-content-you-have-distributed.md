---
title: "監視內容 | System Center Configuration Manager"
description: "使用 Configuration Manager 主控台了解如何監視發佈的內容。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 402c06ed92bbfe509206d3e7800e41e90c5d3a38

---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>監視您已使用 System Center Configuration Manager 所發佈的內容

*適用於：System Center Configuration Manager (最新分支)*

使用 System Center Configuration Manager 主控台來監視發佈的內容，包括：  

-   與關聯的發佈點相關之所有封裝類型的狀態。  

-   封裝中內容的內容驗證狀態  

-   指派至特定發佈點群組的內容狀態  

-   指派至發佈點群組的內容狀態  

-   每個發佈點 (內容驗證、PXE 與多點傳送) 的選用功能狀態。  

> [!NOTE]  
>  Configuration Manager 僅監視位於內容庫中之發佈點上的內容。 不會監視儲存在套件或自訂共用中發佈點上的內容。  

##  <a name="a-namebkmkcontentstatusa-content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> 內容狀態監視  
 [監視]  工作區中的 [內容狀態]  節點會提供有關內容套件的資訊。 在 Configuration Manager 主控台中，您可以檢閱下列這類資訊：  

-   封裝名稱  

-   類型  

-   已傳送至套件的發佈點數量  

-   相容率  

-   封裝建立的時間  

-   套件識別碼  

-   來源版本  

您也可以找到任何封裝的詳細狀態資訊，以及封裝的發佈狀態，包括：  

-   失敗次數  

-   擱置的發佈  

-   安裝的數量  

您也可以管理對發佈點持續進行的發佈，或是未能成功將內容發佈到發佈點的發佈：  

-   當您在 [內容狀態]  節點之 [進行中]  索引標籤或 [錯誤]  索引標籤的 [資產詳細資料]  窗格中，檢視對發佈點之發佈工作的部署狀態訊息時，可使用取消或重新發佈內容等適用選項。  

-   此外，當您檢視 [進行中] 索引標籤的工作詳細資料時，該資料會顯示已完成的工作百分比  ，而從 [錯誤]  索引標籤處檢視工作詳細資料時，則會顯示工作重試次數，以及距離下一次重試還有多久時間。  

當您取消尚未完成的部署時，傳送該內容的發佈工作會停止進行：  

-   部署的狀態會接著更新，指出發佈失敗，並已因使用者的動作而被取消。  

-   此新狀態會出現在 [錯誤]  索引標籤處。  

> [!TIP]  
>  當部署作業接近完成時，取消該發佈的動作可能不會在完成發佈點的發佈作業之前進行。 萬一發生了，就會忽略取消部署的動作，而部署狀態會顯示為成功。  

> [!NOTE]  
>  雖然您可以選擇取消針對位於站台伺服器的發佈點進行發佈的選項，但這麼做是無效的。 這是因為站台伺服器和站台伺服器上的發佈點共用相同的單一執行個體內容存放區，但實際上並沒有可取消的發佈工作。  

當您重新發佈之前失敗的內容以傳送到發佈點時，Configuration Manager 會立即開始將該內容再次部署到發佈點，並且會更新部署狀態以反映該重新部署的進行中狀態。  

使用下列程序可檢視內容狀態，並可管理仍在進行中或已失敗的發佈作業。  

#### <a name="to-monitor-content-status"></a>若要監視內容狀態  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [發佈狀態] ，然後按一下 [內容狀態] 。 套件便會顯示。  

3.  選取需要其詳細狀態資訊的套件。  

4.  在 [首頁]  索引標籤上，按一下 [檢視狀態] 。 套件的詳細狀態資訊隨即顯示。  

#### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>取消仍在進行中的發佈作業  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [發佈狀態] ，然後按一下 [內容狀態] 。 套件便會顯示。  

3.  選取您要管理的套件，然後在詳細資料窗格中按一下 [檢視狀態] 。  

4.  在 [進行中] 索引標籤的 [資產詳細資料]  窗格中，  ，以滑鼠右鍵按一下您要取消之發佈項目，然後選取 [取消] 。  

5.  按一下 [是]  確認動作，並取消對於該發佈點的發佈工作。  

#### <a name="to-redistribute-content-that-failed-to-distribute"></a>重新發佈無法發佈的內容  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [發佈狀態] ，然後按一下 [內容狀態] 。 套件便會顯示。  

3.  選取您要管理的套件，然後在詳細資料窗格中按一下 [檢視狀態] 。  

4.  在 [錯誤] 索引標籤的 [資產詳細資料]  窗格中，  ，以滑鼠右鍵按一下您要重新發佈之發佈項目，然後選取 [重新發佈] 。  

5.  按一下 [是]  確認動作，並開始進行對於該發佈點的重新發佈程序。  

## <a name="distribution-point-group-status"></a>發佈點群組狀態  
[監視]  工作區中的 [發佈點群組狀態]  節點會提供有關發佈點群組的資訊。 您可以檢閱如下列的資訊：  

-   發佈點群組名稱  

-   說明  

-   屬於發佈點群組的發佈點數目  

-   已指派至群組的封裝數目  

-   發佈點群組狀態  

-   相容率  

您也可以檢視下列項目的詳細狀態資訊：  

-   發佈點群組的錯誤  

-   正在進行中的發佈數目  

-   已成功發佈的數目  

#### <a name="to-monitor-distribution-point-group-status"></a>若要監視發佈點群組狀態  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [發佈狀態] ，然後按一下 [發佈點群組狀態] 。 發佈點群組隨即顯示。  

3.  選取需要其詳細狀態資訊的發佈點群組。  

4.  在 [首頁]  索引標籤上，按一下 [檢視狀態] 。 發佈點群組的詳細狀態資訊隨即顯示。  

## <a name="distribution-point-configuration-status"></a>發佈點設定狀態  
 [監視]  工作區中的 [發佈點設定狀態]  節點會提供有關發佈點的資訊。 您可以檢閱已啟用的發佈點屬性，例如 PXE、多點傳送及內容驗證，以及發佈點的發佈狀態。 您也可以檢視發佈點的詳細狀態資訊。  

> [!WARNING]  
>  發佈點設定狀態是指過去 24 小時的相對狀態。 如果發佈點發生錯誤而後復原，錯誤狀態會在發佈點復原後最多顯示 24 小時。  

利用下列程序可檢視發佈點設定狀態。  

#### <a name="to-monitor-distribution-point-configuration-status"></a>若要監視發佈點設定狀態  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [發佈狀態] ，然後按一下 [發佈點設定狀態] 。 發佈點隨即顯示。  

3.  選取需要其發佈點狀態資訊的發佈點群組。  

4.  在結果窗格中，按一下 [詳細資料]  索引標籤。 發佈點的狀態資訊隨即顯示。  



<!--HONumber=Nov16_HO1-->


