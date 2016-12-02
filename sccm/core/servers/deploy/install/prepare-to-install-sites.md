---
title: "準備安裝站台 | System Center Configuration Manager"
description: "閱讀這些詳細資料，以節省安裝多個站台期間的時間，並避免錯誤。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6f240f1da4561c05bee974b78f43bfcdba591df6

---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>準備安裝 System Center Configuration Manager 站台

*適用於：System Center Configuration Manager (最新分支)*

若要準備一或多個 System Center Configuration Manager 站台的成功部署，請熟悉本文中的詳細資訊。 這些步驟可以節省安裝多個站台期間的時間，並協助防止可能會導致需要重新安裝一或多個站台的錯誤步驟。
 > [!TIP]
 >  下列案例與安裝 System Center Configuration Manager 最新分支站台類似但不同：
 > -  **升級**：安裝 System Center Configuration Manager 以從 System Center 2012 Configuration Manager 進行**升級**，請參閱[升級至 System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)
 > -  **更新**：使用主控台內更新以將新的**更新版本**安裝至現有 System Center Configuration Manager 站台，請參閱 [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)
 > -  **移轉**：若要從另一個 Configuration Manager 階層**移轉資料**至目前的 System Center Configuration Manager 階層，請參閱[規劃移轉至 System Center Configuration Manager](../../../../core/migration/planning-for-migration.md)



## <a name="a-namebkmkoptionsa-options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a> 安裝不同類型站台的選項
當您安裝新的 Configuration Manager 時，可使用的原始程式檔版本取決於已在階層 (如果有的話) 中的站台版本，而且可供您使用的安裝方法取決於您想要安裝的站台類型。  

安裝站台之前，請確定您已規劃階層，並了解您要安裝的站台類型。 如需詳細資訊，請參閱[設計站台階層](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)。


### <a name="first-site"></a>第一個站台
您要為階層安裝的第一個站台將是獨立主要站台或管理中心網站。

**安裝媒體**：若要將管理中心網站或獨立主要站台安裝為新階層中的第一個站台，您必須[使用基準版本](../../../../core/servers/manage/updates.md#bkmk_Baselines)的 Configuration Manager。 請不要使用來自任何站台之 [CD.Latest 資料夾](../../../../core/servers/manage/the-cd.latest-folder.md)的已更新來源檔案，來安裝新階層的第一個站台。

**安裝方法**︰您可以使用 [Configuration Manager 安裝精靈](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)來安裝任一種類型的站台，也可以設定指令碼以與[指令式命令列安裝](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)搭配使用。


### <a name="additional-sites"></a>其他站台
安裝初始站台之後，即可隨時新增其他站台。 下列選項可用來新增其他站台 (最多為[支援的限制](../../../../core/plan-design/configs/size-and-scale-numbers.md))：

您擁有的站台          |您可安裝的其他站台  
---------                   |---------
管理中心網站 |   安裝子主要站台            
子主要站台          |   安裝次要站台        
獨立主要站台    |   安裝次要站台<br />展開主要站台，將獨立主要站台轉換至子主要站台

**安裝媒體**：如果您安裝管理中心網站以在獨立主要站台上進行擴充，或在現有階層中安裝新的子主要站台，則必須使用符合現有一或多個站台版本的安裝媒體 (原始程式檔)。
> [!IMPORTANT]
> 如果您所安裝的主控台內更新已變更先前安裝站台的版本，請不要使用原始安裝媒體，而是改成使用更新站台之 [CD.Latest 資料夾](../../../../core/servers/manage/the-cd.latest-folder.md)中的原始程式檔。  Configuration Manager 會要求您使用與新站台將連線之現有站台版本相符的來源檔案。


次要站台必須安裝在 Configuration Manager 主控台內，因此，一律會從父主要站台中使用原始程式檔進行安裝。

**安裝方法**：您用來安裝其他站台的方式取決於所要安裝的站台類型。
-   **新增管理中心網站**：  
您可以使用 Configuration Manager 安裝精靈或指令式命令列，以將新的管理中心網站當成父站台安裝至現有的獨立主要站台。  如需詳細資訊，請參閱[擴充獨立主要站台](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)。
-   **新增子主要站台**：  
您可以使用 Configuration Manager 安裝精靈或命令列安裝，以將子主要站台新增至管理中心網站下方。
-   **新增次要站台**：   
您可以使用 Configuration Manager 主控台，以將次要站台當成子站台安裝至主要站台下方。 次要站台不支援其他方法。



## <a name="a-namebkmktasksa-common-tasks-to-complete-before-starting-an-install"></a><a name="bkmk_tasks"></a> 要在開始安裝之前完成的一般工作
-   了解將要用於部署的階層拓撲    
     (請參閱[為 System Center Configuration Manager 設計站台階層](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md))  

-   準備並設定個別伺服器，以符合與 Configuration Manager 搭配使用的必要條件和支援的設定 (請參閱[站台和站台系統必要條件](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md))  

-   安裝和設定 SQL Server 以裝載站台資料庫 (請參閱    
    [System Center Configuration Manager 的 SQL Server 版本支援](../../../../core/plan-design/configs/support-for-sql-server-versions.md))  

-   準備支援 Configuration Manager 的網路環境 (請參閱[設定準備 Configuration Manager 的防火牆、連接埠和網域](/sccm/core/plan-design/network/configure-firewalls-ports-domains))  

-   如果您將使用 PKI，請準備基礎結構和憑證 (請參閱 [Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)

-   在要當成站台伺服器或站台系統伺服器使用的電腦上安裝最新安全性更新，並在必要時重新啟動電腦。



## <a name="a-namebkmksitecodesa-about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a>  關於站台名稱及站台碼
站台碼和站台名稱是用來識別和管理 Configuration Manager 階層中的站台。 在 Configuration Manager 主控台中，站台碼和站台名稱的顯示格式為 &lt;站台碼\> - &lt;站台名稱\>。 階層中所使用的每個站台碼都必須是唯一的。 如果針對 Configuration Manager 擴充 Active Directory 架構，而且站台正在發行資料，即使站台碼用於不同的 Configuration Manager 階層中，或者，如果站台碼已經用於先前的 Configuration Manager 安裝中，則 Active Directory 樹系中所使用的站台碼必須為唯一代碼。 請務必仔細規劃您的站台碼和站台名稱以部署階層。

### <a name="specify-a-site-code-and-site-name"></a>指定站台碼和站台名稱
在 Configuration Manager 安裝程式期間，系統會提示您輸入管理中心網站、每個主要和次要站台的站台碼和站台名稱以進行安裝。 站台碼必須可唯一識別階層中的每個站台。 因為站台碼會用於資料夾名稱中，所以請勿為站台碼使用下列名稱，它們包含 Configuration Manager 保留名稱和 Windows 保留名稱：
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> Configuration Manager 安裝程式不會驗證您指定的站台碼是否使用中。



若要在 Configuration Manager 安裝期間輸入站台的站台碼，您必須輸入三位英數字元。 指定網站碼時，只允許字母 A 到 Z，數字 0 到 9 或是兩者的組合代碼。 字母或數字的順序不會影響網站間的通訊。 例如，您不需要將主要網站命名為 ABC，並將次要網站命名為 DEF。

網站名稱是此網站的易記名稱識別項。 網站名稱中只可使用標準字母 A 到 Z，小寫 a 到 z，0 到 9 以及連字號 (-)。
> [!IMPORTANT]
> 不支援在安裝後變更網站碼或網站名稱。

### <a name="reuse-a-site-code"></a>重複使用站台碼
站台碼在管理中心網站或主要站台中的 Configuration Manager 階層中不可使用超過一次，即使尚未解除安裝原始站台和站台碼也是一樣。 如果您重複使用站台碼，階層中就會有物件識別碼衝突的風險。 如果 Configuration Manager 階層或 Active Directory 樹系內不再使用站台碼，就可以重複使用次要站台的站台碼。


## <a name="limits-and-restrictions-for-installed-sites"></a>已安裝站台的限制
安裝站台之前，請了解下列站台和階層適用的限制︰
-   完成安裝程式之後，若沒有解除安裝站台，再使用新的值重新安裝，即無法變更以下站台內容：  
    -   程式檔安裝目錄  
    -   站台碼  
    -   站台描述  
-   當階層包含管理中心網站時：  
    -   Configuration Manager 不支援將子主要站台移出階層來建立獨立主要站台，或將它附加至不同的階層。 相反地，請先解除安裝子主要站台，然後將其重新安裝為新的獨立主要站台，或不同階層之管理中心網站的子系。  


## <a name="a-namebkmkoptionalstepsa-optional-steps-to-run-before-starting-setup"></a><a name="bkmk_optionalsteps"></a>  要在啟動安裝程式之前執行的選擇性步驟
**您可以手動執行[安裝程式下載程式](../../../../core/servers/deploy/install/setup-downloader.md)**，以下載 Configuration Manager 的更新版安裝檔案。

當執行安裝程式的電腦未連線到網際網路時，或您預計要安裝多部站台伺服器時，請考慮使用「安裝程式下載程式」來為安裝程式檔下載必要的更新：

-  安裝程式預設會連線至網際網路，下載更新版安裝檔案
-  這些檔案預設會儲存在名為 Redist 的資料夾中
-  您可以將安裝程式指向您先前儲存這些檔案複本的網路位置


**您可以手動執行[先決條件檢查程式](../../../../core/servers/deploy/install/prerequisite-checker.md)**找出並修正問題，再執行安裝程式。 在安裝程式開始安裝站台之前，且在伺服器上安裝站台系統角色之前，可以執行先決條件檢查程式，以確定電腦是否符合裝載該站台或站台系統角色的需求。
 -  安裝程式預設會執行必要條件檢查程式。
 -  如果發生任何錯誤，將會暫止安裝程式，直到問題得到解決為止。


**識別選擇性連接埠** 以用於站台系統與用戶端。
 -  站台系統和用戶端預設會使用預先定義的連接埠進行通訊。
 -  在安裝期間，您可以設定替代連接埠。
 -  如需詳細資訊，請參閱 [System Center Configuration Manager 中使用的連接埠](../../../../core/plan-design/hierarchy/ports.md)。



<!--HONumber=Nov16_HO1-->

