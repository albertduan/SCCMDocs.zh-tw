---
title: "排除資料夾不進行軟體清查 | Microsoft Docs"
description: "在 System Center Configuration Manager 中排除資料夾不進行軟體清查。"
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6d1aabbde576f01de920468fd3ef372bd23be9df
ms.openlocfilehash: 7850b69cdccb0e897ee71b75255004bdc8d0ae97


---
# <a name="how-to-exclude-folders-from-software-inventory-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中排除資料夾不進行軟體清查

*適用於：System Center Configuration Manager (最新分支)*

 這個程序可設定軟體清查的預設用戶端設定，並套用到階層中的所有電腦。 如果您只想將這些設定套用至某些電腦，請建立自訂裝置用戶端設定，並將它指派給包含您要使用軟體清查之電腦的集合。 如需如何建立自訂裝置設定的詳細資訊，請參閱 [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md) (如何在 System Center Configuration Manager 中設定用戶端設定)。  

### <a name="to-configure-software-inventory"></a>設定軟體清查  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [用戶端設定] [預設用戶端設定]。  

4.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

5.  在 [預設設定] 對話方塊中，選擇 [軟體清查]。  

6.  在 [裝置設定]  清單中，設定下列值：  

    -   **在用戶端上啟用軟體清查** - 從下拉式清單中選取 [True]。  

    -   **排程軟體清查和檔案收集** - 設定用戶端收集軟體清查和檔案的間隔。   

7.  設定您需要的用戶端設定。 如需可供設定的軟體清查用戶端設定清單，請參閱[關於 Configuration Manager 中的用戶端設定](../../../../core/clients/deploy/about-client-settings.md)主題的[軟體清查](../../../../core/clients/deploy/about-client-settings.md#software-inventory)一節。  

 用戶端電腦將會在下一次下載用戶端原則時進行這些設定。 若要起始單一用戶端的原則擷取，請參閱 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  



<!--HONumber=Dec16_HO3-->


