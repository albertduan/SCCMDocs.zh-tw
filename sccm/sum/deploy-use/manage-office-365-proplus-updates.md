---
title: "管理 Office 365 ProPlus 更新 | Microsoft Docs"
description: "Configuration Manager 會將 Office 365 用戶端更新從 WSUS 類別目錄同步處理至站台伺服器，讓更新能夠部署至用戶端。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/04/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 6bb2bf0a029bc21e9420ac0ba782e8ea21291896
ms.openlocfilehash: df9ad09c4ce0c2a18ee012cd3ace7b1a850df7b4

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

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>在 Office 365 用戶端管理儀表板中顯示資料
[Office 365 用戶端管理] 儀表板中所顯示的資料來自硬體清查。 硬體清查必須予以啟用，而且您必須先選取 [Office 365 ProPlus Configurations] (Office 365 ProPlus 設定) 硬體清查類別，資料才會顯示在儀表板中。
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>在 Office 365 用戶端管理儀表板中顯示資料
1. 啟用硬體清查 (若尚未啟用)。 如需詳細資料，請參閱[設定硬體清查](\sccm\core\clients\manage\configure-hardware-inventory)。
2. 在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [用戶端設定] > [預設用戶端設定]。  
3. 在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  
4. 在 **預設用戶端設定**  對話方塊中按一下 **硬體清查**。  
5. 在 **裝置設定** 清單中，按一下 **設定類別**。  
6. 在 [硬體清查類別] 對話方塊中，選取 [Office 365 ProPlus Configurations] (Office 365 ProPlus 設定)。  
7.  按一下 **確定** 以儲存您的變更並關閉 **硬體清查類別** 對話方塊。  
[Office 365 用戶端管理] 儀表板將在報告硬體清查時開始顯示資料。

<!---
 On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).
--->

## <a name="deploy-office-365-updates-with-configuration-manager"></a>使用 Configuration Manager 部署 Office 365 更新
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

<!--  ## Add other languages for Office 365 update downloads
Beginning in Configuration Manager version 1610, you can add support for Configuration Manager to download updates for any languages supported by Office 365 regardless of whether they are supported in Configuration Manager.

### To add support to download updates for additional languages
Use the following procedure on the central administration site, or stand-alone primary site, where the software update point site system role is installed.
1. From a command prompt, type *wbemtest* as an administrative user to open the Windows Management Instrumentation Tester.
2. Click **Connect**, and then type *root\sms\site_<siteCode>*.
3. Click **Query**, and then run the following query:
   *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*
4. Double-click the object with the site code for the central administration site or stand-alone primary site.

5. Browse the properties for View Embedded.
3). Find the SMS_EmbeddedProperty instance with the PropertyName of "AdditionalUpdateLanguagesForO365"
4). Set Value2 to be additional languages, e.g.:  pt-pt,af-za,nn-no, and save
5). Right click to download an O365 update, choose languages from UI
6). Verify that the language packs got downloaded including the UI specified ones plus the SDK specified ones. Admin can check the content package share specified to verify this.
-->

<!-- ## Change the update channel after you enable Office 365 clients to receive updates from Configuration Manager
To change the update channel after you enable Office 365 clients to receive updates from Configuration Manager, you must distribute a registry key value change to Office 365 clients using group policy. Change the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** registry key to use one of the following values:

- Current Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Deferred Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- First Release for Current Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- First Release for Deferred Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf
-->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->



<!--HONumber=Jan17_HO3-->


