---
title: "設定可用性群組 | Microsoft Docs"
description: "使用 SCCM 設定和管理 SQL Server Always On 可用性群組。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: 0d6527abba24b685151ae63feaae29b30d1e2cc9
ms.contentlocale: zh-tw
ms.lasthandoff: 07/29/2017

---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>針對 Configuration Manager 來設定 SQL Server Always On 可用性群組

適用於：System Center Configuration Manager (最新分支)

使用本主題中的資訊，搭配使用 Configuration Manager 來設定和管理可用性群組。

在開始之前：  
-   熟悉[透過 Configuration Manager 準備使用 SQL Server Always On 可用性群組](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)的資訊。
-   熟悉 SQL Server 的文件，其中涵蓋可用性群組的使用方式及相關程序。 該資訊是完成下列案例所需資訊。

> [!TIP]  
>  本主題中 SQL Server 的連結會移至適用於 SQL Server 2016 的內容。 如果您不是使用該版本的 SQL Server，請參閱所使用版本的文件。

## <a name="create-and-configure-an-availability-group"></a>建立和設定可用性群組
使用下列程序建立可用性群組，然後將站台資料庫的複本移至該可用性群組。

若要完成此程序，您使用的帳戶必須是：
-   可用性群組中之每部電腦上的**本機 Administrators** 群組成員。
-   每個裝載站台資料庫之 SQL Server 執行個體上的 **sysadmin**。

### <a name="to-create-and-configure-an-availability-group-for-configuration-manager"></a>針對 Configuration Manager 建立和設定可用性群組  
1.  使用下列命令來停止 Configuration Manager 站台：**Preinst.exe /stopsite**。 如需有關使用 Preinst.exe 的詳細資訊，請參閱[階層維護工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)。

2.  將站台資料庫的備份模式從 **[簡單]** 變更為 **[完整]**。
請參閱 SQL Server 文件中的 [檢視或變更資料庫的復原模式](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) 。 (可用性群組僅支援 [完整] 模式)。

3.  使用 SQL Server 來建立您站台資料庫的完整備份。 然後視裝載站台資料庫的伺服器是否將會是新可用性群組的複本成員來執行下列其中一項：
    -   **將會是可用性群組的成員：**  
        如果您使用此伺服器作為可用性群組的初始主要複本成員，則不需要將站台資料庫的複本還原至此伺服器或群組中的其他伺服器。 資料庫會在主要複本上準備就緒，而 SQL Server 在稍後的步驟中會將資料庫複寫至次要複本。  

      -    **不會是可用性群組的成員：**   
    將站台資料庫複本還原至將裝載群組主要複本的伺服器。

    如需如何完成此步驟的資訊，請參閱 SQL Server 文件中的[建立完整資料庫備份](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)和[使用 SSMS 還原資料庫備份](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。

4.  在將裝載群組之初始主要複本的伺服器上，使用[新增可用性群組精靈](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio)來建立可用性群組。 在精靈中：
      -    在 [選取資料庫] 頁面上，為您的 Configuration Manager 站台選取資料庫。  

      -    在 **[指定複本]** 頁面上，設定︰
          -    **複本**︰指定將裝載次要複本的伺服器。

          -    **接聽程式**︰指定 [接聽程式 DNS 名稱] 作為完整 DNS 名稱 (例如 **&lt;Listener_Server>.fabrikam.com**)。 當您設定 Configuration Manager 使用可用性群組中的資料庫時，將會使用此項目。

      -    在 **[選取初始資料同步處理]** 頁面上，選取 **[完整]**。 在精靈建立可用性群組之後，精靈會備份主要資料庫和交易記錄檔， 然後在裝載次要複本的每部伺服器上還原它們。 (如果您不使用此步驟，就必須將站台資料庫的複本還原到裝載次要複本的每部伺服器，然後手動將該資料庫加入群組中)。   

5.  檢查每個複本上的設定：   
  1.    確定站台伺服器的電腦帳戶是每部可用性群組成員電腦上的「本機 Administrators」群組成員。  

  2.  執行必要條件的[驗證指令碼](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites)，以確認每個複本上的站台資料庫都設定正確。

  3.    如果必須設定次要複本的設定，您必須手動將主要複本容錯移轉至次要複本，然後才能繼續進行。 您只能設定主要複本的資料庫。 如需詳細資訊，請參閱 SQL Server 文件中的[執行可用性群組規劃的手動容錯移轉](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server)。

6.  所有複本都符合需求之後，可用性群組就已準備好可搭配使用 Configuration Manager。

## <a name="configure-a-site-to-use-the-database-in-the-availability-group"></a>設定站台以使用可用性群組中的資料庫
在您[建立和設定可性群組](#create-and-configure-an-availability-group)之後，請使用 Configuration Manager 站台維護來設定站台，以使用可用性群組裝載的資料庫。

不支援在可用性群組中安裝附有資料庫的新站台。 例如，如果您使用基準 1702 媒體，則必須使用 SQL Server 單一執行個體來安裝站台。 安裝站台之後，接著便可以將站台資料庫移動至可用性群組。

若要完成此程序，您用來執行 Configuration Manager 的帳戶必須是：
-   每部可用性群組成員電腦上的「本機 Administrator」群組成員。
-   每個裝載站台資料庫之 SQL Server 執行個體上的 **sysadmin**。

> [!IMPORTANT]
> 當您以混合式組態搭配使用 Microsoft Intune 與 Configuration Manager，從可用性群組來回移動站台資料庫會觸發雲端資料的重新同步處理。 此重新同步處理程序是無法避免的。

### <a name="to-configure-a-site-to-use-the-availability-group"></a>設定站台以使用可用性群組
1.  從 **&lt;*Configuration Manager 站台安裝資料夾*>\BIN\X64\setup.exe** 執行「Configuration Manager 安裝程式」。

2.  在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台] ，然後按 [下一步] 。

3.  選取 **[修改 SQL Server 設定]** 選項，然後按一下 **[下一步]**。

4.  為站台資料庫重新設定下列各項︰
    -   **SQL Server 名稱**：輸入建立可用性群組時所設定的可用性群組「接聽程式」虛擬名稱。 這個虛擬名稱應該是完整 DNS 名稱，例如 **&lt;*endpointServer*>.fabrikam.com**。  

    -   **執行個體：**此值必須為空白以指定可用性群組「接聽程式」的預設執行個體。 如果目前的站台資料庫是安裝在具名執行個體上，該具名執行個體將會列出且必須清除。

    -   **資料庫︰** 保留顯示的名稱。 這是目前站台資料庫的名稱。

5.  提供新資料庫位置的資訊之後，請使用您的一般程序和設定來完成安裝。



## <a name="add-and-remove-synchronous-replica-members"></a>新增和移除同步複本成員  
當站台資料庫裝載於可用性群組中時，可使用下列程序來新增或移除同步複本成員。 如需支援的複本類型和數目的相關資訊，請參閱準備使用可用性群組主題中[必要條件](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites)底下的**可用性群組設定**。

若要完成下列程序，您使用的帳戶必須是：
-   每部可用性群組成員電腦上的「本機 Administrator」群組成員。
-   每個裝載或即將裝載站台資料庫之 SQL Server 上的 **sysadmin**。


### <a name="to-add-a-new-synchronous-replica-member"></a>新增同步複本成員
1.  新增新的伺服器作為可用性群組的次要複本。 請參閱 SQL Server 文件庫中的[將次要複本加入至可用性群組 (SQL Server)](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server)。

2.  執行 **Preinst.exe /stopsite** 來停止 Configuration Manager 站台。 請參閱[階層維護工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)。

3.  使用 SQL Server 從主要複本建立站台資料庫的備份，然後將該備份還原到新的次要複本伺服器。 請參閱 SQL Server 文件中的[建立完整資料庫備份](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)和[使用 SSMS 還原資料庫備份](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。

4.  設定每個次要複本。 針對可用性群組中的每個次要複本執行下列動作︰

    1.  確定站台伺服器的電腦帳戶是每部可用性群組成員電腦上的「本機 Administrators」群組成員。

    2.  執行必要條件的[驗證指令碼](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites)，以確認每個複本上的站台資料庫都設定正確。

    3.  如果必須設定新的複本，請手動將主要複本容錯移轉至新的次要複本，然後進行所需的設定。 請參閱 SQL Server 文件中的 [執行可用性群組的已規劃手動容錯移轉](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) 。

5.  啟動「站台元件管理員」(**sitecomp**) 和 **SMS_Executive** 服務來重新啟動站台。

### <a name="to-remove-a-replica-member"></a>移除複本成員
針對此程序，請使用 SQL Server 文件中[將次要複本從可用性群組移除](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server)中的資訊。

## <a name="configure-an-asynchronous-commit-replica"></a>設定非同步認可複本
從 Configuration Manager 1706 版開始，您可以在搭配 Configuration Manager 使用的可用性群組中新增非同步複本。 基於此目的，您不需執行設定同步複本所需的設定指令碼。 (這是因為不支援使用該非同步複本作為站台資料庫)。如需有關如何將次要複本新增到可用性群組的資訊，請參閱 [SQL Server 文件](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot))。

## <a name="use-the-asynchronous-replica-to-recover-your-site"></a>使用非同步複本來復原您的站台
使用 Configuration Manager 1706 版和更新版本，您可以使用非同步複本來復原站台資料庫。 若要這樣做，您必須停止使用中的主要站台，以防止其他寫入站台資料庫的活動。 在停止該站台之後，您可以使用非同步複本來取代使用[手動復原的資料庫](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption)。

若要停止該站台，您可以使用[階層維護工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)來停止站台伺服器上的主要服務。 請使用命令列：**Preinst.exe /stopsite**   

停止該站台相當於停止站台伺服器上後面接著 SMS_Executive 服務的「站台元件管理員」服務 (sitecomp)。

<!-- For inclusion with passive primary site support:
> [!TIP]  
> If you use a primary passive replica (introduced in version [TBD],  you do not need to stop the passive replica. Only the active primary site must be stopped.
-->  

## <a name="stop-using-an-availability-group"></a>停止使用可用性群組
當您不想再將站台資料庫裝載在可用性群組中時，請使用下列程序。 這牽涉到將站台資料庫移回 SQL Server 的單一執行個體。

若要完成此程序，您使用的帳戶必須是：
-   每部可用性群組成員電腦上的「本機 Administrator」群組成員
-   每個裝載站台資料庫之 SQL Server 執行個體上的 **sysadmin**。

> [!IMPORTANT]  
> 當您以混合式組態搭配使用 Microsoft Intune 與 Configuration Manager，從可用性群組來回移動站台資料庫會觸發雲端資料的重新同步處理。 這並無法避免。

### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>將站台資料庫從可用性群組移回到單一執行個體 SQL Server
1.  使用下列命令來停止 Configuration Manager 站台：**Preinst.exe /stopsite**。 如需詳細資訊，請參閱[階層維護工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)。

2.  使用 SQL Server 從主要複本建立站台資料庫的完整備份。 如需如何完成此步驟的資訊，請參閱 SQL Server 文件中的 [建立完整資料庫備份](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) 。

3.  如果可用性群組主要複本伺服器將裝載站台資料庫的單一執行個體，則可以略過此步驟︰  

    -   使用 SQL Server 將站台資料庫備份還原到將裝載站台資料庫的伺服器。 請參閱 SQL Server 文件中的[使用 SSMS 還原資料庫備份](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。   <br />  <br />

4.  在將裝載站台資料庫的伺服器上 (主要複本，或還原站台資料庫的伺服器)，將站台資料庫的備份模式從 [完整] 變更為 [簡單]。 請參閱 SQL Server 文件中的 [檢視或變更資料庫的復原模式](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) 。  

5.  從 **&lt;*Configuration Manager 站台安裝資料夾*>\BIN\X64\setup.exe** 執行「Configuration Manager 安裝程式」。

6.  在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台] ，然後按 [下一步] 。  

7.  選取 **[修改 SQL Server 設定]** 選項，然後按一下 **[下一步]**。  

8.  為站台資料庫重新設定下列各項︰
    -   **SQL Server 名稱：** 輸入現在裝載站台資料庫的伺服器名稱。

    -   **執行個體︰** 指定裝載站台資料庫的具名執行個體，或如果資料庫位於預設執行個體上，則保留空白。

    -   **資料庫︰** 保留顯示的名稱。 這是目前站台資料庫的名稱。    

9.  提供新資料庫位置的資訊之後，請使用您的一般程序和設定來完成安裝。 當安裝完成時，站台會重新啟動並開始使用新的資料庫位置。    

10. 若要清除具備可用性群組成員身分的伺服器，請遵循 SQL Server 文件中 [移除可用性群組](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server) 中的指引進行。

