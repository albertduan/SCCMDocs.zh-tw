---
title: "設定混合式 MDM | System Center Configuration Manager 和 Microsoft Intune"
description: "使用 Configuration Manager 和 Intune 設定混合式裝置註冊。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 44c0947fcb7abdc4369fe0b4f47409b49d068861

---

# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 設定混合式行動裝置管理 (MDM)

*適用於：System Center Configuration Manager (最新分支)*


必須先向 Intune 註冊 iOS、Windows 和 Android 裝置，才能使用 Configuration Manager 管理它們。 使用下列步驟，以搭配使用 Configuration Manager 與 Intune 來設定混合式裝置註冊。 完成下列步驟，即可啟用使用者的「自備裝置 (BYOD)」註冊。 這些步驟也是[註冊公司所擁有的裝置](enroll-company-owned-devices.md)的必要條件。

 |步驟|詳細資料|  
 |-----------|-------------|  
 |**步驟 1：**[建立 MDM 集合](#step-1-create-an-mdm-collection)|建立可註冊其裝置之使用者的 Configuration Manager 使用者集合|  
 |**步驟 2：**[網域名稱需求](#step-2-domain-name-requirements)|確認您組織的網域名稱服務 (DNS) 和 Active Directory 使用者管理符合 MDM 需求|
 |**步驟 3：**[設定 Intune 訂閱](#step-3-configure-intune-subscription)|Intune 服務可讓您透過網際網路管理裝置。|  
 |**步驟 4：**[新增條款和條件](#step-4-add-terms-and-conditions)| 建立使用者必須在使用公司入口網站應用程式之前接受的條款和條件|
 |**步驟 5：**[建立服務連接點](#step-5-create-service-connection-point)|服務連接點會將設定和軟體部署資訊傳送至 Configuration Manager，並從行動裝置擷取狀態和清查訊息。 |  
 |**步驟 6：**[啟用平台註冊](#step-6-enable-platform-enrollment)|適用於 [iOS](#ios-and-mac-enrollment-setup) 和 [Windows](#windows-enrollment-setup) 裝置的 MDM 註冊需要額外的步驟，才能進行服務與裝置之間的通訊。 Android 不需要額外進行設定。|  
 |**步驟 7：**[設定額外的管理](#step-7-set-up-additional-management)|(選擇性) 設定已註冊裝置的設定項目和條件式存取|
 |**步驟 8：**[確認 MDM 設定](#step-8-verify-mdm-configuration)|檢視記錄檔，確認已成功建立服務連接點，而且使用者帳戶正在進行同步處理。|
 |**步驟 9：**[註冊裝置](#step-9-enroll-devices)|告訴使用者如何註冊其裝置，或開始註冊公司所擁有的裝置，以符合組織需求|

在不使用 Configuration Manager 的情況下尋找 Intune？
> [!div class="button"]
[檢視 Intune 文件 >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)

## <a name="step-1-create-an-mdm-collection"></a>步驟 1：建立 MDM 集合
您需要有 Configuration Manager 使用者集合，以指定可將裝置註冊至管理的使用者。 因為 Intune 授權是指派給使用者，所以目標只能是使用者集合。 基於測試，您可以設定**直接規則**，並新增可註冊裝置的特定使用者。 在 Configuration Manager 主控台中，選擇 [資產與相容性] > [使用者集合]，並按一下 [首頁] 索引標籤 > [建立] 群組，然後按一下 [建立使用者集合]。 針對更廣泛的發佈，您應該使用 [查詢規則] 來定義使用者。 如需集合的詳細資訊，請參閱[如何建立集合](https://technet.microsoft.com/library/mt629371.aspx)。

![建立 MDM 的使用者集合](../media/mdm-create-user-collection.png)

## <a name="step-2-domain-name-requirements"></a>步驟 2：網域名稱需求

如有必要，請採取下列步驟來滿足 Configuration Manager 外部的任何相依性：

1. 每位使用者都必須要有指派來註冊裝置的 Intune 授權。 若要建立 Intune 授權與使用者的關聯，每位使用者都必須要有可公開解析的使用者主要名稱 (UPN) (例如 johndoe@contoso.com) 或 Azure Active Directory 中設定的替代登入 ID。 例如，設定替代登入識別碼可讓使用者使用電子郵件地址登入，即使其 UPN 的格式為 NetBIOS 也是一樣 (例如，CONTOSO\johndoe)。

  - 如果公司使用可公開解析的 UPN (即 johndoe@contoso.com),，就不需要進行後續設定。
  - 如果公司使用無法解析的 UPN (即 CONTOSO\johndoe)，則您必須[在 Azure Active Directory 中設定替代識別碼](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync)。

2.  部署和設定 Active Directory Federation Services (AD FS)。 (選用)

     當您設定單一登入時，您的使用者可使用其公司認證登入，以存取 Intune 中的服務。

     如需詳細資訊，請參閱下列主題：
    -   [準備進行單一登入](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [規劃及部署 AD FS 2.0 以搭配使用單一登入](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  部署及設定目錄同步處理。

     目錄同步處理可讓您在 Intune 中填入同步處理的使用者帳戶。 同步處理的使用者帳戶和安全性群組會新增至 Intune。 無法註冊目錄同步作業是使用 Microsoft Intune 設定 Configuration Manager MDM 時，無法註冊裝置的一個常見原因。

     如需詳細資訊，請參閱 Active Directory 文件庫中的 [目錄整合](http://go.microsoft.com/fwlink/?LinkID=271120) 。

4.  選擇性但不建議：如果您未使用 Active Directory Federation Services，可重新設定使用者的 Microsoft Online 密碼。

     如果您未使用 AD FS，您必須為每個使用者設定 Microsoft Online 密碼。

## <a name="step-3-configure-intune-subscription"></a>步驟 3：設定 Intune 訂閱
 Intune 訂閱可讓您透過網際網路管理裝置。 這包含指定哪些使用者集合可以註冊裝置，以及定義要向使用者呈現的資訊。 Intune 訂閱會執行下列動作：

-   擷取服務連線點所需的憑證，以連線至 Intune 服務
-   定義可讓使用者註冊行動裝置的使用者集合
-   定義及設定您要支援的行動平台

> [!IMPORTANT]
>  在 Configuration Manager 中建立 Microsoft Intune 訂閱會讓您的站台服務連接點進入「線上模式」。 請參閱[關於 System Center Configuration Manager 中的服務連線點](../../core/servers/deploy/configure/about-the-service-connection-point.md)。

### <a name="to-create-the-microsoft-intune-subscription"></a>建立 Windows Intune 訂閱

1.  如果您還沒有這麼做，可在 [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216) 上註冊 Microsoft Intune 帳戶。  建立 Intune 帳戶之後，就不需要將任何使用者新增至 Intune 帳戶，或執行其他設定。

2.  在 Configuration Manager 主控台中，按一下 [系統管理] 。

3.  在 **[系統管理]** 工作區中，展開 **[雲端服務]**，然後按一下 **[Microsoft Intune 訂閱]**(搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理新功能)。 在 [首頁]  索引標籤上按一下 [新增 Microsoft Intune 訂閱] 。

![建立 Intune 訂閱](../media/mdm-set-intune.png)

4.  在 [建立 Microsoft Intune 訂閱精靈] 的 [簡介]  頁面檢閱文字，然後按 [下一步] 。

5.  在 [訂閱]  頁面上按一下 [登入]  ，並使用您的工作或學校帳戶登入。 在 [設定行動裝置管理授權單位] 對話方塊中，選取只透過 Configuration Manager 主控台使用 Configuration Manager 管理行動裝置的核取方塊。 若要繼續訂閱，您必須選取此選項。

    > [!IMPORTANT]
    >  一旦將 Configuration Manager 選取為您的管理授權單位，日後您就無法將管理授權單位變更為 Microsoft Intune。

6.  按一下隱私權連結以檢閱其內容，然後按 [下一步] 。

7.  在 [一般]  頁面指定下列選項，然後按 [下一步] 。

  -   **集合**：指定包含將註冊其行動裝置之使用者的使用者集合。

      > [!NOTE]
      >  如果從集合中移除使用者，則從使用者資料庫中移除使用者記錄時，使用者的裝置將會繼續受到管理達 24 小時。

  -   **公司名稱**：指定您的公司名稱。

  -   **公司隱私權文件的 URL**：如果您將公司隱私權資訊發佈至可從網際網路存取的連結，請提供使用者可以從公司入口網站存取的連結，例如 http://www.contoso.com/CP_privacy.html。 隱私權資訊可釐清使用者與您的公司共用哪些資訊。

  -   **公司入口網站的色彩配置**：您可以選擇變更公司入口網站預設的藍色色彩。

  -   **Configuration Manager 網站碼**：指定主要網站的網站碼，以管理行動裝置。

    > [!NOTE]
    >  變更網站碼只會影響新的註冊項目，不會影響現有已註冊的裝置。

8.  在 [公司連絡資訊] 頁面上，於公司入口網站應用程式的 [連絡 IT] (Contact IT) 下指定向使用者顯示的公司連絡資訊。 提供您公司的連絡資訊，然後按一下 [下一步]。

9. 在 [公司標誌] 頁面上，您可以選擇是否要在公司入口網站中顯示標誌，然後按一下 [下一步]。

10. 完成精靈。

## <a name="step-4-add-terms-and-conditions"></a>步驟 4：新增條款和條件
 一旦您設定行動裝置的 Intune 管理，便建立 [條款及條件] 。 使用條款與條件向使用者說明他們註冊裝置時會發生什麼事。 使用者必須接受這些條款和條件，才能註冊裝置。 在 Configuration Manager 主控台中，移至 [資產與相容性] > [概觀] > [相容性設定] > [條款及條件]，然後按一下 [建立條款及條件]。 請參閱 [System Center Configuration Manager 中的條款和條件](terms-and-conditions.md)。

##  <a name="step-5-create-service-connection-point"></a>步驟 5：建立服務連接點
建立訂閱後，您就可以安裝服務連線點站台系統角色，該角色可讓您連線至 Intune 服務。 這個站台系統角色會將設定和應用程式推送到 Intune 服務。

 服務連接點會將設定和軟體部署資訊傳送至 Configuration Manager，並從行動裝置擷取狀態和清查訊息。 Configuration Manager 服務是與行動裝置進行通訊，以及儲存設定的閘道。

> [!NOTE]
>  服務連線點站台系統角色只能安裝在管理中心網站或獨立主要站台上。 服務連接點必須能夠存取網際網路。


### <a name="configure-the-service-connection-point-role"></a>設定服務連接點角色

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。

2.  在 [系統管理] 工作區中，展開 [站台]，然後按一下 [伺服器和站台系統角色]。

3.  使用關聯步驟，將 [服務連線點]  角色新增至新的或現有的站台系統伺服器：

    -   新增站台系統伺服器：在 [首頁]  索引標籤的 [建立]  群組中按一下 [建立站台系統伺服器]  ，啟動 [建立站台系統伺服器精靈]。

    -   現有的站台系統伺服器：按一下您要安裝服務連線點角色的伺服器。 在 [首頁]  索引標籤的 [伺服器]  群組中按一下 [新增網站系統角色]  ，啟動 [新增網站系統角色精靈]。

4.  在 [系統角色選取]  頁面選取 [服務連線點] ，然後按一下 [下一步] 。

![建立服務連接點](../media/mdm-service-connection-point.png)

5.  完成精靈。

### <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>請問服務連線點要如何向 Microsoft Intune 服務驗證？
 服務連接點會對透過網際網路管理行動裝置的雲端 Intune 服務建立連線，藉此擴充 Configuration Manager。 服務連接點使用 Intune 服務來驗證，如下所示：

1.  當您在 Configuration Manager 主控台建立 Intune 訂閱時，會連線到 Azure Active Directory 以驗證 Configuration Manager 系統管理員，其會重新導向至個別的 ADFS 伺服器，以提示輸入使用者名稱和密碼。 然後 Intune 會將憑證發行至租用戶。

2.  步驟 1 中的憑證安裝在服務連線點站台角色上，用來驗證和授權所有其他與 Microsoft Intune 服務的通訊。

## <a name="step-6-enable-platform-enrollment"></a>步驟 6：啟用平台註冊
  不同的裝置平台需要額外的設定，才能啟用裝置註冊︰
  - [iOS 和 Mac 註冊設定](#ios-and-mac-enrollment-setup)：取得 Apple MDM Push 憑證
  - [Windows 註冊設定](#windows-enrollment-setup)︰設定 DNS，並啟用 Windows 電腦、Windows 10 行動裝置版和 Windows Phone 裝置的註冊
  - Android：Android 裝置不需要任何額外的步驟即可啟用註冊


### <a name="ios-and-mac-enrollment-setup"></a>iOS 和 Mac 註冊設定
  下列步驟將 Apple MDM Push 憑證上傳至 Intune 服務，以啟用 Apple 裝置的管理。

  1.  **下載憑證簽署要求** - 需有憑證簽署要求檔案 (.csr) 才能向 Apple 要求 APNs 憑證。  

      1.  在 Configuration Manager 主控台的 **[系統管理]** 工作區中，移至 **[雲端服務]**> **[Microsoft Intune 訂閱]**。  

      2.  在 [首頁]  索引標籤上，按一下 [建立 APNs 憑證要求] 。 [要求 Apple Push Notification Service 憑證簽署要求]  對話方塊隨即開啟。  

      3.  **瀏覽** 至儲存新的憑證簽署要求 (.csr) 檔案的路徑。 在本機儲存憑證簽署要求 (.csr) 檔案。  

      4.  按一下 [下載] 。 下載新的 Microsoft Intune .csr 檔案，並由 Configuration Manager 儲存。 .csr 檔案用來向 Apple Push Certificates Portal 要求信任關係憑證。  

  2.  **申請 Apple 的 APNs 憑證** - Apple Push Notification Service (APNs) 憑證用以建立管理服務、Intune 和已註冊的 iOS 行動裝置間的信任關係。  

      1.  在瀏覽器中連線至 [Apple Push Certificates 入口網站](http://go.microsoft.com/fwlink/?LinkId=269844) ，並使用您的公司 Apple ID 登入。 未來必須使用這個 Apple ID 來更新 APNs 憑證。  

      2.  使用憑證簽署要求 (.csr) 檔案完成精靈。 下載 APNs 憑證並在本機儲存 .pem 檔案。 這個 APNs 憑證 (.pem) 檔案用來建立 Apple Push Notification 伺服器與 Intune 的行動裝置管理授權單位之間的信任關係。  

  3.  **啟用註冊並上傳 APNs 憑證** - 啟用 iOS 註冊及上傳 APNs 憑證。  

      1.  在 Configuration Manager 主控台的 **[系統管理]** 工作區中，移至 **[雲端服務]** > **[Microsoft Intune 訂閱]**。  

      2.  在 **[訂閱]** 群組的 **[首頁]** 索引標籤中，按一下 **[設定平台]** > **[iOS]**。  

          > [!NOTE]  
          >  除非已在 Configuration Manager 主控台中啟用 iOS 註冊，否則請不要上傳 Apple Push Notification service (APNs) 憑證。  

      3.  在 [Microsoft Intune 訂閱內容]  對話方塊中，選取 [iOS]  索引標籤並按一下選取 [啟用 iOS 註冊]  核取方塊。  

      4.  按一下 [瀏覽] ，然後移至從 Apple 下載的 APNs 憑證 (.cer) 檔案。 Configuration Manager 顯示 APNs 憑證的資訊。 按一下 [確定]  將 APN 憑證儲存到 Intune。    


[iOS 和 Mac 註冊](enroll-hybrid-ios-mac.md)的其他資訊。

### <a name="windows-enrollment-setup"></a>Windows 註冊設定  
您可以搭配使用 Configuration Manager 與 Intune，將執行 Windows 的桌上型電腦、膝上型電腦及其他裝置當成行動裝置來管理。 您也可以將 Windows 10 裝置設定為[在加入 Azure Active Directory 時自動註冊](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/enroll-hybrid-windows#azure-active-directory-enrollment)，方法是在其裝置上新增公司或學校帳戶。

DNS 別名 (CNAME 記錄類型) 會在裝置註冊期間自動填入伺服器名稱，以便使用者能夠更輕鬆地註冊其裝置。 您接著可以啟用 Windows 電腦行動裝置的註冊。  

1. 在 Configuration Manager 主控台的 [系統管理] 工作區中，移至 [雲端服務] > [Microsoft Intune 訂閱]，然後執行下列動作︰  
  - **Windows 電腦：**在 [首頁] 索引標籤上，按一下 [設定平台]，然後按一下 [Windows]。 在 [一般]  索引標籤上，選取 [啟用 Windows 註冊] 。  
  - **Windows 10 行動裝置和 Windows Phone：**在 [首頁] 索引標籤上，按一下 [設定平台]，然後按一下 [Windows Phone]。  在 **[一般]** 索引標籤上，選擇  **[Windows Phone 8.1 和 Windows 10 行動裝置版]**。

2.  您也可以設定 Configuration Manager，使用公司入口網站應用程式來簡化註冊。
(選擇性) 在公司的 DNS 記錄中建立 DNS 別名 (CNAME 記錄類型)，讓傳送到您公司網域中之 URL 的要求重新導向至 Microsoft 的雲端服務伺服器。  例如，假設您公司的網域為 contoso.com，您應該在 DNS 中建立 CNAME，其會將 EnterpriseEnrollment.contoso.com 重新導向到 EnterpriseEnrollment-s.manage.microsoft.com。  

|類型|主機名稱|指向|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  

如需其他資訊，請參閱 [Windows 註冊](enroll-hybrid-windows.md)。

### <a name="android-enrollment-setup"></a>Android 註冊設定
您可以搭配使用 Configuration Manager 與 Intune，來管理執行 Android 的電話和平板電腦。
1.  在 Configuration Manager 主控台的 **[系統管理]** 工作區中，移至 **[雲端服務]** > **[Microsoft Intune 訂閱]**。  

2.  在 **[首頁]** 索引標籤的 **[訂閱]** 群組中，按一下 **[設定平台]** > **[Android]**。  

3.  在 [Microsoft Intune 訂閱內容]  對話方塊中，選取 [Android]  索引標籤並按一下選取 [啟用 Android 註冊]  核取方塊。

如需其他資訊，請參閱 [Android](enroll-hybrid-android.md)。

## <a name="step-7-set-up-additional-management"></a>步驟 7：設定額外的管理
(選擇性) 註冊裝置之前，您可以設定額外的管理。 在註冊裝置之後，即可建立和部署這些管理解決方案，雖然許多組織都想要在管理裝置時部署裝置。

**設定項目**可讓您管理設定，例如，根據裝置平台，可能需要 PIN 或需要加密註冊裝置︰
- [Windows 10 和 Windows 8.1 裝置](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)
- [Windows Phone 裝置](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client)
- [iOS 和 Mac 裝置](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)
- [Android 和 Samsung KNOX 裝置](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)

**應用程式**可以部署至受管理裝置：
- [iOS 應用程式](/sccm/apps/get-started/creating-ios-applications)
- [Mac 應用程式](/sccm/apps/get-started/creating-mac-computer-applications)
- [Windows PC 應用程式](/sccm/apps/get-started/creating-windows-applications)
- [Windows Phone 應用程式](/sccm/apps/get-started/creating-windows-phone-applications)
- [Android 應用程式](/sccm/apps/get-started/creating-android-applications)

**條件式存取**可讓您管理對公司資源的存取，包含：  
- [電子郵件存取](/sccm/protect/deploy-use/manage-email-access)
- [SharePoint 存取](/sccm/protect/deploy-use/manage-sharepoint-online-access)
- [商務用 Skype 存取](/sccm/protect/deploy-use/manage-skype-for-business-online-access)
- [Dynamic CRM Online](/sccm/protect/deploy-use/manage-dynamics-crm-online-access)

## <a name="step-8-verify-mdm-configuration"></a>步驟 8：確認 MDM 設定

 您可以藉由檢查下列記錄檔來確認特定的裝置管理元件︰

-   檢查 Cloudusersync.log 確認使用者帳戶已順利同步處理。

-   檢查 Sitecomp.log 確認已順利建立服務連線點。

## <a name="step-9-enroll-devices"></a>步驟 9：註冊裝置
現在已經完成混合式設定。 有數種方式可以在 Configuration Manager 中註冊裝置︰
- 自備裝置 (BYOD)：[通知使用者如何註冊其裝置](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) - Intune 和 Hybrid 所管理之裝置的註冊指導方針相同
- 公司擁有的裝置 (COD)：[註冊公司擁有的裝置](enroll-company-owned-devices.md)提供註冊公司所擁有裝置之不同平台特有方式的指引。

### <a name="managing-intune-subscriptions-associated-with-configuration-manager"></a>管理與 Configuration Manager 相關聯的 Intune 訂閱
 如果您將 Microsoft Intune (試用訂閱或付費訂閱) 新增至 Configuration Manager，但之後需要切換至不同的 Intune 訂閱，則必須先從 Configuration Manager 主控台刪除 **Microsoft Intune 訂閱**和**服務連接點**，才能新增訂閱。

#### <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>如何從 Configuration Manager 刪除 Intune 訂閱

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。

2.  在 **[系統管理]** 工作區中，展開 **[概觀]**，移至 **[雲端服務]**，然後按一下 **[Microsoft Intune 訂閱]**。

3.  以滑鼠右鍵按一下 **[Microsoft Intune 訂閱]** ，然後按一下 **[刪除]**。 **Microsoft Intune 訂閱**。

    > [!IMPORTANT]
    >  包括使用者註冊、原則，以及針對 Intune 評估訂閱所設定的應用程式部署在內的所有內容都將遺失。

4.  在 **[系統管理]** 工作區中，展開 **[概觀]**，移至 **[站台設定]**，然後選取 **[伺服器和站台系統角色]**。

5.  選取裝載 **服務連接點** 角色的伺服器。

6.  在 **[站台系統角色]** 清單中，選取 **[服務連接點]** ，然後按一下功能區中的 **[移除角色]** 。 確認您想要移除該角色。 隨即會刪除該服務連接點。

7.  您現在可以建立新的服務連接點、將新的 Intune 訂閱加入至 Configuration Manager，然後將 Configuration Manager 設定為 MDM 授權單位。



<!--HONumber=Nov16_HO1-->


