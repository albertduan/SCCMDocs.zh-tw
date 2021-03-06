---
title: "規劃軟體更新 | Microsoft Docs"
description: "在 System Center Configuration Manager 生產環境中使用軟體更新之前，請務必先規劃軟體更新點基礎結構。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 06/27/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: 8b739a01a6bb5cacf0f7109e2e6fa3b31dd666d3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-software-updates-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中規劃軟體更新

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 生產環境中使用軟體更新之前，請務必先進行規劃程序。 成功的軟體更新實作一定要有良好的軟體更新點基礎結構計劃。

## <a name="capacity-planning-recommendations-for-software-updates"></a>軟體更新的容量規劃建議  
 您可以使用下列建議做為基準，協助您判定適用於組織的軟體更新容量規劃資訊。 實際的容量需求可能會依下列準則而與本主題中列出的建議有所不同：您的特定網路環境、用於裝載軟體更新點站台系統的硬體、安裝的用戶端數目，以及安裝在伺服器上的站台系統角色。  

###  <a name="BKMK_SUMCapacity"></a> 軟體更新點的容量規劃  
 支援的用戶端數目，取決於軟體更新點上執行的 Windows Server Update Services (WSUS) 版本，同時也取決於是否存在與其他站台系統角色共存的軟體更新點站台系統角色：  

-   當軟體更新點電腦上執行的是 WSUS，而且軟體更新點與其他站台系統角色共存時，軟體更新點最多可支援 25,000 個用戶端。  

-   當遠端電腦符合 WSUS 需求、將 WSUS 與 Configuration Manager 搭配使用，而且您設定了下列各項時，軟體更新點就能支援多達 150,000 個用戶端：

    IIS 應用程式集區：
    - 將 WsusPool 佇列長度增加至 2000
    - 將 WsusPool 專用記憶體限制增加為 4 倍，或設為 0 (無限制)      

    如需軟體更新點的硬體需求詳細資訊，請參閱[站台系統的建議硬體](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems)。

-   根據預設，Configuration Manager 不支援將軟體更新點設定為 NLB 叢集。 在 Configuration Manager 版本 1702 之前，您可以使用 Configuration Manager SDK，在 NLB 叢集上設定最多四個軟體更新點。 不過，從 Configuration Manager 版本 1702 開始，不支援使用 NLB 叢集作為軟體更新點，而且如果偵測到此設定，將會封鎖升級至 Configuration Manager 版本 1702 的動作。

### <a name="capacity-planning-for-software-updates-objects"></a>軟體更新物件的容量規劃  
 使用下列容量資訊規劃軟體更新物件。  

-   **部署中有 1000 個軟體更新的限制**  

     您必須將各軟體更新部署的軟體更新數目限制為 1000。 當您建立自動部署規則時，可指定傳回的軟體更新數目限制準則。 自動部署規則會在您指定傳回超過 1000 個軟體更新的準則時失敗。 您可以從 Configuration Manager 主控台的 [自動部署規則] 節點檢查自動部署規則的狀態。 當您手動部署軟體更新時，請勿選取部署多於 1000 個軟體更新。  

     您也必須在設定基準中將軟體更新數目限制為 1000。 如需詳細資訊，請參閱[建立設定基準](../../compliance/deploy-use/create-configuration-baselines.md)。

##  <a name="BKMK_SUPInfrastructure"></a> 判斷軟體更新點基礎結構  
 管理中心網站和所有子主要站台必須擁有將部署軟體更新的軟體更新點。 當您在規劃軟體更新點基礎結構時，必須判斷下列相依性：
 - 安裝站台軟體更新點的位置
 - 哪些站台需要可接受來自網際網路用戶端之通訊的軟體更新點
 - 次要站台是否需要軟體更新點。

使用以下各節，判斷軟體更新點基礎結構。  

> [!IMPORTANT]  
>  如需軟體更新所需之內部和外部相依性的資訊，請參閱[軟體更新的必要條件](prerequisites-for-software-updates.md)。  

 您可以在 Configuration Manager 主要站台上新增多個軟體更新點。 可在提供容錯功能的站台上擁有多個軟體更新點，而不需要使用複雜的 NLB。 不過，您使用多個軟體更新點接收的容錯移轉不像 NLB 所提供單純負載平衡那麼穩固，但是它是針對容錯所設計。 同時，軟體更新點的容錯移轉設計與設計管理點所使用單純的隨機模型不同。 和管理點的設計不同，在軟體更新點中，用戶端和網路效能成本與切換至新軟體更新點相關聯。 當用戶端切換至新的 WSUS 伺服器以掃描軟體更新時，會導致類別目錄大小增加，並且會提高相關聯用戶端及網路效能的需求。 因此，用戶端會與其順利掃描的上一個軟體更新點保留親和性。  

 您在主要站台上安裝的第一個軟體更新點，即是您在主要站台上新增之所有其他軟體更新點的同步處理來源。 在您新增軟體更新點並起始軟體更新同步處理後，可以從 [監視]  工作區的 [軟體更新點同步處理狀態]  節點檢視軟體更新點的狀態和同步處理來源。  

 當軟體更新點失敗，且該軟體更新點已設定為站台上其他軟體更新點的同步處理來源時，您必須手動移除失敗的軟體更新點，並選取新的軟體更新點做為同步處理來源。 如需如何移除軟體更新點的詳細資訊，請參閱[移除軟體更新點站台系統角色](../get-started/remove-a-software-update-point.md)。  

###  <a name="BKMK_SUPList"></a> 軟體更新點清單  
 Configuration Manager 在下列案例中會為用戶端提供軟體更新點清單：當新的用戶端接收到啟用軟體更新的原則時，或當用戶端無法與其軟體更新點連線，並需要切換至其他軟體更新點時。 用戶端會從清單中隨機選取一個軟體更新點，但會優先選取位於相同樹系中的軟體更新點。 Configuration Manager 為用戶端提供的清單會依用戶端的類型而有所不同。  

-   **以內部網路為基礎的用戶端**：您可以設定為只允許內部網路連線接收軟體更新點清單，或允許網際網路和內部網路用戶端連線接收軟體更新點清單。  

-   **以網際網路為基礎的用戶端**：您可以設定為只允許網際網路連線接收軟體更新點清單，或允許網際網路和內部網路用戶端連線接收軟體更新點清單。  

###  <a name="BKMK_SUPSwitching"></a> 軟體更新點切換  
> [!NOTE]
> 從 1702 版開始，用戶端會使用界限群組來尋找新的軟體更新點，並在目前的軟體更新點已不再可供存取的情況下，尋找新的軟體更新點來遞補。 您可以將個別的軟體更新點新增到不同的界限群組，以控制用戶端可以尋找的伺服器。 如需詳細資訊，請參閱[設定界限群組](/sccm/core/servers/deploy/configure/boundary-groups)主題中的[軟體更新點](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)。

如果站台擁有多個軟體更新點，而其中有某一個軟體更新點失敗或無法使用，用戶端將會連線至不同的軟體更新點，並繼續掃描最新的軟體更新。 當用戶端第一次獲指派軟體更新點時，除非無法在該軟體更新點上掃描軟體更新，否則會保持指派給該軟更新點。  

軟體更新的掃描可能會失敗好幾次，並傳回非重試錯誤碼。 當掃描失敗且傳回重試錯誤碼時，用戶端會開始進行重試程序，以掃描軟體更新點上的軟體更新。 導致傳回重試錯誤碼的高層級狀態，通常是因為無法與 WSUS 伺服器連線，或是發生暫時性的超載情形。 用戶端會在無法掃描軟體更新時使用下列程序：  

1.  用戶端會在排程時間掃描軟體更新，或在透過用戶端的控制台或使用 SDK 起始時掃描軟體更新。 如果掃描失敗，用戶端會等待 30 分鐘重試掃描，並且會使用相同的軟體更新點。  

2.  用戶端最少會依 30 分鐘的間隔重試四次。 當第四次重試失敗，並再等待兩分鐘後，用戶端將會移至軟體更新點清單中的下一個軟體更新點。  

3.  用戶端在新的軟體更新點上會經歷相同的程序。 掃描成功後，用戶端將會繼續與新的軟體更新點連線。

 下列清單提供您可在考量軟體更新點重試及切換案例時使用的其他資訊：  

-   如果用戶端與公司內部網路中斷連線，並且無法掃描軟體更新，該用戶端會切換至另一個軟體更新點。 這是預期發生的失敗情形，因為用戶端無法與公司網路或允許內部網路連線的軟體更新點連線。 Configuration Manager 用戶端會判斷內部網路軟體更新點的可用性。  

-   如果已啟用以網際網路為基礎的用戶端管理，而且有多個軟體更新點已設定為接受網際網路用戶端通訊，則會依照上一個案例所述的標準重試程序進行切換程序。  

-   如果掃描程序已啟動，但用戶端在掃描完成前關機，此情況不會視為掃描失敗，也不會將此狀況計為四次重試的計數中。  

當 Configuration Manager 收到下列任一 Windows Update 代理程式錯誤碼時，它會讓用戶端重試連線︰  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

若要查閱錯誤碼的意義，您必須將十進位的錯誤碼轉換成十六進位，然後在 [Windows Update Agent - Error Codes Wiki](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx) (Windows Update 代理程式 - 錯誤碼 Wiki) 此類站台上，搜尋十六進位值。


###  <a name="BKMK_ManuallySwitchSUPs"></a>手動將用戶端切換到新軟體更新點
從 Configuration Manager 版本 1606 開始，您可以啟用讓 Configuration Manager 用戶端在主動式軟體更新點發生問題時切換到新軟體更新點的選項。 只有在用戶端從管理點接收到多個軟體更新點時，此選項才會導致變更。

> [!IMPORTANT]    
> 當您切換裝置以使用新伺服器時，裝置就會使用後援設定來尋找新伺服器。 因此，在開始這項變更之前，請先檢閱您的界限群組設定，確定軟體更新點均位於正確的界限群組中。 如需詳細資訊，請參閱[軟體更新點](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)。
>
> 切換到新的軟體更新點會產生額外的網路流量。 流量取決於您的 WSUS 組態設定 (更新分類、產品，軟體更新點是否共用 WSUS 資料庫等等)。 如果您打算切換多個裝置，請考慮在維護期間進行，以降低新的軟體更新點伺服器同步處理期間對網路的影響。

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>啟用切換軟體更新點的選項  
在裝置集合或一組選取的裝置上啟用此選項。 啟用之後，用戶端會在下次掃描時尋找另一個軟體更新點。

1.  在 Configuration Manager 主控台中，移至 **[資產與相容性] > [概觀] > [裝置集合]**。  

2.  在 [常用] 索引標籤的 [及] 群組中，按一下 [用戶端通知]，然後按一下 [切換至下一個軟體更新點]。  


###  <a name="BKMK_SUP_CrossForest"></a> 不受信任樹系中的軟體更新點  
 您可以在站台上建立一個或多個軟體更新點，以支援不受信任樹系中的用戶端。 若要在其他樹系中新增軟體更新點，您必須先在樹系中安裝及設定 WSUS 伺服器。 接著，再啟動精靈以新增具有軟體更新點站台系統角色的 Configuration Manager 站台伺服器。 在精靈中設定下列設定，即可與不受信任樹系中的 WSUS 順利連線：  

-   指定可存取樹系中 WSUS 伺服器的站台系統安裝帳戶。  

-   指定要用於連線至 WSUS 伺服器的 WSUS 伺服器連線帳戶。  

 例如，您的樹系 A 中有一個主要站台，以及兩個軟體更新點 (SUP01 和 SUP02)。 同時，針對相同的主要站台，您在樹系 B 中有兩個軟體更新點 (SUP03 和 SUP04)。當此例中發生切換情形時，會優先使用來自與用戶端相同之樹系的軟體更新點。  

###  <a name="BKMK_WSUSSyncSource"></a> 在頂層站台上使用現有 WSUS 伺服器作為同步處理來源  
 通常會在階層的頂層站台設定與 Microsoft Update 同步處理軟體更新中繼資料。 當您的公司安全性原則不允許從頂層站台存取網際網路時，您可以為頂層站台設定同步處理來源，使用不在您 Configuration Manager 階層中的現有 WSUS 伺服器。 例如，您在可存取網際網路的 周邊網路 中安裝 WSUS 伺服器，但頂層站台則沒有。 您可以在 周邊網路 中將 WSUS 伺服器設定為軟體更新中繼資料的同步處理來源。 您必須確定 DMZ 同步處理軟體更新中的 WSUS 伺服器符合 Configuration Manager 階層中所需的準則。 否則，頂層站台可能不會與預期的軟體更新同步處理。 當您安裝軟體更新點時，設定可存取 周邊網路 中 WSUS 伺服器的 WSUS 連線帳戶，並確認防火牆允許適當連接埠的流量。 如需詳細資訊，請參閱[軟體更新點用來同步處理來源的連接埠](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS)。  

###  <a name="BKMK_NLBSUPSP1"></a> 設定為使用 NLB 的軟體更新點  
 軟體更新點切換可能會解決您的容錯需求。 根據預設，Configuration Manager 不支援將軟體更新點設定為 NLB 叢集。 在 Configuration Manager 版本 1702 之前，您可以使用 Configuration Manager SDK，在 NLB 叢集上設定最多四個軟體更新點。 不過，從 Configuration Manager 版本 1702 開始，不支援使用 NLB 叢集作為軟體更新點，而且如果偵測到此設定，將會封鎖升級至 Configuration Manager 版本 1702 的動作。 如需 Set-CMSoftwareUpdatePoint PowerShell Cmdlet 的詳細資訊，請參閱 [Set-CMSoftwareUpdatePoint](http://go.microsoft.com/fwlink/?LinkId=276834)。

###  <a name="BKMK_SUPSecSite"></a> 次要站台上的軟體更新點  
 軟體更新點在次要站台上是選用項目。 當您在次要站台上安裝軟體更新點時，會將 WSUS 資料庫設定為父主要站台上預設軟體更新點的複本。 您可以只在次要站台上安裝一個軟體更新點。 當次要站台未安裝軟體更新點時，指派給次要站台的裝置會設定為使用父站台上的軟體更新點。 當指派給次要站台之裝置和父主要站台的軟體更新點之間的網路頻寬有所受限，或軟體更新點接近容量限制時，您通常會在次要站台上安裝軟體更新點。 順利安裝軟體更新點並在次要站台上進行設定後，會針對指派給站台的用戶端電腦更新全站台原則，同時會開始使用新的軟體更新點。  

##  <a name="BKMK_SUPInstallation"></a> 規劃軟體更新點安裝  
 請先根據您的 Configuration Manager 基礎結構考量幾項需求，再於 Configuration Manager 中建立軟體更新點站台系統角色。 當您將軟體更新點設定為使用 SSL 進行通訊時，請務必檢閱本節的內容，因為您必須針對階層的軟體更新點採取其他步驟才能夠正常運作。 本節提供有關您必須採取某些步驟才能順利規劃及準備軟體更新點安裝的資訊。  

###  <a name="BKMK_SUPSystemRequirements"></a> 軟體更新點的需求  
 必須在符合 WSUS 的最低需求及支援 Configuration Manager 站台系統設定的站台系統上，安裝軟體更新點站台系統角色。  

-   如需 Windows Server 2012 中 WSUS 伺服器角色的最低需求詳細資訊，請參閱 Windows Server 2012 文件庫中的[檢查考量及系統需求](https://technet.microsoft.com/library/hh852344.aspx#BKMK_1.1)。  

-   如需 Configuration Manager 站台系統所支援設定的詳細資訊，請參閱[站台及站台系統必要條件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

###  <a name="BKMK_PlanningForWSUS"></a> 規劃 WSUS 安裝  

軟體更新需要在您針對軟體更新點站台系統角色所設定的所有站台系統伺服器上安裝支援版本的 WSUS。 此外，當您未在站台伺服器上安裝軟體更新點時，必須在站台伺服器電腦上安裝 WSUS 管理主控台 (如果尚未安裝)。 如此做可讓站台伺服器與軟體更新點上執行的 WSUS 進行通訊。  

 當您在 Windows Server 2012 上使用 WSUS 時，必須設定額外的權限，以允許 Configuration Manager 中的 **WSUS Configuration Manager** 連線至 WSUS，以便執行定期的健全狀況檢查。 選擇下列其中一個選項以設定權限：  

-   新增 [SYSTEM]  帳戶至 [WSUS Administrators]  群組  

-   新增 [NT AUTHORITY\SYSTEM]  帳戶做為 WSUS 資料庫 (SUSDB) 的使用者，並設定最小的 webService 資料庫角色成員資格  

 如需有關如何在 Windows Server 2012 上安裝 WSUS 的詳細資訊，請參閱 Windows Server 2012 文件庫中的 [安裝 WSUS 伺服器角色](http://go.microsoft.com/fwlink/p/?LinkId=272355) 。  

 當您在主要站台安裝一個以上的軟體更新點時，請在相同的 Active Directory 樹系中針對各軟體更新點使用相同的 WSUS 資料庫。 如果您共用相同資料庫，則當用戶端切換至新的軟體更新點時，可能會大幅度減輕，但不完全排除可能遭遇到的用戶端和網路效能的影響。 當用戶端切換到與舊的軟體更新點共用資料庫的新軟體更新點時，仍會進行差異掃描，但此掃描遠低於 WSUS 伺服器自己擁有資料庫的情況。  

####  <a name="BKMK_CustomWebSite"></a> 將 WSUS 設定為使用自訂網站  
 當您安裝 WSUS 時，可以選擇使用現有 IIS 預設網站，或建立自訂 WSUS 網站。 為 WSUS 建立自訂網站可讓 IIS 在專用的虛擬網站上裝載 WSUS 服務，而不是共用與其他 Configuration Manager 站台系統或其他應用程式使用的相同網站。 當您在站台伺服器上安裝軟體更新點站台系統角色時，更是如此。 當您在 Windows Server 2012 或 Windows Server 2016 中執行 WSUS 時，預設會將 WSUS 設定為針對 HTTP 使用連接埠 8530，並針對 HTTPS 使用連接埠 8531。 您必須在建立站台的軟體更新點時指定這些連接埠設定。  

####  <a name="BKMK_WSUSInfrastructure"></a> 使用現有 WSUS 基礎結構  
 在將 Configuration Manager 安裝為軟體更新點之前，您可以選取在您環境中作用的 WSUS 伺服器。 設定軟體更新點時，您必須指定同步處理設定。 Configuration Manager 會連線至在軟體更新點伺服器上執行的 WSUS 伺服器，並且以相同的設定值設定 WSUS。 如果您在將 WSUS 設定為軟體更新點之前，將它與未設定為軟體更新點同步處理設定之一部分的產品或分類進行同步處理，則無論您針對軟體更新點所設定的同步處理設定為何，產品與分類的軟體更新中繼資料皆會針對 WSUS 資料庫中所有的軟體更新中繼資料同步處理。 如此可能導致站台資料庫中的軟體更新中繼資料與預期不符。 當您將產品或分類直接新增至 WSUS 管理主控台，然後立即啟動同步處理時，將會經歷相同的行為。 根據預設，Configuration Manager 每小時都會連線至軟體更新點上的 WSUS，並且重設任何在 Configuration Manager 以外修改的設定。 與您在同步處理設定中所指定的產品和分類不符的軟體更新會設定為到期，然後從站台資料庫中予以移除。

 當 WSUS 伺服器設定為軟體更新點時，就無法將它當作獨立的 WSUS 伺服器使用。 如果您需要未受 Configuration Manager 管理的個別獨立 WSUS 伺服器，則您必須在不同的伺服器上設定它。

####  <a name="BKMK_WSUSAsReplica"></a> 將 WSUS 設定為複本伺服器  
 當您在主要站台伺服器上建立軟體更新點站台系統角色時，您無法使用設定為複本的 WSUS 伺服器。 當 WSUS 伺服器設定為複本時，Configuration Manager 無法設定 WSUS 伺服器，而 WSUS 也會無法同步處理。 在次要站台上建立軟體更新點時，Configuration Manager 會將 WSUS 設定為父主要站台軟體更新點上執行的 WSUS 複本伺服器。 您在主要站台安裝的第一個軟體更新點就是預設的軟體更新點。 站台的其他軟體更新點會設定為預設軟體更新點的複本。  

####  <a name="BKMK_WSUSandSSL"></a> 決定是否要將 WSUS 設定為使用 SSL  
 您可以使用 SSL 通訊協定來確保軟體更新點上執行的 WSUS 的安全。 WSUS 會使用 SSL 驗證對 WSUS 伺服器通訊的用戶端電腦與下游 WSUS 伺服器。 WSUS 還會使用 SSL 將軟體更新中繼資料加密。 當您選擇以 SSL 確保 WSUS 的安全時，必須在安裝軟體更新點之前準備好 WSUS 伺服器。  

 當您安裝並設定軟體更新點時，必須選取 [為 WSUS 伺服器啟用 SSL 通訊]  設定。 否則，Configuration Manager 就不會設定 WSUS 使用 SSL。 當您為軟體更新點上執行的 WSUS 啟用 SSL 時，在任何子站台的軟體更新點上執行的 WSUS 也都必須設定為使用 SSL。  

###  <a name="BKMK_ConfigureFirewalls"></a> 設定防火牆  
 Configuration Manager 管理中心網站上的軟體更新會與軟體更新點上執行的 WSUS 通訊，WSUS 則依次與同步處理來源通訊以同步處理軟體更新中繼資料。 子站台上的軟體更新點會與父站台上的軟體更新點通訊。 當主要站台中有一個以上的軟體更新點時，站台安裝的第一個軟體更新點為預設軟體更新點，其他軟體更新點必須與其進行通訊。  

 在下列情形中，防火牆可能需要設定為接受 WSUS 所使用的 HTTP 或 HTTPS 連接埠：當 Configuration Manager 軟體更新點與網際網路之間有企業防火牆時；當您擁有軟體更新點與其上游同步處理來源時；或者當您擁有額外軟體更新點時。 與 Microsoft Update 的連線一律設定為 HTTP 使用連接埠 80 以及 HTTPS 使用連接埠 443。 您可以將自訂連接埠用於子站台軟體更新點上執行的 WSUS 與父站台軟體更新點上執行的 WSUS的連線。 當您的安全原則不允許連線時，您必須使用匯出和匯入同步處理方式。 如需詳細資訊，請參閱本主題中的 [同步處理來源](#BKMK_SyncSource) 一節。 如需 WSUS 所使用連接埠的詳細資訊，請參閱[如何判斷 WSUS 在 System Center Configuration Manager 中使用的連接埠設定](../get-started/install-a-software-update-point.md#wsus-settings)。  

#### <a name="restrict-access-to-specific-domains"></a>限制對特定網域的存取權  
 如果貴組織不允許將連接埠與通訊協定開放給主動式軟體更新點與網際網路之間防火牆上的所有位址，您可以限制以下網域的存取權，讓 WSUS 與自動更新可以與 Microsoft Update 通訊：  

-   http://windowsupdate.microsoft.com

-   http://*.windowsupdate.microsoft.com  

-   https://*.windowsupdate.microsoft.com  

-   http://*.update.microsoft.com  

-   https://*.update.microsoft.com  

-   http://*.windowsupdate.com  

-   http://download.windowsupdate.com  

-   http://download.microsoft.com  

-   http://*.download.windowsupdate.com  

-   http://test.stats.update.microsoft.com  

-   http://ntservicepack.microsoft.com  

 在下列情況中，您可能需要將以下位址新增至位於兩個站台系統之間的防火牆：如果子站台具有軟體更新點或者如果站台有遠端主動式以網際網路為基礎的軟體更新點：  

 **子站台上的軟體更新點**  

-   http://<子站台上軟體更新點的 FQDN>  

-   https://<子站台上軟體更新點的 FQDN>  

-   http://<父站台上軟體更新點的 FQDN>  

-   https://<父站台上軟體更新點的 FQDN>  

##  <a name="BKMK_SyncSettings"></a> 規劃同步處理設定  
 Configuration Manager 中的軟體更新同步處理是指根據您設定的準則擷取軟體更新中繼資料的程序。 在階層中的頂層站台、管理中心網站或獨立主要站台會從 Microsoft Update 同步處理軟體更新。 您可以選擇將頂層站台上的軟體更新點設定為與現有 WSUS 伺服器同步處理，而不是在 Configuration Manager 階層中。 子主要站台會同步處理管理中心網站上軟體更新點的軟體更新中繼資料。 在您安裝並設定軟體更新點之前，請使用本節規劃同步處理設定。  

###  <a name="BKMK_SyncSource"></a> 同步處理來源  
 軟體更新點的同步處理來源設定會指定軟體更新點擷取軟體更新中繼資料的位置，以及是否在同步處理程序期間建立 WSUS 報告事件。  

-   **同步處理來源：** 根據預設，頂層站台的軟體更新點會設定 Microsoft Update 的同步處理來源。 您可以選擇以現有的 WSUS 伺服器同步處理頂層站台。 子主要站台上的軟體更新點會根據預設將同步處理來源設定為管理中心網站的軟體更新點。  

    > [!NOTE]  
    >  您在主要站台安裝的第一個軟體更新點 (即預設的軟體更新點) 會與管理中心網站同步處理。 主要站台上的其他軟體更新點則會與主要站台上的預設軟體更新點同步處理。  

     當軟體更新點與 Microsoft Update 或上游更新伺服器中斷連線時，您可以將同步處理來源設定為不與設定的同步處理來源同步處理，改為使用 WSUSUtil 工具的匯出與匯入功能同步處理軟體更新。 如需詳細資訊，請參閱[從已中斷連線的軟體更新點同步處理軟體更新](../get-started/synchronize-software-updates-disconnected.md)。  

-   **WSUS 報告事件:** 用戶端電腦上的 Windows Update 代理程式可以建立用於 WSUS 報告的事件訊息。 在 Configuration Manager 中的軟體更新並不使用這些事件，因此預設為選取 [不要建立 WSUS 報告事件] 選項。 沒有建立這些事件時，軟體更新評估與相容性掃描期間是用戶端電腦唯一應該連線至 WSUS 伺服器的時間。 如果需要這些事件用於報告 Configuration Manager 中軟體更新以外的範圍，您將需要修改此設定以建立 WSUS 報告事件。  

###  <a name="BKMK_SyncSchedule"></a> 同步處理排程  
 您只能在 Configuration Manager 階層中頂層站台上的軟體更新點設定同步處理排程。 當您設定同步處理排程時，軟體更新點會在您指定的日期和時間進行與同步處理來源的同步處理。 自訂排程則可讓您在 WSUS 伺服器、站台伺服器以及網路的需求量較低的日期和時間同步處理軟體更新，例如每週上午 2:00 進行一次。 或者，您也可以使用 Configuration Manager 主控台中 [所有軟體更新] 或 [軟體更新群組] 節點的 [同步處理軟體更新] 動作，起始頂層站台上的同步處理。  

> [!TIP]  
>  請使用適合您環境的時間範圍來排程執行軟體更新同步處理的時間。 常見的情形是設定為在 Microsoft 每個月的第二個星期二 (一般稱為 Patch Tuesday (周二修補日)) 的定期安全性更新發行後，馬上執行軟體更新同步處理。 另一種常見的情形是將軟體更新同步處理排程，設定為在每天當您使用軟體更新執行 Endpoint Protection 定義和引擎更新時執行。  

 在軟體更新點成功完成同步處理後，會傳送同步處理要求至子站台。 如果您在主要站台有其他軟體更新點，則會將同步處理要求傳送至各個軟體更新點。 此程序會在階層中的每個站台上重複。  

###  <a name="BKMK_UpdateClassifications"></a> 更新分類  
 每個軟體更新都利用有助於組織不同類型更新的更新分類來加以定義。 在同步處理程序期間，將會同步處理指定分類的軟體更新中繼資料。 Configuration Manager 可讓您以下列更新分類來同步處理軟體更新：  

-   **重大更新：** 針對特定問題指定廣為發行的更新，以解決重大、與安全性無關的錯誤。  

-   **定義更新：** 將更新指定至病毒或其他定義檔案。  

-   **Feature Pack：** 指定產品版本範圍以外的新產品功能以及一般包含在下一個完整產品版本的功能。  

-   **安全性更新：** 針對產品特定、與安全相關的問題，指定廣為發行的更新。  

-   **Service Pack：** 指定適用於應用程式的累計 Hotfix 集。 這些 Hotfix 可能包含安全性更新、重大更新、軟體更新等。  

-   **工具：** 指定有助於完成一項或多項工作的公用程式或功能。  

-   **更新彙總套件：** 指定封裝在一起以便於部署的累計 Hotfix 集。 這些 Hotfix 可能包含安全性更新、重大更新、更新等。 更新彙總套件一般處理特定領域，例如安全性或產品元件。  

-   **更新：** 指定給目前已安裝的應用程式或檔案的更新。  

 更新分類設定只會在頂層站台上設定。 更新分類設定不會在子站台的軟體更新點上設定，因為軟體更新中繼資料是從頂層站台覆寫至子主要站台。 當您選取更新分類時，請留意選取的分類越多，同步處理軟體更新中繼資料的時間就會越長。  

> [!WARNING]  
>  最佳做法是在您第一次同步處理軟體更新之前清除所有分類。 在初始同步處理後，從 [軟體更新點元件內容] 選取分類，然後重新初始同步處理。  

###  <a name="BKMK_UpdateProducts"></a> 產品  
 各個軟體更新的中繼資料會針對適用的更新定義一項或多項產品。 產品即為特定版本的作業系統或應用程式。 產品的範例有 Microsoft Windows Server 2008， 而產品系列則是指衍生出個別產品的基礎作業系統或應用程式。 產品系列的範例有 Microsoft Windows，Microsoft Windows Server 2008 就是其中的成員。 您可以指定產品系列或產品系列中的個別產品。  

 當軟體更新適用於多個產品，而且至少已選取其中一個產品來進行同步處理，則所有產品都會顯示於 Configuration Manager 主控台，即使並未選取某些產品。 例如，若 Windows Server 2012 是您訂閱的唯一作業系統，而且若軟體更新適用於 Windows Server 2012 和 Windows Server 2012 Datacenter Edition，則會在站台資料庫中提供兩種產品的軟體更新。  

 只會在頂層站台上設定產品設定。 產品設定不會在子站台的軟體更新點上設定，因為軟體更新中繼資料是從頂層站台覆寫至子主要站台。 當您選取產品，請留意選取的產品越多，同步處理軟體更新中繼資料的時間就會越長。  

> [!IMPORTANT]  
>  Configuration Manager 會儲存一份產品清單，以及您可以在第一次安裝軟體更新點時從中選擇的產品系列。 在您完成軟體更新同步處理之前，可能無法選取在 Configuration Manager 發行後發行的產品和產品系列，因為同步處理會更新可供您選擇的可用產品和產品系列清單。 最佳作法是在您第一次同步處理軟體更新之前清除所有產品。 在初始同步處理後，從 [軟體更新點元件內容] 選取產品，然後重新初始同步處理。  

###  <a name="BKMK_SupersedenceRules"></a>取代規則  
 通常，取代其他軟體更新的軟體更新，會執行下列一個或多個動作：  

-   增強、改進或更新由一個或多個先前發行之更新所提供的修正程式。  

-   提升已取代更新檔案套件的效率，如果已核准安裝更新，則會將其安裝在用戶端電腦上。 例如，已取代的更新可能包含不再與新更新所支援的修正程式或作業系統相關的檔案，因此不會將這些檔案包含在更新的檔案套件中。  

-   更新較新版本的產品。 換句話說，它會更新不再適用於舊版本或產品設定的版本。 如果更新修改為擴充語言支援，更新也可以取代其他更新。 例如，Microsoft Office 的新版修訂版產品更新可能會移除對舊版作業系統的支援，但可能在初始更新版本中新增了對新語言的其他支援。  

 在軟體更新點的內容中，您可以指定已取代的軟體更新立即到期 (以免包含在新的部署中)，並且將現有的部署加上旗標，表示其中含有一個或多個到期的軟體更新。 或者，您也可以指定已取代的軟體更新經過多久以後到期，如此可讓您繼續部署已取代的軟體更新。 在您需要部署已取代的軟體更新時，考慮下列案例：  

-   如果取代的軟體更新只支援較新版本的作業系統，而您的某些用戶端電腦執行的是舊版的作業系統。  

-   如果取代的軟體更新，比其所取代的軟體更新的適用性更加受限。 此情形將不適用於某些用戶端電腦。  

-   如果取代的軟體更新未獲核准部署在您的生產環境。  

    > [!NOTE]  
    > 當 Configuration Manager 將已取代的軟體更新設定為 [已到期] 時，它並不會在 WSUS 中將該更新設定為 [已拒絕]。 但是在執行 WSUS 清除工作時，在 Configuration Manager 中設定為 [已到期] 的更新，將會在 WSUS 伺服器上設定為 [已拒絕] 的狀態，且電腦上的 Windows Update 代理程式將不會再掃描這些更新。 這表示在執行清除工作之前，用戶端將會繼續掃描已到期的更新。 如需 WSUS 清理工作的相關資訊，請參閱[軟體更新維護](/sccm/sum/deploy-use/software-updates-maintenance)。

###  <a name="BKMK_UpdateLanguages"></a> 語言  
 軟體更新點的語言設定，可讓您設定哪些摘要詳細資料的語言 (軟體更新中繼資料) 要與軟體更新同步處理，以及將為軟體更新下載的軟體更新檔案語言。  

#### <a name="software-update-file"></a>軟體更新檔案  
 您在軟體更新點內容中針對 [軟體更新檔案]  所做的設定，會在您於站台下載軟體更新時提供可用的預設語言設定。 您可以在每次下載軟體更新或部署時，修改預設選取的語言。 下載程序進行期間，如果有提供所選語言的軟體更新檔案，則會將已設定語言的軟體更新檔案下載到部署套件來源位置。 接著，再將這些檔案複製到站台伺服器的內容庫，然後再將它們複製到針對套件所設定的發佈點。  

 軟體更新檔案語言設定應搭配環境中最常使用的語言進行設定。 例如，若用戶端電腦已指派給最常使用英文版和日文版作業系統語言的站台，而且該站台上很少使用其他語言，則當您下載或部署軟體更新時，可在 [軟體更新檔案]  欄位中選取 [英文] 和 [日文]。 如此做可讓妳在部署及下載精靈的 [語言選擇]  頁面中使用預設設定。 如此做可避免下載不需要的更新檔案。 此設定會在 Configuration Manager 階層中的各個軟體更新點設定。  

#### <a name="summary-details"></a>摘要詳細資料  
 進行同步處理程序期間，會使用您所指定的語言更新軟體更新的摘要詳細資訊 (軟體更新中繼資料)。 中繼資料提供與軟體更新相關的資訊，例如名稱、描述、更新所支援的產品、更新分類、發行項識別碼、下載 URL、適用性規則等等。  

 摘要詳細資料設定只會在頂層站台上設定。 子站台上的軟體更新點並未設定摘要詳細資料，因為軟體更新中繼資料會使用以檔案為基礎的複寫，從管理中心網站向下複寫到這些站台。 當您選取摘要詳細資料語言時，請只選取您環境中所需的語言。 所選的語言越多，花在同步處理軟體更新中繼資料的時間就越久。 Configuration Manager 會以執行 Configuration Manager 主控台的作業系統地區設定，顯示軟體更新中繼資料。 如果作業系統的地區設定未提供軟體更新的當地語系化內容，則會顯示英文版的軟體更新資訊。  

> [!IMPORTANT]  
>  您必須選取 Configuration Manager 階層中所需的所有摘要詳細資料語言。 當頂層站台的軟體更新點與同步處理來源進行同步處理時，所選的摘要詳細資料語言會判斷所擷取的軟體更新中繼資料。 如果您在至少執行一次同步處理後修改了摘要詳細資料語言，則只有在新的或更新的軟體更新時，才會擷取已修改之摘要詳細資料語言的軟體更新中繼資料。 除非在同步處理來源上變更軟體更新，否則已同步處理的軟體更新，不會使用已修改語言之新中繼資料進行更新。  

##  <a name="BKMK_MaintenanceWindow"></a> 規劃軟體更新維護期間  
 您可以新增專用於軟體更新安裝的維護期間。 這可讓您設定一般的維護期間和用於軟體更新的不同維護期間。 當一般的維護期間和軟體更新維護期間都設定好後，用戶端只會在軟體更新維護期間安裝軟體更新。 如需維護期間的詳細資訊，請參閱[如何在 Configuration Manager 中使用維護期間](../../core/clients/manage/collections/use-maintenance-windows.md)。  

##  <a name="BKMK_RestartOptions"></a> 提供在安裝軟體更新後重新啟動 Windows 10 用戶端的選項
如果需要重新啟動的軟體更新使用 Configuration Manager 來進行部署並安裝於電腦上，則會排定擱置重新啟動，並顯示重新啟動對話方塊。

從 Configuration Manager 版本 1606 開始，只要 Configuration Manager 軟體更新擱置重新啟動，處於 Windows 電源選項的 Windows 10 電腦上就會有 **[更新並重新啟動]**和 **[更新並關機]** 選項。 使用其中一個選項之後，在重新開機之後不會顯示重新啟動對話方塊。

在舊版 Configuration Manager 中，如果 Windows 8 和更新版本的電腦擱置重新啟動，以及使用 Windows 電源選項 (而不是透過重新啟動對話方塊) 關閉或重新啟動電腦，則在重新啟動電腦之後會保留重新啟動對話方塊，而且在設定的期限時仍然需要重新啟動電腦。

## <a name="next-steps"></a>後續步驟
一旦規劃軟體更新，請參閱 [Prepare for software updates management](../get-started/prepare-for-software-updates-management.md) (準備軟體更新管理)。
