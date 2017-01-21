---
title: "升級內部部署基礎結構 | System Center Configuration Manager"
description: "了解如何升級基礎結構 (例如 SQL Server 和站台系統的站台作業系統)。"
ms.custom: na
ms.date: 10/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c8115fba0722fc902e60ce201d8a9914036c1245
ms.openlocfilehash: 1239bf81991bb233a9640606bb47f598a70d5e50


---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>升級支援 System Center Configuration Manager 的內部部署基礎結構

*適用於：System Center Configuration Manager (最新分支)*

使用下列資訊有助於升級可執行 System Center Configuration Manager 的基礎結構。  

##  <a name="a-namebkmksupconfigupgradesitesrva-upgrade-site-operating-system-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> 升級站台系統的站台作業系統  
 Configuration Manager 在下列案例中支援就地升級裝載站台伺服器的伺服器的作業系統，以及裝載任何站台系統角色的遠端伺服器的作業系統︰  

-   如果 Configuration Manager 仍然支援產生的 Windows Service Pack 層級，則會就地升級至更高版本的 Windows Server Service Pack。  
-   就地升級方向：
    - Windows Server 2012 R2 到 Windows Server 2016 ([請參閱其他詳細資料](#upgrade-windows-server-2012-r2-to-2016))
    - Windows Server 2012 到 Windows Server 2012 R2 ([請參閱其他詳細資料](#upgrade-windows-server-2012-to-windows-server-2012-r2))
    - 當您使用 Configuration Manager 1602 版或更新版本時，也支援將 Windows Server 2008 R2 升級至 Windows Server 2012 R2 ([請參閱其他詳細資料](#upgrade-windows-server-2008-r2-to-windows-server-2012-r2))

    > [!WARNING]  
    >  在升級到 Windows Server 2012 R2 之前，您必須從伺服器 **解除安裝 WSUS 3.2** 。  
    >   
    >  如需此重要步驟的資訊，請參閱 Windows Server 文件中 [Windows Server Update Services 概觀](https://technet.microsoft.com/library/hh852345.aspx) 的＜新功能和變更的功能＞一節。  

若要升級伺服器，請使用您要升級的目標作業系統所提供的升級程序。  請參閱下列項目：
  -  Windows Server 文件中的 [Windows Server 2012 R2 的升級選項](https://technet.microsoft.com/library/dn303416.aspx)。  
  - Windows Server 文件中的 [Windows Server 2016 的升級和轉換選項](https://technet.microsoft.com/windows-server-docs/get-started/supported-upgrade-paths)。

### <a name="upgrade-windows-server-2012-r2-to-2016"></a>將 Windows Server 2012 R2 升級到 2016  
此作業系統升級案例的條件如下：

**升級之前：**  
-   移除 System Center Endpoint Protection (SCEP) 用戶端。 Windows Server 2016 內建 Windows Defender，其取代 SCEP 用戶端。 SCEP 用戶端的存在與否可以防止升級至 Windows Server 2016。

**升級之後：**
-   確定 Windows Defender 已啟用、設為自動啟動，並且執行中。
-   確定下列 Configuration Manager 服務正在執行︰
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   確定已啟用 [Windows 處理程序啟動] 和 **WWW/W3svc** 服務、設定為自動啟動，並執行下列站台系統角色 (在升級期間，會停用這些服務)：
  -     網站伺服器
  -     管理點
  -     應用程式類別目錄 Web 服務點
  -     應用程式類別目錄網站點


-   請確定每部裝載站台系統角色的伺服器仍然符合在該伺服器上執行的所有[站台系統角色必要條件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。 例如，您可能需要重新安裝 BITS、WSUS，或設定 IIS 的特定設定。

  還原任何遺失必要條件之後，請再重新啟動伺服器一次，確保服務已啟動並操作。

**遠端 Configuration Manager 主控台的已知問題：**  
在您將站台伺服器或裝載 SMS_Provider 執行個體的伺服器升級至 Windows Server 2016 之後，系統管理使用者可能無法將 Configuration Manager 主控台連線至站台。 若要解決這個問題，您必須手動還原 WMI 中 SMS Admins 群組的權限。 必須設定站台伺服器以及每部裝載 SMS 提供者執行個體之遠端伺服器的權限︰

1. 在適用的伺服器上，開啟 Microsoft Management Console (MMC)，並新增 [WMI 控制] 的嵌入式管理單元，然後選取 [本機電腦]。
2. 在 MMC 中，開啟 [WMI 控制 (本機)] 的 [內容]，然後選取 [安全性] 索引標籤。
3. 展開 [根目錄] 下方的樹狀結構，並選取 [SMS] 節點，然後按一下 [安全性]。  確定 **SMS Admins** 群組具有下列權限︰
  -     啟用帳戶
  -     遠端啟用
4. 接下來，在 [安全性] 索引標籤上，於 SMS 節點下選取 **site_<sitecode>** 節點，然後按一下 [安全性]。 確定 **SMS Admins** 群組具有下列權限︰
  -   執行方法
  -   提供者寫入
  -   啟用帳戶
  -   遠端啟用
5. 儲存還原 Configuration Manager 主控台存取權的權限。

### <a name="windows-server-2012-to-windows-server-2012-r2"></a>Windows Server 2012 到 Windows Server 2012 R2

**升級之前：**
-  與其他支援的案例不同，在升級之前，這種情況不需要額外的考量。

**升級之後：**
  - 確定 Windows 部署服務已啟動並執行下列站台系統角色 (在升級期間，會停止這個服務)︰
    - 網站伺服器
    - 管理點
    - 應用程式類別目錄 Web 服務點
    - 應用程式類別目錄網站點


  -     確定已啟用 [Windows 處理程序啟動] 和 **WWW/W3svc** 服務、設定為自動啟動，並執行下列站台系統角色 (在升級期間，會停用這些服務)：
    -   網站伺服器
    -   管理點
    -   應用程式類別目錄 Web 服務點
    -   應用程式類別目錄網站點


  -     請確定每部裝載站台系統角色的伺服器仍然符合在該伺服器上執行的所有[站台系統角色必要條件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。 例如，您可能需要重新安裝 BITS、WSUS，或設定 IIS 的特定設定。

  還原任何遺失必要條件之後，請再重新啟動伺服器一次，確保服務已啟動並操作。

### <a name="upgrade-windows-server-2008-r2-to-windows-server-2012-r2"></a>將 Windows Server 2008 R2 升級到 Windows Server 2012 R2
此作業系統升級案例的條件如下：  

**升級之前：**
-   解除安裝 WSUS 3.2。  
    將伺服器作業系統升級到 Windows Server 2012 R2 之前，您必須從伺服器解除安裝 WSUS 3.2。 如需此重要步驟的相關資訊，請參閱 Windows Server 文件中＜Windows Server Update Services 概觀＞的＜新功能和變更的功能＞一節。

**升級之後：**
  - 確定 Windows 部署服務已啟動並執行下列站台系統角色 (在升級期間，會停止這個服務)︰
    - 網站伺服器
    - 管理點
    - 應用程式類別目錄 Web 服務點
    - 應用程式類別目錄網站點


  -     確定已啟用 [Windows 處理程序啟動] 和 **WWW/W3svc** 服務、設定為自動啟動，並執行下列站台系統角色 (在升級期間，會停用這些服務)：
    -   網站伺服器
    -   管理點
    -   應用程式類別目錄 Web 服務點
    -   應用程式類別目錄網站點


  -     請確定每部裝載站台系統角色的伺服器仍然符合在該伺服器上執行的所有[站台系統角色必要條件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。 例如，您可能需要重新安裝 BITS、WSUS，或設定 IIS 的特定設定。

  還原任何遺失必要條件之後，請再重新啟動伺服器一次，確保服務已啟動並操作。


### <a name="unsupported-upgrade-scenarios"></a>不支援的升級案例
下列是一般會問及的 Windows Server 升級案例，但不受 Configuration Manager 支援：  

-   Windows Server 2008 到 Windows Server 2012 或更新版本  
-   Windows Server 2008 R2 到 Windows Server 2012



##  <a name="a-namebkmksupconfigupgradeclienta-upgrade-the-operating-system-of-configuration-manager-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> 升級 Configuration Manager 用戶端的作業系統  
 在下列情況下，Configuration Manager 支援 Configuration Manager 用戶端的作業系統就地升級：  

-   如果 Configuration Manager 仍然支援產生的 Service Pack 層級，則會就地升級至更高版本的 Windows Service Pack。  

-   將 Windows 從支援的版本就地升級到 Windows 10。 如需詳細資訊，請參閱[使用 System Center Configuration Manager 將 Windows 升級至最新版本](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)。  

-   Windows 10 的組建至組建維護升級。  如需詳細資訊，請參閱[使用 System Center Configuration Manager 管理 Windows 即服務](../../../osd/deploy-use/manage-windows-as-a-service.md)。  

##  <a name="a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> 在站台資料庫伺服器升級 SQL Server  
  Configuration Manager 支援從站台資料庫伺服器上的支援 SQL 版本進行 SQL Server 就地升級。 下列是 Configuration Manager 所支援 SQL Server 升級案例的詳細資料，以及每個案例的需求。

 如需 Configuration Manager 所支援 SQL Server 版本的相關資訊，請參閱 [System Center Configuration Manager 的 SQL Server 版本支援](../../../core/plan-design/configs/support-for-sql-server-versions.md)。  

 **升級 SQL Server 的 Service Pack 版本：**    
 如果 Configuration Manager 仍然支援產生的 SQL Server Service Pack 層級，Configuration Manager 就會支援將 SQL Server 就地升級至更高版本的 Service Pack。

 當您的階層中有多個 Configuration Manager 站台時，每個站台都可以執行不同的 SQL Server Service Pack 版本，而且站台升級 SQL Server 用於站台資料庫的 Service Pack 版本的順序沒有限制。

 **升級到新版 SQL Server：**   
 Configuration Manager 支援將 SQL Server 就地升級至下列版本：

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

當您升級裝載站台資料庫的 SQL Server 版本時，必須以下列順序升級在站台使用的 SQL Server 版本：

 1. 先升級管理中心網站的 SQL Server。
 2. 先升級次要站台，再升級次要站台的父主要站台。
 3. 最後升級父主要站台。 這包括向管理中心網站以及為階層之頂層站台的獨立主要站台報告的二個子主要站台。



**如需 SQL Server 的詳細資訊，請參閱 TechNet 上的 SQL Server 文件：**  
-   [升級到 SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  
-   [升級到 SQL Server 2012](http://technet.microsoft.com/library/ms143393\(v=sql.110))
-   [升級到 SQL Server 2016](https://technet.microsoft.com/library/bb677622(v=sql.130))



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>在站台資料庫伺服器升級 SQL Server  

1.  停止站台上的所有 Configuration Manager 服務。  
2.  將 SQL Server 升級為支援的版本。  
3.  重新啟動 Configuration Manager 服務。  

> [!NOTE]  
>  當您將管理中心網站使用的 SQL Server 版本，從 Standard Edition 變更成 Datacenter 或 Enterprise Edition 時，限制階層支援的用戶端數目的資料庫資料分割不會變更。



<!--HONumber=Nov16_HO1-->


