---
title: "定義界限群組 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中將用戶端連結至站台系統的界限群組。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 8da48e89e8376cc23109faa1c74b29a64699aa87
ms.lasthandoff: 03/27/2017


---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>設定 System Center Configuration Manager 的界限群組


*適用對象：System Center Configuration Manager (最新分支)*

使用 System Center Configuration Manager 中的界限群組對相關的網路位置 (或[界限](/sccm/core/servers/deploy/configure/boundaries)) 進行邏輯分組，使其更容易管理您的基礎結構。 您必須先將界限指派給界限群組，才能使用界限群組。

根據預設，Configuration Manager 會在每個站台建立預設的站台界限群組。

> [!IMPORTANT]  
>  **此界限群組區段及其子區段中的資訊適用於 1610 版或更新版本。** 本內容已針對界限群組與此更新版本推出的設計變更而修改。
>
> **如果您使用 1610 之前的版本**，請參閱 [System Center Configuration Manager 1511、1602 和 1606 版的界限群組](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606)，以取得這些產品版本如何使用與設定界限群組的相關資訊。

若要設定界限群組時，您可以將界限 (網路位置) 和站台系統角色 (例如發佈點) 關聯至界限群組。 這可協助將用戶端與站台系統伺服器產生關聯，例如位於網路上用戶端附近的發佈點。

當您將相同的界限指派給多個界限群組，並將發佈點之類的相同站台系統伺服器指派給多個界限群組時，您可以增加站台系統對眾多網路位置的可用性。

用戶端將界限群組用於：  

-   自動站台指派  
-   若要尋找可以提供服務的站台系統伺服器，包括︰
    - 內容位置的發佈點
    -    軟體更新點 (從 1702 版開始)
    - 狀態移轉點
    - 偏好的管理點 (如果您將會使用偏好的管理點，就必須針對階層啟用此選項，而非從界限群組組態中啟動。 請參閱本主題中的[若要允許使用偏好的管理點](#to-enable-use-of-preferred-management-points))。

##  <a name="boundary-groups-and-relationships"></a>界限群組和關聯性
對於階層中的每個界限群組，您可以指派︰

-  一或多個界限。 當用戶端所在的網路位置定義為指派給特定界限群組的界限時，就稱為「目前」的界限群組。 用戶端可以有多個目前的界限群組。
- 一或多個站台系統角色。  用戶端永遠可以使用和其目前界限群組相關聯的站台系統角色。 視其他組態而定，它們可能無法使用其他界限群組中的站台系統角色。  

對於您建立的每個界限群組，您可以設定和另一個界限群組的單向連結。 該連結稱為「關聯性」。 您連結到的界限群組稱為「鄰近」界限群組。 界限群組可以有多個關聯性，各有特定的鄰近界限群組。

當無法在其目前的界限群組中找到可用站台系統伺服器的用戶端，開始搜尋鄰近界限群組以尋找可用的站台系統時，會決定每個關聯性的設定。 搜尋其他群組的這個行為稱為「後援」。

## <a name="fallback"></a>後援
為了避免用戶端在目前界限群組中找不到可用站台系統時發生問題，您可以定義界限群組之間的關聯性來定義後援行為。 後援可讓用戶端將其搜尋範圍擴大至其他界限群組，以尋找可用的站台系統。

關聯性可在界限群組屬性上的 [關聯性] 索引標籤設定。 當您設定關聯性時，您會定義鄰近界限群組的連結。 對於每一種支援的站台系統角色，您都可以設定該鄰近界限群組的獨立後援設定。 例如，當您設定特定界限群組的關聯性時，您可以設定發佈點的後援在 20 分鐘之後發生，而不是預設的 120 分鐘。 如需更廣泛的範例，請參閱[使用界限群組的範例](#example-of-using-boundary-groups)。

如果用戶端無法在其目前的界限群組中找到可用的網站系統角色，用戶端會使用以分鐘為單位的後援時間，來決定之後多久可以開始搜尋和該鄰近界限群組相關聯的可用站台系統。  

當用戶端找不到可用的站台系統並從鄰近界限群組開始搜尋位置時，它會採取界限群組的設定和其關聯性所定義的方式，增加可使用的可用站台系統集區。

- 界限群組可以有多個關聯性。 這可讓您將每種站台系統類型設定在不同的期間後切換回不同的鄰近界限群組。    
- 用戶端只會切換回其目前界限群組的直接芳鄰界限群組。
- 當用戶端是多個界限群組的成員時，目前界限群組會定義為該用戶端的所有界限群組聯集。 該用戶端接著可切換回任何原始界限群組的鄰近界限群組。

### <a name="the-default-site-boundary-group"></a>預設站台界限群組
除了您所建立的界限群組，每個站台都有由 Configuration Manager 建立的預設站台界限群組。 此群組名為 ***Default-Site-Boundary-Group&lt;sitecode>***。 例如，站台 ABC 的群組會命名為 *Default-Site-Boundary-Group&lt;ABC>*。

對於您所建立的每個界限群組，Configuration Manager 都會自動建立階層中的每個預設站台界限群組的隱含連結。
-    隱含連結為預設後援選項，從目前界限群組切換回站台預設界限群組的預設後援時間為 120 分鐘。
-    不在與您階層中任何界限群組相關聯之界限上的用戶端會使用其指派站台中的預設站台界限群組，來識別其可以使用的有效站台系統角色。

管理遞補的預設站台界限群組：
- 您可以移至站台預設界限群組的屬性，然後變更 [預設行為] 索引標籤上的值。 您在此處所做的變更適用於此界限群組的「所有」隱含連結。 從另一個界限群組設定此預設站台界限群組的明確連結時，可以覆寫這些設定。
- 您可以移至所建立界限群組的內容，然後變更連至預設站台界限群組之明確連結的值。 當您以分鐘為單位設定切換回或防止切換回的新時間時，該變更只會影響您正在設定的連結。 明確連結的設定會覆寫預設站台界限群組的 [預設行為] 索引標籤上的那些設定。


## <a name="site-assignment"></a>網站指派  
 您可以使用為用戶端指派的站台設定各個邊界群組。  

-   使用自動站台指派的新安裝用戶端，將會加入包含用戶端目前網路位置之界限群組的指派站台。  
-   用戶端在指派到站台後，不會在變更其網路位置的同時變更其站台指派。 例如，如果用戶端漫遊至新的網路位置，而該位置是以擁有不同站台指派之界限群組中的界限所表示，則用戶端的指派的站台將維持不變。  
-   當 Active Directory 系統探索發現新資源時，所探索資源的網路資訊會根據界限群組中的界限進行評估。 此程序會將新資源與指派的站台產生關聯，以供用戶端推入安裝方法使用。  
-   當界限屬於具有不同指派站台的多個界限群組時，用戶端會隨機選取其中一個站台。  
-   界限群組指派站台的變更僅適用於新的站台指派動作。 若先前已將用戶端指派給站台，請勿依界限群組組態 (或其本身網路位置) 的變更重新評估其站台指派。  

如需用戶端站台指派的詳細資訊，請參閱[如何將用戶端指派給 System Center Configuration Manager 中的站台](../../../../core/clients/deploy/assign-clients-to-a-site.md)中的[針對電腦使用自動站台指派](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment)。  

## <a name="distribution-points"></a>發佈點

當用戶端要求的發佈點的位置時，Configuration Manager 會將包含適當類型的站台系統清單傳送給用戶端，所列均與包含用戶端目前網路位置的每個界限群組相關聯：

-   **在軟體發佈期間**，用戶端會要求可部署內容的位置，從發佈點或其他有效的內容來源取得。

-   **在作業系統部署期間**，用戶端會要求可傳送或接收其狀態移轉資訊的位置。  

在內容部署期間，如果用戶端要求無法從其目前界限群組中的來源取得的內容，用戶端會不斷向其目前界限群組中的不同內容來源嘗試要求該內容，直到達到鄰近界限群組或預設站台界限群組的後援期間為止。 如果用戶端仍未能找到內容，接下來會將其內容來源搜尋範圍擴大至包含鄰近界限群組。

不過，如果是隨需發佈且為發佈點未提供的內容，當用戶端要求時，將內容傳送至該發佈點的程序隨即開始，用戶端很可能會在切換回使用鄰近界限群組之前，就找到做為內容來源的伺服器。

## <a name="software-update-points"></a>軟體更新點
從 1702 版開始，用戶端會使用界限群組來尋找新的軟體更新點。 您可以將個別的軟體更新點新增到不同的界限群組，以控制用戶端可以尋找的伺服器。

當您從 1702 之前的版本更新時，所有現有的軟體更新點都會加入至每個站台的預設站台界限群組。 如此可保留更新前行為，用戶端會從您為階層設定的可用軟體更新點集區中選取軟體更新點。  在您選擇將個別的軟體更新點新增至使用受控制選擇與後援行為的不同界限群組之前，都會維持這種行為。


設定的軟體更新點後援行為類似於其他站台系統角色，但有下列幾點需要特別注意︰
- **新用戶端會使用界限群組來選取軟體更新點。** 安裝 1702 版之後，您安裝的新用戶端會選取和已設定界限群組相關聯的軟體更新點。

  這會取代先前行為，即用戶端從共用用戶端樹系的軟體更新點清單中隨機選取軟體更新點。

- **先前安裝的用戶端會繼續使用其目前軟體更新點，直到它們後援以找到新的軟體更新點。** 先前安裝的用戶端以及已有軟體更新點的用戶端將繼續使用該軟體更新點，直到該伺服器無法連線。 這包括繼續使用未與用戶端目前界限群組建立關聯的軟體更新點。

  當用戶端已有無法連線到的軟體更新點，用戶端可以尋找另一個來遞補。 使用後援時，用戶端會收到一份清單，列出其目前界限群組中的所有軟體更新點。 如果它無法在 120 分鐘內找到可用的伺服器，就會切換回其鄰近界限群組和預設站台界限群組。 因為軟體更新點的鄰近群組後援時間設定為 120 分鐘且無法變更，所以會同時切換回這兩個界限群組。 切換回預設站台界限群組的預設期間也是使用 120 分鐘。 當用戶端切換回鄰近和預設站台界限群組時，用戶端會先嘗試連線到鄰近界限群組的軟體更新點，然後再嘗試使用預設站台界限群組的軟體更新點。

  即使該伺服器不在用戶端目前的界限群組中，也繼續使用現有的軟體更新點則是刻意的設計。 原因是用戶端與新的軟體更新點同步處理資料時，軟體更新點的變更可能會導致使用大量網路頻寬。 轉換延遲有助於避免讓網路飽和，讓所有用戶端同時切換至新的軟體會更新點。

- **後援時間的設定：**和其他站台系統角色的後援設定不同，軟體更新點尚不支援以分鐘為單位來設定時間。 相反地，後援行為僅限於下列項目︰  
  - **後援時間 (以分鐘為單位)：** 軟體更新點的此選項會呈現灰色且無法設定。 其設定為 120 分鐘。
  -     **永不後援︰**使用此設定時，您可以防止軟體更新點切換回鄰近界限群組。

## <a name="preferred-management-points"></a>慣用的管理點

 慣用的管理點可讓用戶端識別與用戶端目前網路位置 (或界限) 相關聯的管理點。  

-   用戶端會先嘗試使用其指派站台中的慣用管理點，再使用其指派站台中未設定為慣用的管理點。  
-   若要使用這個選項，您必須針對階層加以啟用，然後設定個別主要站台上的界限群組，以包含應與界限群組相關界限產生關聯的管理點。  
-   設定慣用的管理點且用戶端組織其管理點清單之後，用戶端會將慣用的管理點放在指派的管理點清單頂端 (其中包含來自用戶端指派站台的所有管理點)。  

> [!NOTE]  
>  當用戶端漫遊時 (亦即變更其網路位置，就像從膝上型電腦到遙遠的辦公位置傳輸時)，可能會在嘗試使用其指派站台 (包含偏好管理點) 的管理點前，先使用位於其新位置的本機站台管理點 (或 Proxy 管理點)。  如需詳細資訊，請參閱[了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

### <a name="overlapping-boundaries"></a>重疊界限  
 Configuration Manager 支援內容位置的重疊界限設定：  

-   **當用戶端要求內容時**，若用戶端網路位置屬於多個界限群組，Configuration Manager 會為用戶端傳送一份具有內容的所有發佈點清單。  
-   **當用戶端要求伺服器傳送或接收其狀態移轉資訊時**，若用戶端網路位置屬於多個界限群組，Configuration Manager 會為用戶端傳送一份包含與界限群組 (其包含用戶端目前的網路位置) 相關聯的所有狀態移轉點清單。  

此行為可讓用戶端選取最接近的伺服器，以傳送內容或狀態移轉資訊。  



## <a name="example-of-using-boundary-groups"></a>使用界限群組的範例
下列範例會使用用戶端搜尋發佈點的內容。 這個範例可以套用至使用界限群組的其他站台系統角色。 不過，套用到軟體更新點時，請記住，軟體更新點執行不支援以分鐘為單位設定切換回鄰近群組的時間，而且一律使用 120 分鐘。

您將建立不共用界限或站台系統伺服器三個界限群組：
-    群組 BG_A，以及與該群組相關聯的發佈點 DP_A1 和 DP_A2
-    群組 BG_B，以及與該群組相關聯的發佈點 DP_B1 和 DP_B2
-    群組 BG_C，以及與該群組相關聯的發佈點 DP_C1 和 DP_C2

您會將用戶端的網路位置只新增至 BG_A 界限群組作為界限，接著您會設定從該界限群組到其他兩個界限群組的關聯性：
-    您將設定要在 10 分鐘後使用之第一個「芳鄰」群組 (BG_B) 中的發佈點。 此群組包含發佈點 DP_B1 和 DP_B2。 這兩者會適當地連線到第一個群組界限位置。
-    您將設定要在 20 分鐘後使用的第二個「芳鄰」 群組 (BG_C)。 此群組包含發佈點 DP_C1 和 DP_C2。 這兩者來自其他兩個界限群組並跨 WAN。
-    您也會將位於站台伺服器上的另一個發佈點新增至站台預設站台界限群組。 這是您最少使用的內容來源位置，但它位於所有界限群組的中央。

    界限群組和後援時間的範例：

     ![BG_Fallack](media/BG_Fallback.png)


使用下列設定：
-    用戶端會從其「目前」界限群組 (BG_A) 中的發佈點開始搜尋內容，搜尋每個發佈點兩分鐘，再切換到界限群組中的下一個發佈點。 有效內容來源位置的用戶端集區包含 DP_A1 和 DP_A2。
-    如果用戶端從其「目前」界限群組搜尋 10 分鐘後找不到內容，則會在其搜尋中新增 BG_B 界限群組中的發佈點。 接著會從其結合之發佈點集區中的發佈點繼續搜尋內容，該集區現在包含 BG_A 和 BG_B 界限群組中的發佈點。 用戶端會繼續花兩分鐘的時間連絡每個發佈點，再切換到其集區中的下一個發佈點。 有效內容來源位置的用戶端集區包含 DP_A1、DP_A2、DP_B1 和 DP_B2。
-    如果用戶端在延長的 10 分鐘 (20 分鐘) 後仍然找不到具有內容的發佈點，它會擴充其可用的發佈點集區，加入第二個「芳鄰」群組 (界限群組 BG_C) 中的發佈點。 用戶端現在有 6 個發佈點可供搜尋 (DP_A1、DP_A2、DP_B2、DP_B2、DP_C1 和 DP_C2)，而且會繼續每隔兩分鐘變更為新的發佈點，直到找到內容為止。
-    如果用戶端在總計 120 分鐘後找不到內容，就會切換回加入「預設站台界限群組」作為其繼續搜尋的一部分。 現在，發佈點集區包含已設定之三個界限群組中的所有發佈點，而且最後一個發佈點位於站台伺服器電腦上。  用戶端接著會繼續搜尋內容，每隔兩分鐘變更發佈點一次，直到找到內容為止。

藉由設定在不同的時間使用不同的芳鄰群組，您就可以控制何時將特定發佈點新增為內容來源位置，以及用戶端何時或是否會使用後援當做防護機制，以在任何其他位置都沒有內容時切換回預設站台界限群組。






### <a name="update-existing-boundary-groups-to-the-new-model"></a>將現有的界限群組更新為新的模型
當您更新至 1610 之前的版本時，會自動進行下列設定。 這些設定是為了確保您目前的後援行為在您設定新的界限群組和關聯性之前維持可用。

-    每個主要站台都會建立預設的站台界限群組，其名稱為 ***Default-Site-Boundary-Group&lt;站台碼>。***
  -    主要站台上勾選了 [允許內容的後援來源位置] 的發佈點及狀態移轉點會新增至該站台的 *Default-Site-Boundary-Group&lt;站台碼>* 界限群組。
  -    從 1702 版開始，軟體更新點會新增至每個站台 *Default-Site-Boundary-Group&lt;sitecode>*。
-    系統會為每個現有的界限群組建立一個複本，其中包含設定為低速連線的站台伺服器。 新群組的名稱是 ***&lt;原始界限群組名稱>-&lt;原始界限群組識別碼>***：  
    -    原始界限群組中會保留使用快速連線的站台系統。
    -    連線速度很慢的站台系統複本 (發佈點、管理點) 會加入界限群組的複本。 設定為慢速的原始站台系統會在原始界限群組中保留供回溯相容性，但不會從這些界限群組中使用。
    - 此界限群組複本沒有相關聯的界限。 不過，原始群組與後援時間設定為零的新界限群組複本之間，會建立一個後援連結。  


- **專屬於次要站台︰**
  - 如果次要站台有至少一個勾選了 [允許內容的後援來源位置] 的發佈點或狀態移轉點，即建立界限群組。 界限群組的名稱是 ***Secondary-Site-Neighbor--Tmp&lt;站台碼>。***
  - 所有勾選 [允許內容的後援來源位置] 的發佈點以及狀態移轉點會加入此新建站台的次要站台界限群組。
  - 原始界限群組與新建芳鄰界限群組之間會建立一個後援連結，且後援時間設定為零。


 下表指出結合原始部署設定與發佈點設定之後，您可以預期的新後援行為：

低速網路中之 [不要執行程式] 的原始部署設定  |[允許用戶端使用內容的後援來源位置] 的原始發佈點設定  |新的後援行為  
---------|---------|---------
已選取     |  已選取    |  **沒有後援** - 只使用目前界限群組中的發佈點       
已選取     |  未選取|  **沒有後援** - 只使用目前界限群組中的發佈點       
未選取 |  未選取|  **切換回芳鄰** - 使用目前界限群組中的發佈點，然後新增芳鄰界限群組中的發佈點。 除非設定預設站台界限群組的明確連結，否則用戶端不會切換回該群組。    
未選取 | 已選取        |   **標準後援** - 先使用目前界限群組中的發佈點，再使用芳鄰和站台預設界限群組中的發佈點

 所有其他部署設定都會導致**標準後援**。  




## <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>舊版 UI 和內容位置行為的變更
以下是界限群組及用戶端尋找內容方式的主要變更。 這些變更都是 1610 版所引進。 許多變更和概念會搭配運作。


-    **移除快速或低速的設定︰**您不會再將個別發佈點設定為快速或低速。  相反地，與界限群組相關聯的每個站台系統都會視為相同。 由於這項變更，界限群組內容的 [參考] 索引標籤不再支援快速或低速的設定。
-     **每個站台的新預設界限群組︰**每個主要站台都有新的預設界限群組，名為 ***Default-Site-Boundary-Group&lt;站台碼>***。  如果用戶端不在指派給界限群組的網路位置，該用戶端會從其指派的站台使用與預設群組相關聯的站台系統。 請規劃使用此界限群組，來取代後援內容位置的概念。      
 -    移除 [允許內容的後援來源位置]︰您無法再明確設定要用於後援的發佈點，而且已從 UI 移除此設定選項。

    此外，應用程式部署類型的 [允許用戶端使用內容的後援來源位置] 設定結果已變更。 部署類型的這項設定現在可讓用戶端使用預設站台界限群組作為內容來源位置。

 -    **界限群組關聯性︰**每個界限群組可以連結至一或多個額外的界限群組。 這些連結會形成關聯性，可在名為 [關聯性] 的新界限群組內容索引標籤上設定：
     -    直接與用戶端建立關聯的每個界限群組稱為**目前**界限群組。  
    -     用戶端因其「目前」界限群組與另一個群組之間的關聯而可以使用的任何界限群組，稱為**芳鄰**界限群組。
    -  它位於 [關聯性] 索引標籤上，您可以在其中新增界限群組以作為「芳鄰」界限群組。 您也可以設定時間 (以分鐘為單位)，以決定若使用者無法從「目前」群組中的發佈點找到內容，將於何時從這些「芳鄰」界限群組開始搜尋內容位置。

        當您新增或變更界限群組設定時，您可以選擇防止您設定的目前群組切換回該特定界限群組。

    若要使用新的設定，您可以定義從一個界限群組到另一個界限群組的明確關聯 (連結)，並將該關聯群組中的所有發佈點設定為相同的時間 (以分鐘為單位)。 您設定的時間會決定若用戶端無法從其「目前」界限群組找到內容，可於何時從該芳鄰界限群組開始搜尋內容來源。

    除了明確設定的界限群組之外，每個界限群組還有預設站台界限群組的隱含連結。 此連結會在 120 分鐘後開始生效，此時預設站台界限群組會成為芳鄰界限群組，讓用戶端可使用與該界限群組相關聯的發佈點作為內容來源位置。

    此行為會取代先前稱為內容後援的行為。  您可以覆寫此 120 分鐘的預設行為，方法是將預設站台界限群組明確關聯至「目前」群組，然後以分鐘為單位設定特定時間，或完全封鎖以防止使用後援。


-     **用戶端嘗試從每個發佈點取得內容，最多 2 分鐘︰**當用戶端搜尋內容來源位置時，它會嘗試存取一個發佈點 2 分鐘，再嘗試另一個發佈點。 這是舊版的一項變更，在舊版中，用戶端會嘗試連線到發佈點，最多 2 小時。

    - 用戶端嘗試使用的第一個發佈點，是從用戶端的「目前」界限群組 (或群組) 中可用的發佈點集區隨機選取而來。

    - 如果用戶端在兩分鐘後還找不到內容，則會切換至新的發佈點，並嘗試從該伺服器取得內容。 此程序會每隔兩分鐘重複一次，直到用戶端找到內容或到達其集區中最後一部伺服器為止。

    - 如果用戶端在必須切換回「鄰近」界限群組之前，從其「目前」集區找不到有效的內容來源位置，則用戶端會將該「鄰近」群組中的發佈點新增至其目前清單結尾，然後搜尋包含兩個界限群組之發佈點的擴充來源位置群組。

        > [!TIP]  
        > 如果您建立從目前界限群組到預設站台界限群組的明確連結，並定義比連結至芳鄰界限群組的後援時間更短的後援時間，用戶端在包含芳鄰群組之前，會先從預設站台界限群組開始搜尋來源位置。

    - 當用戶端無法從集區中的最後一部伺服器取得內容時，就會重新開始此程序。


## <a name="procedures-for-boundary-groups"></a>界限群組的程序
下列程序適用於 1610 或更新版本。 如果使用 1610 之前的版本，請參閱 [System Center Configuration Manager 1511 版、1602 版和 1606 版界限群組](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606)中的程序。


### <a name="to-create-a-boundary-group"></a>建立界限群組  
1.  在 Configuration Manager 主控台中按一下 [系統管理] > [階層設定] >  [界限群組]。  

2.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立界限群組] 。  

3.  在 [建立界限群組]  對話方塊中，選取 [一般]  索引標籤並指定此界限群組的 [名稱]  。  

4.  按一下 [確定]  儲存新界限群組。  


### <a name="to-configure-a-boundary-group"></a>設定界限群組  
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

 6.  選取 [關聯性] 索引標籤設定後援行為︰  

     - 按一下 [新增]，然後選取想要設定的界限群組。

     - 設定發佈點的後援時間。 這段時間之後，您要設定關聯性的界限群組中的用戶端，就能夠開始從您要加入的界限群組中搜尋發佈點的內容。

     - 為避免特定界限群組的後援，包括預設設定的「預設站台界限群組」，請選取界限群組然後勾選 [Never fallback] (永不後援) 核取方塊。   

 7.  按一下 [確定]  關閉界限群組內容，並儲存設定。  

#### <a name="to-associate-a-site-systme-server-with-a-boundary-group"></a>將站台系統伺服器與界限群組產生關聯  
 1.  在 Configuration Manager 主控台中按一下 [系統管理] > [階層設定] >  [界限群組]。  

 2.  選取您要修改的界限群組。  

 3.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

 4.  在界限群組的 [內容]  對話方塊中，選取 [參照]  索引標籤。  

 5.  在 [選取站台系統伺服器] 下，按一下 [新增] ，選取要與此界限群組產生關聯之站台系統伺服器的核取方塊，然後按一下 [確定] 。  

 6.  按一下 [確定]  關閉對話方塊，並儲存界限群組設定。  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>設定自動站台指派的後援站台  

  1.  在 Configuration Manager 主控台中按一下 [系統管理] > [站台設定] >  [站台]。  

  2.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [階層設定] 。  

  3.  在 [一般]  索引標籤上，選取 [使用後援站台] 核取方塊，然後從 [後援站台]  下拉式清單中選取站台。  

  4.  按一下 [確定]  儲存設定。  

#### <a name="to-enable-use-of-preferred-management-points"></a>若要允許使用偏好的管理點  

 1.  在 Configuration Manager 主控台中按一下 [系統管理] > [站台設定] > [站台]，然後在 [首頁] 索引標籤上選取 [階層設定]。  

 2.  在 [階層設定] 的 [一般]  索引標籤，選取 [用戶端偏好使用界限群組中指定的管理點] 。  

 3.  按一下 [確定]  關閉對話方塊並儲存組態。  
