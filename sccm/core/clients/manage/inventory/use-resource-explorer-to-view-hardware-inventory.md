---
title: "檢視硬體清查 | 資源總管 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中，使用資源總管檢視硬體清查。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 12bf49b6a68d277c7f505ddfe37556363d0e3e53


---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>如何使用資源總管檢視 System Center Configuration Manager 中的硬體清查

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 中使用資源總管，檢視從階層中用戶端所收集的硬體清查相關資訊。  

> [!NOTE]  
>  資源總管不會顯示資料直到硬體清查週期已在用戶端執行您要連接到任何清查。  

 Configuration Manager 中的資源總管包含下列與硬體清查相關的區段：  

-   **硬體** - 包含從指定的 Configuration Manager 用戶端裝置收集來的最新硬體清查。 您可以檢閱庫存項目 **工作站狀態** 來探索裝置上次執行硬體清查的日期和時間。  

-   **硬體歷程記錄** - 包含上次執行硬體清查後所變更的清查項目之歷程記錄。 清單中的每個項目都包含**目前**節點以及一或多個 < 日期\> 節點。 您可以比較目前節點的其中一個來探索用戶端電腦的硬體清查中已變更的項目歷程記錄的節點中的資訊。  

    > [!NOTE]  
    >  Configuration Manager 會將硬體清查歷程記錄，保留 [刪除過時清查歷程記錄] 站台維護工作中所指定的天數  

> [!NOTE]  
>  如需如何檢視執行 Linux 與 UNIX 之用戶端的硬體清查資訊，請參閱 [How to monitor clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md)。  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>如何從 Configuration Manager 主控台執行資源總管  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [裝置]  或開啟顯示裝置的任何集合。  

3.  按一下您想要檢視、包含清查的電腦，然後在 [首頁]  索引標籤的 [裝置]  群組中，依序按一下 [開始]  和 **資源總管**。 **資源總管** ] 視窗隨即開啟。  

4.  您可以在 **[資源總管]** 視窗的右窗格中，於任一項目上按一下滑鼠右鍵，然後按一下 **[內容]** 開啟 [<項目名稱\>**內容]** 對話方塊，其可協助您以更容易閱讀的格式來檢視收集到的清查資訊。  

5.  完成後請關閉 **資源總管** 視窗。  



<!--HONumber=Nov16_HO1-->


