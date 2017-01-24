---
title: "站台的必要條件 | Microsoft Docs"
description: "了解安裝不同類型的 System Center Configuration Manager 站台所需的不同必要條件。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: d39c8acca79c97c3979020c284616038b897d7cf

---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>安裝 System Center Configuration Manager 站台的必要條件

*適用於：System Center Configuration Manager (最新分支)*


下列各節詳述安裝不同類型的 System Center Configuration Manager 站台所需的不同必要條件。



## <a name="primary-sites-and-the-central-administration-site"></a>主要站台和管理中心網站
下列必要條件適用於將管理中心網站安裝為階層的第一個站台、獨立主要站台或子主要站台。 如果您要將管理中心網站安裝為階層擴充案例的一部分，請參閱本主題中的[擴充獨立主要站台](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand
)。

####  <a name="a-namebkmkprereqpria-prerequisites-to-install-a-primary-site-or-central-administration-site"></a><a name="bkmk_PrereqPri"></a> 安裝主要站台或管理中心網站的必要條件  

-   安裝站台的使用者必須擁有下列權限：  

    -   站台伺服器電腦上的**本機系統管理員** 權限  

    -   會裝載**站台資料庫** 的每部電腦上，或是該站台 **本機系統管理員** 的執行個體之 **本機系統管理員** 權限  

    -   在裝載站台資料庫之 SQL Server 執行個體上的**Sysadmin** 權限  

        > [!IMPORTANT]  
        >  安裝完成之後，執行安裝程式的使用者帳戶和網站伺服器電腦帳戶都必須保留 SQL Server 的 sysadmin 權限。 不支援從這些帳戶移除 sysadmin 權限。  

-   安裝主要站台時，需要下列額外的權限：  
    -  在其他將會安裝初始管理點與發佈點的電腦上之**本機系統管理員** 權限 (若不在站台伺服器上)。  

-   在管理中心網站下安裝新的子主要站台時，需要下列額外的權限：  

    -   裝載管理中心網站之電腦上的**本機系統管理員** 權限  

    -   Configuration Manager 內以角色為基礎的系統管理權限，相當於 [基礎結構系統管理員] 或 [系統高權限管理員] 的安全性角色。  

-   您必須使用正確的安裝媒體 (來源檔案)，並從該位置執行安裝程式。 如需用來安裝不同站台的正確來源檔案的相關資訊，請參閱[準備安裝站台](../../../../core/servers/deploy/install/prepare-to-install-sites.md)主題中的[安裝不同類型的站台的選項](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options)。

-   站台伺服器電腦必須能夠從 Microsoft 存取更新版安裝檔案：
    -  開始安裝之前，您可以使用[安裝程式下載程式](../../../../core/servers/deploy/install/setup-downloader.md)下載這些檔案，並將其複本儲存在本機網路。
    -  如果這些檔案的本機複本無法使用，站台伺服器就必須能夠存取網際網路，才可在安裝期間從 Microsoft 下載這些檔案。

  - 擴充已安裝服務連接點站台系統角色的獨立主要站台之前，必須先解除安裝服務連接點。 此角色執行個體在階層中只能有一個，且只可位於該階層的頂層站台。 您將有機會在安裝管理中心網站的期間，重新安裝該角色。
  - 站台伺服器與站台資料庫電腦必須符合所有必要條件組態。 開始安裝之前，可[手動執行必要條件檢查程式](../../../../core/servers/deploy/install/prerequisite-checker.md)來找出問題並加以修正。  


## <a name="a-namebkmkexpanda-expanding-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> 擴充獨立主要站台
獨立主要站台必須符合以下必要條件，您才能將獨立主要站台擴充到具有管理中心網站的階層：


-   **您必須安裝符合獨立主要站台版本的新管理中心網站安裝媒體 (來源檔案)：**  
     若要確保版本相符，請使用獨立主要站台的 [CD.Latest 資料夾](../../../../core/servers/manage/the-cd.latest-folder.md)中找到的來源檔案，來安裝新的站台。

     如需用來安裝不同站台的正確來源檔案的詳細資訊，請參閱[準備安裝站台](../../../../core/servers/deploy/install/prepare-to-install-sites.md)主題中的[安裝不同類型的站台的選項](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options)。


-   **您無法將獨立主要站台設定為從另一個 Configuration Manager 階層移轉資料：**  

     您必須停止從其他 Configuration Manager 階層進行至獨立主要站台的作用中移轉，並移除所有移轉的設定。 這包括尚未完成的移轉作業、資料收集，以及使用中來源階層的設定。  

     這是必要的，原因是移轉作業都是由階層中的頂層站台執行，在您擴充獨立主要站台時，移轉設定並不會移轉到管理中心網站。  

     擴充獨立主要站台後，若您在主要站台上重新設定移轉，則這會是執行移轉相關操作的管理中心網站。 如需如何設定移轉的詳細資訊，請參閱[設定來源階層和來源站台以移轉到 System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)。  

-   **即將裝載全新管理中心網站之電腦的電腦帳戶，必須是獨立主要站台的系統管理員群組成員：**  

     若要成功擴充獨立主要站台，新管理中心網站的電腦帳戶必須是獨立主要站台 [系統管理員]  群組的成員。 這只有在站台擴充期間才需要，而在完成站台擴充後，就可以從主要站台的群組中移除該帳戶。  

-   **執行安裝程式以安裝新管理中心網站的使用者帳戶，必須取得獨立主要站台上以角色為基礎的系統管理權限：**  

     若要在站台擴充案例中安裝管理中心網站，執行安裝程式以安裝管理中心網站的使用者帳戶，必須在獨立主要站台的以角色為基礎的系統管理中，定義為 [系統高權限管理員]  或 [基礎結構系統管理員] 。  

-   **您必須先從獨立主要站台解除安裝以下站台系統角色，才能擴充站台：**  

    -   Asset Intelligence 同步處理點  

    -   Endpoint Protection 點  

    -   服務連接點  

     僅階層中的頂層站台才支援這些站台系統角色。 因此，在擴充獨立主要站台前，必須先解除安裝這些站台系統角色。 擴充站台後，您就可以在管理中心網站重新安裝這些站台系統角色。  

    主要站台上所有其他站台系統角色則仍可維持安裝狀態。  

-   **必須開啟獨立主要站台和將安裝管理中心網站的電腦之間的 SQL Server Service Broker 連接埠：**  

     為了在管理中心網站和主要站台之間成功複寫資料，Configuration Manager 要求兩個站台之間必須開啟連接埠讓 SQL Server Service Broker 使用。 當您安裝管理中心網站並展開獨立主要站台時，必要條件檢查未證實主要站台上已開啟您為 SQL Server Service Broker 指定的連接埠。  


## <a name="a-namebkmksecondarya-secondary-sites"></a><a name="bkmk_secondary"></a> 次要站台
下列是安裝次要站台的必要條件：
-   在 Configuration Manager 主控台中設定安裝次要站台的系統管理使用者，必須具備以角色為基礎的系統管理權限，相當於 [基礎結構系統管理員] 或 [系統高權限管理員] 的安全性角色。  

-   父主要站台的電腦帳戶，必須是次要站台伺服器電腦上的 **本機系統管理員** 。  

-   次要網站使用先前安裝的 SQL Server 執行個體來裝載次要網站資料庫時：  

    -   父主要站台的 **電腦帳戶** ，在次要站台伺服器電腦上的 SQL Server 執行個體上，必須具備 **sysadmin** 權限。  

    -   次要站伺服器電腦的 **本機系統** 帳戶，在次要站台伺服器電腦上的 SQL Server 執行個體上，必須具備 **sysadmin** 權限。  

        > [!IMPORTANT]  
        >  安裝程式完成之後，這兩個帳戶對 SQL Server 必須保有 sysadmin 權限。 不支援從這些帳戶移除 sysadmin 權限。  

-   次要站台伺服器電腦必須符合所有必要條件的組態，其中包括 SQL Server 與管理點和發佈點的預設站台系統角色。  



<!--HONumber=Dec16_HO3-->


