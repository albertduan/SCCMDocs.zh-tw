---
title: "設定 Windows 的混合式裝置管理與 System Center Configuration Manager 和 Microsoft Intune"
description: "使用 System Center Configuration Manager 和 Microsoft Intune 設定 Windows 裝置管理。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 55fca210e5b3ce11e513662994105027f1a4f227


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>設定 Windows 的混合式裝置管理與 System Center Configuration Manager 和 Microsoft Intune

*適用於：System Center Configuration Manager (最新分支)*

您可以搭配使用 Configuration Manager 與 Intune，將執行 Windows 的桌上型電腦、膝上型電腦及其他裝置當作行動裝置來管理。 您可以設定 Azure Active Directory，以允許 Windows 電腦的自動註冊。 您也可以設定 Configuration Manager，使用公司入口網站應用程式來簡化註冊。


Windows 註冊選項包括︰

- [使用 Azure AD 的自動註冊](#azure-active-directory-enrollment)
- [Windows 電腦](#set-up-windows-device-enrollment)
- [Windows 10 Mobile 和 Windows Phone 裝置](#enable-windows-phone-devices)

## <a name="azure-active-directory-enrollment"></a>Azure Active Directory 註冊

自動註冊可讓使用者在 Intune 中，新增工作或學校帳戶，並同意進行管理，以註冊公司擁有或個人的 Windows 10 電腦與 Windows 10 行動裝置。 在背景中，使用者的裝置會註冊並加入 Azure Active Directory。 註冊之後，可使用 Intune 來管理裝置。

**先決條件**
- Azure Active Directory Premium 訂閱 ([試用訂閱](http://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune 訂閱


### <a name="configure-automatic-mdm-enrollment"></a>設定自動執行 MDM 註冊

1. 在 [Azure 管理入口網站](https://manage.windowsazure.com) (https://manage.windowsazure.com)，瀏覽至 **Active Directory** 節點，然後選取您的目錄。

2. 按一下 [應用程式] 索引標籤，您應該會在應用程式清單中看到 **Microsoft Intune**。

    ![Azure AD 應用程式與 Microsoft Intune](../media/aad-intune-app.png)

3. 按一下 **Microsoft Intune** 的箭號，您應該會看到一個讓您設定 Microsoft Intune 的頁面。

4. 按一下 [設定] 開始設定向 Microsoft Intune 自動執行 MDM 註冊。

5. 指定 Intune 的 URL：

  - **MDM 註冊 URL** – 使用 `https://enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc` 作為 MDM 註冊 URL。
  - **MDM 條款 URL** – 使用預設值。 註冊裝置時，此 URL 會顯示使用者的使用條款。
  - **MDM 合規性 URL** – 使用預設值。 如果發現裝置不符合要求，會顯示「拒絕存取」的訊息與此 URL。 URL 指向的頁面可以協助使用者了解為何他們的裝置不符合原則，以及如何讓裝置能夠重新恢復合規性。

6.  指定哪些使用者的裝置應該由 Microsoft Intune 管理。 這些使用者的 Windows 10 裝置將會自動註冊，以便使用 Microsoft Intune 管理。

  - **全部**
  - **群組**
  - **無**

7. 選擇 [儲存]。

## <a name="configure-windows-pc-enrollment"></a>設定 Windows PC 註冊
 若要啟用 Windows 行動裝置管理，您要啟用作業系統的管理。  您也可以新增 DNS CNAME，以簡化使用者的註冊。

### <a name="create-dns-alias-for-device-enrollment"></a>建立裝置註冊的 DNS 別名  
 DNS 別名 (CNAME 記錄類型) 會在裝置註冊期間自動填入伺服器名稱，以便使用者能夠更輕鬆地註冊其裝置。 若要建立 DNS 別名 (CNAME 記錄類型)，您必須在您公司的 DNS 記錄中設定 CNAME，使傳送到您公司網域中之 URL 的要求會重新導向至 Microsoft 的雲端服務伺服器。  例如，假設您公司的網域為 contoso.com，您應該在 DNS 中建立 CNAME，其會將 EnterpriseEnrollment.contoso.com 重新導向到 EnterpriseEnrollment-s.manage.microsoft.com。  

|類型|主機名稱|指向|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  
### <a name="to-enable-enrollment-for-windows-devices"></a>啟用 Windows 裝置的註冊  

1.  **必要條件** - 請先完成[設定混合式 MDM](setup-hybrid-mdm.md) 中的必要條件和程序，才能為任何平台設定註冊。  

2.  在 Configuration Manager 主控台的 **[系統管理]** 工作區中，移至 **[雲端服務]** > **[Microsoft Intune 訂閱]**。  

    > [!WARNING]  
    >  如果已開啟其他 Configuration Manager 對話方塊，請關閉它們，然後再繼續此程序。  

3.  在 [首頁]  索引標籤上按一下 [設定平台] ，然後按一下 [Windows] 。  

4.  在 [一般]  索引標籤上，選取 [啟用 Windows 註冊] 。  

 設定好之後，您需要讓使用者了解如何註冊其裝置。 請參閱[要告訴使用者關於註冊其裝置的事項](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 這項資訊適用於透過 Microsoft Intune 與 Configuration Manager 管理的行動裝置。

## <a name="enable-windows-phone-devices"></a>啟用 Windows Phone 裝置  
  如果您的使用者只會註冊 Windows Phone 8.1 及更新的裝置，且您不會將企業營運應用程式部署到 Windows Phone 裝置，則不需要 Symantec 憑證。 啟用 Windows Phone 註冊之後，您應該指示使用者從 Windows Phone 市集安裝公司入口網站應用程式以註冊其裝置。  

  請針對您要管理的 Windows Phone 裝置完成下列步驟。  

### <a name="to-enable-enrollment-for-windows-phone-81-and-later-devices"></a>啟用 Windows Phone 8.1 和更新裝置的註冊  

 1.  **必要條件** - 請先完成[設定混合式 MDM](setup-hybrid-mdm.md) 中的必要條件和程序，才能為任何平台設定註冊。  

 2.  在 Configuration Manager 主控台的 **[系統管理]** 工作區中，移至 **[雲端服務]** > **[Microsoft Intune 訂閱]**。  

     > [!WARNING]  
     >  如果已開啟其他 Configuration Manager 對話方塊，請關閉它們，然後再繼續此程序。  

 3.  在 [首頁]  索引標籤上按一下 [設定平台] ，然後按一下 [Windows Phone] 。  

 4.  在 **[一般]** 索引標籤上，選擇 **[Windows Phone 8.1 和 Windows 10 行動裝置版]**。 您可以上傳 AET .xml 檔案資料或 .pfx 檔案來支援部署公司入口網站，或者指示使用者從 Windows Phone 市集下載公司入口網站。  

      按一下 [ **確定**]。  

  設定好之後，您需要讓使用者了解如何註冊其裝置。 請參閱[要告訴使用者關於註冊其裝置的事項](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 這項資訊適用於透過 Microsoft Intune 與 Configuration Manager 管理的行動裝置。  



<!--HONumber=Nov16_HO1-->


