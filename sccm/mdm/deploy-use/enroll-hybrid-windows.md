---
title: "設定 System Center Configuration Manager 和 Microsoft Intune 的 Windows 混合式裝置管理 | Microsoft Docs"
description: "使用 System Center Configuration Manager 和 Microsoft Intune 設定 Windows 裝置管理。"
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 4189fe34efc2ae134150a89791dc10bbab1b9d02
ms.lasthandoff: 03/17/2017


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>設定 Windows 的混合式裝置管理與 System Center Configuration Manager 和 Microsoft Intune

*適用對象：System Center Configuration Manager (最新分支)*

本主題將對 IT 系統管理員說明如何使用 Configuration Manager 和 Microsoft Intune，藉以將使用者的 Windows 電腦和行動裝置納入管理。 註冊方式有兩種︰
-  Azure Active Directory (AD) 會在使用者將其帳戶連線至裝置時自動註冊
- 藉由安裝並登入公司入口網站應用程式來註冊

## <a name="choose-how-to-enroll-windows-devices"></a>選擇註冊 Windows 裝置的方式

有兩個因素會決定註冊 Windows 裝置的方式︰
- **您是否使用 Azure Active Directory Premium？** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) 隨附於企業行動力 + 安全性和其他授權計劃內。
- **哪些版本的 Windows 用戶端會進行註冊？** <br>加入工作或學校帳戶即可自動註冊 Windows 10 裝置。 較舊版本則必須使用公司入口網站應用程式進行註冊。

||**Azure AD Premium**|**其他 AD**|
|----------|---------------|---------------|  
|**Windows 10**|[自動註冊](#automatic-enrollment) |[公司入口網站註冊](#company-portal-enrollment)|
|**舊版 Windows**|[公司入口網站註冊](#company-portal-enrollment)|[公司入口網站註冊](#company-portal-enrollment)|

## <a name="automatic-enrollment"></a>自動註冊

自動註冊可讓使用者藉由新增工作或學校帳戶，並同意進行管理，以註冊公司擁有或個人的 Windows 10 裝置。 在背景中，使用者的裝置會註冊並連接至 Azure Active Directory。 註冊之後，可使用 Intune 來管理裝置。 受管理的裝置仍然可以使用公司入口網站進行工作，但不一定要安裝它才能註冊。

**先決條件**
- Azure Active Directory Premium 訂閱 ([試用訂閱](http://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune 訂閱

### <a name="configure-automatic-enrollment"></a>設定自動註冊

1. 登入 [Azure 入口網站](https://manage.windowsazure.com)，並瀏覽至左窗格中的 [Active Directory] 節點，然後選取您的目錄。
2. 選取 [設定] 索引標籤，並捲動至稱為 [裝置] 的區段。
3. 選取 [All] (全部)，因為**使用者可能會將裝置與工作場所聯結**。
4. 選取您想要授權給每位使用者的裝置數目上限。

根據預設，並未對服務啟用雙因素驗證。 不過，於註冊裝置時，會建議使用雙因素驗證。 您必須先在 Azure Active Directory 中設定雙因素驗證提供者，並針對多重要素驗證來設定您的使用者帳戶之後，才會需要此服務的雙因素驗證。 請參閱[開始使用 Azure Multi-Factor Authentication Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud)。

## <a name="company-portal-enrollment"></a>公司入口網站註冊
您的使用者或[裝置註冊管理員](enroll-devices-with-device-enrollment-manager.md)可以藉由安裝公司入口網站應用程式後以其工作認證進行登入，以註冊 Windows 裝置。 若要為您的使用者簡化註冊程序，您應該將一個 CNAME 新增至 DNS 登錄。

### <a name="enable-windows-device-management"></a>啟用 Windows 裝置管理
若要為電腦或行動裝置啟用 Windows 裝置管理，請執行下列步驟︰

1.  請先完成[設定混合式 MDM](setup-hybrid-mdm.md) 中的必要條件和程序，之後再為任何平台設定註冊。  
2.  在 Configuration Manager 主控台的 [系統管理] 工作區中，依序移至 [概觀] > [雲端服務] > [Microsoft Intune 訂閱]。  
3.  在功能區中，按一下 [設定平台]，然後針對 Windows 電腦和膝上型電腦
    - 選取 Windows 平台：[Windows]，然後執行下列步驟︰
      1. 在 [一般]  索引標籤中，按一下 [Enable Windows enrollment] (啟用 Windows 註冊) 核取方塊。
      2. 如果您使用憑證以進行程式碼簽署和部署公司入口網站應用程式的話，請瀏覽至**程式碼簽署憑證**。 裝置的使用者也可以從 Windows 市集安裝公司入口網站應用程式，或著您也可以從商務用 Windows 市集部署應用程式，而不需要程式碼簽署。
      3. 您也可以設定 [Windows Hello 企業版設定](windows-hello-for-business-settings.md)。
    - 為 Windows phone 和平板電腦使用 **Windows Phone** 設定，然後執行下列步驟︰
      1. 在 [一般] 索引標籤中，按一下 [Windows Phone 8.1 and Windows 10 Mobile] (Windows Phone 8.1 和 Windows 10 行動裝置版) 核取方塊。 已不再支援 Windows Phone 8.0。
      2. 如果您的組織需要側載公司應用程式，您可以上傳所需的權杖或檔案。 如需側載應用程式的詳細資訊，請參閱[建立 Windows 應用程式](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications)。
        - **應用程式註冊權杖**
        - **.pfx 檔案**
        - **無**如果您使用 Symantec 憑證，您可以指定 [Show an alert before Symantec certificates expire] (在 Symantec 憑證過期前顯示警示)。
4. 按一下 [確定]  關閉對話方塊。  若要使用公司入口網站簡化註冊程序，您應該為裝置註冊建立 DNS 別名。 您接著就可以告訴使用者如何註冊其裝置。

### <a name="create-dns-alias-for-device-enrollment"></a>建立裝置註冊的 DNS 別名  
DNS 別名 (CNAME 記錄類型) 可讓使用者連線至服務來輕鬆註冊其裝置，而不需要使用者輸入伺服器位址。 若要建立 DNS 別名 (CNAME 記錄類型)，您必須在您公司的 DNS 記錄中設定 CNAME，使傳送到您公司網域中 URL 的要求會重新導向至 Microsoft 的雲端服務伺服器。  例如，假設您公司的網域為 contoso.com，您應該在 DNS 中建立 CNAME，其會將 EnterpriseEnrollment.contoso.com 重新導向到 EnterpriseEnrollment-s.manage.microsoft.com。  

 雖然建立 CNAME DNS 項目並非必要，但 CNAME 記錄可以方便使用者進行註冊。 若找不到任何 CNAME 記錄，將會提示使用者手動輸入 MDM 伺服器名稱 enrollment.manage.microsoft.com。

|類型|主機名稱|指向|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 小時|

如果您有多個 UPN 尾碼，您需要為每個網域名稱建立一個 CNAME，並將其一一指向至 EnterpriseEnrollment-s.manage.microsoft.com。 例如，如果 Contoso 上的使用者使用 name@contoso.com，但也使用 name@us.contoso.com 和 name@eu.constoso.com 作為他們的電子郵件/UPN，Contoso DNS 系統管理員就必須建立下列 CNAME。

|類型|主機名稱|指向|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 小時|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 小時|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 小時|

## <a name="tell-users-how-to-enroll-devices"></a>告知使用者如何註冊裝置  

 設定好之後，您需要讓使用者了解如何註冊其裝置。 請參閱 [What to tell users about enrolling their devices](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) (如何指導使用者註冊其裝置)。 您可以將使用者導向 [Enroll your Windows device in Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows) (將您的 Windows 裝置註冊到 Intune)。 這項資訊適用於透過 Microsoft Intune 與 Configuration Manager 管理的行動裝置。

> [!div class="button"]
[< 上一個步驟](create-service-connection-point.md)  [下一個步驟 >](set-up-additional-management.md)

