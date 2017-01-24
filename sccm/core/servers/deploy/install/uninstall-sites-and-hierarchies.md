---
title: "解除安裝站台 | Microsoft Docs"
description: "請使用下列詳細資料，作為必須解除安裝 System Center Configuration Manager 站台時的指南。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: f41e70c98c4b2ede575debb868978afa3dad1abc


---
# <a name="uninstall-sites-and-hierarchies-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中解除安裝站台和階層

*適用於：System Center Configuration Manager (最新分支)*

請使用下列詳細資料，作為必須解除安裝 System Center Configuration Manager 站台時的指南。  

若要解除委任包含多個站台的階層，則移除順序十分重要：  

-   從解除安裝階層底部的站台開始，然後向上進行。  

-   先移除連接到主要站台的次要站台  

-   然後移除主要站台  

-   移除所有主要站台之後，您可以解除安裝管理中心站台。  


##  <a name="a-namebkmkremovesecondarysitea-remove-a-secondary-site-from-a-hierarchy"></a><a name="BKMK_RemoveSecondarysite"></a> 從階層中移除次要站台  
您無法將次要網站移動或重新指派至新的父主要網站。 若要從階層中移除次要網站，必須從其直接父網站中將它刪除。 從 Configuration Manager 主控台中，使用 [刪除次要站台精靈] 移除次要站台。 當您移除次要網站時，必須選擇要刪除或解除安裝次要網站：  

-   **解除安裝次要站台**：使用此選項會移除可從網路存取的正常運作次要站台。 此選項會從次要站台伺服器解除安裝 Configuration Manager，然後從 Configuration Manager 階層中刪除站台的所有資訊及其資源。 如果 Configuration Manager 已在安裝次要站台期間安裝 SQL Server Express，Configuration Manager 將在解除安裝次要站台時一併解除安裝 SQL Express。 如果 SQL Server Express 是在您安裝次要站台之前安裝，則 Configuration Manager 不會解除安裝 SQL Server Express。  

-   **刪除次要站台**：如果發生下列其中一種情況，請使用此選項：  

    -   次要網站安裝失敗。  

    -   次要站台解除安裝後，還是會繼續顯示在 Configuration Manager 主控台中。  

    此選項會從 Configuration Manager 階層中刪除站台的所有資訊及其資源，但會保留安裝在次要站台伺服器上的 Configuration Manager。  

    > [!NOTE]  
    >  您也可以使用階層維護工具和 **/DELSITE** 選項刪除次要站台。 如需詳細資訊，請參閱 [System Center Configuration Manager 的階層維護工具 (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)。  

#### <a name="to-uninstall-or-delete-a-secondary-site"></a>若要解除安裝或刪除次要網站  

1.  確認執行安裝程式的系統管理使用者具有下列安全性權限：  

    -   次要網站電腦上的系統管理權限。  

    -   主要網站的遠端網站資料庫伺服器上的本機系統管理員權限 (若位於遠端)。  

    -   父主要網站上的基礎結構系統管理員或系統高權限管理員安全性角色。  

    -   次要網站的網站資料庫上的 Sysadmin 權限。  

2.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

3.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [網站] 。  

4.  選取要移除的次要網站伺服器。  

5.  在 [首頁]  索引標籤的 [網站]  群組中，按一下 [刪除] 。  

6.  在 [一般]  頁面上，選取要解除安裝或刪除次要網站，然後按 [下一步] 。  

7.  在 [摘要]  頁面上確認設定，然後按 [下一步] 。  

8.  在 [完成]  頁面上，按一下 [關閉]  結束精靈。  

##  <a name="a-namebkmkuninstallprimarya-uninstall-a-primary-site"></a><a name="BKMK_UninstallPrimary"></a> 解除安裝主要站台  
您可以執行 Configuration Manager 安裝程式以解除安裝沒有相關聯次要站台的主要站台。 在您解除安裝主要網站之前，請考慮下列事項：  

-   如果 Configuration Manager 用戶端位於站台上所設定界限內，且主要站台是 Configuration Manager 階層的一部分，請考慮先將界限新增至階層中不同的主要站台，再解除安裝主要站台。  

-   當主要網站已無法使用時，您必須使用管理中心網站上的階層維護工具從網站資料庫中刪除主要網站。 如需詳細資訊，請參閱 [System Center Configuration Manager 的階層維護工具 (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)。  

利用下列程序解除安裝主要網站。  

#### <a name="to-uninstall-a-primary-site"></a>若要解除安裝主要網站  

1.  確認執行安裝程式的系統管理使用者具有下列安全性權限：  

    -   管理中心網站伺服器上的本機系統管理員權限。  

    -   管理中心網站的遠端網站資料庫伺服器上的本機系統管理員權限 (若位於遠端)。  

    -   管理中心網站之網站資料庫上的 Sysadmin 權限。  

    -   主要站台電腦上的本機系統管理員權限。  

    -   主要網站的遠端網站資料庫伺服器上的本機系統管理員權限 (若位於遠端)。  

    -   與管理中心網站上的基礎結構系統管理員或系統高權限管理員安全性角色相關聯的使用者名稱。  

2.  使用下列其中一種方法啟動主要站台伺服器上的 Configuration Manager 安裝程式：  

    -   在 [開始] 上按一下 [Configuration Manager 安裝程式] 。  

    -   從 &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64 開啟 Setup.exe。  

    -   從 &lt;*ConfigMgrInstallationPath*>\BIN\X64 開啟 Setup.exe。  

3.  在 [ **開始之前** ] 頁面上，按 [ **下一步**]。  

4.  在 [開始使用]  頁面上，選取 [解除安裝 Configuration Manager 網站] ，然後按 [下一步] 。  

5.  在 [解除安裝 Configuration Manager 站台] 上，指定是否從主要站台伺服器移除站台資料庫，以及是否移除 Configuration Manager 主控台。 根據預設，安裝程式會移除這兩個項目。  

    > [!IMPORTANT]  
    >  次要網站連結至主要網站時，您必須先移除次要網站才可解除安裝主要網站。  

6.  按一下 [是] 以確認解除安裝 Configuration Manager 主要站台。  

##  <a name="a-namebkmkuninstallprimarydistviewsa-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a><a name="BKMK_UninstallPrimaryDistViews"></a> 解除安裝以分散式檢視設定的主要站台  
 如果子主要網站以分散式檢視來設定管理中心網站的複寫連結，您必須先停用階層上的分散式檢視才能解除安裝該網站。 請使用下列資訊在解除安裝主要網站前先停用分散式檢視。  

#### <a name="to-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a>解除安裝以分散式檢視設定的主要網站  

1.  解除安裝任何主要網站之前，您必須停用管理中心網站與主要網站之間的每個階層中連結上的分散式檢視。  

2.  停用每個連結上的分散式檢視之後，確認來自主要網站的資料已完成中央管理網站的重新初始化。 在 Configuration Manager 主控台之 [監視] 工作區的 [資料庫複寫] 節點中檢視連結時，可以監視資料的初始化。  

3.  在透過管理中心網站將資料重新初始化之後，您就可以解除安裝主要網站。 若要解除安裝主要網站，請參閱本主題中的 [解除安裝主要站台](#BKMK_UninstallPrimary) 一節。  

4.  解除安裝主要網站之後，您可以重新設定主要網站連結的分散式檢視。  

    > [!IMPORTANT]  
    >  如果您在停用每個網站的分散式檢視或是來自主要網站的資料成功地在管理中心網站重新初始之前就解除安裝主要網站，主要網站與管理中心網站間的資料複寫可能會失敗。 在此案例中，您必須停用階層中每個連結的分散式檢視，然後，在透過管理中心網站重新初始化資料之後，您就可以重新設定分散式檢視。  

##  <a name="a-namebkmkuninstallcasa-uninstall-the-central-administration-site"></a><a name="BKMK_UninstallCAS"></a> 解除安裝管理中心網站  
 您可以執行 Configuration Manager 安裝程式以解除安裝沒有子主要站台的管理中心網站。 利用下列程序解除安裝管理中心網站。  

#### <a name="to-uninstall-a-central-administration-site"></a>解除安裝管理中心網站  

1.  確認執行安裝程式的系統管理使用者具有以下安全性權限：  

    -   管理中心網站伺服器上的本機系統管理員權限。  

    -   當網站資料庫伺服器未安裝在網站伺服器上時，管理中心網站上網站資料庫伺服器的本機系統管理員權限。  

2.  使用下列其中一個方法啟動管理中心網站上的 Configuration Manager 安裝程式：  

    -   在 [開始] 上按一下 [Configuration Manager 安裝程式] 。  

    -   從 &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64 開啟 Setup.exe。  

    -   從 &lt;*ConfigMgrInstallationPath*>\BIN\X64 開啟 Setup.exe。  

3.  在 [ **開始之前** ] 頁面上，按 [ **下一步**]。  

4.  在 [開始使用]  頁面上，選取 [解除安裝 Configuration Manager 網站] ，然後按 [下一步] 。  

5.  在 [解除安裝 Configuration Manager 站台] 上，指定是否從管理中心網站伺服器移除站台資料庫，以及是否移除 Configuration Manager 主控台。 根據預設，安裝程式會移除這兩個項目。  

    > [!IMPORTANT]  
    >  主要網站連結至管理中心網站時，您必須解除安裝主要網站才可解除安裝管理中心網站。  

6.  按一下 [是] 以確認解除安裝 Configuration Manager 管理中心網站。  



<!--HONumber=Dec16_HO3-->


