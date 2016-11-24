---
title: "管理大量採購的 iOS 應用程式 | System Center Configuration Manager"
description: "部署、管理和追蹤透過 iOS 應用程式市集購買的應用程式授權。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5e7cead-e257-405b-a2aa-b0130e48dc40
caps.latest.revision: 23
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4289f4853f77392df420e44e179961609f83683f


---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Manage volume-purchased iOS apps with System Center Configuration Manager

*適用對象：System Center Configuration Manager (最新分支)*



 iOS 應用程式市集可讓您購買多個您想要在公司內執行的應用程式授權。 這可協助您降低追蹤多個已購買之應用程式複本的管理開銷。  

 System Center Configuration Manager 現在藉由從應用程式市集匯入授權資訊，可透過程式協助您管理購買的應用程式，並追蹤您已經使用了多少個授權。  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>管理大量採購的 iOS 裝置應用程式  
 您可以透過 Apple 大量採購方案 (VPP) 購買 iOS 應用程式的多個授權。 這項作業包括從 Apple 網站設定 Apple VPP 帳戶，並將 Apple VPP 權杖上傳到提供下列功能的 Configuration Manager：  

-   同步處理大量採購資訊與 Configuration Manager。  

-   Configuration Manager 主控台會顯示您已購買的應用程式。  

-   您可以部署和監視這些應用程式，也可以追蹤每個應用程式已使用的授權數量。  

-   Configuration Manager 可以解除安裝部署至使用者的大量採購應用程式，協助您在需要時取回授權。  

## <a name="before-you-start"></a>開始之前  
 在開始之前，您必須從 Apple 取得 VPP 權杖，並上傳至 Configuration Manager。  

> [!IMPORTANT]  
>  -   每個組織目前只能有一個 VPP 帳戶和權杖。  
> -   僅支援商用 Apple 大量採購方案。  
> -   一旦您將 Apple VPP 帳戶與 Intune 建立關聯後，之後就不能與其他帳戶建立關聯。 基於這個理由，請務必讓一人以上取得您所使用帳戶的詳細資料。  
> -   如果您先前已使用現有 Apple VPP 帳戶中不同 MDM 產品的 VPP 權杖，您必須產生新的權杖，才能搭配 Configuration Manager 使用。  
> -   每個權杖有效期限為一年。  
> -   Configuration Manager 預設一天同步處理兩次 Apple VPP 服務，以確保您的授權與 Configuration Manager 同步處理。  
>   
>      只會同步處理您的授權變更。 不過，每 7 天會執行一次完全同步處理。  
>   
>      當您按一下 [同步] 執行手動同步處理時，一律會執行完全同步處理。  
> -   如果需要復原或還原您的 Configuration Manager 資料庫，建議在此之後執行手動同步處理，以確保同步處理的授權資料是最新狀態。  
> -   雖然您可以將 iOS 大量採購的應用程式部署至使用者或裝置集合，但不會解除安裝您部署至無使用者裝置的 VPP 應用程式 (例如，您使用裝置註冊計劃 (DEP) 或 Apple Configurator 註冊的裝置沒有使用者親和性)。  

 此外，您必須已從 Apple 匯入有效的 Apple Push Notification Service (APNs) 憑證，才能管理 iOS 裝置，包括應用程式部署。 如需詳細資訊，請參閱 [Set up iOS hybrid device management](../../mdm/deploy-use/set-up-ios-hybrid-device-management.md) (設定 iOS 混合式裝置管理)。  

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>步驟 1 - 取得並上傳 Apple VPP 權杖  
  
1.  在 Configuration Manager 主控台中，按一下 [管理] > [雲端服務] > [Apple 大量採購方案權杖]。   
  
3.  在 [首頁] 索引標籤的 [Apple 大量採購方案權杖] 群組中，按一下 [新增 Apple 大量採購方案權杖]。  

4.  在 [新增 Apple 大量採購方案權杖精靈] 的 [一般] 頁面中，設定下列各項︰   

    -   **名稱**：輸入此權杖的名稱，因為它會顯示在 Configuration Manager 主控台中。  

    -   **權杖**：按一下 [瀏覽] 然後選取您從 Apple 網站下載的 VPP 權杖。  

         若尚未這麼做，請按一下 [查看 Apple VPP 帳戶] 連結，註冊商用或教育單位使用的大量採購方案。 註冊之後，請下載您帳戶的 Apple VPP 權杖。  

    -   **描述**：(選擇性) 輸入可協助您在 Configuration Manager 主控台中識別此 VPP 權杖的描述。  

    -   **已指派類別來改善搜尋和篩選效果**：(選擇性) 您可以將類別指派給 VPP 權杖，讓搜尋在 Configuration Manager 主控台中更為容易。  

5.  按一下 [下一步] 完成精靈。  
  
您現在可以在 [Apple 大量採購方案權杖] 節點中檢視 Apple VPP 權杖資訊，包含上次更新時間、到期時間，以及上次同步處理時間。 
  
您可以在 [同步] 群組中按一下 [首頁] 索引標籤的 [同步]，隨時完全同步處理 Apple 使用 Configuration Manager 來保留的資料。  
  
## <a name="step-2---deploy-a-volume-purchased-app"></a>步驟 2 - 部署大量採購應用程式  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] > [應用程式管理] > [市集應用程式的授權資訊]。  

3.  選擇要部署的應用程式，然後在 [首頁] 索引標籤的 [建立] 群組中，按一下 [建立應用程式]。
建立 Configuration Manager 應用程式以包含商務用 Windows 市集應用程式。 然後可以如處理任何其他 Configuration Manager 應用程式一樣，部署及監視此應用程式。

    > [!IMPORTANT]  
    > 部署目的必須選擇 [必要]。 目前不支援可用的安裝。

 當您部署應用程式時，安裝應用程式的每位使用者都會使用授權。  

 若要回收授權，您必須變更部署動作為 [解除安裝] 。 一旦應用程式解除安裝，將會回收授權。  

## <a name="step-3---monitor-ios-vpp-apps"></a>步驟 3 - 監視 iOS VPP 應用程式  
 [軟體程式庫] 工作區的 [市集應用程式的授權資訊] 節點會顯示大量採購 iOS 應用程式的相關資訊，包括每種應用程式擁有的授權數，以及已部署的數目。

 您也可以使用 [Apple 大量採購方案 iOS 應用程式與授權計數] 報告，監視已購買的所有 VPP 應用程式授權使用量。  

 此報表會顯示每個應用程式名稱以及您所購買的授權、可用授權數量的總數等等。  

 如需執行 Configuration Manager 報告的協助，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)。  



<!--HONumber=Nov16_HO1-->


