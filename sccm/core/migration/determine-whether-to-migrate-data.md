---
title: "選擇要移轉的項目 | Microsoft Docs"
description: "了解您可以移轉哪些資料，以及無法移轉哪些資料至 System Center Configuration Manager。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 66e01cbe84206cb1b29893b768c1bc831f2f6cfc


---
# <a name="determine-whether-to-migrate-data-to-system-center-configuration-manager"></a>判斷是否要將資料移轉至 System Center Configuration Manager

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 移轉中，會提供一項程序，能將支援的 Configuration Manager 版本所製作的資料與組態，傳輸到新階層。  您可以使用該程序：  

-   將多個階層結合成一個階層  

-   將資料與組態從實驗室部署移至生產部署  

-   從先前版本的 Configuration Manager，像是無法升級到 System Center Configuration Manager 的 Configuration Manager 2007，或是從 System Center 2012 Configuration Manager (它不支援升級到 System Center Configuration Manager)，移動資料和設定。  

除了發佈點站台系統角色和裝載發佈點的電腦以外，各階層間無法共用基礎結構 (包括站台、站台系統角色或裝載站台系統角色的電腦)、移轉和傳送。  

 雖然您無法移轉伺服器基礎結構，但可在階層間移轉 Configuration Manager 用戶端。 用戶端移轉包括將用戶端使用的資料從來源階層移轉至目的地階層，然後再安裝或重新指派用戶端軟體，使用戶端回報至新階層。 在您安裝用戶端至新階層並且在用戶端提交其資料後，其獨有的 Configuration Manager 識別碼可協助 Configuration Manager 將您先前移轉的資料與各個用戶端電腦建立關聯。  

 移轉所提供的功能，有助於保有您在組態及部署期間所做的投資，同時您可充分發揮 System Center 2012 Configuration Manager 中首次出現且在 System Center Configuration Manager 仍然使用的產品中有關核心變更的好處。 這些變更包括使用較少站台及資源的精簡型 Configuration Manager 階層，以及使用原生 64 位元程式碼在 64 位元硬體上執行，以改善處理程序。  

 如需移轉支援之 Configuration Manager 版本的資訊，請參閱[在 System Center Configuration Manager 中進行移轉的必要條件](../../core/migration/prerequisites-for-migration.md)。  

 以下章節有助於規劃可以或不可以移轉的資料：  

-   [可以移轉至 System Center Configuration Manager 的資料](#Can_Migrate)  

-   [無法移轉至 System Center Configuration Manager 的資料](#Cannot_migrate)  

##  <a name="a-namecanmigratea-data-that-you-can-migrate-to-system-center-configuration-manager"></a><a name="Can_Migrate"></a> 可以移轉至 System Center Configuration Manager 的資料  
 移轉程序可在支援的 Configuration Manager 階層間移轉大部分物件。 從支援的 Configuration Manager 2007 版本移轉的某些物件執行個體，必須進行修改才能符合 Systerm Center 2012 Configuration Manager 架構及物件格式。 這些修改不會影響來源站台資料庫中的資料。 從支援的 System Center 2012 Configuration Manager 或 System Center Configuration Manager 版本移轉的物件，不需要修改。  

 以下是可根據來源階層中的 Configuration Manager 版本進行移轉的物件。 有些物件 (例如查詢) 並不會移轉。 如果您想要繼續使用這些不會移轉的物件，就必須在新階層中重新建立這些物件。 其他物件 (包括某些用戶端資料) 會在您於該階層中管理用戶端時，於新階層中自動重新建立這些物件。  

 **您可以從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 最新分支移轉的物件：**  

-   公告  

-   System Center 2012 Configuration Manager 及更新版本的應用程式  

-   System Center 2012 Configuration Manager 及更新版本的 App-V 虛擬環境  

-   Asset Intelligence 自訂  

-   界限  

-   集合 - 若要從支援的 System Center 2012 Configuration Manager 或 System Center Configuration Manager 版本移轉集合，您需使用物件移轉作業。  

-   相容性設定：  

    -   設定基準  

    -   設定項目  

-   作業系統部署：  

    -   開機映像  

    -   驅動程式套件  

    -   驅動程式  

    -   映像  

    -   套件  

    -   工作順序  

-   搜尋結果 - 已儲存的搜尋條件  

-   軟體更新：  

    -   部署  

    -   部署套件  

    -   範本  

    -   軟體更新清單  

-   軟體發佈套件  

-   軟體計量規則  

-   虛擬應用程式套件  

 **您可以從 Configuration Manager 2007 SP2 移轉的物件：**  

-   公告  

-   System Center 2012 Configuration Manager 及更新版本的應用程式  

-   System Center 2012 Configuration Manager 及更新版本的 App-V 虛擬環境  

-   Asset Intelligence 自訂  

-   界限  

-   集合 - 您可以使用集合移轉作業，從支援的 Configuration Manager 2007 版本移轉集合。  

-   相容性設定 (在 Configuration Manager 2007 中稱為 Desired Configuration Management)：  

    -   設定基準  

    -   設定項目  

-   作業系統部署：  

    -   開機映像  

    -   驅動程式套件  

    -   驅動程式  

    -   映像  

    -   套件  

    -   工作順序  

-   搜尋結果 - 搜尋資料夾  

-   軟體更新：  

    -   部署  

    -   部署套件  

    -   範本  

    -   軟體更新清單  

-   軟體發佈套件  

-   軟體計量規則  

-   虛擬應用程式套件  

##  <a name="a-namecannotmigratea-data-that-you-cannot-migrate-to-system-center-configuration-manager"></a><a name="Cannot_migrate"></a> 無法移轉至 System Center Configuration Manager 的資料  
 您無法移轉下列類型的物件：  

-   AMT 用戶端佈建資訊  

-   用戶端上的檔案，其中包含：  

    -   用戶端清查和歷程記錄資料  

    -   用戶端快取中的檔案  

-   查詢  

-   Configuration Manager 2007 安全性權限及執行個體  

-   來自 SQL Server Reporting Services 的 Configuration Manager 2007 報表  

-   Configuration Manager 2007 Web 報表  

-   System Center 2012 Configuration Manager 和 System Center Configuration Manager 報表  

-   System Center 2012 Configuration Manager 和 System Center Configuration Manager 以角色為基礎的系統管理：  

    -   安全性角色  

    -   安全性範圍  



<!--HONumber=Dec16_HO3-->


