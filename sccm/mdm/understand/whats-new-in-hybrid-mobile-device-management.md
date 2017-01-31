---
title: "混合式 MDM 的新功能 | Microsoft Docs"
description: "了解 System Center Configuration Manager 與 Intune 的混合式部署可以使用的新行動裝置管理功能。"
ms.custom: na
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 7327c969402b9b467cfb50d1dd3255797a9d4c4e
ms.openlocfilehash: 27b75831f28860ca435b4a53aad31abd15b9e451

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 和 Microsoft Intune 混合式行動裝置管理的新功能

*適用對象：System Center Configuration Manager (最新分支)*

本文提供 System Center Configuration Manager 與 Microsoft Intune 混合式部署可以使用的新行動裝置管理 (MDM) 功能的詳細資訊。  

##  <a name="compatibility-with-configuration-manager-versions"></a>與 Configuration Manager 版本的相容性  

 本文的各節會列出 3 個不同目錄下的混合式功能。 請使用下列指導方針判斷每個類別功能與 Configuration Manager 不同版本的相容性︰  

|功能類別|說明|
|-|-|
|**Microsoft Intune 的新功能** | 通常此類別下列出的所有功能都應該能夠與所有的 Configuration Manager 版本 (包括 System Center 2012 R2 Configuration Manager 版本) 搭配使用，因為這些功能只需要 Intune 服務，不需要其他的 Configuration Manager 功能。|
|**Configuration Manager Technical Preview 的新功能**| 此類別下列出的所有功能只能搭配指定的 Technical Preview 版本使用。 若要試用這些功能，您必須安裝功能描述中指定的 Technical Preview 版本。 如需詳細資訊，請參閱 [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) 。|
|**Configuration Manager (最新分支) 的新功能**| 此類別下列出的所有功能只能搭配指定的 Configuration Manager 版本 (最新分支) 使用，例如 1511 版或 1602 版。 如果您的混合式部署使用舊版的 Configuration Manager，即必須升級到功能描述中指定的 Configuration Manager 版本 (最新分支)。 如需詳細資訊，請參閱[升級至 System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。|

## <a name="new-hybrid-features-in-january-2017"></a>2017 年 1 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2017 年 1 月推出的下列 Intune 功能可在混合式部署中運作：

- **Android 7.1.1 支援**

  Intune 現在可完全支援及管理 Android 7.1.1。

- **解決 iOS 裝置處於非使用中狀態或管理主控台無法與其通訊的問題**

  當使用者的裝置失去與 Intune 的連線時，您可以為使用者提供新的疑難排解步驟，以協助他們重新取得公司資源的存取權。 請參閱[裝置處於非使用中狀態或管理主控台無法與其通訊](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them)。


## <a name="new-hybrid-features-in-december-2016"></a>2016 年 12 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2016 年 12 月推出的下列 Intune 功能可在混合式部署中運作：

- **移至 Azure 入口網站的註冊相關 Multi-Factor Authentication (MFA)**

  您之前會移至 Intune 主控台或 Configuration Manager 主控台，來設定用於 Intune 註冊的 MFA。 透過這項更新的功能，您現在可以使用 Intune 認證登入 [Microsoft Azure 入口網站] (https://manage.windowsazure.com)，並透過 Azure AD 進行 MFA 設定。 若要深入了解，請參閱 [Microsoft Intune 的 Multi-Factor Authentication] (https://aka.ms/mfa_ad)。

- **中國現在提供適用於 Android 的公司入口網站應用程式**

  中國現在提供適用於 Android 的公司入口網站應用程式。 由於中國沒有 Google Play 商店，因此 Android 裝置必須從中文應用程式服務商場取得應用程式。 適用於 Android 的公司入口網站應用程式已於下列市集中可供下載：

  - [百度](https://go.microsoft.com/fwlink/?linkid=836946)
  - [華為](https://go.microsoft.com/fwlink/?linkid=836948)
  - [騰訊](https://go.microsoft.com/fwlink/?linkid=836949)
  - [豌豆莢](https://go.microsoft.com/fwlink/?linkid=836950)
  - [小米應用商店](https://go.microsoft.com/fwlink/?linkid=836947)

  適用於 Android 的公司入口網站應用程式會使用 Google Play 服務來與 Microsoft Intune 服務通訊。 由於中國尚無法使用 Google Play 服務，因此執行下列任何工作可能需要多達 8 小時才能完成。

  | Configuration Manager 系統管理員主控台 | 適用於 Android 的 Intune 公司入口網站應用程式 | Intune 公司入口網站 |
  |----|----|----|      
  | 淘汰/抹除 (移除所有資料)   | 移除遠端裝置 | 移除裝置 (本機和遠端) |
  | 淘汰/抹除 (移除公司資料)   | 重設裝置 | 重設裝置|
  | 新的或更新的應用程式部署 | 安裝可用的企業營運應用程式 | 裝置密碼重設|
  | 遠端鎖定 | | |
  | 密碼重設 | | |        


## <a name="new-hybrid-features-in-november-2016"></a>2016 年 11 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2016 年 11 月推出的下列 Intune 功能可在混合式部署中運作：

- **適用於 Windows 10 裝置的新 Microsoft Intune 公司入口網站**

  Microsoft 已發行新的[適用於 Windows 10 裝置的公司入口網站應用程式](https://www.microsoft.com/store/apps/9wzdncrfj3pz)。 此應用程式會利用新的 Windows 10 通用格式，提供與所有 Windows 10 裝置、電腦及行動裝置之類的裝置上完全相同的更新使用者體驗，同時仍會啟用先前公司入口網站應用程式所提供的所有相同功能。

  新的應用程式會利用 Windows 10 裝置上的平台功能，例如單一登入 (SSO) 和憑證式驗證。 此應用程式可用來升級到現有的 Windows 8.1 公司入口網站，而 Windows Phone 8.1 公司入口網站會從 Windows 市集進行安裝。 如需詳細資訊，請參閱 [Intune 支援小組部落格](http://aka.ms/intunecp_universalapp)。

  新的公司入口網站應用程式也會在 Configuration Manager 主控台中，顯示所有標記為**可用**的商務用 Windows 市集應用程式。


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)

Configuration Manager Technical Preview 各版本過去提供的下列功能，目前可在 Intune 和 Configuration Manager (最新分支) 1610 版的混合式部署中使用。

* [設定項目的額外設定和改進體驗](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [DEP 設定檔的其他設定](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [商務用 Windows 市集的付費 App](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Windows 10 VPN 設定檔的原生連接類型](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Intune 相容性圖表](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [從主控台要求同步處理原則](/sccm/mdm/deploy-use/sync-intune-device)
* [Windows Defender 組態設定](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

Configuration Manager (最新分支) 1610 版也包含下列額外的混合式功能：

- **增加已註冊裝置的數目**

  您現在可讓使用者最多註冊 15 個裝置。 先前的限制是每位使用者 5 個裝置。


- **其他的安全性支援**

  除了系統高權限管理員，下列內建的安全性角色現在也具備「公司擁有的所有裝置」節點中項目的完整存取權，包括預先宣告的裝置、iOS 註冊設定檔，以及 Windows 註冊設定檔：

    - 資產管理員
    - 公司資源存取管理員

  系統仍會為唯讀分析師角色授與 Configuration Manager 主控台中這些區域的唯讀存取權。

- **從 Windows 資訊保護應用程式自動觸發 VPN 存取**

  您可以將 Windows 資訊保護主要網域加入 Windows 10 VPN 設定檔，這將導致所有相關聯的應用程式在裝置上執行時會自動觸發 VPN 連線。 唯有在選擇原生連線類型時，才能使用此選項。

- **Windows 10 VPN 設定檔的條件式存取**

    您現在可以要求在 Azure Active Directory 中註冊的 Windows 10 裝置必須符合標準，才能透過在 Configuration Manager 主控台中建立的 Windows 10 VPN 設定檔來存取 VPN。 這能夠透過 VPN 設定檔精靈中 [驗證方法] 頁面上新的 [為此 VPN 連線啟用條件存取] 核取方塊以及 Windows 10 VPN 設定檔的 VPN 設定檔內容來進行。 唯有在選擇原生連線類型時，才能使用此選項。

    如果您啟用設定檔的條件式存取，您也可以指定不同的憑證來進行單一登入驗證。


## <a name="notices"></a>通知

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 和 System Center 2012 R2 Configuration Manager (RTM)：對混合式行動裝置管理的支援將於 2017 年 4 月 10 日結束

*2017 年 1 月 11 日*

對 System Center 2012 Configuration Manager SP1 和 System Center 2012 R2 Configuration Manager RTM 的支援已經於 2016 年 7 月 12 日結束。 接著，對連線到 Microsoft Intune 服務以使用混合式 MDM 的這些版本的支援將於 2017 年 4 月 10 日結束。 在這個日期之後，搭配這些版本使用的混合式 MDM 將會停止運作。 受管理的裝置基本上會變成不受管理，因為 Intune Connector 將不會再連線到 Intune 服務。 除非執行升級，否則 Configuration Manager 資料 (例如原則和應用程式) 將不會往上流動至 Intune，而受管理裝置的資料不會往下流動至 Configuration Manager。

如果您正在執行使用 Configuration Manager 2012 SP1 或 R2 RTM 的混合式部署，建議您在 2017 年 4 月 10 日之前升級至 Configuration Manager (最新分支)，或是最新支援的 Configuration Manager 2012 Service Pack (R2 SP1 或 SP2)，以避免服務中斷。

其他資源：
-   [升級至 System Center Configuration Manager (最新分支)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [規劃升級至 System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [規劃升級至 System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Windows Phone 8 公司入口網站上傳已停用
*2016 年 10 月 25 日*

Configuration Manager 主控台已移除上傳已簽署公司入口網站應用程式的功能，因為 Windows 8、Windows Phone 8 和 Windows RT 已停用 Intune 支援，且對 Windows Phone 8 公司入口網站的支援將於 11 月終止。  會繼續支援已註冊的 Windows 8、Windows Phone 8 和 Windows RT 裝置，但不支援使用這些平台來註冊其他裝置。


## <a name="see-also"></a>另請參閱

- [過去的混合式 MDM 功能](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager 中 MDM 的新功能](https://technet.microsoft.com/library/mt445560.aspx)



<!--HONumber=Jan17_HO2-->


