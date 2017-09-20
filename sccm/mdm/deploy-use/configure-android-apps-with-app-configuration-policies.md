---
title: "使用應用程式設定原則設定 Android for Work 應用程式 | Microsoft Docs"
description: "在使用者執行應用程式之前先將應用程式設定原則部署到使用者，以避免執行 Android for Work 的裝置發生設定問題。"
ms.custom: na
ms.date: 09/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9126d188-7780-45a4-b21d-7fcf4fad7da2
caps.latest.revision: "0"
caps.handback.revision: "0"
author: NathBarn
ms.author: NathBarn
manager: angrobe
ms.openlocfilehash: bd8388689a49873860fa9951b7d522f9d96fc11f
ms.sourcegitcommit: 31c670a4bce74fd64a7d46ebf7702f65b80d4147
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/13/2017
---
# <a name="apply-settings-to-android-for-work-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中使用應用程式設定原則將設定套用到 Android for Work 應用程式

*適用於：System Center Configuration Manager (最新分支)*

您可以在 System Center Configuration Manager 中使用應用程式設定原則，發佈使用者執行應用程式時可能需要的設定。 例如，應用程式可能需要使用者指定這些詳細資料：
- 自訂連接埠號碼
- 語言設定
- 安全性設定
- 公司標誌等品牌設定

如果使用者輸入不正確的設定，修正這些設定可能會增加技術支援中心的負擔，並使應用程式部署的速度變慢。 為了協助您避免這些問題，您可以在使用者執行應用程式之前，使用應用程式設定原則將必要的設定部署給使用者。 這些設定會自動與使用者相關聯。 使用者不需要採取任何動作。
不是將設定原則直接部署給使用者和裝置，而是在部署應用程式時建立原則與部署類型的關聯。 每當應用程式檢查是否有原則時 (通常是第一次執行應用程式時)，便會套用這些原則設定。

Android 應用程式設定原則只能在執行 Android for Work 的裝置上使用。 應用程式設定原則適用於來自 Play for Work 商店的已核准應用程式。 如需 Android 大量購買的應用程式的詳細資訊，請參閱[如何將應用程式部署到 Android for Work 裝置](https://docs.microsoft.com/en-us/intune/deploy-use/android-for-work-apps)。

如需應用程式安裝類型的詳細資訊，請參閱[應用程式管理簡介](/sccm/apps/understand/introduction-to-application-management)。

## <a name="create-an-app-configuration-policy"></a>建立應用程式設定原則

1. 在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [應用程式設定原則]。
2. 在 [首頁] 索引標籤的 [應用程式設定原則] 群組中，選擇 [建立應用程式設定原則]。
3. 在 [建立應用程式設定原則精靈] 的 [一般] 頁面上，設定下列原則資訊：
  - **名稱**。 輸入原則的唯一名稱。
  - **描述**。 (選擇性) 為了更輕鬆地識別原則，您可以新增描述。
  -  **選取設定原則類型**。 指定應用程式設定原則的目標平台：[適用於 Android for Work 應用程式的設定原則]。
  -  **已指派類別來改善搜尋和篩選效果**。 (選擇性) 若要建立並指派類別給原則，請選擇 [類別]。 [類別] 可讓您更輕鬆地在 Configuration Manager 主控台中排序及尋找項目。
4. 在 [Android for Work 原則] 頁面上，選擇設定原則資訊的設定方式：
  - **指定名稱及值配對**。 您可以對不使用巢狀結構的內容清單檔案使用此選項。 指定名稱/值對：
        1. 若要加入新的 JSON 配對，請選擇 [新增]。
        2. 在 [加入成對的名稱/值] 對話方塊中，指定下列詳細資料：
            - **類型**。 從清單中，選取您要指定的值類型。
            - **名稱**。 輸入您要指定值之內容清單索引鍵的名稱。
            - **值**。 輸入的值會套用到您輸入的索引鍵。

  - **瀏覽至屬性清單 JSON 檔案**。 如果您已經有應用程式設定 JSON 檔案，或針對使用巢狀結構的較複雜檔案，請使用此選項。 在 [應用程式設定原則] 欄位中，以正確的 JSON 格式輸入屬性清單資訊。
5. 若要匯入您稍早建立的 JSON 檔案，請選擇 [選取檔案]。
6. 選擇 [下一步]。 如果 JSON 碼有錯誤，您必須先更正這些錯誤才能繼續。
7. 完成精靈中所顯示的步驟。

新的應用程式設定原則會顯示在 [軟體程式庫] 工作區的 [應用程式設定原則] 節點中。

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>建立應用程式組態原則與 Configuration Manager 應用程式的關聯

若要建立應用程式設定原則與 Android for Work 應用程式部署的關聯，請使用[部署應用程式](/sccm/apps/deploy-use/deploy-applications)主題中的程序像平常那樣部署應用程式。

在 [部署軟體精靈] 的 [應用程式設定原則] 頁面上，選擇 [新增]。 在 [選取應用程式設定原則] 對話方塊中，選擇應用程式部署類型和您希望與它建立關聯的應用程式設定原則。
部署類型安裝後，就會自動套用應用程式設定原則設定。
