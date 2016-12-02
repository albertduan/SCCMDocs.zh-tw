---
title: "主控台內更新 | System Center Configuration Manager"
description: "System Center Configuration Manager 會與 Microsoft 雲端進行同步處理以取得更新，讓您可在主控台內安裝這類更新。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: b9721737b4181d8f5e41224c3e2c32ae41647554


---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>安裝適用於 System Center Configuration Manager 的主控台內更新

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 會與 Microsoft 雲端服務進行同步處理以取得更新，讓您可在 Configuration Manager 主控台內安裝這類更新。

## <a name="get-available-updates"></a>取得可用的更新
只會針對您的階層，下載並提供適用於您的基礎結構和版本的更新。 根據您設定階層服務連接點的方式而定，此同步處理可以自動或手動執行︰

-   在 **線上模式**中，服務連接點會自動連線到 Microsoft 雲端服務，並下載適用的更新。  

     根據預設，Configuration Manager 每隔 24 小時就會檢查新的更新。 從 1602 版或更新版本起，您也可以在 Configuration Manager 主控台的 [系統管理] > [雲端服務] > [更新與服務] 節點中按一下 [檢查更新]，立即檢查更新。  

-   在**離線模式**中，服務連接點不會連線到 Microsoft 雲端服務，因此您必須手動[使用 System Center Configuration Manager 的服務連接工具](../../../core/servers/manage/use-the-service-connection-tool.md)，以下載並匯入可用的更新。  

> [!NOTE]  
>  您的主控台會匯入與 Microsoft 雲端服務進行同步處理時所取得的更新，以及使用 [更新註冊工具](http://technet.microsoft.com/library/mt691544.aspx) 安裝的頻外修正程式，供您選取以進行安裝。  

同步處理更新之後，您可以在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [雲端服務] > [更新與服務] 節點來檢視它們︰  

-   您尚未安裝的更新會顯示為 **[可用]**。

-   您已安裝的更新會顯示為 **[已安裝]**。  從 1606 版開始，只會顯示最近安裝的更新，您可以按一下功能區上的 [歷程記錄] 按鈕以檢視先前安裝的更新。



請先了解並規劃可能會影響這個站台系統角色設定方式的其他用途，再設定服務連接點：  

-   服務連接點用來上傳您站台的使用資訊。 這項資訊可協助 Microsoft 雲端服務找出適用於您基礎結構之目前版本的更新。 如需詳細資訊，請參閱 [System Center Configuration Manager 的診斷和使用方式資料](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)。  

-   您可以使用服務連接點搭配 Microsoft Intune 與 Configuration Manager 內部部署行動裝置管理功能，來管理裝置。 如需詳細資訊，請參閱[搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理 (MDM)](../../../mdm/plan-design/hybrid-mobile-device-management.md)。  

若要進一步了解下載更新時會發生什麼情況，請參閱：  

-   [流程圖 - 下載 System Center Configuration Manager 的更新](../../../core/servers/manage/download-updates-flowchart.md)。  

-   [流程圖 - System Center Configuration Manager 的更新複寫](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="permissions-to-view-and-manage-updates-and-features"></a>檢視及管理更新和功能的權限
在安裝版本 1606 之前，若要在主控台中檢視更新，您必須為使用者指派安全性角色，其中包括 **站台** 權限群組中的 **讀取**權限，以及 **全部**安全性範圍。 從更新 1606 開始，已導入以角色為基礎的新系統管理安全性類別，名稱為 **[更新套件]** ，其可授與在 Configuration Manager 主控台中檢視及管理更新的存取權限。    

**關於更新套件類別：**  
依預設， **[更新套件]** (SMS_CM_Updatepackages) 屬於下列內建安全性角色的一部分，並具有所列的權限︰
 -  具有**修改** 和 **讀取** 權限的 **系統高權限管理員** ：
    -   如果使用者具有此安全性角色和 **所有** 安全性範圍的存取權限，即可檢視更新、安裝更新、在安裝期間啟用功能，並在安裝好先前的更新之後啟用個別功能。
    - 如果使用者具有此安全性角色和 **預設** 安全性範圍的存取權限，即可檢視更新、安裝更新、在安裝期間啟用功能，並在安裝好更新之後，檢視已安裝更新的功能，但不能在安裝好先前的更新之後啟用相關功能。

- 具有**讀取** 權限的 **唯讀分析師** ：
  -  如果使用者具有此安全性角色和 **預設** 範圍的存取權，即可檢視更新，但不能安裝更新；可以在安裝好更新之後檢視功能，但不能加以啟用。

**更新和服務的必要權限摘要︰**   
  - 請使用已指派安全性角色的帳戶，並具有 **[更新套件]** 類別的 **修改** 和 **讀取** 權限。
  - 帳戶必須指派 **預設** 範圍。

**若只要檢視更新**：
  - 請使用已指派安全性角色的帳戶，並僅具有 **[更新套件]** 類別的 **讀取** 權限。
  - 帳戶必須指派 **預設** 範圍。

**若要在安裝更新後啟用功能︰**
  -   請使用已指派安全性角色的帳戶，並具有 **[更新套件]** 類別的 **修改** 和 **讀取** 權限。
  -  帳戶必須獲得 **所有** 範圍的指派。






##  <a name="a-namebkmkbeforeinstalla-before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> 安裝主控台內更新之前  
 在 Configuration Manager 主控台內安裝更新之前，請檢閱以下步驟︰  

###  <a name="a-namebkmkstep1a-step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> 步驟 1︰檢閱更新檢查清單  
在 Configuration Manager 主控台中安裝新的更新之前，請檢閱適用的更新檢查清單，以了解開始更新之前應採取的動作︰  

-   依據[升級至 System Center Configuration Manager](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) 的內容，升級至 1511    

-   從 1511 更新為 1602：請參閱[安裝 1602 更新的檢查清單](../../../core/servers/manage/checklist-for-installing-update-1602.md)

- 從 1511 或 1602 更新為 1606：請參閱[安裝 1606 更新的檢查清單](../../../core/servers/manage/checklist-for-installing-update-1606.md)  


###  <a name="a-namebkmkstep2a-step-2-test-the-database-upgrade-before-installing-an-update"></a><a name="bkmk_step2"></a> 步驟 2︰安裝更新之前，先測試資料庫升級  
在階層中安裝新的更新之前 (例如更新 1602)，您應該測試站台資料庫的升級。 您可使用名為 **testdbupgrade**的命令列選項，進行安裝更新到站台資料庫備份的測試。  

如果安裝更新失敗，您應不需像舊版 Configuration Manager 一樣執行站台復原，而可以「重試」更新安裝。 因此，儘管比起在過去的產品版本中，資料庫的測試升級變得較不重要，但它仍然是建議的步驟。  

##### <a name="to-run-testdbupgrade-before-installing-an-update"></a>安裝更新之前先執行 testdbupgrade  

1.  如果某個站台是執行您打算更新的目標版本，請從其中的 **CD.Latest** 資料夾，取得一組原始程式檔。 若要這麼做，您可能要先在實驗室或測試環境中安裝執行該版本 System Center Configuration Manager 的站台。  

     站台的 **CD.Latest** 資料夾會包含該版本的原始程式檔。 您必須使用這些原始程式檔來執行站台資料庫的測試升級。 如需詳細資訊，請參閱 [System Center Configuration Manager 的 CD.Latest 資料夾](../../../core/servers/manage/the-cd.latest-folder.md)。  

     例如，如果您的站台執行版本 1501，而您想要更新至 1602，就必須從已經升級至版本 1602 的站台中取得 CD.Latest 資料夾。 您通常可以在實驗室中安裝新的暫時站台，並將其升級至版本 1602，以利用必要的檔案來建立 CD.Latest 資料夾。  

2.  將 CD.Latest 資料夾複製到 SQL Server 上您將用來執行測試資料庫升級的位置 (請參閱後續步驟)。  

3.  建立您想要測試升級的站台資料庫備份，然後將該資料庫的複本還原至未裝載 Configuration Manager 站台的 SQL Server 執行個體。 SQL Server 必須使用與您站台資料庫相同的 SQL Server 版本。  

4.  還原資料庫複本後，從您自實驗室或測試環境中複製的 CD.Latest 資料夾執行 **安裝程式** 。 當您執行安裝程式時，請使用 **/TESTDBUPGRADE** 命令列選項。 如果裝載資料庫複本的 SQL Server 執行個體不是預設的執行個體，您還需要提供命令列引數，以識別裝載站台資料庫複本的執行個體。  

     例如，您想要升級資料庫名稱為 SMS_ABC 的站台資料庫。 您會將此站台資料庫的複本，還原到執行個體名稱為 DBTest 的受支援 SQL Server 執行個體。 若要測試此站台資料庫複本的升級，請使用下列命令列： **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     您可在 System Center Configuration Manager 來源媒體的下列位置找到 Setup.exe：**SMSSETUP\BIN\X64**。  

5.  在您執行資料庫升級測試的 SQL Server 執行個體上，監視位於系統磁碟機根目錄中的 ConfigMgrSetup.log，以了解進度及成功與否：  

     如果測試升級失敗，請解決與站台資料庫升級失敗相關的問題，建立新的站台資料庫備份，然後再測試新的站台資料庫複本的升級。  

     順利進行所有程序後，便可以刪除資料庫複本。  

    > [!NOTE]  
    >  不支援還原您用於測試升級的站台資料庫複本，以當成任何站台上的站台資料庫使用。  

###  <a name="a-namebkmkstep3a-step-3-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step3"></a> 步驟 3︰安裝更新之前，先執行必要條件檢查工具  
安裝更新之前，請考慮執行該更新的必要條件檢查。 如果您在安裝更新之前先執行必要條件：  

-   更新檔案會在實際安裝更新之前複寫到其他站台  

-   必要條件檢查將會在您選擇安裝更新時再次自動執行  

稍後當您安裝更新時，您可以選擇設定更新以略過必要條件檢查警告。  

##### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>安裝更新之前先執行必要條件檢查工具  

1.  在 Configuration Manager 主控台中，前往 [系統管理] > [雲端服務] > [更新與服務]。  

2.  以滑鼠右鍵按一下您想要執行必要條件檢查的更新套件。  

3.  選擇 **[執行必要條件檢查]**。  您可以檢視  

     當您執行必要條件檢查時，更新的內容會複寫到子站台。  您可以檢視站台伺服器上的 **distmgr.log** ，以確認該內容複寫成功。  

4.  若要檢視檢查的結果，可在 Configuration Manager 主控台中，移至 [監視] > [更新與服務狀態]，然後尋找必要條件狀態。 您也可以檢視站台伺服器上的 ConfigMgrPrereq.log，來取得更多詳細資料。  



##  <a name="a-namebkmkinstalla-install-in-console-updates"></a><a name="bkmk_install"></a> 安裝主控台內更新  
 當您準備好從 Configuration Manager 主控台內安裝更新時，請先由階層的頂層站台開始。 這可能是管理中心網站或獨立主要站台。  

 建議您規劃在正常營業時間以外針對各個站台安裝更新，在這些時間內安裝更新的程序與其重新安裝站台元件和站台系統角色的動作，對您的商務營運所產生的影響最小。  

-   當管理中心網站完成安裝更新之後，子主要站台就會自動啟動更新。 這是預設的建議程序。 不過，當主要站台安裝更新時，您可以使用[站台伺服器的維護時段](#bkmk_ServiceWindow)來進行控制。  

-   當主要父站台更新完成之後，您必須從 Configuration Manager 主控台內手動更新次要站台。 不支援次要站台伺服器的自動更新。  

-   當您在站台更新之後使用 Configuration Manager 主控台時，系統會提示您更新主控台。  

-  站台伺服器已成功完成更新安裝之後，便會自動更新所有適用的站台系統角色。  唯一要注意的一點是關於發佈點的下列事項：
  - 由於更新 1606 導入了一些變更，因此在已執行 1606 版或更新版本的站台上進行更新安裝時，不會再將所有發佈點同時設為離線以進行更新。 反之，站台伺服器會使用站台的內容發佈設定，逐一將更新發佈至發佈點子集。 這樣一來，只有部分發佈點會設為離線以安裝更新。 如此可讓還沒有開始更新或已完成更新的發佈點保持線上狀態，以提供內容給用戶端。


###  <a name="a-namebkmkoverviewa-overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> 主控台內更新安裝概觀  
**1.開始安裝更新時**  
您會看到更新精靈，其中顯示更新所適用的產品區域清單。  

-   在精靈的 **[一般]** 頁面中，您可以設定 **[必要條件警告]**。  
      -   必要條件錯誤一律會停止安裝更新。 您必須先解決錯誤，才能成功重試更新安裝。 如需詳細資訊，請參閱 [重試失敗更新的安裝](#bkmk_retry) 。  

    -   必要條件警告也會停止安裝更新。 您應該先解決警告，然後重試安裝更新。   如需詳細資訊，請參閱 [重試失敗更新的安裝](#bkmk_retry) 。  
    -   選取 **[忽略任何必要條件檢查警告並安裝此更新 (不管遺漏的必要項)]**選項、設定更新安裝的條件以忽略必要條件警告，並允許繼續安裝更新。 如果您未選取此選項，更新安裝將會在遇到警告時停止。 除非您先前已針對某個站台執行必要條件檢查並解決必要條件警告，否則不建議使用此選項。  

      從版本 1606 開始， **[系統管理]** 和 **[監視]** 工作區的 [更新與服務] 節點，其功能區上皆包含名為 **[忽略必要條件警告]**的按鈕。 當更新套件無法完成安裝時，會產生必要條件檢查警告，此按鈕即變成可用。  比方說，如果您從 [更新精靈] 安裝更新時未使用忽略必要條件警告的選項，但該更新安裝突然停止並處於必要條件警告 (但不含錯誤) 的狀態中，您可以稍後選取功能區上的 **[忽略必要條件警告]** ，觸發自動接續安裝要忽略必要條件警告的這項更新。  使用此選項時，會在幾分鐘後自動繼續安裝更新。



-   當有適用於 Configuration Manager 用戶端的更新時，即會顯示特定選項，讓您透過有限的用戶端來測試用戶端更新。 如需詳細資訊，請參閱[如何測試 System Center Configuration Manager 的進入生產階段前集合用戶端升級](../../../core/clients/manage/upgrade/test-client-upgrades.md)。  

**2.安裝更新期間**  
在安裝更新期間，Configuration Manager 會執行下列動作：  

-   重新安裝站台系統角色或 Configuration Manager 主控台等任何受影響的元件。  

-   依據您為試驗用戶端以及 [自動用戶端升級](https://technet.microsoft.com/library/mt627885.aspx)所選的項目，來管理用戶端的更新  

-   不需要在更新期間重新啟動站台系統伺服器 (除非已安裝 .NET 做為站台系統角色必要條件的一部分)  

> [!TIP]  
>  安裝更新之後，Configuration Manager 也會更新 CD.Latest 資料夾 (在站台復原期間使用)。  

**3.安裝更新時，監視更新的進度**  
使用下列動作來監視進度︰  

-   在 Configuration Manager 主控台中：[系統管理] > [雲端服務] > [更新與服務] 節點。 此節點會顯示所有更新套件的安裝狀態。


-   在 Configuration Manager 主控台中：[監視] > [概觀] > [更新與服務狀態] 節點。 此節點只會顯示目前正在安裝之更新套件的安裝狀態。  

    從版本 1606 開始，更新套件安裝細分成下列階段，以簡化監視。 現在，下列每個階段都提供額外的詳細資料，包括應檢視哪些記錄檔案以取得詳細資訊︰  
    -   **下載** (僅適用於服務連接點的站台系統角色安裝所在的頂層站台)
    -   **複寫**
    - **必要條件檢查**
    - **安裝**

-   您可以檢視 **&lt;ConfigMgr_Installation_Directory>\Logs\\** 中的 **CMUpdate.log** 檔案。  

**4.安裝更新完成時**  
當第一個站台更新完成安裝之後︰  

-   子主要站台將會自動安裝更新。 不需要進行其他動作。  

-   次要站台必須從 Configuration Manager 主控台內手動更新。
> [!TIP]
> 雖然主控台不會顯示次要站台的版本，但您可以使用 Configuration Manager SDK 來確認站台版本。 請參閱 [SMS_Site Server WMI Class](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx) (SMS_Site Server WMI 類別)。


-   在階層中的所有站台都更新至新版本之前，您的階層仍會以混合版本模式運作。 如需詳細資訊，請參閱 [Interoperability between different versions of System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md)。  

**5. 更新 Configuration Manager 主控台**  
在管理中心網站或主要站台更新之後，連線至該站台的每個 Configuration Manager 主控台也必須更新。 系統會提示您更新主控台︰  

-   當您開啟主控台時  

-   當您在開啟的主控台中瀏覽至新節點時  

我們建議您立即安裝更新且不延遲。  

當主控台更新完成之後，您可以確認主控台和站台版本是正確的。 移至主控台左上角的 **[關於 System Center Configuration Manager]** ，其中會顯示新的站台和主控台版本。  

###  <a name="a-namebkmktoptiera-to-start-the-update-installation-at-the-top-tier-site"></a><a name="bkmk_toptier"></a> 在頂層站台上開始安裝更新  
在階層的頂層站台上，於 Configuration Manager 主控台中，移至 [系統管理] > [雲端服務] > [更新與服務]、選取某項**可用**更新，然後按一下 [安裝更新套件]。  

###  <a name="a-namebkmksecondarya-to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> 在次要站台上開始安裝更新  
在更新次要站台的父主要站台之後，您即可從 Configuration Manager 主控台內更新次要站台。  若要這樣做，您可以使用 **[升級次要站台精靈]**。  

1.  在 Configuration Manager 主控台中，移至 [系統管理] > [站台設定] > [站台]、選取要更新的站台，然後在 [常用] 索引標籤的 [站台] 群組中，按一下 [升級]。  

2.  按一下 **[是]** 以開始更新次要站台。  

若要監視次要站台上的更新安裝，可選取次要站台伺服器，然後在 [常用] 索引標籤的 [站台] 群組中，按一下 **[顯示安裝狀態]**。 您也可以在主控台顯示中新增 **[版本]** 欄，讓您能夠檢視每個次要站台的版本。  

在次要站台成功更新之後，如果主控台中的狀態未重新整理或顯示更新失敗，您可以使用 [重試安裝] 選項。 這個選項不會重新為次要站台安裝已成功安裝的更新，但會強制主控台更新狀態。


##  <a name="a-namebkmkretrya-retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> 重試失敗更新的安裝  
當更新安裝失敗時，檢閱主控台內的回饋，以找出適用於警告和錯誤的解決方式。  您也可以檢視站台伺服器上的 ConfigMgrPrereq.log，來取得更多詳細資料。 重試安裝更新之前，您必須先解決錯誤且應解決警告。  

當您準備好要重試安裝更新時，請選取失敗的更新，然後選取適用的選項。 重試更新安裝的行為取決於您啟動重試的節點和所使用的重試選項而定：  

1.  **重試階層安裝︰**  
當更新處於下列其中一種狀態時，您可以重試整個階層的更新安裝︰  

    -   已通過必要條件檢查但有一或多個警告，而且未在 [更新精靈] 中設定略過必要條件檢查警告的選項 (在 [更新與服務] 節點中， **[忽略必要條件警告]** 的更新值是 **[否]**)   
    -   必要條件失敗    
    -   安裝失敗
    -   將內容複寫至站台失敗   

    移至 **[系統管理]** > **[雲端服務]** > **[更新與服務]**、選取更新，然後按一下下列其中一項：  

    -   **[重試]** - 當您從這個節點執行 [重試] 時，更新安裝會再次啟動，並自動忽略必要條件警告。 它也會重新複寫更新的內容 (如果先前複寫失敗的話)。
    - **[忽略必要條件警告]** - 從版本 1606 起，如果因為警告導致更新安裝突然停止，您可以按一下 [忽略必要條件警告]。 此動作會在幾分鐘後繼續安裝更新，並使用忽略必要條件警告的選項。   

2.  **重試站台的安裝︰**  
 當更新處於下列其中一種狀態時，您可以在特定站台上重試更新安裝︰  

    -   已通過必要條件檢查但有一或多個警告，而且未在 [更新精靈] 中設定略過必要條件檢查警告的選項 (在 [更新與服務] 節點中， **[忽略必要條件警告]** 的更新值是 **[否]**)  
    -   必要條件失敗    
    -   安裝失敗    

    移至 **[監視]** > **[概觀]** > **[站台服務狀態]**、選取更新，然後按一下下列其中一項：

       - **[重試]** - 當您從這個節點執行 [重試] 時，只會重新啟動該站台的更新安裝。 但這項重試與從 [更新與服務] 節點中執行 [重試] 不同，其不會忽略必要條件警告。
       -    **[忽略必要條件警告]** - 從版本 1606 起，如果因為警告導致更新安裝突然停止，您可以按一下 [忽略必要條件警告]。 此動作會在幾分鐘後繼續安裝更新，並使用忽略必要條件警告的選項。

##  <a name="a-namebkmkaftera-after-a-site-installs-an-update"></a><a name="bkmk_after"></a> 當站台安裝更新之後  
使用下列檢查清單，完成站台更新之後所做的一般工作和設定︰  

**確認站台對站台複寫正在作用中：**在  Configuration Manager 主控台中，移至下列位置來檢視狀態，並確認複寫正在作用中：  

-   **[監視]** > **[概觀]** > **[站台階層]**  

-   **[監視]** > **[概觀]** > **[資料庫複寫]**  

如需詳細資訊，請參閱[監視 System Center Configuration Manager 的階層及複寫基礎結構](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md)和[關於複寫連結分析師](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA)。  

 **確認站台伺服器和遠端站台系統伺服器已重新啟動 (如有必要)︰** 檢閱您的站台基礎結構，並確保適用的站台伺服器和站台系統伺服器 (站台伺服器的遠端) 已成功重新啟動。  通常只有在 Configuration Manager 將 .NET 安裝為站台系統角色的必要項目時，才預期會有這種行為。  

 **更新獨立 Configuration Manager 主控台︰**確保所有遠端的 Configuration Manager 主控台都會更新為相同的版本。 系統會在下列時機提示您更新主控台︰  

-   您在主控台中瀏覽至新節點  

-   當您開啟主控台時  

**在主要站台上重新設定管理點的資料庫複本：** 如果您在主要站台上使用管理點的資料庫複本，就必須先解除安裝資料庫複本，才能更新站台。 更新主要站台之後，請重新設定管理點的資料庫複本。 如需詳細資訊，請參閱 [System Center Configuration Manager 的管理點資料庫複本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

**重新設定您在更新之前停用的任何資料庫維護工作：**如果您已在更新之前停用站台上資料庫之 [System Center Configuration Manager 的維護工作](../../../core/servers/manage/maintenance-tasks.md)，請使用更新前的相同設定值，在站台上重新設定這些工作。  

**升級用戶端：**如需如何升級現有用戶端以及如何安裝新用戶端的資訊，請參閱[如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

**額外的設定︰** 檢閱您在開始更新之前所做的變更，然後將這些設定還原至您的站台和階層。  

##  <a name="a-namebkmkoptionsa-enable-optional-features-from-updates"></a><a name="bkmk_options"></a> 從更新啟用選擇性功能  
當您安裝其中包含一或多個選擇性功能的更新時，將有機會在您的階層中啟用這些功能。  您可以在安裝更新期間執行此動作，或者稍後返回主控台並啟用選擇性功能。

若要檢視可用功能及其狀態，可在主控台中瀏覽至 **[系統管理]** > **[雲端服務]** > **[更新與服務]** > **[功能]**。

若功能不是選擇性的，就會自動安裝，且不會出現在 **[功能]** 節點中。  

##  <a name="a-namebkmkprereleasea-use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> 使用更新的發行前版本功能
從 1606 開始，您必須同意使用 System Center Configuration Manager 中的發行前版本功能，才可以選取功能並啟用其用法。  

發行前版本功能會包含在產品內，以便在生產環境中進行早期測試，但不應視為生產環境就緒。

若要表示同意，可在主控台中瀏覽至 **[系統管理]** > **[站台設定]** > **[站台]**，然後選取 **[階層設定]**。 在 **[一般]** 索引標籤上，選取 **[同意使用發行前版本功能]**。
 -  每個階層的同意都是一次性且無法取消的動作  
 -  只有在您同意之後，才能啟用更新 1606 或以上更新版本所隨附的新發行前版本功能

 > [!NOTE]
 > 如果您在安裝更新 1606 之前已啟用更新 1602 的發行前版本功能，則在安裝 1606 之後，這些功能仍然可供使用 (即使您未同意使用發行前版本功能亦同)。

若階層執行 1606 版或更新版本，之後您再安裝包含發行前版本功能的更新，則 [更新與服務精靈] 中會顯示這些功能與一般功能：
  - **如果您已同意：** 安裝更新時，您即可透過 [更新與服務精靈] 啟用發行前版本功能。 若要這樣做，請選取發行前版本功能 (方法和選取任何其他功能相同)。     

    您可以稍後透過主控台的 **[系統管理]** > **[雲端服務]** > **[更新與服務]** > **[功能]** 節點，啟用發行前版本功能。 若要這樣做，請在 [功能] 節點中選取功能，然後按一下 **[開啟]** (如果您尚未同意，這個選項會呈現灰色且無法使用)。  
  -   **如果您尚未同意︰** 安裝更新時，[更新與服務精靈] 中會顯示發行前版本功能，但為灰色且無法啟用。 更新安裝完成後，您可以在 [功能] 節點中檢視這些功能，但只有在 [階層設定] 中表示同意之後，才能加以啟用。

 > [!TIP]
 > 若您正在安裝更新 1606，[更新與服務精靈] 中不會顯示隨附於更新 1606 的發行前版本功能，此時亦無法啟用。 要等 1606 更新安裝完成之後，您才可以在 [功能] 節點中檢視隨附的發行前版本功能。

如果您已授權獨立主要站台，並藉由安裝新的管理中心網站來擴充階層，則必須於管理中心網站再授權一次。

**下列為可用的發行前版本功能：**

 |功能                    |已新增為發行前版本 |已新增為完整功能 |  
|----------------------------|---------------------|------------------------|
| Microsoft Operations Management Suite (OMS) 連接器  | [1606 版](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![尚未提供此服務](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 服務叢集感知集合 (用於服務伺服器群組)| [版本 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#bkmk_servergroups)|![尚未提供此服務](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|條件式存取由 System Center Configuration Manager 所管理的電腦 | [版本 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     |![尚未提供此服務](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)                        |




##  <a name="a-namebkmkservicewindowa-service-windows-for-site-servers"></a><a name="bkmk_ServiceWindow"></a> 站台伺服器的維護時段  
您可在站台伺服器上設定維護時段，以控制何時將 Configuration Manager 的基礎結構更新套用至該站台伺服器。  每個站台伺服器支援多個視窗，包含可用於安裝由此站台伺服器所有設定的視窗組合所決定之基礎結構更新的視窗。  

**若要設定服務視窗︰**  

1.  在 Configuration Manager 主控台中，依序開啟 [系統管理] > [站台設定] > [站台]，然後選取要設定維護時段的站台伺服器。  

2.  接著，編輯站台伺服器的 **[內容]** ，然後選取 **[維護時段]** 索引標籤，您可在此為該站台伺服器設定一或多個維護時段。  

##  <a name="a-namebkmkfaqa-why-dont-i-see-certain-updates-in-my-console"></a><a name="bkmk_faq"></a> 為什麼我在主控台中看不到特定的更新？  
 如果您找不到特定的更新，或者與 Microsoft 雲端服務成功同步處理之後在主控台中找不到任何更新，這可能是因為︰  

-   更新需要您的基礎結構未使用的設定，或者目前的產品版本未滿足接收更新的必要條件。  

     如果您認為已具備某項更新的必要設定或符合其他必要條件，但仍缺少該項更新，請確認您的服務連接點處於線上模式，然後使用 [更新與服務] 節點中的 **[檢查更新]** 選項來強制執行檢查。  若您處於離線模式，就必須使用服務連線工具，手動與雲端服務進行同步。  

-   您的帳戶缺少以角色為基礎的正確系統管理權限，無法在 Configuration Manager 主控台中檢視更新。

    請參閱本主題中的[管理更新的權限](../../../core/servers/manage/install-in-console-updates.md#Permissions-to-view-and-manage-updates-and-features)，以了解如何從主控台內檢視更新並啟用功能的必要權限。



<!--HONumber=Nov16_HO1-->


