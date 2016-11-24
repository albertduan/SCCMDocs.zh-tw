---
title: "記錄檔 | System Center Configuration Manager"
description: "使用記錄檔對 System Center Configuration Manager 階層中的問題進行疑難排解。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cb27f2f2a6e0b0e3d6fca2d616d8ab806b74f9df


---
# <a name="log-files-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的記錄檔

適用於：System Center Configuration Manager (最新分支)

在 System Center Configuration Manager 中，用戶端和站台伺服器元件會在個別記錄檔中記錄程序資訊。 根據預設，Configuration Manager 中會啟用用戶端和伺服器元件記錄。 利用這些記錄檔中的資訊可幫助您解決 Configuration Manager 階層中可能發生的問題。  

 下面各節提供有關不同記錄檔的詳細資料。 利用此資訊檢視和監視 Configuration Manager 用戶端和伺服器記錄檔取得操作詳細資料，並識別錯誤資訊以幫助您進行任何問題的疑難排解。  

-   [關於 Configuration Manager 記錄檔](#BKMK_AboutLogs)  

    -   [使用 Configuration Manager Service Manager 設定記錄選項](#BKMK_LogOptions)  

    -   [尋找 Configuration Manager 記錄檔](#BKMK_LogLocation)  

-   [Configuration Manager 用戶端記錄檔](#BKMK_ClientLogs)  

    -   [用戶端操作](#BKMK_ClientOpLogs)  

    -   [用戶端安裝記錄檔](#BKMK_ClientInstallLog)  

    -   [Linux 和 UNIX 的用戶端](#BKMK_LogFilesforLnU)  

    -   [Mac 電腦的用戶端](#BKMK_LogfilesforMac)  

-   [Configuration Manager 網站伺服器記錄檔](#BKMK_ServerLogs)  

    -   [網站伺服器與網站系統伺服器記錄](#BKMK_SiteSiteServerLog)  

    -   [網站伺服器安裝記錄檔](#BKMK_SiteInstallLog)  

    -   [後援狀態點記錄檔](#BKMK_FSPLog)  

    -   [管理點記錄檔](#BKMK_MPLog)  

    -   [軟體更新點記錄檔](#BKMK_SUPLog)  

-   [Configuration Manager 功能的記錄檔](#BKMK_FunctionLogs)  

    -   [應用程式管理](#BKMK_AppManageLog)  

    -   [Asset Intelligence](#BKMK_AILog)  

    -   [備份和復原](#BKMK_BnRLog)  

    -   [用戶端通知](#BKMK_BGB)  

    -   [憑證註冊](#BKMK_CertificateEnrollment)  

    -   [相容性設定和公司資源存取](#BKMK_CompSettingsLog)  

    -   [Configuration Manager 主控台](#BKMK_ConsoleLog)  

    -   [內容管理](#BKMK_ContentLog)  

    -   [探索](#BKMK_DiscoveryLog)  

    -   [Endpoint Protection](#BKMK_EPLog)  

    -   [擴充功能](#BKMK_Extensions)  

    -   [清查](#BKMK_InventoryLog)  

    -   [計量](#BKMK_MeteringLog)  

    -   [移轉](#BKMK_MigrationLog)  

    -   [行動裝置](#BKMK_MDMLog)  

    -   [作業系統部署](#BKMK_OSDLog)  

    -   [電源管理](#BKMK_PowerMgmtLog)  

    -   [遠端控制](#BKMK_RCLog)  

    -   [報告](#BKMK_ReportLog)  

    -   [以角色為基礎的系統管理](#BKMK_RBALog)  

    -   [服務連接點](#BKMK_WITLog)  

    -   [軟體更新](#BKMK_SU_NAPLog)  

    -   [網路喚醒](#BKMK_WOLLog)  

    -   [Windows Update 代理程式](#BKMK_WULog)  

    -   [WSUS 伺服器](#BKMK_WSUSLog)  

##  <a name="a-namebkmkaboutlogsa-about-configuration-manager-log-files"></a><a name="BKMK_AboutLogs"></a> 關於 Configuration Manager 記錄檔  
 根據預設，Configuration Manager 中大部分程序會將操作資訊寫入該程序專用的記錄檔中。 這些記錄檔是由 **.LOG** 或 **.LO_** 擴充功能所識別。 Configuration Manager 會寫入 .LOG 檔，直到記錄檔到達大小上限。 記錄檔已滿時，.LOG 檔案就會複製到同名的檔案，但副檔名為 .LO_，而程序或元件會繼續寫入 .LOG 檔案中。 當 .LOG 檔案再次達到其大小上限時，就會覆寫 .LO_ 檔案，且此程序會重複。 某些元件會藉由附加日期和時間戳記至記錄檔名稱並且保留 .LOG 副檔名的方式，建立記錄檔歷程記錄。 **.LO_** 檔案的大小上限和使用例外是 Linux 和 UNIX 的用戶端。 如需 Linux 和 UNIX 的用戶端如何使用記錄檔的相關資訊，請參閱本主題之 [Linux 和 UNIX 的用戶端](#BKMK_LogFilesforLnU) 一節中的＜管理用於 Linux 和 UNIX 用戶端的用戶端記錄檔＞。  

 若要檢視記錄檔，可以使用 Configuration Manager 記錄檢視器工具 CMTrace，其位於 Configuration Manager來源媒體的 **\SMSSETUP\TOOLS** 資料夾中。 CMTrace 工具也會新增至所有 [軟體程式庫] 中新增的開機映像內。  

###  <a name="a-namebkmklogoptionsa-configure-logging-options-by-using-the-configuration-manager-service-manager"></a><a name="BKMK_LogOptions"></a> 使用 Configuration Manager Service Manager 設定記錄選項  
 Configuration Manager 支援可讓您變更記錄檔儲存位置和記錄檔大小的選項。  

 利用下列程序即可使用 [Configuration Manager Service Manager]  修改記錄檔大小、記錄檔名稱和位置，以及強制多個元件寫入單一記錄檔。  

##### <a name="to-modify-logging-for-a-component"></a>若要修改元件的記錄：  

1.  在 Configuration Manager 主控台中，按一下 [監視] 和 [系統狀態]，然後按一下 [站台狀態] 或 [元件狀態]。  

2.  在 [首頁]  索引標籤的 [元件]  群組中，按一下 [啟動]  並選取 [Configuration Manager Service Manager] 。  

3.  Configuration Manager Service Manager 開啟時，連線至您要管理的網站。  

     如果您未看見要管理的網站，請依序按一下 [網站] 、[連線] ，然後輸入正確網站的網站伺服器名稱。  

4.  展開網站，並根據您要管理的元件所在位置瀏覽至 [元件]  或 [伺服器] 。  

5.  在右側窗格中，選取一個或多個元件。  

6.  在 [元件]  功能表上，按一下 [記錄] 。  

7.  在 [Configuration Manager 元件記錄]  對話方塊中，完成您選取的可用設定選項。  

8.  按一下 [確定]  儲存設定。  

###  <a name="a-namebkmkloglocationa-locating-configuration-manager-logs"></a><a name="BKMK_LogLocation"></a> 尋找 Configuration Manager 記錄檔  
 根據預設，Configuration Manager 記錄檔會依據建立記錄檔的程序以及您站台系統的設定，儲存在各種不同的位置。 由於特定電腦的記錄檔位置可能有所不同，因此請使用搜尋尋找 Configuration Manager 電腦上的相關記錄檔幫助您進行特定案例的疑難排解。  

##  <a name="a-namebkmkclientlogsa-configuration-manager-client-logs"></a><a name="BKMK_ClientLogs"></a> Configuration Manager 用戶端記錄檔  
 下面各節列出與用戶端操作及用戶端安裝相關的記錄檔。  

###  <a name="a-namebkmkclientoplogsa-client-operations"></a><a name="BKMK_ClientOpLogs"></a> 用戶端操作  
 下表列出 Configuration Manager 用戶端上找到的記錄檔。  

|記錄檔名稱|說明|  
|--------------|-----------------|  
|CAS.log|內容存取服務。 維護用戶端上的本機套件快取。|  
|Ccm32BitLauncher.log|記錄啟動用戶端上標記為「以 32 位元執行」之應用程式的動作。|  
|CcmEval.log|記錄 Configuration Manager 用戶端狀態評估活動，以及 Configuration Manager 用戶端所需元件的詳細資料。|  
|CcmEvalTask.log|記錄評估排程工作起始的 Configuration Manager 用戶端狀態評估活動。|  
|CcmExec.log|記錄用戶端和 SMS Agent Host 服務的活動。 此記錄檔也包含有關啟用和停用喚醒 Proxy 的資訊。|  
|CcmMessaging.log|記錄與用戶端和管理點之間通訊相關的活動。|  
|CCMNotificationAgent.log|記錄與用戶端通知操作相關的活動。|  
|Ccmperf.log|記錄維護相關活動以及擷取用戶端效能計數器相關資料的活動。|  
|CcmRestart.log|記錄用戶端服務重新啟動活動。|  
|CCMSDKProvider.log|記錄用戶端 SDK 介面的活動。|  
|CertificateMaintenance.log|維護 Active Directory 網域服務和管理點的憑證。|  
|CIDownloader.log|記錄有關設定項目定義下載的詳細資料。|  
|CITaskMgr.log|記錄針對每一種應用程式和部署類型起始的工作，例如內容下載，或是安裝或解除安裝動作。|  
|ClientAuth.log|記錄用戶端的簽署和驗證活動。|  
|ClientIDManagerStartup.log|建立和維護用戶端 GUID，並識別在用戶端登錄和指派期間執行的工作。|  
|ClientLocation.log|記錄與用戶端網站指派相關的工作。|  
|CMHttpsReadiness.log|記錄執行 Configuration Manager HTTPS 整備評估工具的結果。 此工具會檢查電腦是否擁有可用於 Configuration Manager 的 PKI 用戶端驗證憑證。|  
|CmRcService.log|記錄遠端控制服務的資訊。|  
|ContentTransferManager.log|排程背景智慧型傳送服務 (BITS) 或伺服器訊息區 (SMB) 下載或存取套件。|  
|DataTransferService.log|記錄針對原則或套件存取的所有 BITS 通訊。|  
|EndpointProtectionAgent|記錄有關安裝 Endpoint Protection 用戶端以及對該用戶端應用反惡意程式碼原則的資訊。|  
|execmgr.log|記錄有關用戶端上所執行套件和工作順序的詳細資料。|  
|ExpressionSolver.log|記錄有關啟用詳細資訊記錄或偵錯記錄時所使用增強偵測方法的詳細資料。|  
|ExternalEventAgent.log|記錄 Endpoint Protection 惡意程式碼偵測的歷程記錄，以及與用戶端狀態相關的事件。|  
|FileBITS.log|記錄所有 SMB 套件存取工作。|  
|FileSystemFile.log|記錄 Windows Management Instrumentation (WMI) 提供者的軟體清查和檔案收集活動。|  
|FSPStateMessage.log|記錄用戶端傳送至後援狀態點的狀態訊息記錄。|  
|InternetProxy.log|記錄用戶端的網路 Proxy 設定和使用情形。|  
|InventoryAgent.log|記錄用戶端上硬體清查、軟體清查和活動訊號探索動作的活動。|  
|LocationCache.log|記錄用戶端的位置快取使用情形和維護的活動。|  
|LocationServices.log|記錄尋找管理點、軟體更新點和發佈點的用戶端活動。|  
|MaintenanceCoordinator.log|記錄用戶端一般維護工作的活動。|  
|Mifprovider.log|記錄 .MIF 檔的 WMI 提供者活動。|  
|mtrmgr.log|監視所有軟體計量程序。|  
|PolicyAgent.log|記錄使用資料傳輸服務發出的原則要求。|  
|PolicyAgentProvider.log|記錄原則變更。|  
|PolicyEvaluator.log|記錄有關用戶端電腦上原則評估的詳細資料，包括來自軟體更新的原則。|  
|PolicyPlatformClient.log|記錄位於 **%Program Files%\Microsoft Policy Platform**中所有提供者的補救和相容性程序，但不包括檔案提供者。|  
|PolicySdk.log|記錄原則系統 SDK 介面的活動。|  
|Pwrmgmt.log|記錄有關啟用或停用和設定喚醒 Proxy 用戶端設定的資訊。|  
|PwrProvider.log|記錄 Windows Management Instrumentation (WMI) 服務中所裝載電源管理提供者 (PWRInvProvider) 的活動。 在所有支援的 Windows 版本上，提供者會在硬體清查期間列舉電腦上目前的設定，並套用電源計畫的設定。|  
|SCClient_&lt;網域\>@&lt;使用者名稱\>_1.log|記錄軟體中心內用戶端電腦上所指定使用者的活動。|  
|SCClient_&lt;網域\>@&lt;使用者名稱\>_2.log|記錄軟體中心內用戶端電腦上所指定使用者的歷史活動。|  
|Scheduler.log|記錄所有用戶端操作之排程工作的活動。|  
|SCNotify_&lt;網域\>@&lt;使用者名稱\>_1.log|記錄通知使用者有關所指定使用者之軟體的活動。|  
|SCNotify_&lt;網域\>@&lt;使用者名稱\>_1-&lt;日期時間>.log|記錄通知使用者有關所指定使用者之軟體的歷史資訊。|  
|setuppolicyevaluator.log|記錄 WMI 中的設定和清查原則建立。|  
|SleepAgent_&lt;網域\>@&lt;@SYSTEM_0.log|喚醒 Proxy 的主要記錄檔。|  
|smscliui.log|記錄控制台中 Configuration Manager 用戶端的使用情形。|  
|SrcUpdateMgr.log|記錄更新為最新發佈點來源位置之已安裝 Windows Installer 應用程式的活動。|  
|StatusAgent.log|記錄用戶端元件所建立的狀態訊息。|  
|SWMTRReportGen.log|產生計量代理程式所收集的使用量資料報告。 這項資料會記錄在 Mtrmgr.log 中。|  
|UserAffinity.log|記錄有關使用者裝置親和性的詳細資料。|  
|VirtualApp.log|記錄評估 App-V 部署類型的專屬資訊。|  
|Wedmtrace.log|記錄有關 Windows Embedded 用戶端上寫入篩選器的操作。|  
|wakeprxy-install.log|記錄用戶端裝置收到啟用喚醒 Proxy 的用戶端設定選項時的安裝資訊。|  
|wakeprxy-uninstall.log|記錄有關用戶端收到停用喚醒 Proxy 的用戶端設定選項時，解除安裝喚醒 Proxy 的資訊 (如果之前已啟用喚醒 Proxy)。|  

###  <a name="a-namebkmkclientinstallloga-client-installation-log-files"></a><a name="BKMK_ClientInstallLog"></a> 用戶端安裝記錄檔  
 下表列出包含 Configuration Manager 用戶端安裝資訊的記錄檔。  

|記錄檔名稱|說明|  
|--------------|-----------------|  
|ccmsetup.log|記錄用戶端安裝、用戶端升級和用戶端移除的 **ccmsetup** 工作。 可用來進行用戶端安裝問題的疑難排解。|  
|ccmsetup-ccmeval.log|記錄用戶端狀態和補救 **ccmsetup** 工作。|  
|CcmRepair.log|記錄用戶端代理程式的修復活動。|  
|client.msi.log|記錄 client.msi 所執行的安裝工作。 可用於疑難排解用戶端安裝或移除問題。|  

###  <a name="a-namebkmklogfilesforlnua-client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a> Linux 和 UNIX 的用戶端  
 Linux 和 UNIX 的 Configuration Manager 用戶端會在下列記錄檔中記錄資訊。  

> [!TIP]  
>  從累計更新 1 之 Linux 和 UNIX 的用戶端開始，您可以使用 CMTrace 檢視 Linux 和 UNIX 的用戶端記錄檔。  

> [!NOTE]  
>  當您使用 Linux 和 UNIX 的用戶端初始版本，並參照本節中的說明文件時，請取代下列每個檔案或處理程序的參照：  
>   
>  -   將 **omiserver.bin** 取代為 **nwserver.bin**  
> -   將 **omi** 取代為 **nanowbem**  

|記錄檔名稱|詳細資料|  
|--------------|-------------|  
|scxcm.log|這是 Linux 和 UNIX 的 Configuration Manager 用戶端核心服務的記錄檔 (ccmexec.bin)。 此記錄檔包含有關 ccmexec.bin 的安裝和進行中操作的資訊。<br /><br /> 這個記錄檔預設建立在下列位置： **/var/opt/microsoft/scxcm.log**<br /><br /> 若要變更記錄檔的位置，請編輯 **/opt/microsoft/configmgr/etc/scxcm.conf** ，並變更 **PATH** 欄位。 您不需要重新啟動用戶端電腦或服務，變更會直接生效。<br /><br /> 您可以將記錄層級設定為下列四項不同設定的其中一項：|  
|scxcmprovider.log|這是 Linux 和 UNIX 的 Configuration Manager 用戶端 CIM 服務的記錄檔 (omiserver.bin)。 此記錄檔包含 nwserver.bin 進行中操作的相關資訊。<br /><br /> 這個記錄檔預設建立在下列位置： **/var/opt/microsoft/configmgr/scxcmprovider.log**<br /><br /> 若要變更記錄檔的位置，請編輯 **/opt/microsoft/omi/etc/scxcmprovider.conf** ，並變更 **PATH** 欄位。 您不需要重新啟動用戶端電腦或服務，變更會直接生效。<br /><br /> 您可以將記錄層級設定為下列三項不同設定的其中一項：|  

 **這兩個記錄檔支援數個記錄層級︰**  

-   **scxcm.log** - 若要變更記錄層級，請編輯 **/opt/microsoft/configmgr/etc/scxcm.conf** ，然後將 **MODULE** 標記的每一個執行個體變更為所需的記錄層級：  

    -   錯誤：指出需要注意的問題。  

    -   警告：指出用戶端作業可能發生的問題。  

    -   資訊：更詳細的記錄，表示用戶端上各種不同事件的狀態。  

    -   追蹤：詳細資訊記錄，通常用來診斷問題。  

-   **scxcmprovider.log** - 若要變更記錄層級，請編輯 **/opt/microsoft/omi/etc/scxcmprovider.conf** ，然後將標記 **MODULE** 的每一個執行個體變更為所需的記錄層級：  

    -   錯誤：指出需要注意的問題。  

    -   警告：指出用戶端作業可能發生的問題。  

    -   資訊：更詳細的記錄，表示用戶端上各種不同事件的狀態。  

在正常作業條件下，應該使用 ERROR 記錄層級。 ERROR 記錄層級會建立最小的記錄檔。 記錄層級由 ERROR 提升至 WARNING，再升至 INFO、TRACE，每個步驟都會隨著資料的寫入而使記錄檔變得更大。  

####  <a name="a-namebkmkmanagelinuxlogsa-manage-log-files-for-the-client-for-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a> 管理用於 Linux 和 UNIX 用戶端的用戶端記錄檔  
Linux 和 UNIX 的用戶端不會限制用戶端記錄檔大小上限，用戶端也不會自動將其 **.LOG** 檔的內容複製到另一個檔案，例如 **.LO_** 檔。 如果您想要控制記錄檔的大小上限，請實作一個可管理記錄檔，但與 Linux 和 UNIX 的 Configuration Manager 用戶端無關的程序。  

例如，您可以使用標準 Linux 和 UNIX 命令 **logrotate** 來管理用戶端記錄檔的大小和輪替。 Linux 與 UNIX 的 Configuration Manager 用戶端所提供的介面，可以讓 **logrotate** 提示用戶端記錄檔完成輪換的時間，方便用戶端可以繼續記錄到記錄檔。  

如需 **logrotate**的詳細資訊，請參閱您用於 Linux 和 UNIX 發佈的文件。  

###  <a name="a-namebkmklogfilesformaca-client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a> Mac 電腦的用戶端  
Mac 電腦的 Configuration Manager 用戶端會在下列記錄檔中記錄資訊。  

|記錄檔名稱|詳細資料|  
|--------------|-------------|  
|CCMClient-*&lt;日期時間>*.log|記錄與 Mac 用戶端作業的相關活動，包括應用程式管理、清查以及錯誤記錄。<br /><br /> 這個記錄檔位於 Mac 電腦上的 **/Library/Application Support/Microsoft/CCM/Logs** 資料夾內。|  
|CCMAgent-*&lt;日期時間>*.log|記錄與用戶端作業相關的資訊，包括使用者登入與登出作業以及 Mac 電腦活動。<br /><br /> 這個記錄檔位於 Mac 電腦上的 **~/Library/Logs** 資料夾內。|  
|CCMNotifications-*&lt;日期時間>*.log|記錄顯示在 Mac 電腦上，與 Configuration Manager 通知相關的活動。<br /><br /> 這個記錄檔位於 Mac 電腦上的 **~/Library/Logs** 資料夾內。|  
|CCMPrefPane-*&lt;日期時間>*.log|記錄 Mac 電腦上，與 Configuration Manager 喜好設定對話方塊相關的活動，包括一般狀態與錯誤記錄。<br /><br /> 這個記錄檔位於 Mac 電腦上的 **~/Library/Logs** 資料夾內。|  

 此外，網站系統伺服器上的 SMS_DM.log 記錄檔會記錄 Mac 電腦與針對行動裝置與 Mac 電腦啟用的管理點之間的通訊。  

##  <a name="a-namebkmkserverlogsa-configuration-manager-site-server-log-files"></a><a name="BKMK_ServerLogs"></a> Configuration Manager 站台伺服器記錄檔  
 下列章節列出在網站伺服器上找到的或是與特定網站系統角色相關的記錄檔。  

###  <a name="a-namebkmksitesiteserverloga-site-server-and-site-system-server-logs"></a><a name="BKMK_SiteSiteServerLog"></a> 站台伺服器與站台系統伺服器記錄檔  
 下表列出在 Configuration Manager 站台伺服器與站台系統伺服器上找到的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|adctrl.log|記錄註冊處理活動。|網站伺服器|  
|ADForestDisc.log|記錄 Active Directory 樹系探索動作。|網站伺服器|  
|ADService.log|記錄 Active Directory 內的帳戶建立與安全性群組詳細資料。|網站伺服器|  
|adsgdis.log|記錄 Active Directory 群組探索動作。|網站伺服器|  
|adsysdis.log|記錄 Active Directory 系統探索動作。|網站伺服器|  
|adusrdis.log|記錄 Active Directory 使用者探索動作。|網站伺服器|  
|ccm.log|記錄用戶端推入安裝活動。|網站伺服器|  
|CertMgr.log|記錄網站內通訊的憑證活動。|網站系統伺服器|  
|chmgr.log|記錄用戶端健全狀況管理員的活動。|網站伺服器|  
|Cidm.log|記錄由用戶端安裝資料管理員 (CIDM) 所做出的用戶端設定變更。|網站伺服器|  
|colleval.log|記錄有關集合評估工具建立、變更和刪除集合時的詳細資料。|網站伺服器|  
|compmon.log|記錄網站伺服器受監視元件執行緒的狀態。|網站系統伺服器|  
|compsumm.log|記錄元件狀態摘要器的工作。|網站伺服器|  
|ComRegSetup.log|記錄網站伺服器 COM 註冊的初始安裝結果。|網站系統伺服器|  
|dataldr.log|記錄有關處理 Configuration Manager 資料庫中管理資訊格式 (MIF) 檔案和硬體清查的資訊。|網站伺服器|  
|ddm.log|記錄探索資料管理員的活動。|網站伺服器|  
|despool.log|記錄傳入的網站對網站通訊傳輸。|網站伺服器|  
|distmgr.log|記錄有關套件建立、壓縮、差異複寫以及資訊更新的詳細資料。|網站伺服器|  
|EPCtrlMgr.log|記錄有關進入 Configuration Manager 資料庫，來自 Endpoint Protection 站台系統的惡意程式碼威脅的同步處理資訊。|網站伺服器|  
|EPMgr.log|記錄 Endpoint Protection 網站系統角色的狀態。|網站系統伺服器|  
|EPSetup.log|提供有關安裝 Endpoint Protection 網站系統角色的資訊。|網站系統伺服器|  
|EnrollSrv.log|記錄註冊服務處理程序的活動。|網站系統伺服器|  
|EnrollWeb.log|記錄註冊網站處理程序的活動。|網站系統伺服器|  
|fspmgr.log|記錄後援狀態點網站系統角色的活動。|網站系統伺服器|  
|hman.log|記錄有關網站設定變更的資訊，以及 Active Directory 網域服務中的網站資訊發佈。|網站伺服器|  
|Inboxast.log|記錄從管理點移動到網站伺服器上相對應 INBOXES 資料夾的檔案。|網站伺服器|  
|inboxmgr.log|記錄收件匣資料夾之間的檔案傳輸活動。|網站伺服器|  
|inboxmon.log|記錄收件匣檔案處理與效能計數器更新。|網站伺服器|  
|invproc.log|記錄從次要網站將 MIF 檔案轉寄至其父網站的情形。|網站伺服器|  
|migmctrl.log|記錄移轉動作的資訊，包括移轉作業、共用發佈點以及發佈點升級。|Configuration Manager 階層中的頂層站台，以及每個子主要站台<br /><br /> 在多重主要網站階層中，使用管理中心網站上建立的記錄檔。|  
|mpcontrol.log|記錄具有 WINS 的管理點的註冊。 每 10 分鐘記錄一次管理點的可用性。|網站系統伺服器|  
|mpfdm.log|記錄將用戶端檔案移動到網站伺服器上相對應 INBOXES 資料夾的管理點元件動作。|網站系統伺服器|  
|mpMSI.log|記錄有關管理點安裝的詳細資料。|網站伺服器|  
|MPSetup.log|記錄管理點安裝包裝函式處理程序。|網站伺服器|  
|netdisc.log|記錄網路探索的動作。|網站伺服器|  
|ntsvrdis.log|記錄網站系統伺服器的探索活動。|網站伺服器|  
|Objreplmgr|針對複寫動作記錄物件變更通知的處理。|網站伺服器|  
|offermgr.log|記錄公告更新。|網站伺服器|  
|offersum.log|記錄部署狀態訊息的摘要。|網站伺服器|  
|OfflineServicingMgr.log|記錄套用更新至作業系統影像檔案的活動。|網站伺服器|  
|outboxmon.log|記錄寄件匣檔案處理與效能計數器更新。|網站伺服器|  
|PerfSetup.log|記錄效能計數器的安裝結果。|網站系統伺服器|  
|PkgXferMgr.log|記錄負責從主要網站傳送內容至遠端發佈點的 SMS Executive 元件的動作。|網站伺服器|  
|policypv.log|記錄可反映用戶端設定或部署變更的用戶端原則更新。|主要網站伺服器|  
|rcmctrl.log|記錄階層中網站間的資料庫複寫活動。|網站伺服器|  
|replmgr.log|記錄網站伺服器元件與排程器元件之間的檔案複寫。|網站伺服器|  
|ResourceExplorer.log|記錄有關執行資源總管的錯誤、警告以及資訊。|執行 Configuration Manager 主控台的電腦|  
|ruleengine.log|記錄有關識別、內容下載以及軟體更新群組與部署建立的自動部署規則的詳細資料。|網站伺服器|  
|schedule.log|記錄有關網站對網站作業與檔案複寫的詳細資料。|網站伺服器|  
|sender.log|記錄網站間檔案複寫所傳輸的檔案。|網站伺服器|  
|sinvproc.log|記錄網站資料庫之軟體清查資料處理的相關資訊。|網站伺服器|  
|sitecomp.log|記錄有關網站內所有網站系統伺服器上已安裝網站元件的維護詳細資料。|網站伺服器|  
|sitectrl.log|記錄資料庫內網站控制物件的網站設定變更。|網站伺服器|  
|sitestat.log|記錄所有網站系統的可用性與磁碟空間監視程序。|網站伺服器|  
|SmsAdminUI.log|記錄 Configuration Manager 主控台活動。|執行 Configuration Manager 主控台的電腦|  
|SMSAWEBSVCSetup.log|記錄應應用程式類別目錄 Web 服務的安裝活動。|網站系統伺服器|  
|smsbkup.log|記錄來自網站備份程序的輸出。|網站伺服器|  
|smsdbmon.log|記錄資料庫變更。|網站伺服器|  
|SMSENROLLSRVSetup.log|記錄註冊 Web 服務的安裝活動。|網站系統伺服器|  
|SMSENROLLWEBSetup.log|記錄註冊網站的安裝活動。|網站系統伺服器|  
|smsexec.log|記錄所有網站伺服器元件執行緒的處理。|網站伺服器或網站系統伺服器|  
|SMSFSPSetup.log|記錄由後援狀態點安裝所產生的訊息。|網站系統伺服器|  
|SMSPORTALWEBSetup.log|記錄應用程式類別目錄網站的安裝活動。|網站系統伺服器|  
|SMSProv.log|記錄對網站資料庫的 WMI 提供者存取。|SMS 提供者的電腦|  
|srsrpMSI.log|記錄從 MSI 輸出的報告點安裝處理的詳細結果。|網站系統伺服器|  
|srsrpsetup.log|記錄報告點安裝處理的結果。|網站系統伺服器|  
|statesys.log|記錄狀態系統訊息的處理訊息。|網站伺服器|  
|statmgr.log|記錄傳送至資料庫的所有狀態訊息的編寫。|網站伺服器|  
|swmproc.log|記錄測量檔案與設定的處理。|網站伺服器|  

###  <a name="a-namebkmksiteinstallloga-site-server-installation-log-files"></a><a name="BKMK_SiteInstallLog"></a> 站台伺服器安裝記錄檔  
 下表列出包含網站安裝相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|記錄先決條件元件評估和安裝活動。|網站伺服器|  
|ConfigMgrSetup.log|記錄來自網站伺服器安裝的詳細資料輸出。|網站伺服器|  
|ConfigMgrSetupWizard.log|記錄安裝精靈內與活動相關的資訊。|網站伺服器|  
|SMS_BOOTSTRAP.log|記錄有關啟動次要網站安裝處理進度的資訊。 包含在 ConfigMgrSetup.log 內的實際安裝處理詳細資料。|網站伺服器|  
|smstsvc.log|記錄安裝、使用以及移除 Windows 服務的資訊，而該服務使用初始連線的伺服器的電腦帳戶，測試伺服器間的網路連線性與權限。|網站伺服器和網站系統|  

###  <a name="a-namebkmkfsploga-fallback-status-point-logs-files"></a><a name="BKMK_FSPLog"></a> 後援狀態點記錄檔  
 下表列出包含後援狀態點相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|FspIsapi|記錄有關行動裝置舊版用戶端和用戶端電腦與後援狀態點之通訊的詳細資料。|網站系統伺服器|  
|fspMSI.log|記錄由後援狀態點安裝所產生的訊息。|網站系統伺服器|  
|fspmgr.log|記錄後援狀態點網站系統角色的活動。|網站系統伺服器|  

###  <a name="a-namebkmkmploga-management-point-logs-files"></a><a name="BKMK_MPLog"></a> 管理點記錄檔  
 下表列出包含管理點相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|記錄端點上的用戶端訊息活動。|網站系統伺服器|  
|MP_CliReg.log|記錄由管理點處理的用戶端註冊活動。|網站系統伺服器|  
|MP_Ddr.log|記錄來自用戶端的 XML.ddr 記錄轉換，並將這些記錄複製到網站伺服器。|網站系統伺服器|  
|MP_Framework.log|記錄核心管理點與用戶端架構元件的活動。|網站系統伺服器|  
|MP_GetAuth.log|記錄用戶端授權活動。|網站系統伺服器|  
|MP_GetPolicy.log|記錄來自用戶端電腦的原則要求活動。|網站系統伺服器|  
|MP_Hinv.log|記錄來自用戶端的 XML 硬體清查記錄轉換的詳細資料，並將這些檔案複製到網站伺服器。|網站系統伺服器|  
|MP_Location.log|記錄來自用戶端的位置要求與回覆活動。|網站系統伺服器|  
|MP_OOBMgr.log|記錄從用戶端接收 OTP 的相關管理點活動。|網站系統伺服器|  
|MP_Policy.log|記錄原則的通訊。|網站系統伺服器|  
|MP_Relay.log|記錄收集自用戶端的檔案傳輸。|網站系統伺服器|  
|MP_Retry.log|記錄硬體清查重試處理程序。|網站系統伺服器|  
|MP_Sinv.log|記錄來自用戶端的 XML 軟體清查記錄轉換的詳細資料，並將這些檔案複製到網站伺服器。|網站系統伺服器|  
|MP_SinvCollFile.log|記錄有關檔案集合的詳細資料。|網站系統伺服器|  
|MP_Status.log|記錄來自用戶端的 XML.svf 狀態訊息轉換，並將這些檔案複製到網站伺服器的詳細資料。|網站系統伺服器|  
|mpcontrol.log|記錄具有 WINS 的管理點的註冊。 每 10 分鐘記錄一次管理點的可用性。|網站伺服器|  
|mpfdm.log|記錄將用戶端檔案移動到網站伺服器上相對應 INBOXES 資料夾的管理點元件動作。|網站系統伺服器|  
|mpMSI.log|記錄有關管理點安裝的詳細資料。|網站伺服器|  
|MPSetup.log|記錄管理點安裝包裝函式處理程序。|網站伺服器|  

###  <a name="a-namebkmksuploga-software-update-point-log-files"></a><a name="BKMK_SUPLog"></a> 軟體更新點記錄檔  
 下表列出包含軟體更新點相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|記錄從父網站到子網站的軟體更新通知檔案的複寫詳細資料。|網站伺服器|  
|PatchDownloader.log|記錄有關從更新來源將軟體更新下載至網站伺服器上目的地之程序的詳細資料。|裝載 Configuration Manager 主控台的電腦，下載會從該處起始|  
|ruleengine.log|記錄有關識別、內容下載以及軟體更新群組與部署建立的自動部署規則的詳細資料。|網站伺服器|  
|SUPSetup.log|記錄有關軟體更新點安裝的詳細資料。 當軟體更新點安裝完成時， **Installation was successful** 會寫入此記錄檔中。|網站系統伺服器|  
|WCM.log|記錄有關訂閱的更新類別、分類和語言的軟體更新點設定，以及 Windows Server Update Services (WSUS) 伺服器連線的詳細資料。|連線至 Windows Server Update Services (WSUS) 伺服器的網站伺服器|  
|WSUSCtrl.log|記錄有關網站的設定、資料庫連線和 WSUS 伺服器健全狀況的詳細資料。|網站系統伺服器|  
|wsyncmgr.log|記錄有關軟體更新同步處理程序的詳細資料。|網站系統伺服器|  
|WUSSyncXML.log|記錄有關 Inventory Tool for Microsoft Updates 同步處理程序的詳細資料。|設定為 Inventory Tool for Microsoft Updates 之同步處理主機的用戶端電腦。|  

##  <a name="a-namebkmkfunctionlogsa-log-files-for-configuration-manager-functionality"></a><a name="BKMK_FunctionLogs"></a> Configuration Manager 功能的記錄檔  
 下面各節列出與 Configuration Manager 中不同功能相關的記錄檔。  

###  <a name="a-namebkmkappmanageloga-application-management"></a><a name="BKMK_AppManageLog"></a> 應用程式管理  
 下表列出包含應用程式管理相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|記錄有關應用程式目前和預期狀態、其適用性、是否符合需求、部署類型及相依性的詳細資料。|用戶端|  
|AppDiscovery.log|記錄有關用戶端電腦上探索和偵測應用程式的詳細資料。|用戶端|  
|AppEnforce.log|記錄有關針對用戶端上的應用程式所採取強制動作的詳細資料 (安裝和解除安裝)。|用戶端|  
|awebsctl.log|記錄應用程式類別目錄 Web 服務點網站系統角色的監視活動。|網站系統伺服器|  
|awebsvcMSI.log|記錄應用程式類別目錄 Web 服務點網站系統角色的詳細安裝資訊。|網站系統伺服器|  
|CCMSDKProvider.log|記錄應用程式管理 SDK 的活動。|用戶端|  
|colleval.log|記錄有關集合評估工具建立、變更和刪除集合時的詳細資料。|網站系統伺服器|  
|ConfigMgrSoftwareCatalog.log|記錄應用程式類別目錄的活動，包括其 Silverlight 的使用情形。|用戶端|  
|portlctl.log|記錄應用程式類別目錄網站點網站系統角色的監視活動。|網站系統伺服器|  
|portlwebMSI.log|記錄應用程式類別目錄網站角色的 MSI 安裝活動。|網站系統伺服器|  
|PrestageContent.log|記錄有關遠端預先設置的發佈點上 ExtractContent.exe 工具使用情形的詳細資料。 此工具會擷取已匯出至檔案的內容。|網站系統伺服器|  
|ServicePortalWebService.log|記錄應用程式類別目錄 Web 服務的活動。|網站系統伺服器|  
|ServicePortalWebSite.log|記錄應用程式類別目錄網站的活動。|網站系統伺服器|  
|SMSdpmon.log|記錄有關發佈點上所設定發佈點健全狀況監視排程工作的詳細資料。|網站伺服器|  
|SoftwareCatalogUpdateEndpoint.log|記錄管理軟體中心內所顯示應用程式類別目錄 URL 的活動。|用戶端|  
|SoftwareCenterSystemTasks.log|記錄軟體中心必要條件元件驗證的活動。|用戶端|  

 下表列出包含部署封裝和程式之相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|colleval.log|記錄有關集合評估工具建立、變更和刪除集合時的詳細資料。|網站伺服器|  
|execmgr.log|記錄有關所執行套件和工作順序的詳細資料。|用戶端|  

###  <a name="a-namebkmkailoga-asset-intelligence"></a><a name="BKMK_AILog"></a> Asset Intelligence  
 下表列出包含 Asset Intelligence 相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|記錄 Asset Intelligence 清查動作的活動。|用戶端|  
|aikbmgr.log|記錄有關處理收件匣中 XML 檔案以更新 Asset Intelligence 類別目錄的詳細資料。|網站伺服器|  
|AIUpdateSvc.log|記錄 Asset Intelligence 同步處理點與 SCO (System Center Online) 線上 Web 服務的互動。|網站系統伺服器|  
|AIUSMSI.log|記錄有關安裝 Asset Intelligence 同步處理點網站系統角色的詳細資料。|網站系統伺服器|  
|AIUSSetup.log|記錄有關安裝 Asset Intelligence 同步處理點網站系統角色的詳細資料。|網站系統伺服器|  
|ManagedProvider.log|記錄有關使用相關軟體識別標記探索軟體的詳細資料。 另外也會記錄有關硬體清查的活動。|網站系統伺服器|  
|MVLSImport.log|記錄有關處理所匯入授權檔案的詳細資料。|網站系統伺服器|  

###  <a name="a-namebkmkbnrloga-backup-and-recovery"></a><a name="BKMK_BnRLog"></a> 備份及復原  
 下表列出包含備份和復原動作相關資訊的記錄檔，包括網站重設以及 SMS 提供者的變更。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|記錄有關 Configuration Manager 從備份復原站台時的設定和復原工作的資訊。|網站伺服器|  
|smsbkup.log|記錄有關網站備份活動的詳細資料。|網站伺服器|  
|smssqlbkup.log|記錄 SQL Server 與網站伺服器安裝在不同伺服器上時，來自網站資料庫備份程序的輸出。|網站資料庫伺服器|  
|Smswriter.log|記錄有關備份程序所使用 Configuration Manager VSS 寫入器之狀態的資訊。|網站伺服器|  

###  <a name="a-namebkmkcertificateenrollmenta-certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a> 憑證註冊  
 下表列出包含與憑證註冊相關資訊的 Configuration Manager 記錄檔，其使用憑證登錄點以及伺服器上執行網路裝置註冊服務的 Configuration Manager 原則模組。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|Crp.log|記錄註冊活動。|憑證登錄點|  
|Crpctrl.log|記錄憑證登錄點的操作健全狀況。|憑證登錄點|  
|Crpsetup.log|記錄有關憑證登錄點的安裝和設定詳細資料。|憑證登錄點|  
|Crpmsi.log|記錄有關憑證登錄點的安裝和設定詳細資料。|憑證登錄點|  
|NDESPlugin.log|記錄挑戰驗證和憑證註冊活動。|Configuration Manager 原則模組和網路裝置註冊服務|  

 除了 Configuration Manager 記錄檔以外，檢閱執行網路裝置註冊服務之伺服器上，以及裝載憑證登錄點之伺服器上的事件檢視器中的 Windows 應用程式記錄檔。 例如，尋找來自 **NetworkDeviceEnrollmentService** 來源的訊息。 您也可以使用下列記錄檔：  

-   網路裝置註冊服務的 IIS 記錄檔︰**&lt;路徑\>\inetpub\logs\LogFiles\W3SVC1**  

-   憑證登錄點的 IIS 記錄檔︰**&lt;路徑\>\inetpub\logs\LogFiles\W3SVC1**  

-   網路裝置註冊原則記錄檔： **mscep.log**  

    > [!NOTE]  
    >  此檔案位於網路裝置註冊服務帳戶設定檔的資料夾內，例如 C:\Users\SCEPSvc。 如需如何啟用網路裝置註冊服務記錄功能的詳細資訊，請參閱 TechNet WiKi 上的 Network Device Enrollment Service (NDES) in Active Directory Certificate Services (AD CS) 文章中 [Enable Logging (啟用記錄功能)](http://go.microsoft.com/fwlink/?LinkId=320576) 一節。  

###  <a name="a-namebkmkbgba-client-notification"></a><a name="BKMK_BGB"></a> 用戶端通知  
 下表列出包含用戶端通知相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|記錄與用戶端通知工作及處理線上和工作狀態檔案相關的網站伺服器活動詳細資料。|網站伺服器|  
|BGBServer.log|記錄通知伺服器的活動，例如用戶端與伺服器通訊和推送工作給用戶端。 也記錄線上和要傳送到站台伺服器之工作狀態檔案產生的相關資訊。|管理點|  
|BgbSetup.log|記錄安裝和解除安裝期間通知伺服器安裝包裝函式程序的活動。|管理點|  
|bgbisapiMSI.log|記錄有關通知伺服器安裝和解除安裝的詳細資料。|管理點|  
|BgbHttpProxy.log|記錄通知 HTTP Proxy 使用 HTTP 在通知伺服器上來回轉送用戶端訊息時的活動。|用戶端|  
|CCMNotificationAgent.log|記錄通知代理程式的活動，例如用戶端-伺服器通訊，以及接收到和發送至其他用戶端代理程式之工作的相關資訊。|用戶端|  

###  <a name="a-namebkmkcompsettingsloga-compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a> 相容性設定和公司資源存取  
 下表列出包含相容性設定和公司資源存取相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|記錄有關相容性設定、軟體更新及應用程式管理之補救和相容性程序的詳細資料。|用戶端|  
|CITaskManager.log|記錄有關設定項目工作排程的資訊。|用戶端|  
|DCMAgent.log|記錄有關設定項目和應用程式的評估、衝突報告及補救的高階資訊。|用戶端|  
|DCMReporting.log|記錄有關在設定項目的狀態訊息內報告原則平台結果的資訊。|用戶端|  
|DcmWmiProvider.log|記錄有關從 Windows Management Instrumentation (WMI) 讀取設定項目 synclet 的資訊。|用戶端|  

###  <a name="a-namebkmkconsoleloga-configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a> Configuration Manager 主控台  
 下表列出包含 Configuration Manager 主控台相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|記錄 Configuration Manager 主控台的安裝。|執行 Configuration Manager 主控台的電腦|  
|SmsAdminUI.log|記錄有關操作 Configuration Manager 主控台的資訊。|執行 Configuration Manager 主控台的電腦|  
|SMSProv.log|SMS 提供者所執行的記錄活動。 Configuration Manager 主控台活動會使用 SMS 提供者。|網站伺服器或網站系統伺服器|  

###  <a name="a-namebkmkcontentloga-content-management"></a><a name="BKMK_ContentLog"></a> 內容管理  
 下表列出包含內容管理相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;GUID\>.log|記錄特定雲端發佈點的詳細資料，包括有關儲存和內容存取的資訊。|網站系統伺服器|  
|CloudMgr.log|記錄有關佈建內容、收集儲存和頻寬分析資料，以及系統管理員起始動作以停止或啟動執行雲端發佈點之雲端服務等等的詳細資料。|網站系統伺服器|  
|DataTransferService.log|記錄針對原則或套件存取的所有 BITS 通訊。 提取發佈點進行內容管理時也會使用此記錄。|設定為提取發佈點的電腦|  
|PullDP.log|記錄有關提取發佈點從來源發佈點傳送之內容的詳細資料。|設定為提取發佈點的電腦|  
|PrestageContent.log|記錄有關遠端預先設置的發佈點上 ExtractContent.exe 工具使用情形的詳細資料。 此工具會擷取已匯出至檔案的內容。|網站系統角色|  
|SMSdpmon.log|記錄發佈點上所設定之發佈點健全狀況監視排程工作的詳細資料。|網站系統角色|  
|smsdpprov.log|記錄有關從主要網站收到之壓縮檔解壓縮的詳細資料。 此記錄檔為遠端發佈點的 WMI 提供者所產生。|未與網站伺服器共置的發佈點電腦。|  

###  <a name="a-namebkmkdiscoveryloga-discovery"></a><a name="BKMK_DiscoveryLog"></a> 探索  
下表列出包含探索相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|記錄 Active Directory 安全性群組探索的動作。|網站伺服器|  
|adsysdis.log|記錄 Active Directory 系統探索動作。|網站伺服器|  
|adusrdis.log|記錄 Active Directory 使用者探索動作。|網站伺服器|  
|ADForestDisc.log|記錄 Active Directory 樹系探索動作。|網站伺服器|  
|ddm.log|記錄探索資料管理員的活動。|網站伺服器|  
|InventoryAgent.log|記錄用戶端上硬體清查、軟體清查和活動訊號探索動作的活動。|用戶端|  
|netdisc.log|記錄網路探索的動作。|網站伺服器|  

###  <a name="a-namebkmkeploga-endpoint-protection"></a><a name="BKMK_EPLog"></a> Endpoint Protection  
 下表列出包含 Endpoint Protection 相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|記錄有關安裝 Endpoint Protection 用戶端，以及對該用戶端應用反惡意程式碼原則的詳細資料。|用戶端|  
|EPCtrlMgr.log|記錄有關將 Endpoint Protection 角色伺服器中的惡意程式碼威脅資訊同步處理至 Configuration Manager 資料庫的詳細資料。|網站系統伺服器|  
|EPMgr.log|監視 Endpoint Protection 網站系統角色的狀態。|網站系統伺服器|  
|EPSetup.log|提供有關安裝 Endpoint Protection 網站系統角色的資訊。|網站系統伺服器|  

###  <a name="a-namebkmkextensionsa-extensions"></a><a name="BKMK_Extensions"></a> 擴充功能  
 下表列出包含擴充功能相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|記錄有關從 Microsoft 下載擴充功能，以及安裝和解除安裝所有擴充功能的資訊。|執行 Configuration Manager 主控台的電腦|  
|FeatureExtensionInstaller.log|記錄有關在 Configuration Manager 主控台中啟用或停用擴充功能時，安裝及移除個別擴充功能的資訊。|執行 Configuration Manager 主控台的電腦|  
|SmsAdminUI.log|記錄 Configuration Manager 主控台活動。|執行 Configuration Manager 主控台的電腦|  

###  <a name="a-namebkmkinventoryloga-inventory"></a><a name="BKMK_InventoryLog"></a> 清查  
 下表列出包含處理清查資料之相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|dataldr.log|記錄有關處理 Configuration Manager 資料庫中管理資訊格式 (MIF) 檔案和硬體清查的資訊。|網站伺服器|  
|invproc.log|記錄從次要網站將 MIF 檔案轉寄至其父網站的情形。|次要網站伺服器|  
|sinvproc.log|記錄網站資料庫之軟體清查資料處理的相關資訊。|網站伺服器|  

###  <a name="a-namebkmkmeteringloga-metering"></a><a name="BKMK_MeteringLog"></a> 計量  
 下表列出包含計量相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|監視所有軟體計量程序。|網站伺服器|  

###  <a name="a-namebkmkmigrationloga-migration"></a><a name="BKMK_MigrationLog"></a> 移轉  
 下表列出包含移轉相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|記錄有關包含移轉作業、共用發佈點及發佈點升級等移轉動作的資訊。|Configuration Manager 階層中的頂層站台，以及每個子主要站台<br /><br /> 在多重主要網站階層中，使用管理中心網站上建立的記錄檔。|  

###  <a name="a-namebkmkmdmloga-mobile-devices"></a><a name="BKMK_MDMLog"></a> 行動裝置  
 下面各節列出包含管理行動裝置之相關資訊的記錄檔。  

####  <a name="a-namebkmkenrollmentloga-enrollment"></a><a name="BKMK_EnrollmentLog"></a> 註冊  
 下表列出包含行動裝置註冊相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|記錄針對行動裝置啟用之管理點與管理點端點之間的通訊。|網站系統伺服器|  
|dmpmsi.log|記錄設定針對行動裝置啟用之管理點的 Windows Installer 資料。|網站系統伺服器|  
|DMPSetup.log|記錄針對行動裝置啟用之管理點的設定。|網站系統伺服器|  
|enrollsrvMSI.log|記錄設定註冊點的 Windows Installer 資料。|網站系統伺服器|  
|enrollmentweb.log|記錄行動裝置與註冊 Proxy 點之間的通訊。|網站系統伺服器|  
|enrollwebMSI.log|記錄設定註冊 Proxy 點的 Windows Installer 資料。|網站系統伺服器|  
|enrollmentservice.log|記錄註冊 Proxy 點與註冊點之間的通訊。|網站系統伺服器|  
|SMS_DM.log|記錄行動裝置、Mac 電腦及針對行動裝置與 Mac 電腦啟用的管理點之間的通訊。|網站系統伺服器|  

####  <a name="a-namebkmkexchsrvloga-exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a> Exchange Server 連接器  
 下表列出包含 Exchange Server 連接器相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|easdisc.log|記錄 Exchange Server 連接器的活動和狀態。|網站伺服器|  

####  <a name="a-namebkmkmdlegloga-mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a> 行動裝置舊版  
 下表列出包含行動裝置舊版用戶端相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|記錄有關行動裝置舊版用戶端上憑證註冊資料的詳細資料。|用戶端|  
|DMCertResp.htm|記錄行動裝置舊版用戶端註冊工具程式要求 PKI 憑證時，來自憑證伺服器的 HTML 回應。|用戶端|  
|DmClientHealth.log|記錄與針對行動裝置啟用的管理點進行通訊之所有行動裝置舊版用戶端的 GUID。|網站系統伺服器|  
|DmClientRegistration.log|記錄行動裝置舊版用戶端上的登錄要求和回應。|網站系統伺服器|  
|DmClientSetup.log|記錄行動裝置舊版用戶端的用戶端安裝資料。|用戶端|  
|DmClientXfer.log|記錄行動裝置舊版用戶端和 ActiveSync 部署的用戶端傳輸資料。|用戶端|  
|DmCommonInstaller.log|記錄設定行動裝置舊版用戶端傳輸檔案的用戶端傳輸檔案安裝。|用戶端|  
|DmInstaller.log|記錄行動裝置舊版用戶端的 DMInstaller 是否正確呼叫 DmClientSetup，以及 DmClientSetup 結束為成功或失敗。|用戶端|  
|DmpDatastore.log|記錄針對行動裝置啟用之管理點進行的所有網站資料庫連線和查詢。|網站系統伺服器|  
|DmpDiscovery.log|記錄針對行動裝置啟用的管理點上，行動裝置舊版用戶端的所有探索資料。|網站系統伺服器|  
|DmpHardware.log|記錄針對行動裝置啟用的管理點上，行動裝置舊版用戶端的硬體清查資料。|網站系統伺服器|  
|DmpIsapi.log|記錄行動裝置舊版用戶端與針對行動裝置啟用之管理點的通訊。|網站系統伺服器|  
|dmpmsi.log|記錄設定針對行動裝置啟用之管理點的 Windows Installer 資料。|網站系統伺服器|  
|DMPSetup.log|記錄針對行動裝置啟用之管理點的設定。|網站系統伺服器|  
|DmpSoftware.log|記錄針對行動裝置啟用的管理點上，行動裝置舊版用戶端的軟體發佈資料。|網站系統伺服器|  
|DmpStatus.log|記錄針對行動裝置啟用的管理點上，行動裝置用戶端的狀態訊息資料。|網站系統伺服器|  
|DmSvc.log|記錄行動裝置舊版用戶端與針對行動裝置啟用之管理點的用戶端通訊。|用戶端|  
|FspIsapi.log|記錄有關行動裝置舊版用戶端和用戶端電腦與後援狀態點之通訊的詳細資料。|網站系統伺服器|  

###  <a name="a-namebkmkosdloga-operating-system-deployment"></a><a name="BKMK_OSDLog"></a> 作業系統部署  
 下表列出包含作業系統部署相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|CAS.log|記錄找到參照內容的發佈點時的詳細資料。|用戶端|  
|ccmsetup.log|記錄用戶端安裝、用戶端升級和用戶端移除的 **ccmsetup** 工作。 可用來進行用戶端安裝問題的疑難排解。|用戶端|  
|CreateTSMedia.log|記錄建立工作順序媒體的詳細資料。|執行 Configuration Manager 主控台的電腦|  
|DeployToVhd.log|記錄有關 VHD 建立和修改程序的詳細資料|執行 Configuration Manager 主控台的電腦|  
|Dism.log|記錄離線維修的驅動程式安裝動作或更新套用動作。|網站系統伺服器|  
|distmgr.log|記錄有關設定啟用 PXE 之發佈點的詳細資料。|網站系統伺服器|  
|DriverCatalog.log|記錄有關已匯入驅動程式類別目錄之裝置驅動程式的詳細資料。|網站系統伺服器|  
|mcsisapi.log|記錄多點傳送套件傳輸和用戶端要求回應的資訊。|網站系統伺服器|  
|mcsexec.log|記錄健全狀況檢查、命名空間、工作階段建立及憑證檢查的動作。|網站系統伺服器|  
|mcsmgr.log|記錄設定、安全性模式和可用性的變更。|網站系統伺服器|  
|mcsprv.log|記錄多點傳送提供者與 Windows 部署服務 (WDS) 的互動。|網站系統伺服器|  
|MCSSetup.log|記錄有關多點傳送伺服器角色安裝的詳細資料。|網站系統伺服器|  
|MCSMSI.log|記錄有關多點傳送伺服器角色安裝的詳細資料。|網站系統伺服器|  
|Mcsperf.log|記錄有關多點傳送效能計數器更新的詳細資訊。|網站系統伺服器|  
|MP_ClientIDManager.log|記錄從 PXE 或開機媒體起始之用戶端識別碼要求工作順序的管理點回應。|網站系統伺服器|  
|MP_DriverManager.log|記錄對 [自動套用驅動程式] 工作順序動作要求的管理點回應。|網站系統伺服器|  
|OfflineServicingMgr.log|記錄作業系統 .wim 檔案上的離線維修排程和更新套用動作的詳細資料。|網站系統伺服器|  
|Setupact.log|記錄有關 Windows Sysprep 和安裝記錄檔的詳細資料。|用戶端|  
|Setupapi.log|記錄有關 Windows Sysprep 和安裝記錄檔的詳細資料。|用戶端|  
|Setuperr.log|記錄有關 Windows Sysprep 和安裝記錄檔的詳細資料。|用戶端|  
|smpisapi.log|記錄有關用戶端狀態擷取和還原動作的詳細資料，以及臨界值資訊。|用戶端|  
|Smpmgr.log|記錄有關狀態移轉點健全狀況檢查和設定變更之結果的詳細資料。|網站系統伺服器|  
|smpmsi.log|記錄有關狀態移轉點的安裝和設定詳細資料。|網站系統伺服器|  
|smpperf.log|記錄狀態移轉點效能計數器更新。|網站系統伺服器|  
|smspxe.log|記錄有關 PXE 開機之用戶端的回應詳細資料，以及擴充開機映像和開機檔案的相關詳細資料。|網站系統伺服器|  
|smssmpsetup.log|記錄有關狀態移轉點的安裝和設定詳細資料。|網站系統伺服器|  
|Smsts.log|記錄工作序列的活動。|用戶端|  
|TSAgent.log|記錄啟動工作順序之前工作順序相依性的結果。|用戶端|  
|TaskSequenceProvider.log|記錄有關匯入、匯出或編輯工作順序時的詳細資料。|網站系統伺服器|  
|loadstate.log|記錄有關使用者狀態移轉工具 (USMT) 和還原使用者狀態資料的詳細資料。|用戶端|  
|scanstate.log|記錄有關使用者狀態移轉工具 (USMT) 和擷取使用者狀態資料的詳細資料。|用戶端|  

###  <a name="a-namebkmkpowermgmtloga-power-management"></a><a name="BKMK_PowerMgmtLog"></a> 電源管理  
 下表列出包含電源管理相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|Pwrmgmt.log|記錄有關用戶端電腦上電源管理活動的詳細資料，包括電源管理用戶端代理程式的監視和強制執行設定。|用戶端|  

###  <a name="a-namebkmkrcloga-remote-control"></a><a name="BKMK_RCLog"></a> 遠端控制  
 下表列出包含遠端控制相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|記錄有關遠端控制檢視器之活動的詳細資料。|位於執行遠端控制檢視器之電腦上的 *%temp%* 資料夾中。|  

###  <a name="a-namebkmkreportloga-reporting"></a><a name="BKMK_ReportLog"></a> 報告  
 下表列出包含報告相關資訊的 Configuration Manager 記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|srsrp.log|記錄有關 Reporting Services 點之活動和狀態的資訊。|網站系統伺服器|  
|srsrpMSI.log|記錄來自 MSI 輸出的 Reporting Services 點安裝程序的詳細結果。|網站系統伺服器|  
|srsrpsetup.log|記錄 Reporting Services 點安裝程序的結果。|網站系統伺服器|  

###  <a name="a-namebkmkrbaloga-role-based-administration"></a><a name="BKMK_RBALog"></a> 以角色為基礎的系統管理  
 下表列出包含管理以角色為基礎之系統管理相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|hman.log|記錄有關網站設定變更，以及發佈網站資訊至 Active Directory 網域服務的資訊。|網站伺服器|  
|SMSProv.log|記錄對網站資料庫的 WMI 提供者存取。|SMS 提供者的電腦|  

###  <a name="a-namebkmkwitloga-service-connection-point"></a><a name="BKMK_WITLog"></a> 服務連接點  
 下表列出包含與服務連接點相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|記錄憑證和 Proxy 帳戶資訊。|網站伺服器|  
|colleval.log|記錄有關集合評估工具建立、變更和刪除集合時的詳細資料。|主要網站和管理中心網站|  
|Cloudusersync.log|記錄使用者的授權啟用。|具有服務連接點的電腦|  
|dataldr.log|記錄處理 MIF 檔案的相關資訊。|網站伺服器|  
|ddm.log|記錄探索資料管理員的活動。|網站伺服器|  
|distmgr.log|記錄有關內容發佈要求的詳細資訊。|頂層網站伺服器|  
|Dmpdownloader.log|記錄來自 Microsoft Intune 的下載詳細資料。|設有服務連接點的電腦|  
|Dmpuploader.log|記錄資料庫變更上傳到 Microsoft Intune 的詳細資料。|設有服務連接點的電腦|  
|hman.log|記錄有關訊息轉寄的資訊。|網站伺服器|  
|objreplmgr.log|記錄原則與指派的處理。|主要網站伺服器|  
|policypv.log|記錄所有原則的原則產生。|網站伺服器|  
|outgoingcontentmanager.log|記錄上傳至 Microsoft Intune 的內容。|具有服務連接點的電腦|  
|sitecomp.log|記錄服務連接點安裝的詳細資料。|網站伺服器|  
|SmsAdminUI.log|記錄 Configuration Manager 主控台活動。|執行 Configuration Manager 主控台的電腦|  
|SMSProv.log|SMS 提供者所執行的記錄活動。 Configuration Manager 主控台活動會使用 SMS 提供者。|SMS 提供者的電腦|  
|SrvBoot.log|記錄服務連接點安裝程式服務的詳細資料。|具有服務連接點的電腦|  
|statesys.log|記錄行動裝置管理訊息的處理。|主要網站和管理中心網站|  

###  <a name="a-namebkmksunaploga-software-updates"></a><a name="BKMK_SU_NAPLog"></a> 軟體更新  
 下表列出包含軟體更新相關資訊的記錄檔。  此外，某些詳細資料仍與網路存取保護相關，此為 System Center Configuration Manager 上已不再使用的功能。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|ccmcca.log|記錄有關處理以 Configuration Manager NAP 原則處理為基礎之相容性評估的詳細資料，並且包含處理相容性所需的每項軟體更新補救的詳細資料。|用戶端|  
|Ccmperf.log|記錄維護相關活動以及擷取用戶端效能計數器相關資料的活動。|用戶端|  
|PatchDownloader.log|記錄有關從更新來源將軟體更新下載至網站伺服器上目的地之程序的詳細資料。|裝載 Configuration Manager 主控台的電腦，下載會從該處起始|  
|PolicyEvaluator.log|記錄有關用戶端電腦上原則評估的詳細資料，包括來自軟體更新的原則。|用戶端|  
|RebootCoordinator.log|記錄有關協調軟體更新安裝後，用戶端電腦上系統重新啟動的詳細資料。|用戶端|  
|ScanAgent.log|記錄有關軟體更新、WSUS 位置及相關動作之掃描要求的詳細資料。|用戶端|  
|SdmAgent.log|記錄有關追蹤補救和相容性的詳細資料。 不過，軟體更新記錄檔 Updateshandler.log 提供有關安裝相容性所需軟體更新之更具參考價值的詳細資料。<br /><br /> 此記錄檔會與相容性設定共用。|用戶端|  
|ServiceWindowManager.log|記錄有關評估維護期間的詳細資料。|用戶端|  
|smssha.log|Configuration Manager 網路存取保護用戶端的主要記錄檔，且其包含來自兩個 Configuration Manager 元件的健全狀況資訊合併聲明：定位服務 (LS) 及設定相容性代理程式 (CCA)。 此記錄檔也會包含 Configuration Manager 系統健康情況代理程式與作業系統 NAP 代理程式之間，以及 Configuration Manager 系統健康情況代理程式與設定相容性代理程式和定位服務這兩者之間互動的相關資訊。 它提供有關 NAP 代理程式是否成功初始化、健全狀況資料聲明及健全狀況回應聲明的資訊。|用戶端|  
|Smsshv.log|這是系統健全狀況驗證程式點的主要記錄檔，其中會記錄系統健全狀況驗證程式服務的基本操作，包括初始化進度。|網站系統伺服器|  
|Smsshvadcacheclient.log|記錄有關從 Active Directory 網域服務擷取 Configuration Manager 健全狀況狀態參照的詳細資料。|網站系統伺服器|  
|SmsSHVCacheStore.log|記錄有關用來保存從 Active Directory 網域服務擷取的 Configuration Manager NAP 健全狀況狀態參照之快取存放區的詳細資料，例如從存放區讀取，以及清除本機快取存放區檔案中的項目。 快取存放區無法設定。|網站系統伺服器|  
|smsSHVQuarValidator.log|記錄用戶端的健全狀況資訊聲明和處理操作。 若要取得完整資訊，請將下列位置中的登錄機碼 **LogLevel** 從 1 變更為 0：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMSSHV\Logging\\@GLOBAL**|網站系統伺服器|  
|smsshvregistrysettings.log|記錄服務正在執行時，對系統健全狀況驗證程式元件設定的任何動態變更。|網站系統伺服器|  
|SMSSHVSetup.log|記錄安裝系統健全狀況驗證程式點的成功或失敗 (包含失敗原因) 資訊。|網站系統伺服器|  
|SmsWusHandler.log|記錄有關 Inventory Tool for Microsoft Updates 之掃描程序的詳細資料。|用戶端|  
|StateMessage.log|記錄有關所建立並傳送至管理點之軟體更新狀態訊息的詳細資料。|用戶端|  
|SUPSetup.log|記錄有關軟體更新點安裝的詳細資料。 當軟體更新點安裝完成時， **Installation was successful** 會寫入此記錄檔中。|網站系統伺服器|  
|UpdatesDeployment.log|記錄有關用戶端上部署的詳細資料，包括啟動、評估和強制執行軟體更新。 詳細資訊記錄會顯示與用戶端使用者介面互動的其他相關資訊。|用戶端|  
|UpdatesHandler.log|記錄有關軟體更新相容性掃描，以及在用戶端上下載和安裝軟體更新的詳細資料。|用戶端|  
|UpdatesStore.log|記錄有關相容性掃描週期期間所評估的軟體更新相容性狀態的詳細資料。|用戶端|  
|WCM.log|記錄有關軟體更新點設定與連線至 Windows Server Update Services (WSUS) 伺服器取得更新目錄、分類以及語言的詳細資料。|網站伺服器|  
|WSUSCtrl.log|記錄有關網站的設定、資料庫連線和 WSUS 伺服器健全狀況的詳細資料。|網站系統伺服器|  
|wsyncmgr.log|記錄有關軟體更新同步處理程序的詳細資料。|網站伺服器|  
|WUAHandler.log|記錄有關用戶端上 Windows Update 代理程式搜尋軟體更新時的詳細資料。|用戶端|  

###  <a name="a-namebkmkwolloga-wake-on-lan"></a><a name="BKMK_WOLLog"></a> 網路喚醒  
 下表列出包含網路喚醒相關資訊的記錄檔。  

> [!NOTE]  
>  如果您使用喚醒 Proxy 來補充網路喚醒，這項活動就會記錄在用戶端上。 例如，您可以參閱本主題之[用戶端作業](#BKMK_ClientOpLogs)一節中的 CcmExec.log 與 SleepAgent_&lt;網域\>@SYSTEM_0.log。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|記錄有關需要傳送喚醒封包給那一個用戶端，喚醒封包的數量以及重試喚醒封包的數量等詳細資料。|網站伺服器|  
|wolmgr.log|記錄有關喚醒程序的詳細資料，例如何時喚醒已設定為進行網路喚醒的部署。|網站伺服器|  

###  <a name="a-namebkmkwuloga-windows-update-agent"></a><a name="BKMK_WULog"></a> Windows Update 代理程式  
 下表列出包含與 Windows Update 代理程式相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|記錄有關 Windows Update 代理程式連接至 WSUS 伺服器並擷取軟體更新以進行相容性評估時，是否有代理程式元件的更新的詳細資料。|用戶端|  

###  <a name="a-namebkmkwsusloga-wsus-server"></a><a name="BKMK_WSUSLog"></a> WSUS 伺服器  
 下表列出包含與 WSUS 伺服器相關資訊的記錄檔。  

|記錄檔名稱|說明|含有記錄檔的電腦|  
|--------------|-----------------|----------------------------|  
|Change.log|記錄有關已變更 WSUS 伺服器資料庫資訊的詳細資料。|WSUS 伺服器|  
|SoftwareDistribution.log|記錄有關從已設定更新來源同步至 WSUS 伺服器資料庫的軟體更新詳細資料。|WSUS 伺服器|  



<!--HONumber=Nov16_HO1-->


