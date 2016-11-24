---
title: "定義站台界限 | System Center Configuration Manager"
description: "了解如何在您的內部網路上定義網路位置，其中可包含您要管理的裝置。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9df8b5d5fd67a5ced5860771295d05dfb56a3982


---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 定義站台界限和界限群組

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 的界限會在您的內部網路上定義網路位置，其中可包含您要管理的裝置。 界限群組是您所設定之界限的邏輯群組。 界限群組和界限在整個階層中都可使用，而您不需要針對個別站台進行設定。  

 階層可以包含任意數目的界限群組，每個界限群組可包含下列界限類型的任意組合：  

-   IP 子網路、  

-   Active Directory 站台名稱  

-   IPv6 首碼  

-   IP 位址範圍  

內部網路上的用戶端會評估其目前網路位置，然後使用該資訊來識別所屬界限群組。  

 用戶端將界限群組用於：  

-   **尋找指派的站台：** 界限群組可讓用戶端在主要站台尋找用戶端指派 (自動站台指派)。  

-   **尋找可用的特定站台系統角色：**  當您建立界限群組與特定站台系統角色的關聯時，界限群組會提供站台系統清單，以供用於內容位置，並用作偏好管理點。  

位於內部網路上的用戶端或設為僅限內部網路的用戶端不會使用界限資訊。 這些用戶端無法使用自動站台指派，並且一律會在發佈點設定為允許網際網路用戶端連線時，從其指派的站台內任何發佈點下載內容。  


##  <a name="a-namebkmkboundariesa-boundaries"></a><a name="BKMK_Boundaries"></a> 界限  
 您可以手動建立個別界限。 此外，您可以設定 [Active Directory 樹系探索](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest)以自動探索，並針對其探索到的各個 IP 子網路和 Active Directory 站台建立界限。  

-   每個界限各代表某個網路位置，而且在階層中的每個站台都可供使用。  

-   Configuration Manager 不支援使用 Supernet 的直接入口作為界限。 不過，您可以使用 IP 位址範圍界限類型。  

-   當 Active Directory 樹系探索識別指派給 Active Directory 網站的 Supernet 時，Configuration Manager 會將 Supernet 轉換為 IP 位址範圍界限。  

-   用戶端所在的界限等同於 Active Directory 站台，或用戶端所識別的網路 IP 位置。 (用戶端使用 Configuration Manager 未注意到的 IP 位置並不是罕見狀況。 如果對用戶端網路位置存疑，請對該用戶端使用 **IPCONFIG** 命令，確認用戶端回報為位置的內容)。  

當您建立界限時，界限會自動收到根據界限類型和範圍所定的名稱。 您無法修改這個名稱。 但是當您設定界限時，請指定描述以協助您在 Configuration Manager 主控台中識別界限。  

 建立界限後，您可以修改其內容以執行下列動作：  

-   將界限新增至一個或多個界限群組。  

-   變更界限的類型或範圍。  

-   檢視界限 [站台系統]  索引標籤，查看與界限相關聯的站台系統伺服器 (發佈點、狀態移轉點和管理點)。  

#### <a name="to-create-a-boundary"></a>建立界限  

1.  在 Configuration Manager 主控台中按一下 [系統管理] > [階層設定] > [界限]。  

2.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立界限] ** Boundary.**。  

3.  在 [建立界限] 對話方塊的 [一般]  索引標籤上，您可以指定 [描述]  ，以易記名稱或參照來識別界限。  

4.  選取此界限的 [類型]  ：  

    -   如果您選取 [IP 子網路] ，則必須指定此界限的 [子網路識別碼]  。  

        > [!TIP]  
        >  您可以指定 [網路]  和 [子網路遮罩]  ，以自動指定 [子網路識別碼]  。 儲存界限時，只會儲存 [子網路識別碼] 值。  

    -   如果您選取 [Active Directory 站台] ，則必須指定或 [瀏覽]  至本機站台伺服器樹系中的 Active Directory 站台。  

        > [!IMPORTANT]  
        >  您為界限指定 Active Directory 站台時，界限會包含每一個身為該 Active Directory 站台成員的 IP 子網路。 如果 Active Directory 中 Active Directory 站台的設定變更，此界限中的網路位置也會變更。  

    -   如果您選取 [IPv6 首碼] ，則必須指定 IPv6 首碼格式的 [首碼]  。  

    -   如果您選取 [IP 位址範圍] ，則必須指定包含部分 IP 子網路或包含多個 IP 子網路的 [起始 IP 位址]  和 [結束 IP 位址]  。  

5.  按一下 [確定]  儲存新界限。  

#### <a name="to-configure-a-boundary"></a>設定界限  

1.  在 Configuration Manager 主控台中按一下 [系統管理] > [階層設定] > [界限]。  

2.  選取您要修改的界限。  

3.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

4.  在界限的 [內容]  對話方塊中，選取 [一般]  索引標籤以編輯界限的 [描述]  或 [類型]  。 您也可以編輯界限的網路位置來變更界限的範圍。 例如，您可以為 Active Directory 站台界限指定新的 Active Directory 站台名稱。  

5.  選取 [站台系統]  索引標籤即可檢視與此界限相關聯的站台系統。 您無法從界限的內容變更此設定。  

    > [!TIP]  
    >  若要使站台系統伺服器成為界限的站台系統，站台系統伺服器必須是包含此界限的至少一個界限群組的相關聯站台系統伺服器。 這設定在界限群組的 [參照]  索引標籤上。  

6.  選取 [界限群組]  索引標籤可修改此界限的界限群組成員資格：  

    -   若要將此界限新增至一個或多個界限群組，請按一下 [新增] ，選取一個或多個界限群組的核取方塊，然後按一下 [確定] 。  

    -   若要從界限群組中移除此界限，請選取界限群組，然後按一下 [移除] 。  

7.  按一下 [確定]  關閉界限內容，並儲存設定。  

##  <a name="a-namebkmkboundarygroupsa-boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Boundary groups  
 將界限群組建立到與邏輯網路相關的網路位置 (或界限) 使其更容易管理您的基礎結構。 您必須先將界限指派給界限群組，才能使用界限群組。 用戶端將界限群組組態用於：  

-   自動站台指派  

-   內容位置  

-   偏好的管理點 (如果您將會使用偏好的管理點，就必須針對階層啟用此選項，而非從界限群組組態中啟動)。 請參閱下列程序＜若要允許使用偏好的管理點＞ )  

當您設定界限群組時，會將一個或多個界限新增到界限群組，然後進行其他設定以供位於這些界限上的用戶端使用。  

#### <a name="to-create-a-boundary-group"></a>建立界限群組  

1.  在 Configuration Manager 主控台中按一下 [系統管理] > [階層設定] >  [界限群組]。  

2.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立界限群組] 。  

3.  在 [建立界限群組]  對話方塊中，選取 [一般]  索引標籤並指定此界限群組的 [名稱]  。  

4.  按一下 [確定]  儲存新界限群組。  

#### <a name="to-configure-a-boundary-group"></a>設定界限群組  

1.  在 Configuration Manager 主控台中按一下 [系統管理] > [階層設定] >  [界限群組]。  

2.  選取您要修改的界限群組。  

3.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

4.  在界限群組的 [內容]  對話方塊中，選取 [一般]  索引標籤修改身為此界限群組成員的界限。  

    -   若要新增界限，請按一下 [新增] ，選取一個或多個界限的核取方塊，然後按一下 [確定] 。  

    -   若要移除界限，請選取界限，然後按一下 [移除] 。  

5.  選取 [參照]  索引標籤可修改站台指派和相關聯的站台系統伺服器組態：  

    -   若要讓用戶端使用此界限群組進行站台指派，請選取 [使用此界限群組進行站台指派] ，然後從 [指派的站台]  下拉式方塊選取站台。  

    -   若要設定哪些可用的站台系統伺服器與此界限群組相關聯：  

    1.  按一下 [新增] ，然後選取一部或多部伺服器的核取方塊。 伺服器會加入為此界限群組的站台系統伺服器。 只能使用有安裝受支援站台系統角色的伺服器。  

        > [!NOTE]  
        >  您可以從階層中的任何網站選取可用站台系統的任何組合。 選取的站台系統會在每個身為此界限群組成員之界限內容中的 [站台系統]  索引標籤內列出。  

    2.  若要從此界限群組中移除伺服器，請選取該伺服器，然後按一下 [移除] 。  

        > [!NOTE]  
        >  若要停止使用此界限群組做為相關聯的站台系統，您必須移除所有列為相關聯站台系統伺服器的伺服器。  

    3.  若要變更此界限群組之站台系統伺服器的網路連線速度，請選取伺服器，然後按一下 [變更連線] 。  

         根據預設，每個站台系統的連線速度為 [快] ，但是可以變更為 [慢] 。 網路連線速度和部署設定會決定用戶端是否可從伺服器下載內容。  

6.  按一下 [確定]  關閉界限群組內容，並儲存設定。  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>使內容部署伺服器或管理點與界限群組產生關聯  

1.  在 Configuration Manager 主控台中按一下 [系統管理] > [階層設定] >  [界限群組]。  

2.  選取您要修改的界限群組。  

3.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

4.  在界限群組的 [內容]  對話方塊中，選取 [參照]  索引標籤。  

5.  在 [選取站台系統伺服器] 下，按一下 [新增] ，選取要與此界限群組產生關聯之站台系統伺服器的核取方塊，然後按一下 [確定] 。  

6.  按一下 [確定]  關閉對話方塊，並儲存界限群組設定。  

#### <a name="to-enable-use-of-preferred-management-points"></a>若要允許使用偏好的管理點  

1.  在 Configuration Manager 主控台中按一下 [系統管理] > [站台設定] > [站台]，然後在 [首頁] 索引標籤上選取 [階層設定]。  

2.  在 [階層設定] 的 [一般]  索引標籤，選取 [用戶端偏好使用界限群組中指定的管理點] 。  

3.  按一下 [確定]  關閉對話方塊並儲存組態。  

#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>設定自動站台指派的後援站台  

1.  在 Configuration Manager 主控台中按一下 [系統管理] > [站台設定] >  [站台]。  

2.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [階層設定] 。  

3.  在 [一般]  索引標籤上，選取 [使用後援站台] 核取方塊，然後從 [後援站台]  下拉式清單中選取站台。  

4.  按一下 [確定]  儲存設定。  

 下列章節提供有關界限群組組態的其他詳細資料。  

###  <a name="a-namebkmkboundarysiteassignmenta-about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> 關於站台指派  
 您可以使用為用戶端指派的站台設定各個邊界群組。  

-   使用自動站台指派的新安裝用戶端，將會加入包含用戶端目前網路位置之界限群組的指派站台。  

-   用戶端在指派到站台後，不會在變更其網路位置的同時變更其站台指派。 例如，如果用戶端漫遊至新的網路位置，而該位置是以擁有不同站台指派之界限群組中的界限所表示，則用戶端的指派的站台將維持不變。  

-   當 Active Directory 系統探索發現新資源時，所探索資源的網路資訊會根據界限群組中的界限進行評估。 此程序會將新資源與指派的站台產生關聯，以供用戶端推入安裝方法使用。  

-   當界限屬於具有不同指派站台的多個界限群組時，用戶端會隨機選取其中一個站台。  

-   界限群組指派站台的變更僅適用於新的站台指派動作。 若先前已將用戶端指派給站台，請勿依界限群組組態 (或其本身網路位置) 的變更重新評估其站台指派。  

如需用戶端站台指派的詳細資訊，請參閱[如何將用戶端指派給 System Center Configuration Manager 中的站台](../../../../core/clients/deploy/assign-clients-to-a-site.md)中的[針對電腦使用自動站台指派](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment)。  

###  <a name="a-namebkmkboundarycontentlocationa-about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> 關於內容位置  
 您可以使用一個或多個發佈點和狀態移轉點來設定各個界限群組，而且可以將同一個發佈點和狀態移轉點與多個界限群組產生關聯。  

-   **在軟體發佈期間**，用戶端會要求可部署內容的位置。 Configuration Manager 會傳送一份發佈點清單給用戶端，這些發佈點與包含用戶端目前網路位置的每個界限群組相關聯。  

-   **在作業系統部署期間** ，用戶端會要求可傳送或接收其狀態移轉資訊的位置。 Configuration Manager 會傳送一份狀態移轉點清單給用戶端，這些狀態移轉點與包含用戶端目前網路位置的每個界限群組相關聯。  

此行為可讓用戶端選取最接近的伺服器，以傳送內容或狀態移轉資訊。  

###  <a name="a-namebkmkpreferredmpa-about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> 關於慣用的管理點  
 慣用的管理點可讓用戶端識別與用戶端目前網路位置 (或界限) 相關聯的管理點。  

-   用戶端會先嘗試使用其指派站台中的慣用管理點，再使用其指派站台中未設定為慣用的管理點。  

-   若要使用這個選項，您必須針對階層加以啟用，並設定個別主要站台上的界限群組，以包含應與界限群組相關界限產生關聯的管理點  

-   設定慣用的管理點且用戶端組織其管理點清單之後，用戶端會將慣用的管理點放在指派的管理點清單頂端 (其中包含來自用戶端指派站台的所有管理點)  

> [!NOTE]  
>  當用戶端漫遊時 (亦即變更其網路位置，就像從膝上型電腦到遙遠的辦公位置傳輸時)，可能會在嘗試使用其指派站台 (包含偏好管理點) 的管理點前，先使用位於其新位置的本機站台管理點 (或 Proxy 管理點)。  如需詳細資訊，請參閱[了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

###  <a name="a-namebkmkboundaryoverlapa-about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> 關於重疊界限  
 Configuration Manager 支援內容位置的重疊界限設定：  

-   **當用戶端要求內容時**，若用戶端網路位置屬於多個界限群組，Configuration Manager 會為用戶端傳送一份具有內容的所有發佈點清單。  

-   **當用戶端要求伺服器傳送或接收其狀態移轉資訊時**，若用戶端網路位置屬於多個界限群組，Configuration Manager 會為用戶端傳送一份包含與界限群組 (其包含用戶端目前的網路位置) 相關聯的所有狀態移轉點清單。  

此行為可讓用戶端選取最接近的伺服器，以傳送內容或狀態移轉資訊。  

###  <a name="a-namebkmkboudnarynetworkspeeda-about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> 關於網路連線速度  
 您可以針對界限群組中的各個站台系統伺服器設定網路連線速度。 此設定適用於依據此界限群組設定連接到站台系統的用戶端。 同一部站台系統伺服器可以針對不同界限群組而設有不同的連線速度。  

 根據預設，網路連線速度會設定為 [快] ，但也可以設定為 [慢] 。 網路連線速度和部署設定，取決於用戶端是否可以在用戶端位於相關聯的界限群組時，從發佈點下載內容。  

 如需網路連線速度設定如何影響取得內容方式的詳細資訊，請參閱[內容來源位置案例](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  

##  <a name="a-namebkmkboundarybestpracticesa-best-practices-for-boundaries"></a><a name="BKMK_BoundaryBestPractices"></a> 界限的最佳做法  

-   **只有在無法使用其他界限類型時，才考慮使用 IP 位址範圍界限類型**  

     設計界限策略時，建議您在使用其他界限類型之前先使用以 Active Directory 網站為基礎的界限。 無法選擇使用以 Active Directory 網站為基礎的界限時，就使用 IP 子網路或 IPv6 界限。 如果這些選項都不可用，請運用 IP 位址範圍界限。 這是因為網站會定期評估界限成員，而評估 IP 位址範圍的成員所需的查詢需要使用的 SQL Server 資源多於評估其他界限類型成員的查詢。  

-   **避免自動站台指派的重複界限：**  

     雖然每個界限群組都同時支援站台指派設定和內容位置組態，最佳的做法仍是建立僅適用於站台指派的個別界限群組。 意義：確保界限群組中的每個界限不屬於另一個具有不同站台指派的界限群組。 原因：  

    -   單一界限可包含在多個界限群組中  

    -   每個界限群組都可以和不同主要站台建立關係以進行站台指派  

    -   界限上屬於兩個不同界限群組且站台指派互異的用戶端，會隨機選取站台加入，而這不一定會是您希望用戶端加入的站台。  此組態稱為重複界限。  

     重複界限對於內容位置而言不是問題而是想要的組態，可提供用戶端其他資源，或可用的內容位置。  



<!--HONumber=Nov16_HO1-->


