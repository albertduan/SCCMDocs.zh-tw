---
title: "1511、1602 和 1606 版的界限群組 | System Center Configuration Manager"
description: "搭配 Configuration Manager 1511、1602 和 1606 版使用界限群組。"
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: b64f1f06af1ab4a255b6291b6eb5f85cff99ae63
ms.openlocfilehash: ef408041eb6d0d6716e244d34b9a2a4ebe5cb9cc


---
# <a name="boundary-groups-for-system-center-configuration-manager-version-1511-1602-and-1606"></a>System Center Configuration Manager 1511、1602 和 1606 版的界限群組

*適用於：System Center Configuration Manager (最新分支)*

本主題中的資訊適用於搭配 System Center Configuration Manager 1511、1602 和 1606 版使用界限群組。
如果您使用 1610 版或更新版本，請參閱＜為 System Center Configuration Manager 定義站台界限和界限群組＞中的[界限群組](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-group/)。  


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



<!--HONumber=Dec16_HO3-->

