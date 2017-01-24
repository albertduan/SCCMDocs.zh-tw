---
title: SQL Server AlwaysOn | Microsoft Docs
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 9d4d0c741418af29edc586a5d629fc61f86da426


---
# <a name="sql-server-alwayson-for-a-highly-available-site-database-for-system-center-configuration-manager"></a>適用於 System Center Configuration Manager 之高可用性站台資料庫的 SQL Server AlwaysOn

*適用於：System Center Configuration Manager (最新分支)*



 從 System Center Configuration Manager 1602 版開始，您可以使用 SQL Server [AlwaysOn 可用性群組](https://msdn.microsoft.com/library/hh510230\(v=sql.120\).aspx)於主要站台和管理中心網站裝載站台資料庫，以作為高可用性和災害復原方案。 可用性群組可以裝載在內部部署環境或 Microsoft Azure 中。  

 當您使用 Microsoft Azure 來裝載可用性群組時，您可以將「SQL Server AlwaysOn 可用性群組」與「Azure 可用性設定組」搭配使用，以進一步提升站台資料庫的可用性。 如需 Azure 可用性集合的詳細資訊，請參閱 [管理虛擬機器的可用性](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/)。  

 支援可用性群組的案例如下︰  

-   您可以將站台資料庫移至可用性群組的預設執行個體  

-   您可以新增或移除裝載站台資料庫的可用性群組複本成員  

-   您可以從可用性群組將站台資料庫移動至獨立 SQL Server 的預設或具名執行個體  


> [!NOTE]  
>  若要成功設定及使用可用性群組，您必須熟悉 SQL Server 和 SQL Server 可用性群組的設定。 本主題中的 System Center Configuration Manager 程序有賴於可在 SQL Server 文件庫中找到的其他文件和程序說明。  

 **搭配 Configuration Manager 使用 AlwaysOn 可用性群組時的已知的問題︰**  

-   **所有複本伺服器都需要在設定 Configuration Manager 使用可用性群組時，使用相同的檔案路徑︰**  

    -   在您執行 Configuration Manager 安裝程式，以將站台重新導向至使用可用性群組中的資料庫時，群組中的每部次要複本伺服器必須具有檔案路徑，該檔案路徑等同於用來裝載目前主要複本上站台資料庫檔案的檔案路徑。 如果相同的路徑不存在於次要複本上，安裝程式就無法將可用性群組執行個體作為站台資料庫的新位置加入。  

         此外，每個次要複本伺服器上，本機 SQL Server 服務帳戶必須有 **[完全控制]** 此資料夾的權限。  

         只有當您使用安裝程式來指定可用性群組中的資料庫執行個體時，次要複本伺服器才需要此檔案路徑。  在安裝程式完成使用可用性群組中之站台資料庫的變更之後，您可以從次要複本伺服器刪除不使用的路徑。  

         例如，請考慮下列案例：  

        -   建立使用三部 SQL Server 的可用性群組  

        -   您的主要複本伺服器是 SQL Server 2014 的全新安裝。  依預設，資料庫 .MDF 和 .LDF 檔案會儲存在 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA  

        -   您的兩個次要複本伺服器從舊版升級至 SQL Server 2014，並保留原始的檔案路徑來儲存下列資料庫檔案︰C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA  

        -   在您嘗試將站台資料庫移至這個可用性群組之前，您必須在每個次要複本伺服器上建立下列檔案路徑 (如果次要複本不會使用這個檔案位置)︰C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA (這是在主要複本上使用之路徑的複製)  

        -   之後，授與每個次要複本上的 SQL Server 服務帳戶在該伺服器上新建立之檔案位置的完全控制存取  

        -   現在，您可以成功執行 Configuration Manager 安裝程式，將站台導向使用可用性群組中的站台資料庫  

-   **執行安裝程式以導向使用可用性群組中的站台資料庫時，則可能會將類似下列的錯誤記錄在 configmgrsetup.log 中︰**  

    -   錯誤︰SQL Server 錯誤：[25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server] 無法更新資料庫 "CM_AAA"，因為資料庫處於唯讀狀態。   Configuration Manager 安裝程式 1/21/2016 4:54:59 PM  7344 (0x1CB0)  

     當安裝程式嘗試處理可用性群組之次要複本上的資料庫角色時，就會記錄這些錯誤。 您可以放心地忽略這些錯誤。
- **裝載其他可用性群組的 SQL 伺服器︰**

  安裝 1610 版之前，如果您使用可用性群組，然後執行 Configuration Manager 安裝程式或安裝 Configuration Manager 的更新，則裝載 Configuration Manager 可用性群組之 SQL Server 上每個其他可用性群組中的每個複本都必須具有下列設定：
    - **[手動容錯移轉]**
    - **[允許任何唯讀連線]**


##  <a name="a-namebkmkbnra-changes-for-backup-and-recovery-when-you-use-a-sql-server-alwayson-availability-group"></a><a name="bkmk_BnR"></a> 使用 SQL Server AlwaysOn 可用性群組時的備份和復原變更  
 **備份：**  

 當站台資料庫在可用性群組中執行時，您應該繼續執行內建的「備份站台」伺服器維護工作以備份一般 Configuration Manager 設定和檔案，但計劃不使用該備份所建立的 .MDF 或 .LDF 檔案。 取而代之的是，改為使用 SQL Server 來直接備份站台資料庫。  

 此外，由於資料庫的復原模式是設定為完整，因此您必須計劃監控和維護站台資料庫交易記錄檔的大小。  在完整復原模式下，必須等到建立資料庫或交易記錄檔的完整備份之後，才會強行寫入交易。 完整復原模式是使用可用性群組中站台資料庫的要求條件，並且是在您設定要與 Configuration Manager 搭配使用的群組時所設定。 如需 SQL Server 備份與還原的詳細資訊，請參閱 SQL Server 文件中的 [SQL Server 資料庫的備份與還原](https://msdn.microsoft.com/library/ms187048\(v=sql.120\).aspx) 。  

 **復原：**  

 進行站台復原時，只要其中一個可用性群組節點維持正常運作，您便可以使用 **[略過資料庫復原 (如果資料庫未受到影響，則使用此選項)]**站台復原選項。  

 不過，如果可用性群組的所有節點都已遺失，您就必須先重新建立可用性群組 (System Center Configuration Manager 無法重建或還原可用性節點)，才能復原站台。在使用還原的備份來重新建立群組並重新設定之後，您便可以使用 **[略過資料庫復原 (如果資料庫未受到影響，則使用此選項)]** 站台復原選項。  

 如需備份與復原的詳細資訊，請參閱 [Backup and recovery for System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md) (System Center Configuration Manager 中的備份和復原)。  

##  <a name="a-namebkmkcreatea-configure-an-availability-group-for-use-with-configuration-manager"></a><a name="bkmk_create"></a> 設定要與 Configuration Manager 搭配使用的可用性群組  
 在您開始下列程序前，請先熟悉完成這項設定所需的 SQL Server 程序，以及下列適用於您所設定要與 Configuration Manager 搭配使用之可用性群組的詳細資訊。  

 **與 System Center Configuration Manager 搭配使用的 AlwaysOn 可用性群組需求：**  

-   可用性群組中的每個節點 (或複本) 都必須執行 System Center Configuration Manager 所支援的 SQL Server 版本  

-   可用性群組必須有一個主要複本，而且最多可以有兩個同步次要複本  

-  在將資料庫加入可用性群組之後，您必須將主要複本容錯移轉到次要複本 (讓它成為新的主要複本)，並接著使用下列項目來設定資料庫︰
    - 啟用 Trustworthy︰等於 True
    - 啟用 Service Broker︰等於 True
    - 設定 dbowner︰等於 SA

    您可以執行下列指令碼以進行這些設定，其中 cm_ABC 是站台資料庫的名稱︰  

    >     USE master  
    >     ALTER DATABASE cm_ABC SET NEW_BROKER   
    >     ALTER DATABASE cm_ABC SET ENABLE_BROKER  
    >     ALTER DATABASE cm_ABC SET TRUSTWORTHY ON;  
    >     USE cm_ABC  
    >     EXEC sp_changedbowner 'sa'  
    >     Exec sp_configure 'max text repl size (B)', 2147483647
    >     reconfigure



-   可用性群組至少必須有一個 **可用性群組接聽程式**。  當您將 Configuration Manager 設定為使用可用性群組中的站台資料庫時，將會使用此接聽程式的虛擬名稱。 雖然一個可用性群組可以包含多個接聽程式，但是 Configuration Manager 只能使用一個接聽程式  

-   每個主要和次要複本都必須︰  
    - 設定為 **[允許任何唯讀連線]**
    - 使用 **[預設執行個體]**
    - 針對 **[手動容錯移轉]**做設定  

        > [!TIP]  
        >  設定為 [自動容錯移轉] 時，System Center Configuration Manager 支援使用可用性群組複本。 不過，當您執行安裝程式以指定使用可用性群組中的站台資料庫，以及當您安裝任何 Configuration Manager 更新 (不只是適用於站台資料庫的更新) 時，都必須設定「手動容錯移轉」。  

  **可用性群組的限制**
   - 可用性群組只支援站台資料庫，而不適用於軟體更新資料庫或報表資料庫   
   - 當您使用可用性群組時，您必須手動設定報告點以使用目前的主要複本，而不是可用性群組接聽程式。 如果主要複本容錯移轉至另一個複本，則必須將報告點重新設定為使用新的主要複本。  
   - 安裝更新之前 (像是 1606 版本)，請確定可用性群組設定為手動容錯移轉。 站台更新之後，您可以還原為自動容錯移轉。



 **設定和使用可用性群組時必須具備的權限︰**  

-   站台伺服器的電腦帳戶必須是具備可用性群組成員身分之每部電腦上的 **「本機系統管理員」** 群組成員。  

#### <a name="to-configure-an-availability-group-to-host-a-site-database"></a>設定可用性群組以裝載站台資料庫  

1.  使用下列命令來停止 Configuration Manager 站台：  
     **Preinst.exe /stopsite**  

     如需使用 Preinst.exe 的詳細資訊，請參閱 [System Center Configuration Manager 的階層維護工具 (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)。  

2.  將站台資料庫的備份模式從 **[簡單]** 變更為 **[完整]**。  

     請參閱 SQL Server 文件中的 [檢視或變更資料庫的復原模式](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) 。 (可用性群組僅支援 [完整] 模式)。  

3.  在將裝載群組之主要複本的伺服器上，使用 **[新增可用性群組精靈]** 來建立可用性群組。 在精靈中：  

    -   在 [選取資料庫] 頁面上，為您的 Configuration Manager 站台選取資料庫  

    -   在 **[指定複本]** 頁面上，設定︰  

        -   **複本**︰指定將裝載次要複本的伺服器  

        -   **接聽程式**︰指定 [接聽程式 DNS 名稱] 作為完整 DNS 名稱 (例如 **&lt;Listener_Server>.fabrikam.com**)。 當您設定 Configuration Manager 使用可用性群組中的資料庫時，將會使用此項目。

    -   在 **[選取初始資料同步處理]** 頁面上，選取 **[完整]**。 在精靈建立可用性群組之後，精靈會備份主要資料庫和交易記錄檔，然後在裝載次要複本的每部伺服器上還原它們。 如果您不使用此步驟，就必須將站台資料庫的複本還原到裝載次要複本的每部伺服器，然後手動將該資料庫加入群組中。  

    如需詳細資訊，請參閱 SQL Server 文件中的 [使用可用性群組精靈](https://msdn.microsoft.com/library/hh403415\(v=sql.120\).aspx) 。  

4.  設定可用性群組之後，請為主要複本上的站台資料庫設定 **TRUSTWORTHY** 屬性，然後 **[啟用 CLR 整合]**。 如需如何進行這些設定的資訊，請參閱 SQL Server 文件中的 [TRUSTWORTHY 資料庫屬性](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) 和  [啟用 CLR 整合](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx) 。  

5.  採取下列動作來設定可用性群組中的每個次要複本︰  

    1.  將目前的主要複本手動容錯移轉至次要複本。 請參閱 SQL Server 文件中的 [執行可用性群組的已規劃手動容錯移轉](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) 。  

    2.  為新主要複本上的資料庫設定 **TRUSTWORTHY** 屬性，然後 **[啟用 CLR 整合]**。  

6.  在所有複本都升級為主要複本且設定好資料庫之後，可用性群組即可與 Configuration Manager 搭配使用。  





##  <a name="a-namebkmkdirecta-move-a-site-database-to-an-availability-group"></a><a name="bkmk_direct"></a> 將站台資料庫移至可用性群組  
 您可以將先前安裝之站台的站台資料庫移至可用性群組。 您必須先建立可用性群組，然後設定可用性群組中作業的資料庫。  

 若要完成此程序，執行 Configuration Manager 安裝程式的使用者帳戶必須是具備可用性群組成員身分之每部電腦上的**本機系統管理員**群組成員。  

#### <a name="to-move-a-site-database-to-an-availability-group"></a>將站台資料庫移至可用性群組  

1.  從 **&lt;Configuration Manager 站台安裝資料夾\>\BIN\X64\setup.exe** 執行 [Configuration Manager 安裝程式]。  

2.  在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台] ，然後按 [下一步] 。  

3.  選取 **[修改 SQL Server 設定]** 選項，然後按一下 **[下一步]**。  

4.  為站台資料庫重新設定下列各項︰  

    -   **SQL Server 名稱** ：輸入建立可用性群組時所設定的可用性群組接聽程式虛擬名稱。 這個虛擬名稱應該是完整 DNS 名稱，例如 **&lt;endpointServer\>.fabrikam.com**  

    -   **執行個體：** 此值必須為空白以指定可用性群組之可用性群組接聽程式的預設執行個體。  如果目前的站台資料庫是安裝在具名執行個體上，該具名執行個體將會列出且必須清除  

    -   **資料庫︰** 保留顯示的名稱。 這是目前站台資料庫的名稱。  

5.  提供新資料庫位置的資訊之後，請使用您的一般程序和設定來完成安裝。  

##  <a name="a-namebkmkchangea-add-or-remove-members-of-an-active-availability-group"></a><a name="bkmk_change"></a> 新增或移除作用中可用性群組的成員  
 在 Configuration Manager 使用裝載在可用性群組中的站台資料庫之後，您可以移除複本成員或新增其他複本成員 (不要超過一個主要和兩個次要節點)。  

#### <a name="to-add-a-new-replica-member"></a>新增新的複本成員  

1.  新增新的伺服器作為可用性群組的次要複本。 請參閱 SQL Server 文件庫中的  [將次要複本加入至可用性群組 (SQL Server)](https://msdn.microsoft.com/library/hh213247\(v=sql.120\).aspx)。  

2.  藉由執行 **Preinst.exe /stopsite** 以停止 Configuration Manager 站台。請參閱 [System Center Configuration Manager 的階層維護工具 (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)。  

3.  設定每個次要複本。 針對可用性群組中的每個次要複本執行下列動作︰  

    1.  將主要複本手動容錯移轉至新的次要複本。 請參閱 SQL Server 文件中的 [執行可用性群組的已規劃手動容錯移轉](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) 。  

    2.  將新伺服器上的資料庫設定成 Trustworthy，然後啟用 CLR 整合。 請參閱 SQL Server 文件中的 [TRUSTWORTHY 資料庫屬性](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) 和  [啟用 CLR 整合](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx)。  

4.  啟動「站台元件管理員」(**sitecomp**) 和 **SMS_Executive** 服務來重新啟動站台。  

#### <a name="to-remove-a-replica-member-from-the-availability-group"></a>從可用性群組移除複本成員  

-   請參閱 SQL Server 文件庫中 [將次要複本從可用性群組移除](https://msdn.microsoft.com/library/hh213149\(v=sql.120\).aspx) 中的資訊。  

##  <a name="a-namebkmkremovea-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a><a name="bkmk_remove"></a> 將站台資料庫從可用性群組移回到單一執行個體 SQL Server  
 當您不想再將站台資料庫裝載在可用性群組中時，請使用下列程序。  

#### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>將站台資料庫從可用性群組移回到單一執行個體 SQL Server  

1.  使用下列命令來停止 Configuration Manager 站台：  
     **Preinst.exe /stopsite**。  如需詳細資訊，請參閱 [System Center Configuration Manager 的階層維護工具 (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)。  

2.  使用 SQL Server 從主要複本建立站台資料庫的完整備份。 如需如何完成此步驟的資訊，請參閱 SQL Server 文件中的 [建立完整資料庫備份](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) 。  

3.  如果裝載可用性群組之主要複本的伺服器現在將裝載站台資料庫的單一執行個體，您可以略過此步驟 ︰  

    -   使用 SQL Server 將站台資料庫備份還原到將裝載站台資料庫的伺服器。  請參閱 SQL Server 文件中的 [還原資料庫備份 (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx) 。  

4.  在已還原的站台資料庫上，將站台資料庫的備份模式從 **[完整]** 變更為 **[簡單]**。  請參閱 SQL Server 文件中的 [檢視或變更資料庫的復原模式](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) 。  

5.  從 **&lt;Configuration Manager 站台安裝資料夾\>\BIN\X64\setup.exe** 執行 [Configuration Manager 安裝程式]。  

6.  在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台] ，然後按 [下一步] 。  

7.  選取 **[修改 SQL Server 設定]** 選項，然後按一下 **[下一步]**。  

8.  為站台資料庫重新設定下列各項︰  

    -   **SQL Server 名稱：** 輸入現在裝載站台資料庫的伺服器名稱。  

    -   **執行個體︰** 指定裝載站台資料庫的具名執行個體，或如果資料庫位於預設執行個體上，則保留空白。  

    -   **資料庫︰** 保留顯示的名稱。 這是目前站台資料庫的名稱。  

9. 提供新資料庫位置的資訊之後，請使用您的一般程序和設定來完成安裝。 當安裝完成時，站台會重新啟動並開始使用新的資料庫位置。  

10. 若要清除具備可用性群組成員身分的伺服器，請遵循 SQL Server 文件中 [移除可用性群組](https://msdn.microsoft.com/library/ff878113\(v=sql.120\).aspx) 中的指引進行。



<!--HONumber=Dec16_HO3-->


