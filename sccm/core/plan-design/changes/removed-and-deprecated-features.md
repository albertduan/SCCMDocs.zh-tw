---
title: "已淘汰的功能 | Microsoft Docs"
description: "了解 System Center Configuration Manager 不再支援的功能、產品和作業系統。"
ms.custom: na
ms.date: 06/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 0ec241d07f51b80b84d65676ef1207b31a9a9983
ms.openlocfilehash: e23acf743d8f73afd213c44c3728d1b66d7e558f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/28/2017


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>System Center Configuration Manager 的已移除和已淘汰功能

*適用於︰System Center Configuration Manager (最新分支)*

本主題說明已從 System Center Configuration Manager 取消支援的功能、產品與作業系統，或在後續更新中將會移除 (已淘汰) 的功能、產品與作業系統。 這會讓您提早注意可能影響您使用 Configuration Manager 的未來變更。  

這項資訊有可能隨著後續版本而有所變更，且可能不會包含每項已淘汰的功能、產品或作業系統。  

## <a name="how-to-use-this-information"></a>如何使用此資訊  
若已先將某個功能或作業系統列為已淘汰，則對於將它與 Configuration Manager 搭配使用的支援，就會納入要從未來版本的 Configuration Manager 中移除的排程。 我們提供此資訊以協助您規劃使用該功能或作業系統的替代方案。 在發行移除此支援的 Configuration Manager 第一個版本時，本主題隨之更新以指出該特定版本。  

移除對某個功能或作業系統的支援時，只要該版本的 Configuration Manager 仍受到支援，該功能或作業系統仍會在您使用舊版 Configuration Manager 時受到支援。 不過，當您使用在指定或版本日期之後發行的 Configuration Manager 版本時，該版本的 Configuration Manager 就不提供支援。

例如，如果某個功能已排程為要透過 2016 年 9 月後發行的第一個更新來移除其支援，對該功能的支援將不再隨附於更新 1610 (於 2016 年 10 月發行) 中。
-  透過更新 1610，就不再支援該功能。
-  本主題隨即更新，指出 1610 版已移除支援。
不過，如果您繼續使用支援該功能的較早版本 (例如，版本 1602 或 1606)，您就能繼續使用該功能，直到您使用的版本不再受到支援為止。

如需詳細資訊，請參閱：
 - [Microsoft 週期原則](https://support.microsoft.com/lifecycle)網站。
 - [System Center Configuration Manager 最新分支版本支援](/sccm/core/servers/manage/current-branch-versions-supported)。




## <a name="deprecated-operating-systems"></a>已淘汰的作業系統
### <a name="server-operating-systems"></a>伺服器作業系統  

|**作業系統**|**首次宣布的淘汰項目**|**移除的支援** |  
|-|-|-|  
|Windows Server 2008|2015 年 7 月 10 日|版本 1511 </br></br>已移除作為站台系統的支援。 (請參閱註 1)。|  
|Windows Server 2008 R2|2015 年 7 月 10 日| 版本 1702 (請參閱註 2)|  

-   註 1︰此作業系統不支援站台伺服器或站台系統角色，但發佈點和提取發佈點為例外。 您能持續將此作業系統作為發佈點使用，直到宣告此項支援已遭取代，或此作業系統的延伸支援期限過期。 如需詳細資訊，請參閱 [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (在 Windows Server 2008 上安裝 System Center Configuration Manager CB 和 LTSB 失敗)。

-   註 2：從版本 1702 開始，站台伺服器或大部分站台系統角色將不會支援此作業系統，不過 1702 之前的版本會繼續支援使用此作業系統。 此作業系統仍會持續支援發佈點站台系統角色 (包括提取發佈點，以及針對 PXE 和多點傳送)，直到宣佈此支援已被取代，或是此作業系統的延伸支援期限過期。 從 1602 版開始，您可以將站台伺服器的作業系統從 Windows Server 2008 R2 就地升級到 Windows Server 2012 R2。  

     如需站台伺服器作業系統之就地升級的詳細資訊，請參閱 [What's changed in System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) (System Center Configuration Manager 中的變更) 中的[就地升級執行 Windows Server 2008 R2 之站台伺服器的作業系統](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS)一節。



### <a name="client-operating-systems"></a>用戶端作業系統  

 除非另有說明，否則只要作業系統是受支援的 Configuration Manager 用戶端，則在作業系統的「延伸支援結束日期」之前，皆會受到支援。 如需延伸支援結束日期的詳細資訊，請參閱 [Microsoft 週期原則](https://support.microsoft.com/lifecycle)。 如果 Configuration Manager 支援的作業系統將在「延伸支援結束日期」之前結束，該作業系統的淘汰日期及支援移除日期將在此列出。  

|**作業系統**|**首次宣布的淘汰項目**|**移除的支援**|  
|-|-|-|  
|Windows XP|2015 年 7 月 10 日|版本 1511|  
|Windows XP Embedded|2015 年 7 月 10 日|版本 1702|  
|Windows Server 2003|2015 年 7 月 10 日|版本 1511|  
|Windows Server 2003 R2|2015 年 7 月 10 日|版本 1511|  
|Windows Vista|2015 年 7 月 10 日|版本 1511|  
|Mac OS X  10.6 - 10.8|2015 年 7 月 10 日|版本 1511|  
|Windows Mobile 6.0 - 6.5|2015 年 7 月 10 日|版本 1511|  
|Nokia Symbian Belle|2015 年 7 月 10 日|版本 1511|  
|Windows CE 5.0 - 6.0|2015 年 7 月 10 日|版本 1511|  


## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>已淘汰可作為站台資料庫之 SQL Server 版本的支援  

|**SQL Server 版本**|**首次宣布的淘汰項目**|**移除的支援**|   
|-|-|-|  
|SQL Server 2008|2015 年 7 月 10 日|版本 1511|  
|SQL Server 2008 R2|2015 年 7 月 10 日|版本 1702|  

如果您需要升級您的 SQL Server 版本，建議您使用下列方法 (依複雜度由低到高排列)。
1. [就地升級 SQL Server](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (建議選項)。
2. 在新的電腦上安裝新版本的 SQL Server，然後使用 Configuration Manager 安裝程式的[資料庫移動選項](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration)，將您的站台伺服器指向新的 SQL Server。
3. 使用[備份及復原](/sccm/protect/understand/backup-and-recovery)。


## <a name="deprecated-features"></a>已淘汰的功能  

|**功能**|**首次宣布的淘汰項目**|**移除的支援**|  
|-|-|-|  
|網路存取保護 (NAP) - 自 System Center 2012 Configuration Manager 起提供|2015 年 7 月 10 日|版本 1511|  
|頻外管理 - 自 System Center 2012 Configuration Manager 起提供|2015 年 10 月 16 日|版本 1511|
|工作順序： <br /> - OSDPreserveDriveLetter  <br /><br /> 在作業系統部署期間，Windows 安裝程式現在預設會決定要使用的最佳磁碟機代號 (通常是 C:)。 如果您想要指定使用不同的磁碟機，您可以在「套用作業系統」工作順序步驟中變更位置。 移至 [請選取要套用此作業系統的位置] 設定，選取 [特定邏輯磁碟機代號]，然後選擇您想要使用的磁碟機。 |2016 年 6 月 20日 |1606 版 |
|工作順序： <br /> - 將磁碟轉換成動態磁碟 <br /> - 安裝部署工具 |2016 年 11 月 18 日|對於這些工作順序的支援將結束於 2017 年 6 月 1 日後發行的第一個更新。|
|軟體中心有新的新式外貌。 先前只出現在 Silverlight 相依應用程式類別目錄 (使用者可用的應用程式) 中的應用程式，現在會出現在軟體中心的 [應用程式] 索引標籤中。 應用程式類別目錄還是可以使用軟體中心 [安裝狀態] 索引標籤的連結進行存取。<br><br>幾個月後即不再提供舊版的軟體中心。<br><br>您可以啟用用戶端設定的 [電腦代理程式] > **[使用新的軟體中心]**，設定用戶端使用新的軟體中心。<br><br>如需關於軟體中心的詳細資訊，請參閱[在 System Center Configuration Manager 中規劃和設定應用程式管理](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management)。|2016 年 12 月 13 日|針對舊版軟體中心的支援將隨著於 2018 年 1 月 1 日後所發行的第一個更新而結束。|
|使用 Configuration Manager 管理虛擬硬碟 (VHD)。 </br></br>這包括移除建立新 VHD 或是使用工作序列管理 VHD 的選項，以及從 Configuration Manager 主控台移除虛擬硬碟節點。 </br></br>移除這項支援之後，不會刪除現有的 VHD，但也無法再從 Configuration Manager 主控台中存取它。  |2017 年 1 月 6 日 |VHD 的支援將結束於 2017 年 6 月 1 日後發行的第一個更新。|
|System Center Configuration Manager 升級評估工具。 </br></br>「升級評估工具」同時依賴 System Center Configuration Manager 和應用程式相容性工具組 (ACT) 6.x。 ACT 的最終版本隨附於 Windows 10 v1511 ADK。 因為 ACT 已不會有任何進一步的更新，將會中止升級評估工具的支援。 </br></br>升級評估工具會由[升級整備](/sccm/core/clients/manage/upgrade/upgrade-analytics)功能取代。 取代注意事項已於 2016 年 9 月 12 日新增至 [UAT 下載頁面 (英文)](https://www.microsoft.com/download/details.aspx?id=37145)。 |2016 年 9 月 12 日  | 2017 年 7 月 11 日 |  


<br></br>
System Center Configuration Manager 1511 版中已移除功能的其他詳細資訊︰

###  <a name="bkmk_amt"></a> 超出訊號範圍管理  
 Configuration Manager 已從 Configuration Manager 主控台內移除 AMT 型電腦的原生支援。  

-   當您使用 [Microsoft System Center Configuration Manager 的 Intel SCS 附加元件](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)時，仍會完全管理 AMT 電腦。 附加元件可讓您存取管理 AMT 的最新功能，同時移除 Configuration Manager 併入那些變更之前所引入的限制。  

-   這項變更不會影響 System Center 2012 Configuration Manager 中的頻外管理。  

###  <a name="bkmk_nap"></a> 網路存取保護  
 System Center Configuration Manager 已移除網路存取保護的支援。 此功能在 Windows Server 2012 R2 中已淘汰，且已從 Windows 10 移除。  

 如需了解網路存取保護的替代方案，請參閱 *網路原則與存取服務概觀* 中的 [淘汰的功能](https://technet.microsoft.com/library/hh831683.aspx)一節。

