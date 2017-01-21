---
title: "設定 Intune 訂閱 | 內部部署 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中為內部部署行動裝置管理設定 Intune 訂閱來追蹤授權。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
caps.latest.revision: 8
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4daf5d6ea30aa1fb4aa189ef6da9b364fe197805


---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>為 System Center Configuration Manager 中的內部部署行動裝置管理設定 Microsoft Intune 訂閱

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 內部部署行動裝置管理需要 Microsoft Intune 訂閱來追蹤授權。 不會使用 Intune 服務來管理裝置或儲存管理資訊。 針對內部部署行動裝置管理，所有裝置管理都是透過 Configuration Manager 基礎結構來處理。  

> [!IMPORTANT]  
>  Configuration Manager 不支援同時使用 Microsoft Intune 和內部部署 Configuration Manager 基礎結構作為管理授權單位。 因此，當您設定 Intune 訂閱以進行內部部署管理時，可以有效地停用 Intune 管理。  

 設定 Intune 服務以使用內部部署行動裝置管理的過程牽涉到下列高階步驟：  

-   [註冊 Microsoft Intune](#bkmk_signup)  

-   [將 Intune 訂閱新增至 Configuration Manager](#bkmk_addSub)  

-   [設定進行內部部署行動裝置管理的 Intune 訂閱](#bkmk_configure)  

> [!TIP]  
>  建議您在安裝必要站台系統角色，讓新安裝的站台系統角色能以最快時間開始運作前，先設定進行內部部署行動裝置管理的 Intune 訂閱。  

##  <a name="a-namebkmksignupa-sign-up-for-microsoft-intune"></a><a name="bkmk_signup"></a> 註冊 Microsoft Intune  
 需要有 Intune，才能進行內部部署行動裝置管理功能。 只要[註冊](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/)試用版或付費訂閱，並前往下一個步驟，就能將訂閱新增至 Configuration Manager。  

##  <a name="a-namebkmkaddsuba-add-the-intune-subscription-to-configuration-manager"></a><a name="bkmk_addSub"></a> 將 Intune 訂閱新增至 Configuration Manager  
 若要將訂閱新增至 Configuration Manager，請遵循與使用 Intune 新增行動裝置管理的訂閱時相同的基本步驟。 閱讀下面注意事項以了解特定差異，然後使用[使用 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理 (MDM)](../../mdm/plan-design/hybrid-mobile-device-management.md) 之[建立 Microsoft Intune 訂閱](../../mdm/plan-design/hybrid-mobile-device-management.md#bkmk_subscription)中的指示。  

> [!NOTE]  
>  當新增 Intune 訂閱時，請記住：  
>   
>  -   [新增 Microsoft Intune 訂閱精靈] 中指定的集合不會用於內部部署行動裝置管理使用者權限委派， 而僅用於透過 Intune 進行的行動裝置管理。 不過，您必須指定集合，精靈才能繼續。  
> -   內部部署行動裝置管理會忽略精靈中所指定的站台碼設定。 而使用您在註冊設定檔中指定的站台碼，此設定檔可授與使用者註冊裝置的權限。  
> -   請勿啟用多重要素驗證。 不支援內部部署行動裝置管理。  

##  <a name="a-namebkmkconfigurea-configure-the-intune-subscription-for-on-premises-mobile-device-management"></a><a name="bkmk_configure"></a> 設定進行內部部署行動裝置管理的 Intune 訂閱  

1.  在 Configuration Manager 主控台中，以滑鼠右鍵按一下 [Microsoft Intune 訂閱]，然後按一下 [內容]。  

2.  在 [內部部署行動裝置管理] 方塊中，按一下 [僅管理內部部署裝置] 旁的核取方塊，然後按一下 [確定] 。  

    > [!NOTE]  
    >  按一下此核取方塊後，即表示您將 Intune 訂閱設為讓所有管理資訊皆維持在內部部署，且不會將資料複寫至雲端。  

3.  如果您打算管理 Windows 10 行動裝置版的裝置，請以滑鼠右鍵依序按一下 [Microsoft Intune 訂閱] 、[設定平台] 及 [Windows Phone]  。  

4.  按一下 [Windows Phone 8.1 與 Windows 10 行動裝置版] 旁的核取方塊，然後按一下 [確定] 。  

5.  如果您打算管理 Windows 10 桌上型電腦，請以滑鼠右鍵依序按一下 [Microsoft Intune 訂閱] 、[設定平台] 及 [啟用 Windows 註冊] 。  

6.  按一下 [啟用 Windows 註冊] 旁的核取方塊，然後按一下 [確定] 。  



<!--HONumber=Nov16_HO1-->


