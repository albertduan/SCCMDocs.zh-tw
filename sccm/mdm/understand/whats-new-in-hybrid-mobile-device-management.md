---
title: "混合式 MDM 的新功能 | Microsoft Docs"
description: "了解 System Center Configuration Manager 與 Intune 的混合式部署可以使用的新行動裝置管理功能。"
ms.custom: na
ms.date: 11/18/2016
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
ms.sourcegitcommit: 9f3088e90c3259adc3c3b9c6873978d1db4dd1d8
ms.openlocfilehash: 05e4a9687d29c5377303afd8b08352a6a77fa58e

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

* [設定項目的額外設定和改進體驗](/sccm/core/plan-design/changes/whats-new-in-version-1610?branch=sccm-1610-release#new-compliance-settings-for-configuration-items)
* [DEP 設定檔的其他設定](#new-in-configuration-manager-technical-preview-1609)
* [商務用 Windows 市集的付費 App](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Windows 10 VPN 設定檔的原生連接類型](#new-in-configuration-manager-technical-preview-1609)
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

## <a name="new-hybrid-features-in-october-2016"></a>2016 年 10 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2016 年 10 月推出的下列 Intune 功能可在混合式部署中運作。

- **行動應用程式管理的條件式存取**

  您可以限制存取 Exchange Online，只讓支援 Intune 行動應用程式管理原則的應用程式存取，例如 Outlook。 [這項新功能](/intune/deploy-use/allow-policy-managed-apps-access-to-o365)可以完美配合 Intune 行動應用程式管理 (MAM) 原則，因為您可以封鎖內建郵件用戶端或其他尚未使用 Intune MAM 原則設定之應用程式的存取權。 這可確保您的使用者以使用 Intune MAM 保護的應用程式存取組織資料。 您可以透過 Azure 入口網站在 Intune 行動裝置應用程式管理中開始。 在 [設定] 刀鋒視窗中尋找新的 [條件式存取] 區段。

-   **適用於 Android 的 Intune 應用程式包裝工具**

  您可以使用 Intune 應用程式包裝工具，讓應用程式使用 Intune 行動應用程式管理 (MAM) 原則。

- **Android Samsung KNOX Standard 與 Intune 的相容性**

  Samsung Galaxy Ace 手機有些型號不能當成 Samsung KNOX Standard 裝置由 Intune 管理。 當您向 Intune 註冊這些裝置時，它們會改作為標準的 Android 裝置來管理。

  受影響的型號為︰

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  您和您的使用者不需要採取任何進一步的動作。 如需詳細資訊，請瀏覽 Samsung KNOX 網站。

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Configuration Manager Technical Preview 1610 的新功能

Configuration Manager Technical Preview 1610 於 2016 年 10 月推出下列新的混合式功能。

- **要求從管理主控台同步處理原則**

  您可以從 Configuration Manager 主控台要求同步處理已註冊的行動裝置原則，不必要求在裝置本身的公司入口網站應用程式中同步處理。 這是 [遠端裝置動作] 功能表中的新動作，稱為 **「Send Sync Request」** (傳送同步要求)，在 [裝置] 節點中選取行動裝置時會出現在功能區。

- **Windows Defender 組態設定**

  您現在可以使用 Configuration Manager 主控台中的設定項目，在 Intune 註冊的 Windows 10 電腦上設定 Windows Defender 用戶端設定。 設定項目精靈中有一個新的設定群組，稱為 **Windows Defender**。 請注意，只有 Windows 10 1511 版和更新版本才支援。


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)

Configuration Manager 2016 年 8 月 (最新分支) 未推出任何新的混合式功能。

## <a name="new-hybrid-features-in-september-2016"></a>2016 年 9 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2016 年 9 月推出的下列 Intune 功能可在混合式部署中運作。

- **Android 公司入口網站新增「通知」**

  新的通知圖示已經加入 Android 公司入口網站的首頁。 點選此圖示可存取 [通知] 頁面，向使用者顯示公司入口網站應用程式中需要注意的所有項目，例如不相容的裝置、註冊更新以及啟用註冊。 iOS 公司入口網站應用程式已有此通知體驗。 擁有新的 [通知] 頁面表示，只要裝置已註冊，使用者每次啟動或繼續公司入口網站時，不會看到 [公司存取設定] 頁面。 如果您建立自己的使用者指南，您可能想要更新自己的文件以反映這項變更。 在[這裡](https://aka.ms/androidcpupdate)尋找已更新的螢幕擷取畫面。

- **iOS 公司入口網站應用程式的支援變更**

  iOS 的 Microsoft Intune 公司入口網站應用程式的所有使用者，現在都必須使用其最新版本。 新的使用者只能夠下載最新版本，而目前的使用者則必須更新它。 最新版本需要 iOS 8.0 或更新版本，因此在裝置更新至 iOS 8.0 或更新版本，再將公司入口網站應用程式更新至最新版本前，執行較舊 iOS 版本的裝置無法使用公司入口網站或註冊。 執行版本低於 iOS 8.0 的已註冊裝置會繼續由 Intune 管理主控台所管理及列示。

- **Windows Phone 8.1 公司入口網站應用程式新增意見反應按鈕**

  Windows Phone 8.1 公司入口網站應用程式可讓使用者使用新的 [傳送意見反應] 按鈕，傳送有關應用程式的意見反應。 若要尋找按鈕，使用者可點選公司入口網站應用程式畫面右下方的「三個點」功能表，然後點選 [傳送意見反應]。 收集的匿名意見反應會協助 Microsoft 改善使用者的公司入口網站應用程式體驗。

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Configuration Manager Technical Preview 1609 的新功能

Configuration Manager Technical Preview 1609 於 2016 年 9 月推出下列新的混合式功能。

- **設定項目設定的額外設定和改進體驗**

  Android、iOS 和 Windows 已新增新的設定，只有套用至您在 [支援的平台] 頁面上所選平台的設定，才會顯示在精靈中。 如需詳細資訊，請參閱 [TP 1609 中的設定項目新相容性設定](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items)。

- **DEP 設定檔的其他設定**

  TouchID、ApplePay 及 Zoom 已加入為 iOS 裝置之 DEP 設定檔可設定的設定值。

- **商務用 Windows 市集的付費 App**

  現在，您可以在商務用 Windows 市集中新增付費及免費的應用程式，並將它們部署到組織中的使用者。 如需詳細資訊，請參閱 [TP 1609 的商務用 Windows 市集增強功能](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager)。

- **Windows 10 VPN 設定檔的原生連接類型**

  您現在可以在 Configuration Manager 主控台中不使用 OMA URI，以 Microsoft Automatic、IKEv2 和 PPTP 連線類型建立 MDM 的 Windows 10 VPN 設定檔。

- **Intune 相容性圖表**

  您可以使用 [監視] 工作區中的新圖表，快速檢視整部裝置的相容性和不相容的主要原因。 如需詳細資訊，請參閱 [TP 1609 中的 Intune 相容性圖表](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts)。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)

2016 年 9 月推出的下列新功能可用於 Microsoft Intune 和 Configuration Manager 1606 版 (最新分支) 的混合式部署。

- **iOS 10 支援**

  如果您有以所有 iOS 平台為目標的設定檔或設定項目，它們也會推送至 iOS 10。 我們也已經發行 Configuration Manager 1606 版的更新，讓您以個別 iOS 平台，包括 iOS 10 的設定檔和設定項目為目標。 您可以在 [管理] > [概觀] > [雲端服務] > [更新與服務]，使用 Configuration Manager 管理主控台安裝更新。 您可以在 [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616) 找到更新的詳細資訊。

## <a name="new-hybrid-features-in-august-2016"></a>2016 年 8 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2016 年 8 月推出的下列 Intune 功能可在混合式部署中運作。

- **公司入口網站應用程式對 Android 7 的支援**

  Android 的 Intune 公司入口網站應用程式為即將推出的行動裝置 Android 7.0 作業系統提供「零時差」支援。

- **Google 移除了 Android 7.0 裝置上的遠端密碼重設功能**

  Google 正在移除 IT 系統管理員和使用者從遠端重設 Android 7.0 裝置密碼的能力。 過去，IT 系統管理員可以從遠端重設使用者的密碼，讓使用者從公司入口網站重設其密碼。

- **Samsung KNOX Standard 裝置的允許和封鎖應用程式原則**

  您現在可以設定 Samsung KNOX Standard 裝置的自訂原則，讓您建立下列其中一項：

  - 在裝置上封鎖執行的應用程式清單。 即使已安裝，封鎖清單中定義的應用程式也無法在裝置上啟動。
  - 允許裝置使用者從 Google Play 商店安裝的應用程式清單。 沒有任何其他應用程式可以從該商店安裝。

  這些設定只能供執行 Samsung KNOX Standard 的裝置使用。 如需詳細資訊，請參閱[使用自訂原則來允許及封鎖 Samsung KNOX Standard 裝置的應用程式](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps)。

- **從公司入口網站的意見反應連結到 Microsoft**

   公司入口網站可讓使用者點選頁面底部的新 [意見反應] 連結，將其有關站台經驗的意見傳送給 Microsoft。 收集的匿名意見反應會協助 Microsoft 改善使用者的公司入口網站體驗。

- **iOS Managed Browser 版本至少要更新至 8.0**

  iOS 的 Microsoft Intune Managed Browser 應用程式已更新為支援執行 iOS 8.0 或更新版本的裝置。 雖然 iOS 7.1 裝置仍可使用現有的 Managed Browser 應用程式，但建議使用者更新至 iOS 8.0 或更新版本，以存取並充分利用新的 Managed Browser 功能。

### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview 的新功能

Configuration Manager Technical Preview 2016 年 8 月未推出任何新的混合式功能。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)

Configuration Manager 2016 年 8 月 (最新分支) 未推出任何新的混合式功能。

## <a name="new-hybrid-features-in-july-2016"></a>2016 年 7 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2016 年 7 月推出的下列 Intune 功能可在混合式部署中運作。

- **Xamarin SDK for Intune 應用程式可供使用**

  Intune 應用程式 SDK Xamarin 元件可讓您在以 Xamarin 建置的 iOS 和 Android 行動應用程式中，啟用 Intune 行動應用程式管理功能。 您可以在 [Xamarin 市集](https://components.xamarin.com/view/Microsoft.Intune.MAM)或 [Microsoft Intune Github 頁面](https://github.com/msintuneappsdk)找到元件。

- **註冊 Windows 裝置之改善的使用者經驗**

  當您使用條件式存取時，公司入口網站中已明確說明 Windows 8.1、Windows 10 Desktop 和 Windows 10 行動裝置的註冊步驟。 如果發生工作場所聯結 (WPJ) 失敗，使用者現在會看到不同的**裝置註冊**和**工作場所聯結**步驟，可輕鬆查看裝置狀態並完成程序。 分開的步驟也可以簡化 IT 系統管理員的疑難排解程序。 以前，當使用者嘗試註冊，且除了 WPJ 以外的所有註冊步驟都成功時，註冊的裝置不會出現在裝置清單中供使用者識別，進而造成使用者混淆。

 - **Windows 10 裝置現在可使用完整抹除**

    可以抹除註冊為行動裝置的 Windows 10 電腦和膝上型電腦，將裝置重設回其原廠設定。 如需詳細資訊，請參閱 [How to protect your devices with remote wipe](/sccm/mdm/deploy-use/wipe-lock-reset) (如何保護裝置免於遠端抹除)。

- **iOS 公司入口網站應用程式中的裝置註冊管理員帳戶變更**

  為改善效能和延展性，Intune 不再於 iOS 公司入口網站應用程式的 [我的裝置] 窗格中，顯示所有裝置註冊管理員 (DEM) 裝置。 僅顯示執行應用程式的本機裝置，而且僅限透過公司入口網站應用程式註冊的本機裝置。

  DEM 使用者可在本機裝置上執行動作，但其他已註冊裝置的遠端管理只能從 Intune 管理主控台執行。 此外，Intune 會淘汰使用 Apple 裝置註冊方案或 Apple Configurator 工具的 DEM 帳戶。 這兩種註冊方法都支援共用 iOS 裝置的無使用者註冊。

  只有當共用裝置的無使用者註冊無法使用時，才使用 DEM 帳戶。 如需詳細資訊，請參閱[使用 Microsoft Intune 中的裝置註冊管理員註冊公司所擁有的裝置](../deploy-use/enroll-devices-with-device-enrollment-manager.md)。

- **Android 公司入口網站應用程式的變更**

  Android 使用者如果看到裝置缺少必要憑證的錯誤訊息，可以點選 「How to resolve this」 (問題解決方法) 按鈕，取得安裝所缺憑證的步驟。 如果使用者完成這些步驟，但看到其他「缺少憑證」錯誤訊息，就需要連絡 IT 系統管理員並提供此連結，訊息中包含 IT 系統管理員可用來解決憑證問題的步驟。

- **限制已註冊 Android 裝置的側載應用程式安裝**

  Android 裝置無法再透過公司入口網站來安裝應用程式，除非裝置已使用 Android 的 Intune 公司入口網站應用程式向 Intune 註冊。


### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview 的新功能

Configuration Manager Technical Preview 2016 年 7 月未推出任何新的混合式功能。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)

Configuration Manager Technical Preview 各版本過去提供的下列功能，目前可在 Intune 和 Configuration Manager 1606 版 (最新分支) 的混合式部署中使用。

* 從 Configuration Manager 主控台尋找、管理及散發 Windows 10 裝置的商務用 Windows 市集應用程式 ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   適用於 Android 裝置的 SmartLock 設定 ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   適用於 Windows 10 裝置的應用程式觸發的 VPN ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   遠端裝置動作的全新體驗 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   商務用 Windows 市集應用程式 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   針對大量購買之應用程式的一般改進 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Windows 資訊保護 (WIP) ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   自動將裝置分類為集合 ([1606](whats-new-hybrid-archive.md#new-in-1606-technical-preview))

如需新功能的資訊，請參閱指定的 Technical Preview 版本文件。

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


