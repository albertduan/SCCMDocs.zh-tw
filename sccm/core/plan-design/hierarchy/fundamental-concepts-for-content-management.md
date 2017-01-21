---
title: "內容管理基本概念 | System Center Configuration Manager"
description: "請使用 System Center Configuration Manager 中的工具和選項來管理您部署的內容。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: 28
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 27342ef83d877c31f39bc232e3e19e37b78e62da


---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的內容管理基本概念

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 支援強固的工具和選項系統，以管理您部署為應用程式、套件、軟體更新和作業系統部署的內容。  

 您部署的內容會同時儲存於站台伺服器和發佈點站台系統伺服器上。 此內容在位置之間傳送時，可能需要大量網路頻寬。  若要有效規劃及使用內容管理基礎結構，您應該要了解可用的選項與設定，然後考量如何設定才能最滿足您的網路環境和內容部署需求。  

內容管理的重要概念。 當概念需要其他資訊或複雜資訊時，便會提供連結將您導向那些詳細資料。  

## <a name="accounts-used-for-content-management"></a>用於內容管理的帳戶  
 下列帳戶可用於內容管理：  

-   **網路存取帳戶** - 由用戶端用以連接到發佈點和存取內容。 用戶端預設會先嘗試其電腦帳戶  

     提取發佈點也會使用此帳戶從遠端樹系中的來源發佈點獲取內容  

-   **套件存取帳戶** - Configuration Manager 預設會將發佈點上的內容存取權授與一般存取帳戶使用者和系統管理員。 不過，您可以設定其他權限以限制存取。 請參閱&lt;管理帳戶以存取套件內容\>  

-   **多點傳送連接帳戶** - 用於作業系統部署  

如需這些帳戶的詳細資訊，請參閱 [Manage accounts to access content in System Center Configuration Manager](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md) (在 System Center Configuration Manager 中管理帳戶以存取內容)。

## <a name="bandwidth-throttling-and-scheduling"></a>頻寬節流設定和排程  
 節流和排程選項皆可協助您控制將內容從站台伺服器發佈到發佈點的時機。 這類似於站台對站台檔案式複寫的頻寬控制，但並不直接相關。  

 如需詳細資訊，請參閱 [Manage network bandwidth for content management in System Center Configuration Manager](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) (在 System Center Configuration Manager 中管理網路頻寬以進行內容管理)。

## <a name="binary-differential-replication"></a>二進位差異複寫  
 二進位差異複寫 (BDR) 也稱為差異複寫，是發佈點的必要條件，系統會自動使用此功能，減少將您先前部署內容的更新發佈到其他站台或遠端發佈點時的頻寬用量。  

 BDR 只會重新傳送新的或變更的內容，而不是在每次變更這些檔案時就傳送完整的內容來源檔案，藉此大幅降低傳送發佈內容更新時使用的頻寬。  

 當使用二進位差異複寫時，Configuration Manager 會針對之前發佈的每一組內容識別來源檔案的變更。  

-   當來源內容中的檔案變更時，Configuration Manager 會建立新的內容集累加版本，並只將變更的檔案複寫到目的地站台和發佈點。 任何重新命名、移動或檔案內容有所變動的檔案都會視為是已變更的檔案。 舉例來說，如果您在之前發佈至數個網站的作業系統部署套件中替換其中一個驅動程式，則只有變更的驅動程式檔案會複寫至這些目的地網站。  

-   Configuration Manager 最多可支援五個累加版本的內容集。 在第五次更新之後，下一次的內容集變動會使 Configuration Manager 建立一個新版本的內容集。 Configuration Manager 便會發佈新的內容集以取代舊的內容集以及任何累加版本。 在發佈新的內容集之後，二進位差異複寫會再次複寫來源檔案的後續累加變更。  


系統支援階層中每個父子站台之間的 BDR。 在站台中，系統支援站台伺服器與其發佈點之間的 BDR。 此支援包含提取發佈點，但不包含雲端式發佈點。 雲端發佈點不支援二進位差異複寫以傳送內容。  

應用程式會一律使用二進位差異複寫。 在使用套件時，二進位差異複寫是選擇性的方式，且依預設不會啟用。 若要使用套件的二進位差異複寫，您必須為每個套件啟用此功能。 若要執行這項操作，當您建立新套件或編輯套件內容的 [資料來源]  時，請選取 [啟用二進位差異複寫]  選項。  

## <a name="branchcache"></a>BranchCache  
 這項 Windows 技術可讓支援 BranchCache 並且已下載為分支快取所設定部署的用戶端，將內容來源當作其他支援 BranchCache 的用戶端使用。  

 例如，當第一個支援 BranchCache 的用戶端電腦從執行 Windows Server 2012 並且已設定為 BranchCache 伺服器的發佈點要求內容時，用戶端電腦會下載該內容並加以快取。  

-   該用戶端電腦接著可以將內容提供給相同子網路上其他支援分支快取的用戶端使用，這些用戶端也會快取內容。  

-   後續相同子網路上的用戶端若用這種方式，就不需要從發佈點下載內容，之後要傳送時會透過多個用戶端發佈內容。  





## <a name="windows-pe-peer-cache"></a>Windows PE 對等快取
當您在 System Center Configuration Manager 中部署新的作業系統時，執行工作順序的電腦可使用 Windows PE 對等快取，從本機對等裝置 (對等快取來源) 取得內容，而不是從發佈點下載內容。 這有助於在分公司沒有本機發佈點的案例中，降低廣域網路 (WAN) 流量。

如需詳細資訊，請參閱 [Windows PE 對等快取](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)。


## <a name="client-locations"></a>用戶端位置  
 用戶端可從下列位置存取內容：  

-   **內部網路** (內部部署)：  

    -   發佈點可使用 HTTP 或 HTTPs  

    -   請只在內部部署發佈點無法使用時，才將雲端式發佈點用於後援  

-   **內部網路** ：  

    -   需要發佈點接受 HTTPS  

    -   您可將雲端式發佈點用於後援  

-   **工作群組**：  

    -   需要發佈點接受 HTTPS  

    -   您可將雲端式發佈點用於後援  



## <a name="content-library"></a>內容庫  
 內容的唯一存放區，而 Configuration Manager 可用該內容來減少發佈之內容的合併主體之整體大小。  

進一步了解[內容庫](../../../core/plan-design/hierarchy/the-content-library.md)。


## <a name="distribution-point"></a>發佈點  
 Configuration Manager 使用發佈點來儲存在用戶端電腦上執行軟體所需要的檔案。 用戶端必須能存取至少一個發佈點，且必須可從該發佈點下載檔案以用於您所部署的內容。  

 基本 (非特製化) 發佈點通常是指標準發佈點。  標準發佈點有以下兩個值得特別注意的變化：  

-   **提取發佈點** - 為發佈點的一種變化，發佈點可透過此處從其他發佈點 (來源發佈點) 取得內容，其方式類似於用戶端從發佈點下載內容。 當站台伺服器將內容直接發佈到每個發佈點時，提取發佈點可協助您避免這段期間所發生的網路頻寬瓶頸，提升內容發佈的效率。  [使用提取發佈點搭配 System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

-   **雲端式發佈點** - 為安裝於 Microsoft Azure 當中的一種發佈點變化。 [使用雲端架構發佈點搭配 System Center Configuration Manager](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  


標準發佈點支援豐富的設定與功能，例如節流和排程、PXE 和多點傳送，或預先設置的內容。  

-   您可以使用 **排程** 或 **頻寬節流設定** 等控制項，來協助控制這類傳輸。  

-   您也可以使用 **預先設置內容**、 **提取發佈點**等其他選項，或利用 **BranchCache** 以減少部署內容時使用的網路頻寬。  

-   針對作業系統部署，發佈點支援 **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** 和**[多點傳送](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**之類的不同設定，或支援**行動裝置**的設定。  

 雲端式發佈點和提取發佈點支援上述許多相同設定，但每種發佈點變化亦有其特有的限制。  

## <a name="distribution-point-group"></a>發佈點群組  
 可簡化內容發佈的發佈點邏輯群組。  

 如需詳細資訊，請參閱[管理發佈點群組](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)。

## <a name="distribution-point-priority"></a>發佈點優先順序  
 發佈點優先順序值的依據是將先前部署傳送到該發佈點所花費的時間。  

-   這個指派到發佈點的值可自我調整，協助 Configuration Manager 以較短時間，將內容傳送到更多發佈點。  

-   當您同時將內容發佈至多個發佈點或一個發佈點群組時，Configuration Manager 會將內容傳送至具有最高優先順序的發佈點，然後才將相同內容傳送至優先順序較低的發佈點。  

-   傳送不同的發佈時，封裝的發佈優先順序依然是順序的決定因素，並不會受到取代。  


**舉例來說，** 當您將發佈優先順序較高的內容發佈至發佈點優先順序較低的發佈點時，發佈優先順序較高的封裝會一律在發佈優先順序較低的封裝之前傳送。 即使將發佈優先順序較低的套件發佈至發佈點優先順序較高的發佈點時，發佈優先順序仍然適用。 套件的高發佈優先順序可確保 Configuration Manager 在傳送發佈優先順序較低的任何套件之前，能先將該內容發佈至適用的發佈點。  

> [!NOTE]  
>  提取發佈點也會使用優先順序的概念來排序其來源發佈點的順序。  
>   
>  -   將內容傳送至發佈點的發佈點優先順序，與提取發佈點在搜尋來源發佈點內容時使用的優先順序並不相同  
> -   如需詳細資訊，請參閱[使用提取發佈點搭配 System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)。  


## <a name="fallback"></a>後援  
 後援設定與 **慣用發佈點** 的使用和用戶端所用內容來源位置有關。  

-   用戶端預設只會從慣用發佈點 (與用戶端的界限群組相關聯者) 下載內容  

-   然而，當發佈點設定為 **[Allow clients to use this site system as a fallback source location for content (允許用戶端將此站台系統用作內容的後援來源位置)]**時，則僅有在用戶端無法從其慣用發佈點之一取得部署的情況下，該發佈點才可作為此用戶端的有效內容來源。  


如需不同內容位置和後援案例的資訊，請參閱[內容來源位置案例](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)。

## <a name="network-bandwidth"></a>網路頻寬  
 若要協助管理發佈內容時所用的網路頻寬量，您可以使用下列選項：  

-   使用預先設置的內容：不依賴 Configuration Manager 透過網路發佈內容，而將內容傳送到發佈點的程序。  

-   使用排程及節流：此設定可協助您控制將內容發佈到發佈點的時機和方式。  

如需詳細資訊，請參閱 [Manage network bandwidth for content management in System Center Configuration Manager](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) (在 System Center Configuration Manager 中管理網路頻寬以進行內容管理)。

## <a name="network-connection-speed-to-content-source"></a>內容來源的網路連線速度  
 您可以在界限群組中為各發佈點設定網路連線速度：  

-   用戶端會在連線至發佈點時使用此值  

-   網路連線速度預設會設定為 [快] ，但也可以設定為 [慢]   

-   **網路連線速度** 和部署組態會決定用戶端位於相關聯的界限群組時，是否可以從發佈點下載內容。  


如需不同內容位置和後援案例的資訊，請參閱[內容來源位置案例](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  

## <a name="on-demand-content-distribution"></a>依需求發佈內容  
 您可以針對個別應用程式和封裝 (部署) 設定此選項，允許依需求將內容發佈到慣用發佈點。  

-   若要為部署啟用此功能，您可以啟用 **將此封裝的內容發佈到慣用發佈點**  

-   當此選項已針對部署啟用，而用戶端嘗試要求該內容，但用戶端的任何慣用發佈點上皆未提供內容時，則 Configuration Manager 會自動將該內容發佈到用戶端慣用發佈點  

-   雖然這會觸發 Configuration Manager 自動將內容發佈到該用戶端慣用發佈點，但是用戶端可能會在用戶端的慣用發佈點收到部署之前，先從其他發佈點得到該內容。 發生此情況時，內容就會出現在該發佈點上，以供下一個搜尋該項部署的用戶端使用  


如需不同內容位置和後援案例的資訊，請參閱[內容來源位置案例](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  


## <a name="package-transfer-manager"></a>封裝傳輸管理員  
 此站台伺服器元件可將內容傳送到其他電腦上的發佈點。  

 進一步了解[套件傳輸管理員](../../../core/plan-design/hierarchy/package-transfer-manager.md)。  

## <a name="preferred-distribution-point"></a>慣用發佈點  
 與用戶端目前界限群組相關聯的發佈點。  

 您可以將每個發佈點與一個或多個界限群組產生關聯：  

-   此關聯可協助用戶端識別可從中下載內容的發佈點  

-   用戶端預設只會從慣用發佈點下載內容  


如需不同內容位置和後援案例的資訊，請參閱[內容來源位置案例](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  

## <a name="prestage-content"></a>預先設置內容  
 不依賴 Configuration Manager 透過網路發佈內容，而將內容傳送到發佈點的程序。  

 如需詳細資訊，請參閱 [Manage network bandwidth for content management in System Center Configuration Manager](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) (在 System Center Configuration Manager 中管理網路頻寬以進行內容管理)。



<!--HONumber=Nov16_HO1-->


