---
title: "使用 System Center Configuration Manager 和 Microsoft Intune 設定 iOS 和 Mac 的混合式裝置管理"
description: "使用 System Center Configuration Manager 和 Microsoft Intune 設定 iOS 裝置管理。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: 10
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3754f0e49d8393aed51bb6519af99b9eb728402f


---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>設定 iOS 的混合式裝置管理與 System Center Configuration Manager 和 Microsoft Intune

*適用於：System Center Configuration Manager (最新分支)*

使用 Configuration Manager 和 Intune，您可以啟用 BYOD (「自備裝置」) iOS 和 Mac OS X 裝置註冊，將公司電子郵件和資源的存取權授與 iPhone、iPad 和 Mac 使用者。 使用者只要安裝 Intune 公司入口網站應用程式，就可以透過原則將他們的裝置設為目標。 您必須從 Apple 匯入 Apple Push Notification Service (APNs) 憑證，才能管理 iOS 和 Mac 裝置。 這個憑證允許 Intune 管理 iOS 和 Mac 裝置以及建立與行動裝置管理授權單位服務的合格和加密 IP 連線。  

 您也可以註冊公司擁有的 iOS 裝置。  請參閱[註冊公司擁有的裝置](enroll-company-owned-devices.md)。  

## <a name="enable-ios-device-enrollment"></a>啟用 iOS 裝置註冊  
 若要支援註冊 iOS 裝置，您必須遵循下列步驟：  

#### <a name="set-up-ios-device-enrollment-in-configuration-manager"></a>在 Configuration Manager 中設定 iOS 裝置註冊  

1.  **必要條件** - 請先完成[設定混合式 MDM](setup-hybrid-mdm.md) 中的必要條件和程序，才能為任何平台設定註冊。    

2.  **下載憑證簽署要求** - 需有憑證簽署要求檔案 (.csr) 才能向 Apple 要求 APNs 憑證。  

    1.  在 Configuration Manager 主控台的 **[系統管理]** 工作區中，移至 **[雲端服務]**> **[Microsoft Intune 訂閱]**。  

    2.  在 [首頁]  索引標籤上，按一下 [建立 APNs 憑證要求] 。 [要求 Apple Push Notification Service 憑證簽署要求]  對話方塊隨即開啟。  

    3.  **瀏覽** 至儲存新的憑證簽署要求 (.csr) 檔案的路徑。 在本機儲存憑證簽署要求 (.csr) 檔案。  

    4.  按一下 [下載] 。 下載新的 Microsoft Intune .csr 檔案，並由 Configuration Manager 儲存。 .csr 檔案用來向 Apple Push Certificates Portal 要求信任關係憑證。  

3.  **申請 Apple 的 APNs 憑證** - Apple Push Notification Service (APNs) 憑證用以建立管理服務、Intune 和已註冊的 iOS 行動裝置間的信任關係。  

    1.  在瀏覽器中連線至 [Apple Push Certificates 入口網站](http://go.microsoft.com/fwlink/?LinkId=269844) ，並使用您的公司 Apple ID 登入。 未來必須使用這個 Apple ID 來更新 APNs 憑證。  

    2.  使用憑證簽署要求 (.csr) 檔案完成精靈。 下載 APNs 憑證並在本機儲存 .pem 檔案。 這個 APNs 憑證 (.pem) 檔案用來建立 Apple Push Notification 伺服器與 Intune 的行動裝置管理授權單位之間的信任關係。  

4.  **啟用註冊並上傳 APNs 憑證** - 啟用 iOS 註冊及上傳 APNs 憑證。  

    1.  在 Configuration Manager 主控台的 **[系統管理]** 工作區中，移至 **[雲端服務]** > **[Microsoft Intune 訂閱]**。  

    2.  在 **[訂閱]** 群組的 **[首頁]** 索引標籤中，按一下 **[設定平台]** > **[iOS]**。  

        > [!NOTE]  
        >  除非已在 Configuration Manager 主控台中啟用 iOS 註冊，否則請不要上傳 Apple Push Notification service (APNs) 憑證。  

    3.  在 [Microsoft Intune 訂閱內容]  對話方塊中，選取 [iOS]  索引標籤並按一下選取 [啟用 iOS 註冊]  核取方塊。  

    4.  按一下 [瀏覽] ，然後移至從 Apple 下載的 APNs 憑證 (.cer) 檔案。 Configuration Manager 顯示 APNs 憑證的資訊。 按一下 [確定]  將 APN 憑證儲存到 Intune。  

 設定好之後，您需要讓使用者了解如何註冊其裝置。 請參閱[要告訴使用者關於註冊其裝置的事項](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 這項資訊適用於透過 Microsoft Intune 與 Configuration Manager 管理的行動裝置。



<!--HONumber=Nov16_HO1-->

