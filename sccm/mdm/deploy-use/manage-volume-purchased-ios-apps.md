---
title: "管理大量採購的 iOS 應用程式 | Microsoft Docs"
description: "部署、管理和追蹤透過 iOS 應用程式市集購買的應用程式授權。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: aef92114af913b420a6e96876141a13a855677ea
ms.lasthandoff: 03/06/2017

---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Manage volume-purchased iOS apps with System Center Configuration Manager

*適用於：System Center Configuration Manager (最新分支)*



 iOS App Store 可讓您購買多個想要在公司內執行的應用程式授權。 這可協助您降低針對多個已購買之應用程式複本的追蹤管理開銷。  

 System Center Configuration Manager 可從 App Store 匯入授權資訊，並追蹤您已經使用的授權數量，以協助您部署及管理透過方案購買的 iOS 應用程式。  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>管理大量採購的 iOS 裝置應用程式  
 您可以透過 Apple 大量採購方案 (VPP) 購買 iOS 應用程式的多個授權。 這項作業包括從 Apple 網站設定 Apple VPP 帳戶，並將 Apple VPP 權杖上傳到 Configuration Manager，以提供下列功能：  

-   同步處理大量採購資訊與 Configuration Manager。  

-   Configuration Manager 主控台會顯示您已購買的應用程式。  

-   您可以部署和監視這些應用程式，並追蹤每個應用程式已使用的授權數量。  

-   Configuration Manager 可以解除安裝部署至使用者的大量採購應用程式，協助您在需要時取回授權。  

## <a name="before-you-start"></a>開始之前  
 在開始之前，您必須從 Apple 取得 VPP 權杖，並上傳至 Configuration Manager。  

> [!IMPORTANT]  
>  -   每個組織目前只能有一個 VPP 帳戶和權杖。  
> -   僅支援商用 Apple 大量採購方案。  
> -   當您將 Apple VPP 帳戶與 Intune 建立關聯後，就不能再與其他帳戶建立關聯。 因此，您所使用的帳戶詳細資訊盡量不要只有自己一人知道，以免不慎遺忘。  
> -   如果您先前是使用現有 Apple VPP 帳戶中不同 MDM 產品的 VPP 權杖，則必須產生新的權杖，才能搭配 Configuration Manager 使用。  
> -   每個權杖有效期限為一年。  
> -   Configuration Manager 預設一天同步處理兩次 Apple VPP 服務，以確保您的授權與 Configuration Manager 保持同步。  
>   
>      只會同步處理您的授權變更。 但每隔七天，皆會執行一次完整同步處理。  
>   
>      當您選擇 [同步處理] 以執行手動同步處理時，一律會執行完整同步處理。  
> -   如果需要復原或還原您的 Configuration Manager 資料庫，建議您在作業之後執行手動同步處理，以確保同步處理的授權資料是最新狀態。  
> -   雖然您可以將 iOS 大量採購的應用程式部署至使用者或裝置集合，但如果您將 VPP 應用程式部署至無使用者的裝置 (例如您使用裝置註冊計劃 (DEP) 或 Apple Configurator 註冊而沒有使用者親和性的裝置)，就不會安裝這些應用程式。  

 此外，您必須已從 Apple 匯入有效的 Apple Push Notification Service (APNs) 憑證，才能管理 iOS 裝置，包括應用程式部署。 如需詳細資訊，請參閱 [Set up iOS hybrid device management](enroll-hybrid-ios-mac.md) (設定 iOS 混合式裝置管理)。  

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>步驟 1 - 取得並上傳 Apple VPP 權杖  

1.  在 Configuration Manager 主控台中，選擇 [管理] > [雲端服務] > [Apple 大量採購方案權杖]。   

3.  在 [首頁] 索引標籤的 [Apple 大量採購方案權杖] 群組中，選擇 [Add Apple Volume Purchase Program Token]\(新增 Apple 大量採購方案權杖)。  

4.  在 [新增 Apple 大量採購方案權杖精靈] 的 [一般] 頁面中，設定下列各項︰   

    -   **名稱**：輸入此權杖的名稱，因為它會顯示在 Configuration Manager 主控台中。  

    -   **權杖** - 依序選擇 [瀏覽] 以及您從 Apple 網站下載的 VPP 權杖。  

         選擇 [查看 Apple VPP 帳戶] 連結；如果您還沒有這個帳戶，請註冊商用或教育單位使用的大量採購方案。 註冊之後，請下載您帳戶的 Apple VPP 權杖。  

    -   **描述**：(選擇性) 輸入可協助您在 Configuration Manager 主控台中識別此 VPP 權杖的描述。  

    -   **已指派類別來改善搜尋和篩選效果**：(選擇性) 您可以將類別指派給 VPP 權杖，讓搜尋在 Configuration Manager 主控台中更為容易。  

5.  選擇 [下一步]，然後完成精靈。  

您現在可以在 [Apple 大量採購方案權杖] 節點中檢視 Apple VPP 權杖的相關資訊，包含上次更新時間、到期時間，以及上次同步處理時間。

您可以在 [同步處理] 群組中，選擇 [首頁] 索引標籤的 [同步處理]，隨時將 Apple 保留的資料與 Configuration Manager 進行完整同步處理。  

## <a name="step-2---deploy-a-volume-purchased-app"></a>步驟 2 - 部署大量採購應用程式  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [License Information for Store Apps]\(市集應用程式的授權資訊)。  

3.  選擇要部署的應用程式，然後在 [常用] 索引標籤的 [建立] 群組中，選擇 [建立應用程式]。
隨即建立包含商務用 Windows 市集應用程式的 Configuration Manager 應用程式。 然後可以如處理任何其他 Configuration Manager 應用程式一樣，部署及監視此應用程式。

    > [!IMPORTANT]  
    > 部署目的必須選擇 [必要]。 目前不支援可用的安裝。

 當您部署應用程式時，安裝應用程式的每位使用者都會使用授權。  

 若要回收授權，您必須變更部署動作為 [解除安裝] 。 解除安裝應用程式之後，即會回收授權。  

## <a name="step-3---monitor-ios-vpp-apps"></a>步驟 3 - 監視 iOS VPP 應用程式  
 [軟體程式庫] 工作區的 [License Information for Store Apps]\(市集應用程式的授權資訊) 節點中，會顯示您大量購買的 iOS 應用程式相關資訊。 這些資訊包括您所擁有之每個應用程式的授權總數及已部署的數量。

 您也可以使用 [Apple Volume Purchase Program apps for iOS with license counts]\(Apple 大量採購方案 iOS 應用程式與授權計數) 報告，監視已購買的所有 VPP 應用程式授權使用量。  

 這份報告會顯示每個應用程式名稱以及您所購買的授權總數、可用授權數量等等。  

 如需執行 Configuration Manager 報告的協助，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)。  

