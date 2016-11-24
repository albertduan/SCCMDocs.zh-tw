---
title: "已淘汰的功能 | System Center Configuration Manager"
description: "了解 System Center Configuration Manager 不再支援的功能、產品和作業系統。"
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f1e1070fd5b56b1abf22159e9f95b3b4bd8a8c6


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>System Center Configuration Manager 的已移除和已淘汰功能

適用於：System Center Configuration Manager (最新分支)

本主題說明已從 System Center Configuration Manager 取消支援的功能、產品與作業系統，或將在後續更新中將會移除 (淘汰) 的功能、產品與作業系統。 這些未來變更可能會對您的 Configuration Manager 使用產生影響，因此本主題旨在提供相關預警。  

 這項資訊有可能隨著後續版本而有所變更，且可能不會包含每項被淘汰的功能、產品或作業系統。  

## <a name="deprecated-features-products-and-operating-systems"></a>已淘汰的功能、產品與作業系統  
 列為已淘汰的 Microsoft 產品與作業系統，目前處於延長支援或已到達支援時限的結尾。 如果 Microsoft 產品與作業系統列為已淘汰，但只要未逾其 Microsoft 技術支援週期，仍會使用目前的  Configuration Manager 版本進行測試。  如需詳細資訊，請參閱 [Microsoft 支援服務週期](https://support.microsoft.com/lifecycle) 網站。  

 **已淘汰的功能：**  


|**功能**|**首次宣布的淘汰項目**|**移除的支援**|  
|-|-|-|  
|網路存取保護 (NAP) - 自 System Center 2012 Configuration Manager 起提供|7/10/2015|√|  
|頻外管理 - 自 System Center 2012 Configuration Manager 起提供|10/16/2015|√|  

 **已淘汰的伺服器作業系統：**  

 |**作業系統**|**首次宣布的淘汰項目**|**移除的支援**|  
|-|-|-|  
|Windows Server 2008|7/10/2015|支援將結束於 2016 年 12 月 31 日後發行的第一項更新 (請參閱附註 1)|  
|Windows Server 2008 R2|7/10/2015|支援將結束於 2016 年 12 月 31 日後發行的第一項更新 (請參閱附註 2)|  

-   附註 1：支援結束之後，此作業系統將不再支援站台伺服器或大部分的站台系統角色。 不過，它仍會持續支援發佈點站台系統角色 (包括提取發佈點)，直到宣佈此項支援已遭取代，或此作業系統的延伸支援期限過期。  

-   附註 2：支援結束之後，此作業系統將不再支援站台伺服器或大部分的站台系統角色。 不過，它仍會持續支援狀態移轉點和發佈點站台系統角色 (包括提取發佈點，並且適用於 PXE 和多點傳送)，直到宣佈此項支援已遭取代，或此作業系統的延伸支援期限過期。  從 1602 版開始，您可以將站台伺服器的作業系統從 Windows Server 2008 R2 就地升級到 Windows Server 2012 R2。  

     如需站台伺服器作業系統之就地升級的詳細資訊，請參閱 [What's changed in System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) (System Center Configuration Manager 中的變更) 中的[就地升級執行 Windows Server 2008 R2 之站台伺服器的作業系統](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS)一節。



 **已淘汰的用戶端作業系統：**  

 除非另有說明，否則只要作業系統是受支援的 Configuration Manager 用戶端，則在作業系統的「延伸支援結束日期」之前，皆會受到支援，如 [Microsoft 週期原則](https://support.microsoft.com/lifecycle)中所述。  如果 Configuration Manager 支援的作業系統將在「延伸支援結束日期」之前結束，該作業系統的淘汰日期及支援移除日期將在此列出。  

|**作業系統**|**首次宣布的淘汰項目**|**移除的支援**|  
|-|-|-|  
|Windows XP|7/10/2015|√|  
|Windows XP Embedded|7/10/2015|支援將結束於 2016 年 12 月 31 日後發行的第一項更新|  
|Windows Server 2003|7/10/2015|√|  
|Windows Server 2003 R2|7/10/2015|√|  
|Windows Vista|7/10/2015|√|  
|Mac OS X  10.6 - 10.8|7/10/2015|√|  
|Windows Mobile 6.0 - 6.5|7/10/2015|√|  
|Nokia Symbian Belle|7/10/2015|√|  
|Windows CE 5.0 - 6.0|7/10/2015|√|  


 **已淘汰可支援做為站台資料庫的 SQL Server 版本：**  

|**SQL Server 版本**|**首次宣布的淘汰項目**|**移除的支援**|   
|-|-|-|  
|SQL Server 2008|7/10/2015|√|  
|SQL Server 2008 R2|7/10/2015|支援將結束於 2016 年 12 月 31 日後發行的第一項更新|  

## <a name="features-removed-in-system-center-configuration-manager"></a>System Center Configuration Manager 中移除的功能  
 從初始 System Center Configuration Manager 版本開始，已移除下列功能：

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a> 頻外管理  
 Configuration Manager 已從 Configuration Manager 主控台內移除 AMT 型電腦的原生支援。  

-   當您使用 [Microsoft System Center Configuration Manager 的 Intel SCS 附加元件](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)時，仍會完全管理 AMT 電腦。  

-   使用附加元件可讓您存取管理 AMT 的最新功能，同時移除 Configuration Manager 併入那些變更之前所引入的限制。  

-   這項變更不會影響 System Center 2012 Configuration Manager 中的頻外管理。  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a> 網路存取保護  
 System Center Configuration Manager 已移除網路存取保護的支援。 此功能在 Windows Server 2012 R2 中已淘汰，且已從 Windows 10 移除。  

 如需了解網路存取保護的替代方案，請參閱 **網路原則與存取服務概觀** 中的 [淘汰的功能](https://technet.microsoft.com/library/hh831683.aspx)一節。  



<!--HONumber=Nov16_HO1-->


