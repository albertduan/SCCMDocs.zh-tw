---
title: "SQL Server 支援 | System Center Configuration Manager"
description: "取得裝載 System Center Configuration Manager 站台資料庫的 SQL Server 版本和設定需求。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b17720021f797d404a89933939427696dfafd7dc


---
# <a name="support-for-sql-server-versions-for-system-center-configuration-manager"></a>System Center Configuration Manager 的 SQL Server 版本支援

*適用於：System Center Configuration Manager (最新分支)*

每個 System Center Configuration Manager 站台都必須有支援的 SQL Server 版本和設定，才能裝載站台資料庫。  

##  <a name="a-namebkmkinstancesa-sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> SQL Server 執行個體和位置  
 **管理中心網站和主要站台：**  

站台資料庫必須使用完整的 SQL Server 安裝。  

 SQL Server 的位置可以在︰  

-   網站伺服器電腦  
-   站台伺服器的遠端電腦  

以下是支援的執行個體：  

-   SQL Server 預設或具名執行個體  
-   多個執行個體組態  
-   SQL Server 叢集  - 請參閱 [Use a SQL Server cluster to host the site database](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md) (使用 SQL Server 叢集裝載站台資料庫)
-   SQL Server AlwaysOn 可用性群組 - 此選項需要 Configuration Manager 1602 或更新版本。 如需詳細資訊，請參閱[適用於 System Center Configuration Manager 之高可用性站台資料庫的 SQL Server AlwaysOnn](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)  

> [!NOTE]  
>  在網路負載平衡 (NLB) 叢集組態中不支援 SQL Server 叢集。 此外，也不支援 SQL Server 資料庫鏡像技術和點對點複寫。 僅支援將 SQL Server 標準異動複寫用於將物件複寫至設定為使用 [資料庫複本](https://technet.microsoft.com/library/mt608546.aspx)的管理點。  


 **次要站台：**  

 站台資料庫可以使用預設的完整 SQL Server 安裝執行個體，或是使用 SQL Server Express  

 SQL Server 的位置必須在站台伺服器電腦上  

##  <a name="a-namebkmksqlversionsa-supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> 支援的 SQL Server 版本  
 在具有多個站台的階層中，不同站台可以使用不同版本的 SQL Server 來裝載站台資料庫，只要 Configuration Manager 支援您使用的 SQL Server 版本即可。  

 以下是 System Center Configuration Manager 1511 和更新版本支援的 SQL Server 版本。  

> [!IMPORTANT]  
>  在管理中心網站針對資料庫使用 SQL Server Standard 時，一個階層所能支援的用戶端總數會受到限制。 請參閱 [Size and scale numbers](../../../core/plan-design/configs/size-and-scale-numbers.md) (大小與縮放比例)。

### <a name="sql-server-2016---standard-enterprise"></a>SQL Server 2016 - Standard、Enterprise  

支援與 1606 版搭配使用。   
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要網站  
-   次要網站  


### <a name="sql-server-2014-sp2---standard-enterprise"></a>SQL Server 2014 SP2 - Standard、Enterprise  

支援用於 1511 版和更新版本。  
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要網站  
-   次要網站  



### <a name="sql-server-2014-sp1---standard-enterprise"></a>SQL Server 2014 SP1 - Standard、Enterprise  

支援用於 1511 版和更新版本。  
 您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要網站  
-   次要網站  


### <a name="sql-server-2012-sp3---standard-enterprise"></a>SQL Server 2012 SP3 - Standard、Enterprise  

支援用於 1511 版和更新版本。  
 您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要網站  
-   次要網站  


### <a name="sql-server-2012-sp2---standard-enterprise"></a>SQL Server 2012 SP2 - Standard、Enterprise  

支援用於 1511 版和更新版本。  
 您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要網站  
-   次要網站  


### <a name="sql-server-2008-r2-sp3---standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3 - Standard、Enterprise、Datacenter  

支援用於 1511 版和更新版本。    
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要網站  
-   次要網站  

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
支援與 1606 版搭配使用。  
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：
-   次要網站

### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2  
支援與 1511 版和更新版本搭配使用。  
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   次要網站  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1  
 支援與 1511 版和更新版本搭配使用。   
 您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   次要網站  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
支援與 1511 版和更新版本搭配使用。   
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   次要網站  

### <a name="sql-server-2012-express-sp2"></a>SQL Server 2012 Express SP2  
 支援與 1511 版和更新版本搭配使用。  
 您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   次要網站  

##  <a name="a-namebkmksqlconfiga-required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> 必要的 SQL Server 設定  
 以下是您用於站台資料庫的所有 SQL Server 安裝 (包括 SQL Server Express) 的必要設定。 如果 Configuration Manager 在安裝次要站台時一併安裝 SQL Server Express，就會自動為您進行這些設定。  

 **SQL Server 架構版本：**  
 Configuration Manager 需要 64 位元版本的 SQL Server 才能裝載站台資料庫。  

 **資料庫定序：**  
 在每個站台，用於站台和站台資料庫的 SQL Server 執行個體都必須使用下列定序： **SQL_Latin1_General_CP1_CI_AS**。  

 Configuration Manager 支援此定序的兩種例外狀況，以符合用於中國以 GB18030 定義的標準。 如需詳細資訊，請參閱 [System Center Configuration Manager 的多語系支援](../../../core/plan-design/hierarchy/international-support.md)。  

 **SQL Server 功能：**  
 只有 **Database Engine Services** 功能為每個站台伺服器所需。  

 Configuration Manager 資料庫複寫不需要 **SQL Server 複寫**功能。 不過，當您將使用 [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) (System Center Configuration Manager 之管理點的資料庫複本) 時，此 SQL Server 設定則為必要。  

 **Windows 驗證：**  
 Configuration Manager 需要 **Windows 驗證**來驗證資料庫連線。  

 **SQL Server 執行個體：**  
 您必須為每個站台使用專用的 SQL Server 執行個體。 可以是 **具名執行個體** 或 **預設執行個體**。  

 **SQL Server 記憶體：**  
 使用 SQL Server Management Studio 並設定 **[伺服器記憶體選項]** 底下的 **[最小伺服器記憶體]**，即可保留 SQL Server 的記憶體。 如需如何設定固定記憶體容量的詳細資訊，請參閱 [如何：設定固定的記憶體容量 (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759)。  

-   **與站台伺服器安裝在相同電腦上的資料庫伺服器：** - 請將 SQL Server 記憶體限制在可用可定址系統記憶體的 50% 到 80%。  

-   **專用資料庫伺服器 (站台伺服器的遠端)：** -  請將 SQL Server 記憶體限制在可用可定址系統記憶體的 80% 到 90%。  

-   **為每個使用中 SQL Server 執行個體的緩衝集區所保留的記憶體：**  

    -   管理中心網站：最少 8 GB  
    -   主要站台：最少 8 GB  
    -   次要站台：最少 4 GB  

 **SQL 巢狀觸發程序：**  

 必須啟用[SQL 巢狀觸發程序](http://go.microsoft.com/fwlink/?LinkId=528802) 。  

 **SQL Server CLR 整合**  

  站台資料庫會要求啟用 SQL Server 通用語言執行平台 (CLR)。 當 Configuration Manager 安裝時，會自動啟用此功能。 如需 CLR 的詳細資訊，請參閱 [SQL Server CLR 整合簡介](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx)  

##  <a name="a-namebkmkoptionala-optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> 選擇性的 SQL Server 設定  
 下列組態可選擇性用於使用完整 SQL Server 安裝的各個資料庫。  

 **SQL Server 服務：**  
 您可以將 SQL Server 服務設為執行時使用：  

-   **網域本機使用者** 帳戶：  

    -   這是最佳做法，可能需要您手動註冊該帳戶的「服務主體名稱」(SPN)。  

-   執行 SQL Server 的電腦**本機系統** 帳戶：  

    -   使用本機系統帳戶簡化組態程序。  
    -   當您使用本機系統帳戶時，Configuration Manager 會自動註冊 SQL Server 服務的 SPN。  
    -   請注意，針對 SQL Server 服務使用本機系統帳戶不是 SQL Server 最佳做法。  

當 SQL Server 不使用電腦的本機系統帳戶執行 SQL Server 服務時，您必須在 Active Directory 網域服務中，設定執行 SQL Server 服務之帳戶的服務主體名稱 (SPN)。 (若是使用系統帳戶，將會自動為您登錄 SPN)。

如需站台資料庫 SPN 的資訊，請參閱  [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) 主題中的 [Manage the SPN for the site database server](../../../core/servers/manage/modify-your-infrastructure.md) 。  

如需如何變更 SQL Service 所用帳戶的相關資訊，請參閱 [如何：變更 SQL Server 的服務啟動帳戶 (SQL Server 組態管理員)](http://go.microsoft.com/fwlink/p/?LinkId=237661)。  

**SQL Server Reporting Services：**  
安裝可讓您執行報告的 Reporting Services 點所需。  

**SQL Server 連接埠：**  
如為 SQL Server 資料庫引擎和網站間複寫通訊，可以使用預設 SQL Server 連接埠組態或指定自訂連接埠：  

-   **站台間通訊** 使用 SQL Server Service Broker，其預設使用連接埠 TCP 4022。  
-   SQL Server 資料庫引擎與不同 Configuration Manager 站台系統角色之間的**站台內通訊**預設會使用連接埠 TCP 1433。 下列網站系統角色會直接與 SQL Server 資料庫通訊：  

    -   管理點  
    -   SMS 提供者的電腦  
    -   Reporting Services 點  
    -   網站伺服器  

SQL Server 裝載來自多個站台的資料庫時，每個資料庫都必須使用不同的 SQL Server 執行個體，而且每個執行個體都必須設定成使用一組唯一的連接埠。  

> [!WARNING]  
>  Configuration Manager 不支援動態連接埠。 由於 SQL Server 具名執行個體預設使用動態連接埠連線至資料庫引擎，因此，當您使用具名執行個體時，必須手動設定要用於網站間通訊的靜態連接埠。  

如果在執行 SQL Server 的電腦上啟用防火牆，請確定將其設定為允許您的部署正在使用之連接埠，以及與 SQL Server 通訊的電腦之間的任何網路位置所使用的連接埠。  

如需如何將 SQL Server 設為使用特定連接埠的範例，請參閱 SQL Server TechNet 文件庫中的 [如何：將伺服器設為在特定 TCP 連接埠上接聽 (SQL Server 組態管理員)](http://go.microsoft.com/fwlink/p/?LinkID=226349) 。  



<!--HONumber=Nov16_HO1-->


