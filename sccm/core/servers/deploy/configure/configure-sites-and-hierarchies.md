---
title: "設定站台 | System Center Configuration Manager"
description: "請參閱這份檢查清單，確保考慮到對站台和階層皆有影響的最常見設定。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: 15
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 470efc428045398588345f4546eb27831837715c


---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 設定站台與階層

*適用對象：System Center Configuration Manager (最新分支)*

安裝第一個 System Center Configuration Manager 站台，或將其他站台加入您的階層之後，使用下列檢查清單可確保您考慮到會影響站台與階層的最常見設定。  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>新站台與和其他站台的一般組態檢查清單  
 對於大多數的部署，您並不需要依照特定順序設定下列選項：  

-   但有些選項是彼此相依的，例如 Active Directory 樹系探索、界限以及界限群組。  

-   其中有一些組態有預設值，無須任何設定變更即可使用 (至少暫時如此)。  

-   而其他組態 (例如界限群組與發佈點群組) 則必須先設定之後才可使用。  

|動作|詳細資料|  
|------------|-------------|  
|設定以角色為基礎的系統管理|以角色為基礎的系統管理，是您如何分隔系統管理的指派，以控制哪些系統管理使用者在 Configuration Manager 環境中可檢視及管理不同的物件與資料。<br /><br /> 階層中的所有站台，會共用以角色為基礎之系統管理的組態。   <br />請參閱[為 System Center Configuration Manager 設定以角色為基礎的系統管理](../../../../core/servers/deploy/configure/configure-role-based-administration.md)。|  
|發佈站台資料至 Active Directory 網域服務 (AD DS)|將站台資料發佈到 AD DS 時，用戶端即可輕易地找到服務，並有效率地使用站台資源。<br /><br /> 您必須先個別[擴充 System Center Configuration Manager 的 Active Directory 架構](../../../../core/plan-design/network/extend-the-active-directory-schema.md)，並將每個站台設為[發佈 System Center Configuration Manager 的站台資料](../../../../core/servers/deploy/configure/publish-site-data.md)。|  
|設定服務連接點|您應該在階層的頂層站台，規劃安裝及設定服務連線點。 如需詳細資訊，請參閱[關於 System Center Configuration Manager 中的服務連線點](../../../../core/servers/deploy/configure/about-the-service-connection-point.md)。|  
|新增站台系統角色|為各個站台安裝一個或多個額外的站台系統角色。  請參閱 [Add site system roles for System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md)|  
|設定界限與界限群組|指定界限，其定義可包含您要管理之裝置的內部網路上的網路位置，然後設定界限群組，讓這些網路位置上的用戶端可找到 Configuration Manager 服務資源。 請參閱[為 System Center Configuration Manager 定義站台界限和界限群組](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)。|  
|設定發佈點群組|設定發佈點的邏輯群組，讓管理部署更容易。 請參閱 [Install and configure distribution points for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) (為 System Center Configuration Manager 安裝及設定發佈點) 中的 [Manage distribution point groups](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) (管理發佈點群組)。|  
|執行探索工作|執行探索工作以在網路上尋找資源，包括網路基礎結構、裝置與使用者。<br /><br /> 請參閱[為 System Center Configuration Manager 執行探索](../../../../core/servers/deploy/configure/run-discovery.md)。|  
|為管理基礎結構的人員新增備援及容量|您可以安裝其他 SMS 提供者與 Configuration Manager 主控台，為管理基礎結構的系統管理員擴充容量：<br /><br /> **安裝額外的 SMS 提供者** 可為連絡點提供備援，以管理站台與階層。 請參閱 [Modify your System Center Configuration Manager 中的frastructure](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) 中的 [Modify your System Center Configuration Manager 中的frastructure](../../../../core/servers/manage/modify-your-infrastructure.md)。<br /><br /> **安裝其他 Configuration Manager 主控台** 可同時為額外的系統管理使用者提供存取。 請參閱[安裝 Configuration Manager 主控台](../../../../core/servers/deploy/install/install-consoles.md)。|  
|設定站台元件|您可以在每個站台設定站台元件，以修改站台系統角色與站台狀態報表的行為。 請參閱 [Site components for System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md)|  
|建立自訂集合|請使用探索到的裝置與使用者相關資訊，建立物件的自訂集合，以簡化之後的管理工作。 請參閱[如何在 System Center Configuration Manager 中建立集合](../../../../core/clients/manage/collections/create-collections.md)。|  
|設定管理高風險部署的設定|在系統管理使用者建立高風險的工作順序部署時，會對其發出警告的站台上，進行設定。  請參閱 [Settings to manage high-risk deployments for System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md)|  
|為管理點設定資料庫複本|依據管理點設定資料庫複本，以減少站台資料庫伺服器的 CPU 負載，因為這些管理點會服務來自用戶端的服務要求。 請參閱 [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)|  
|設定 SQL Server AlwaysOn 可用性群組來裝載站台資料庫|從 1602 版開始，您可以將可用性群組設定為於主要站台和管理中心網站裝載站台資料庫的高可用性和災害復原方案。 請參閱[適用於 System Center Configuration Manager 之高可用性站台資料庫的 SQL Server AlwaysOn](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。|  
|修改站台間的複寫|請參閱 [System Center Configuration Manager 中的站台間資料傳輸](../../../../core/servers/manage/data-transfers-between-sites.md)以了解下列主題：<br /><br /> 設定次要站台之間的 [File-based replication](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute)<br /><br /> 設定 [Database replication links](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> 設定 [Distributed views](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  



<!--HONumber=Nov16_HO1-->


