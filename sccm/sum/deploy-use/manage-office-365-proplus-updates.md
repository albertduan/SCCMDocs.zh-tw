---
title: "管理 Office 365 ProPlus 更新 | Microsoft Docs"
description: "Configuration Manager 會將 Office 365 用戶端更新從 WSUS 類別目錄同步處理至站台伺服器，讓更新能夠部署至用戶端。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 11/10/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 5415bfa0ac4af14891a9445cdeab6a4509fffc38
ms.openlocfilehash: 630ccdf7b7f45a88586c9ab530c164985267bec9

---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>使用 Configuration Manager 管理 Office 365 ProPlus 更新

*適用對象：System Center Configuration Manager (最新分支)*

從 Configuration Manager 1602 版開始，Configuration Manager 能夠使用軟體更新管理工作流程來管理 Office 365 用戶端更新。 當 Microsoft 將新的 Office 365 用戶端更新發佈至 Office 內容傳遞網路 (CDN) 時，Microsoft 也會將更新套件發佈至 Windows Server Update Services (WSUS)。 當 Configuration Manager 將 Office 365 用戶端更新從 WSUS 類別目錄同步處理至站台伺服器之後，更新就可以部署至用戶端。

## <a name="office-365-client-management-dashboard"></a>Office 365 用戶端管理儀表板  
從 Configuration Manager 1610 版開始，您即可在 Configuration Manager 主控台中使用 Office 365 用戶端管理儀表板。 若要檢視此儀表板，請移至 [軟體程式庫] > [概觀] > [Office 365 用戶端管理]。

<!--- >[!NOTE]
>In the **What's New** workspace in the Configuration Manager console, the new dashboard is incorrectly named **Office 365 Servicing dashboard**. --->

此儀表板會顯示下列圖表：

- Office 365 用戶端數目
- Office 365 用戶端版本
- Office 365 用戶端語言
- Office 365 用戶端通道     
如需詳細資訊，請參閱 [Office 365 ProPlus 更新通道的概觀](https://technet.microsoft.com/library/mt455210.aspx)。
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

使用儀表板頂端的 [集合] 下拉式清單設定，依特定集合成員篩選儀表板資料。

<!---
 On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).
--->

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

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->



<!--HONumber=Dec16_HO3-->


