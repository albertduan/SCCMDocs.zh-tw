---
title: "備份和復原 | Microsoft Docs"
description: "了解如何在發生失敗或資料遺失時，使用 System Center Configuration Manager 備份和復原您的站台。"
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3aa9f2e4d3f7210981b5b84942485de11fe15cb2
ms.openlocfilehash: a7e052bc0e1c354b75a7f95afdd266ed742ce689

---

# <a name="backup-and-recovery"></a>備份與復原

*適用對象：System Center Configuration Manager (最新分支)*

準備備份和復原方法，以避免資料遺失。 對於 Configuration Manager 站台，備份和復原方法有助於在遺失最少資料的情況下更快復原站台和階層。 本主題中的章節可協助您備份站台，並在發生失敗或資料遺失時復原站台。  



- [備份 Configuration Manager 站台](#BKMK_SiteBackup)   

  - [備份維護工作](#BKMK_BackupMaintenanceTask)   

  - [使用 Data Protection Manager 備份網站資料庫](#BKMK_DPMBackup)   

  -  [封存備份快照](#BKMK_ArchivingBackupSnapshot)   

  -  [使用 AfterBackup.bat 檔案](#BKMK_UsingAfterBackup)   

  -  [增補的備份工作](#BKMK_SupplementalBackup)   

-  [復原 Configuration Manager 站台](#BKMK_RecoverSite)   

  -   [決定您的復原選項](#BKMK_DetermineRecoveryOptions)   

         -   [站台伺服器復原選項](#BKMK_SiteServerRecoveryOptions)   

         -   [網站資料庫復原選項](#BKMK_SiteDatabaseRecoveryOption)   

         -   [SQL Server 變更追蹤保留期間](#bkmk_SQLretention)   

         -   [重新初始化站台或全域資料的程序](#bkmk_reinit)   

         -   [網站資料庫復原案例](#BKMK_SiteDBRecoveryScenarios)  

  -   [自動站台復原指令碼檔案索引鍵](#BKMK_UnattendedSiteRecoveryKeys)  

  -   [復原後的工作](#BKMK_PostRecovery)  

  -   [復原次要站台](#BKMK_RecoverSecondarySite)  

-   [SMS 寫入器服務](#BKMK_SMSWriterService)  

> [!NOTE]  
>  若是使用 SQL Server AlwaysOn 可用性群組裝載站台資料庫，請依照[適用於 System Center Configuration Manager 之高可用性站台資料庫的 SQL Server AlwaysOn](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)主題之[使用 SQL Server AlwaysOn 可用性群組時的備份和復原變更](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#bkmk_BnR)一節所述，修改您的備份和復原計劃。  

##  <a name="a-namebkmksitebackupa-back-up-a-configuration-manager-site"></a><a name="BKMK_SiteBackup"></a> 備份 Configuration Manager 站台  
 Configuration Manager 提供的備份維護工作可以：  

-   依排程執行  

-   備份站台資料庫  

-   備份特定的登錄機碼  

-   備份特定的資料夾和檔案  

-   備份 **CD.Latest** 資料夾 (請參閱 [System Center Configuration Manager 的 CD.Latest 資料夾](../../core/servers/manage/the-cd.latest-folder.md))  

 規劃至少每隔 5 天執行預設站台備份工作。 這是因為 Configuration Manager 使用 5 天的 [SQL Server 變更追蹤保留期間](#bkmk_SQLretention)。  

 若要簡化備份程序，您可以建立 **AfterBackup.bat** 檔案，自動在順利執行備份維護工作後執行備份後動作。 AfterBackup.bat 檔案通常用來將備份快照封存到安全的位置。 您也可以使用 AfterBackup.bat 檔案將檔案複製到備份資料夾，並開始進行其他增補的備份工作。

使用下列各節可協助您建立 Configuration Manager 備份策略。  

> [!NOTE]  
>  Configuration Manager 可以從 Configuration Manager 備份維護工作，或從您使用其他程序建立的站台資料庫備份，來復原站台資料庫。 例如，您可以使用 Microsoft SQL Server 維護計畫建立的備份還原站台資料庫。 您可以從使用 System Center 2012 Data Protection Manager (DPM) 建立的備份還原站台資料庫。 如需詳細資訊，請參閱 [使用 Data Protection Manager 備份網站資料庫](#BKMK_DPMBackup)。  

###  <a name="a-namebkmkbackupmaintenancetaska-backup-maintenance-task"></a><a name="BKMK_BackupMaintenanceTask"></a> 備份維護工作  
 您可以藉由排程預先定義的「備份站台伺服器」維護工作，自動備份 Configuration Manager 站台。 您可以備份管理中心網站和主要網站，但不支援次要網站或網站系統伺服器的備份。 當 Configuration Manager 備份服務執行時，會依照備份控制檔案 (**&lt;ConfigMgrInstallationFolder\>\Inboxes\Smsbkup.box\Smsbkup.ctl**) 中定義的指示進行。 您可以修改備份控制檔案，以變更備份服務的行為。 站台備份狀態資訊會寫入至 **Smsbkup.log** 檔案。 此檔案會在您於「備份網站伺服器」維護工作內容中指定的目的地資料夾中建立。  


##### <a name="to-enable-the-site-backup-maintenance-task"></a>啟用網站備份維護工作  

1.  在 Configuration Manager 主控台中，開啟 [系統管理] > [站台設定]  

     \> [站台]。  

2.  選取您要啟用網站備份維護工作的網站。  

3.  在 [常用] 索引標籤的 [設定] 群組中，選擇 [站台維護工作]。  

4.  選擇 [備份站台伺服器]  >  [編輯]。  

5.  選擇 [啟用此工作] > [設定路徑] 以指定備份目的地。 下列選項可供您選擇：  

    > [!IMPORTANT]  
    >  若要預防備份檔案遭到竄改，請將檔案儲存在安全的位置。 最安全的備份路徑是本機磁碟機，您可以在資料夾上設定 NTFS 檔案系統權限。 Configuration Manager 不會加密儲存在備份路徑中的備份資料。  

    -   **用於站台資料和資料庫的站台伺服器本機磁碟機**：指定將站台和站台資料庫的備份檔案儲存在站台伺服器本機磁碟上指定的路徑。 您必須先建立本機資料夾才可以執行備份工作。   網站伺服器的本機系統帳戶必須擁有網站伺服器備份本機資料夾的 **寫入** NTFS 檔案系統權限。 電腦若是執行 SQL Server，其本機系統帳戶必須擁有網站資料庫備份資料夾的 **寫入** NTFS 權限。  

    -   **用於站台資料和資料庫的網路路徑 (UNC 名稱)**：指定將站台和站台資料庫的備份檔案儲存在指定的 UNC 路徑。 您必須先建立共用才可以執行備份工作。站台伺服器的電腦帳戶和 SQL Server 的電腦帳戶 (如果 SQL Server 安裝在其他電腦上) 必須擁有共用網路資料夾的 **寫入** NTFS 和共用權限。  

    -   **站台伺服器和 SQL Server 上的本機磁碟機**：指定將站台的備份檔案儲存在站台伺服器本機磁碟機上指定的路徑，並將站台資料庫的備份檔案儲存在站台資料庫伺服器本機磁碟機上指定的路徑。 您必須先建立本機資料夾才可以執行備份工作。 網站伺服器的電腦帳戶必須擁有您在網站伺服器上建立之資料夾的 **寫入** NTFS 權限。 SQL Server 的電腦帳戶必須擁有您在網站資料庫伺服器上建立之資料夾的 **寫入** NTFS 權限。 此選項僅在網站伺服器上未安裝網站資料庫時適用。  

    > [!NOTE]  
    >    - 只有在您指定備份目的地的 UNC 路徑時才可以使用瀏覽備份目的地的選項。

    > - 用於不支援使用 Unicode 字元之備份目的地的資料夾名稱或共用名稱。  


6.  為站台備份工作設定排程。 基於最佳作法，請考慮將備份排程在非工作時間執行。 如果您有階層，請考慮將排程設在一週至少執行二次，以確保在發生網站失敗時可以保留較多的資料。  

    當您在與設定備份相同的站台伺服器上執行 Configuration Manager 主控台時，「備份站台伺服器」維護工作會使用當地時間進行排程。 當您從來自設定要進行備份的遠端站台電腦執行 Configuration Manager 主控台時，「備份站台伺服器」維護工作會使用 UTC 進行排程。  

7.  選擇是否要在站台備份工作失敗時建立警示，按一下 [確定]，再按一下 [確定]。 選取時，Configuration Manager 會建立備份失敗的重大警示，您可以在 [監視] 工作區的 [警示] 節點中檢閱該警示的內容。  

 接下來，確認「備份站台伺服器」維護工作正在執行，以確定備份已建立。  

##### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>確認備份站台伺服器維護工作正在執行  

-   藉由檢閱下列任一項，確認「站台備份」維護工作正在執行：  

    -   檢查此工作所建立備份目的地資料夾中檔案的時間戳記。 確認時間戳記的時間已更新為符合此工作上次排程執行的時間。  

    -   在 [監視]  工作區的 [元件狀態]  節點中，檢閱 SMS_SITE_BACKUP 的狀態訊息。 當網站備份順利完成時，您會看到訊息識別碼 5035，表示網站備份已順利完成且沒有發生錯誤。  

    -   當「備份網站伺服器」維護工作設定為在備份失敗時建立警示時，您可以在 [監視]  工作區的 [警示]  節點中檢查備份失敗的內容。  

    -   在 &lt;*ConfigMgrInstallationFolder*>\Logs 中，查看 Smsbkup.log 中的警示及錯誤。 當網站備份順利完成時，您會看到含有時戳的 `Backup completed` ，以及訊息識別碼 `STATMSG: ID=5035`。  

    > [!TIP]  
    >  當備份維護工作失敗時，您可以藉由停止再重新啟動 SMS_SITE_BACKUP 服務，重新啟動備份工作。  

###  <a name="a-namebkmkdpmbackupa-using-data-protection-manager-to-back-up-your-site-database"></a><a name="BKMK_DPMBackup"></a> 使用 Data Protection Manager 備份網站資料庫  
 您可以使用 System Center 2012 Data Protection Manager (DPM) 來備份站台資料庫。 您必須在網站資料庫電腦的 DPM 中建立新的保護群組。 在 [建立新保護群組精靈] 的 [選擇群組成員]  頁面上，您可以從資料來源清單選取 SMS 寫入器服務，然後選取網站資料庫作為適當的成員。 如需使用 DPM 備份網站資料庫的詳細資訊，請參閱 TechNet 上的 [Data Protection Manager Documentation Library (Data Protection Manager 文件庫)](http://go.microsoft.com/fwlink/?LinkId=272772) 。  

> [!IMPORTANT]  
>  Configuration Manager 不支援為使用具名執行個體的 SQL Server 叢集執行 DPM 備份，但支援在使用 SQL Server 預設執行個體的 SQL Server 叢集上執行 DPM 備份。  

 在您還原網站資料庫後，請依照安裝程式中的步驟還原網站。 選取 [使用手動復原的站台資料庫] 復原選項，以使用您透過 Data Protection Manager 復原的站台資料庫。  

###  <a name="a-namebkmkarchivingbackupsnapshota-archiving-the-backup-snapshot"></a><a name="BKMK_ArchivingBackupSnapshot"></a> 封存備份快照  
 第一次執行「備份網站伺服器」維護工作時，它會建立一個備份快照，您可以在發生失敗時使用這個備份快照復原您的網站。 當備份工作在後續的週期中再次執行時，它會建立新的備份快照，並使用該備份快照覆寫先前的快照。 因此網站只有一個備份快照，您無法擷取舊版的備份快照。  

 作為最佳作法，請針對以下原因保留多個備份快照封存：  

-   備份媒體失敗、錯置，或僅包含部分備份，都是常見狀況。 從過去的備份復原失敗的獨立主要網站總比完全沒有備份要來得好。 對於階層中的網站伺服器，備份必須是在 SQL Server 變更追蹤保留期間內，否則就不需要備份。  

-   有可能在數個備份週期中都偵測不到網站損毀。 您可能必須使用站台損毀前的備份快照。 這可套用至獨立主要站台以及其備份是在 SQL Server 變更追蹤保留期間內的階層中站台。  

-   例如，如果備份網站伺服器維護工作失敗，網站就可能完全沒有備份快照。 由於備份工作會在開始備份現有資料前將過去的備份快照全部移除，如此就會沒有有效的備份快照。  

###  <a name="a-namebkmkusingafterbackupa-using-the-afterbackupbat-file"></a><a name="BKMK_UsingAfterBackup"></a> 使用 AfterBackup.bat 檔案  
 順利備份站台之後，備份站台伺服器工作會自動嘗試執行名為 AfterBackup.bat 的檔案。 您必須在 &lt;*ConfigMgrInstallationFolder*>\Inboxes\Smsbkup 中手動建立 AfterBackup.bat 檔案。 如果 AfterBackup.bat 檔案存在，且儲存在正確的資料夾中，則會在備份工作完成後自動執行。 AfterBackup.bat 檔案可讓您在每次備份操作結束時封存備份快照，並自動執行其他非備份網站伺服器維護工作的備份後工作。 AfterBackup.bat 檔案會整合封存與備份操作，如此即可確保封存每個新的備份快照。 若 AfterBackup.bat 檔案不存在，則備份工作就會將其略過，而對於備份操作沒有任何影響。 若要確認網站備份工作是否已成功執行 AfterBackup.bat 檔，請參閱 [監視]  工作區內的 [元件狀態]  節點，並檢閱 SMS_SITE_BACKUP 的狀態訊息。 工作成功啟動 Afterbackup.bat 命令檔時，您會看見訊息 ID 5040。  

> [!TIP]  
>  若要建立 AfterBackup.bat 檔案以封存您的站台伺服器備份檔案，您必須使用批次檔中的複製命令工具，例如 Robocopy。 例如，您可以建立 AfterBackup.bat 檔，然後在第一行加入一些內容，如： `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`。 如需 Robocopy 的詳細資訊，請參閱 [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408) 命令列參照網頁。  

 雖然 AfterBackup.bat 的用途是封存備份快照，您也可以建立 AfterBackup.bat 檔，在每次備份操作結束時執行額外工作。  

###  <a name="a-namebkmksupplementalbackupa-supplemental-backup-tasks"></a><a name="BKMK_SupplementalBackup"></a> 增補的備份工作  
 備份網站伺服器維護工作為網站伺服器檔案和網站資料庫提供備份快照，但在您建立備份策略時，還有其他項目並未備份，這是必須納入考慮的。 使用下列各節可協助您完成 Configuration Manager 備份策略。  

#### <a name="back-up-custom-reporting-services-reports"></a>支持自訂 Reporting Services 報告  
 您已經修改預先定義或建立自訂的 Reporting Services 報告時，針對報告伺服器資料庫檔案建立備份也是備份策略中很重要的部分。 報告伺服器備份必須包含報告和模組、加密金鑰、自訂組件或延伸、設定檔案、自訂報告中所使用之自訂 SQL Server 檢視、自訂儲存程序等的來源檔備份。  

> [!IMPORTANT]  
>  Configuration Manager 升級到較新版本時，新報告可能會覆寫預先定義的報告。 如果您修改預先定義的報告，請先備份報告，然後在 Reporting Services 中還原。  

 如需備份 Reporting Services 中的自訂報告的詳細資訊，請參閱《SQL Server 2014 線上叢書》中的 [Reporting Services 安裝的備份與還原作業](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) 。  

#### <a name="backup-content-files"></a>備份內容檔  
 Configuration Manager 中的內容庫是儲存軟體更新、應用程式、作業系統部署等之所有內容檔案的位置。 內容庫位於站台伺服器和每個發佈點上。 備份網站伺服器維護工作並不包括內容庫或套件來源檔案的備份。 網站伺服器失敗時，內容庫檔案相關資訊會還原至網站資料庫，但您必須在網站伺服器上還原內容庫和套件來源檔案。  

-   **內容庫**：必須先還原內容庫，您才能將內容重新發佈至發佈點。 當您開始重新發佈內容時，Configuration Manager 會從站台伺服器的內容庫將檔案複製到發佈點。 站台伺服器的內容庫位於 SCCMContentLib 資料夾中，這個資料夾一般位於安裝站台時可用磁碟空間最大的磁碟機上。  

-   **封裝來源檔案**：必須先還原封裝來源檔案，您才能在發佈點上更新內容。 當您開始進行內容更新時，Configuration Manager 會從套件來源將新的或修改過的檔案複製到內容庫，接著將檔案複製到關聯的發佈點。 您可以在 SQL Server 中執行以下查詢，找出所有套件和應用程式的套件來源位置： `SELECT * FROM v_Package`。 您可以查看封裝識別碼的前三個字元，藉此識別封裝來源站台。 例如，如果封裝識別碼為 CEN00001，則來源站台的站台碼為 CEN。 當您還原套件來源檔案時，檔案必須還原到失敗前所在的相同位置。  

 確認您在網站伺服器的檔案系統備份中同時包含內容庫和套件來源位置。  

#### <a name="back-up-custom-software-updates"></a>備份自訂的軟體更新  
 System Center Updates Publisher 2011 是一種獨立工具，可讓您將自訂軟體更新發佈到 Windows Server Update Services (WSUS)、將軟體更新同步處理至 Configuration Manager、評估軟體更新合規性，以及將自訂軟體更新部署至用戶端。 Updates Publisher 會使用本機資料庫作為其軟體更新存放庫。 使用 Updates Publisher 管理自訂軟體更新時，需判斷您是否需要將 Updates Publisher 資料庫納入您的備份計畫中。 如需更新發行者的詳細資訊，請參閱 System Center TechCenter 文件庫中的 [System Center Updates Publisher 2011 (System Center 更新發行者 2011)](http://go.microsoft.com/fwlink/p/?LinkId=228726) 。  

 使用以下程序來備份 Updates Publisher 資料庫。  

###### <a name="to-back-up-the-updates-publisher-2011-database"></a>備份更新發行者 2011 資料庫  

1.  在執行 Updates Publisher 的電腦上，瀏覽至 %*使用者設定檔*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\ 中的 Updates Publisher 資料庫檔案 (Scupdb.sdf)。 每個執行 Updates Publisher 的使用者都有不同的資料庫檔案。  

2.  將資料庫檔案複製到備份目的地。 例如，若備份目的地是 E:\ConfigMgr_Backup，您可以將 Updates Publisher 資料庫檔案複製到 E:\ConfigMgr_Backup\SCUP2011。  

    > [!TIP]  
    >  電腦上有一個以上的資料庫檔案時，請考慮將檔案儲存於指出與資料庫檔案關聯之使用者設定檔的子資料夾中。 例如，您可以在 E:\ConfigMgr_Backup\SCUP2011\User1 中有一個資料庫檔案，而在 E:\ConfigMgr_Backup\SCUP2011\User2 中有另一個資料庫檔案。  

### <a name="user-state-migration-data"></a>使用者狀態移轉資料  
 您可以使用 Configuration Manager 工作順序來擷取和還原作業系統部署案例 (您想保留目前作業系統的使用者狀態) 中的使用者狀態資料。 儲存使用者狀態資料的資料夾會列在狀態移轉點的內容中。 此使用者狀態移轉資料並不會備份為網站伺服器備份維護工作的一部分。 作為您備份計畫的一部分，您必須手動備份所指定用來儲存使用者狀態移轉資料的資料夾。   

#### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>判斷用來儲存使用者狀態移轉資料的資料夾  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理] 工作區中，展開 [站台設定]，然後選擇 [伺服器和站台系統角色]。  

3.  選取裝載狀態移轉角色的站台系統，然後選擇 [站台系統角色] 中的 [狀態移轉點]。  


4.  在 [網站角色]  索引標籤的 [內容]  群組中，按一下 [內容] 。  
5.  儲存使用者狀態移轉資料的資料夾會列在 [一般]  索引標籤上的 [資料夾詳細資料]  區段中。  

## <a name="recover-a-configuration-manager-site"></a>復原 Configuration Manager 站台
 只要站台資料庫發生 Configuration Manager 站台失敗或資料遺失的狀況，就需要進行 Configuration Manager 站台復原。 修復和重新同步處理資料是網站復原的核心工作，也是避免操作中斷的必要手段。  

> [!IMPORTANT]  
>  當您復原站台的資料庫時：  

>  -   您必須使用相同的 SQL Server 版本。 例如，不支援將 SQL Server 2012 上執行的資料庫還原至 SQL Server 2014。 同樣地，不支援將 SQL Server 2014 Standard Edition 上執行的站台資料庫還原至 SQL Server 2014 Enterprise Edition。  
> -   SQL Server 絕不能設為 **單一使用者模式**。  
> -   確定 .MDF 和 .LDF 檔案有效。 復原站台時，未核取要還原的檔案狀態。  


 從 CD.Latest 資料夾執行 [Configuration Manager 安裝精靈]，以啟動站台復原。  您也可以設定自動安裝指令碼後使用安裝命令 **/script** 選項，從相同的 CD.Latest 資料夾中執行安裝。 您的復原選項會依您是否有 Configuration Manager 站台資料庫的備份而有所不同。 如需詳細資訊，請參閱 [System Center Configuration Manager 的 CD.Latest 資料夾](../../core/servers/manage/the-cd.latest-folder.md)。  

> [!IMPORTANT]  
>  如果您從站台伺服器的 [開始] 功能表執行 Configuration Manager 安裝程式，就無法使用 [復原站台] 選項。  

>  如果在進行備份之前，您已在 Configuration Manager 主控台內安裝任何更新，您可能無法順利從安裝媒體或 Configuration Manager 安裝路徑使用安裝程式來重新安裝站台。  

> [!NOTE]  
>  在您還原為資料庫複本設定的網站資料庫之後，必須先重新設定每個資料庫複本並重建發佈及訂閱，才能使用資料庫複本。  

###  <a name="a-namebkmkdeterminerecoveryoptionsa-determine-your-recovery-options"></a><a name="BKMK_DetermineRecoveryOptions"></a> 決定您的復原選項  
 針對 Configuration Manager 主要站台伺服器和管理中心網站復原，您需要考慮兩個主要區域：站台伺服器與站台資料庫。 使用以下區段，協助您決定必須為復原案例選取的選項。  

> [!NOTE]  

####  <a name="a-namebkmksiteserverrecoveryoptionsa-site-server-recovery-options"></a><a name="BKMK_SiteServerRecoveryOptions"></a> 站台伺服器復原選項  
 您必須從您在 Configuration Manager 安裝資料夾外部所建立的 CD.Latest 資料夾複本中啟動安裝程式。 然後選取 [復原站台]  選項。 執行安裝程式時，針對失敗的網站伺服器，您有以下復原選項：  

-   **使用現有備份復原站台伺服器**：如果您在站台失敗前，已於**備份站台伺服器**維護工作期間，在站台伺服器上建立了Configuration Manager 站台伺服器的備份，請使用此選項。 此時會重新安裝網站，並根據備份的網站來設定網站設定。  

-   **重新安裝站台伺服器**：若您沒有站台伺服器的備份，請使用此選項。 此時會重新安裝網站伺服器，且您必須指定網站設定，如同您進行初始安裝時一樣。 您必須使用失敗的網站第一次安裝時使用的相同網站碼和網站資料庫名稱，才能成功復原網站。  

> [!NOTE]  
>  安裝程式在伺服器上偵測到現有的 Configuration Manager 站台時，您就可以啟動站台復原，不過站台伺服器的復原選項有限。 例如，若您在現有網站伺服器上執行安裝程式，當您選擇復原時，就可以復原網站資料庫伺服器，但會停用復原網站伺服器的選項。  

####  <a name="a-namebkmksitedatabaserecoveryoptiona-site-database-recovery-options"></a><a name="BKMK_SiteDatabaseRecoveryOption"></a> 網站資料庫復原選項  
 執行安裝程式時，針對網站資料庫，您有以下復原選項：  

-   **使用備份組復原站台資料庫**：如果您在站台資料庫失敗前，已於站台上執行**備份站台伺服器**維護工作期間，建立了 Configuration Manager 站台資料庫的備份，請使用此選項。 若您有階層，則會從主要網站的管理中心網站，或管理中心網站的參照主要網站，擷取最後一次進行網站資料庫備份後，對網站資料庫所做的變更。 當您復原獨立主要網站的網站資料庫時，您會遺失最後一次備份後的網站變更。  

     當您復原階層中某個網站的網站資料庫時，管理中心網站與主要網站的復原行為不同，並且上次備份是在 SQL Server 變更追蹤保留期間內或保留期間外，復原行為也不一樣。 如需詳細資訊，請參閱本主題中的＜ [網站資料庫復原案例](#BKMK_SiteDBRecoveryScenarios) ＞一節。  

    > [!NOTE]  
    >  若您選取使用備份集來還原網站資料庫，但已經存在網站資料庫，則復原就會失敗。  

-   **為此站台建立新的資料庫**：若您沒有 Configuration Manager 站台資料庫的備份，請使用此選項。 您有階層時，會建立新的網站資料庫，使用從主要網站的管理中心網站或管理中心網站的參照主要網站的複寫資料，就會復原資料。 若您復原獨立主要網站或沒有主要網站的管理中心網站，就無法使用此選項。  

-   **使用手動復原的站台資料庫**：如果您已復原 Configuration Manager 站台資料庫，但必須完成復原程序，請使用此選項。 Configuration Manager 可以從 Configuration Manager 備份維護工作，或從您使用 DPM 或其他程序執行的站台資料庫備份，來復原站台資料庫。 在您使用 Configuration Manager 以外的方法復原站台資料庫後，您必須執行安裝程式，然後選取這個選項來完成站台資料庫復原。 若您有階層，則會從主要網站的管理中心網站，或管理中心網站的參照主要網站，擷取最後一次進行網站資料庫備份後，對網站資料庫所做的變更。 當您復原獨立主要網站的網站資料庫時，您會遺失最後一次備份後的網站變更。  

    > [!NOTE]  
    >  使用 DPM 備份站台資料庫時，在 Configuration Manager 中繼續還原程序前，請使用 DPM 程序將站台資料庫還原到指定的位置。 如需 DPM 的詳細資訊，請參閱 TechNet 上的 [Data Protection Manager Documentation Library (Data Protection Manager 文件庫)](http://go.microsoft.com/fwlink/?LinkId=272772) 。  

-   **略過資料庫復原**：若 Configuration Manager 站台資料庫伺服器上並沒出現資料遺失的狀況，請使用此選項。 只有在網站資料庫位於不同電腦而不是在您正在復原的網站伺服器上時，這個選項才有效。  

####  <a name="a-namebkmksqlretentiona-sql-server-change-tracking-retention-period"></a><a name="bkmk_SQLretention"></a> SQL Server 變更追蹤保留期間  
 變更追蹤會在 SQL Server 的網站資料庫中啟用。 變更追蹤可讓 Configuration Manager 查詢有關上次時間點後，資料庫資料表中已經出現之變更的資訊。 保留期間會指定保留變更追蹤資訊的時間長度。 根據預設，會將網站資料庫設定為 5 天的保留期間。 復原網站資料庫時，您的備份是在保留期間內或保留期間外，復原程序的進行方式也隨之不同。 例如，若網站資料庫伺服器失敗，而上次備份是 7 天以前，表示備份是在保留期間外。

 如需 SQL Server 變更追蹤本質的詳細資訊，請參閱來自 SQL Server 團隊的下列部落格︰[Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1) (變更追蹤清除 - 第 1 部分) 和 [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2) (變更追蹤清除 - 第 2 部分)。



####  <a name="a-namebkmkreinita-process-to-reinitialize-site-or-global-data"></a><a name="bkmk_reinit"></a> 重新初始化站台或全域資料的程序  
 重新初始化網站或全域資料的程序，會以來自另一個網站資料庫的資料取代網站資料庫中的現有資料。 例如，若網站 ABC 重新初始化來自網站 XYZ 的資料，會發生以下步驟：  

-   資料從網站 XYZ 複製到 ABC。  

-   網站 XYZ 的現有資料會從網站 ABC 上的網站資料庫中移除。  

-   從網站 XYZ 複製的資料會插入網站 ABC 的網站資料庫。  

##### <a name="example-scenario-1"></a>範例案例 1  
 **主要站台重新初始化來自管理中心網站的全域資料**：復原程序會從主要站台資料庫移除主要站台的現有全域資料，並以從管理中心網站複製的全域資料加以取代。  

##### <a name="example-scenario-2"></a>範例案例 2  
 **管理中心網站重新初始化來自主要站台的站台資料**：復原程序會從管理中心網站資料庫中移除該主要站台的現有站台資料，並以從主要站台複製的站台資料加以取代。 其他主要網站的網站資料則不受影響。  

####  <a name="a-namebkmksitedbrecoveryscenariosa-site-database-recovery-scenarios"></a><a name="BKMK_SiteDBRecoveryScenarios"></a> 網站資料庫復原案例  
 從備份還原站台資料庫後，Configuration Manager 會嘗試還原站台內上次資料庫備份後的變更以及全域資料。 下文說明從備份還原站台資料庫之後，Configuration Manager 會啟動的動作。  

 **復原的站台是管理中心網站：**  

-   **變更追蹤保留期間內的資料庫備份**  

    -   **全域資料：** 所有主要站台複寫備份之後全域資料中的變更。  

    -   **站台資料：** 從所有主要站台複寫備份之後站台資料中的變更。  

-   **比變更追蹤保留期間還舊的資料庫備份**  

    -   **全域資料：** 如有指定，管理中心網站會重新初始化參照主要站台的全域資料。 接著，所有其他主要網站會重新初始化來自管理中心網站的全域資料。 若沒有指定任何參照網站，則所有主要網站都會重新初始化來自管理中心網站的全域資料 (從備份還原的資料)。  

    -   **站台資料：** 管理中心網站會重新初始化每個主要站台的站台資料。  

 **復原的站台是主要站台：**  

-   **變更追蹤保留期間內的資料庫備份**  

    -   **全域資料：** 從管理中心站台複寫備份之後全域資料中的變更。  

    -   **站台資料：** 管理中心站台會重新初始化主要站台的站台資料。 備份後的變更會遺失，但把資訊傳送到主要網站的用戶端會重新產生大部分的資料。  

-   **比變更追蹤保留期間還舊的資料庫備份**  

    -   **全域資料：** 主要站台會重新初始化管理中心站台的全域資料。  

    -   **站台資料：** 管理中心站台會重新初始化主要站台的站台資料。 備份後的變更會遺失，但把資訊傳送到主要網站的用戶端會重新產生大部分的資料。  

### <a name="site-recovery-procedures"></a>網站復原程序  
 使用以下其中一種程序來協助您復原網站伺服器和網站資料庫。  

##### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>在安裝精靈中啟動網站復原  

1.  將 CD.Latest 資料夾複製到 Configuration Manager 安裝資料夾外部的位置 (請參閱 [System Center Configuration Manager 的 CD.Latest 資料夾](../../core/servers/manage/the-cd.latest-folder.md))。  

     從 CD.Latest 資料夾的複本執行 [Configuration Manager 安裝精靈]。  

2.  在 [開始使用]  頁面上，選取 [復原網站] ，然後按 [下一步] 。  

3.  使用適合復原網站的選項來完成精靈。  

    > [!IMPORTANT]  
    >  在復原期間，安裝程式會識別 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 在復原期間，請勿變更此連接埠設定，否則在復原完成後，會無法正常執行資料複寫。  

    > [!NOTE]  
    >  您可以在 [安裝精靈] 指定用於 Configuration Manager 安裝的原始或新路徑。  

##### <a name="to-start-an-unattended-site-recovery"></a>啟動自動網站復原  

1.  針對復原網站時所需的選項，準備自動安裝指令碼。  

2.  使用命令 **/script** 選項執行 Configuration Manager 安裝程式。 例如，若您將安裝程式初始設定檔命名為 ConfigMgrUnattend.ini，並儲存在您要執行安裝程式之電腦的 C:\Temp 目錄中，則命令如下所示： **Setup /script C:\temp\ConfigMgrUnattend.ini**。  

> [!NOTE]  
>  復原管理中心網站後，可能無法建立某些從子站台複寫過來的站台資料。 這可能包括硬體清查、軟體清查和狀態訊息。  
>   
>  如果發生這種情況，您必須為資料庫複寫重新初始化 **ConfigMgrDRSSiteQueue** 。  若要這樣做，請使用 **SQL Server Manager** 在管理中心網站的 Configuration Manager 站台資料庫上執行下列查詢：  
>   
>  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**  
>   
>  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**  

###  <a name="a-namebkmkunattendedsiterecoverykeysa-unattended-site-recovery-script-file-keys"></a><a name="BKMK_UnattendedSiteRecoveryKeys"></a> 自動站台復原指令碼檔案索引鍵  
 若要執行 Configuration Manager 管理中心網站或主要站台的自動復原，您可以建立自動安裝指令碼，並使用安裝程式搭配 /script 命令選項。 指令碼提供與安裝精靈提示相同的資訊類型，不過沒有預設設定。 所有值必須針對適用於您所使用之復原類型的安裝識別碼進行指定。  

 您可以藉由使用含有 /script 安裝命令列選項的初始設定檔案，自動執行 Configuration Manager 安裝程式。 Configuration Manager 管理中心網站與主要站台的復原支援自動安裝。 若要使用 /script 安裝命令列選項，您必須建立初始設定檔案，並在 /script 安裝命令列選項後指定初始設定檔案名稱。 檔案名稱並不重要，只要檔案名稱的副檔名為 .ini 即可。 當您參照來自命令列的安裝初始設定檔案時，您必須提供檔案的完整路徑。 例如，若您將安裝初始設定檔案命名為 setup.ini，並儲存於 C:\setup 資料夾，則命令列為：  

 **setup /script c:\setup\setup.ini**。  

> [!IMPORTANT]  
>  您必須具有系統管理員權限才能執行安裝程式。 使用自動指令碼執行安裝程式時，請使用 [以系統管理員身分執行] ，在 [系統管理員] 內容中啟動 [命令提示字元]。  

 指令碼包含區段名稱、索引鍵名稱與值。 根據您進行指令碼處理時的復原類型，所需的區段索引鍵名稱也不同。 區段中索引鍵的順序與檔案內區段的順序都不重要。 索引鍵不區分大小寫。 提供索引鍵的值時，索引鍵名稱後必須加上等號 (=) 與索引鍵的值。  

 使用以下區段來協助您建立自動網站復原的指令碼。 下表列出可用的安裝指令碼索引鍵、其對應的值、是否為必要、用於何種安裝類型，以及該索引鍵的簡單說明。  

#### <a name="recover-a-central-administration-site-unattended"></a>自動復原管理中心網站  
 使用下列資訊設定自動安裝指令碼檔案來復原管理中心網站。  

 **識別**  

-   **索引鍵名稱：** Action  

    -   **必要︰** 是  

    -   **值：** RecoverCCAR  

    -   **詳細資料︰** 復原管理中心站台  

**RecoveryOptions**  

-   **索引鍵名稱：** ServerRecoveryOptions  

    -   **必要︰** 是  

    -   **值︰** 1、2 或 4  

         1 = 復原網站伺服器和 SQL Server。  

         2 = 僅復原網站伺服器。  

         4 = 僅復原 SQL Server。  

    -   **詳細資料：** 指定安裝程式只要復原站台伺服器、SQL Server 或同時復原兩者。 針對 ServerRecoveryOptions 設定以下值時，需要關聯的索引鍵：  

        -   **值 = 1** ：您可以選擇為 **SiteServerBackupLocation** 索引鍵指定值，以使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

             將 **DatabaseRecoveryOptions** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原網站資料庫。  

        -   **值 = 2** ：您可以選擇為 **SiteServerBackupLocation** 索引鍵指定值，以使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

        -   **值 = 4** 將 **BackupLocation** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原網站資料庫。  

-   **索引鍵名稱：** DatabaseRecoveryOptions  

    -   **必要：** 可能  

    -   **值︰** 10、20、40、80  

         10 = 從備份還原網站資料庫。  

         20 = 使用以另一種方式手動復原的網站資料庫。  

         40 = 為網站建立新的資料庫。 若無可用網站資料庫備份，請使用此選項。 透過從其他網站複寫來復原全域和網站資料。  

         80 = 略過資料庫復原。  

    -   **詳細資料：** 指定安裝程式如何復原 SQL Server 中的站台資料庫。 **ServerRecoveryOptions** 設定值為 **1** 或 **4**時，需要此索引鍵。  

-   **索引鍵名稱：** ReferenceSite  

    -   **必要：** 可能  

    -   **值：**&lt;ReferenceSiteFQDN\>  

    -   **詳細資料︰** 若資料庫備份比變更追蹤保留期間還舊，或未使用備份復原站台，請指定管理中心所使用的參照主要站台來復原全域資料。  

         若沒有指定參照網站，且備份又比變更追蹤保留期間還舊，所有主要網站都會以來自管理中心網站的還原資料重新初始化。  

         若您並未指定參照網站，且備份是在變更追蹤保留期間內，則只會從主要網站複寫備份後的變更。 若不同主要網站間的變更發生衝突，則管理中心網站會使用第一個收到的變更。  

         **DatabaseRecoveryOptions** 設定值為 **40**時，需要此索引鍵。  

-   **索引鍵名稱：** SiteServerBackupLocation  

    -   **必要：** 否  

    -   **值：**&lt;PathToSiteServerBackupSet\>  

    -   **詳細資料︰** 指定站台伺服器備份集的路徑。 **ServerRecoveryOptions** 設定值為 **1** 或 **2**時，可選擇是否要使用此索引鍵。 指定 **SiteServerBackupLocation** 索引鍵值，藉此使用網站備份來復原網站。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

-   **索引鍵名稱：** BackupLocation  

    -   **必要：** 可能  

    -   **值：**&lt;PathToSiteDatabaseBackupSet\>  

    -   **詳細資料：** 指定站台資料庫備份集的路徑。 **ServerRecoveryOptions** 索引鍵的設定值為 **1** 或 **4** ，且 **DatabaseRecoveryOptions** 索引鍵的設定值為 **10** 時，需要 **BackupLocation** 索引鍵。  

**選項**  

-   **索引鍵名稱︰** ProductID  

    -   **必要︰** 是  

    -   **值：**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         評估版  

    -   **詳細資料：**Configuration Manager 安裝的產品金鑰，含破折號。 輸入 **Eval** 可安裝 Configuration Manager 的評估版。  

-   **索引鍵名稱：** SiteCode  

    -   **必要︰** 是  

    -   **值︰**&lt;站台碼\>  

    -   **詳細資料：** 三個英數字元，專門用於識別您階階層中的該站台。 您必須指定失敗前網站所使用的網站碼。  

-   **索引鍵名稱：** SiteName  

    -   **必要︰** 是  

    -   **值：** SiteName  

    -   **詳細資料︰** 此站台的描述。  

-   **索引鍵名稱：** SMSInstallDir  

    -   **必要︰** 是  

    -   **值︰**&lt;onfiguraton Manager 安裝路徑*C*>  

    -   **詳細資料：**指定 Configuration Manager 程式檔案的安裝資料夾。  

        > [!NOTE]  
        >  您可以指定用於 Configuration Manager 安裝的原始路徑或新路徑。  

-   **索引鍵名稱：** SDKServer  

    -   **必要︰** 是  

    -   **值：**&lt;SMS 提供者的FQDN>  

    -   **詳細資料：** 指定將裝載 SMS 提供者的伺服器 FQDN。 您必須指定失敗前裝載 SMS 提供者的伺服器。  

         您可以在初始安裝後設定站台的其他 SMS 提供者。  

-   **索引鍵名稱︰** PrerequisiteComp  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 下載  

         1 = 已下載  

    -   **詳細資料：** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 0 值，安裝程式會下載檔案。  

-   **索引鍵名稱︰** PrerequisitePath  

    -   **必要︰** 是  

    -   **值：** &lt;安裝路必要條件檔案>  

    -   **詳細資料：** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑儲存下載的檔案或尋找之前下載的檔案。  

-   **索引鍵名稱：** AdminConsole  

    -   **必要：** 可能  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定是否安裝 Configuration Manager 主控台。 此索引鍵為必要，除非 **ServerRecoveryOptions** 設定的值為 **4**。  

-   **索引鍵名稱：** JoinCEIP  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **詳細資料：** 指定是否加入「客戶經驗改進計畫」。  

**SQLConfigOptions**  

-   **索引鍵名稱：** SQLServerName  

    -   **必要︰** 是  

    -   **值︰***&lt;SQLServerName\>*  

    -   **詳細資料：**執行要用於裝載站台資料庫之 SQL Server 的伺服器名稱或叢集執行個體名稱。 您必須指定失敗前裝載網站資料庫的相同伺服器。  

-   **索引鍵名稱：** DatabaseName  

    -   **必要︰** 是  

    -   **值：**  

         *&lt;SiteDatabaseName\>*  

         對話方塊中的 [動作]  

         *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*  

    -   **詳細資料：**指定要建立或用於安裝管理中心網站資料庫之 SQL Server 資料庫的名稱。 您必須指定失敗前所使用的相同資料庫名稱。  

        > [!IMPORTANT]  
        >  如果您未使用預設執行個體，則必須指定執行個體名稱及網站資料庫名稱。  

-   **索引鍵名稱：** SQLSSBPort  

    -   **必要：** 否  

    -   **值：** &lt;SSB 埠號>  

    -   **詳細資料：** 指定 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 通常 SSB 是設定為使用 TCP 連接埠 4022，但也支援其他連接埠。 您必須指定失敗前所使用的相同 SSB 連接埠。  

#### <a name="recover-a-primary-site-unattended"></a>自動復原主要網站  
 使用下列資訊設定自動安裝指令碼檔案來復原管理中心網站。  

 **識別**  

-   **索引鍵名稱：** Action  

    -   **必要︰** 是  

    -   **值︰** RecoverPrimarySite  

    -   **詳細資料︰** 復原主要站台  

**RecoveryOptions**  

-   **索引鍵名稱：** ServerRecoveryOptions  

    -   **必要︰** 是  

    -   **值︰** 1、2 或 4  

         1 = 復原網站伺服器和 SQL Server。  

         2 = 僅復原網站伺服器。  

         4 = 僅復原 SQL Server。  

    -   **詳細資料：** 指定安裝程式只要復原站台伺服器、SQL Server 或同時復原兩者。 針對 ServerRecoveryOptions 設定以下值時，需要關聯的索引鍵：  

        -   **值 = 1** ：您可以選擇為 **SiteServerBackupLocation** 索引鍵指定值，以使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

             將 **DatabaseRecoveryOptions** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原網站資料庫。  

        -   **值 = 2** ：您可以選擇為 **SiteServerBackupLocation** 索引鍵指定值，以使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

        -   **值 = 4** 將 **BackupLocation** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原網站資料庫。  

-   **索引鍵名稱：** DatabaseRecoveryOptions  

    -   **必要：** 可能  

    -   **值︰** 10、20、40、80  

         10 = 從備份還原網站資料庫。  

         20 = 使用以另一種方式手動復原的網站資料庫。  

         40 = 為網站建立新的資料庫。 若無可用網站資料庫備份，請使用此選項。 透過從其他網站複寫來復原全域和網站資料。  

         80 = 略過資料庫復原。  

    -   **詳細資料：** 指定安裝程式如何復原 SQL Server 中的站台資料庫。 **ServerRecoveryOptions** 設定值為 **1** 或 **4**時，需要此索引鍵。  

-   **索引鍵名稱：** SiteServerBackupLocation  

    -   **必要：** 否  

    -   **值：**&lt;PathToSiteServerBackupSet\>  

    -   **詳細資料︰** 指定站台伺服器備份集的路徑。 **ServerRecoveryOptions** 設定值為 **1** 或 **2**時，可選擇是否要使用此索引鍵。 指定 **SiteServerBackupLocation** 索引鍵值，藉此使用網站備份來復原網站。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

-   **索引鍵名稱：** BackupLocation  

    -   **必要：** 可能  

    -   **值：**&lt;PathToSiteDatabaseBackupSet\>  

    -   **詳細資料：** 指定站台資料庫備份集的路徑。 **ServerRecoveryOptions** 索引鍵的設定值為 **1** 或 **4** ，且 **DatabaseRecoveryOptions** 索引鍵的設定值為 **10** 時，需要 **BackupLocation** 索引鍵。  

**選項**  

-   **索引鍵名稱︰** ProductID  

    -   **必要︰** 是  

    -   **值：**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         評估版  

    -   **詳細資料：**Configuration Manager 安裝的產品金鑰，含破折號。 輸入 **Eval** 可安裝 Configuration Manager 的評估版。  

-   **索引鍵名稱：** SiteCode  

    -   **必要︰** 是  

    -   **值︰**&lt;站台碼\>  

    -   **詳細資料：** 三個英數字元，專門用於識別您階階層中的該站台。 您必須指定失敗前網站所使用的網站碼。  

-   **索引鍵名稱：** SiteName  

    -   **必要︰** 是  

    -   **值：** SiteName  

    -   **詳細資料︰** 此站台的描述。  

-   **索引鍵名稱：** SMSInstallDir  

    -   **必要︰** 是  

    -   **值︰**&lt;onfiguraton Manager 安裝路徑*C*>  

    -   **詳細資料：**指定 Configuration Manager 程式檔案的安裝資料夾。  

        > [!NOTE]  
        >  您可以指定用於 Configuration Manager 安裝的原始路徑或新路徑。  

-   **索引鍵名稱：** SDKServer  

    -   **必要︰** 是  

    -   **值：**&lt;SMS 提供者的FQDN>  

    -   **詳細資料：** 指定將裝載 SMS 提供者的伺服器 FQDN。 您必須指定失敗前裝載 SMS 提供者的伺服器。  

         您可以在初始安裝後設定站台的其他 SMS 提供者。  

-   **索引鍵名稱︰** PrerequisiteComp  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 下載  

         1 = 已下載  

    -   **詳細資料：** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 0 值，安裝程式會下載檔案。  

-   **索引鍵名稱︰** PrerequisitePath  

    -   **必要︰** 是  

    -   **值：** &lt;安裝路必要條件檔案>  

    -   **詳細資料：** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑儲存下載的檔案或尋找之前下載的檔案。  

-   **索引鍵名稱：** AdminConsole  

    -   **必要：** 可能  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定是否安裝 Configuration Manager 主控台。 此索引鍵為必要，除非 **ServerRecoveryOptions** 設定的值為 **4**。  

-   **索引鍵名稱：** JoinCEIP  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **詳細資料：** 指定是否加入「客戶經驗改進計畫」。  

**SQLConfigOptions**  

-   **索引鍵名稱：** SQLServerName  

    -   **必要︰** 是  

    -   **值︰***&lt;SQLServerName\>*  

    -   **詳細資料：**執行要用於裝載站台資料庫之 SQL Server 的伺服器名稱或叢集執行個體名稱。 您必須指定失敗前裝載網站資料庫的相同伺服器。  

-   **索引鍵名稱：** DatabaseName  

    -   **必要︰** 是  

    -   **值：**  

         *&lt;SiteDatabaseName\>*  

         對話方塊中的 [動作]  

         *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*  

    -   **詳細資料：**指定要建立或用於安裝管理中心網站資料庫之 SQL Server 資料庫的名稱。 您必須指定失敗前所使用的相同資料庫名稱。  

        > [!IMPORTANT]  
        >  如果您未使用預設執行個體，則必須指定執行個體名稱及網站資料庫名稱。  

-   **索引鍵名稱：** SQLSSBPort  

    -   **必要：** 否  

    -   **值：** &lt;SSB 埠號>  

    -   **詳細資料：** 指定 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 通常 SSB 是設定為使用 TCP 連接埠 4022，但也支援其他連接埠。 您必須指定失敗前所使用的相同 SSB 連接埠。  

**階層 ExpansionOption**  

-   **索引鍵名稱：** CCARSiteServer  

    -   **必要：** 可能  

    -   **值：**&lt;管理中心網站的站台碼>  

    -   **詳細資料︰**指定主要站台加入 Configuration Manager 階層時要連接的管理中心網站。 如果主要網站在失敗前連接至管理中心網站，則此設定為必要。 您必須指定失敗前用於管理中心網站的網站碼。  

-   **索引鍵名稱：** CASRetryInterval  

    -   **必要：** 否  

    -   **值︰**&lt;間隔>  

    -   **詳細資料：** 指定連線失敗後，嘗試連線至管理中心站台的重試間隔 (分鐘)。 例如，如果與管理中心網站的連線失敗，主要網站會等待您針對 CASRetryInterval 指定的分鐘數，然後重試連線。  

-   **索引鍵名稱：** WaitForCASTimeout  

    -   **必要：** 否  

    -   **值︰**&lt;逾時>  

    -   **詳細資料：** 指定主要站台連線至管理中心站台的逾時上限值 (分鐘)。 例如，如果主要網站連線至管理中心網站失敗，則主要網站會依據 CASRetryInterval 重試與管理中心網站的連線，直到達到 WaitForCASTimeout 期間。 您可以指定 0 到 100 的值。  

###  <a name="a-namebkmkpostrecoverya-post-recovery-tasks"></a><a name="BKMK_PostRecovery"></a> 復原後的工作  
 復原網站後，有幾項後續復原工作必須納入考量，網站復原才算完成。 利用下面各節可幫助您完成網站復原程序。  

#### <a name="re-enter-user-account-passwords"></a>重新輸入使用者帳戶密碼  
 網站伺服器復原後，必須重新輸入為網站所指定使用者帳戶的密碼，因為在網站復原期間會重設這些密碼。 網站復原完成後，帳戶會列在 [安裝精靈] 的 [已完成]  頁面上，並且儲存到已復原網站伺服器的 C:\ConfigMgrPostRecoveryActions.html。  

###### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>在網站復原後重新輸入使用者帳戶的密碼  

1.  開啟 Configuration Manager 主控台並連線至復原的站台。  

2.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

3.  在 [系統管理]  工作區中，展開 [安全性] ，然後按一下 [帳戶] 。  

4.  針對必須重新輸入其密碼的每個帳戶執行下列操作：  

    1.  從網站復原後識別的帳戶清單中選取帳戶。 您可以在已復原網站伺服器的 C:\ConfigMgrPostRecoveryActions.html 中找到此清單。  

    2.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容]  開啟帳戶內容。  

    3.  在 [一般]  索引標籤上按一下 [設定] ，然後重新輸入帳戶的密碼。  

    4.  按一下 [確認] ，為所選取使用者帳戶選取適當的資料來源，然後按一下 [測試連線]  確認使用者帳戶能夠連線至資料來源。  

    5.  按一下 [確定]  儲存密碼變更，然後按一下 [確定] 。  

#### <a name="re-enter-sideloading-keys"></a>重新輸入側載金鑰  
 網站伺服器復原後，您必須重新輸入指定給網站的 Windows 側載金鑰，因為在網站復原期間會重設這些金鑰。 重新輸入側載金鑰之後，Configuration Manager 主控台中 Windows 側載金鑰的 [已使用的啟用數量] 欄中的計數便會重設。 例如，假設在站台失敗前，您的 [啟用總數] 計數設為 [100]，而代表裝置已用金鑰數目的 [已使用的啟用數量] 是 [90]。 在網站復原之後，[啟用總數]  欄仍會顯示 [100] ，但是 [已使用的啟用數量]  欄會不正確地顯示 [0] 。 不過，在 10 個新裝置使用側載金鑰之後，就不會有任何剩餘的側載金鑰，因此下一個裝置將無法套用側載金鑰。  

#### <a name="recreate-the-microsoft-intune-subscription"></a>重新建立 Microsoft Intune 訂閱  
 如果在站台伺服器重新製作映像後才復原 Configuration Manager 站台伺服器，就不會還原 Microsoft Intune 訂閱。 您必須在復原站台後，重新連線到訂閱。  請不要建立新的 APN 要求，而改為上傳目前有效的 .pem，也就是上次設定或更新 iOS 管理所上傳的檔案。 如需詳細資訊，請參閱 [Configuring the Microsoft Intune subscription](../../mdm/deploy-use/setup-hybrid-mdm.md#step-3-configure-intune-subscription)。  

#### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>為使用 IIS 的網站系統角色設定 SSL  
 當您復原執行 IIS 且在失敗前設定為使用 HTTPS 的網站系統時，必須重新設定 IIS 使用 Web 伺服器憑證。  

#### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>重新安裝已復原網站伺服器中的 Hotfix  
 網站復原後，您必須重新安裝之前套用至網站伺服器的任何 Hotfix。 站台復原後，之前安裝的 Hotfix 清單會列在 [安裝精靈] 的 [已完成]  頁面上，並且儲存到已復原站台伺服器的 **C:\ConfigMgrPostRecoveryActions.html** 。  

#### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>復原執行 Reporting Services 之電腦上的自訂報告  
 當您已建立自訂 Reporting Services 報告，而 Reporting Services 失敗時，若您已備份報告伺服器，則可以復原報告。 如需還原 Reporting Services 中自訂報告的詳細資訊，請參閱《SQL Server 2008 線上叢書》中的 [Reporting Services 安裝的備份與還原作業](http://go.microsoft.com/fwlink/p/?LinkId=228724) 。  

#### <a name="recover-content-files"></a>復原內容檔案  
 網站資料庫包含內容檔案在網站伺服器上儲存位置的相關資訊，但是內容檔案不會隨備份或復原程序備份或還原。 若要完整復原內容檔案，您必須將內容庫及套件來源檔案還原至原始位置。 您可利用數種方法復原內容檔案，但是最簡單的方法是從網站伺服器的檔案系統備份還原檔案。  

 如果您沒有套件來源檔案的檔案系統備份，則必須手動複製或下載套件來源檔案，就如同初次建立套件一般。 您可以在 SQL Server 中執行以下查詢，找出所有套件和應用程式的套件來源位置： `SELECT * FROM v_Package`。 您可以查看封裝識別碼的前三個字元，藉此識別封裝來源站台。 例如，如果封裝識別碼為 CEN00001，則來源站台的站台碼為 CEN。 當您還原套件來源檔案時，檔案必須還原到失敗前所在的相同位置。  

 如果沒有包含內容庫的檔案系統備份，您可以選擇下列還原方式：  

-   **匯入預先設置的內容檔案**：如果您有 Configuration Manager 階層，則可以建立包含另一個位置的所有套件及應用程式的預先設置內容檔案，然後匯入預先設置的內容檔案，以便在站台伺服器上復原內容庫。  

-   **更新內容**：您對封裝或應用程式部署類型開始進行更新內容動作時，內容會從封裝來源複製到內容庫。 原始位置中必須有套件來源檔案，此動作才能成功完成。 您必須在每個套件及應用程式上執行此動作。  

#### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>在執行更新發行者的電腦上復原自定軟體更新  
 若備份計劃包含 Updates Publisher 資料庫檔案，一旦執行 Updates Publisher 的電腦發生故障，就可以復原該資料庫。 如需更新發行者的詳細資訊，請參閱 System Center TechCenter 文件庫中的 [System Center Updates Publisher 2011 (System Center 更新發行者 2011)](http://go.microsoft.com/fwlink/p/?LinkId=228726) 。  

 使用以下程序來還原 Updates Publisher 資料庫。  

###### <a name="to-restore-the-updates-publisher-2011-database"></a>還原更新發行者 2011 年資料庫  

1.  在復原的電腦上重新安裝 Updates Publisher。  

2.  將資料庫檔案 (Scupdb.sdf) 從備份目的地複製到執行 Updates Publisher 之電腦上的 %*使用者設定檔*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\。  

3.  如果電腦中有一位以上的使用者執行 Updates Publisher，必須將每個資料庫檔案複製到適當的使用者設定檔位置。  

#### <a name="user-state-migration-data"></a>使用者狀態移轉資料  
 指定用於儲存使用者狀態移轉資料的資料庫，作為狀態移轉點網站系統內容。 復原含使用者狀態移轉資料資料夾的伺服器後，必須將伺服器上的使用者狀態移轉資料手動還原至故障前儲存這些資料的資料夾。  

#### <a name="regenerate-the-certificates-for-distribution-points"></a>重新產生用於發佈點的憑證  
 還原站台後，distmgr.log 可能包含下列一或多個發佈點項目： **無法解密憑證 PFX 資料**。 此項目指出站台無法解密發佈點憑證資料。 若要解決此問題，您必須針對受影響的發佈點重新產生或重新匯入憑證。 這可利用 PowerShell Cmdlet [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) 加以完成。  

#### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>更新用於雲端發佈點的憑證  
 Configuration Manager 需要使用管理憑證讓站台伺服器與雲端發佈點通訊。 復原網站後，必須更新用於雲端發佈點的憑證。  

####  <a name="a-namebkmkrecoversecondarysitea-recover-a-secondary-site"></a><a name="BKMK_RecoverSecondarySite"></a> 復原次要站台  
 Configuration Manager 不支援次要站台的資料庫備份，但可透過重新安裝次要站台支援復原。 Configuration Manager 次要站台故障時，必須復原次要站台。 您可以從 Configuration Manager主控台的 [站台] 節點，使用 [復原次要站台] 動作來復原次要站台。 不同於管理中心網站或主要網站的復原，復原次要網站不會使用備份檔案，而是改為在已失敗的次要網站電腦上重新安裝次要網站檔案。 然後從父主要網站資料上重新初始化次要網站資料。 復原過程中，Configuration Manager 會驗證次要站台電腦上是否有內容庫，以及是否有適當的內容。 如果有適當的內容，次要網站會使用現有內容庫。 否則，若要復原已復原的次要網站內容庫，您需要重新發佈或預先設置該已復原網站的內容。 如果發佈點不在次要網站上，復原次要網站時可以不重新安裝發佈點。 復原次要網站後，網站會自動與發佈點同步。  

 您可以從 Configuration Manager 主控台的 [站台] 節點，使用 [顯示安裝狀態] 動作來確認次要站台復原的狀態。  

> [!IMPORTANT]  
>  您使用的電腦必須和故障電腦擁有相同的設定 (例如其 FQDN)，才能順利復原次要網站。 電腦也必須符合所有次要網站必要條件，而且必須設定適當的安全性權限。 此外，請使用先前在故障網站中使用的安裝路徑。  

> [!IMPORTANT]  
>  復原次要站台時，如果電腦中尚未安裝 SQL Server Express，Configuration Manager 不會進行安裝。 因此，復原次要網站前，您必須手動安裝 SQL Server Express 或 SQL Server。 您必須使用次要網站資料庫故障前所使用的 SQL Server 版本及相同的 SQL Server 執行個體。  

##  <a name="a-namebkmksmswriterservicea-sms-writer-service"></a><a name="BKMK_SMSWriterService"></a> SMS 寫入器服務  
 SMS 寫入器是一個服務，會在備份程序進行期間與磁碟區陰影複製服務 (VSS) 互動。 Configuration Manager 站台備份必須執行 SMS 寫入器服務才可以順利完成。  

### <a name="purpose"></a>目的  
 SMS 寫入器會登錄至 VSS 服務，並繫結至其介面和事件。 當 VSS 廣播事件或傳送特定通知到 SMS 寫入器時，SMS 寫入器會回應通知，並採取適當的動作。 SMS 寫入器會讀取位於 &lt;ConfigMgr 安裝路徑>\inboxes\smsbkup.box 的備份控制檔案 (smsbkup.ctl)，並決定所備份的檔案及資料。 SMS 寫入器會根據此資訊與來自 SMS 登錄機碼及子機碼的特定資料建立由各種元件組成的中繼資料。 它會在收到要求時將中繼資料傳送至 VSS。 VSS 接著會傳送中繼資料給提出要求的應用程式，即 Configuration Manager 備份管理員。 備份管理員會選取已備份的資料，並經由 VSS 將此資料傳送給 SMS 寫入器。 SMS 寫入器會採取適當的步驟來進行備份的準備。 稍後當 VSS 準備好建立快照時會傳送一個事件，此時 SMS 寫入器會停止所有 Configuration Manager 服務，並確定 Configuration Manager 活動在建立快照時已遭到凍結。 在快照建立完成後，SMS 寫入器會重新啟動服務和活動。  

 SMS 寫入器服務會自動進行安裝。 當 VSS 應用程式要求備份或還原時，SMS 寫入器必須處於執行中狀態。  

### <a name="writer-id"></a>寫入器 ID  
 SMS 寫入器的寫入器 ID 為：03ba67dd-dc6d-4729-a038-251f7018463b。  

### <a name="permissions"></a>權限  
 SMS 寫入器服務必須在本機系統帳號戶下執行。  

### <a name="volume-shadow-copy-service"></a>磁碟區陰影複製服務  
 VSS 是一組 COM API，其中實作了一個架構以允許進行磁碟區備份時系統上的應用程式仍能繼續寫入磁碟區。 VSS 提供一致的介面，可在磁碟上更新資料的使用者應用程式 (SMS 寫入器服務) 與備份應用程式 (備份管理員服務) 之間進行協調。 如需 VSS 的詳細資訊，請參閱 Windows Server TechCenter 中的 [Volume Shadow Copy Service (磁碟區陰影複製服務)](http://go.microsoft.com/fwlink/p/?LinkId=241968) 主題。  



<!--HONumber=Feb17_HO2-->


