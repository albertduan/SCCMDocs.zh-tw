---
title: "管理受管理電腦的 O365 服務存取權 | Microsoft Docs"
description: "了解如何針對 System Center Configuration Manager 管理的電腦設定條件式存取。"
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccdb424a-b603-4ccc-af36-558924248022
caps.latest.revision: 15
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: da5fcd65d7af8d73aa23f4a7d96cd8fc6e48f9dc


---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>管理 System Center Configuration Manager 所管理之電腦對 O365 服務的存取

適用於：System Center Configuration Manager (最新分支)



 從 Configuration Manager 1602 版開始，您可以針對 System Center Configuration Manager 管理的電腦設定條件式存取。  

> [!IMPORTANT]  
>  這是 1602、1606 和 1610 更新版所提供的發行前版本功能。 發行前版本功能會包含在產品內，以便在生產環境中進行早期測試，但不應視為生產環境就緒。 如需詳細資訊，請參閱[使用發行前版本功能](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)。
> - 安裝 1602 更新版之後，功能類型會顯示為已發行，不過這是發行前功能。
> - 如果您接著從 1602 更新至 1606，功能類型會顯示為已發行，不過這仍是發行前功能。
> - 如果您從 1511 版直接更新至 1606，功能類型會顯示為發行前版本。

 如果您正在尋找如何針對 Intune 所註冊和管理的裝置，或者已加入網域但未評估其相容性的電腦，對其設定條件式存取的資訊，請參閱[管理 System Center Configuration Manager 中的服務存取權](../../protect/deploy-use/manage-access-to-services.md)。  


## <a name="supported-services"></a>支援的服務  

-   Exchange Online  

-   SharePoint Online  

## <a name="supported-pcs"></a>支援的電腦  

-   Windows 7  

-   Windows 8.1  

-   尚未完全支援 Windows 10。  如果您嘗試設定 Windows 10 電腦的條件式存取，您可能會遇到一些問題。  如需詳細資訊，請參閱 [已知問題](#bkmk_KnownIssues) 。  

## <a name="configure-conditional-access"></a>設定條件式存取  
 若要設定條件式存取，您必須先建立相容性原則，並設定條件式存取原則。 當您設定電腦的條件式存取原則時，可以要求電腦必須符合相容性原則，才能存取 Exchange Online 和 SharePoint Online 服務。  

### <a name="prerequisites"></a>先決條件  

-   ADFS 同步處理以及 O365 訂閱。 O365 訂閱可用於設定 Exchange Online 和 SharePoint Online。  

-   Microsoft Intune 訂閱。 應該在 Configuration Manager 主控台中設定 Microsoft Intune 訂閱。 這仍會要求您處於混合式部署中。  

 電腦必須符合下列需求：  

-   自動向 Azure Active Directory 註冊裝置的[必要條件](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)   

     您可以透過相容性原則向 Azure AD 電腦註冊。  

    -   對於 Windows 8.1 和 Windows 10 電腦，您可以使用 Active Directory 群組原則，將裝置設定為自動向 Azure AD 註冊。  

    -   o   針對 Windows 7 電腦，您必須透過 System Center Configuration Manager 裝置，將裝置註冊軟體套件部署到 Windows 7 電腦。 [自動向 Azure Active Directory 註冊加入網域的 Windows 裝置](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)主題會提供更多詳細資料。  

-   必須使用已 [啟用](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)新式驗證的 Office 2013 或 Office 2016。  

 如下所述的步驟適用於 Exchange Online 和 SharePoint Online  

### <a name="step-1-configure-compliance-policy"></a>步驟 1： 設定相容性原則  
 在 Configuration Manager 主控台中，使用下列規則建立相容性原則︰  

-   需要在 Azure Active Directory 中註冊：這個規則會確認使用者的裝置是否為已加入 Azure AD 的工作區，如果不是，則會在 Azure AD 中自動註冊裝置。 在 Windows 8.1 上才支援自動註冊。 在 Windows 7 電腦上，部署 MSI 以執行自動註冊。 如需詳細資訊，請參閱 [自動向 Azure Active Directory 註冊裝置](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)  

-   **所有期限超過特定天數的已安裝必要更新：**這個規則會確認使用者的裝置在您指定的期限和寬限期內是否具有所有必要更新 (在必要的自動更新規則中指定)，並會自動安裝任何擱置的必要更新。  

-   **需要 BitLocker 磁碟機加密：**這會確認裝置上的主要磁碟機 (例如 C:\\) 是否為 BitLocker 加密。 如果未在主要裝置上啟用 BitLocker 加密，則會封鎖存取電子郵件和 SharePoint 服務。  

-   **需要反惡意程式碼：**這會確認是否已啟用並執行反惡意程式碼軟體 (僅限 System Center Endpoint Protection 或 Windows Defender)。 如果未啟用，則會封鎖存取電子郵件和 SharePoint 服務。  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>步驟 2： 評估條件式存取的效果  
 執行條件式存取相容性報告。 您可以在 [報告] > [相容性和設定管理] 下方的 [監視] 區段中找到此報告。 這會顯示所有裝置的相容性狀態。  報告為不相容的裝置將遭到封鎖而無法存取 Exchange Online 和 SharePoint Online。  

 ![CA&#95;相容性&#95;報告](../media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>設定 Active Directory 安全性群組  
 您可以根據原則類型，將條件式存取原則的目標設為使用者群組。 這些群組包含將成為原則目標的使用者，或是免套用此原則的使用者。 當使用者成為原則的目標時，他們使用的每個裝置都必須相容，才能存取服務。  

 Active Directory 安全性使用者群組。 這些使用者群組應該同步處理至 Azure Active Directory。 您也可以在 Office 365 系統管理中心或 Intune 帳戶入口網站中設定這些群組。  

 您可以在每個原則中指定兩種群組類型。 :  

-   **目標群組** - 套用原則的使用者群組。 您應針對合規性和條件式存取原則使用相同的群組。  

-   **免套用的群組** - 免套用原則的使用者群組 (選擇性)  
    如果使用者隸屬於這兩個群組，他們將免套用原則。  

     系統只會評估條件式存取原則設定為目標的群組。  

### <a name="step-3--create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>步驟 3：  建立 Exchange Online 和 SharePoint Online 的條件式存取原則  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  若要建立 Exchange Online 原則，請選取 **[啟用 Exchange Online 的條件式存取原則]**。  

     若要建立 SharePoint Online 原則，請選取 **[啟用 Exchange Online 的條件式存取原則]**。  

3.  在 [常用]  索引標籤的 [連結]  群組中，按一下 [在 Intune 主控台中設定條件存取原則] 。 您可能需要提供用來連線 Configuration Manager 與 Intune 的帳戶使用者名稱和密碼。  

     Intune 管理主控台隨即開啟。  

4.  針對 Exchange Online，在 Microsoft Intune 管理主控台中，按一下 [原則] > [條件式存取] > [Exchange Online 原則]。  

     針對 SharePoint Online，在 Microsoft Intune 管理主控台中，按一下 [原則] > [條件式存取] > [SharePoint Online 原則]。  

5.  將 Windows 電腦需求設定為**[裝置必須符合規定]**選項。  

6.  按一下 [目標群組] 下方的 [修改]  ，選取要套用原則的 Azure Active Directory 安全性群組。  

    > [!NOTE]  
    >  部署合規性政策和條件式存取原則的 [目標群組] 時，應使用相同的安全性使用者群組。  

     按一下 [豁免群組] 下方的 [修改]  ，選取豁免此原則的 Azure Active Directory 安全性群組。  

7.  按一下 **[儲存]** 來建立並儲存原則  

 因不相容而遭到封鎖的使用者將可在 System Center Configuration Manager 軟體中心檢視相容性資訊，並且將在補救相容性問題時起始新的原則評估。  

##  <a name="a-namebkmkknownissuesa-known-issues"></a><a name="bkmk_KnownIssues"></a> 已知問題  
 使用此功能時，您可能會看到下列問題︰  

-   在這個 1602 更新中，不會強制執行 5 天的相容性。 即使使用者裝置上的相容性檢查是在 5 天前發生，使用者仍然可以存取 Office 365 和 SharePoint Online。  

-   當裝置不符合相容性原則時，不會自動顯示原因。 使用者必須移至新的軟體中心來尋找不相容的原因。 原因會顯示於軟體中心的 [裝置相容性] 區段中。  

-   當 Windows 10 使用者嘗試連線到 O365 和/或 SharePoint 線上資源時，可能會看到多個存取失敗。 請注意，條件式存取並未完全支援 Windows 10。  

### <a name="see-also"></a>請參閱  
 [使用 System Center Configuration Manager 保護資料和站台基礎結構](../../protect/understand/protect-data-and-site-infrastructure.md)



<!--HONumber=Dec16_HO3-->


