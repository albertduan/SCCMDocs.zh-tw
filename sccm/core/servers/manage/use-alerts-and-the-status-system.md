---
title: "警示和狀態系統 | System Center Configuration Manager"
description: "設定警示，並使用狀態系統通知有關 Configuration Manager 部署的狀態。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: dda2e3af6ae14a949af5c70f300f8c7c6772e1a8


---
# <a name="use-alerts-and-the-status-system-for-system-center-configuration-manager"></a>使用 System Center Configuration Manager 的警示和狀態系統

*適用於：System Center Configuration Manager (最新分支)*

設定警示，並使用內建狀態系統通知有關 System Center Configuration Manager 部署的狀態。  


##  <a name="a-namebkmkstatusa-status-system"></a><a name="bkmk_Status"></a> 狀態系統  
 所有主要網站元件都會產生可提供網站和階層作業意見反應的狀態訊息。    這項資訊可讓您隨時掌握不同網站處理序的健全狀況。 您可以調整警示系統以略過已知問題，同時加速早期發現可能需要注意的其他問題。  

 Configuration Manager 狀態系統預設會使用適合多數環境的設定操作，而不需要進行任何設定。 不過，您可以進行下列設定：  

-   **狀態摘要器：** 您可以編輯每個網站的狀態摘要器，以控制產生下列四個摘要器之狀態指示器變更的狀態訊息頻率：  

    -   應用程式部署摘要器  

    -   應用程式統計資料摘要器  

    -   元件狀態摘要器  

    -   站台系統狀態摘要器  

-   **狀態篩選規則：** 您可以建立新的狀態篩選規則、修改規則的優先順序、停用或啟用規則，以及刪除每個站台中未使用的規則。  

    > [!NOTE]  
    >  狀態篩選規則不支援使用環境變數執行外部命令。  

-   **狀態報告：**您可以設定伺服器和用戶端元件報告來修改如何向 Configuration Manager 狀態系統報告狀態訊息，以及指定傳送狀態訊息的目的地。  

    > [!WARNING]  
    >  由於預設報告設定適用於大部分的環境，如需變更請務必小心謹慎。 選擇報告所有狀態詳細資料以提高狀態報告的層級時，您可以增加狀態訊息的處理量，這麼做也會增加 Configuration Manager 站台的處理負載。 如果降低狀態報告的層級，可能會使狀態摘要器的效果受到限制。  

因為狀態系統會維護每個站台的個別組態，所以您必須分別編輯每個站台。  

###  <a name="a-namebkmkconfigstatusa-procedures-for-configuring-the-status-system"></a><a name="bkmk_configstatus"></a> 設定狀態系統的程序  

##### <a name="to-configure-status-summarizers"></a>設定狀態摘要器  

1.  在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [站台設定] >[站台]，然後選取要設定狀態系統的站台。  

2.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [狀態摘要器] 。  

3.  在 [狀態摘要器]  對話方塊中，選取您要設定的狀態摘要器，然後按一下 [編輯]  ，開啟該摘要器的內容。 如果要編輯應用程式部署摘要器或應用程式統計資料摘要器，請繼續進行步驟 5。 如果要編輯元件狀態，請跳至步驟 6。 如果要編輯站台系統狀態摘要器，請跳至步驟 7。  

4.  開啟應用程式部署摘要器或應用程式統計資料摘要器的內容頁後，請執行下列步驟：  

    1.  在摘要器內容頁的 [一般]  索引標籤中設定摘要間隔，然後按一下 [確定]  關閉內容頁。  

    2.  按一下 [確定]  關閉 [狀態摘要器]  對話方塊並完成此程序。  

5.  開啟元件狀態摘要器的內容頁後，請執行下列步驟：  

    1.  在摘要器內容頁的 [一般] 索引標籤上設定複寫和閾值期間值。  

    2.  在 [閾值]  索引標籤上選取您要設定的 [訊息類型]  ，然後在 [閾值]  清單中按一下元件的名稱。  

    3.  在 [狀態閾值內容]  對話方塊中編輯警告和重大閾值的值，然後按一下 [確定] 。  

    4.  視需要重複執行步驟 6.b 和 6.c，完成後按一下 [確定]  關閉摘要器內容。  

    5.  按一下 [確定]  關閉 [狀態摘要器]  對話方塊並完成此程序。  

6.  開啟站台系統狀態摘要器的內容頁後，請執行下列步驟：  

    1.  在摘要器內容頁的 [一般] 索引標籤上設定複寫值和排程值。  

    2.  在 [閾值]  索引標籤上，指定 [預設閾值]  的值，設定重大和警告狀態顯示的預設閾值。  

    3.  若要編輯特定 [儲存物件] 的值，請從 [特定閾值]  清單中選取該物件，然後按一下 [內容]  按鈕，存取及編輯儲存物件的警告和重大閾值。 按一下 [確定]  以關閉儲存物件內容。  

    4.  若要建立新的儲存物件，請按一下 [建立物件]  按鈕並指定儲存物件值。 按一下 [確定]  以關閉物件內容。  

    5.  若要刪除儲存物件，請選取該物件，然後按一下 [刪除]  按鈕。  

    6.  視需要重複執行步驟 7.b 到 7.e 。 完成時，請按一下 [確定]  關閉摘要器內容。  

    7.  按一下 [確定]  關閉 [狀態摘要器]  對話方塊並完成此程序。  

##### <a name="to-create-a-status-filter-rule"></a>建立狀態篩選規則  

1.  在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [站台設定] >[站台]，然後選取要設定狀態系統的站台。  

2.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [狀態篩選規則] 。 [狀態篩選規則]  對話方塊隨即開啟。  

3.  按一下 [建立] 。  

4.  在 [建立狀態篩選規則精靈] 的 [一般]  頁面中，為新的狀態篩選規則指定名稱及該規則的訊息比對準則，然後按一下 [下一部] 。  

5.  在 [動作]  頁面中，指定狀態訊息符合篩選規則時應執行的動作，然後按 [下一步] 。  

6.  在 [摘要]  頁面中檢視新規則的詳細資料，然後完成精靈。  

    > [!NOTE]  
    >  Configuration Manager 只會要求新的狀態篩選規則必須要有名稱。 如果已建立規則但並未指定任何狀態訊息處理準則，則此狀態篩選規則不會有任何作用。 此行為可讓您在設定每個規則的狀態篩選準則之前建立及組織規則。  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>修改或刪除狀態篩選規則  

1.  在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [站台設定] >[站台]，然後選取要設定狀態系統的站台。  

2.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [狀態篩選規則] 。  

3.  在 [狀態篩選規則]  對話方塊中選取要修改的規則，然後執行下列任一動作：  

    -   按一下 [增加優先順序]  或 [降低優先順序]  ，以變更該狀態篩選規則的處理順序。 接著選取另一個動作，或移至本程序的步驟 8 以完成此工作。  

    -   按一下 [停用]  或 [啟用]  以變更規則的狀態。 變更規則的狀態後，請選取另一個動作，或移至本程序的步驟 8 以完成此工作。  

    -   如果要刪除此站台的狀態篩選規則，請按一下 [刪除]  ，然後按一下 [是]  確認該動作。 刪除規則後，請選取另一個動作，或移至本程序的步驟 8 以完成此工作。  

    -   如果要變更狀態訊息規則的準則，請按一下 [編輯]  ，然後繼續進行本程序的步驟 5。  

4.  在狀態篩選規則內容對話方塊的 [一般]  索引標籤中，修改規則和訊息比對準則。  

5.  在 [動作]  索引標籤中，修改狀態訊息符合篩選規則時應執行的動作。  

6.  按一下 [確定]  儲存變更。  

7.  按一下 [確定]  關閉 [狀態篩選規則]  對話方塊。  

##### <a name="to-configure-status-reporting"></a>設定狀態報告  

1.  在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [站台設定] > [站台]，然後選取要設定狀態系統的站台。  

2.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [設定站台元件] 然後選取 [狀態報告] 。  

3.  在 [狀態報告元件內容]  對話方塊中，指定您要報告或記錄的伺服器和用戶端元件狀態訊息：  

    1.  設定 [報告]，將狀態訊息傳送至 Configuration Manager 狀態訊息系統。  

    2.  設定 [記錄]  將狀態訊息的類型和嚴重性寫入 Windows 事件記錄檔。  

4.  按一下 [ **確定**]。  

###  <a name="a-namebkmkmonitorsystemstatusa-monitor-the-status-system-of-configuration-manager"></a><a name="BKMK_MonitorSystemStatus"></a> 監視 Configuration Manager 的狀態系統  
 Configuration Manager 中的 [系統狀態] 概述階層中的一般站台作業和站台伺服器作業。 它可顯示站台系統伺服器或元件的作業問題，而且您可以使用系統狀態檢閱不同 Configuration Manager 作業的特定詳細資料。 您可以從 Configuration Manager 主控台之 [監視] 工作區的 [系統狀態] 節點監視系統狀態。  

 大部分 Configuration Manager 站台系統角色和元件都會產生狀態訊息。 狀態訊息詳細資料會記錄在每個元件的操作記錄中，同時也會提交至站台資料庫，於其中摘要、並且在每個元件或站台系統健全狀況的一般彙總套件中呈現。 這些狀態訊息彙總套件可提供一般操作的資訊詳細資料，以及警告和錯誤詳細資料。 您可以設定觸發警告或錯誤的臨界值，並且微調系統以確保彙總套件資訊忽略不相關的已知問題，同時著重於伺服器上或您想調查之元件操作的實際問題。  

 系統狀態會做為站台資料複寫至階層中的其他站台，而不是做為全域資料。 這表示，您只能看見您的 Configuration Manager 主控台所連線的站台，以及該站台下任何子站台的狀態。 因此，當您檢視系統狀態時，請考慮將您的 Configuration Manager 主控台連線至階層中的頂層站台。  

 利用下表識別不同的系統狀態檢視以及各檢視的使用時機。  

|節點|詳細資訊|  
|----------|----------------------|  
|站台狀態|利用此節點檢視各站台系統狀態的彙總套件，檢閱每部站台系統伺服器的健全狀況。 站台系統健全狀況是由您在 [站台系統狀態摘要器] 中為每個站台設定的臨界值所決定。<br /><br /> 您可以檢視每個站台系統的狀態訊息、設定狀態訊息的臨界值，以及使用 [Configuration Manager Service Manager] 管理站台系統上元件的操作。|  
|元件狀態|使用此節點檢視每個 Configuration Manager 元件狀態的彙總套件，以檢閱元件的操作健全狀況。 元件健全狀況是由您在 [元件狀態摘要器] 中為每個站台設定的臨界值所決定。<br /><br /> 您可以檢視每個元件的狀態訊息、設定狀態訊息的臨界值，以及使用 [Configuration Manager Service Manager] 管理元件的操作。|  
|衝突的記錄|利用此節點檢視可能有衝突記錄之用戶端的狀態訊息。<br /><br /> Configuration Manager 會使用硬體識別碼嘗試識別可能重複的用戶端，並發出衝突記錄的警示。 例如，如果您需要重新安裝電腦，則硬體識別碼會相同，但 Configuration Manager 使用的 GUID 可能會變更。|  
|狀態訊息查詢|利用此節點查詢特定事件的狀態訊息和相關詳細資料。 您可以使用狀態訊息查詢尋找與特定事件相關的狀態訊息。<br /><br /> 您可以經常使用狀態訊息查詢識別特定元件、作業或 Configuration Manager 物件何時經過修改，以及用來進行修改的帳戶。 例如，您可以執行 [已建立、修改或刪除的集合]  的內建查詢，識別特定集合的建立時間以及用來建立集合的使用者帳戶。|  

####  <a name="a-namebkmkmanagestatusa-manage-site-status-and-component-status"></a><a name="bkmk_managestatus"></a> 管理站台狀態和元件狀態  
 利用下列資訊管理站台狀態和元件狀態：  

-   若要設定狀態系統的臨界值，請參閱 [設定狀態系統的程序](#bkmk_configstatus)。  

-   若要在 Configuration Manager 中管理個別元件，請使用 **Configuration Manager Service Manager**。  

####  <a name="a-namebkmkviewa-view-status-messages"></a><a name="bkmk_view"></a> 檢視狀態訊息  
 您可以檢視個別站台系統伺服器和元件的狀態訊息。  

 若要在 Configuration Manager 主控台中檢視狀態訊息，請選取特定站台系統伺服器或元件，然後按一下 [顯示訊息]。 當您檢視訊息時，可以選取檢視特定訊息類型或指定期間的訊息，也可以根據狀態訊息詳細資料篩選結果。  

##  <a name="a-namebkmkalertsa-alerts"></a><a name="bkmk_Alerts"></a> 警示  
 特定條件發生時，部分作業會產生 Configuration Manager 警示。  

-   通常警示是在發生您必須解決的錯誤時產生  

-   可能會因為某條件存在而產生警示來警告您，讓您能夠繼續監視此情況  

-   部分警示 (例如 Endpoint Protection 和用戶端狀態的警示) 是由您設定，其他警示則會自動予以設定  

-   您可以設定警示的訂閱，然後透過電子郵件傳送詳細資料，進而提高主要問題的識別度  

 使用下表尋找如何在 Configuration Manager 中設定警示和警示訂閱的相關資訊：  


|動作|更多資訊|  
|------------|----------------------|  
|設定集合的 Endpoint Protection 警示|請參閱[在 System Center Configuration Manager 中設定 Endpoint Protection](../../../protect/deploy-use/configure-endpoint-protection.md) 中的**如何在 Configuration Manager 中設定 Endpoint Protection 的警示**。|  
|設定集合的用戶端狀態警示|請參閱[如何在 System Center Configuration Manager 中設定用戶端狀態](../../../core/clients/deploy/configure-client-status.md)。|  
|管理 Configuration Manager 警示|請參閱本主題中的 [Management tasks for alerts](#BKMK_Manage) 一節。|  
|設定電子郵件警示訂閱|請參閱本主題中的 [Management tasks for alerts](#BKMK_Manage) 一節。|  
|監視警示|請參閱本主題中的 [監視警示](#BKMK_MonitorAlerts)|  

###  <a name="a-namebkmkmanagea-management-tasks-for-alerts"></a><a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>管理一般警示  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視] > [警示]，然後選取管理工作。  

  請參閱下表，了解選取管理工作前需要知道的資訊。  

|管理工作|詳細資料|  
    |---------------------|-------------|  
    |**設定 [報告]**|開啟 [*&lt;警示名稱*\> 內容] 對話方塊，您可以在其中修改所選取警示的名稱、嚴重性和閾值。 如果您變更警示的嚴重性，這項設定會影響 Configuration Manager 主控台中警示的顯示方式。|  
    |**編輯註解**|輸入所選取警示的註解。 這些註解會與警示一起顯示在 Configuration Manager 主控台中。|  
    |**延期**|在到達指定的日期之前暫止警示監視。 此時，會更新警示的狀態。<br /><br /> 您只能在啟用警示時將其延期。|  
    |**建立訂閱**|開啟 [新增訂閱]  對話方塊，您可以在其中建立所選取警示的電子郵件訂閱。|  

##### <a name="to-configure-endpoint-protection-alerts-for-a-collection"></a>設定集合的 Endpoint Protection 警示  

1.  擱置  

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>設定集合的用戶端狀態警示  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] >   [裝置集合]。  

2.  在 [裝置集合]  清單中，選取您要用於設定警示的集合，然後在 [首頁]  索引標籤的 [內容]  群組中按一下 [內容] 。  

    > [!NOTE]  
    >  您無法設定使用者集合的警示。  

3.  在 [*&lt;集合名稱*\> 內容] 對話方塊的 **[警示]** 索引標籤上，按一下 [新增]。  

    > [!NOTE]  
    >  您所指派到的安全性角色具有警示權限時，才會顯示 [警示]  索引標籤。  

4.  在 [新增集合警示]  對話方塊中，選擇您要在用戶端狀態閾值低於特定值時產生的警示，然後按一下 [確定] 。  

5.  在 [警示]  索引標籤的 [條件]  清單中選取每個用戶端狀態警示，然後指定下列資訊。  

    -   **警示名稱** - 接受預設名稱或輸入新的警示名稱。  

    -   **警示嚴重性** - 從下拉式清單中，選擇將顯示在 Configuration Manager 主控台中的警示等級。  

    -   **產生警示** - 指定警示的閾值百分比。  

6.  按一下 [確定] 關閉 [*&lt;集合名稱*\> 內容] 對話方塊。  

##### <a name="to-configure-email-notification-for-alerts"></a>設定警示的電子郵件通知  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視] > [警示] > [訂閱]。  

2.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [設定電子郵件通知] 。  

3.  在 [電子郵件通知元件內容]  對話方塊中，指定下列資訊：  

    -   **啟用警示的電子郵件通知**：選取此核取方塊可讓 Configuration Manager 使用 SMTP 伺服器傳送電子郵件警示。  

    -   **要傳送電子郵件警示之 SMTP 伺服器的 FQDN 或 IP 位址**：輸入您想要用於這些警示之電子郵件伺服器的完整網域名稱 (FQDN) 或 IP 位址和 SMTP 連接埠。  

    -   **SMTP 伺服器連線帳戶**：指定 Configuration Manager 用來連線電子郵件伺服器的驗證方法。  

    -   **電子郵件警示的寄件者地址**：指定用來傳送警示電子郵件的電子郵件地址。  

    -   **測試 SMTP 伺服器**：將測試電子郵件傳送給 [電子郵件警示的寄件者地址] 中所指定的電子郵件地址。  

4.  按一下 [確定]  儲存設定，並且關閉 [電子郵件設定元件內容]  對話方塊。  

##### <a name="to-subscribe-to-email-alerts"></a>訂閱電子郵件警示  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視] > [警示]。  

2.  選取警示，然後在 [首頁]  索引標籤的 [訂閱]  群組中按一下 [建立訂閱] 。  

3.  在 [新增訂閱]  對話方塊中，指定下列資訊：  

    -   **名稱**：輸入用來識別電子郵件訂閱的名稱。 您最多可以使用 255 個字元。  

    -   **電子郵件地址**：輸入您想要傳送警示的目標電子郵件地址。 您可以使用分號分隔多個電子郵件地址。  

    -   **電子郵件語言**：在清單中，指定電子郵件的語言。  

4.  按一下 [確定]  關閉 [新增訂閱]  對話方塊，並建立電子郵件訂閱。  

    > [!NOTE]  
    >  如果您展開 [警示]  節點，然後按一下 [訂閱]  節點，則可以在 [監視]  工作區中刪除和編輯訂閱。  

###  <a name="a-namebkmkmonitoralertsa-monitor-alerts"></a><a name="BKMK_MonitorAlerts"></a> 監視警示  
 您可以在 [監視]  工作區的 [警示]  節點中檢視警示。 警示會有下列其中一種警示狀態：  

-   **永不觸發**：尚未符合警示的條件。  

-   **作用中**：符合警示條件。  

-   **已取消**：不再符合作用中警示的條件。 此狀態表示造成警示的條件已獲得解決。  

-   **延後**：系統管理使用者已設定 Configuration Manager 稍後再評估警示的狀態。  

-   **已停用**：系統管理使用者已停用警示。 警示為此狀態時，Configuration Manager 不會更新警示，即使警示的狀態改變。  

 您可以在 Configuration Manager 產生警示時，採取下列其中一個動作：  

-   解決造成警示的條件，例如，解決產生警示的網路問題或設定問題。 在 Configuration Manager 偵測到問題已不存在之後，警示的狀態會變更為 [取消]。  

-   如果警示為已知問題，您可以將警示延後一段特定時間。 此時 Configuration Manager 會將警示更新為其目前狀態。  

     您只能在警示為作用中時將其延後。  

-   您可以編輯警示的 [註解]  ，讓其他系統管理使用者得知您已注意到警示。 例如，您可以在註解中識別如何解決此條件、提供此條件目前狀態的相關資訊，或解釋延後警示的理由。  



<!--HONumber=Nov16_HO1-->

