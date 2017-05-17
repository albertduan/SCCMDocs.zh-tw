---
title: "雲端管理閘道規劃 | Microsoft Docs"
description: 
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: c61769cc97c320452c9ee27a924cb01480e6f33d
ms.contentlocale: zh-tw
ms.lasthandoff: 03/27/2017

---

# <a name="plan-for-cloud-management-gateway-in-configuration-manager"></a>Configuration Manager 的雲端管理閘道規劃

*適用於：System Center Configuration Manager (最新分支)*

從 1610 版開始，雲端管理閘道提供簡單的方法，管理網際網路上的 Configuration Manager 用戶端。 雲端管理閘道服務已部署至 Microsoft Azure，並需要 Azure 訂用帳戶。 它會使用稱為雲端管理閘道連接器端點的新角色，連線至您內部部署的 Configuration Manager 基礎結構。 在部署及設定後，用戶端就能夠存取內部部署的 Configuration Manager 站台系統角色，不論它們位在內部的私人網路還是網際網路。

請使用 Configuration Manager 主控台將服務部署至 Azure、新增雲端管理閘道連接器端點角色，並設定站台系統角色以允許雲端管理閘道流量。 雲端管理閘道目前只支援管理點和軟體更新點角色。

需要用戶端憑證和安全通訊端層 (SSL) 憑證，才能進行電腦驗證，以及加密不同服務層級之間的通訊。 用戶端電腦通常會透過強制執行群組原則來接收用戶端憑證。 若要加密用戶端與裝載角色的站台系統伺服器之間的流量，您必須從 CA 建立自訂 SSL 憑證。 您也需要在 Azure 上設定管理憑證，以允許 Configuration Manager 部署雲端管理閘道服務。

## <a name="requirements-for-cloud-management-gateway"></a>雲端管理閘道的需求

-   用戶端電腦和執行雲端管理閘道連接器端點的站台系統伺服器。

-   來自內部 CA 的自訂 SSL 憑證 - 用來加密與用戶端電腦的通訊，並驗證雲端管理閘道服務的身分識別。

-   雲端服務的 Azure 訂用帳戶。

-   Azure 管理憑證 - 用來向 Azure 驗證 Configuration Manager。

## <a name="specifications-for-cloud-management-gateway"></a>雲端管理閘道的規格

- 每個雲端管理閘道執行個體支援 4000 個用戶端。
- 建議您至少建立兩個雲端管理閘道執行個體，以改善可用性。
- 雲端管理閘道只支援管理點和軟體更新點角色。
-   雲端管理閘道目前不支援下列 Configuration Manager 功能︰

    -   用戶端部署
    -   自動站台指派
    -   使用者原則
    -   應用程式類別目錄 (包括軟體核准要求)
    -   完整的作業系統部署 (OSD)
    -   Configuration Manager 主控台
    -   遠端工具
    -   報告網站
    -   網路喚醒
    -   Mac、Linux 及 UNIX 用戶端
    -   Azure Resource Manager
    -   對等快取
    -   內部部署行動裝置管理

## <a name="cost-of-cloud-management-gateway"></a>雲端管理閘道的成本

>[!IMPORTANT]
>下面提供的成本資訊僅供評估之用。 您的環境可能有其他變數會影響使用雲端管理閘道的總成本。

雲端管理閘道使用下列 Microsoft Azure 功能，會產生 Azure 訂閱帳戶費用︰

-   虛擬機器

    -   雲端管理閘道目前需要 Standard\_A2 虛擬機器。 建立服務時，您可以選取支援服務的 VM 數量 (預設值為一部)。

    -   僅供評估之用，預期單一 Azure Standard\_A2 虛擬機器可同時支援約 2000 個以網際網路為基礎的用戶端。

    -   請參閱 [Azure 價格計算機](https://azure.microsoft.com/en-us/pricing/calculator/)以利判斷潛在成本。

      >[!NOTE]
      >虛擬機器的成本隨地區而異。

-   輸出資料傳輸

    -   資料從服務傳出即產生費用。 請參閱 [Azure 頻寬定價詳細資料](https://azure.microsoft.com/en-us/pricing/details/bandwidth/)以利判斷潛在成本。

    -   僅供評估之用，以網際網路為基礎的用戶端每小時執行原則重新整理計算，預期每個用戶端每月大約為 100 MB。

    >[!NOTE]
    > 執行透過雲端管理閘道支援的其他動作 (例如部署軟體更新或應用程式)，會增加從 Azure 輸出的資料傳輸量。

-   內容儲存體

    -   使用雲端管理閘道管理的以網際網路為基礎的用戶端，會從 Windows Update 免費取得軟體更新內容。

    -   任何其他必要內容 (例如，應用程式) 必須發佈至雲端架構發佈點。 目前，雲端管理閘道只支援雲端發佈點將內容傳送至用戶端。

    - 如需詳細資訊，請參閱使用[雲端式發佈](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution)的成本。

## <a name="next-steps"></a>後續步驟

[設定雲端管理閘道](setup-cloud-management-gateway.md)

