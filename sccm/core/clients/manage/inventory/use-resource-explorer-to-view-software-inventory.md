---
title: "檢視軟體清查 | 資源總管 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中，使用資源總管檢視軟體清查。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b4ecb27cfb119ae80d1ed7d90d84c61a87b183c8


---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>如何使用資源總管檢視 System Center Configuration Manager 的軟體清查

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 中使用資源總管，檢視從階層中電腦所收集的軟體清查相關資訊。  

> [!NOTE]  
>  資源總管要到軟體清查週期在您連線的用戶端上執行過後，才會顯示所有的清查資料。  

 Configuration Manager 中的資源總管包含下列與軟體清查相關的區段：  

-   **軟體** - 資源總管的軟體區段包含四個部分：  

    -   **收集到的檔案** - 顯示在軟體清查期間收集到的檔案相關資訊。  

    -   **檔案詳細資料** - 顯示在軟體清查期間清查到與特定產品或製造商無關聯的檔案相關資訊。  

    -   **上次軟體掃描** - 顯示用戶端電腦上次執行軟體清查和檔案收集的日期和時間。  

    -   **產品詳細資料** - 顯示軟體清查清查到且依製造商分組的軟體產品相關資訊。  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台執行資源總管  
 請使用下列程序在 Configuration Manager 中執行資源總管。  

#### <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台執行資源總管  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [裝置]  或開啟顯示裝置的任何集合。  

3.  按一下您想要檢視、包含清查的電腦，然後在 [首頁]  索引標籤的 [裝置]  群組中，依序按一下 [開始]  和 **資源總管**。 **資源總管** 視窗隨即開啟。  

4.  您可以在 [資源總管] 視窗的右窗格中以滑鼠右鍵按一下任何項目，然後按一下 [內容] 開啟 [*<項目名稱\>* 內容] 對話方塊，其可協助您以更容易閱讀的格式來檢視收集到的清查資訊。  

5.  完成後請關閉 **資源總管** 視窗。  



<!--HONumber=Nov16_HO1-->


