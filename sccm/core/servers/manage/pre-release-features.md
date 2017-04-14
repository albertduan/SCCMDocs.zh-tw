---
title: "發行前版本功能| Microsoft Docs"
description: "System Center Configuration Manager 的發行前版本功能"
ms.custom: na
ms.date: 4/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 32f7fc4ef9c8e8d3c2ec8eeaf9a3174bad992ffb
ms.openlocfilehash: a7ebfea849afcaf236d7e630aad2c7f3f1807a23
ms.lasthandoff: 04/08/2017


---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>System Center Configuration Manager 的發行前版本功能
*適用對象：System Center Configuration Manager (最新分支)*

 發行前版本功能是「最新分支」中所包含，用來在生產環境中進行早期測試的功能。 這些功能不應視為已準備好用於生產環境，但是可以在您的生產環境中使用。

 在您可以使用發行前版本功能之前，您必須在 Configuration Manager 主控台內同意使用發行前版本功能，才能選取並啟用。  

每個階層的同意都是無法取消的一次性動作。 直到您同意之前，您無法啟用包含於更新的發行前版本功能。

若要表示同意，請在主控台中移至 [系統管理] > [站台設定] > [站台]，然後選擇 [階層設定]。 在 [一般] 索引標籤上，選擇 [同意使用發行前功能]。

 > [!NOTE]
 > 如果您先前已啟用更新 1602 的發行前版本功能，在安裝較新的更新版本之前，那些功能將仍然可供使用，即使您未同意使用發行前版本功能。

當您安裝包含發行前版本功能的更新時，[更新與服務精靈] 中會顯示這些功能和包含在更新中的一般功能：
  - **如果您已同意：**安裝更新時，您即可透過 [更新與服務精靈] 啟用發行前版本功能。 若要這樣做，請選取發行前版本功能 (方法和選取任何其他功能相同)。     

    您也可以稍後透過主控台的 [系統管理] > [更新與服務] > [功能] 節點，啟用發行前版本功能。 在 [功能] 節點中，選擇功能，然後選擇 [開啟] 除非您同意，否則這個選項會呈現灰色。 (1702 版之前，[更新與服務] 位於 [系統管理] > [雲端服務] 底下)。
  -   **如果您尚未同意︰**安裝更新時，[更新與服務精靈] 中會顯示發行前版本功能，但為灰色且無法啟用。 安裝更新之後，您可以在 [功能] 節點中檢視這些功能，但未在 [階層設定] 中表示同意之前將無法啟用它們。

如果您已在獨立主要站台表示同意，然後藉由安裝新的管理中心網站來擴充階層，則必須於管理中心網站再授權一次。

 當您啟用發行前功能時，Configuration Manager 階層管理員 (HMAN) 必須在該功能提供使用前，先處理變更。 變更的處理通常立即進行，但可能需要 30 分鐘的時間完成，時間長度取決於 HAMN 處理循環。 在處理變更後，您必須先重新啟動主控台，才能檢視該功能相關的新 UI。

**下列為可用的發行前版本功能：**

 |功能          |已新增為發行前版本 | 已新增為完整功能|  
|------------------|---------------------|---------------------|
| 在安裝應用程式之前檢查執行中可執行檔  |   [版本 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |![尚未提供此服務](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 資料倉儲服務點  |  [版本 1702](/sccm/core/servers/manage/data-warehouse) |![尚未提供此服務](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 可將內容發佈至用戶端的對等快取 |  [版本 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![尚未提供此服務](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 雲端管理閘道 |  [版本 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![尚未提供此服務](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 用戶端資料來源儀表板 |  [版本 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![尚未提供此服務](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Microsoft Operations Management Suite 連接器  | [版本 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![尚未提供此服務](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 服務叢集感知集合 (用於服務伺服器群組)| [版本 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![尚未提供此服務](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|System Center Configuration Manager 所管理電腦的條件式存取 | [版本 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     | [版本 1702](/sccm/mdm/deploy-use/manage-access-to-services)                     |

