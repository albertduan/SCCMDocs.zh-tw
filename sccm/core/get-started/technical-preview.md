---
title: "Configuration Manager 的 Technical Preview | Microsoft Docs"
description: "了解可讓您試用 System Center Configuration Manager 新功能的 Technical Preview 版本。"
ms.custom: na
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: "157"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 429e20185bd23519f78c37ded39f2638d0c80ced
ms.sourcegitcommit: 8ac9c2c9ba1fdcbb7cc8d5be898586865fcf67c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2017
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager 的 Technical Preview

*適用於︰System Center Configuration Manager (Technical Preview)*

**歡迎使用 System Center Configuration Manager Technical Preview**。 本主題提供預覽版本的相關詳細資料；這些版本不斷演變，並導入我們正在開發的新功能。 當我們提供每個 Technical Preview 版本時，皆會在其中導入 System Center Configuration Manager 最新分支中尚未包含的新功能。 這些功能最終可能包含在最新分支版本的更新中，但是我們希望能讓您先試用並提供意見反應之後，再完成功能並將它們加入。  

 由於這是 Technical Preview，因此詳細資料和功能可能會有所變更。  

 本主題包含適用於所有 Technical Preview 版本的資訊，也會列出每項新功能與最先出現該功能的 Technical Preview 版本，例如 1701 版即表示 2017 年 1 月的版本。 這些功能的詳細資料會在每個預覽版本專屬的個別主題中詳述。  

 如需 Configuration Manager 最新分支新功能的相關資訊，請參閱 [System Center Configuration Manager 的新功能](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)。



##  <a name="bkmk_reqs"></a> Technical Preview 的需求與限制  

> [!IMPORTANT]     
>  Technical Preview 僅授權在實驗室環境中使用。  Microsoft 可能無法提供支援服務；預覽軟體亦可能未提供某些功能。 此外，相較於市面上提供的軟體，預覽軟體的安全性、隱私權、可存取性、可用性和可靠性標準可能較低或有所差異。  

 如需大部分產品必要條件，請使用[支援的 System Center Configuration Manager 設定](../../core/plan-design/configs/supported-configurations.md)中的資訊。 以下是 Technical Preview 版本適用的例外狀況：  

-   每個安裝可持續有效 90 天，之後即變成無效。  

-   英文是唯一支援的語言。


-   僅支援下列安裝旗標 (參數)：  

    -   **/silent**  
    -   **/testdbupgrade**    


-   根據預設，當您使用 Technical Preview 時，服務連接點會在安裝時設定為線上模式，且不支援變更為離線模式。

-   每個 Technical Preview 的特定版本都會附有其他限制或需求，且提供詳細說明 (如果有的話)  

-   不支援移轉至這個預覽版或從中進行移轉。  

-   不支援升級為這個預覽版。  

-   不支援從這個預覽版升級為生產版本 (最新分支)。 但為預覽版本提供可用更新時，可從 Configuration Manager 主控台的 [更新與服務] 節點尋找更新，並加以安裝。 如需取得在主控台中升級程序的影片，請參閱 youtube.com 上的 [安裝 Configuration Mananger 更新套件](https://www.youtube.com/embed/KBd_EGFbUT8) 。  
-   僅支援獨立主要站台。 不支援管理中心網站、多個主要站台或次要站台。  

此 Configuration Manager 分支支援下列產品和技術。 不過，本內容對這些產品和技術的包含，並不表示對任何產品或版本超出產品個別支援週期的支援延伸。 已超出其支援週期的產品不支援搭配 Configuration Manager 使用。 如需 Microsoft 支援週期的詳細資訊，請造訪 [Microsoft 支援週期](http://go.microsoft.com/fwlink/p/?LinkId=208270) 網站。  

-   僅支援下列 SQL Server 版本：  

    -   SQL Server 2016 (不含 Service Pack 和更新版本)
    -   SQL Server 2014 (含 Service Pack 1 和更新版本)
    -   SQL Server 2012 (含 Service Pack 3 或更新版本)


-   站台最多支援 10 個用戶端，每個用戶端都必須執行下列其中一項：  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> 安裝並更新 Technical Preview  
 System Center Configuration Manager Technical Preview 與 System Center Configuration Manager 目前版本不同。  

 若要使用 Technical Preview，您必須先安裝 Technical Preview 組建的 **基準版本** 。 安裝基準版本之後，您便可以使用 **主控台內更新** ，將安裝升級成最新的預覽版本。     一般而言，每個月都會提供新版本的 Technical Preview。

每個預覽版本最多支援三個連續版本。 亦即發行 1708 版時，將不再支援 1704 版，但仍然支援 1705、1706 和 1707 版。 當不再支援基準時 (例如 1703 版)，仍然會支援安裝新的 Technical Preview 站台。等到有可用的新基準版本時，只要將該安裝更新至支援的版本即可。 在更新時，如果您在主控台中沒有看到最新版本可用，請更新至所提供的最新版本，然後重複該程序，直到可以安裝最新版的 Technical Preview 為止。

> [!TIP]  
>  當您將更新安裝為 Technical Preview 時，可以將 Preview 安裝更新為新的 Technical Preview 版本。    Technical Preview 安裝永遠無法升級為最新分支安裝，也不會從最新分支版本接收更新。  

**Technical Preview 的作用中基準版本︰**  
在發行後的 1 年內，您都可以安裝基準版本。 不過，當您安裝新的 Technical Preview 站台時，建議您使用最新可用的基準版本。
-  **Technical Preview 1703** - Configuration Manager Technical Preview 1703 同時以兩種形式提供：Configuration Manager Technical Preview 的主控台內更新，以及 [TechNet Evaluation Center 網站提供的](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)新基準版本。

<!-- out of support. Use baseline 1703
-  **Technical Preview 1610** - The Configuration Manager Technical Preview 1610 was available as both an in-console update for the Configuration Manager Technical Preview, and as a baseline version. If you have media for installing 1610, we recommend you download version 1703 and install that version instead.
-->



##  <a name="BKMK_TPFeedback"></a> 提供意見反應  
 歡迎您提供有關 Technical Preview 的意見反應。 若要提交有關每個預覽版中之功能的意見反應，請遵循 Microsoft Connect 網站之 [Configuration Manager 意見反應計劃](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) 頁面上的回函表單連結。  

 此外，如果您有想要看到之新功能的構想，也請告訴我們。 若要提交新構想，以及投票給其他人所提交的構想，請 [瀏覽我們的 UserVoice 網頁](http://configurationmanager.uservoice.com)。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> 最新 Technical Preview 中提供的功能  
 下方列出每個 Configuration Manager Technical Preview 版本所提供的功能。  自 Technical Preview 開始提供的功能仍會保留在較新版本中。 同樣地，已新增至 System Center Configuration Manager 版本 (最新分支) 的功能仍會在後續的 Technical Preview 中提供。  您可以按一下每個預覽版本的內容，以進一步了解特定功能。  

 |功能 |Technical Preview 版本 |最新分支版本|  
 |----------------|---------------------|--------------------|
 |改善的 Configuration Manager 主控台 VPN 設定檔體驗 <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |![未新增](media/Red_X.gif)    |
 |Windows 10 裝置的共同管理|[Tech Preview 1709](capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices)|![未新增](media/Red_X.gif)    |


## <a name="capabilities-delivered-in-previous-technical-previews"></a>舊版 Technical Preview 中提供的功能
 當所支援的最低版本「最新分支」中有提供某個 Technical Preview 版本的所有功能時，該預覽版本的詳細資料便會從下表中移除。  

 |功能 |Technical Preview 版本 |最新分支版本|  
 |----------------|---------------------|--------------------|
 |從 Configuration Manager 部署 PowerShell 指令碼時，改善指令碼參數的指定<!-- 1236459 -->|[Tech Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|![未新增](media/Red_X.gif)|
 |Management Insights  <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|![未新增](media/Red_X.gif)|
 |從 Configuration Manager 主控台重新啟動電腦<!-- 1356283 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console)|![未新增](media/Red_X.gif)|
 |軟體中心自訂 <!-- 1351224 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#software-center-customization)|![未新增](media/Red_X.gif)|
|Windows 10 和 Office 365 快速安裝檔案的用戶端對等快取支援|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365)|![未新增](media/Red_X.gif)|
 |Surface 裝置儀表板|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|![未新增](media/Red_X.gif)|
 |設定及部署 Windows Defender 應用程式防護原則|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#configure-and-deploy-windows-defender-application-guard-policies)|![未新增](media/Red_X.gif)|
 |在從 Configuration Manager 部署 PowerShell 指令碼時新增參數|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|![未新增](media/Red_X.gif)|
 |新的行動應用程式管理原則設定|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-mobile-application-management-policy-settings)|![未新增](media/Red_X.gif)|
 |改進的軟體更新點界限群組|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#improved-boundary-groups-for-software-update-points)|[版本 1706](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)|
 |站台伺服器角色高可用性|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |![未新增](media/Red_X.gif)|
 |在 Device Guard 原則中包含對特定檔案和資料夾的信任|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#include-trust-for-specific-files-and-folders-in-a-device-guard-policy)|[版本 1706](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|
 |隱藏工作順序進度|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#hide-task-sequence-progress)|![未新增](media/Red_X.gif)|
 |針對安裝內容和解除安裝內容指定不同的內容位置|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#specify-a-different-content-location-for-install-content-and-uninstall-content)|[版本 1706](/sccm/core/get-started/capabilities-in-technical-preview-1706#hide-task-sequence-progress)|
 |協助工具改進 |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#accessibility-improvements)|[版本 1706](/sccm/core/understand/accessibility-features)|
 |Azure 服務精靈對升級整備的支援 |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#changes-to-the-azure-services-wizard-to-support-upgrade-readiness)|[版本 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |雲端服務的新用戶端設定|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-client-settings-for-cloud-services)|[版本 1706](/sccm/core/clients/deploy/deploy-clients-cmg-azure)|
 |從 Configuration Manager 主控台建立及執行 PowerShell 指令碼|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)|[版本 1706](/sccm/apps/deploy-use/create-deploy-scripts)|
 |適用於 IPv6 的 PXE 網路開機支援 |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|![未新增](media/Red_X.gif)|
 |管理 Microsoft Surface 驅動程式更新 |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#manage-microsoft-surface-driver-updates)|[版本 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#manage-microsoft-surface-driver-updates)|
 |設定 Windows Update for Business 延遲原則 |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#configure-windows-update-for-business-deferral-policies)|[版本 1706](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)|
 |iOS 註冊限制|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[版本 1706](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions)|
 |Android 註冊限制|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[版本 1706](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)|
 |Android for Work 的應用程式複製貼上管理原則|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-for-work-application-management-policy-for-copy-paste)|[版本 1706](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client#android-for-work-configuration-item-settings-reference)|
 |新的 Windows 組態項目設定|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-windows-configuration-item-settings)|[版本 1706](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |新的裝置合規性政策規則|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-device-compliance-policy-rules)|[版本 1706](/sccm/mdm/deploy-use/create-compliance-policy)|
 |條件式存取之合規性政策的裝置健康情況證明評估|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|![未新增](media/Red_X.gif)|
 |針對 Entrust 憑證授權單位的支援|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#support-for-entrust-certification-authorities)|[版本 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |針對 macOS VPN 設定檔的 Cisco (IPsec) 支援|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#cisco-ipsec-support-for-macos-vpn-profiles)|[版本 1706](/sccm/protect/deploy-use/vpn-profiles)|
 |Azure AD 和雲端管理的新功能|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management)|[版本 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#azure-ad-integration-with-configuration-manager)|
 |設定及部署 Windows Defender 應用程式防護原則|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#configure-and-deploy-windows-defender-application-guard-policies)|![未新增](media/Red_X.gif)|
 |更新重設工具  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#update-reset-tool)|[版本 1706](/sccm/core/servers/manage/update-reset-tool)|
 |高 DPI 主控台支援  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#high-dpi-console-support)|[版本 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#high-dpi-console-support)|
 |對等快取改善  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#peer-cache-improvements) |[版本 1706](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache)|
 |對 SQL Server Always On 可用性群組的改進 |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#improvements-for-sql-server-always-on-availability-groups) |[版本 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#improvements-for-sql-server-always-on-availability-groups)|
 |適用於 Office 365 更新的改良式使用者通知|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#improved-user-notifications-for-office-365-updates) |[版本 1706](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates)|
 |使用 Azure 服務精靈來設定與 OMS 的連線|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) |[版本 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |使用應用程式組態原則設定 Android 應用程式  |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![未新增](media/Red_X.gif)|
 |硬體清查會收集安全開機資訊 |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|[版本 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#hardware-inventory-collects-secure-boot-information)|
 |將子工作順序新增至工作順序|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![未新增](media/Red_X.gif)|
 |以目前的 Windows PE 版本重新載入開機映像 |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|[版本 1706](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image)|
 |作業系統部署增強功能<!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![未新增](media/Red_X.gif)|
 |將大量採購的 iOS 應用程式部署至裝置集合|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[版本 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |應用程式的軟體中心直接連結|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|[版本 1706](/sccm/apps/deploy-use/share-applications)
 |Configuration Manager Windows 用戶端電腦的 PFX 憑證|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|[版本 1706](/sccm/protect/deploy-use/create-certificate-profiles)|
 |設定 Azure 服務精靈|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|[版本 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |依作業系統升級工作順序從 BIOS 轉換至 UEFI| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[版本 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |可摺疊的工作順序群組| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |[版本 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#collapsible-task-sequence-groups)|
 |設定 Windows Analytics 進行升級整備用的用戶端設定 | [Tech Preview 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |[版本 1706](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics)|
 |iOS 裝置的新合規性設定|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[版本 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |使用 S/MIME 支援來建立 PFX 憑證|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[版本 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |在安裝應用程式之前檢查執行中可執行檔|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[版本 1702](/sccm/apps/deploy-use/deploy-applications)|
 |從 Configuration Manager 主控台傳送意見反應 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |更新與服務的變更  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |對等快取改善  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[版本 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |使用 Azure Active Directory<!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![未新增](media/Red_X.gif)|
 |條件式存取裝置合規性政策改進 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[版本 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |反惡意程式碼用戶端版本警示 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[版本 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Windows Update for Business 更新的合規性評估 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![未新增](media/Red_X.gif)|
 |具有強烈影響之工作順序的軟體中心設定和通知訊息的改進|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[版本 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Android for Work 支援| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[版本 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |軟體更新點的界限群組增強功能 | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[版本 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |硬體清查會收集 UEFI 資訊 | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[版本 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |作業系統部署增強功能| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |在雲端式發佈點上裝載軟體更新| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|[版本 1702](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#plan-to-use-a-cloud-based-distribution-point) |
 |透過管理點來驗證裝置健全狀況證明資料| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [版本 1702](/sccm/core/servers/manage/health-attestation) |
 |針對 Microsoft Azure Government 雲端的 OMS 連接器 |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[版本 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |建立精靈無法再將目標設為 Android 與 iOS 版本 |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |
 |OData 端點資料存取 |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![未新增](media/Red_X.gif)|
 |資料倉儲服務點 |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[版本 1702](/sccm/core/servers/manage/data-warehouse)|
 |內容庫清理工具 |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[版本 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |主控台內搜尋的新增功能 |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |防止在指定的程式正在執行時安裝應用程式|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[版本 1702](/sccm/apps/deploy-use/deploy-applications)|
 |新增針對使用者的 Windows Hello 企業版通知|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#new-windows-hello-for-business-notification-for-end-users)|
 |Configuration Manager 中的商務用 Windows 市集支援|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|[版本 1702](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |工作順序失敗時返回上一頁|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Windows 10 更新的快速安裝檔案支援|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[版本 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Azure Active Directory 上架|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|[版本 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |設定裝置註冊之 Multi-Factor Authentication 的變更|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![未新增](media/Red_X.gif)|
 |預先快取部署和工作順序內容 |[Tech Preview 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[版本 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Windows Defender 組態設定|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[1610 版](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |從系統管理員主控台要求原則同步|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[1610 版](/sccm/mdm/deploy-use/sync-intune-device)|
 |公司擁有的所有裝置節點的其他安全性角色支援|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[1610 版](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Windows 10 VPN 設定檔的條件式存取|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[1610 版](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |自動部署規則中依內容大小進行篩選|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[1610 版](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |所需軟體對話方塊的功能改善|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[1610 版](/sccm/apps/deploy-use/deploy-applications)|
 |拒絕先前核准的應用程式要求|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[1610 版](/sccm/apps/deploy-use/deploy-applications)|
 |排除自動升級用戶端|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[1610 版](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Endpoint Protection 的改進|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[版本 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |增加已註冊裝置的數目|[Tech Preview 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[版本 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |其他 Apple DEP 設定|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[1610 版](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |商務用 Windows 市集與 Configuration Manager 整合的改善|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[1610 版](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |設定項目的新相容性設定|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[1610 版](/sccm/compliance/deploy-use/create-configuration-items)|
 |與 Upgrade Analytics 的整合|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[1610 版](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Windows 10 VPN 混合式設定檔的原生連線類型|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![未新增](media/Red_X.gif)|
 |界限群組的增強功能|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[1610 版](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Office 365 用戶端管理儀表板|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[1610 版](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |將 Office 365 應用程式部署至用戶端|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[版本 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |BIOS 轉換成 UEFI 的增強功能|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[1610 版](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Intune 相容性圖表|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[版本 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|


 <!--  TP 1608 and earlier have aged out of support. Features from these previews are either in the minimum supported Current Branch version, or are not scheduled for inclusion.
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Improvements to Software Center|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Improvements to Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|N/A|
 |Remote control keyboard translation|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|[Version 1702](/sccm/core/clients/manage/remote-control/configuring-remote-control#enable-keyboard-translation)|
 |Improvements to the Windows 10 Edition Upgrade Policy|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Version 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Customizable Branding for Software Center Dialogs|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#customizable-branding-for-software-center-dialogs)|  
 |Multiple device management points for On-premises Mobile Device Management|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Automatically categorize devices into collections|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Enforcement grace period for required application and software update deployments|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Using Configuration Manager as a Managed Installer with Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|[Version 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|
 |Cloud management gateway (formerly Cloud Proxy Service)|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Manage the Office 365 client agent in Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |The OSDPreserveDriveLetter task sequence variable has been deprecated|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Version 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Changes for the Updates and Servicing Node|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |Per-app VPN for Windows 10 devices|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Version 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Improvements to the Install software updates task sequence|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Grace period for required application deployments |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|N/A|  
 |New experience for remote device actions |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Windows Store for Business apps |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |General improvements for volume-purchased apps|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Enterprise Data Protection (EDP)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |End users can install apps from the Company Portal |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|N/A|  
 |New tabs for Updates and Operating Systems in Software Center|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Version 1606 ](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Service a server group |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Version 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Support for Windows Defender Advanced Threat Protection service |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Version 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |New restart options for Windows 10 clients after software update installation|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |On-premises Device Health Attestation |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |Pre-declare corporate-owned devices with IMEI or iOS serial number|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Version 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |Manage volume-purchased apps from the Windows Store for Business| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Improvements to Microsoft Passport for Work management|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Option for clients to switch to a new software update point|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Client settings to manage Client Cache Settings and client Peer Cache |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Client Settings: [Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Peer Cache: [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Support for Passport for Work as a KSP |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Version 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |On-premises Device Health Attestation|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |SmartLock setting for Android devices|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Version 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Improvements to Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Improvements to remote control|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
-->



## <a name="see-also"></a>另請參閱  
[System Center Configuration Manager 的新功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [System Center Configuration Manager 簡介](../../core/understand/introduction.md)
