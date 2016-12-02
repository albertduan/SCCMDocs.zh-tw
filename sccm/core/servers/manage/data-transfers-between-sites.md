---
title: "資料移轉 | System Center Configuration Manager"
description: "了解 Configuration Manager 如何在站台之間移動資料，以及如何管理該資料在您網路上的移轉。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1abd28aa4ce4f946f6328f8f7924b5f5a81e640c


---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的站台間資料傳輸

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 會使用**檔案複寫**與**資料庫複寫**在站台之間傳送不同類型的資訊。  本主題中的主題可協助您了解 Configuration Manager 如何在站台之間移動資料，以及您如何管理該資料在網路之間的傳輸。  


##  <a name="a-namebkmkfileroutea-file-based-replication"></a><a name="bkmk_fileroute"></a> File-based replication  
 Configuration Manager 會使用檔案複寫在階層中網站間傳送檔案資料。 這項資料包括您想要部署至子網站中發佈點的應用程式和套件，以及傳送至進行處理所在父網站的未經處理探索資料記錄等內容。  

 站台之間以檔案為主的通訊會透過 **TCP/IP 連接埠 445** 來使用 **伺服器訊息區**(SMB) 通訊協定。 您可以指定包括頻寬節流和脈衝模式的組態來控制經網路傳輸的資料量，並且進行排程，以控制經網路傳送資料的時間。  

###  <a name="a-namebkmkroutesa-file-replication-routes"></a><a name="bkmk_routes"></a> 檔案複寫路由  
 下列資訊可協助您設定及使用檔案複寫路由：  

 **檔案複寫路由** - 每個檔案複寫路由都會識別可傳送檔案資料的目的地站台。 每個網站都支援連接至特定目的地網站的單一檔案複寫路由。  

 Configuration Manager 支援下列檔案複寫路由的設定：  

-   **檔案複寫帳戶**：此帳戶用來連線至目的地網站以及將資料寫入該網站的 **SMS_SITE** 共用。 寫入此共用的資料會由接收網站處理。 根據預設，將站台加入階層時，Configuration Manager 會將新站台的站台伺服器電腦帳戶指派為該站台的**檔案複本帳戶**。 此帳戶會接著加入目的地站台的 **SMS_SiteToSiteConnection_&lt;站台碼\>** 群組中，而該群組是電腦上具有 **SMS_SITE** 共用之存取授權的本機群組。 您可以將此帳戶變更為 Windows 使用者帳戶。 如果您變更帳戶，請務必將新帳戶加入目的地站台的 **SMS_SiteToSiteConnection_&lt;站台碼\>** 群組。  

    > [!NOTE]  
    >  次要網站一律使用次要網站伺服器的電腦帳戶做為 [檔案複寫帳戶] 。  

-   **排程**：您可以設定每個檔案複寫路由的排程，限制可傳送至目的地網站的資料類型和時間。  

-   **速率限制**：您可以設定每個檔案複寫路由的速率限制，以控制網站傳送資料至目的地網站時使用的網路頻寬：  

    -   使用 [脈衝模式]  指定傳送至目的地網站的資料區塊大小。 您也可以指定傳送每個資料區塊之間的時間延遲。 如果您必須經由非常低頻寬的網路連線傳送資料至目的地網站，請使用此選項。 例如，您可能限制每五秒傳送 1 KB 的資料，而非每三秒 1 KB，無論於特定時間的連結速度或其使用情形為何。  

    -   使用 [限制為每小時最大傳送速率]  ，讓網站僅使用您指定的時間百分比傳送資料至目的地網站。 使用此選項時，Configuration Manager 不會識別網路的可用頻寬，而會將可傳送資料的時間細分成時間片段。 然後資料會在一小片段時間內傳送，下一個時間片段則不傳送資料。 例如，如果最大速率設為 **50%**，則 Configuration Manager 會在沒有資料傳輸時的一段相等時間間隔之後，傳輸一定時間量的資料。 不會管理實際資料量大小 (或資料區塊大小)。 只會管理傳送資料的時間長度。  

        > [!CAUTION]  
        >  根據預設，網站最多可以使用三個 [並行傳送]  將資料傳送至目的地網站。 當您啟用檔案複寫路由的速率限制時，傳送資料至該網站的 [並行傳送]  會限制為一個。 這項限制在 [限制可用的頻寬 (%)]  設為 [100%] 時也適用。 例如，如果您針對寄件者使用預設設定，這樣就會將傳送至目的地網站的傳輸速率減少為預設容量的三分之一。  

-   您可以在兩個次要網站之間設定檔案複寫路由，在網站之間路由傳送檔案內容。  

若要管理檔案複寫路由，請在 [系統管理]  工作區中展開 [階層設定]  節點，並選取 [檔案複寫] 。  

**傳送者** - 每個站台都有一位傳送者。 傳送者會管理從一個網站到目的地網站的網路連線，並可以同時建立和多個網站間的連線。 為了連線至網站，傳送者會使用至該網站的檔案複寫路由，以識別用來建立網路連線的帳戶。 傳送者也會使用這個帳戶將資料寫入目的地網站的 **SMS_SITE** 共用。  

 根據預設，傳送者會使用多個 [並行傳送] (一般視為執行緒)，將資料寫入目的地網站。 每個並行傳送 (或執行緒) 可以將不同的檔案物件傳輸到目的地網站。 根據預設，傳送者開始傳送物件時，傳送者會繼續寫入該物件的資料區塊，直到整個物件傳送完畢為止。 物件的所有資料都傳送完畢後，新的物件就會開始在該執行緒上傳送。  

 您可以為傳送者設定以下設定：  

-   **並行傳送上限**：根據預設，每個網站都設定為使用五個 [並行傳送] ，傳送資料到任一目的地網站時可以使用三個。 增加此數量時，您可以經由啟用 Configuration Manager 來增加網站間資料的輸送量，以便同時傳輸更多檔案。 不過，增加數量也會增加對網站間網路頻寬的需求。  

-   **重試設定**：根據預設，每個網站都設定為重試有問題的連線兩次，每次連線嘗試間會有一分鐘的延遲。 您可以修改網站進行連線嘗試的次數，以及每次嘗試間等候的時間長度。  

若要管理網站的傳送者，請展開 [系統管理]  工作區中的 [階層設定]  節點，然後選取 [網站]  ，接著按一下您要管理之網站的 [內容]  。 按一下 [傳送者]  索引標籤，變更傳送者設定。  

##  <a name="a-namebkmkdbrepa-database-replication"></a><a name="bkmk_dbrep"></a> Database replication  
Configuration Manager 資料庫複寫會使用 SQL Server 來傳輸資料，以及合併站台資料庫中的變更和儲存在階層中其他站台資料庫中的資訊。  

-   這可讓所有站台共用相同資訊  

-   在階層中安裝站台時，會在新站台和其指定的父站台間自動設定資料庫複寫  

-   站台安裝完成後，就會自動開始進行資料庫複寫  

當您將新的站台加入階層時，Configuration Manager 會在新站台建立一般資料庫。 接著，父網站會建立其資料庫中相關資料的快照，並藉由以檔案為基礎的複寫，將該快照傳輸到新網站。 然後，新站台會使用 SQL Server 大量複製程式 (BCP)，將資訊載入 Configuration Manager 資料庫的本機複本中。 載入快照後，每個網站都會和其他網站一起執行資料庫複寫。  

為了在網站間複寫資料，Configuration Manager 會使用其擁有的資料庫複寫服務。 資料庫複寫服務會使用 SQL Server 變更追蹤來監控本機網站資料庫的變更，然後使用 **SQL Server Service Broker**將這些變更複寫至其他站台。 根據預設，這個程序會使用 **TCP/IP 連接埠 4022**。  

Configuration Manager 會將資料庫複寫所複寫的資料分門別類到不同的複寫群組內。  

-   每個複寫群組都有各自固定的複寫排程，這會決定將群組中的資料變更複寫至其他網站的頻率。  

     例如，針對以角色為基礎之系統管理設定的設定變更會很快複寫到其他網站，確保能儘快執行這些變更。 而較低優先順序的組態變更 (如請求安裝新的次要站台) 並不存在急迫複寫的需求，因此可能會花上幾分鐘的時間，才會將新站台請求送達目的地主要站台  

-   您可以修改資料庫複寫的下列項目：  

    -   **資料庫複寫連結** ，讓您控制何時特定流量會周遊網路。  

    -   **分散式檢視** ，是複寫連結的組態，可針對所選站台資料在管理中心網站所提出的請求，讓這些請求從子主要站台資料庫直接存取該站台資料。  

    -   **排程** 可以讓您設定何時使用複寫連結，並指定何時複寫不同類型的站台資料。  

    -   根據預設，有關周遊複寫連結之網路流量資料的**摘要** 每 15 分鐘產生一次，並且在資料庫複寫的報表中使用。  

    -   **資料庫複寫閾值** 定義何時將連結報告為降級或失敗。 您也可以設定 Configuration Manager 何時發出有關複寫連結之狀態降級或失敗的警示。  

Configuration Manager 會將資料庫複寫複製的資料分類為全域資料或網站資料。 發生資料庫複寫時，全域資料和網站資料的變更都會傳輸到所有的資料庫複寫連結。 全域資料可以複寫至父和子網站，而網站資料只能複寫到父網站。 第三種資料類型名為本機資料，其不會複寫到其他網站。 本機資料包括其他網站並不需要的資訊：  

-   **全域資料**：全域資料是指會複寫到整階層中所有網站並由系統管理員建立的物件，但次要網站只會接收全域資料中全域 Proxy 資料這部分。 全域資料的範例包括軟體部署、軟體更新、收集定義和以角色為基礎的系統管理安全性範圍。 系統管理員可以在管理中心網站和主要網站上建立全域資料。  

-   **網站資料**：網站資料是指 Configuration Manager 主要網站和用戶端回報至主要網站時建立的操作資訊。 網站資料會複寫到管理中心網站，但不會複寫到其他主要網站。 網站資料範例包括硬體清查資料、狀態訊息、警示，以及以查詢為基礎之集合的結果。 您只能從資料最初來源的管理中心網站和主要網站檢視網站資料， 且只能在建立該資料的主要網站上修改網站資料。  

     所有網站資料都會複寫到管理中心網站；因此，管理中心網站可以執行系統管理，並報告整個階層。  

下列章節將詳細說明您可以為管理資料庫複寫所做的組態  

###  <a name="a-namebkmkdblinksa-database-replication-links"></a><a name="bkmk_Dblinks"></a> 資料庫複寫連結  
在階層中安裝新網站時，Configuration Manager 會在兩個新網站間自動建立資料庫複寫連結。 系統會在新網站和父網站間建立單一連結。  

每個資料庫複寫連結都支援協助控制跨複寫連結的資料傳輸的組態。 每個複寫連結支援個別的設定。 資料庫複寫連結的控制項包括以下項目：  

-   使用分散式檢視，以停止將所選網站資料從主要網站複寫到管理中心網站，並啟用管理中心網站直接從主要網站資料庫存取此資料。  

-   排定何時將選取的網站資料從子主要網站傳輸到管理中心網站。  

-   定義判斷資料庫複寫連結是否降級或失敗的設定。  

-   設定何時發出複寫連結失敗的警示。  

-   指定 Configuration Manager 摘要使用複寫連結之複寫流量資料的頻率。 此資料會用在報告中。  

若要設定資料庫複本連結，您可以在 Configuration Manager 主控台的 [資料庫複本] 節點編輯此內容的連結。 此節點會出現在 [監視]  工作區下，以及 [系統管理]  工作區中的 [階層設定]  節點下。 您可以從複寫連結的父網站或子網站編輯複寫連結。  

> [!TIP]  
>  您可以從其中一個工作區的 [資料庫複寫]  節點編輯資料庫複寫連結。 不過，使用 [監視]  工作區中的 [資料庫複寫]  節點時，您也可以檢視複寫連結的資料庫複寫狀態，以及存取 [複寫連結分析師] 工具，以協助您調查資料庫複寫的問題。  

如需如何設定複寫連結的詳細資訊，請參閱 [網站資料庫複寫控制](#BKMK_DBRepControls)。 如需如何監視複寫的詳細資訊，請參閱 [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) 主題中的 [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) 一節。  

使用以下各節中的資訊來規劃資料庫複寫連結。  

###  <a name="a-namebkmkdistviewsa-distributed-views"></a><a name="bkmk_distviews"></a> 分散式檢視  
針對所選網站資料在管理中心網站所提出的請求，分散式檢視可讓這些請求從子主要網站資料庫直接存取該網站資料。 這種直接存取會取代從主要網站將此網站資料複寫到管理中心網站的需求。 由於每個複寫連結和其他複寫連結各自獨立，因此您僅能在您選擇的複寫連結上啟用分散式檢視。 主要網站和次要網站間則不支援分散式檢視。  

分散式檢視可提供以下優勢：  

-   降低處理管理中心網站和主要網站之資料庫變更方面的 CPU 負載。  

-   降低經由網路傳輸到管理中心網站的資料量。  

-   改善搭載管理中心網站資料庫之 SQL Server 的效能。  

-   降低管理中心網站資料庫使用的磁碟空間。  

若主要網站在網路上和管理中心網站十分接近，且兩個網站持續開啟並保持連線，那麼請考慮使用分散式檢視。 這是因為分散式檢視會以每個網站上 SQL Server 間的直接連線，取代網站間所選取資料的複寫。 每次在管理中心網站上請求此資料時，就會進行這種直接連線。 一般來說，在您執行報告或查詢、於資源總管內檢視資訊，以及依據集合評估 (針對含有以網站資料為基礎之規則的集合) 來檢視資訊時，皆可發出啟用分散式檢視的資料請求。  

根據預設，每個複寫連結都會停用分散式檢視。 為複寫連接啟用分散式檢視時，您應選取不會經由該連結複寫至管理中心網站的網站資料，並讓管理中心網站直接從共用連結之子主要網站的資料庫存取此資料。 您可以針對分散式檢視設定以下網站資料類型：  

-   來自用戶端的硬體清查資料  

-   來自用戶端的軟體清查和計量資料  

-   用戶端、主要網站和所有次要網站的狀態訊息  

您也可以選擇讓檢視 Configuration Manager 主控台或報告內資料的系統管理員無法看到分散式檢視。 當發出啟用分散式檢視的資料請求時，裝載管理中心網站資料庫的 SQL Server 會直接存取子主要網站的 SQL Server，以擷取資訊。 例如，當您使用管理中心網站的 Configuration Manager 主控台，從兩個網站請求有關硬體清查的資訊，但只有一個網站擁有啟用分散式檢視之硬體清查的情況時， 來自未設定分散式檢視之網站的用戶端清查資訊，會經由管理中心網站的資料庫進行擷取。 而來自已設定分散式檢視之網站的用戶端清查資訊，可經由子主要網站的資料庫進行存取。 此資訊會顯示在 Configuration Manager 主控台或報告中，內容和來源並無不同。  

只要複寫連結具備啟用分散式檢視的資料類型，子主要網站就不會將該資料複寫到管理中心網站。 一旦您關閉某個資料類型的分散式檢視，子主要網站就會恢復將該資料複寫到管理中心網站，做為一般資料複寫的一部分。 不過，包含此資料的複寫群組必須在主要網站和管理中心網站間重新初始化，才可於管理中心網站上看到此資料。 在您解除安裝已啟用分散式檢視的主要網站後，管理中心網站必須先完成其資料的重新初始化，您才能存取在管理中心網站上啟用分散式檢視的資料。  

> [!IMPORTANT]  
>  在階層中任何複寫連結上使用分散式檢視時，您必須先停用所有複寫連結的分散式檢視，再解除安裝任何主要網站。 如需詳細資訊，請參閱 [Uninstall a primary site that is configured with distributed views](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews)。  

**分散式檢視的必要條件和限制：**  

-   只有在管理中心網站和主要網站間的複寫連結上才支援分散式檢視。  

-  管理中心網站必須使用 SQL Server 企業版。 主要站台沒有這項需求。

-   管理中心網站可以只有一個已安裝之 SMS 提供者的執行個體，且該執行個體必須安裝在網站資料庫伺服器上。 若要支援在管理中心網站上啟用 SQL Server 所需的 Kerberos 驗證以存取子主要網站上的 SQL Server，就必須具備這項條件。 對於子主要網站上的 SMS 提供者，沒有任何限制。  

-   管理中心網站上可以只安裝一個 SQL Server Reporting Services 點，且必須位於網站資料庫伺服器上。 若要支援在管理中心網站上啟用 SQL Server 所需的 Kerberos 驗證以存取子主要網站上的 SQL Server，就必須具備這項條件。  

-   網站資料庫無法裝載在 SQL Server 叢集上。  

-   站台資料庫無法裝載在 SQL Server AlwaysOn 可用性群組上。  

-   管理中心網站的資料庫伺服器電腦帳戶，需要主要網站之網站資料庫的 **Read** 權限。  

> [!IMPORTANT]  
>  分散式檢視及資料複寫排程，都是資料庫複寫連結的互斥設定。  

###  <a name="a-namebkmkschedulesa-schedule-transfers-of-site-data-on-database-replication-links"></a><a name="BKMK_schedules"></a> 資料庫複寫連結上的站台資料傳送排程  
為了協助您控制從子主網站複寫網站資料到管理中心網站所用的網路頻寬，您可以排定何時使用複寫連結，並指定何時複寫不同類型的網站資料。 您可以控制主要網站何時複寫狀態訊息、清查和計量資料。 次要網站的資料庫複寫連結不支援網站資料的排程。 無法排定全域資料傳送的時程。  

設定資料庫複寫連結排程時，您可以限制只從主要網站將選定網站資料傳送到管理中心網站，並且可以設定複寫不同類型網站資料的不同時間。  

> [!IMPORTANT]  
>  分散式檢視及資料複寫排程，都是資料庫複寫連結的互斥設定。  

###  <a name="a-namebkmksummarizedbreplicationa-summarization-of-database-replication-traffic"></a><a name="BKMK_SummarizeDBReplication"></a> 資料庫複寫流量摘要  
每個站台都會定期將有關周遊包括站台在內的資料庫複寫連結之網路流量的資料，製作成摘要。 此摘要資料可用於資料庫複寫報告中。 複寫連結上的兩個網站，都會將周遊複寫連結的網路流量製做為摘要。 資料的摘要是由裝載網站資料庫的 SQL Server 所執行。 製作資料摘要後，此資訊便會複寫至其他網站做為全域資料。  

根據預設，每隔 15 分鐘便會摘要一次。 您可以藉由編輯資料庫複寫連結內容中的 [摘要間隔]  ，修改網路流量摘要的頻率。 摘要的頻率會影響您在資料庫複寫報告中檢視的資訊。 您可以將此間隔時間修改為 5 到 60 分鐘。 當您增加摘要的頻率時，便會增加複寫連結上各網站的 SQL Server 處理負載。  

###  <a name="a-namebkmkdbrepthresholdsa-database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a> 資料庫複寫閾值  
資料庫複寫閾值可定義資料庫複寫連結狀態會在何時報告為降級或失敗。 根據預設，當有任何一個複寫群組連續 12 次都無法完成複寫時，便會將連結設為降級，當有任何一個複寫群組連續 24 次都無法複寫時，則設為失敗。  

您可以指定自訂值以微調 Configuration Manager 在何時將複寫連結報告為已降級或失敗。 調整 Configuration Manager 在何時報告各個資料庫複寫連結狀態可協助您準確地監視整個資料庫複寫連結的資料庫複寫健全狀況。  

由於可能會有一個或少數複寫群組複寫失敗，而其他複寫群組卻繼續成功複寫的情況，因此請在第一次報告降級狀態時，便檢閱複寫連結的複寫狀態。 如果有特定的複寫群組週期性地出現延遲，而這些延遲並未造成任何問題，或者網站之間的網路連結可用的頻寬過低時，請考慮修改連結降級或失敗狀態的重試次數值。 您可增加連結設為降級或失敗之前的重試次數，藉此減少已知問題的錯誤警告，以更加準確地追蹤連結狀態。  

您也可將各複寫群組的複寫同步處理間隔納入考慮，以了解該群組複寫的頻率。 您也可以在 [監視]  工作區中，[資料庫複寫]  節點之複寫連結的 [複寫詳細資料]  索引標籤上，檢視複寫群組的 [同步處理間隔]  。  

如需如何監視資料庫複寫 (包括如何檢視複寫狀態) 的詳細資訊，請參閱 [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) 主題中的 [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) 一節。  

如需設定資料庫複寫閾值的相關資訊，請參閱 [網站資料庫複寫控制](#BKMK_DBRepControls)。  

##  <a name="a-namebkmkdbrepcontrolsa-site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a> 站台資料庫複寫控制  
各網站皆支援可協助您控制用於資料庫複寫之網路頻寬的設定。 這些設定只適用於您配置設定值的網站資料庫，當網站將資料庫複寫的任何資料複寫到其他網站時一律會使用這些設定。  

各網站資料庫的複寫控制，包括以下各項：  

-   變更 Configuration Manager 用於 SQL Server Service Broker 的連接埠。  

-   設定複寫失敗觸發網站重新初始化其網站資料庫複本之前的等待時間。  

-   將網站資料庫設定為壓縮由資料庫複寫所複寫的資料。 只會壓縮網站之間傳送的資料，並不會壓縮儲存在任一網站之網站資料庫中的資料。  

若要設定站台資料庫複本控制，您可以在 Configuration Manager 主控台的 [資料庫複寫] 節點編輯此站台資料庫的內容。 此節點會出現在 [系統管理]  工作區中的 [階層設定]  節點之下，也會出現在 [監視工作區] 中。 若要編輯網站資料庫的內容，請選取網站之間的複寫連結，然後開啟 [父資料庫內容]  或 [子資料庫內容] 。  

> [!TIP]  
>  您可以從任一工作區的 [資料庫複寫]  節點，設定資料庫複寫控制。 不過，當您使用 [監視]  工作區中的 [資料庫複寫]  節點時，也可以檢視複寫連結的資料庫複寫狀態，並且存取 [複寫連結分析師] 工具，以協助調查複寫問題。  



<!--HONumber=Nov16_HO1-->

