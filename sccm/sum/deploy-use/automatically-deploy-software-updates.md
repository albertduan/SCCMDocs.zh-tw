---
title: "自動部署軟體更新 | Microsoft Docs"
description: "經由將新的更新新增到與現用部署相關聯的更新群組，或使用 ADR，來自動部署軟體更新。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: 804a9d7a32cfbdb498c6748c5d99a1874261c231
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_AutoDeploy"></a> 自動部署軟體更新  

*適用於：System Center Configuration Manager (最新分支)*

 您可經由將新的軟體更新新增到與現用部署相關聯的更新群組，或使用自動部署規則 (ADR)，來自動部署軟體更新。 您通常會使用 ADR 部署每月軟體更新 (一般稱為「週二修補程式日」更新) 以及管理定義更新。 如果需要協助來判斷哪種部署方法最適合您，請參閱[部署軟體更新](deploy-software-updates.md)

##  <a name="BKMK_AddUpdatesToExistingGroup"></a> 將軟體更新新增至已部署的更新群組  
建立並部署軟體更新群組之後，您可以將軟體更新新增至更新群組，然後就會自動部署軟體更新。  

> [!IMPORTANT]  
>  將軟體更新新增到已經部署完成的現有軟體更新群組時，將額外軟體更新新增到部署前可能要花費幾分鐘時間。  

利用下列程序將軟體更新新增到現有更新群組內。  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>將軟體更新新增至現有軟體更新群組  

1.  在 Configuration Manager 主控台中，巡覽至 [軟體程式庫] > [概觀] > [軟體更新]。  

2.  選取要新增到新軟體群組的軟體更新。  

3.  在 [首頁]  索引標籤的 [更新]  群組中，按一下 [編輯成員資格] 。  

4.  選取您要新增軟體更新作為成員的軟體更新群組。  

5.  按一下 [軟體更新群組]  節點，以顯示軟體更新群組。  

6.  按一下軟體更新群組，然後在 [首頁]  索引標籤的 [更新]  群組中按一下 [顯示成員]  ，顯示此群組的軟體更新清單。  

##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> 建立自動部署規則 (ADR)  
您可以使用 ADR 來自動核准並部署軟體更新。 每次執行規則或在現有群組中新增軟體更新時，您都可以在新的軟體更新群組中加入軟體更新。 在現有群組執行規則並加入軟體更新時，該規則會從群組中移除所有軟體更新，然後新增符合您定義群組之準則的軟體更新。 例如，若要每天執行 ADR，以尋找新發行的軟體更新並將其部署至用戶端，您必須選擇建立新軟體更新群組的選項，而非在現有群組中新增軟體更新。  

> [!WARNING]  
>  第一次建立 ADR 前，請驗證已經在網站上完成軟體更新同步處理。 在您執行非英語版本的 Configuration Manager 時，這個步驟特別重要，因為進行首次同步處理前，會以英文顯示軟體更新分類。軟體更新同步處理完成後，則會以本地化語言顯示。 進行同步處理軟體更新前建立的規則，在同步處理後可能無法正確運作，因為文字字串會不相符。  

 使用下列程序建立 ADR。  

#### <a name="to-create-an-adr"></a>建立 ADR  

1.  在 Configuration Manager 主控台中，巡覽至 [軟體程式庫][概觀] > [軟體更新] > [自動部署規則]。  

2.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立自動部署規則] 。 [建立自動部署規則精靈] 隨即開啟。  

3.  在 [一般]  頁面，設定以下設定：  

    -   **名稱**：指定 ADR 的名稱。 名稱必須是唯一的，且能協助描述規則目標，並能在 Configuration Manager 站台上從其他名稱中輕易找出。  

    -   **描述**：指定 ADR 的描述。 描述應提供部署規則的概觀，以及其他可協助您在 Configuration Manager 站台內找出並區分的規則。 描述欄位是選用欄位，長度限制為 256 字元，預設為空白值。  

    -   **選取部署範本**：指定是否要套用先前儲存的部署範本。 您可以設定部署範本，納入多個可以在建立 ADR 時使用的常見軟體更新部署內容。 這些範本可協助確保類似部署的一致性，同時節省時間。  

         您可以從 [自動部署規則精靈] 的內建軟體更新部署範本中選取。 [定義更新]  範本提供部署定義軟體更新時使用的一般設定。 [周二修補]  範本提供每月部署軟體更新時使用的一般設定。  

    -   **集合**：指定部署用的目標集合。 集合內的成員會收到部署中定義的軟體更新。  

    -   決定要將軟體更新新增至新的或現有軟體更新群組。 在大多數狀況下，執行 ADR 時，您可能會選擇建立新的軟體更新群組。 不過，若以更頻繁的排程執行規則的話，您應選擇使用現有群組。 例如，若您要每天執行定義更新，那麼您可以將軟體更新新增至某個現有軟體更新群組。  

    -   **在執行此規則後啟用部署**：指定執行 ADR 後，是否要啟用軟體更新部署。 關於此規格，請考慮下列各項：  

        -   啟用部署時，會將符合規則中定義之準則的軟體更新新增到某個軟體更新群組，必要時會下載軟體更新內容，而內容會複製到指定的發佈點，軟體更新則會在目標集合的用戶端上部署。  

        -   您不啟用部署時，會將符合規則中定義之準則的軟體更新新增至某個軟體群組，並設定軟體更新部署原則，但不會將軟體更新下載或部署至用戶端。 這個狀況能提供您需要的時間以準備部署軟體更新，請確認符合準則的軟體更新是正確的，並於稍後啟用部署。  

4.  在 [部署設定] 頁面，指定以下設定：  

    -   **使用網路喚醒來喚醒用戶端進行必要的部署**：指定是否於期限啟用網路喚醒，將喚醒封包傳送到在部署中需要一或多個軟體更新的電腦。 安裝期限時處於睡眠模式的任何電腦都會喚醒，如此即可起始軟體更新安裝。 在部署中處於睡眠狀態且不需要任何軟體更新的用戶端並不會啟動。 根據預設不會啟用此設定。  

        > [!WARNING]  
        >  在您可使用此選項前，必須針對網路喚醒設定電腦和網路。  

    -   **詳細等級**：針對由用戶端電腦報告的狀態訊息，指定詳細等級。  

        > [!IMPORTANT]  
        >  部署定義更新時，請將詳細等級設定至 [僅錯誤]  ，僅在定義更新無法傳遞給用戶端時，讓用戶端回報狀態訊息。 否則，用戶端會回報一大批的狀態訊息，可能影響到網站伺服器的效能。  

    -   **授權條款設定**：指定是否使用相關聯的授權條款自動部署軟體更新。 某些軟體更新會包含授權條款，如 Service Pack。 自動部署軟體更新時，不會顯示授權條款，也沒有接受授權條款的選項。 您可以選擇不論相關聯授權條款為何，或僅部署沒有相關聯授權條款的軟體更新，皆自動部署所有軟體更新。  

        > [!NOTE]  
        >  若要檢閱軟體更新的授權條款，您可以在 [軟體程式庫]  工作區 [所有軟體更新]  節點內選取軟體更新，然後在 [首頁]  索引標籤上的 [更新]  群組中按一下 [檢閱授權] 。  
        >   
        >  若要找出具備相關聯授權條款的軟體更新，您可以在 [所有軟體更新]  節點的結果窗格中新增 [授權條款]  欄，然後按一下該欄的標頭，即可依具備授權條款的軟體更新來排序。  

5.  在 [軟體更新] 頁面上，替 ADR 所擷取並新增至軟體更新群組的軟體更新設定準則。  

    > [!IMPORTANT]  
    >  ADR 中軟體更新的限制為 1000 個軟體更新。 若要確保您在本頁指定的準則少於 1000 個軟體更新，請考慮在 [軟體程式庫]  工作區內 [所有軟體更新]  節點上設定相同準則。  

    > [!NOTE]
    > 從 Configuration Manager 版本 1610 開始，您可以在自動部署規則中依軟體更新的內容大小進行篩選。 例如，您可以將 [內容大小 (KB)] 篩選設定為 [< 2048]，僅下載小於 2MB 的軟體更新。 使用此篩選可防止自動下載大型軟體更新，以在網路頻寬有限時，提供簡化 Windows 下層服務的更佳支援。 如需詳細資訊，請參閱 [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)(Configuration Manager 及下層作業系統上的簡化 Windows 服務)。

6.  在 [評估排程] 頁面上，指定是否要啟用 ADR 使其按照排程執行。 啟用時，按一下 [自訂]  設定週期性排程。  

    > [!IMPORTANT]  
    >  此時會顯示軟體更新點同步處理排程，協助您決定評估排程的頻率。 切勿將評估排程的頻率設定為超過軟體更新同步處理排程。 排程的開始時間設定是以執行 Configuration Manager 主控台之電腦的本機時間為根據。  

    > [!NOTE]  
    >  若要手動執行 ADR，請選取規則，然後按一下自動部署規則  群組內 首頁  索引標籤上的 立即執行  。 手動執行 ADR 前，請驗證從上次執行規則後，已經執行過的軟體更新同步處理。  

    > [!IMPORTANT]  
    >  ADR 評估一天最多可執行 3 次。  

7.  在 [部署排程] 頁面，指定以下設定：  

    -   **排程評估**：指定 Configuration Manager 是否要使用 UTC 或執行 Configuration Manager 主控台之電腦上的本機時間，來評估可用的時間和安裝期限時間。  

        > [!NOTE]  
        >  當您選取本機時間，然後針對 [軟體可用時間] 或 [安裝期限] 選取 [盡快] 時，就會使用執行 Configuration Manager 主控台之電腦上的目前時間，來評估更新可用時間或更新安裝於用戶端的時間。 如果在用戶端位於其他時區，則會在用戶端的時間達到評估時間時，執行這些動作。  

    -   **軟體可用時間**：選取以下其中一種設定來指定用戶端可以使用軟體更新的時間：  

        -   **盡快**：選取此設定可讓用戶端電腦在最短時間內使用部署內含的軟體更新。 利用選取的設定建立部署時，Configuration Manager 會更新用戶端原則。 接著，在下一個用戶端原則輪詢循環中，用戶端將會察覺該部署並取得安裝可用的更新。  

        -   **特定時間**：選取此設定可讓用戶端電腦在特定日期和時間使用部署內含的軟體更新。 建立部署時啟用此設定，Configuration Manager 會更新用戶端原則。 接著，在下一個用戶端原則輪詢循環中，用戶端將會察覺該部署。 不過，在設定的日期和時間前，無法使用並安裝部署中的軟體更新。  

    -   **安裝期限**：選取以下其中一種設定來指定部署中軟體更新的安裝期限：  

        -   **盡快**：選取此設定可在最短時間內自動安裝部署中的軟體更新。  

        -   **特定時間**：選取此設定可在特定日期和時間自動安裝部署中的軟體更新。 將已設定的 [特定時間] 間隔新增到 [軟體可用時間]，Configuration Manager 藉此判斷安裝軟體更新的期限。  

        > [!NOTE]  
        >  實際安裝的期限時間是顯示的期限時間，加上最多 2 小時的隨機總時間。 這能減少對同時在部署中安裝軟體更新之目的地集合裡所有用戶端電腦的潛在影響。  
        >   
        >  您可以設定 [電腦代理程式]  用戶端設定的 [停用期限隨機設定]  ，針對必要的軟體更新停用安裝隨機延遲。 如需詳細資訊，請參閱 [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent)。  

8. 在 [使用者經驗] 頁面，設定以下設定：  

    -   **使用者通知**：指定是否要在設定的 [軟體可用時間]  ，於用戶端電腦上 [軟體中心] 內顯示軟體更新的通知，以及是否要在用戶端電腦上顯示使用者通知。  

    -   **期限行為**：指定到達軟體更新部署期限時會發生的行為。 指定是否安裝部署中的軟體更新。 同時也指定是否於無論設定之維護期間為何的狀況下，只要軟體更新安裝完成，就執行系統重新啟動。 如需維護期間的詳細資訊，請參閱[如何使用維護期間](../../core/clients/manage/collections/use-maintenance-windows.md)。  

    -   **裝置重新啟動行為**：於安裝軟體更新，且需要重新啟動系統才能完成安裝的狀況下，指定是否抑制在伺服器和工作站上重新啟動系統。  

        > [!IMPORTANT]  
        >  在伺服器環境中，或者是您不想讓安裝軟體更新的電腦根據預設重新啟動時，抑制系統重新啟動是很有用的。 不過，如此一來就會讓電腦處於不安全的狀態，允許強制重新啟動則可協助確保軟體更新安裝能立即完成。  

    -   **Windows Embedded 裝置的寫入篩選器處理**：將軟體更新部署至啟用寫入篩選器的 Windows Embedded 裝置時，您可以指定在暫時重疊上安裝軟體更新，並於稍後再認可變更，或是在安裝期限或維護期間認可變更。 當您在安裝期限或維護期間認可變更時，需要重新啟動裝置才能保存裝置的變更。  

        > [!NOTE]  
        >  當您將軟體更新部署至 Windows Enbedded 裝置時，請確認裝置是已設定維護期間之集合的成員。  

    - **重新啟動時的軟體更新部署重新評估行為**︰從 Configuration Manager 版本 1606 開始，選取此設定來設定軟體更新部署，讓用戶端能夠在用戶端安裝軟體更新和重新啟動之後立即執行軟體更新相容性掃描。 這可讓用戶端檢查是否有在用戶端重新啟動後變成適用的其他軟體更新，然後在同一個維護期間內安裝這些更新 (而變成相容)。

9. 於 [警示] 頁面上設定 Configuration Manager 和 System Center Operations Manager 如何針對此部署產生警示。  

    > [!NOTE]  
    >  您可經由 [軟體程式庫]  工作區中的 [軟體更新]  節點檢閱最新的軟體更新警示。  

10. 在 [下載設定] 頁面，設定以下設定：  

    - 指定當用戶端連線到速度較慢的網路，或使用後援內容位置時，是否要下載並安裝軟體更新。  

    - 指定無法在慣用發佈點使用軟體更新內容時，是否要讓用戶端從後援發佈點下載並安裝軟體更新。  

    - **允許用戶端與同一個子網路上的其他用戶端共用內容**：指定是否允許針對下載內容使用 BranchCache。 如需有關 BranchCache 的詳細資訊，請參閱 [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)。  

    - **如果在目前、鄰近或網站群組的發佈點上找不到軟體更新，則從 Microsoft Update 下載內容**：選取這個設定可讓連線至內部網路的用戶端，在發佈點上找不到軟體更新時從 Microsoft Update 下載軟體更新。 可連上網際網路的用戶端隨時可移至 Microsoft Update 取得軟體更新內容。

    - 指定當用戶端使用計量付費網際網路連線時，是否在過了安裝期限後仍允許用戶端進行下載。 在您處於計量付費網際網路連線時，網際網路提供者有時會根據您傳送和接收的資料量來收取費用。  

    > [!NOTE]  
    >  用戶端會從部署內軟體更新的管理點來請求內容位置。 下載行為會根據您如何設定發佈點、部署套件和本頁設定而定。 如需詳細資訊，請參閱 [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  

11. 在 [部署套件] 頁面上選取現有的部署套件，或進行下列設定以建立新的部署套件：  

    1.  **名稱**：指定部署套件的名稱。 此名稱必須是描述套件內容的唯一名稱。 長度限制為 50 個字元。  

    2.  **描述**：指定描述，提供部署套件的相關資訊。 描述限制為 127 個字元。  

    3.  **套件來源**：指定軟體更新來源檔案的位置。  輸入來源位置的網路路徑，例如 \ **\\\server\sharename\path**，或按一下 **[瀏覽]** 尋找網路位置。 您必須先建立部署套件來源檔案的共用資料夾，才能繼續前往下一個頁面。  

        > [!NOTE]  
        >  您指定的部署套件來源位置不能供另一個軟體部署套件使用。  

        > [!IMPORTANT]  
        >  SMS 提供者電腦帳戶和執行精靈下載軟體更新的使用者，都必須具有下載位置的 **寫入** NTFS 權限。 您應謹慎限制下載位置的存取權，以降低攻擊者竄改軟體更新來源檔案的風險。  

        > [!IMPORTANT]  
        >  您可以在 Configuration Manager 建立部署套件之後，變更部署套件內容中的套件來源位置。 不過，如果您這樣做，則必須先將內容從原始套件來源複製到新的套件來源位置。  

    4.  **傳送優先順序**：指定部署封裝的傳送優先順序。 Configuration Manager 將套件傳送到發佈點時，會針對部署套件使用傳送優先順序。 部署套件會依優先順序傳送：高、中或低。 優先順序相同的套件，會依照建立的順序傳送。 若沒有積存，則無論其優先順序為何，都會立即處理該套件。  

12. 在 [發佈點] 頁面上，指定將裝載軟體更新檔案的發佈點或發佈點群組。 如需發佈點的詳細資訊，請參閱[發佈點設定](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)。  

    > [!NOTE]  
    >  此頁面只有在您建立新的軟體更新部署套件時才可使用。  

13. 在 [下載位置] 頁面上，指定要從網際網路或您的區域網路下載軟體更新檔案。 進行以下設定：  

    -   **從網際網路下載軟體更新**：選取此設定可從網際網路上指定的位置下載軟體更新。 預設會啟用此設定。  

    -   **從區域網路上的位置下載軟體更新**：選取此設定可從本機目錄或共用資料夾下載軟體更新。 此設定在執行精靈的電腦沒有網際網路存取時很實用。 有網際網路存取的任何電腦都可預先下載軟體更新，並將其儲存到區域網路上可從執行精靈的電腦存取的位置。  

14. 在 [語言選擇] 頁面上，選取選定之軟體更新所下載的語言。 軟體更新只會在有提供所選取的語言時才能下載。 無指定語言的軟體更新，則都會下載的。 根據預設，精靈會選取您在軟體更新點內容中設定的語言。 您必須至少選取一種語言才能繼續至下一頁。 如果您只選取軟體更新不支援的語言，則軟體更新下載將會失敗。  

15. 在 [摘要] 頁面上檢閱設定。 若要將設定儲存至部署範本，請按一下 儲存成範本 ，輸入名稱，並選取要納入範本的設定，然後按一下儲存 。 若要變更已經設定的設定，請按一下相關聯的精靈頁面，然後變更設定。  

    > [!NOTE]  
    >  範本名稱可以包含英數字 ASCII 字元以及 **\\** (反斜線) 或 **'** (單引號)。  

16. 按一下 [下一步]  以建立 ADR。  

 在您完成精靈後，ADR 就會執行。 它會將符合指定準則的軟體更新新增至軟體更新群組、將軟體更新下載至網站伺服器上的內容庫、將軟體更新發佈至設定的發佈點，然後將軟體更新群組部署至目標集合中的用戶端。  

##  <a name="BKMK_AddDeploymentToADR"></a> 將新的部署新增至現有的 ADR  
 建立 ADR 之後，您可以將其他的部署加入規則中。 如此可協助您管理將不同更新部署到不同集合的複雜性。 每個新部署都會有完整的功能和部署監視體驗。  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>將新的部署新增至現有的 ADR  

1.  在 Configuration Manager 主控台中，巡覽至 [軟體程式庫] > [概觀] > [軟體更新] > [自動部署規則]，然後選取所需的規則。  

2.  在 [首頁]  索引標籤的 [自動部署規則]  群組中，按一下 [新增部署] 。 [新增部署精靈] 隨即開啟。  

3.  在 [集合]  頁面上，設定下列設定：  

    -   **集合**：指定部署用的目標集合。 集合內的成員會收到部署中定義的軟體更新。  

    -   **在執行此規則後啟用部署**：指定執行 ADR 後，是否要啟用軟體更新部署。 關於此規格，請考慮下列各項：  

        -   啟用部署時，會將符合規則中定義之準則的軟體更新新增到某個軟體更新群組，必要時會下載軟體更新內容，而內容會複製到指定的發佈點，軟體更新則會在目標集合的用戶端上部署。  

        -   您不啟用部署時，會將符合規則中定義之準則的軟體更新新增至某個軟體群組，並設定軟體更新部署原則，但不會將軟體更新下載或部署至用戶端。 這個狀況能提供您需要的時間以準備部署軟體更新，請確認符合準則的軟體更新是正確的，並於稍後啟用部署。  

4.  在 [部署設定] 頁面，指定以下設定：  

    -   **使用網路喚醒來喚醒用戶端進行必要的部署**：指定是否於期限啟用網路喚醒，將喚醒封包傳送到在部署中需要一或多個軟體更新的電腦。 安裝期限時處於睡眠模式的任何電腦都會喚醒，如此即可起始軟體更新安裝。 在部署中處於睡眠狀態且不需要任何軟體更新的用戶端並不會啟動。 根據預設不會啟用此設定。  

        > [!WARNING]  
        >  在您可使用此選項前，必須針對網路喚醒設定電腦和網路。  

    -   **詳細等級**：針對由用戶端電腦報告的狀態訊息，指定詳細等級。  

        > [!IMPORTANT]  
        >  部署定義更新時，請將詳細等級設定至 [僅錯誤]  ，僅在定義更新無法傳遞給用戶端時，讓用戶端回報狀態訊息。 否則，用戶端會回報一大批的狀態訊息，可能影響到網站伺服器的效能。  

5.  在 [部署排程] 頁面，指定以下設定：  

    -   **排程評估**：指定 Configuration Manager 是否要使用 UTC 或執行 Configuration Manager 主控台之電腦上的本機時間，來評估可用的時間和安裝期限時間。  

        > [!NOTE]  
        >  當您選取本機時間，然後針對 [軟體可用時間] 或 [安裝期限] 選取 [盡快] 時，就會使用執行 Configuration Manager 主控台之電腦上的目前時間，來評估更新可用時間或更新安裝於用戶端的時間。 如果在用戶端位於其他時區，則會在用戶端的時間達到評估時間時，執行這些動作。  

    -   **軟體可用時間**：選取以下其中一種設定來指定用戶端可以使用軟體更新的時間：  

        -   **盡快**：選取此設定可讓用戶端電腦在最短時間內使用部署內含的軟體更新。 利用選取的設定建立部署時，Configuration Manager 會更新用戶端原則。 接著，在下一個用戶端原則輪詢循環中，用戶端將會察覺該部署並取得安裝可用的更新。  

        -   **特定時間**：選取此設定可讓用戶端電腦在特定日期和時間使用部署內含的軟體更新。 建立部署時啟用此設定，Configuration Manager 會更新用戶端原則。 接著，在下一個用戶端原則輪詢循環中，用戶端將會察覺該部署。 不過，在設定的日期和時間前，無法使用並安裝部署中的軟體更新。  

    -   **安裝期限**：選取以下其中一種設定來指定部署中軟體更新的安裝期限：  

        -   **盡快**：選取此設定可在最短時間內自動安裝部署中的軟體更新。  

        -   **特定時間**：選取此設定可在特定日期和時間自動安裝部署中的軟體更新。 將已設定的 [特定時間] 間隔新增到 [軟體可用時間]，Configuration Manager 藉此判斷安裝軟體更新的期限。  

        > [!NOTE]  
        >  實際安裝的期限時間是顯示的期限時間，加上最多 2 小時的隨機總時間。 這能減少對同時在部署中安裝軟體更新之目的地集合裡所有用戶端電腦的潛在影響。  
        >   
        >  您可以設定 [電腦代理程式]  用戶端設定的 [停用期限隨機設定]  ，針對必要的軟體更新停用安裝隨機延遲。 如需詳細資訊，請參閱 [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent)。  

6.  在 [使用者經驗] 頁面，設定以下設定：  

    -   **使用者通知**：指定是否要在設定的 [軟體可用時間]  ，於用戶端電腦上 [軟體中心] 內顯示軟體更新的通知，以及是否要在用戶端電腦上顯示使用者通知。  

    -   **期限行為**：指定到達軟體更新部署期限時會發生的行為。 指定是否安裝部署中的軟體更新。 同時也指定是否於無論設定之維護期間為何的狀況下，只要軟體更新安裝完成，就執行系統重新啟動。 如需維護期間的詳細資訊，請參閱[如何使用維護期間](../../core/clients/manage/collections/use-maintenance-windows.md)。  

    -   **裝置重新啟動行為**：於安裝軟體更新，且需要重新啟動系統才能完成安裝的狀況下，指定是否抑制在伺服器和工作站上重新啟動系統。  

        > [!IMPORTANT]  
        >  在伺服器環境中，或者是您不想讓安裝軟體更新的電腦根據預設重新啟動時，抑制系統重新啟動是很有用的。 不過，如此一來就會讓電腦處於不安全的狀態，允許強制重新啟動則可協助確保軟體更新安裝能立即完成。  

    -   **Windows Embedded 裝置的寫入篩選器處理**：將軟體更新部署至啟用寫入篩選器的 Windows Embedded 裝置時，您可以指定在暫時重疊上安裝軟體更新，並於稍後再認可變更，或是在安裝期限或維護期間認可變更。 當您在安裝期限或維護期間認可變更時，需要重新啟動裝置才能保存裝置的變更。  

        > [!NOTE]  
        >  當您將軟體更新部署至 Windows Enbedded 裝置時，請確認裝置是已設定維護期間之集合的成員。  

7.  於 [警示] 頁面上設定 Configuration Manager 和 System Center Operations Manager 如何針對此部署產生警示。  

    > [!WARNING]  
    >  您可經由 [軟體程式庫]  工作區中的 [軟體更新]  節點檢閱最新的軟體更新警示。  

8. 在 [下載設定] 頁面，設定以下設定：  

    - 指定當用戶端連線到速度較慢的網路，或使用後援內容位置時，是否要下載並安裝軟體更新。  

    - 指定無法在慣用發佈點使用軟體更新內容時，是否要讓用戶端從後援發佈點下載並安裝軟體更新。  

    - **允許用戶端與同一個子網路上的其他用戶端共用內容**：指定是否允許針對下載內容使用 BranchCache。 如需有關 BranchCache 的詳細資訊，請參閱 [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)。  

    - **如果在目前、鄰近或網站群組的發佈點上找不到軟體更新，則從 Microsoft Update 下載內容**：選取這個設定可讓連線至內部網路的用戶端，在發佈點上找不到軟體更新時從 Microsoft Update 下載軟體更新。 可連上網際網路的用戶端隨時可移至 Microsoft Update 取得軟體更新內容。

    - 指定當用戶端使用計量付費網際網路連線時，是否在過了安裝期限後仍允許用戶端進行下載。 在您處於計量付費網際網路連線時，網際網路提供者有時會根據您傳送和接收的資料量來收取費用。  

    > [!NOTE]  
    > 用戶端會從部署內軟體更新的管理點來請求內容位置。 下載行為會根據您如何設定發佈點、部署套件和本頁設定而定。 如需詳細資訊，請參閱 [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  

如需部署程序的詳細資訊，請參閱 [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess)。

## <a name="next-steps"></a>後續步驟
[監視軟體更新](monitor-software-updates.md)
