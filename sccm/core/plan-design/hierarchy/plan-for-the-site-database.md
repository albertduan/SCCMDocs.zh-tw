---
title: "規劃站台資料庫 | System Center Configuration Manager"
description: "當您在規劃 System Center Configuration Manager 階層時，請考慮站台資料庫及站台資料庫伺服器角色。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 40ebfaa9b82a65a6265f0c031dbbd0bcdb85da6e


---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>規劃 System Center Configuration Manager 的站台資料庫

*適用對象：System Center Configuration Manager (最新分支)*

網站資料庫伺服器是執行 Mcrosoft SQL Server (儲存 Configuration Manager 網站的資料) 受支援版本的電腦。 Configuration Manager 階層中的每個網站都包含網站資料庫，以及獲指派網站資料庫伺服器角色的伺服器。  

-   針對管理中心網站和主要站台，您可以在站台伺服器上安裝 SQL Server，或者在站台伺服器以外的電腦上安裝 SQL Server。  

-   針對次要站台，您可以使用 SQL Server Express (而非完整 SQL Server 安裝)；不過，資料庫伺服器必須在次要伺服器上執行。  

如果您使用遠端資料庫伺服器電腦，請確保中介網路連線為高可用性、高頻寬的網路連線。 這是因為網站伺服器與部分網站系統角色必須持續與裝載網站資料庫的 SQL Server 保持通訊。  


**選取遠端資料庫伺服器位置時，請考量以下項目：**  

-   與資料庫伺服器通訊所需的頻寬量依結合多少不同網站和用戶端設定而定。因此，實際需要的頻寬無法精準預測。  

-   每台執行 SMS 提供者的電腦，以及連線至網站資料庫的電腦，都會增加網路頻寬的需求。  

-   執行 SQL Server 的電腦所在的網域，是必須網站伺服器和所有執行 SMS 提供者之電腦間具備雙向信任的網域。  

-   網站資料庫與網站伺服器共置時，您無法使用網站資料庫伺服器的叢集 SQL 伺服器。  


一般來說，站台系統伺服器支援僅來自單一 Configuration Manager 站台的站台伺服器角色；不過，您也可以使用 SQL Server 的不同執行個體，在執行 SQL Server 的叢集或非叢集伺服器上，裝載來自不同 Configuration Manager 站台的資料庫。 若要支援來自不同網站的資料庫，您必須設定每個 SQL Server 執行個體使用通訊用的唯一連接埠。  


**下列的 SQL Server 組態可以用來裝載站台資料庫：**  

-   SQL Server 預設執行個體  

-   在執行 SQL Server 之單一電腦上的具名執行個體  

-   在 SQL Server 叢集執行個體上的具名執行個體  

-   SQL Server AlwaysOn 可用性群組 (自 1602 版開始)


**站台資料庫的必要條件：**  

-   若要裝載站台資料庫， SQL Server 必須符合 [System Center Configuration Manager 的 SQL Server 版本支援](../../../core/plan-design/configs/support-for-sql-server-versions.md)中所述的需求。  



<!--HONumber=Nov16_HO1-->


