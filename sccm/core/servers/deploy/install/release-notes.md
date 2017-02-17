---
title: "版本資訊 - Configuration Manager | Microsoft Docs"
description: "請參閱這些注意事項，以了解產品中尚未修正或 Microsoft 知識庫文章未涵蓋的緊急問題。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3743c80b0c2b5142f3a537ba3855ffd14794d42b
ms.openlocfilehash: 9e853c8fda236125717c3912f6f3cb02d6dd1058


---
# <a name="release-notes-for-system-center-configuration-manager"></a>Release notes for System Center Configuration Manager (System Center Configuration Manager 的版本資訊)

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 的產品版本資訊僅限於產品中尚未修正的緊急問題 (可透過主控台內更新)，或 Microsoft 知識庫文章中未詳述的緊急問題。  

 對於影響核心案例的已知問題，這項資訊顯示於 System Center Configuration Manager 文件庫中的線上產品文件中。  

> [!TIP]  
>  本主題包含 System Center Configuration Manager 最新分支的版本資訊。 若是 System Center Configuration Manager Technical Preview 版本，請參閱 [Technical Preview for System Center Configuration Manager](../../../../core/get-started/technical-preview.md) (System Center Configuration Manager 的 Technical Preview)。  

## <a name="setup-and-upgrade"></a>安裝與升級  

### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>安裝使用 1606 版的長期維護分支站台時，會安裝最新分支站台
當您使用 2016 年 10 月發行版的 1606 版基準媒體安裝長期維護分支 (LTSB) 站台時，安裝程式會改為安裝最新分支站台。 發生原因是未選取使用站台安裝來安裝服務連接點的選項。

 - 雖然不需要服務連接點，但是您必須在安裝程式期間選擇安裝它，才能安裝 LTSB 站台。

安裝程式完成之後，您可以解除安裝服務連接點。  不過，您必須擁有離線或線上模式的服務連接點才能提交遙測資料，並取得最新分支和 LTSB 站台的安全性更新。

如果您的站台安裝為最新分支站台，但您想要安裝 LTSB，則可以將站台解除安裝後，再重新安裝。 或者，您可以呼叫 [Microsoft 說明及支援](http://go.microsoft.com/fwlink/?LinkId=243064)以取得協助。  

若要確認安裝的分支，請在主控台的 [系統管理] > [站台設定] > [站台]，然後開啟 [階層設定]。 只有在站台執行 LTSB 時，才能使用將站台轉換為最新分支站台的選項。  

**因應措施：**  無。   





### <a name="the--sql-server-backup-model-in-use-by-configuration-manager-can-change-from-full-to-simple"></a>由 Configuration Manager 所使用的 SQL Server 備份模型可以從完整變更為簡易  
 當您升級至 System Center Configuration Manager 1511 版時，Configuration Manager 正在使用的 SQL Server 備份模型可以從完整變更為簡單。  

-   如果您搭配使用自訂 SQL Server 備份工作與完整備份模型 (而不是 Configuration Manager 的內建備份工作)，則升級可以將您的備份模型從完整變更為簡單。  

**因應措施**：升級至 1511 版之後，請檢閱 SQL Server 組態，並在必要時將它還原為完整。  

### <a name="when-you-add-a-service-window-to-a-new-site-server-service-windows-that-were---configured-for-another-site-server-are-deleted"></a>當您在新的站台伺服器中加入服務視窗時，就會刪除之前為另一部站台伺服器所設定的服務視窗  
 當您使用搭配 System Center Configuration Manager 版本 1511 的維護時段時，您只能為階層中的單一站台伺服器設定維護時段。 在一部伺服器上設定服務視窗之後，當您接著在第二部站台伺服器上設定服務視窗時，第一部站台伺服器上的服務視窗就會以無訊息方式刪除，且不提示任何警告或錯誤。  

**因應措施**：從 [Microsoft 知識庫文章 3142341](http://support.microsoft.com/kb/3142341)安裝 Hotfix。 當您安裝 System Center Configuration Manager 的 1602 更新時，也可解決此問題。  

### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>在 Configuration Manager 主控台 [更新與服務] 節點中，更新卡在「正在下載」狀態  
由線上服務連接點自動下載更新期間，更新可能會卡在「正在下載」狀態。 當更新下載卡住時，指示記錄檔中會顯示以下類似項目：  

DMPdownloader log：  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log：  

-   Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**因應措施**︰在站台伺服器上，修改下列登錄機碼以符合下列各項，然後重新啟動 SMS_Executive 服務，或等待下一個自動下載週期 (最多 24 小時)。  

-   **要編輯的機碼**：HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **狀態值**︰設為 **146944** (十進位) 或 **0x00023e00** (十六進位)  

### <a name="pre-release-features-introduced-in-system-center-configuration-manager-1602"></a>System Center Configuration Manager 1602 引進的發行前版本功能  

發行前版本功能會包含在產品內，以便在生產環境中進行早期測試，但不應視為生產環境就緒。  

從更新 1606 開始，您必須同意才能使用發行前版本功能。 如需詳細資訊，請參閱[使用發行前版本功能](../../../../core/servers/manage/install-in-console-updates.md)。

System Center Configuration Manager 1602 版引進了下列兩項發行前版本功能：  

-   System Center Configuration Manager 所管理電腦的條件式存取。 如需詳細資訊，請參閱[管理 System Center Configuration Manager 所管理之電腦對 O365 服務的存取](../../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)。
    - 安裝 1602 更新之後，功能類型會顯示為已發行，不過這是發行前功能。
    - 如果您接著從 1602 更新至 1606，功能類型會顯示為已發行，不過這仍是發行前功能。
    - 如果您從 1511 版直接更新至 1606，功能類型會顯示為發行前版本。


-   服務叢集感知集合。 如需詳細資訊，請參閱 [Capabilities in Technical Preview 1605 for System Center Configuration Manager](../../../../core/get-started/capabilities-in-technical-preview-1605.md) (System Center Configuration Manager 的 Technical Preview 1605 功能) 中的 [Service a server group](../../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups) (服務伺服器群組)。  




### <a name="recovery-options-for-a-secondary-site-are-not-available-in-the-console"></a>主控台不提供次要站台的復原選項  
次要站台復原失敗後，Configuration Manager 主控台可能不再提供 **[復原次要站台]** 選項。  

此問題會影響 System Center Configuration Manager 版本 1511 和 1602，在未來的更新中可望解決。  

**因應措施**︰使用下列方法之一來復原 (重新安裝) 次要站台︰  

-   使用 **Preinst.exe** 和 **/delsite** 命令移除次要站台，然後重新安裝次要站台。 如需 preinst.exe 的資訊，請參閱 [System Center Configuration Manager 的階層維護工具 (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)。  

-   執行下列指令碼啟動次要站台復原。 您可以在想要復原之次要站台的主要父站台資料庫上執行此指令碼︰  

    ```  
    declare @SiteCode NVARCHAR(3)=N'<replace with secondary site code>'   

    UPDATE Sites SET Status = 9  
                    , DetailedStatus = 3  
    FROM Sites WHERE SiteCode = @SiteCode  

    UPDATE SCP SET SCP.Value1 = 9  
                    , SCP.Value2 = N'3'  
    FROM SC_SiteDefinition_Property SCP INNER JOIN SC_SiteDefinition SC ON SC.SiteNumber = SCP.SiteNumber  
    WHERE SC.SiteCode = @SiteCode AND SCP.[Name] = N'Requested Status'  
  ```  

###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>使用來自 CD.Latest 資料夾的可轉散發檔案時，安裝程式會失敗，並顯示資訊清單驗證錯誤
當您透過為 1606 版建立的 CD.Latest 資料夾執行安裝程式，並使用 CD.Latest 資料夾隨附的可轉散發檔案時，安裝程式會失敗，而 Configuration Manager 安裝記錄檔中的錯誤如下︰

  - 錯誤：defaultcategories.dll 的檔案雜湊檢查失敗
  - 錯誤：資訊清單驗證失敗。 資訊清單版本有誤？

**因應措施：**請使用下列其中一種方法：
 - 在安裝期間，選擇從 Microsoft 下載最新的可轉散發檔案，而不使用 CD.Latest 資料夾隨附的可轉散發檔案。
 - 手動刪除 *cd.latest\redist\languagepack\zhh* 資料夾，然後再次執行安裝程式。

### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>服務連接工具在 SQL Server 位於遠端或停用共用記憶體時擲回例外狀況
從 1606 版開始，服務連接工具會在下列其中一項正確時產生例外狀況：  
 -  站台資料庫位於裝載服務連接點並使用非標準連接埠 (1433 以外的連接埠) 之電腦的遠端
 -  站台資料庫位於與服務連接點相同的伺服器上，但已停用 SQL 通訊協定**共用記憶體**

例外狀況與下列類似：
 - 未處理的例外狀況: System.Data.SqlClient.SqlException: 建立連接至 SQL Server 時，發生網路相關或執行個體特定的錯誤。找不到或無法存取伺服器。確認執行個體名稱是否正確，以及 SQL Server 是否設定為允許遠端連線。(提供者: 具名管道提供者，錯誤: 40 - 無法開啟 SQL Server 連線) --

**因應措施**︰使用工具期間，您必須修改裝載服務連接點之伺服器的登錄，以包含 SQL Server 連接埠的相關資訊︰

   1.   使用工具之前，請編輯下列登錄機碼，並將使用中連接埠號碼新增至 SQL Server 名稱︰
    - 機碼：HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - 值：&lt;SQL Server 名稱>
    - 新增：**,&lt;連接埠>**

    例如，若要將連接埠 *15001* 新增至名為 *testserver.test.net* 的伺服器，則產生的機碼會是：***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.   將連接埠新增至登錄之後，工具應該會正常運作。  

   3.   完成工具的使用之後，針對 **-connect** 和 **-import** 步驟，請將登錄機碼變更回原始值。  






## <a name="backup-and-recovery"></a>備份與復原
### <a name="pre-production-client-is-not-available-after-a-site-restore"></a>還原站台後就無法使用進入生產階段前的用戶端
在 1602 版，當您使用進入生產階段前用戶端，從備份還原階層的頂層站台時，還原站台之後就無法使用進入生產階段前用戶端版本。  

**因應措施︰**還原階層的頂層站台之後，您必須手動複製進入生產階段前用戶端檔案，讓 Configuration Manager 可以處理並還原它們，以使用︰
1. 在頂層站台伺服器電腦上，將 *&lt;CM_Install_Location\>\\Client* 資料夾的內容複製到 *&lt;CM_Install_Location\>\\StagingClient* 資料夾。

2. 建立名為 **client.acu** 的空白檔案，將此檔案複製或貼入站台伺服器的 *&lt;CM_Install_Location\>\\Inboxes\\hman.box* 資料夾。 (這個檔案可以是已重新命名的文字檔案，只要它不再有 txt 副檔名)。 將此檔案放入 hman.box 資料夾之後，站台伺服器上的階層管理員會啟動和處理用戶端檔案，並還原進入生產階段前用戶端檔案以供使用。

1606 版已解決此問題。


## <a name="client-deployment-and-upgrade"></a>用戶端部署和升級  

### <a name="expansion-to-central-administration-site-stops-automatic-client-upgrades"></a>擴充至管理中心網站會停止自動用戶端升級  
僅限在版本 1511 中，任何從主要站台擴充至管理中心網站的站台，都將無法執行自動用戶端升級。 當站台擴充時，用戶端升級套件上的授權站台並未正確設定為新的管理中心網站，這會讓自動用戶端升級無法順利運作。 這個問題只存在於版本 1511。 在版本 1602 及更新版本中，已經修正此問題。  

**因應措施：** 在管理中心網站資料庫上執行下列 SQL 指令碼。 在您執行指令碼後，自動用戶端升級應該就會開始正常執行。  

  ```  
  DECLARE @RootSite AS NVARCHAR(3)  
  DECLARE @SourceServer AS NVARCHAR(255)  
  DECLARE @FullClientPkgSource AS NVARCHAR(255)  
  DECLARE @UpgradePkgSource AS NVARCHAR(255)  

  SELECT @RootSite = SiteCode, @SourceServer = SiteServer  
  FROM sites  
  WHERE ISNULL(ReportToSite, N'') = N''  

  SELECT @FullClientPkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\Client'  
  SELECT @UpgradePkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\ClientUpgrade'  

  UPDATE SMSPackages_G  
  SET Source = @FullClientPkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT FullPackageID FROM ClientDeploymentSettings)  

  UPDATE SMSPackages_G  
  SET Source = @UpgradePkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT UpgradePackageID FROM ClientDeploymentSettings)  

  UPDATE ProgramOffers_G  
  SET SourceSite = @RootSite  
  WHERE OfferID IN  
      (SELECT UpgradeAdvertisementID FROM ClientDeploymentSettings)  
  ```  

## <a name="operating-system-deployment"></a>作業系統部署  

### <a name="issue-with-the-windows-adk-for-windows-10-version-1511"></a>Windows ADK for Windows 10 版本 1511 的問題  
如果您是透過使用 Windows ADK 10 版本 1511 之 Windows PE v.10.0.10586 開機映像的軟體中心執行工作順序，當電腦重新啟動為 Windows PE 時，只要「初始化硬體裝置」發生 **Windows PE 初始化失敗，錯誤碼 0x80220014** 的錯誤，工作順序會失敗。  

**因應措施**：使用原始的 Windows 10 ADK。 如需詳細資訊，請參閱下列 System Center Configuration Manager 小組部落格： [Issue with the Windows ADK for Windows 10](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx)  

### <a name="dynamic-application-installation-fails-during-task-sequence-which-successfully-completes"></a>工作順序順利完成時動態應用程式安裝失敗  
當您部署使用 [根據動態變數清單安裝應用程式] 選項的工作順序，而其中一個應用程式因為任何原因無法安裝時，工作順序仍會報告成功。 不論如何設定下列選項都會發生這種情況：  

-   **發生錯誤時仍繼續** (安裝應用程式步驟的 [選項] 索引標籤)  

-   **如果某個應用程式安裝失敗，繼續安裝清單中的其他應用程式** (安裝應用程式步驟的 [內容] 索引標籤)  

您可以檢視 smsts.log 判斷應用程式是否安裝失敗。  

**因應措施**：使用 **_TSAppInstallStatus** 變數作為工作順序後續步驟的條件，且若其中一個動態應用程式發生錯誤，則工作順序失敗的條件。  

### <a name="smb-might-not-work-properly-after-you-use-a-task-sequence-to-install-windows-10"></a>使用工作順序安裝 Windows 10 後，SMB 可能無法正常運作  
當您使用工作順序安裝 Windows 10 映像時，在安裝 Configuration Manager 用戶端之後 SMB 可能無法正常運作。 例如，下列工作順序步驟可能會失敗：  

-   當搭配狀態移轉點還原使用者狀態時  

-   連線到網路資料夾  

例如您仍然可以從 F8 系統管理員命令提示字元，針對電腦執行 PING 命令，但任何的 SMB 網路流量 (例如從命令提示字元執行 NET USE) 可能會失敗並出現錯誤 1231 - 無法連接網路位置。  

**因應措施**：  
在「設定 Windows 和 ConfigMgr」工作順序步驟之後，新增「執行命令行」工作順序步驟來停止，然後啟動「工作站服務」，如下所示：    
**net stop workstation /y &amp; net start workstation**  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>根據預設，服務計劃會建立大量重複的軟體更新群組和部署  
根據預設，「建立服務計劃」精靈目前會在每個軟體更新同步處理後執行。 每次執行精靈時，它會建立新的軟體更新群組和部署。 例如，如果您的軟體更新同步處理排程一天會執行多次，「建立服務計劃」精靈每天將會建立多個幾乎相同的軟體更新群組和部署。  

**因應措施**：    
在您建立服務計劃後，開啟服務計劃的屬性，移至 **[評估排程]** 索引標籤，選取 **[依排程執行規則]**，按一下 **[自訂]**並建立自訂排程。 例如，您可以每隔 60 天執行服務計劃。  

### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>向使用者顯示高風險部署對話方塊時，就不會顯示期限較早的後續高風險對話方塊。
建立高風險工作部署並將其部署給使用者之後，會向使用者顯示高風險對話方塊。 如果使用者未關閉對話方塊，您可以建立和部署期限比第一個高風險部署還要早的另一個高風險部署，除非使用者關閉原始對話方塊，否則他們接收不到更新的對話方塊。 在設定的期限，仍會執行部署。

**因應措施**：  
使用者必須關閉第一個高風險部署的對話方塊，才能查看下一個高風險部署的對話方塊。

## <a name="mobile-device-management"></a>行動裝置管理  

### <a name="cannot-create-an-enrollment-profile-on-a-primary-site"></a>主要站台無法建立註冊設定檔  
系統管理員無法在連線至主要站台的 System Center Configuration Manager 系統管理主控台中建立註冊設定檔。 嘗試註冊時，系統管理員會在 [註冊設定檔精靈] 中看到下列錯誤： 「DEP 權杖尚未更新。請上傳 DEP 權杖。」 即使將有效的 DEP 權杖上傳至管理中心網站，還是會發生這個錯誤。  

**因應措施**：在連線至管理中心網站的 System Center Configuration Manager 主控台中建立註冊設定檔。  

### <a name="dep-cannot-use-non-alpha-numeric-characters-in-enrollment-profiles"></a>DEP 無法在註冊設定檔中使用非英數字元  
啟用 DEP 時，在註冊設定檔的 [名稱] 、[描述] 、[部門]  和 [電話號碼]  等欄位中，與 Apple 裝置註冊設定檔 (DEP) 相關聯的註冊設定檔無法使用非英數字元。 在這些欄位中使用非英數字元可以建立註冊設定檔，但是設定檔無法上傳至 Apple。 Apple 伺服器不會提供任何錯誤訊息或警告，設定檔也不會部署至 DEP 管理的裝置。  

**因應措施**：無。

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>完整抹除會停用 RAM 小於 4 GB 的 Windows 10 裝置

在 RAM 小於 4 GB 的 Windows 10 RTM 裝置 (1511 前的版本) 上執行完整抹除，會導致裝置無法使用。 嘗試抹除裝置後，裝置無法啟動且停止回應。

**因應措施**︰請先確定 Windows 10 RTM 電腦至少有 4 GB 的 RAM 可用，再對裝置執行完整抹除。 若要檢視 Windows 10 裝置的版本號碼，請在命令提示字元中輸入 'winver'。 如果裝置已抹除且不再回應，請使用可開機的 Windows 10 USB 磁碟機啟動並復原裝置的存取。

### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>當使用者屬於兩個或多個部署了條款與條件原則的使用者集合時，使用者會看到多組相同的條款  

當系統管理員將一組條款部署到多個使用者集合，而某個使用者是多個這些集合的成員時，該使用者在開啟公司入口網站時就會看到多個相同的條款複本。  例如，如果使用者 SampleUser 是 CompanyEmployeesFTE 和 CompanyEmployeesNA 這兩個不同使用者集合的成員，且 CompanyEmployeesFTE 和 CompanyEmployeesNA 都部署了 CompanyTerms 條款與條件，則 SampleUser 在條款接受頁面上就會看到兩組相同的 CompanyTerms。 因為使用者只能接受或拒絕全部條款，所以不可能出現使用者這邊接受條款、那邊拒絕條款的這種模稜兩可的接受狀態。 條款和條件接受報表中，每位使用者的每組條款都只有一個資料列，因此報表中沒有任何錯誤。 唯一的影響是使用者會在接受頁面上看到兩組條款。  

**因應措施**：請確定每位使用者只包含在一個部署了條款的集合中。  

## <a name="reports-and-monitoring"></a>報告和監視  

### <a name="the-health-attestation-report-is-empty-even-though-health-attestation-data-was-previously-collected"></a>即使先前已收集健康情況證明資料，健康情況證明報告仍為空白  
當具有安全性角色 (包含 **健康情況證明** 權限群組的 **讀取** 權限) 的系統管理使用者檢視健康情況證明報告時，報告為空白且無法顯示資料。 這是因為健康情況證明報告中之資料的檢視權限是連結到 **使用者裝置親和性** 權限群組，而非健康情況證明權限群組。  

此問題會影響含有更新 1602 的 System Center Configuration Manager，並預期會在未來的更新中解決。  

**因應措施**︰指派包含 **使用者裝置親和性** 權限群組 **讀取** 權限的安全性群組給系統管理使用者。  

### <a name="conditional-access"></a>條件式存取  

#### <a name="the-same-user-collection-is-not-blocked-from-being-added-to-both-exempted-and-targeted-collections"></a>不會封鎖將相同的使用者集合同時新增到豁免及目標集合。  
這只會發生在您將同樣的 **使用者集合** 新增到 **[目標集合]** 頁面 **之前** ，先將它新增到 **[豁免集合]** 頁面時。  如果您先將 **使用者集合** 新增到 **[目標集合]** 頁面，然後嘗試將相同的 **使用者集合** 新增到 **[豁免集合]** 頁面，您應該會看到正常的封鎖訊息。  

此問題會影響含有更新 1602 之 System Center Configuration Manager 對 **Exchange 內部部署**的條件存取，並預期會在未來的更新中解決。  

**因應措施︰** 新增 **使用者集合** 到 **[目標集合]** 頁面，然後在 **[豁免集合]** 頁面上選取 **使用者集合** ，或確定您沒有將相同的 **使用者集合** 同時新增到目標與豁免集合。



<!--HONumber=Jan17_HO4-->


