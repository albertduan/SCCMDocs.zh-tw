---
title: "使用 System Center Configuration Manager 和 Microsoft Intune 設定 iOS 和 Mac 的混合式裝置管理 | Microsoft Docs"
description: "使用 System Center Configuration Manager 和 Microsoft Intune 設定 iOS 裝置管理。"
ms.custom: na
ms.date: 07/31/2017
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
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: 1a93a542f55d02df20865fa4ae8d7590dd9be753
ms.contentlocale: zh-tw
ms.lasthandoff: 07/29/2017

---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 設定 iOS 的混合式裝置管理

適用於：System Center Configuration Manager (最新分支)

透過 Configuration Manager 和 Intune，您會啟用 iOS 和 macOS 裝置註冊，以將公司電子郵件和資源的存取權限提供給 iPhone、iPad 和 Mac 使用者。 使用者只要安裝 Intune 公司入口網站應用程式，就可以透過原則將他們的裝置設為目標。 您必須從 Apple 匯入 Apple Push Notification Service (APNs) 憑證，才能管理 iOS 和 Mac 裝置。 此憑證允許 Intune 透過建立與 Apple 裝置管理服務的連線，來管理 iOS 和 Mac 裝置。  

 您也可以註冊公司擁有的 iOS 裝置。  請參閱[註冊公司擁有的裝置](enroll-company-owned-devices.md)。  

**先決條件**<br>
您必須先完成[設定混合式 MDM](setup-hybrid-mdm.md) 中的必要條件和程序，才能為任何平台設定註冊。

若要支援註冊 iOS 裝置，您必須遵循下列步驟：  

## <a name="download-a-certificate-signing-request"></a>下載憑證簽署要求
需有憑證簽署要求檔案，才能向 Apple 要求 APNs 憑證。  

1.  在 Configuration Manager 主控台的 **[系統管理]** 工作區中，移至 **[雲端服務]**> **[Microsoft Intune 訂閱]**。  

2.  在 [常用] 索引標籤上，按一下 [建立 APNs 憑證要求]。 [要求 Apple Push Notification Service 憑證簽署要求] 對話方塊隨即開啟。  

3.  「瀏覽」至儲存新憑證簽署要求檔案的路徑。 在本機儲存憑證簽署要求檔案。  

4.  按一下 [下載]。 這會下載新的 Microsoft Intune 憑證簽署要求檔案，並由 Configuration Manager 儲存。 憑證簽署要求檔案是用來向 Apple Push Certificates 入口網站要求信任關係憑證。  

## <a name="request-an-mdm-push-certificate-from-apple"></a>向 Apple 要求 MDM Push Certificate
MDM Push Certificate 是用以建立管理服務、Intune 和已註冊的 iOS 行動裝置之間的信任關係。  

1.  在瀏覽器中連線至 [Apple Push Certificates 入口網站](http://go.microsoft.com/fwlink/?LinkId=269844)，並使用您的公司 Apple ID 登入。 未來必須使用這個 Apple ID 來更新 APNs 憑證。  

2.  使用憑證簽署要求 (.csr) 檔案完成精靈。 下載 MDM Push Certificate 並在本機儲存 .pem 檔案。 這個憑證 (.pem) 檔案是用來建立 Apple Push Notification 伺服器與 Intune 的行動裝置管理授權單位之間的信任關係。  

> [!NOTE]  
>  除非已在 Configuration Manager 主控台中啟用 iOS 註冊，否則請不要將 Apple Push Notification Service (APNs) 憑證上傳至 Intune。  

## <a name="enable-enrollment-and-upload-the-mdm-push-certificate"></a>啟用註冊並上傳 MDM Push Certificate
啟用 iOS 註冊，上傳 APNs 憑證。  

1.  在 Configuration Manager 主控台的 [系統管理] 工作區中，移至 [雲端服務] > [Microsoft Intune 訂閱]。  

2.  在 [常用] 索引標籤的 [訂閱] 群組中，按一下 [設定平台] > [iOS]。  

3.  在 [Microsoft Intune 訂閱內容] 對話方塊中，選取 [iOS] 索引標籤並按一下以選取 [啟用 iOS 註冊] 核取方塊。  
4.  按一下 [瀏覽]，然後移至從 Apple 下載的 APNs 憑證 (.cer) 檔案。 Configuration Manager 顯示 APNs 憑證的資訊。 按一下 [確定] 以將 APN 憑證儲存到 Intune。  

> [!NOTE]
> [註冊限制] 功能目前無法使用。 

> [!div class="button"]
[< 上一個步驟](create-service-connection-point.md)  [下一個步驟 >](set-up-additional-management.md)

