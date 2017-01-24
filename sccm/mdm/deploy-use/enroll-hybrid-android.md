---
title: "設定 System Center Configuration Manager 和 Microsoft Intune 的 Android 混合式裝置管理 | Microsoft Docs"
description: "準備使用 Configuration Manager 和 Intune 管理 Android 行動裝置。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: ab892174643e7565ad9a74abc4f83f2f152669bd


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>以 System Center Configuration Manager 和 Microsoft Intune 設定 Android 混合式裝置管理

*適用於：System Center Configuration Manager (最新分支)*

若為 System Center Configuration Manager，使用者可以從 Google Play 下載 Android 公司入口網站應用程式，以註冊包含 Samsung KNOX Standard 的 Android 裝置。 透過 Android 公司入口網站應用程式，您可以管理相容性設定、抹除或刪除 Android 裝置、部署應用程式，以及收集軟體和硬體清查。 如果 Android 裝置上未安裝 Android 公司入口網站應用程式，您將不會擁有所有管理功能 (例如清查和相容性設定)，但是仍然可以將應用程式部署到 Android 裝置。  

## <a name="prepare-to-manage-android-mobile-devices-with-configuration-manager-and-intune"></a>準備使用 Configuration Manager 和 Intune 管理 Android 行動裝置  
 下列步驟可讓 Configuration Manager 管理 Android 裝置。  

#### <a name="to-enable-android-enrollment"></a>啟用 Android 註冊  

1.  **必要條件** - 請先完成[設定混合式 MDM](setup-hybrid-mdm.md) 中的必要條件和程序，才能為任何平台設定註冊。  

2.  在 Configuration Manager 主控台的 **[系統管理]** 工作區中，移至 **[雲端服務]** > **[Microsoft Intune 訂閱]**。  

3.  在 **[首頁]** 索引標籤的 **[訂閱]** 群組中，按一下 **[設定平台]** > **[Android]**。  

4.  在 [Microsoft Intune 訂閱內容]  對話方塊中，選取 [Android]  索引標籤並按一下選取 [啟用 Android 註冊]  核取方塊。  

 設定好之後，您需要讓使用者了解如何註冊其裝置。 請參閱[要告訴使用者關於註冊其裝置的事項](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 這項資訊適用於透過 Microsoft Intune 與 Configuration Manager 管理的行動裝置。



<!--HONumber=Dec16_HO3-->


