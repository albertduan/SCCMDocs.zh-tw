---
title: "建議的硬體 | System Center Configuration Manager"
description: "了解硬體建議，以協助您在基本部署之外調整 System Center Configuration Manager 環境的規模。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
caps.latest.revision: 26
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d5aa39a9551cc872631895bb1664de5a35531854


---
# <a name="recommended-hardware-for-system-center-configuration-manager"></a>System Center Configuration Manager 的建議硬體

適用於：System Center Configuration Manager (最新分支)

下列建議方針可協助您調整 System Center Configuration Manager 環境，以支援較複雜的站台、站台系統與用戶端部署。 這些建議不完全適用於所有站台與階層設定。  

 請在下列章節中使用這項資訊作為方針，以協助您規劃可滿足用戶端和站台 (使用可用的 Configuration Manager 功能與預設設定) 處理負載的硬體。  


##  <a name="a-namebkmkscalesiesystemsa-site-systems"></a><a name="bkmk_ScaleSieSystems"></a> 站台系統  
 本節說明針對 Configuration Manager 站台系統建議的硬體設定，以用於支援最多用戶端數並使用大多數或所有 Configuration Manager 功能的部署。 支援少於最多用戶端數的部署，和不會使用所有可用功能的部署，可能需要較少的電腦資源。 一般來說，限制整體系統效能的主要因素依序如下所示：  

1.  磁碟 I/O 效能  

2.  可用的記憶體  

3.  CPU  

最佳做法是針對所有資料磁碟和 1Gbps 的乙太網路使用 RAID 10 組態。  

###  <a name="a-namebkmkscalesiteservera-site-servers"></a><a name="bkmk_ScaleSiteServer"></a> 站台伺服器  

|獨立主要網站|CPU 核心|記憶體 GB|SQL Server 的記憶體 % 配置|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|獨立主要站台伺服器，並在相同伺服器上具有資料庫站台角色<sup>1</sup>|16|96|80|  
|獨立主要站台伺服器，並具有遠端站台資料庫|8|16|-|  
|獨立主要站台的遠端資料庫伺服器|16|64|90|  
|管理中心網站伺服器，並在相同伺服器上具有資料庫站台角色<sup>1</sup>|16|96|80|  
|管理中心網站伺服器，並具有遠端站台資料庫|8|16|-|  
|管理中心網站的遠端資料庫伺服器|16|96|90|  
|子主要站台，並在相同伺服器上具有資料庫站台角色|16|96|80|  
|子主要站台伺服器，並具有遠端站台資料庫|8|16|-|  
|子主要站台的遠端資料庫伺服器|16|64|90|  
|次要網站伺服器|8|16|-|  

 <sup>1</sup> 站台伺服器和 SQL Server 安裝在相同電腦上時，此部署可支援最大[規模數目](/sccm/core/plan-design/configs/size-and-scale-numbers)的站台和用戶端。 不過，這項設定可能限制 [System Center Configuration Manager 的高可用性選項](/sccm/protect/understand/high-availability-options)，例如使用 SQL Server 叢集。  此外，因為在同一部電腦上執行時，支援 SQL Server 和 Configuration Manager 站台伺服器需要較高的 I/O 需求，所以具有較大型部署的客戶應考慮使用具有遠端 SQL Server 電腦的設定。  

###  <a name="a-namebkmkremotesitesystema-remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a> 遠端站台系統伺服器  
 下列方針適用於身為單一站台系統角色的電腦。 規劃當您在同一部電腦上安裝多個站台系統角色時進行調整。  

|網站系統角色|CPU 核心|記憶體 GB|磁碟空間：GB|  
|----------------------|---------------|---------------|--------------------|  
|管理點|4|8|50|  
|發佈點|2|8|如作業系統和儲存您部署之內容所需|  
|應用程式類別目錄，以及網站系統電腦上的 Web 服務與網站|4|16|50|  
|軟體更新點<sup>1</sup>|8|16|如作業系統和儲存您部署之更新所需|  
|所有其他的網站系統角色|4|8|50|  

 <sup>1</sup> 裝載軟體更新點的電腦，針對 IIS 應用程式集區需要下列設定：  

-   將 **WsusPool 佇列長度** 增加至 **2000**  

-   增加 **WsusPool 私用記憶體限制** 為 4 倍，或設為 **0** (無限制)  

###  <a name="a-namebkmkdiskspacea-disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a> 站台系統的磁碟空間  
 磁碟配置和設定可決定 Configuration Manager 的效能。 由於每個 Configuration Manager 環境各有不同，因此您實作的值可能與下列方針不盡相同。  

 為發揮最佳效能，請將每個物件分別置於獨立的專用 RAID 磁碟區中。 針對所有資料磁碟區 (Configuration Manager 及其資料庫檔案)，使用 RAID 10 可以發揮最佳效能。  

|資料使用量|磁碟空間下限|25,000 個用戶端|50,000 個用戶端|100,000 個用戶端|150,000 個用戶端|700,000 個用戶端 (管理中心網站)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|作業系統|請參閱作業系統的指引。|請參閱作業系統的指引。|請參閱作業系統的指引。|請參閱作業系統的指引。|請參閱作業系統的指引。|請參閱作業系統的指引。|  
|Configuration Manager 應用程式和記錄檔|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|網站資料庫 .mdf 檔|每 25,000 個用戶端需要 75 GB|75 GB|150 GB|300 GB|500 GB|2 TB|  
|網站資料庫 .ldf 檔|每 25,000 個用戶端需要 25 GB|25 GB|50 GB|100 GB|150 GB|100 GB|  
|暫存資料庫檔案 (.mdf 和.ldf)|視需要|視需要|視需要|視需要|視需要|視需要|  
|內容 (發佈點共用)|視需要<sup>1</sup>|視需要<sup>1</sup>|視需要<sup>1</sup>|視需要<sup>1</sup>|視需要<sup>1</sup>|視需要<sup>1</sup>|  

 <sup>1</sup> 磁碟空間指引中並不包括網站伺服器或發佈點上的內容庫中所需的空間。 如需規劃內容庫的資訊，請參閱 [The content library](../../../core/plan-design/hierarchy/the-content-library.md) (內容庫)。  

 除了前述方針外，規劃磁碟空間需求時亦請考量下列方針：  

-   每個用戶端需要大約 5 MB 的空間。  

-   規劃主要網站暫存資料庫的合併大小時，請以站台資料庫 .mdf 檔的 25% 到 30% 為準。 實際大小可能更小或更大，而且會因網站伺服器的效能及短期或長期內送資料的資料量而有所不同。  

    > [!NOTE]  
    >  當您在站台有 50,000 個以上的用戶端時，請計劃使用 4 個以上的暫存資料庫 .mdf 檔案。  

-   管理中心網站的暫存資料庫大小通常比主要網站的暫存資料庫小。  

-   次要網站資料庫的大小有以下限制：  

    -   SQL Server 2012 Express：10 GB  

    -   SQL Server 2014 Express：10 GB  

##  <a name="a-namebkmkscaleclienta-clients"></a><a name="bkmk_ScaleClient"></a> 用戶端  
 本節說明藉由安裝 Configuration Manager 用戶端軟體所管理之電腦的建議硬體設定。  

### <a name="client-for-windows-computers"></a>Windows 電腦的用戶端  
 以下是您使用 Configuration Manager 管理之 Windows 電腦的最低需求，包括內嵌作業系統：  

-   **處理器和記憶體：** 請參考電腦作業系統的處理器和 RAM 需求。  

-   **磁碟空間：**500 MB 可用磁碟空間，建議使用 5GB 作為 Configuration Manager 用戶端快取。 如果您使用自訂的設定來安裝 Configuration Manager 用戶端，則需要較少的磁碟空間：  

    -   使用 CCMSetup 命令列屬性 /skipprereq 避免安裝用戶端不需要的檔案。 例如，如果用戶端不會使用應用程式類別目錄，即為 **CCMSetup.exe /skipprereq:silverlight.exe** 。  

    -   您可以使用 Client.msi 屬性 SMSCACHESIZE 來設定小於預設值 5120 MB 的快取檔案。 大小下限為 1 MB。 例如， **CCMSetup.exe SMSCachesize=2** 會建立大小為 2 MB 的快取。  

    如需這些用戶端安裝設定的詳細資訊，請參閱 [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (關於 System Center Configuration Manager 中的用戶端安裝內容)。  

    > [!TIP]  
    >  使用最少的磁碟空間安裝用戶端適用於 Windows Embedded 裝置，它們通常磁碟大小比標準的 Windows 電腦小。  

 以下是針對 Configuration Manager 中選用功能的額外最低硬體需求。  

-   **作業系統部署：** 384 MB 的 RAM  

-   **軟體中心：** 500 MHz 處理器  

-   **遠端控制：** Pentium 4 Hyper-Threaded 3GHz (單核心) 或同級 CPU，搭配至少 1 GB RAM 以獲得最佳體驗  

### <a name="client-for-linux-and-unix"></a>Linux 和 UNIX 的用戶端  
 下表列出您使用 Configuration Manager 管理之 Windows 電腦的最低需求：  

|需求|詳細資料|  
|-----------------|-------------|  
|處理器與記憶體|請參考電腦作業系統的處理器和 RAM 需求。|  
|磁碟空間|500 MB 可用磁碟空間，建議使用 5GB 作為 Configuration Manager 用戶端快取。|  
|網路連線|Configuration Manager 用戶端電腦必須具有 Configuration Manager 站台系統的網路連線能力，才能啟用管理功能。|  

##  <a name="a-namebkmkscaleconsolea-configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a> Configuration Manager 主控台  
 下表中的需求適用於執行 Configuration Manager 主控台的每一部電腦。  

 **最低硬體設定：**  

-   Intel i3 或同級 CPU  

-   2 GB 的 RAM  

-   2 GB 的硬碟空間  

|DPI 設定|最低解析度|  
|-----------------|------------------------|  
|96 / 100%|1024 x 768|  
|120 /125%|1280 x 960|  
|144 / 150%|1600 x 1200|  
|196 / 200%|2500x1600|  

 **PowerShell 支援：**  

 當您在執行 Configuration Manager 主控台的電腦上安裝 PowerShell 支援時，可以在該電腦上執行 PowerShell Cmdlet 來管理 Configuration Manager。 支援下列最低版本：  

-   PowerShell 3.0  

-   PowerShell 4.0  

除了 PowerShell 之外，也支援 Windows Management Framework (WMF) 3.0 和 4.0。   
您可以在安裝 Configuration Manager 主控台之前或之後，安裝 PowerShell。  

##  <a name="a-namebkmkscalelaba-lab-deployments"></a><a name="bkmk_ScaleLab"></a> 實驗室部署  
 針對 Configuration Manager 實驗室和測試部署，請使用下列最低硬體建議。 這些建議適用於所有的站台類型，以及用於最多 100 個用戶端：  

|角色|CPU 核心|記憶體 (GB)|磁碟空間 (GB)|  
|----------|---------------|-------------------|-----------------------|  
|站台和資料庫伺服器|2 - 4|7 - 12|100|  
|網站系統伺服器|1 - 4|2 - 4|50|  
|用戶端|1 - 2|1 - 3|30|  



<!--HONumber=Nov16_HO1-->


