---
title: "1602 的新功能 | System Center Configuration Manager"
description: "下列各節提供 System Center Configuration Manager 1602 版中的變更和推出的新功能。"
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 0803a13bb58f0d02803c34e6a3cb20f5e6ba60b7

---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>System Center Configuration Manager 1602 版的新功能

*適用對象：System Center Configuration Manager (最新分支)*


System Center Configuration Manager 1602 更新，是只能從執行版本為 1511 的原安裝站台取得的主控台內更新。 1511 版是您用來安裝新 Configuration Manager 站台的初始基準版本。  


> [!TIP]  
>  深入了解：  
>   
>   -   [安裝新的站台](/sccm/core/servers/deploy/install) (使用 1511 等基準版本)  
>   -   [在站台安裝更新](/sccm/core/servers/manage/updates) (如更新 1602)  

 下列各節提供 Configuration Manager 1602 版中的變更和推出的新功能詳細資料。  

## <a name="site-infrastructure"></a>站台基礎結構  

###  <a name="a-namebkmkupgradeosa-in-place-upgrade-the-operating-system-of-site-servers-that-run-windows-server-2008-r2"></a><a name="bkmk_UpgradeOS"></a> 就地升級執行 Windows Server 2008 R2 之站台伺服器的作業系統  
 執行 1602 或更新版本的 Configuration Manager 站台支援將站台伺服器作業系統從 Windows Server 2008 R2 就地升級到 Windows Server 2012 R2。  

> [!WARNING]  
>  在升級到 Windows Server 2012 R2 之前，您必須從伺服器 **解除安裝 WSUS 3.2** 。  
>   
>  如需此重要步驟的資訊，請參閱 Windows Server 文件中 [Windows Server Update Services 概觀](https://technet.microsoft.com/library/hh852345.aspx) 的＜新功能和變更的功能＞一節。  

 若要升級伺服器，您需使用 Windows Server 2012 R2 升級程序，而不需在升級後執行 Configuration Manager 站台伺服器還原。  如需升級程序，請參閱 Windows Server 文件中的 [Windows Server 2012 R2 的升級選項](https://technet.microsoft.com/library/dn303416.aspx) 。  

###  <a name="a-namebkmkaoaga-sql-server-alwayson-availability-groups"></a><a name="bkmk_AOAG"></a> SQL Server AlwaysOn 可用性群組  
 您可以使用 SQL Server AlwaysOn 可用性群組於主要站台和管理中心網站裝載站台資料庫，以做為高可用性和災害復原方案。  

 如需詳細資訊，請參閱[適用於 System Center Configuration Manager 之高可用性站台資料庫的 SQL Server AlwaysOnn](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)  

## <a name="operating-system-deployment"></a>作業系統部署  

### <a name="windows-10-servicing"></a>Windows 10 服務  
 在 Configuration Manager 1602 版中，新增了下列對 Windows 10 服務的改進：  

-   針對維護計劃提供了新的篩選選項，可讓您針對 [語言]、[必要] 及 [標題] 進行篩選。 只有符合指定準則的升級會新增至相關聯的部署。  

-   當您選取 [升級] 分類進行軟體更新同步處理時，將出現警告對話方塊，讓您知道需有 WSUS 4.0 [Hotfix 3095113](https://support.microsoft.com/kb/3095113) 才能順利同步處理軟體更新，且 Windows 10 服務才能正常運作。 您可以從對話方塊移至關聯的知識庫文章。  

-   可用的 Windows 10 升級現在只顯示於 Configuration Manager 主控台的 [Windows 10 服務] \ [所有 Windows 10 更新] 節點。 這些更新已不再顯示於主控台的 [軟體更新] \ [所有軟體更新] 節點中。  

-   維護計劃被視為是一項高風險部署，[選取集合] 視窗只會顯示與站台內容中所設定之部署驗證設定相符的自訂集合。 如需詳細資訊，請參閱 [Settings to manage high-risk deployments for System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md)。  

-   系統將以對話方塊提示啟動 Windows 10 升級套件的使用者，讓他們知道其將升級作業系統。  

## <a name="application-management"></a>應用程式管理  

### <a name="ios-app-configuration-policies"></a>iOS 應用程式設定原則  
 您可以使用 Configuration Manager 應用程式設定原則，來提供使用者執行 iOS 應用程式時可能需要的設定。 例如，應用程式可能需要使用者指定自訂的連接埠號碼、語言、安全性或公司標誌等品牌設定。   
如果使用者輸入不正確的設定，可能會增加技術支援中心的負擔，並使新應用程式的採用速度變慢。  

 應用程式組態原則可協助您避免這些問題；您可以在使用者執行應用程式之前，先在原則中將這些設定部署給使用者。 接著會自動提供這些設定，使用者不需要採取任何動作。  

 如需詳細資訊，請參閱[在 System Center Configuration Manager 中使用應用程式設定原則設定 iOS 應用程式](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md)。  

### <a name="manage-volume-purchased-ios-apps"></a>Manage volume-purchased iOS apps  
 Configuration Manager 可藉由從應用程式市集匯入授權資訊，並追蹤您已使用多少個授權，協助您部署和管理從「Apple 大量採購方案」(VPP) 大量購買的應用程式。  

 如需詳細資料，請參閱[使用 Configuration Manager 管理您透過大量採購方案購買的 iOS 應用程式](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md)。  

### <a name="automatic-creation-of-office-mobile-apps"></a>自動建立 Office 行動應用程式  
 當您從 1511 更新至 1602 版時，Configuration Manager 會自動為 Android 和 iOS 建立下列 Microsoft Office 行動應用程式：  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (僅限 iOS)  

-   Microsoft Outlook  

您可以在 Configuration Manager 主控台的 [應用程式] 節點中找到這些應用程式。  

 如何有關部署應用程式的詳細資訊，請參閱[如何使用 System Center Configuration Manager 部署應用程式](../../../apps/deploy-use/deploy-applications.md)。  

## <a name="software-updates"></a>軟體更新  

### <a name="manage-office-365-client-updates"></a>管理 Office 365 用戶端更新  
 System Center Configuration Manager 能夠使用軟體更新管理工作流程來管理 Office 365 用戶端更新。 如需詳細資訊，請參閱[使用 System Center Configuration Manager 來管理 Office 365 ProPlus 更新](/sccm/sum/deploy-use/manage-office-365-proplus-updates)。  

## <a name="compliance-settings"></a>相容性設定  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>執行 Windows 10 團隊版之裝置的相容性設定  
 在 **Windows 8.1 和 Windows 10** 設定項目中已加入新的設定，用來協助您控制執行 Windows 10 團隊版的裝置 (例如 Surface Hub 裝置)。  

 如需詳細資料，請參閱[如何為不是使用 System Center Configuration Manager 用戶端所管理的 Windows 8.1 和 Windows 10 裝置建立組態項目](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)。  

### <a name="kiosk-mode-settings-for-android-samsung-knox-devices"></a>Android Samsung KNOX 裝置的 Kiosk 模式設定  
 Kiosk 模式允許您限制裝置只能執行某些特定功能。 例如，您可以允許裝置只執行您指定的一個受管理應用程式，也可以停用裝置上的音量按鈕。 這些設定可能用於裝置的展示模型，或是專用來只執行一個功能的裝置 (例如銷售點裝置)。 在 Configuration Manager 中，您現在可以為 Samsung KNOX 裝置指定 Kiosk 模式。  

 如需詳細資料，請參閱[如何為不是使用 System Center Configuration Manager 用戶端所管理的 Android 和 Samsung KNOX 裝置建立設定項目](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)。  

## <a name="conditional-access"></a>條件式存取  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>System Center Configuration Manager 所管理電腦的條件式存取  
 在此版本之前，若要設定電腦的條件式存取，該電腦必須在 Intune 中註冊或成為加入網域的電腦。 從 1602 更新開始，即可支援 System Center Configuration Manager 所管理電腦的條件式存取。 針對受 System Center Configuration Manager 管理的電腦，您可以限制只有符合您所設定之相容性原則的裝置才能存取 Exchange Online 和 SharePoint Online。  

 如需詳細資料，請參閱[管理 System Center Configuration Manager 所管理之電腦對 O365 服務的存取](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)。  

### <a name="restricting-access-based-on-device-health-attestation-status"></a>根據裝置健康情況證明狀態限制存取  
 您現在可以根據「健康情況證明服務」所報告的裝置健康情況，限制對電子郵件和 O365 服務的存取。 此外，Intune 所管理的裝置也包括在裝置健康情況報告中。  

 新的相容性規則已新增到 Configuration Manager 主控台，可讓您指定是否應該根據裝置的健康情況狀態來允許或封鎖裝置的存取。   如需有關健康情況證明服務及 Intune 中如何報告裝置健康情況的詳細資料，請參閱 [System Center Configuration Manager 的健康情況證明](../../../core/servers/manage/health-attestation.md)。  

### <a name="new-compliance-policy-rules"></a>新的相容性原則規則  
 為了支援更佳的安全性需求，加入了新的相容性原則規則 (例如自動更新、可將裝置解除鎖定的密碼)。  


 如需詳細資料，請參閱 [System Center Configuration Manager 的裝置相容性原則](../../../protect/deploy-use/device-compliance-policies.md)。  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>確定已註冊且相容的裝置一律可以存取 Exchange 內部部署  
 **預設規則覆寫 - 一律允許已在 Intune 註冊且相容的裝置存取 Exchange 內部部署：**當您選取此選項，就會允許已在 Intune 註冊且符合相容原則的裝置存取 Exchange 內部部署。 這個規則會覆寫 [預設規則]，這表示即使您將 [預設規則] 設為隔離或封鎖存取，已註冊且相容的裝置還是可以存取 Exchange 內部部署。 如果您想要讓已註冊且相容的裝置一律可以透過 Exchange 內部部署存取電子郵件，請使用這個設定。  

 Exchange 內部部署之 [設定條件存取原則精靈] 的 [一般] 頁面上有提供此規則。  

 如需詳細的逐步解說，請參閱[管理 System Center Configuration Manager 中的電子郵件存取](../../../protect/deploy-use/manage-email-access.md)。  

## <a name="client-management"></a>用戶端管理  

### <a name="client-online-status"></a>用戶端線上狀態  
 系統會提供用戶端的新狀態來監視電腦是否在線上。 當電腦已連線到受指派的管理點時，就會被視為在線上。 為了表示電腦在線上，用戶端會傳送類似 Ping 的訊息給管理點。 如果管理點在 5 分鐘後未收到訊息，該用戶端就會被視為離線。  

 如需詳細資料，請參閱[如何在 System Center Configuration Manager 中監視用戶端](../../../core/clients/manage/monitor-clients.md)。  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>從軟體中心重新整理 PC 電腦和使用者原則  
 新的 [同步原則] 選項已新增至軟體中心的 [選項] > [電腦維護] 頁面，讓電腦重新整理它的 Configuration Manager 電腦和使用者原則。  

### <a name="software-center-branding-changes"></a>軟體中心商標變更  
 您可以變更「軟體中心」中顯示的色彩、組織名稱及圖示。 套用這些設定時，將會根據下列規則︰  

1.  如果未安裝應用程式類別目錄網站點站台伺服器角色，則軟體中心將會顯示**電腦代理程式**用戶端設定 [顯示在軟體中心的組織名稱] 中指定的組織名稱。  

2.  如果未安裝「應用程式類別目錄網站點」站台伺服器角色，則「軟體中心」將會顯示「應用程式類別目錄網站點」站台伺服器角色內容中指定的組織名稱和色彩。  

3.  如果已設定 Microsoft Intune 訂閱並連線到 Configuration Manager 環境，則軟體中心將會顯示 Intune 訂閱內容中指定的組織名稱、色彩及公司標誌。  

### <a name="health-attestation"></a>健康情況證明  
 系統管理員可以在 Configuration Manager 主控台內檢視 Windows 10 裝置健康情況證明的狀態。  這項功能適用於 Configuration Manager 以及搭配 Microsoft Intune 使用的 Configuration Manager。 系統管理員可透過裝置健康情況證明，確認用戶端電腦已啟用下列可信任的 BIOS、TPM 及開機軟體設定：  

-   早期啟動反惡意程式碼  

-   BitLocker  

-   安全開機  

-   程式碼完整性  

如需詳細資料，請參閱[System Center Configuration Manager 的健康情況證明](../../../core/servers/manage/health-attestation.md)。  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>對 Endpoint Protection 反惡意程式碼設定的改進  
 1602 在適用於 Windows Defender 的 Endpoint Protection 反惡意程式碼原則中新增了下列新設定：  

-   即時保護：在下載時及安裝前封鎖潛在的垃圾應用程式  

-   掃描設定：執行完整掃描時，掃描對應的網路磁碟機  

-   提交自動範例檔案設定：  

     反惡意程式碼引擎可能會要求將範例檔案傳送給 Microsoft，進行進一步分析。 根據預設，在傳送這類範例前一律會出現提示。 系統管理員現已可管理下列設定，來設定此行為：  

    -   進階：啟用自動範例檔提交，可協助 Microsoft 判定某些偵測到的項目是否為惡意  

    -   進階：允許使用者修改自動範例檔提交設定  

    此外，Endpoint Protection 反惡意程式碼原則的 [排除設定] 區段中現有的 [排除檔案及資料夾] 設定，已改良為可以排除裝置。  

如需詳細資料，請參閱[如何在 System Center Configuration Manager 中建立和部署 Endpoint Protection 的反惡意程式碼原則](../../../protect/deploy-use/endpoint-antimalware-policies.md)。  

## <a name="mobile-device-management"></a>行動裝置管理  

### <a name="ios-activation-lock"></a>iOS 啟用鎖定  
 Configuration Manager 可以協助您管理 iOS 啟用鎖定，這是 iOS 7.1 和更新版本裝置之「尋找我的 iPhone」應用程式中的功能。 當裝置上使用「尋找我的 iPhone」應用程式時，啟用鎖定會自動啟用。 啟用之後，就必須輸入使用者的 Apple ID 和密碼，才能夠讓所有人：  

-   關閉「尋找我的 iPhone」  

-   清除裝置  

-   重新啟動裝置  

Configuration Manager 可以要求執行 iOS 7.1 和更新版本之受監督和不受監督裝置的啟用鎖定狀態。 針對受監督的裝置，Configuration Manager 可以擷取「啟用鎖定」略過碼並將它直接發給裝置。  

 如需詳細資料，請參閱[利用 System Center Configuration Manager 中的啟用鎖定略過來協助保護 iOS 裝置](/sccm/mdm/deploy-use/manage-ios-activation-lock)。  

### <a name="monitor-terms-and-conditions-deployments"></a>監視條款和條件部署  
 您可以在 Configuration Manager 主控台中監視條款和條件部署。  

 選取條款和條件部署。 (從部署清單中選取)。 摘要區域將會顯示下列統計資料︰  

-   **相容** - 使用者已接受最新版的條款和條件  

-   **錯誤**  

-   **不相容** - 使用者已接受某個版本的條款和條件，但不是最新版  

-   **不明** - 使用者從未接受條款和條件 (包括沒有已註冊裝置的使用者)  



<!--HONumber=Nov16_HO1-->


