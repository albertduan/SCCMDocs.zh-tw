---
title: "站台和階層基本概念 | System Center Configuration Manager"
description: "取得 System Center Configuration Manager 站台和階層的基本資訊。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 07e10ead8d4b147a4a96b1e5189597e1ac4d4f52


---
# <a name="fundamentals-of-sites-and-hierarchies-for-system-center-configuration-manager"></a>System Center Configuration Manager 的站台和階層基本概念

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 部署必須安裝於 Active Directory 網域中，並具有形成站台階層的一或多個 Configuration Manager 站台的基礎。 從單一站台到多站台階層，如有必要的話，您所安裝的站台類型和位置可讓您向上擴充 (擴展) 您的部署，並且傳送金鑰服務給受管理的使用者和裝置。

## <a name="hierarchies-of-sites"></a>站台的階層架構
當您初次安裝 System Center Configuration Manager 時，您安裝的第一個 Configuration Manager 站台會決定階層的範圍 - 這將作為您管理您企業中裝置和使用者的基礎。 此第一個站台必須是管理中心網站或獨立的主要站台。  

 **管理中心網站**適用於大規模部署，既提供集中的管理點，也提供可支援分散於全球網路基礎結構中裝置的靈活性。 安裝管理中心網站之後，您將需要安裝一或多個主要站台做為子站台。  這是因為管理中心網站並不直接支援裝置管理，那是主要站台的功能。 管理中心網站支援多個子主要站台，當您的受管理裝置位於各個不同地理位置時，您可以使用這些站台來直接管理裝置及控制網路頻寬。  

 **獨立主要站台**適用於較小規模的部署，並且不需安裝其他站台，即可用來管理裝置。 雖然獨立主要站台會限制您的部署大小，但是它支援在稍後藉由安裝新管理中心網站來擴充階層的案例。 使用這個站台擴充案例時，您的獨立主要站台會變成子主要站台，而您可以接著在新管理中心網站底下安裝其他子主要站台。  這樣便可讓您擴充初始部署以滿足您企業未來成長的需求。  

> [!TIP]  
>  獨立主要站台與子主要站台實際上是相同類型的站台：主要站台。 根據您同時使用管理中心網站時所建立的階層關聯性，名稱會有所差異。  此階層關聯性也可以限制擴充 Configuration Manager 功能的特定站台系統角色安裝。 這是因為特定的站台系統角色只能安裝在階層 (管理中心網站或獨立主要站台) 的最上層站台。  

 在安裝第一個站台之後，您可以安裝其他站台。  如果您的第一個站台是管理中心網站，則您可以安裝一或多個子主要站台。  安裝主要站台 (獨立或子主要站台) 之後，您可以接著安裝一或多個次要站台。  

 **次要站台** 只能安裝在主要站台底下作為子站台。 此站台類型延伸了主要站台的涵蓋範圍，使其可以管理所在位置對主要站台連線較慢的裝置。   即使次要站台延伸了主要站台，用戶端仍然是由主要站台管理。 次要站台可藉由對整個網路中您傳送 (部署) 到用戶端及用戶端傳送回站台的資訊進行傳輸壓縮再加以管理，為遠端位置中的裝置提供支援。  

 下圖顯示一些網站設計的範例。  

 ![階層範例](media/Hierarchy_examples.png)  

 如需詳細資訊，請參閱下列主題：  

-   [System Center Configuration Manager 簡介](../../core/understand/introduction.md)  

-   [為 System Center Configuration Manager 設計站台階層](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [安裝 System Center Configuration Manager 站台](/sccm/core/servers/deploy/install/installing-sites)  

## <a name="site-system-servers-and-site-system-roles"></a>站台系統伺服器和站台系統角色  
 每個 Configuration Manager 站台都會安裝支援管理操作的**站台系統角色**。  有些角色是您安裝站台時預設安裝的角色，例如**站台伺服器**角色 (會指派給您安裝站台的電腦) 和站台資料庫伺服器角色 (會指派給裝載站台資料庫的 SQL Server)。 其他站台系統角色則是選用性角色，只有當您想要使用某個站台系統角色所啟用的功能時才使用。  所有裝載站台系統角色的電腦都稱為站台系統伺服器。  

 就較小規模的 Configuration Manager 部署而言，您可能一開始會直接在站台伺服器電腦上執行所有站台系統角色。 然後，隨著您的受管理環境和需求成長，您可以安裝其他站台系統伺服器來裝載其他站台系統角色，以改進站台在提供服務給更多裝置方面的效率。  

 如需不同站台系統角色的資訊，請參閱[為 System Center Configuration Manager 規劃站台系統伺服器和站台系統角色](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)中的[站台系統角色](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)  

## <a name="publishing-site-information-to-active-directory-domain-services"></a>將站台資訊發佈至 Active Directory 網域服務  
 為了簡化 Configuration Manager 的管理，您可以延伸 Active Directory 架構以支援 Configuration Manager 所使用的詳細資料，然後讓站台將其金鑰資訊發佈到「Active Directory 網域服務 (AD DS)」。 這可讓您想要管理的電腦能夠從受信任的 AD DS 來源安全地擷取站台相關資訊。 用戶端可擷取的資訊會識別出可用的站台、站台系統伺服器，以及這些站台系統伺服器所提供的服務。  

 **延伸 Active Directory 架構**的操作在每個樹系只進行一次，並且可在安裝 Configuration Manager 之前或之後進行。   延伸架構時，您必須在每個包含 Configuration Manager 站台 (此站台將發佈可供用戶端尋找的資料) 的網域中，建立一個名為**系統管理**的新 Active Directory 容器。 如需詳細資訊，請參閱 [Extend the Active Directory schema for System Center Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md) (擴充 System Center Configuration Manager 的 Active Directory 架構)。  

 **發佈站台資料**可以改善 Configuration Manager 階層的安全性並減少系統管理額外負荷，但就 Configuration Manager 基本功能而言並不非必要。  



<!--HONumber=Nov16_HO1-->


