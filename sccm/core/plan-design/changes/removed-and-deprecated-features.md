---
title: "已淘汰的功能 | Microsoft Docs"
description: "了解 System Center Configuration Manager 不再支援的功能、產品和作業系統。"
ms.custom: na
ms.date: 12/05/2016
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
translationtype: Human Translation
ms.sourcegitcommit: c899b4beaa2aae4eb609291dca0e23f3c266627a
ms.openlocfilehash: 294166af3d5c6062e3508249c767779876b23931


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>System Center Configuration Manager 的已移除和已淘汰功能

適用於：System Center Configuration Manager (最新分支)

本主題說明已從 System Center Configuration Manager 取消支援的功能、產品與作業系統，或將在後續更新中將會移除 (淘汰) 的功能、產品與作業系統。 這些未來變更可能會對您的 Configuration Manager 使用產生影響，因此本主題旨在提供相關預警。  

 這項資訊有可能隨著後續版本而有所變更，且可能不會包含每項被淘汰的功能、產品或作業系統。  

## <a name="how-to-use-this-information"></a>如何使用此資訊  
若已先將某個功能或作業系統列為已淘汰，則對於將它與 Configuration Manager 搭配使用的支援，就會納入要從未來版本的 Configuration Manager 中移除的排程。 此資訊是提供來協助您規劃使用該功能或作業系統的替代方案。  在發行移除此支援的 Configuration Manager 第一個版本時，本主題中的詳細資料將會更新以指出該特定版本。  

移除對某個功能或作業系統的支援時，該功能或作業系統仍會在您使用舊版 Configuration Manager 時受到支援，但前提是該版本的 Configuration Manager 仍受到支援。 不過，當您使用在指定或版本日期之後發行的 Configuration Manager 版本時，該版本的 Configuration Manager 就不提供支援。

**例如︰**如果某個功能已排程為要透過 2016 年 9 月後發行的第一個更新來移除其支援，這表示對該功能的支援將不再隨附於更新 1610 (於 2016 年 10 月發行) 中。
-  透過更新 1610，就不再支援該功能。
-  此內容加以更新，以指出已透過版本 1610 移除支援。
不過，如果您繼續使用支援該功能的較早版本 (例如，版本 1602 或 1606)，您就能繼續使用該功能，直到您使用的版本不再受到支援為止。

如需詳細資訊，請參閱：
 - [Microsoft 支援週期原則](https://support.microsoft.com/lifecycle)網站
 - [System Center Configuration Manager 最新分支版本支援](/sccm/core/servers/manage/current-branch-versions-supported)

**已淘汰的功能：**  


|**功能**|**首次宣布的淘汰項目**|**移除的支援**|  
|-|-|-|  
|網路存取保護 (NAP) - 自 System Center 2012 Configuration Manager 起提供|7/10/2015|版本 1511|  
|頻外管理 - 自 System Center 2012 Configuration Manager 起提供|10/16/2015|版本 1511|
|工作順序： <br /> - 將磁碟轉換成動態磁碟 <br /> - 安裝部署工具 |11/18/2016|對於這些工作順序的支援將結束於 2017 年 6 月 1 日後發行的第一個更新|  

 **已淘汰的伺服器作業系統：**  

 |**作業系統**|**首次宣布的淘汰項目**|**移除的支援** |  
|-|-|-|  
|Windows Server 2008|7/10/2015|支援將結束於 2016 年 12 月 31 日後發行的第一個更新 (請參閱附註 1)|  
|Windows Server 2008 R2|7/10/2015|支援將結束於 2016 年 12 月 31 日後發行的第一項更新 (請參閱附註 2)|  

-   附註 1：支援結束之後，此作業系統將不再支援站台伺服器或大部分的站台系統角色。 不過，它仍會持續支援發佈點站台系統角色 (包括提取發佈點)，直到宣佈此項支援已遭取代，或此作業系統的延伸支援期限過期。  

-   附註 2：支援結束之後，此作業系統將不再支援站台伺服器或大部分的站台系統角色。 不過，它仍會持續支援狀態移轉點和發佈點站台系統角色 (包括提取發佈點，並且適用於 PXE 和多點傳送)，直到宣佈此項支援已遭取代，或此作業系統的延伸支援期限過期。  從 1602 版開始，您可以將站台伺服器的作業系統從 Windows Server 2008 R2 就地升級到 Windows Server 2012 R2。  

     如需站台伺服器作業系統之就地升級的詳細資訊，請參閱 [What's changed in System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) (System Center Configuration Manager 中的變更) 中的[就地升級執行 Windows Server 2008 R2 之站台伺服器的作業系統](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS)一節。



 **已淘汰的用戶端作業系統：**  

 除非另有說明，否則只要作業系統是受支援的 Configuration Manager 用戶端，則在作業系統的「延伸支援結束日期」之前，皆會受到支援，如 [Microsoft 週期原則](https://support.microsoft.com/lifecycle)中所述。  如果 Configuration Manager 支援的作業系統將在「延伸支援結束日期」之前結束，該作業系統的淘汰日期及支援移除日期將在此列出。  

|**作業系統**|**首次宣布的淘汰項目**|**移除的支援**|  
|-|-|-|  
|Windows XP|7/10/2015|版本 1511|  
|Windows XP Embedded|7/10/2015|支援將結束於 2016 年 12 月 31 日後發行的第一項更新|  
|Windows Server 2003|7/10/2015|版本 1511|  
|Windows Server 2003 R2|7/10/2015|版本 1511|  
|Windows Vista|7/10/2015|版本 1511|  
|Mac OS X  10.6 - 10.8|7/10/2015|版本 1511|  
|Windows Mobile 6.0 - 6.5|7/10/2015|版本 1511|  
|Nokia Symbian Belle|7/10/2015|版本 1511|  
|Windows CE 5.0 - 6.0|7/10/2015|版本 1511|  


 **已淘汰可支援做為站台資料庫的 SQL Server 版本：**  

|**SQL Server 版本**|**首次宣布的淘汰項目**|**移除的支援**|   
|-|-|-|  
|SQL Server 2008|7/10/2015|版本 1511|  
|SQL Server 2008 R2|7/10/2015|支援將結束於 2016 年 12 月 31 日後發行的第一項更新|  

## <a name="features-removed-in-system-center-configuration-manager"></a>System Center Configuration Manager 中移除的功能  
 從初始 System Center Configuration Manager 版本開始，已移除下列功能：

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a> 超出訊號範圍管理  
 Configuration Manager 已從 Configuration Manager 主控台內移除 AMT 型電腦的原生支援。  

-   當您使用 [Microsoft System Center Configuration Manager 的 Intel SCS 附加元件](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)時，仍會完全管理 AMT 電腦。  

-   使用附加元件可讓您存取管理 AMT 的最新功能，同時移除 Configuration Manager 併入那些變更之前所引入的限制。  

-   這項變更不會影響 System Center 2012 Configuration Manager 中的頻外管理。  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a> 網路存取保護  
 System Center Configuration Manager 已移除網路存取保護的支援。 此功能在 Windows Server 2012 R2 中已淘汰，且已從 Windows 10 移除。  

 如需了解網路存取保護的替代方案，請參閱 **網路原則與存取服務概觀** 中的 [淘汰的功能](https://technet.microsoft.com/library/hh831683.aspx)一節。  



<!--HONumber=Dec16_HO1-->


