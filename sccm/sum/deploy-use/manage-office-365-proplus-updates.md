---

title: "管理 Office 365 ProPlus 更新 | Configuration Manager"
description: "Configuration Manager 會將 Office 365 用戶端更新從 WSUS 類別目錄同步處理至站台伺服器，讓更新能夠部署至用戶端。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 58a551425591332264592713fa3cc4e04d9939aa


---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>使用 Configuration Manager 管理 Office 365 ProPlus 更新

*適用對象：System Center Configuration Manager (最新分支)*

從 Configuration Manager 1602 版開始，Configuration Manager 能夠使用軟體更新管理工作流程來管理 Office 365 用戶端更新。 當 Microsoft 將新的 Office 365 用戶端更新發佈至 Office 內容傳遞網路 (CDN) 時，Microsoft 也會將更新套件發佈至 Windows Server Update Services (WSUS)。 當 Configuration Manager 將 Office 365 用戶端更新從 WSUS 類別目錄同步處理至站台伺服器之後，更新就可以部署至用戶端。

#### <a name="to-deploy-office-365-updates-with-configuration-manager"></a>使用 Configuration Manager 部署 Office 365 更新
使用下列步驟以 Configuration Manager 部署 Office 365 更新：

1.  [確認需求](https://technet.microsoft.com/library/mt628083.aspx)：請見主題的＜使用 Configuration Manager 管理 Office 365 用戶端更新的需求＞一節中有關使用 Configuration Manager 管理 Office 365 用戶端更新的需求。  

2.  [設定軟體更新點](../get-started/configure-classifications-and-products.md)，以同步處理 Office 365 用戶端更新。 設定分類的 [更新]，然後針對產品選取 [Office 365 用戶端]。 您可能必須至少同步處理一次軟體更新，才有 Office 365 用戶端產品可供選擇。 設定軟體更新點使用 [更新] 分類之後，必須同步處理軟體更新。  

3.  啟用 Office 365 用戶端從 Configuration Manager 接收更新。 您可以使用 Configuration Manager 用戶端設定來執行這項操作，或使用群組原則。 使用下列方法之一啟用用戶端：  
    - 方法 1︰從 Configuration Manager 1606 版開始，您可以使用 Configuration Manager 用戶端設定來管理 Office 365 用戶端代理程式。 在設定這項設定並部署 Office 365 更新之後，Configuration Manager 用戶端代理程式會與 Office 365 用戶端代理程式進行通訊，從發佈點下載 Office 365 更新並安裝它們。 Configuration Manager 採用 Office 365 ProPlus 用戶端的清查設定。
      1.  在 Configuration Manager 主控台中，按一下 [管理] > [概觀] > [用戶端設定]。  

      2.  開啟適當的裝置設定，以啟用用戶端代理程式。 如需預設和自訂用戶端設定的詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。  

      3.  按一下 [軟體更新]，然後針對 [啟用管理 Office 365 用戶端代理程式] 設定選取 [是]。  

    - 方法 2：使用 Office 部署工具或使用群組原則，[啟用 Office 365 用戶端以從 Configuration Manager 接收更新](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient)。  

4. [部署 Office 365 更新](deploy-software-updates.md)至用戶端。  



<!--HONumber=Nov16_HO1-->


