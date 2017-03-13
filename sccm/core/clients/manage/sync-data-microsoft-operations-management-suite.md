---
title: "同步處理資料 | Microsoft Docs | Microsoft Operations Management Suite "
description: "將資料從 System Center Configuration Manager 同步處理至 Microsoft Operations Management Suite。"
ms.custom: na
ms.date: 10/13/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 0d8944bef9578a41b529a2d53b5a4d0094eaa21c
ms.lasthandoff: 12/16/2016

---
# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>將資料從 Configuration Manager 同步處理至 Microsoft Operations Management Suite

*適用於：System Center Configuration Manager (最新分支)*

您可以使用 Microsoft Operations Management Suite (OMS) 連接器同步處理資料 (例如從 System Center Configuration Manager 到 OMS 的收集)。 這可在 OMS 中顯示 Configuration Manager 部署中的資料。

## <a name="add-an-oms-connection-to-configuration-manager"></a>將 OMS 連線新增至 Configuration Manager

為了新增 OMS 連線，您的 Configuration Manager 環境必須先以[線上模式](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/)設定[服務連接點](../../../core/servers/deploy/configure/about-the-service-connection-point.md)。 當您將 OMS 連線新增至環境時，也會在執行此站台系統角色的電腦上安裝 Microsoft Monitoring Agent。
1.  在 [系統管理] 工作區中，選取 [OMS 連接器]。 在功能區中，按一下 [建立與 Operations Management Suite 的連線]。 這會開啟 「Connection to Operation Management Suite Wizard」 (與 Operations Management Suite 的連線精靈)。 選取 [下一步]。
2.  在 [一般] 畫面上，確認您擁有下列資訊，然後選取 [下一步]。

    * 將 Configuration Manager 註冊為「Web 應用程式和/或 Web API」管理工具，而且您擁有[來自此註冊的用戶端識別碼](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/)。
    * 在 Azure Active Directory 中，為已註冊的管理工具建立用戶端金鑰。
    * 在 Azure 管理入口網站中，為已註冊的 Web 應用程式提供 OMS 存取權限 (如[為 Configuration Manager 提供 OMS 的權限](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms)中所述)。

3.  在 [Azure Active Directory] 畫面上，將 OMS 連線設定設定成 OMS by 提供 [租用戶]、[用戶端識別碼] 和 [用戶端祕密金鑰]，然後選取 [下一步]。
4.  在 「OMS Connection Configuration」 (OMS 連線設定) 畫面上，填入 「Azure subscription」 (Azure 訂閱)、[Azure 資源群組] 和 [Operations Management Suite 工作區] 以提供連線設定。
5.  確認 [摘要] 畫面上的連線設定，然後選取 [下一步]。 [進度] 畫面將會顯示連線狀態，然後應該為 [完成]。

> [!NOTE]
> 您必須將 OMS 連線至階層中的頂層站台。 如果您將 OMS 連線至獨立主要站台，然後將管理中心網站新增至環境，則必須在新的階層內刪除並重新建立 OMS 連線。

將 Configuration Manager 連結至 OMS 之後，可以新增或移除集合，以及檢視 OMS 連線的內容。

## <a name="viewing-microsoft-operations-management-suite-connection-properties-in-configuration-manager"></a>在 Configuration Manager 中檢視 Microsoft Operations Management Suite 連線屬性

1.  瀏覽至 [雲端服務]，然後選取 [OMS 連接器] 開啟 「OMS Connection Properties」 (OMS 連線內容) 頁面。
2.  此頁面有兩個索引標籤︰
  * [Azure Active Directory] 索引標籤會顯示您的 [租用戶]、[用戶端識別碼]、[用戶端祕密金鑰到期]，並可讓您在用戶端祕密金鑰到期時「確認」[用戶端祕密金鑰]。
  * 「OMS Connection Properties」 (OMS 連線內容) 索引標籤會顯示 「Azure subscription」 (Azure 訂閱)、[Azure 資源群組]、[Operations Management Suite 工作區]，以及 [Device collections that Operations Management Suite can get data for (Operations Management Suite 可取得其資料的裝置集合)] 清單。 使用 [新增] 和 [移除] 按鈕修改允許的集合。

