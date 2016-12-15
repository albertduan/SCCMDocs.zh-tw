---
title: "用戶端對等快取 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager 部署內容時，針對用戶端內容來源位置使用對等快取。"
ms.custom: na
ms.date: 12/05/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3329c3180899a4de96f5d9fed46f97744cf5e7da
ms.openlocfilehash: e983358e32502a130f95647a11cd73ff4bbef05f

---
# <a name="peer-cache-for-configuration-manager-clients"></a>Configuration Manager 用戶端的對等快取

*適用於：System Center Configuration Manager (最新分支)*

從 System Center Configuration Manager 版本 1610 開始，您可以使用**對等快取**，以協助管理將內容部署至遠端位置的用戶端。 對等快取是一個內建的 Configuration Manager 解決方案，可讓用戶端直接將其本機快取的內容與其他用戶端共用。   

> [!TIP]  
> 在版本 1610，對等快取和用戶端資料來源儀表板都是發行前版本功能。 若要啟用它們，請參閱[使用更新的發行前版本功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。

 -  您可以使用用戶端設定，讓使用端能夠使用對等快取。
 -  若要共用內容，這兩個對等快取用戶端必須都是搜尋內容的用戶端目前界限群組的成員。 當用戶端使用後援來搜尋鄰近界限群組的內容時，鄰近界限群組中的對等快取用戶端不會包含於可用內容來源位置的集區中。 如需目前和鄰近界限群組的詳細資訊，請參閱[界限群組](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups)。
 -  Configuration Manager 用戶端快取中保存的每種內容類型，都可提供給其他使用對等快取的用戶端。
 -  「對等快取」不會取代其他解決方案 (例如 BranchCache) 的使用，而是可並行運作來提供您更多選項以擴充傳統內容部署解決方案。 由於自訂解決方案不依賴 BranchCache，如果您未啟用或使用 Windows BranchCache，這個解決方案仍能運作。

將啟用對等快取的用戶端設定部署至集合之後，該集合的成員就能做為同一個界限群組中其他用戶端的對等內容來源：
 -  以對等內容來源運作的用戶端將會提交已快取至其管理點的可用內容清單。
 -  然後，當該界限群組中的下一個用戶端要求該內容時，就會傳回具有該內容的每個對等快取來源以做為潛在的內容來源，以及該界限群組中的發佈點與其他內容來源位置。
 -  針對每個標準作業程序，搜尋內容的用戶端會從提供給它的來源集區中選取一個內容來源，然後繼續嘗試取得內容。
 -  如果對內容的鄰近界限群組發生了後援，就不會將來自鄰近界限群組的對等快取內容來源位置新增至用戶端潛在內容來源位置的集區。  

即使您可以讓所有用戶端參與對等快取，但最理想的做法是只選擇最適合做為對等快取來源的用戶端。  您可以根據用戶端的底座類型、磁碟空間、網路連線能力及更多項目來評估用戶端的適用性。 如需可協助您選取最適合用於對等快取的最佳用戶端詳細資訊，請參閱[這個由 Microsoft 顧問所維護的部落格](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/)。

為了協助您了解對等快取的用法，您可以檢視 [用戶端資料來源] 儀表板。 請參閱[用戶端資料來源儀表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。


## <a name="requirements-and-considerations-for-peer-cache"></a>對等快取的需求與考量：
- 您必須為您的站台設定一個**網路存取帳戶**，此帳戶要能夠**完全控制**每個用戶端上的快取資料夾。 此資料夾預設為 ***%windir%\ccmcache***。

- 用戶端只能從其目前界限群組中的對等快取用戶端傳輸內容。

-   因為目前的對等快取內容來源界限是根據該用戶端上次硬體清查提交所決定，所以，若用戶端漫遊至位於不同界限群組的網路位置，基於對等快取的目的，仍然可能被視為是其先前界限群組的成員。 這會導致提供給用戶端的對等快取內容來源不在其中繼網路位置上。 我們建議您排除有此設定傾向的用戶端，不要讓其參與對等快取。

## <a name="to-configure-client-peer-cache-client-settings"></a>設定用戶端對等快取的用戶端設定
1.  在 Configuration Manager 主控台中，移至 [系統管理] > [用戶端設定]，然後開啟您要使用的裝置用戶端設定物件。 您也可以修改 [預設用戶端設定] 物件。
2.  從可用的設定清單中，選取 [用戶端快取設定]。
3.  將 [在完整作業系統中啟用 Configuration Manager 用戶端以共用內容] 設為 [是]。
4.  設定下列設定來定義您想要用於對等快取的連接埠：  
  -  **用於初始網路廣播的連接埠**
  -  **為用戶端對等通訊啟用 HTTPS**
  -  **用於從對等節點下載內容的連接埠 (HTTP/HTTPS)**

在為對等快取啟用的每一部電腦上，如果 Windows 防火牆正在使用中，Configuration Manager 就會設定它，以便使用您設定的連接埠。



<!--HONumber=Dec16_HO1-->


