---
title: "服務連接點 | System Center Configuration Manager"
description: "了解此 Configuration Manager 站台系統角色，並了解及規劃其使用範圍。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: 18
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e30c3d4bbf42e008a3f570c843b2f63251bce158


---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>關於 System Center Configuration Manager 中的服務連線點

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 服務連接點是可提供階層中幾項重要功能的站台系統角色。 請先了解並規劃可能會影響這個站台系統角色設定方式的用途範圍，再設定服務連接點：  

-   **使用 Microsoft Intune 管理行動裝置** – 此角色會取代舊版 Configuration Manager 使用的 Windows Intune 連接器，而且可以使用您的 Intune 訂閱詳細資訊來設定。 請參閱[搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理 (MDM)](../../../../mdm/plan-design/hybrid-mobile-device-management.md)。  

-   **使用內部部署 MDM 管理行動裝置** – 針對您管理之未連接到網際網路的內部部署裝置，此角色提供支援。 請參閱[在 System Center Configuration Manager 中使用內部部署基礎結構管理行動裝置](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

-   **從您的 Configuration Manager 基礎結構上傳使用方式資料** – 您可以控制要上傳的詳細資料層級或數量。 上傳的資料可幫助我們：  

    -   主動識別及疑難排解問題  

    -   改善產品和服務  

    -   識別適用於您所使用之 Configuration Manager 版本的 Configuration Manager 更新  

     請參閱 [Usage data levels and settings](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage)。  

-   **下載適用於您 Configuration Manager 基礎結構的更新** – 系統會根據您上傳的使用方式資料，僅提供與您基礎結構相關的更新。  

 **每個階層支援此角色的單一執行個體：**  

-   站台系統角色只能安裝在您的階層 (管理中心網站或獨立主要站台) 的最上層站台。  

-   如果您擴充獨立主要站台到較大的階層時，您必須從主要站台解除安裝此角色，然後在管理中心網站安裝此角色。  

##  <a name="a-namebkmkmodesa-modes-of-operation"></a><a name="bkmk_modes"></a> 作業模式  
 服務連接點支援兩種作業模式：  

-   在 **線上模式**中，服務連線點每 24 小時會自動檢查更新，然後下載您目前基礎結構和產品版本適用的新增更新，讓它們可在 Configuration Manager 主控台中使用  

-   在**離線模式**中，服務連接點不會連線到 Microsoft 雲端服務，因此您必須手動[使用 System Center Configuration Manager 的服務連接工具](../../../../core/servers/manage/use-the-service-connection-tool.md)以匯入可用的更新。  

若您安裝服務連接點之後要在線上模式或離線模式之間切換，則必須先重新啟動 Configuration Manager SMS_Executive 服務的 SMS_DMP_DOWNLOADER 執行緒，這項變更才會生效。  若要這樣做，請使用 Configuration Manager Service Manager，僅重新啟動 SMS_Executive 服務的 SMS_DMP_DOWNLOADER 執行緒。  您也可以重新啟動 Configuration Manager 的 SMS_Executive 服務 (這樣會重新啟動大部分的站台元件)，或者等候站台備份這類排程工作發生，其會停止 SMS_Executive 並於稍後重新啟動。  

若要使用 Configuration Manager Service Manager，可在主控台中瀏覽至 [監視] > [系統狀態] > [元件狀態]，按一下 [啟動]，然後選取 [Configuration Manager Service Manager]。  在 Service Manager 中：  

-   在瀏覽窗格中，依序展開站台和 **[元件]**，然後選取要重新啟動的元件。  

-   在詳細資料窗格中，以滑鼠右鍵按一下元件，然後選取 **[查詢]**。  

-   確認元件狀態之後，再次以滑鼠右鍵按一下元件，並選取 **[停止]**。  

-   再次選取元件的**[查詢]** 確認它已停止，以滑鼠右鍵再按一下元件，然後選取 **[啟動]**。  

> [!IMPORTANT]  
>  當您將 Microsoft Intune 訂閱新增至服務連接點時，它會自動將站台系統角色設定為線上。 使用 Intune 訂閱進行設定時，服務連接點不支援離線模式。  

**當角色安裝在相對於站台伺服器為遠端的電腦上：**  

-   您必須使用站台系統安裝帳戶設定裝載角色的站台系統伺服器  

-   站台系統安裝帳戶可供站台伺服器上的發佈管理員使用，用於傳送來自服務連接點的更新。  

##  <a name="a-namebkmkurlsa-internet-access-requirements"></a><a name="bkmk_urls"></a> 網際網路存取需求  
若要啟用作業，裝載服務連線點的電腦以及該電腦與網際網路之間的任何防火牆，皆必須透過 **連接埠 TCP 443** 傳遞通訊給下列網際網路位置。 服務連接點也支援使用 Web Proxy (不論有無驗證) 來存取這些位置。  

**更新及服務**  

-   *.akamaiedge.net  

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *manage.microsoft.com  
-   https://bspmts.mp.microsoft.com/V
-   https://login.microsoftonline.com/{TenantID}


**Windows 10 服務**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  



<!--HONumber=Nov16_HO1-->


