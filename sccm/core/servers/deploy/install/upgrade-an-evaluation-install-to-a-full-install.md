---
title: "升級評估安裝 | System Center Configuration Manager"
description: "了解如何將 System Center Configuration Manager 的評估安裝升級至完整安裝。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0ad15c0caddeb3c200b8c663631d2993a338c7c8

---
# <a name="upgrade-an-evaluation-install-of-system-center-configuration-manager-to-a-full-install"></a>將 System Center Configuration Manager 的評估安裝升級至完整安裝

*適用於：System Center Configuration Manager (最新分支)*



 如果安裝的是 System Center Configuration Manager 評估版，則在 180 天之後，Configuration Manager 主控台會變成唯讀，直到您在安裝程式的 [站台維護] 頁面中啟用產品為止。 在 180 天期間之前或之後的任何時間，您都可以選擇將評估安裝升級為完整安裝。  

> [!NOTE]  
>  將 Configuration Manager 主控台連線至 Configuration Manager 的評估安裝時，主控台標題列會顯示評估安裝到期前的剩餘天數。 天數不會自動重新整理，只有在您重新連線到網站時才會更新。  

 **您可以升級下列執行評估安裝的站台：**  

-   管理中心網站  

-   主要網站  

由於次要網站不被視為評估安裝，在主要網站升級為完整安裝之後，您不需要修改次要網站。  

**將評估版升級為完整版的必要條件：**  

-   進行升級時必須具備有效的產品  

-   您的帳戶對於站台安裝所在的電腦，必須具有 **系統管理員** 權限。  

### <a name="to-upgrade-an-evaluation-edition-of-configuration-manager-to-a-licensed-edition"></a>將 Configuration Manager 評估版升級為授權版  

1.  在站台伺服器上，從 Configuration Manager 安裝資料夾 (**%path%\BIN\X64**) 中找到並執行 **SETUP.exe** (Configuration Manager 安裝程式)。  因為當您從安裝媒體執行安裝程式時無法使用站台維護選項，所以您必須執行位於站台伺服器之 Configuration Manager 資料夾中的安裝程式複本。  

2.  在 [ **開始之前** ] 頁面上，按 [ **下一步**]。  

3.  在 [開始使用]  頁面上，選取 [執行網站維護或重設此網站] ，然後按 [下一步] 。  

4.  在 [站台維護]  頁面上，選取 [將評估版升級為授權版] ，輸入有效的產品金鑰，然後按一下 [下一步] 。  

5.  在 [Microsoft 軟體授權條款]  頁面上，閱讀並接受授權條款，然後按 [下一步] 。  

6.  在 [設定]  頁面上，按一下 [關閉]  以完成精靈。  

    > [!NOTE]  
    >  仍然連線至所升級站台之 Configuration Manager 主控台的標題列，在將主控台重新連線至站台之前，可能會指出該站台仍是評估版。  



<!--HONumber=Nov16_HO1-->


