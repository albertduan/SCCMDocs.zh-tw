---
title: "封存 | 新混合式 MDM 的內容 | Microsoft Intune | System Center Configuration Manager"
description: "System Center Configuration Manager 與 Intune 的混合式部署可以使用過去之行動裝置管理功能的封存。"
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: bfc4baefbdddc5125c38272f2087d214151c91d5
ms.openlocfilehash: 4c0910ae365e1fda7b9747b79e13782a6056c0da

---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 和 Microsoft Intune 過去的混合式功能

*適用對象：System Center Configuration Manager (最新分支)*

本文提供 System Center Configuration Manager 與 Microsoft Intune 混合式部署可以使用過去的行動裝置管理 (MDM) 功能的詳細資訊。  

##  <a name="compatibility-with-configuration-manager-versions"></a>與 Configuration Manager 版本的相容性  

 本文的各節會列出 3 個不同目錄下的混合式功能。 請使用下列指導方針判斷每個類別功能與 Configuration Manager 不同版本的相容性︰  

|功能類別|
|-|  
|**Microsoft Intune 的新功能**：通常此類別下列出的所有功能都應該能夠搭配所有的 Configuration Manager 版本，包括 System Center 2012 R2 Configuration Manager 版本，因為這些功能只需要 Intune 服務，不需要其他的 Configuration Manager 功能。<br /><br /> **Configuration Manager Technical Preview 的新功能**：此類別下列出的所有功能只能搭配 Technical Preview 版本使用。 若要試用這些功能，您必須安裝功能描述中指定的 Technical Preview 版本。 如需詳細資訊，請參閱 [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) 。<br /><br /> **Configuration Manager 的新功能 (最新分支)**：此類別下列出的所有功能僅能搭配指定的 Configuration Manager 版本 (最新分支) 使用，例如 1511 版或 1602 版。 如果您的混合式部署使用舊版的 Configuration Manager，即必須升級到功能描述中指定的 Configuration Manager 版本 (最新分支)。 如需詳細資訊，請參閱[升級至 System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。|  

## <a name="new-hybrid-features-in-june-2016"></a>2016 年 6 月的新混合式功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能
2016 年 6 月推出的下列 Intune 功能可在混合式部署中運作。

- **Intune 服務健全狀況**：Intune 服務健全狀況資訊已和其他 Microsoft 服務一起移至中央位置。 現在，可以在 Office 365 管理入口網站的 [服務健全狀況] 下找到這項資訊。 如需詳細資訊，請參閱此[部落格文章](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/)。

- **增強的 Windows 10 企業資料原則設定體驗**

  Intune 現在提供較佳的 Windows 10 資訊保護原則設定體驗。 增強功能包括以更好的方式來建立應用程式規則、指定網路界限定義，以及其他 Windows 資訊保護設定。 若要深入了解，請參閱[使用 Microsoft Intune 建立 Windows 資訊保護 (WIP) 原則](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune)。

- **適用於 Intune 的 Cisco ISE 網路存取控制原則**

  同時使用 Cisco Identity Service Engine (ISE) 2.1 及 Microsoft Intune 的客戶，可以在 ISE 中設定網路存取控制原則。使用此原則，則需要使用 WiFi 或 VPN 連接網路的裝置必須符合下列條件，才能獲准存取︰

  - 必須由 Intune 管理
  - 必須與所有已部署的 Intune 相容性原則相容

  會提示不相容裝置的使用者註冊，並修復任何相容性問題以獲得存取權。

- **瀏覽器的條件式存取**

  您可以設定 Exchange Online 和 SharePoint Online 條件式存取原則，以便只從受管理和相容的 iOS 和 Android 裝置上受支援的網頁瀏覽器存取它們。 嘗試使用 iOS 和 Android 裝置登入 Outlook Web Access (OWA) 和 SharePoint 網站的使用者，系統會提示他們向 Intune 註冊其裝置，以及必須修正所有不相容的問題才能完成登入。 如需詳細資訊，請參閱

  * [使用 Intune 限制對 Exchange Online 及新 Exchange Online Dedicated 的電子郵件存取](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [使用 Microsoft Intune 限制存取 SharePoint Online](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online 支援條件式存取**

  您可以設定 Dynamics CRM Online 的條件式存取原則，使它只能被受管理和相容的 iOS 和 Android 裝置存取。 嘗試登入 iOS 和 Android 的 Dynamics CRM 行動應用程式的使用者，系統會提示他們向 Intune 註冊，以及必須修復所有不相容的問題，才能完成登入。 如需詳細資訊，請參閱[使用 Intune 限制對 Dynamics CRM Online 的存取](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune)。

- **Android 公司入口網站應用程式更新**

  下列的 Intune 新原則會影響 Android 公司入口網站使用者︰   

  原則  |對使用者的影響  
  ---------|---------
  要求裝置不得安裝來源不明的應用程式 (Android 4.0+)     |  Android 4.0 或更新裝置的使用者會看到此訊息：「必須停用來自未知來源的安裝。」 使用者必須移至裝置的 [設定] > [安全性]，並關閉 [未知來源]。 相容性訊息中的連結可讓使用者取得訊息的詳細資訊，以及必須關閉設定的原因。
  要求裝置不得安裝來源不明的應用程式 (Android 4.0+)  |    Android 4.0 或更新裝置的使用者會看到此訊息：「掃描裝置中的安全性威脅。」 使用者必須移至裝置的 [設定] > [Google] > [安全性]，並開啟 [掃描裝置中的安全性威脅]。 相容性訊息中的連結可讓使用者取得訊息的詳細資訊，以及必須開啟設定的原因。     
  需要停用 USB 偵錯 (Android 4.2+)  | Android 4.2 或更新裝置的使用者會看到此訊息：「必須停用 USB 偵錯。」 使用者必須移至裝置的 [設定] > [開發人員選項]，並關閉 [USB 偵錯]。 相容性訊息中的連結可讓使用者取得訊息的詳細資訊，以及必須關閉設定的原因。
  Android 安全性修補程式等級下限 (Android 6.0+)  | Android 6.0 或更新裝置的使用者會看到此訊息：「此裝置不符合最低的 Android 安全性更新程式等級。」 使用者必須安裝必要的安全性修補程式。 相容性訊息中的連結可讓使用者取得如何安裝必要安全性修補程式的相關資訊，以及查看目前已安裝的安全性修補程式。

- **iOS 公司入口網站應用程式更新**

  * 現在當使用者安裝企業營運應用程式時，就會看到改善的應用程式安裝體驗。 如果應用程式安裝花很長的時間，使用者可以手動同步處理裝置，強制同步處理程序繼續執行。 若要檢閱使用者指示，請參閱＜手動同步 iOS 裝置＞。
  * 適用於 iOS 的 Microsoft Intune 公司入口網站應用程式已更新為支援 iOS 8.0 版和更新版本。 此更新表示唯有裝置執行的是 iOS 8.0 版或更新版本時，使用者才能安裝公司入口網站應用程式，並向 Intune 註冊新的裝置。 若使用者已經註冊在不支援的 iOS 版本中執行的裝置，則可繼續使用其裝置上的公司入口網站應用程式。


### <a name="new-in-1606-technical-preview"></a>1606 Technical Preview 的新功能
2016 年 6 月推出的下列新功能可用於 Intune 和 Configuration Manager Technical Preview 1606 的混合式部署。

- **自動將裝置分類為集合**

  您可以建立裝置類別，如此可在您使用 Configuration Manager 與 Intune 時自動將裝置放在裝置集合中。 使用者向 Intune 註冊裝置時，必須選擇裝置類別。 您也可以從 Configuration Manager 主控台中變更裝置類別。 如需詳細資訊，請參閱 [Capabilities in Technical Preview 1606 for System Center Configuration Manager ](/sccm/core/get-started/capabilities-in-technical-preview-1606.md) (System Center Configuration Manager Technical Preview 1606 的功能) 的 [Automatically categorize devices into collections](/sccm/core/get-started/capabilities-in-technical-preview-1606.md#dmp_category) (自動將裝置分類為集合)。

  > [!IMPORTANT]
  > 這項功能適用於 Microsoft Intune 的 2016 年 6 月版。 請先確定已更新為此版，再嘗試這些程序。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)
Configuration Manager 2016 年 6 月 (最新分支) 未推出任何新的混合式功能。

##  <a name="new-hybrid-features-in-may-2016"></a>2016 年 5 月的新混合式功能  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能  
 2016 年 5 月推出的下列 Intune 功能可在混合式部署中運作。

- **MAM SDK︰支援 PIN 長度設定**

  您現在可以指定與裝置 PIN 相似的 MAM 應用程式 PIN 長度。 這需要使用者符合您設定的新限制。 PIN 螢幕為因應較長的輸入而略有修改。 如需詳細資訊，請參閱 [Microsoft Intune 中的 Android 行動應用程式管理原則設定](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings)和 [iOS 行動應用程式管理原則設定](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings)。  

- **適用於 iOS 和 Android 的商務用 Skype**

  您現在可以商務用 Skype 及[沒有註冊原則的 MAM](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune) 為目標。 一旦使用者登入，就會套用 MAM 原則。  

- **可以 MAM 原則管理的新應用程式**

  適用於 Android 的 Microsoft Word、Excel 和 PowerPoint 應用程式，現在可與未向 Intune 註冊的裝置上的 MAM 原則建立關聯。 如需支援的應用程式完整清單，請移至 [Microsoft Intune 應用程式合作夥伴](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx)頁面的 Microsoft Intune 行動應用程式庫。  

- **Android 公司入口網站應用程式︰使用者快顯通知**

  當使用者在公司入口網站註冊或移除裝置時，Android 公司入口網站應用程式就會顯示快顯通知。  

- **公司入口網站︰裝置識別橫幅會向使用者提供詳細資訊**

  現在當使用者使用公司入口網站時，會更容易識別他們選取的裝置。 如果選取了錯誤的裝置，他們可以點選首頁橫幅的 [點選這裡] 連結，選取正確的裝置。  


### <a name="new-in-1605-technical-preview"></a>1605 Technical Preview 的新功能  
 2016 年 5 月推出的下列新功能可用於 Intune 和 Configuration Manager Technical Preview 1605 的混合式部署。 這些功能都需要使用 Configuration Manager 主控台設定及管理。  

- **適用於 Windows 10 裝置的應用程式觸發型 VPN**

  針對使用 Configuration Manager 與 Intune 管理的 Windows 10 裝置，您可以加入會自動開啟 VPN 連線的應用程式清單，這個 VPN 連線是透過 Configuration Manager 管理主控台所設定。 如需詳細資訊，請參閱 [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (System Center Configuration Manager Technical Preview 1605 的功能) 中的 [App-triggered VPN for Windows 10 devices](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Windows 10 裝置的應用程式觸發型 VPN)。  

- **遠端裝置動作的全新體驗**

  從 Configuration Manager 主控台執行遠端裝置動作的體驗已改善。

  現在從 [資產與相容性] 工作區存取 [遠端裝置動作] 功能表即可找到 [淘汰/抹除]、[重設密碼]、[遠端鎖定] 和 [略過啟用鎖定] 等常見動作。

  如需詳細資訊，請參閱 [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (System Center Configuration Manager Technical Preview 1605 的功能) 中的 [New experience for remote device actions](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) (遠端裝置動作的新體驗)。  

- **商務用 Windows 市集應用程式**

  [商務用 Windows 市集](https://www.microsoft.com/en-us/business-store)是您可以在其中為您的組織尋找並個別或大量採購應用程式的地方。 藉由將市集連接到 Configuration Manager，您便可以從 Configuration Manager 主控台管理大量採購的應用程式。 如需詳細資訊，請參閱 [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (System Center Configuration Manager Technical Preview 1605 的功能) 中的 [Windows Store for Business apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) (商務應用程式的 Windows 市集)。  

- **針對大量採購應用程式的一般改進**

  商務用 Windows 市集和 iOS 應用程式市集的大量採購應用程式已合併到 [市集應用程式的授權資訊] 檢視。 此外，大量採購 iOS 應用程式的方式也已改良。 如需詳細資訊，請參閱 [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (System Center Configuration Manager Technical Preview 1605 的功能) 中的 [General improvements for volume-purchased apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) (大量採購應用程式的一般改進)。  

- **使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置**

  您現在可以透過匯入國際行動設備識別碼 (IMEI)，識別公司擁有的裝置。 您可以上傳一個包含裝置 IMEI 編號的逗號分隔值 (.csv) 檔案，也可以手動輸入裝置資訊。  您也可以匯入 iOS 裝置的序號。  如需詳細資訊，請參閱 [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (System Center Configuration Manager Technical Preview 1605 的功能) 中的 [Pre-declare corporate-owned devices with IMEI or iOS serial number](../../core/get-started/capabilities-in-technical-preview-1605.md#pre-declare-corporate-owned-devices-with-with-imei-or-ios-serial-number) (使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置)。  

- **Windows 資訊保護 (WIP)**

  您可以建立讓您部署 Windows 資訊保護 (WIP) 原則的設定項目，包括讓您選擇受保護的應用程式、WIP 保護層級，以及如何在網路上尋找企業資料。 如需 WIP 的詳細資訊，請參閱下列主題：  

  -   [使用 Windows 資訊保護 (WIP) 保護您的企業資料](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [使用 System Center Configuration Manager 建立和部署 Windows 資訊保護 (WIP) 原則](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)  
 Configuration Manager 2016 年 5 月 (最新分支) 未推出任何新的混合式功能。  

##  <a name="new-hybrid-features-in-april-2016"></a>2016 年 4 月的新混合式功能  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能  
 2016 年 4 月推出的下列 Intune 功能可在混合式部署中運作。  

- **MAM 使用者相容性**

  您現在可以檢視 Azure Active Directory (AAD) 租用戶中任何使用者的應用程式管理原則狀態。  如需詳細資訊，請參閱 Intune 程式庫的[使用 Microsoft Intune 監視行動應用程式管理原則](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)。  

- **防止 Outlook 連絡人同步的 MAM 控制項 (Android)**

  現提供新設定，讓您防止應用程式同步處理 Android 裝置的原生通訊錄連絡人。 這個新的設定最初受 Android 裝置的 Outlook 應用程式支援。 如需詳細資訊，請參閱 Intune 程式庫的[使用 Microsoft Intune 建立及部署行動應用程式管理原則](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)。  

- **公司入口網站的增強功能**

  當 Windows 10 行動裝置和 Windows Phone 8.1 使用者安裝企業營運應用程式時，將會看到下列的新狀態，提供他們有關安裝狀態的更詳細資訊︰  

  -   **正在等候裝置同步** – 使用者點選了 [安裝]，裝置現嘗試同步處理 Intune 基礎結構。 必須先同步處理，才能完成安裝。 如果同步處理程序需要較長的時間或已停止，使用者也可以點選「正在等候裝置同步」訊息連結，查看如何手動同步處理裝置與 Intune 的指示。  

  -   **下載** – 正在處理使用者的下載要求，且裝置正在下載並安裝應用程式。  

- **Android 公司入口網站應用程式的增強功能**

  未向 Intune 註冊的裝置以及未安裝正確憑證的使用者，無法登入 Android 公司入口網站應用程式，並會看到此訊息：「由於您的裝置遺漏所需的憑證，因此您無法登入。」 此訊息包含「如何解決此問題」的連結，使用者可以點選它查看安裝憑證的指示。 若要查看解決此問題的使用者遵循步驟，請參閱 Intune 程式庫的[您的裝置遺漏必要的憑證](/intune/enduser/using-your-android-device-with-intune)。  

- **iOS 公司入口網站應用程式的增強功能**

  已對下拉即可重新整理動作加入支援，以重新整理主畫面內容，包括列出的應用程式、列出的裝置，以及 IT 連絡人資訊。 下拉即可重新整理動作不檢查相容性或原則資訊，而這項作業只要選取目前裝置的磚並點選 [同步] 按鈕即可完成。  

- **Windows 10 行動裝置和 Windows Phone 8.1 公司入口網站應用程式的增強功能**

  現在當使用者安裝企業營運應用程式時，就會看到改善的應用程式安裝體驗。 如果應用程式安裝花很長的時間，使用者可以手動同步處理裝置，強制同步處理程序繼續執行。 若要檢閱使用者指示，請參閱 Intune 程式庫中[手動同步裝置以加速安裝應用程式](/intune/enduser/using-your-windows-device-with-intune)。  

###  <a name="new-in-1604-technical-preview"></a>1604 Technical Preview 的新功能
 2016 年 4 月推出的下列新功能可用於 Intune 和 Configuration Manager Technical Preview 1604 的混合式部署。 這些功能都需要使用 Configuration Manager 主控台設定及管理。  

- **從 Configuration Manager 主控台尋找、管理及散發 Windows 10 裝置的商務用 Windows 市集應用程式**


  Configuration Manager Technical Preview 1604 提供商務用 Windows 市集的支援，可協助您尋找、管理及散發應用程式到您管理中的 Windows 10 裝置。 如需詳細資訊，請參閱 [Capabilities in Technical Preview 1604 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604) (System Center Configuration Manager Technical Preview 1604 的功能) 中的 [Manage volume-purchased apps from the Windows Store for Business](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) (從商務用 Windows 市集管理大量採購應用程式)。  

- **適用於 Android 裝置的 SmartLock 設定**

  Android 和 Samsung KNOX 設定項目中已加入新設定，可讓您控制相容 Android 裝置上的 SmartLock 功能。  您可以使用此設定來防止使用者設定 SmartLock。 請參閱 [Capabilities in Technical Preview 1604 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md) (System Center Configuration Manager Technical Preview 1604 的功能) 中的 [SmartLock setting for Android devices](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) (適用於 Android 裝置的 SmartLock 設定)。  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)  
 Configuration Manager 2016 年 4 月 (最新分支) 未推出任何新的混合式功能。  

##  <a name="new-hybrid-features-in-march-2016"></a>2016 年 3 月的新混合式功能  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能  
 2016 年 3 月推出的下列 Intune 功能可在混合式部署中運作。  

- **防止 Outlook 連絡人同步的 MAM 控制項 (iOS)**

  現提供新設定，讓您防止應用程式同步處理 iOS 裝置的原生通訊錄連絡人。 這個新的設定受 iOS 裝置的 Outlook 應用程式支援。 如需此設定及其他設定的詳細資訊，請參閱 Intune 程式庫的[使用 Microsoft Intune 建立及部署行動應用程式管理原則](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)。  

- **商務用 Skype Online 支援條件式存取**

  您可以設定商務用 Skype Online 的條件式存取原則，使它只能被受管理和相容的 iOS 和 Android 裝置存取。  如需詳細資訊，請參閱 Intune 程式庫的[管理商務用 Skype Online 的存取](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune)。  

- **支援 iOS 9.3**

  在 3 月 21 星期一，Apple 宣布 iOS 9.3 上市。 目前可管理 iOS 裝置的所有現有 Intune 功能，在使用者將裝置升級至 iOS 9.3 時，都會繼續順利運作。  

- **Windows 應用程式套件可以直接從公司入口網站取得**

  Windows 8、Windows 8.1 和 Windows RT 電腦的使用者現在可以直接從公司入口網站安裝 Windows 應用程式套件 (副檔名為 .appx)。 過去，您必須部署，或使用者必須在裝置上安裝公司入口網站應用程式，才能安裝應用程式。  

- **使用者可以從公司入口網站遠端鎖定裝置**

  公司入口網站新增了新的 [遠端鎖定] 選項，如果使用者的裝置遺失或遭竊，可讓他們從入口網站遠端鎖定裝置。  

- **協力廠商 MDM 解決方案中註冊的裝置，利用 iOS "Open-In"管理**

  您可以使用協力廠商行動裝置管理 (MDM) 廠商來利用 iOS "Open-In" 管理。 您可以在組態設定檔設定中設定限制，並使用 MDM 軟體部署。 當使用者安裝受管理的應用程式時，就會套用這些限制。 詳情請參閱 Intune 程式庫的 [Microsoft Intune 行動應用程式管理原則和 iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune)。  

- **支援 MAM 的 Microsoft 應用程式**

  可與 Intune 行動應用程式管理原則一起使用的 Microsoft 應用程式清單，已更新至包含最新的應用程式 (僅限向 Intune 註冊的裝置)。  

- **將 Adobe Reader for Microsoft Intune 部署到企業中 Intune 管理的 iOS 裝置**

  在已註冊裝置上的 Adobe Reader for iOS 應用程式現在可用 Intune 行動應用程式管理原則管理。  

- 支援 Android 的 Rights Management 共用應用程式

  IT 系統管理員可以部署行動應用程式管理原則，讓使用者可以更安全地檢視影像、AV 和 PDF 檔案，無論 IT 是否使用 Intune 來管理裝置。  

- **Android 和 iOS 公司入口網站應用程式的增強功能**

  -   當使用者啟動受行動應用程式管理 (MAM) 管理的應用程式時，會看到應用程式受公司管理的通知訊息。 使用者現在可以點選 [Learn More] (深入了解) 連結，了解「受管理應用程式」意義的詳細資訊。 他們也可以點選 [Don’t Show Again] (不要再顯示)，在啟動應用程式時不再顯示訊息。  

  -   已加入新畫面來引導使用者進行註冊程序，並提供使用者應該註冊的原因，以及 IT 系統管理員可在已註冊裝置上看見與否之內容的詳細資訊。  

  -   註冊錯誤訊息現在會顯示在公司入口網站應用程式中。  

### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview 的新功能  
 Configuration Manager Technical Preview 2016 年 3 月未推出任何新的混合式功能。  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)  
 2016 年 3 月推出的下列新功能可用於 Intune 和 Configuration Manager 1602 版 (最新分支) 的混合式部署。 這些功能都需要使用 Configuration Manager 主控台來設定及管理。  

- **iOS 應用程式設定原則**

  在 Configuration Manager 1602 版 (最新分支) 中您可以使用應用程式設定原則，提供使用者執行 iOS 應用程式時可能需要的設定。 如需詳細資訊，請參閱 [Configure iOS apps with app configuration policies in System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) (在 System Center Configuration Manager 中使用應用程式設定原則設定 iOS 應用程式)。  

- **管理大量採購的 iOS 應用程式**

  在 Configuration Manager 1602 版 (最新分支)中，您可從應用程式市集匯入授權資訊，並追蹤您已使用多少個授權，協助您部署和管理從 Apple 大量採購方案 (VPP) 大量購買的應用程式。 如需詳細資訊，請參閱 [Manage volume-purchased iOS apps with System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps) (使用 System Center Configuration Manager 管理大量採購的 iOS 應用程式)。  

- **自動建立 Office 行動應用程式**

  從 Configuration Manager 1602 版 (最新分支) 開始，當您從 1511 版升級時會建立下列 Android 和 iOS 版的 Microsoft Office 行動應用程式：  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (僅限 iOS)  
  -   Microsoft Outlook  

  您可以在 Configuration Manager 主控台的 [應用程式] 節點中找到這些應用程式。 如需部署應用程式的詳細資訊，請參閱 [How to deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md) (如何使用 System Center Configuration Manager 部署應用程式)。  

- **Android Samsung KNOX 裝置的 Kiosk 模式設定**

  Kiosk 模式允許您限制裝置只能執行某些特定功能。  從 Configuration Manager 1602 版 (最新分支) 開始，即可指定 Samsung KNOX 裝置的 Kiosk 模式設定。 如需詳細資訊，請參閱[如何為不是使用 System Center Configuration Manager 用戶端所管理的 Android 和 Samsung KNOX 裝置建立組態項目](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)。  

- **iOS 啟用鎖定**

  從 Configuration Manager 1602 版 (最新分支) 開始，您可以管理 iOS 啟用鎖定，這是 iOS 7.1 和更新版本裝置之「尋找我的 iPhone」應用程式中的功能。 當裝置上使用「尋找我的 iPhone」應用程式時，啟用鎖定會自動啟用。  如需詳細資訊，請參閱[使用 System Center Configuration Manager 管理 iOS 啟用鎖定](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock)。  



<!--HONumber=Nov16_HO1-->


