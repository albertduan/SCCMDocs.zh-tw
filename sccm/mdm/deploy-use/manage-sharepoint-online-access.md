---
title: "管理 SharePoint Online 存取 | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager SharePoint Online 的條件式存取原則，以管理 OneDrive 存取權。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
caps.latest.revision: 11
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 58a82b29743cb37a5d358f020cf11b91d6f6f42e
ms.contentlocale: zh-tw
ms.lasthandoff: 03/06/2017


---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理 SharePoint Online 存取

*適用於：System Center Configuration Manager (最新分支)*


您可以使用 System Center Configuration Manager **SharePoint Online** 條件式存取原則，根據指定的條件，來管理位於 SharePoint Online 之商務用 OneDrive 檔案的存取權。
您可以針對上述平台從下列應用程式中，控制對 SharePoint Online 的存取：  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android 和 iOS)  

-   Microsoft Word (Android 和 iOS)  

-   Microsoft Excel (Android 和 iOS)  

-   Microsoft PowerPoint (Android 和 iOS)  

-   Microsoft OneNote (Android 和 iOS)

Office 傳統型應用程式可以在執行下列項目的電腦上存取 SharePoint Online：  

-   啟用[新式驗證](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) 的 Office 2013 傳統型應用程式和更新版本。  

-   Windows 7.0 或 Windows 8.1  

> [!NOTE]  
>  電腦應該要已加入網域或符合在 Intune 中設定的原則。  



 當目標使用者使用其裝置上支援的應用程式 (例如 OneDrive) 嘗試連接到檔案時，就會出現下列評估：  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 若要連接到所需檔案，執行 OneDrive 的裝置必須：  

-   已向 Microsoft Intune 註冊或屬於已加入網域的電腦。  

-   在 Azure Active Directory 中登錄裝置 (這會在向 Intune 註冊裝置時自動發生)。  

     已加入網域的電腦必須設定為以 Azure Active Directory [自動登錄](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/)。  

-   符合所有已部署的 Configuration Manager 合規性原則  

 裝置狀態儲存在 Azure Active Directory，它會根據您指定的條件，授與或封鎖檔案的存取權。  

 如不符合條件，使用者會在登入時看見下列訊息之一：  

-   如果裝置未註冊 Intune，或未在 Azure Active Directory 中登錄，就會顯示訊息，指示如何安裝及註冊公司入口網站應用程式。  

-   如果裝置不符合規範，即會顯示一則訊息，將使用者引導至 Intune 入口網站，讓他們能夠在該處找到問題的相關資訊，以及如何修復問題的方法。  

- 對於行動裝置：

  您可以在使用 **iOS** 和 **Android** 裝置的瀏覽器時，限制存取 SharePoint Online。  如此，即只能從下列相容裝置的支援瀏覽器上進行存取︰
* Safari (iOS)
* Chrome (Android)
* 受管理的瀏覽器 (iOS 和 Android)

  不支援的瀏覽器將會被封鎖。
-   針對電腦：  


    -   如果原則設定為需要加入網域，而電腦未加入網域，就會顯示連絡 IT 管理員的訊息。  

    -   如果原則設定為需要加入網域或符合規範，但電腦不符合任一要求，即會顯示訊息指示如何安裝及註冊公司入口網站應用程式。  

 您可以從下列應用程式封鎖 SharePoint Online 存取權：  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android 和 iOS)  

-   Microsoft Word (Android 和 iOS)  

-   Microsoft Excel (Android 和 iOS)  

-   Microsoft PowerPoint (Android 和 iOS)  

-   Microsoft OneNote (Android 和 iOS)  

## <a name="configure-conditional-access-for-sharepoint-online"></a>設定 SharePoint Online 的條件式存取  

### <a name="step-1-configure-active-directory-security-groups"></a>步驟 1：設定 Active Directory 安全性群組  
 在開始之前，請先為條件式存取原則設定 Azure Active Directory 安全性群組。 您可以在 **Office 365 系統管理中心**或 **Intune 帳戶入口網站**中設定這些群組。 這些群組包含將成為原則目標的使用者，或是免套用此原則的使用者。 當使用者成為原則的目標時，他們使用的每個裝置都必須符合規範，才能存取資源。  

 您可以在 SharePoint Online 原則中指定兩種群組類型：  

-   **目標群組**â€“ 包含將套用原則的使用者群組  

-   **豁免群組**â€“ 包含豁免原則的使用者群組 (選擇性)  

 如果使用者同時隸屬於這兩個群組，他們將免套用原則。  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>步驟 2：建立及部署合規性原則  
 請確定所有裝置都已建立並部署以 SharePoint Online 原則為目標的合規性原則。  

> [!NOTE]  
>  雖然 Intune 群組或 Configuration Manager 集合部署了合規性原則，但 Azure Active Directory 安全性群組的目標是條件式存取原則。  

 如需如何設定合規性原則的詳細資訊，請參閱 [Configuration Manager 中的合規性原則](../../protect/deploy-use/device-compliance-policies.md)。  

> [!IMPORTANT]  
>  若未部署合規性原則，卻啟用了 SharePoint Online 原則，則允許所有目標裝置存取。  

 當您準備好時，請繼續執行**步驟 3**。  

###  <a name="BKMK_OneDrive"></a> 步驟 3：設定 SharePoint Online 原則  


 接著，設定原則要求只有受管理和符合規範的裝置才可以存取 SharePoint Online。 此原則會儲存在 Azure Active Directory。

 >[!NOTE]
 >您也可以在 Azure AD 管理主控台中建立條件式存取原則。 Azure AD 管理主控台可讓您在其他條件式存取原則 (例如 Multi-Factor Authentication) 之外，建立 Intune 裝置條件式存取原則 (稱為 Azure AD 裝置型條件式存取原則)。 您也可以設定 Azure AD 支援的 Salesforce 和 Box 等協力廠商企業應用程式的條件式存取原則。 如需詳細資訊，請參閱[如何設定 Azure Active Directory 裝置型條件式存取原則來控制對 Azure Active Directory 連線應用程式的存取](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/)。  

1.  在 Configuration Manager 主控台中，按一下 [資產與合規性]。  

2.  選取 [啟用 SharePoint Online 的條件式存取原則]。  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  在適用於 Outlook 和使用新式驗證之應用程式的 [應用程式存取] 下方，您可以選擇僅限符合各平台規範的裝置才有存取權。  

    > [!TIP]  
    >  **新式驗證** 將 Active Directory 驗證庫 (ADAL) 登入整合到 Office 用戶端中。  
    >   
    >  -   ADAL 型驗證可讓 Office 用戶端進行以瀏覽器為基礎的驗證 (又稱為被動驗證)。  系統會將使用者導向登入網頁，以便進行驗證。  
    > -   這個新的登入方法可根據 [裝置合規性] 以及是否執行 [Multi-Factor Authentication] ，來啟用條件式存取等新案例。  
    >   
    >  這篇[文章](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517)包含新式驗證運作方式的更詳細資訊。  

     Windows 電腦必須已加入網域，或向 Intune 註冊並符合其規範。 您可以設定下列要求：  

    -   **裝置必須加入網域或符合規範。** 這表示電腦必須已加入網域或符合 Intune 的原則集合規範。 如果電腦不符合上述任一條件，即會提示使用者向 Intune 註冊裝置。  

    -   **裝置必須已加入網域。** 這表示電腦必須已加入網域才能存取 Exchange Online。 如果電腦未加入網域，則會封鎖存取電子郵件並提示使用者連絡 IT 管理員。  

    -   **裝置必須符合規範。** 這表示電腦必須在 Intune 註冊並符合其規範。 如果電腦未註冊，則會顯示註冊指示訊息。  

4.  在 SharePoint Online 和商務用 OneDrive 的 [瀏覽器存取] 下方，您可以選擇只允許透過下列支援的瀏覽器存取 Exchange Online︰Safari (iOS) 和 Chrome (Android)。 來自其他瀏覽器的存取將會被封鎖。  您針對 OneDrive [應用程式存取] 所選取的相同平台限制也適用於此處。

    在 **Android** 裝置上，使用者必須啟用瀏覽器存取。  若要完成此動作，使用者必須在已註冊的裝置上啟用 [允許瀏覽器存取] 選項，如下所示︰
    1.  啟動**公司入口網站應用程式**。
    2.  透過三個點 (â€¦) 或硬體功能表按鈕，移至 [設定] 頁面。
    3.  按下 [啟用瀏覽器存取] 按鈕。
    4.  在 Chrome 瀏覽器中，登出 Office 365 並重新啟動 Chrome。

    在 **iOS 和 Android** 平台上，Azure Active Directory 會將傳輸層安全性 (TLS) 憑證發行給裝置，以識別用來存取服務的裝置。  裝置會顯示憑證，並包含要使用者選取憑證的提示，如以下螢幕擷取畫面所示。 使用者必須選取此憑證，才能繼續使用瀏覽器。

     **iOS**

     ![iPad 上憑證提示的螢幕擷取畫面](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Android**

      ![Android 裝置上憑證提示的螢幕擷取畫面](media/mdm-browser-ca-android-cert-prompt.png)

4.  在 [常用] 索引標籤的 [連結] 群組中，按一下 [在 Intune 主控台中設定條件存取原則]。 您可能需要提供用來連線 Configuration Manager 與 Intune 的帳戶使用者名稱和密碼。  

     Intune 管理主控台隨即開啟。  

5.  在 [Microsoft Intune 管理主控台](https://manage.microsoft.com)中，按一下 **[原則]** > **[條件式存取]** > **[SharePoint Online 原則]**。  

6.  選取 [若裝置不符合規定，則會讓應用程示不得存取 SharePoint Online]。  

7.  按一下 [目標群組] 下方的 [修改]，以選取要套用原則的 Azure Active Directory 安全性群組。  

8.  按一下 [免套用的群組] 下方的 [修改]，以選取豁免此原則的 Azure Active Directory 安全性群組。  

9. 完成之後，請按一下 [儲存]。  

 您不需部署條件式存取原則，它會立即生效。  

 如需如何從 Intune 主控台監視原則的資訊，請參閱[以 Microsoft Intune 管理 SharePoint Online 存取](https://technet.microsoft.com/library/dn705844.aspx)。  

### <a name="see-also"></a>另請參閱  

 [管理 System Center Configuration Manager 中的服務存取權](../../protect/deploy-use/manage-access-to-services.md)

