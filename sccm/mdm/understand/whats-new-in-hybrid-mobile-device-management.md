---
title: "使用 Configuration Manager 的混合式 MDM 新功能 | Microsoft Docs"
description: "了解 Configuration Manager 與 Intune 的混合式部署可以使用的新行動裝置管理功能。"
ms.custom: na
ms.date: 06/30/2017
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
ms.translationtype: HT
ms.sourcegitcommit: 1035dbbf944a3a467d637a4a948a75b0946eb711
ms.openlocfilehash: a9e03d4c5b290886bda87fae41e4df362eca1b71
ms.contentlocale: zh-tw
ms.lasthandoff: 07/11/2017

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 和 Microsoft Intune 混合式行動裝置管理的新功能

*適用對象：System Center Configuration Manager (最新分支)*

本文提供 System Center Configuration Manager 與 Microsoft Intune 混合式部署可以使用的新行動裝置管理 (MDM) 功能的詳細資訊。  

##  <a name="compatibility-with-configuration-manager-versions"></a>與 Configuration Manager 版本的相容性  

 本文的各節會列出 3 個不同類別下的混合式功能。 請使用下列指導方針判斷每個類別功能與 Configuration Manager 不同版本的相容性︰  

|功能類別|說明|
|-|-|
|**Microsoft Intune 的新功能** | 通常此類別下列出的所有功能都應該能夠與所有的 Configuration Manager 版本 (包括 System Center 2012 R2 Configuration Manager 版本) 搭配使用，因為這些功能只需要 Intune 服務，不需要其他的 Configuration Manager 功能。|
|**Configuration Manager Technical Preview 的新功能**| 此類別下列出的所有功能只能搭配指定的 Technical Preview 版本使用。 若要試用這些功能，您必須安裝功能描述中指定的 Technical Preview 版本。 如需詳細資訊，請參閱 [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) 。|
|**Configuration Manager (最新分支) 的新功能**| 此類別下列出的所有功能只能搭配指定的 Configuration Manager 版本 (最新分支) 使用，例如 1511 版或 1602 版。 如果您的混合式部署使用舊版的 Configuration Manager，即必須升級到功能描述中指定的 Configuration Manager 版本 (最新分支)。 如需詳細資訊，請參閱[升級至 System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。|

## <a name="july-2017"></a>2017 年 7 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

- **新增 Android 支援版本的通知**

    針對 Android 的支援版本，新增了新的通知。 如需詳細資料，請參閱[終止支援 Android 4.3 與較舊版本](#notices)。

## <a name="june-2017"></a>2017 年 6 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

- **變更您的 MDM 授權單位**

  自 Configuration Manager 1610 版和 Microsoft Intune 1705 版開始，不需要連絡 Microsoft 支援服務，也不需要將現有受管理裝置解除註冊並重新註冊，您便可以變更 MDM 授權單位。 如需詳細資訊，請參閱[變更您的 MDM 授權單位]( /sccm/mdm/deploy-use/change-mdm-authority)。

- **受管理的瀏覽器和應用程式 Proxy 整合**

  Intune Managed Browser 現已可和 Azure AD 應用程式 Proxy 服務整合，讓使用者即使在遠端工作也可以存取內部網站。 瀏覽器使用者可以和平常一樣地輸入網站的 URL，Managed Browser 便會透過應用程式 Proxy Web 閘道路由傳送要求。 如需詳細資訊，請參閱[使用受管理的瀏覽器原則管理網際網路存取](/intune/app-configuration-managed-browser)。

- **Android 版公司入口網站應用程式已推出應用程式保護原則的全新使用者體驗**

  我們根據客戶的意見反應修改了 Android 版公司入口網站應用程式，使它會顯示 [存取公司內容] 按鈕。 目的是讓使用者在只需要存取支援應用程式保護原則 (Intune 行動應用程式管理的功能) 的應用程式時，可以避免不必要的註冊程序。 您可以在[應用程式 UI 的新功能](/intune/whats-new-app-ui)頁面上查看這些變更。

- **可輕鬆移除公司入口網站的新功能表動作**

  根據使用者的意見反應，Android 版公司入口網站應用程式已新增可將公司入口網站從裝置上移除的新功能表動作。 此動作會將裝置從 Intune 管理移除，來讓使用者可以將應用程式從裝置移除。 您可以在[應用程式 UI 的新功能](/intune/whats-new-app-ui)頁面上與 [Android 使用者文件](/intune-user-help/unenroll-your-device-from-intune-android)中查看這些變更。

- **針對 Windows 10 Creators Update 改善應用程式同步處理**

  針對具有 Windows 10 Creators Update (1703 版) 的裝置，Windows 10 版公司入口網站應用程式現在會對應用程式安裝要求自動起始同步處理。 如此可減少應用程式安裝在「待同步」狀態期間懸置的問題。 此外，使用者將能從應用程式內手動起始同步處理。 您可以在[應用程式 UI 的新功能](/intune/whats-new-app-ui)頁面上查看這些變更。

- **Windows 10 版公司入口網站新型引導式體驗**

  Windows 10 版公司入口網站應用程式將會針對尚未識別或註冊的裝置提供引導式 Intune 逐步解說體驗。 新型體驗能提供逐步指示，可引導使用者註冊至 Azure Active Directory (取得條件式存取功能所需) 及 MDM 註冊 (取得裝置管理功能所需)。 引導式體驗能透過公司入口網站首頁取得。 未完成註冊的使用者可以繼續使用應用程式，但可使用的功能將會受到限制。

  此更新只會在執行 Windows 10 年度更新版 (組建 1607) 或更新版本的裝置上顯示。 您可以在[應用程式 UI 的新功能](/intune/whats-new-app-ui)頁面上查看這些變更。

- **改善 iOS 版公司入口網站應用程式中的應用程式磚**

  我們已更新首頁上應用程式磚的設計，以反映您針對公司入口網站所設定的商標色彩。 如需詳細資訊，請參閱[應用程式 UI 的新功能](/intune/whats-new-app-ui)。

- **帳戶選擇器現已可供 iOS 版公司入口網站應用程式使用**

  如果 iOS 裝置的使用者是使用公司或學校帳戶登入其他 Microsoft 應用程式，則他們在登入公司入口網站時可能會看到新的帳戶選擇器。 如需詳細資訊，請參閱[應用程式 UI 的新功能](/intune/whats-new-app-ui)。

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Configuration Manager Technical Preview 1706 的新功能

- **新的行動應用程式管理原則設定**    

  現已提供下列行動應用程式管理 (MAM) 原則設定：

  - **封鎖螢幕擷取 (僅限 Android 裝置)：**指定在使用此應用程式時，封鎖裝置的螢幕擷取功能。
  - **停用連絡人同步：**防止應用程式將資料儲存至裝置上的原生「連絡人」應用程式。
  - **停用列印：**防止應用程式列印公司或學校資料。

  若要試用新的應用程式保護原則設定，請參閱[使用 Configuration Manager 中的應用程式保護原則來保護應用程式](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies)。

- **新的 Windows 組態項目設定**  <!-- 1354715 -->    

  有新的 Windows 組態項目可供密碼、裝置、市集和 Microsoft Edge 設定分類使用。 如需詳細資訊，請參閱[新的 Windows 組態項目設定](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings)。

- **新的裝置合規性政策規則**    

  您現在可以針對合規性政策設定各種新的選項，這些選項先前只在 Intune 獨立部署中提供。 如需詳細資訊，請參閱[裝置合規性政策改善](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules)。

- **Android 和 iOS 的註冊限制** <!-- 1290826 -->      

  系統管理員現在能指定使用者不能在混合式環境中註冊個人的 Android 或 iOS 裝置。 這可讓您將註冊的裝置僅限於已預先宣告的公司擁有裝置，或是透過「裝置註冊計劃」註冊的 iOS 裝置。 如需詳細資訊，請參閱 [Android 和 iOS 的註冊限制](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions)。

- **支援 Entrust 憑證授權單位** <!-- 1350740 -->     

  Configuration Manager 現在支援 Entrust 憑證授權單位；這使 PFX 憑證得以傳送到已在 Microsoft Intune 中註冊的裝置。    

  當您在 Configuration Manager 中新增「憑證登錄點」角色時，便可以將 Entrust 設定成憑證授權單位。 當新增發行 PFX 憑證的憑證設定檔時，您可以選取 Microsoft 或 Entrust 憑證授權單位。

  **已知問題**：在 1706 Technical Preview 中，不會為 Microsoft 憑證授權單位發行 PFX 憑證。 這不會影響匯入的 PFX 憑證或 SCEP 設定檔。

- **針對 macOS VPN 設定檔的 Cisco (IPsec) 支援**  <!-- 1321367 -->    

  您可以建立以 Cisco (IPsec) 作為連線類型的 macOS VPN 設定檔。 如需詳細資訊，請參閱[建立 VPN 設定檔](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles)。


## <a name="april-2017"></a>2017 年 4 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

- **MyApps 可供 Managed Browser 使用**

  Microsoft MyApps 現在於 Managed Browser 內有更好的支援。 非管理目標的 Managed Browser 使用者會直接前往 MyApps 服務，並可在其中存取其系統管理員佈建的 SaaS 應用程式。 Intune 管理目標的使用者將能夠繼續從內建 Managed Browser 書籤來存取 MyApps。

- **Managed Browser 和公司入口網站的新圖示**

  Managed Browser 將會同時收到 Android 和 iOS 版應用程式的更新圖示。 此新圖示會包含更新的 Intune 徽章，因此與 Enterprise Mobility + Security (EM+S) 中的其他應用程式更一致。 您可以在 [Intune 應用程式 UI 的新功能頁面](/intune/whats-new/whats-new-in-intune-app-ui.md)上，看到 Managed Browser 的新圖示。

  公司入口網站也會收到 Android、iOS 和 Windows 版應用程式的更新圖示，以增強與 EM+S 中其他應用程式的一致性。 從 4 月到 5 月底，將逐漸在各種不同的平台上發行這些圖示。

- **Android 公司入口網站中的登入進度列指示器**

  當使用者啟動或繼續執行應用程式時，Android 公司入口網站應用程式的更新會顯示登入進度列指示器。 此指示器會顯示新狀態的進度，從 [正在連線...] 開始，接著依序為 [正在登入...] 和 [正在檢查安全性需求...]，之後才允許使用者存取應用程式。 您可以在 [Intune 應用程式 UI 的新功能頁面](/intune/whats-new/whats-new-in-intune-app-ui.md)上，看到 Android 版公司入口網站應用程式的新畫面。

- **禁止應用程式存取 SharePoint Online**

  您現在可以建立以應用程式為基礎的條件式存取原則，禁止應用程式存取 [SharePoint Online](/InTune/deploy-use/mam-ca-for-sharepoint-online)，這樣做不會對其套用應用程式保護原則。 在以應用程式為基礎的條件式存取案例中，您可以指定想要使用 Azure 入口網站存取 SharePoint Online 的應用程式。

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Configuration Manager Technical Preview 1704 的新功能

- **使用應用程式設定原則設定 Android 應用程式**

  您可以在 System Center Configuration Manager (Configuration Manager) 中使用應用程式設定原則，在使用者於 Android for Work 裝置上執行應用程式時發佈預先設定好的設定。 Android 應用程式設定原則僅可於執行 Android for Work 的裝置上使用，並適用於來自 Play for Work 商店的已核准應用程式。 如需如何試用此功能的相關資訊，請參閱[使用應用程式設定原則設定 Android 應用程式](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies)。

## <a name="march-2017"></a>2017 年 3 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

- **Android 版公司入口網站應用程式的新使用者體驗**

  Android 版公司入口網站應用程式的使用者介面，有了更現代的外觀及操作。 值得注意的更新如下︰

  - 色彩：公司入口網站索引標籤標題以 IT 定義的商標上色。
  - 應用程式：[應用程式] 索引標籤中，已更新 [精選應用程式] 和 [所有應用程式] 按鈕。
  - 搜尋：[應用程式] 索引標籤中，[搜尋] 按鈕是浮動的動作按鈕。
  - 瀏覽應用程式：[所有應用程式] 檢視會以索引標籤式的檢視顯示 [精選]、[所有] 與 [類別] 以方便瀏覽。
  - 支援：已更新 [我的裝置] 和 [連絡 IT] 索引標籤，以改善可讀性。

  如需這些變更的詳細資訊，請參閱 [Intune 終端使用者應用程式的 UI 更新](/intune/whats-new/whats-new-in-intune-app-ui)。

- **簽署 Windows 10 公司入口網站的指令碼**

  如果您必須下載及側載 Windows 10 公司入口網站，現在可以使用指令碼為組織簡化應用程式的簽署程序。  若要下載指令碼及其使用指示，請參閱 TechNet 組件庫上的 [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript) (Microsoft Intune 簽署 Windows 10 公司入口網站的指令碼)。 如需此公告的詳細資訊，請參閱 Intune 支援團隊部落格上的[更新您的 Windows 10 公司入口網站應用程式](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) \(英文\)。

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

   - 裝置授權：對於支援裝置授權且部署至裝置集合的應用程式，每個裝置只需要一個授權。  先前，您必須為裝置上的每個使用者使用授權。 如需詳細資訊，請參閱[將大量採購的 iOS 應用程式部署至裝置集合](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections)。
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

  - 您現在不但可將授權的應用程式部署到使用者，還可部署到裝置。 視應用程式是否能夠支援裝置授權而定，當您部署應用程式時，將會如下所述索取適當的授權︰

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

## <a name="february-2017"></a>2017 年 2 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

- **現代化公司入口網站**

  公司入口網站支援以沒有受管理裝置的使用者為目標的應用程式。 網站會與其他 Microsoft 產品和服務一致，方法是使用新的對比色彩配置、動態圖例和「漢堡功能表」，其包含技術服務連絡人詳細資料以及現有受管理裝置的相關資訊。 登陸頁面已重新排列，其透過 [精選和最近更新] 應用程式的浮動切換來強調使用者可用的應用程式。 您可以在 [UI 更新](/intune/whats-new/whats-new-in-intune-app-ui)頁面中找到之前和之後的影像。

- **適用於 Windows 裝置的新 MDM 伺服器位址**

  註冊 Windows 和 Windows Phone 裝置的 MDM 伺服器位址，已從 manage.microsoft.com 變更為 enrollment.manage.microsoft.com。 在註冊 Windows 和 Windows Phone 時，如果出現提示，請通知使用者使用 enrollment.manage.microsoft.com 的 MDM 伺服器位址。 這項更新另要求您將 DNS 中任何把 EnterpriseEnrollment.contoso.com 重新導向 manage.microsoft.com 的 CNAME，取代為把 EnterpriseEnrollment.contoso.com 重新導向 EnterpriseEnrollment-s.manage.microsoft.com 的 DNS CNAME。 如需這項變更的詳細資訊，請造訪 http://aka.ms/intuneenrollsvrchange。

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Configuration Manager Technical Preview 1702 的新功能

- **Android for Work 支援**

  您現在可以使用 Configuration Manager Technical Preview 1702，在混合式 MDM 環境中管理使用 Android for Work 的 Android 裝置。 現在可將支援的 Android 裝置註冊為 Android for Work 裝置，這會在裝置上建立工作設定檔，以便部署 Play for Work 中核准的應用程式。 您也可以為這些裝置設定及部署設定項目、合規性政策和資源存取設定檔。 如需詳細資訊，請參閱 [Android for Work 支援](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support)。

- **不符合規範的應用程式相容性設定**

  您現在可以在合規性政策中，為 Android 和 iOS 應用程式建立不符合規範的應用程式規則。 如果裝置已安裝指定的應用程式，則會標示為「不符合規範」，並根據對應的條件式存取原則而無法存取公司資源。 如需詳細資訊，請參閱[條件式存取裝置合規性政策改善](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements)。

- **PFX 憑證建立和發佈以及 S/MIME 支援**

  您現在可以建立 PFX 憑證，並將該憑證部署給混合式環境中的使用者。 這些憑證接著可供使用者已註冊的裝置用來加密及解密 S/MIME 電子郵件。 如需詳細資訊，請參閱[使用 S MIME 支援來建立 PFX 憑證](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support)。

- **對額外 iOS 組態設定的支援**
   
    您現在有 42 個可在設定項目中設定的額外 iOS 設定。 針對受監督的 iOS 裝置，已新增大部分的設定 (總計 35 個)。 如需詳細資訊，請參閱 [iOS 裝置的新合規性設定](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices)。

## <a name="january-2017"></a>2017 年 1 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

- **Android 7.1.1 支援**

  Intune 現在可完全支援及管理 Android 7.1.1。

- **解決 iOS 裝置處於非使用中狀態或管理主控台無法與其通訊的問題**

  當使用者的裝置失去與 Intune 的連線時，您可以為使用者提供新的疑難排解步驟，以協助他們重新取得公司資源的存取權。 請參閱[裝置處於非使用中狀態或管理主控台無法與其通訊](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them)。

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Configuration Manager Technical Preview 1701 的新功能

- **混合式 MDM 的建立精靈無法再將目標設為 Android 與 iOS 版本**

  從混合式行動裝置管理 (MDM) 的 Technical Preview 1701 開始，您在為受 Intune 管理的裝置建立新原則及設定檔時，不再需要以 Android 或 iOS 的特定版本為目標。 透過這項變更，混合式部署可更快為 Android 及 iOS 版本提供支援，而不需要新的 Configuration Manager 版本或延伸模組。 若要深入了解，請參閱[建立精靈無法再將目標設為 Android 與 iOS 版本](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)。


## <a name="notices"></a>通知

### <a name="end-of-support-for-android-43-and-lower"></a>終止支援 Android 4.3 與較舊版本
<!---1171127--->
*2017 年 7 月 6 日*

受管理的應用程式與 Android 版公司入口網站應用程式將需要 Android 4.4 或更新的版本，才能存取公司資源。 裝置若未在 10 月初之前更新，將無法再存取公司入口網站或前述的應用程式。 最晚不超過 12 月，所有註冊的裝置將在 12 月強制淘汰，而導致無法存取公司資源。 如果您未經由 MDM 來使用應用程式保護原則，應用程式將不再接收更新，應用程式的體驗品質也會隨著時間而下降。


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


### <a name="see-also"></a>另請參閱

- [過去的混合式 MDM 功能](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager 中 MDM 的新功能](https://technet.microsoft.com/library/mt445560.aspx)

