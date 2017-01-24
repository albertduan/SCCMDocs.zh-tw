---
title: "使用裝置註冊管理員來向 Configuration Manager 註冊裝置 | Microsoft Docs"
description: "使用裝置註冊管理員帳戶來向 System Center Configuration Manager 註冊公司擁有的裝置。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
caps.latest.revision: 8
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: ed60b23f7e7a194676cd7b055da9bc3517af8026


---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>使用裝置註冊管理員來向 Configuration Manager 註冊裝置

*適用於：System Center Configuration Manager (最新分支)*

組織可以搭配使用 System Center Configuration Manager 和 Intune，以單一使用者帳戶來管理大量的行動裝置。 「裝置註冊管理員」帳戶是特殊的 Intune 帳戶，具有註冊五部以上裝置的權限。  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>使用裝置註冊管理員註冊公司所擁有的裝置  
 您可以指派存放區管理員或監督員 (例如，裝置註冊管理員使用者帳戶)，讓她可以執行下列作業：  

-   註冊裝置以進行管理  

-   使用公司入口網站應用程式來安裝公司應用程式  

-   安裝和解除安裝軟體  

-   設定公司資料存取  


下列限制適用於使用裝置註冊管理員帳戶管理的裝置︰

- 存放區管理員無法從公司入口網站重設裝置。  
-  裝置不能加入工作區或 Azure Active Directory。 這可以防止這些裝置使用條件式存取。
-  若要將公司應用程式部署到使用裝置註冊管理員管理的裝置，請將公司入口網站應用程式當作**必要安裝**，部署到裝置註冊管理員的使用者帳戶。 裝置註冊管理員就可以啟動公司入口網站應用程式以安裝其他應用程式。
- 為了改善效能，公司入口網站應用程式只會顯示本機裝置。 其他 DEM 裝置的遠端管理只能夠從 Configuration Manager 主控台由系統管理員進行
- 裝置註冊管理員帳戶無法使用公司入口網站。 使用公司入口網站應用程式。

 **裝置註冊管理員案例的範例：**   
餐廳想要有銷售點平板電腦，以取得廚房員工的等待員工和訂單監視器。 員工永遠不需要存取公司資料或以使用者身分登入。 Intune 系統管理員會建立裝置註冊管理員帳戶，並使用該帳戶註冊公司所擁有的裝置。 或者，系統管理員可以將裝置註冊管理員認證提供給餐廳經理，讓他或她註冊和管理裝置。  

 系統管理員或管理員可以將角色特定應用程式部署到餐廳裝置。 系統管理員也可以在主控台中選取裝置，以及淘汰裝置，不進行行動裝置管理。  

#### <a name="add-a-device-enrollment-manager"></a>新增裝置註冊管理員  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 **[系統管理]** 工作區中，展開 **[雲端服務]**，然後按一下 **[Microsoft Intune 訂閱]**(搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理新功能)。 選取您將新增裝置註冊管理員的 Microsoft Intune 訂閱，然後按一下 [內容]。  

3.  在 [Microsoft Intune 訂閱內容] 對話方塊中，按一下 [裝置註冊管理員] 索引標籤。  

4.  按一下 [新增/移除]。  

5.  在 [裝置註冊管理員] 對話方塊中，輸入您想要新增作為裝置註冊管理員的使用者名稱，然後按一下 [搜尋]。 選取您想要新增作為裝置註冊管理員的使用者，然後按一下 [新增]。  

6.  確認將是裝置註冊管理員的使用者帳戶，然後按一下 [新增/移除]。  每位存取該服務的使用者，都需要訂閱授權，而「裝置註冊管理員」(device enrollment manager) 不得為 Intune 系統管理員。 決定是否需要新增更多授權，然後再使用這項功能。  

7.  裝置註冊管理員現在可以在公司入口網站中，運用使用者用於自攜裝置 (BYOD) 案例中的同一程序註冊行動裝置。  

#### <a name="delete-a-device-enrollment-manager-from-intune"></a>從 Intune 刪除裝置註冊管理員  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 **[系統管理]** 工作區中，展開 **[雲端服務]**，然後按一下 **[Microsoft Intune 訂閱]**(搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理新功能)。 選取您將新增裝置註冊管理員的 Microsoft Intune 訂閱，然後按一下 [內容]。  

3.  在 [Microsoft Intune 訂閱內容] 對話方塊中，按一下 [裝置註冊管理員] 索引標籤。  

4.  [搜尋] 您想要刪除的裝置註冊管理員，然後依序按一下 [移除]、[確定]。  

 刪除裝置註冊管理員對已註冊的裝置沒有影響。 刪除裝置註冊管理員之後：  

-   已註冊的裝置不會受到影響  

-   仍可全面管理已註冊的裝置  

-   刪除的裝置註冊管理員帳戶認證仍能繼續用於登入公司入口網站來存取應用程式  

-   刪除的裝置註冊管理員帳戶認證仍然無法抹除或淘汰裝置  

-   刪除之裝置註冊管理員帳戶與註冊裝置之間的關聯性仍然存在，但不能再註冊其他裝置



<!--HONumber=Dec16_HO3-->


