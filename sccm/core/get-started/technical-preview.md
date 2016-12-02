---
title: "System Center Configuration Manager 的 Technical Preview"
description: "了解可讓您試用 System Center Configuration Manager 新功能的 Technical Preview 版本。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 39a9cde3bd955c84f301d25258b413fecaa4393b
ms.openlocfilehash: 2aa78c20c919d04401f663063860df06c5262048


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager 的 Technical Preview

*適用於︰System Center Configuration Manager (Technical Preview)*

**歡迎使用 System Center Configuration Manager Technical Preview**。 本主題提供預覽版本的相關詳細資料；這些版本不斷演變，並導入我們正在開發的新功能。 當我們提供每個 Technical Preview 版本時，皆會在其中導入 System Center Configuration Manager 最新分支中尚未包含的新功能。 這些功能最終可能包含在最新分支版本的更新中，但是我們希望能讓您先試用並提供意見反應之後，再完成功能並將它們加入。  

 由於這是 Technical Preview，因此詳細資料和功能可能會有所變更。  

 本主題包含適用於所有 Technical Preview 版本的資訊，也會列出每項新功能與最先出現該功能的 Technical Preview 版本，例如 1512 版即表示 2015 年 12 月的版本。 這些功能的詳細資料會在每個預覽版本專屬的個別主題中詳述。  

 如需 Configuration Manager 最新分支新功能的相關資訊，請參閱 [System Center Configuration Manager 的新功能](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)。



##  <a name="a-namebkmkreqsa-requirements-and-limitations-for-the-technical-preview"></a><a name="bkmk_reqs"></a> Technical Preview 的需求與限制  

> [!IMPORTANT]  
>  Technical Preview 僅授權在實驗室環境中使用。  Microsoft 可能無法提供支援服務；預覽軟體亦可能未提供某些功能。 此外，相較於市面上提供的軟體，預覽軟體的安全性、隱私權、可存取性、可用性和可靠性標準可能較低或有所差異。  

 如需大部分產品必要條件，請使用[支援的 System Center Configuration Manager 設定](../../core/plan-design/configs/supported-configurations.md)中的資訊。 以下是 Technical Preview 版本適用的例外狀況：  

-   每個安裝可持續有效 90 天，之後即變成無效。  

-   英文是唯一支援的語言。  

-   僅支援獨立主要站台。 不支援管理中心網站、多個主要站台或次要站台。  

-   僅支援下列 SQL Server 版本：  

    -   含累計更新 2 或更新版本的 SQL Server 2012  

    -   SQL Server 2014  

-   站台最多支援 10 個用戶端，每個用戶端都必須執行下列其中一項：  

    -   Windows 7  

    -   Windows 8  

    -   Windows 8.1  

    -   Windows 10  

-   僅支援下列安裝旗標 (參數)：  

    -   **/silent**  

    -   **/testdbupgrade**  

-   每個 Technical Preview 的特定版本都會附有其他限制或需求，且提供詳細說明 (如果有的話)  

-   不支援移轉至這個預覽版或從中進行移轉。  

-   不支援升級為這個預覽版。  

-   不支援從這個預覽版升級為生產版本 (最新分支)。 但為預覽版本提供可用更新時，可從 Configuration Manager 主控台的 [更新與服務] 節點尋找更新，並加以安裝。 如需取得在主控台中升級程序的影片，請參閱 youtube.com 上的 [安裝 Configuration Mananger 更新套件](https://www.youtube.com/embed/KBd_EGFbUT8) 。  

##  <a name="a-namebkmkinstalla-install-and-update-the-technical-preview"></a><a name="bkmk_install"></a> 安裝並更新 Technical Preview  
 System Center Configuration Manager Technical Preview 與 System Center Configuration Manager 目前版本不同。  

 若要使用 Technical Preview，您必須先安裝 Technical Preview 組建的 **基準版本** 。 安裝基準版本之後，您便可以使用 **主控台內更新** ，將安裝升級成最新的預覽版本。     一般而言，每個月都會提供新版本的 Technical Preview。  

> [!TIP]  
>  當您將更新安裝為 Technical Preview 時，可以將 Preview 安裝更新為新的 Technical Preview 版本。    Technical Preview 安裝永遠無法升級為最新分支安裝，也不會從最新分支版本接收更新。  

 **Technical Preview 的作用中基準版本︰**  
 在發行後的 1 年內，您都可以安裝基準版本。

-   **Technical Preview 1610** - Configuration Manager Technical Preview 1610 同時以兩種形式提供：Configuration Manager Technical Preview 的主控台內更新，以及 [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) 網站提供的新基準版本。

-   **System Center Technical Preview 5** 隨附的 **Technical Preview 1603** - Configuration Manager Technical Preview 1603 同時以兩種形式提供：Configuration Manager Technical Preview 的主控台內更新，以及 System Center Technical Preview 5 隨附的新基準版本。    只有 System Center Technical Preview 5 隨附的版本可以用於基準安裝。  

     關於[來自 System Center Technical Preview 5 的 Configuration Manager Technical Preview](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) 基準版本：  

    -   安裝程式和 Configuration Manager 主控台會將版本列為 System Center Configuration Manager Technical Preview 1603。  

    -   此基準版本的功能與 Configuration Manager Technical Preview 1603 相同，都包括主控台內更新支援。  


##  <a name="a-namebkmktpfeedbacka-providing-feedback"></a><a name="BKMK_TPFeedback"></a> 提供意見反應  
 歡迎您提供有關 Technical Preview 的意見反應。 若要提交有關每個預覽版中之功能的意見反應，請遵循 Microsoft Connect 網站之 [Configuration Manager 意見反應計劃](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) 頁面上的回函表單連結。  

 此外，如果您有想要看到之新功能的構想，也請告訴我們。 若要提交新構想，以及投票給其他人所提交的構想，請 [瀏覽我們的 UserVoice 網頁](http://configurationmanager.uservoice.com)。  

##  <a name="a-namebdmktpknownissuesa-general-changes-introduced-in-technical-previews"></a><a name="bdmk_tpknownissues"></a> Technial Preview 中導入的一般變更  

-   **Technical Preview 1603：**  

    -   從 Technical Preview 1603 開始，您可以將軟體更新部署設定成在用戶端安裝軟體更新並重新啟動之後，讓用戶端立即執行軟體更新相容性掃描。 這可讓用戶端檢查是否有在用戶端重新啟動後變成適用的其他軟體更新，然後在同一個維護期間內安裝這些更新 (而變成相容)。  

         若要為某個部署進行此設定，請在 [部署軟體更新精靈] 的 **[使用者體驗]** 頁面上，選取 **[若此部署中的任何更新需要重新啟動系統，請在重新啟動後執行更新部署評估週期]**。  

    -   從 Technical Preview 1603 開始，SMSTSRebootDelay 工作順序變數的行為已變更。 SMSTSRebootDelay 指定在電腦重新啟動之前要等待的秒數。 如果這個變數未設定為 0，工作順序管理員就會在重新啟動之前顯示通知對話方塊。  
        當您為此變數設定值時，該值會持續保留，直到您設定新的值為止。 所有後續電腦重新啟動的延遲都會具有相同的值。 在 Configuration Manager 1602 版或更舊版本中，重新啟動電腦之後，此變數會重設為預設值 (30 秒)。   如需詳細資訊，請參閱 [Task sequence built-in variables in System Center Configuration Manager](../../osd/understand/task-sequence-built-in-variables.md)。

-   **Technical Preview 1602：** 從 Technical Preview 1602 開始，您可以將執行 Windows 2008 Server R2 的站台系統伺服器作業系統就地升級到 Windows 2012 Server R2。  當您使用 Windows Server 2012 R2 的升級程序時，不需要在升級後執行 Configuration Manager 站台伺服器還原。  如需升級程序，請參閱 [Windows Server 2012 R2 的升級選項](https://technet.microsoft.com/library/dn303416.aspx)。  

    > [!WARNING]  
    >  在升級到 Windows Server 2012 R2 之前，您必須從伺服器 **解除安裝 WSUS 3.2** 。  
    >   
    >  如需此重要步驟的資訊，請參閱 Windows Server 文件中 [Windows Server Update Services 概觀](https://technet.microsoft.com/library/hh852345.aspx) 的＜新功能和變更的功能＞一節。  

-   **Technical Preview 1601：** 根據預設，服務連接點在安裝時設定為線上模式，且不支援變更為離線模式。  





##  <a name="a-namebkmktpcapsa-capabilities-delivered-in-technical-previews"></a><a name="bkmk_tpCaps"></a> 在技術預覽中提供功能  
 下方列出每個 Configuration Manager Technical Preview 版本所提供的功能。  自 Technical Preview 開始提供的功能仍會保留在較新版本中。 同樣地，已新增至 System Center Configuration Manager 版本 (最新分支) 的功能仍會在後續的 Technical Preview 中提供。  您可以按一下每個預覽版本的內容，以進一步了解特定功能。  

 |功能|Technical Preview 版本|最新分支版本|  
 |----------------|---------------------|--------------------|
 |自動部署規則中依內容大小進行篩選|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|![未新增](media/Red_X.gif)|
 |所需軟體對話方塊的功能改善|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|![未新增](media/Red_X.gif)|
 |拒絕先前核准的應用程式要求|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|![未新增](media/Red_X.gif)|
 |排除自動升級用戶端|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|![未新增](media/Red_X.gif)|
 |Endpoint Protection 的改善|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|![未新增](media/Red_X.gif)|
 |增加已註冊裝置數目|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#increased-number-of-enrolled-devices)|![未新增](media/Red_X.gif)|
 |其他 Apple DEP 設定|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|![未新增](media/Red_X.gif)|
 |商務用 Windows 市集與 Configuration Manager 整合的改善|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|![未新增](media/Red_X.gif)|
 |設定項目的新相容性設定|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|![未新增](media/Red_X.gif)|
 |與 Upgrade Analytics 的整合|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|![未新增](media/Red_X.gif)|
 |Windows 10 VPN 混合式設定檔的原生連線類型|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![未新增](media/Red_X.gif)|
 |界限群組的增強功能|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|![未新增](media/Red_X.gif)|
 |Office 365 用戶端管理儀表板|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|![未新增](media/Red_X.gif)|
 |將 Office 365 應用程式部署至用戶端|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#ceploy-office-365-apps-to-clients)|![未新增](media/Red_X.gif)|
 |BIOS 轉換成 UEFI 的增強功能|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-bios-to-uefi-conversion)|![未新增](media/Red_X.gif)|
 |Intune 相容性圖表|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|![未新增](media/Red_X.gif)|
 |準備 ConfigMgr 用戶端以進行擷取之工作順序步驟的改進|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|![未新增](media/Red_X.gif)|
 |軟體中心的增強功能|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|![未新增](media/Red_X.gif)|
 |Asset Intelligence 的增強功能|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![未新增](media/Red_X.gif)|
 |遠端控制鍵盤轉譯|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![未新增](media/Red_X.gif)|
 |改進 Windows 10 版本升級原則|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|![未新增](media/Red_X.gif)|
 |可自訂軟體中心對話方塊的商標|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-denter-dialogs)|![未新增](media/Red_X.gif)|  
 |針對內部部署行動裝置管理提供多個裝置管理點|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |自動將裝置分類為集合|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[1606 版](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |針對必要應用程式和軟體更新部署的強制執行寬限期|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|![未新增](media/Red_X.gif)|
 |將 Configuration Manager 作為含 Device Guard 的受管理安裝程式|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![未新增](media/Red_X.gif)|
 |雲端 Proxy 服務|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | ![未新增](media/Red_X.gif)|  
 |在 Configuration Manager 中管理 Office 365 用戶端代理程式|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |OSDPreserveDriveLetter 工作順序變數已被取代|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[1606 版](/sccm/osd/understand/task-sequence-built-in-variables) |
 |更新和服務節點有所變更|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |適用於 Windows 10 裝置的個別應用程式 VPN|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[1606 版](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |改進安裝軟體更新工作順序|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |準備 ConfigMgr 用戶端以進行擷取之工作順序步驟的改進 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|![未新增](media/Red_X.gif) |
 |針對必要應用程式部署的寬限期 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![未新增](media/Red_X.gif)|  
 |遠端裝置動作的全新體驗 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |商務用 Windows 市集應用程式 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[1606 版](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |針對大量購買之應用程式的一般改進|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |企業資料保護 (EDP)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |使用者可從公司入口網站安裝應用程式 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![未新增](media/Red_X.gif)|  
 |提供全新的軟體中心更新和作業系統索引標籤|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |提供伺服器群組 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[1606 版](/sccm/sum/deploy-use/service-a-server-group)|   
 |支援 Windows Defender 進階威脅防護服務 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[1606 版](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |提供在安裝軟體更新後重新啟動 Windows 10 用戶端的新選項|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[1606 版](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |內部部署裝置健康情況證明 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[1606 版](/sccm/core/servers/manage/health-attestation)|  
 |使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[1606 版](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |從商務用 Windows 市集管理大量購買的應用程式| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[1606 版](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |對 Microsoft Passport for Work 管理的改進|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |可供用戶端切換到新軟體更新點的選項|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[1606 版](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |可管理用戶端快取設定和用戶端對等快取的用戶端設定 |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)|  
 |對以 Passport for Work 做為 KSP 的支援 |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[1606 版](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |內部部署裝置健康情況證明|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[1606 版](/sccm/core/servers/manage/health-attestation)|  
 |適用於 Android 裝置的 SmartLock 設定|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[1606 版](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |軟體中心的增強功能|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |對遠端控制的改進|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |自訂支援 PXE 之發佈點的相關 RamDisk TFTP 區塊大小和視窗大小|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[1606 版](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |行動裝置管理的增強功能|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_MDM)|[版本 1602](/sccm/mdm/deploy-use/manage-ios-activation-lock) |  
 |1602 版本中對軟體中心的改進|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_SC1601)| [版本 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#client-management)|  
 |Windows 10 服務的增強功能|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_Win10Servicing)|[版本 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#operating-system-deployment) |  
 |Microsoft Intune 整合的增強功能|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_hybrid1)|[版本 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#conditional-access)|  
 |用戶端線上狀態|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_clientStatus)|[版本 1602](/sccm/core/clients/manage/monitor-clients)|
 |應用程式管理的增強功能|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_appmgmt1601)|[版本 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#application-management)|  
 |相容性設定的增強功能|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_compliance1601)|[版本 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#compliance-settings)|  
 |裝置健全狀況證明|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_devicehealth)|[1602 版](/sccm/core/servers/manage/health-attestation))|
 |主控台中監視的條款和條件|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_viewterms)|[版本 1602](/sccm/mdm/deploy-use/terms-and-conditions)|  
 |Endpoint Protection 原則設定的改善|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_EPpolicy)|[版本 1602](/sccm/protect/deploy-use/endpoint-antimalware-policies)|  
 |與 Windows 10 中的 Windows Update for Business 整合|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_WUfB)|[版本 1602](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|  
 |透過 System Center Configuration Manager 管理 Office 365 ProPlus 用戶端更新|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_Office365ProPlus)|[版本 1602](/sccm/sum/deploy-use/manage-office-365-proplus-updates)|  
 |支援 SQL Server AlwaysOn 高可用性資料庫|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_AlwasyOn)|[版本 1602](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)|  
 |提供伺服器叢集服務|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_ClusterServerUpdates)|[1606 版](/sccm/sum/deploy-use/service-a-server-group)|  
## <a name="see-also"></a>另請參閱  
[System Center Configuration Manager 的新功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [System Center Configuration Manager 簡介](../../core/understand/introduction.md)



<!--HONumber=Nov16_HO1-->


