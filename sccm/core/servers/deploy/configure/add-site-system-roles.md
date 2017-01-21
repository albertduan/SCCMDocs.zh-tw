---
title: "新增站台系統角色 | System Center Configuration Manager"
description: "了解 Configuration Manager 站台系統角色，以及如何加入它們以擴充站台的功能和容量。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
caps.latest.revision: 12
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f9437760936cdc4f9daad67205e635ab916207bd


---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 新增站台系統角色

*適用對象：System Center Configuration Manager (最新分支)*

每個 System Center Configuration Manager 站台支援多個站台系統角色，而每個角色都會擴充站台的功能與容量，以提供服務和管理裝置與使用者。 站台系統伺服器上的每個站台系統角色，都必須來自相同的站台。   

Configuration Manager 不支援單一站台系統伺服器上多個站台的站台系統角色。  

> [!TIP]  
>  如果您不熟悉站台系統角色的基本概念，或不熟悉站台伺服器、站台系統伺服器與站台系統角色之間的差異，請參閱 [Fundamentals of System Center Configuration Manager](../../../../core/understand/fundamentals.md)。  

 下列主題將詳細說明安裝站台系統角色的程序與相關詳細資料：  

-   [為 System Center Configuration Manager 安裝站台系統角色](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     本主題提供有關使用您可以用來安裝新站台系統角色之兩個主控台中精靈的基本指導方針。  

-   [在 Microsoft Azure 中，安裝 System Center Configuration Manager 的雲端架構發佈點](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    若您想使用 Microsoft Azure 來裝載部署至用戶端的內容，本主題的資訊有助於設定必要的憑證檔案，以啟用 Configuration Manager 與 Microsoft Azure 的通訊並使用 Microsoft Azure 訂閱。 此外，您必須設定名稱解析，以讓您的用戶端尋找您的雲端架構發佈點。  

-   [為 System Center Configuration Manager 中的內部部署行動裝置管理安裝站台系統角色](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     本主題將協助您順利設定您的站台系統角色，以支援使用 Configuration Manager 內部部署 MDM 來管理現代裝置。  

-   [System Center Configuration Manager 之站台系統角色的設定選項](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     某些站台系統角色支援的組態需要的詳細資訊，比在使用者介面中能解釋的還多。 本主題提供這些詳細資料。  



<!--HONumber=Nov16_HO1-->


