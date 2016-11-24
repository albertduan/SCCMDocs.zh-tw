---
title: "Proxy 伺服器支援 | System Center Configuration Manager"
description: "了解 System Center Configuration Manager 針對站台系統伺服器和用戶端所使用之 Proxy 伺服器的支援。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d20c734ba8050037cdf4ae290f72723f34781518


---
# <a name="proxy-server-support-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Proxy 伺服器支援

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 站台系統伺服器和用戶端都可以使用 Proxy 伺服器。  

## <a name="site-system-servers"></a>站台系統伺服器  
站台系統角色需要連線到網際網路時，您可以設定它們使用 Proxy 伺服器。  

-   裝載站台系統伺服器的電腦支援單一 Proxy 伺服器設定，且該電腦上所有站台系統角色皆共用這項設定。 如果不同的角色或角色執行個體需要個別的 Proxy 伺服器，則必須將這些角色放在不同的站台系統伺服器上。  

-   當您為已有 Proxy 伺服器組態的站台系統伺服器設定新的 Proxy 伺服器設定時，將會覆寫原始組態。  

-   若要與 Proxy 連線，需使用裝載站台系統角色之電腦的 **系統** 帳戶。  

下列站台系統角色會連線到網際網路，而且可能需要 Proxy 伺服器。  但有一個例外狀況，可使用 Proxy 的站台系統角色這樣做時不需要額外組態。 例外狀況是軟體更新點。 下列清單包含軟體更新點所需的額外設定相關資訊：  

**Asset Intelligence 同步處理點** - 此站台系統角色會連線到 Microsoft，並在裝載 Asset Intelligence 同步處理點的電腦上使用 Proxy 伺服器設定。  

**雲端式發佈點** - 若要為雲端式發佈點設定 Proxy 伺服器，請在管理雲端式發佈點的主要站台上設定 Proxy。  

針對這個組態，主要站台伺服器：  

-   必須能夠連線到 Microsoft Azure，才能佈建、監視及發佈內容到發佈點。  

-   使用電腦 System 帳戶來進行連線。  

-   使用該電腦的預設網頁瀏覽器。  

您無法在 Microsoft Azure 的雲端發佈點上設定 Proxy 伺服器。  

**雲端連接點** - 此站台系統角色會連線到 Configuration Manager 雲端服務以下載 Configuration Manager 的版本更新，並使用裝載服務連接點之電腦上設定的 Proxy 伺服器。  

**Exchange Server 連接器** - 此站台系統角色會連線到 Exchange Server，並使用裝載 Exchange Server 連接器之電腦上的 Proxy 伺服器設定。  

**服務連接點** - 此站台系統角色會連線到 Microsoft Intune，並使用裝載服務連接點之電腦上的 Proxy 伺服器設定。  

**軟體更新點** - 此站台系統角色可在連線到 Microsoft Update 以下載修補程式，並同步處理有關更新的資訊時，使用 Proxy。   
軟體更新點只會針對下列兩個選項使用 Proxy (如果您在設定軟體更新點時啟用該選項的話)：  

-   **同步處理軟體更新時使用 Proxy 伺服器**  

-   **在使用自動部署規則下載內容時使用 Proxy 伺服器** (可供使用時，這項設定不是供次要站台上的軟體更新點使用)  

在 [新增站台系統角色精靈] 的 [主動式軟體更新點] 頁面上，或 [軟體更新點元件內容] 的 [一般] 索引標籤上，設定 Proxy 伺服器設定。  

-   Proxy 伺服器設定只會和站台上的軟體更新點建立關聯。  

-   只有已針對裝載軟體更新點的站台系統伺服器設定 Proxy 伺服器時，才能使用 Proxy 伺服器選項。  

> [!NOTE]  
>  預設會使用已建立自動部署規則之伺服器的**系統**帳戶來連線到網際網路，並在執行自動部署規則時下載軟體更新。  
>   
>  當此帳戶無法存取網際網路時，將無法下載軟體更新，並會在 ruleengine.log 中記錄下列項目：**無法從網際網路下載更新。錯誤 = 12007。**  

#### <a name="to-configure-the-proxy-server-for-a-site-system-server"></a>設定站台系統伺服器的 Proxy 伺服器  

1.  在 Configuration Manager 主控台中，展開 [站台組態]，然後按一下 [伺服器和站台系統角色]。  

2.  選取要編輯的站台系統，然後在詳細資料窗格中，以滑鼠右鍵按一下 [站台系統]，然後按一下 [內容]。  

3.  在 [站台系統內容] 中，選取 [Proxy] 索引標籤，然後為這個主要站台伺服器設定 Proxy 設定值。  

4.  按一下 [確定] 儲存新的 Proxy 伺服器組態。  



<!--HONumber=Nov16_HO1-->


