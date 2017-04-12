---
title: "使用 Configuration Manager 的混合式 MDM 新功能 | Microsoft Docs"
description: "了解 Configuration Manager 與 Intune 的混合式部署可以使用的新行動裝置管理功能。"
ms.custom: na
ms.date: 03/28/2017
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
ms.sourcegitcommit: 3eb48942c1259d2aa1b3c200fad73b39b11c0b8c
ms.openlocfilehash: 51560360a0cb7ecb4a2b0d7eaeb4fdd62d6afc13
ms.lasthandoff: 03/30/2017

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

## <a name="new-hybrid-features-in-march-2017"></a>2017 年 3 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2017 年 3 月推出的下列 Intune 功能可在混合式部署中運作：

- **Android 版公司入口網站應用程式的新使用者體驗**

  Android 版公司入口網站應用程式的使用者介面，有了更現代的外觀及操作。 值得注意的更新如下︰

  - 色彩：公司入口網站索引標籤標題以 IT 定義的商標上色。
  - 應用程式：[應用程式] 索引標籤中，已更新 [精選應用程式] 和 [所有應用程式] 按鈕。
  - 搜尋：[應用程式] 索引標籤中，[搜尋] 按鈕是浮動的動作按鈕。
  - 瀏覽應用程式：[所有應用程式] 檢視會以索引標籤式的檢視顯示 [精選]、[所有] 與 [類別] 以方便瀏覽。
  - 支援：已更新 [我的裝置] 和 [連絡 IT] 索引標籤，以改善可讀性。

  如需這些變更的詳細資料，請參閱 [Intune 終端使用者應用程式的 UI 更新](/intune/enduser/whats-new-in-intune-app-ui)。

- **簽署 Windows 10 公司入口網站的指令碼**

  如果您必須下載及側載 Windows 10 公司入口網站，現在可以使用指令碼為組織簡化應用程式的簽署程序。  若要下載指令碼及其使用指示，請參閱 TechNet 組件庫上的 [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript) (Microsoft Intune 簽署 Windows 10 公司入口網站的指令碼)。 如需此公告的詳細資料，請參閱 Intune Support Team Blog 上的 [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) (更新您的 Windows 10 公司入口網站應用程式)。

- **為中國的 Andriud 使用者改進支援**

  由於中國沒有 Google Play 商店，因此 Android 裝置必須從中國的市集取得應用程式。 公司入口網站會將中國的 Android 使用者重新導向，以從當地應用程式市集下載公司入口網站及 Outlook 應用程式，從而支援此工作流程。 這會在條件式存取原則已啟用的狀態下，改進行動裝置管理及行動應用程式管理的使用者體驗。 Android 版的公司入口網站及 Outlook 應用程式於下列中國應用程式市集提供：

  - [百度](https://go.microsoft.com/fwlink/?linkid=836946)
  - [小米應用商店](https://go.microsoft.com/fwlink/?linkid=836947)
  - [騰訊](https://go.microsoft.com/fwlink/?linkid=836949)
  - [華為](https://go.microsoft.com/fwlink/?linkid=836948)
  - [豌豆莢](https://go.microsoft.com/fwlink/?linkid=836950)

- **確認您的公司入口網站為最新狀態**

  我們在 2016 年 12 月發行的更新，能讓您在一群使用者註冊 iOS, Android、Windows 8.1+ 或 Windows Phone 8.1+ 裝置時強制執行多重要素驗證 (MFA)。 這項功能必須要有 Android (v5.0.3419.0+) 及 iOS (v2.1.17+) 的公司入口網站應用程式特定基準版本才能運作。

  Intune 的管理功能會持續改進，而多項功能改進已協同公司入口網站應用程式的更新，在所有支援的平台上推出。 因此，建議您讓公司入口網站應用程式在安裝的裝置上保持最新狀態，以利用 Intune 的功能改進，並獲得最佳使用者體驗。

  >[!Tip]
  > 請要求您的使用者設定其裝置，以自動從適當的應用程式市集更新應用程式。 如果您已允許 Android 公司入口網站應用程式在網路共用上使用，則可以從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=49140)下載最新版本。

- **Microsoft Teams 現在可於 iOS 及 Android 執行 MAM**

  iOS 及 Android 版的 Microsoft Teams 應用程式現在可執行 Intune 行動應用程式管理 (MAM) 功能，因此您可以讓團隊在不同裝置間自由工作，同時確保對話和公司資料在每個環節都受到保護。 如需詳細資料，請參閱 Enterprise Mobility + Security 部落格上的 [Microsoft Teams 公告](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/)。

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Configuration Manager Technical Preview 1703 的新功能

- **Apple 大量採購方案案例的其他支援**

   自 Technical Preview 1703 起，您現在有下列大量採購方案 (VPP) 案例的支援︰

   - 裝置授權 - 對於支援裝置授權且部署至裝置集合的應用程式，每個裝置只需要一個授權。  先前，您必須為裝置上的每個使用者使用授權。 如需詳細資訊，請參閱[將大量採購的 iOS 應用程式部署至裝置集合](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections)。
   - 使用單一混合式租用戶的多個 VPP 權杖，其中兩個權杖皆用於管理 VPP 應用程式。
   - 使用 VPP 教育權杖，且具備區分商業和教育權杖的功能。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)

下列是過去 Configuration Manager Technical Preview 版本提供功能，現在在 Intune 與 Configuration Manager (最新分支) 1702 版的混合式部署中已可供使用。

- [Android for Work 支援](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [不符合規範的應用程式相容性設定](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [PFX 憑證建立和發佈以及 S/MIME 支援](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [混合式 MDM 的建立精靈無法再將目標設為 Android 與 iOS 版本](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Configuration Manager (最新分支) 1702 版也包含下列額外的混合式功能：

- **對 Apple Volume Purchase Program (大量採購方案) 的改進支援**

  - 您現在不但可將授權的應用程式部署到使用者，還可部署到裝置。 視應用程式是否能夠支援裝置授權而定，當您部署應用程式時，系統會要求適當的授權，如下︰

    | Configuration Manager 版本 | 應用程式是否支援裝置授權？ | 部署集合類型 | 要求的授權 |
    |-|-|-|-|
    |1702 之前|是|使用者|使用者授權|
    |1702 之前|否|使用者|使用者授權|
    |1702 之前|是|裝置|使用者授權|
    |1702 之前|否|裝置|使用者授權|
    |1702 和更新版本|是|使用者|使用者授權|
    |1702 和更新版本|否|使用者|使用者授權|
    |1702 和更新版本|是|裝置|裝置授權|
    |1702 和更新版本|否|裝置|使用者授權|

  - 您現在也可以部署和追蹤從 iOS Volume Purchase Program for Education (教育單位大量採購方案) 購買的應用程式。

  - 您現在可以將多個 Apple 大量採購方案權杖與 Configuration Manager 建立關聯。

  如需有關大量採購之 iOS 應用程式的詳細資訊，請參閱[管理大量採購的 iOS 應用程式](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)。

- **對商務用 Windows 市集中企業營運應用程式的支援**

  您現在可以從「商務用 Windows 市集」同步處理自訂的企業營運應用程式。

- **新的 Mobile Threat Defense 監視工具**

    您現在可以透過新的方式來監視與您 Mobile Threat Defense 服務提供者的合規性狀態。

    如需詳細資訊，請參閱[如何監視 Mobile Threat Defense 合規性](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance)。

## <a name="new-hybrid-features-in-february-2017"></a>2017 年 2 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2017 年 2 月推出的下列 Intune 功能可在混合式部署中運作：

- **現代化公司入口網站**

  公司入口網站支援以沒有受管理裝置的使用者為目標的應用程式。 網站會與其他 Microsoft 產品和服務一致，方法是使用新的對比色彩配置、動態圖例和「漢堡功能表」，其包含技術服務連絡人詳細資料以及現有受管理裝置的相關資訊。 登陸頁面已重新排列，其透過 [精選和最近更新] 應用程式的浮動切換來強調使用者可用的應用程式。 您可以在 [UI 更新](/intune/whats-new/whats-new-in-intune-app-ui)頁面中找到之前和之後的影像。

- **適用於 Windows 裝置的新 MDM 伺服器位址**

  註冊 Windows 和 Windows Phone 裝置的 MDM 伺服器位址，已從 manage.microsoft.com 變更為 enrollment.manage.microsoft.com。 在註冊 Windows 和 Windows Phone 時，如果出現提示，請通知使用者使用 enrollment.manage.microsoft.com 的 MDM 伺服器位址。 這項更新另要求您將 DNS 中任何把 EnterpriseEnrollment.contoso.com 重新導向 manage.microsoft.com 的 CNAME，取代為把 EnterpriseEnrollment.contoso.com 重新導向 EnterpriseEnrollment-s.manage.microsoft.com 的 DNS CNAME。 如需這項變更的詳細資訊，請造訪 http://aka.ms/intuneenrollsvrchange。

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Configuration Manager Technical Preview 1702 的新功能

- **Android for Work 支援**

  您現在可以使用 Configuration Manager Technical Preview 1702，在混合式 MDM 環境中管理使用 Android for Work 的 Android 裝置。 現在可將支援的 Android 裝置註冊為 Android for Work 裝置，這會在裝置上建立工作設定檔，以便部署 Play for Work 中核准的應用程式。 您也可以為這些裝置設定及部署設定項目、合規性政策和資源存取設定檔。 如需詳細資訊，請參閱 [Android for Work 支援](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support)。

- **不符合規範的應用程式相容性設定**

  您現在可以在合規性政策中，為 Android 和 iOS 應用程式建立不符合規範的應用程式規則。 如果裝置已安裝指定的應用程式，則會標示為「不符合規範」，而且根據適當的條件式存取原則將無法存取公司資源。 如需詳細資訊，請參閱[條件式存取裝置合規性政策改善](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements)。

- **PFX 憑證建立和發佈以及 S/MIME 支援**

  您現在可以建立 PFX 憑證，並將該憑證部署給混合式環境中的使用者。 這些憑證接著可供使用者已註冊的裝置用來加密及解密 S/MIME 電子郵件。 如需詳細資訊，請參閱[使用 S MIME 支援來建立 PFX 憑證](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support)。

- **對額外 iOS 組態設定的支援**
   
    您現在有 42 個可在設定項目中設定的額外 iOS 設定。 針對受監督的 iOS 裝置，已新增大部分的設定 (總計 35 個)。 如需詳細資訊，請參閱 [iOS 裝置的新合規性設定](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices)。

## <a name="new-hybrid-features-in-january-2017"></a>2017 年 1 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2017 年 1 月推出的下列 Intune 功能可在混合式部署中運作：

- **Android 7.1.1 支援**

  Intune 現在可完全支援及管理 Android 7.1.1。

- **解決 iOS 裝置處於非使用中狀態或管理主控台無法與其通訊的問題**

  當使用者的裝置失去與 Intune 的連線時，您可以為使用者提供新的疑難排解步驟，以協助他們重新取得公司資源的存取權。 請參閱[裝置處於非使用中狀態或管理主控台無法與其通訊](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them)。

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Configuration Manager Technical Preview 1701 的新功能

- **混合式 MDM 的建立精靈無法再將目標設為 Android 與 iOS 版本**

  從混合式行動裝置管理 (MDM) 的 Technical Preview 1701 開始，您在為受 Intune 管理的裝置建立新原則及設定檔時，不再需要以 Android 或 iOS 的特定版本為目標。 透過這項變更，混合式部署可更快為 Android 及 iOS 版本提供支援，而不需要新的 Configuration Manager 版本或延伸模組。 若要深入了解，請參閱[建立精靈無法再將目標設為 Android 與 iOS 版本](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)。


## <a name="new-hybrid-features-in-december-2016"></a>2016 年 12 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2016 年 12 月推出的下列 Intune 功能可在混合式部署中運作：

- **移至 Azure 入口網站的註冊相關 Multi-Factor Authentication (MFA)**

  您之前會移至 Intune 主控台或 Configuration Manager 主控台，來設定用於 Intune 註冊的 MFA。 透過這項更新的功能，您現在可以使用 Intune 認證登入 [Microsoft Azure 入口網站] (https://manage.windowsazure.com)，並透過 Azure AD 進行 MFA 設定。 若要深入了解，請參閱 [Microsoft Intune 的 Multi-Factor Authentication] (https://aka.ms/mfa_ad)。

- **中國現在提供適用於 Android 的公司入口網站應用程式**

  中國現在提供適用於 Android 的公司入口網站應用程式。 由於中國沒有 Google Play 商店，因此 Android 裝置必須從中文應用程式服務商場取得應用程式。 適用於 Android 的公司入口網站應用程式已於下列市集中可供下載：

  -    [百度](https://go.microsoft.com/fwlink/?linkid=836946)
  -    [華為](https://go.microsoft.com/fwlink/?linkid=836948)
  -    [騰訊](https://go.microsoft.com/fwlink/?linkid=836949)
  -    [豌豆莢](https://go.microsoft.com/fwlink/?linkid=836950)
  -    [小米應用商店](https://go.microsoft.com/fwlink/?linkid=836947)

  適用於 Android 的公司入口網站應用程式會使用 Google Play 服務來與 Microsoft Intune 服務通訊。 由於中國尚無法使用 Google Play 服務，因此執行下列任何工作可能需要多達 8 小時才能完成。

  | Configuration Manager 系統管理員主控台 | 適用於 Android 的 Intune 公司入口網站應用程式 | Intune 公司入口網站 |
  |----|----|----|        
  | 淘汰/抹除 (移除所有資料)    | 移除遠端裝置 | 移除裝置 (本機和遠端) |
  | 淘汰/抹除 (移除公司資料)    | 重設裝置 | 重設裝置|
  | 新的或更新的應用程式部署 | 安裝可用的企業營運應用程式 | 裝置密碼重設|
  | 遠端鎖定    | | |
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
-    [升級至 System Center Configuration Manager (最新分支)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-    [規劃升級至 System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-    [規劃升級至 System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Windows Phone 8 公司入口網站上傳已停用
*2016 年 10 月 25 日*

Configuration Manager 主控台已移除上傳已簽署公司入口網站應用程式的功能，因為 Windows 8、Windows Phone 8 和 Windows RT 已停用 Intune 支援，且對 Windows Phone 8 公司入口網站的支援將於 11 月終止。  會繼續支援已註冊的 Windows 8、Windows Phone 8 和 Windows RT 裝置，但不支援使用這些平台來註冊其他裝置。


### <a name="see-also"></a>另請參閱

- [過去的混合式 MDM 功能](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager 中 MDM 的新功能](https://technet.microsoft.com/library/mt445560.aspx)

