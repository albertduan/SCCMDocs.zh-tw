---
title: "建立 Wi-Fi 設定檔 | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中使用 Wi-Fi 設定檔，將無線網路設定部署至組織中的使用者。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
caps.latest.revision: 13
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 295ccc2ce7c1dae55c45113cc8ff826e30f7079a


---
# <a name="how-to-create-wi-fi-profiles-in-system-center-configuration-manager"></a>如何建立 System Center Configuration Manager 中的 Wi-Fi 設定檔

*適用於︰System Center Configuration Manager (最新分支)*


在 System Center Configuration Manager 中使用 Wi-Fi 設定檔，將無線網路設定部署至組織中的使用者。 部署這些設定，即可讓使用者更輕鬆地連線至 Wi-Fi。  

 例如，您已安裝名稱為 **Contoso Wi-Fi**的新 Wi-Fi 網路。 您現在想要使用連線至此網路所需的設定來佈建執行 iOS 作業系統的所有裝置。 您可建立 Wi-Fi 設定檔，以包含連線至 **Contoso Wi-Fi** 無線網路所需的設定。 接著，您可以將此設定檔部署至階層中持有 iOS 裝置的所有使用者。 iOS 裝置使用者可在無線網路清單中看見公司網路，並且可直接連線至該網路。  

 您可以使用 Wi-Fi 設定檔設定下列裝置類型：  

-   執行 Windows 8.1 32 位元的裝置  

-   執行 Windows 8.1 64 位元的裝置  

-   執行 Windows RT 8.1 的裝置  

-   執行 Windows Phone 8.1 的裝置  

-   執行 Windows 10 Desktop 或 Windows 10 行動裝置版的裝置  

-   執行 iOS 5、iOS 6、iOS 7 與 iOS 8 的 iPhone 裝置  

-   執行 iOS 5、iOS 6、iOS 7 與 iOS 8 的 iPad 裝置  

-   執行第 4 版的 Android 裝置  

> [!IMPORTANT]  
>  若要將設定檔部署到 Android、iOS、Windows Phone 和已註冊的 Windows 8.1 及更新版本的裝置，必須在 Microsoft Intune 註冊這些裝置。 如需如何註冊裝置的相關資訊，請參閱[在 Intune 中註冊裝置以進行管理](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)。  

 建立 Wi-Fi 設定檔時，您可以加入多種安全性設定。 這些安全性設定包括使用 Configuration Manager 憑證設定檔佈建的伺服器驗證和用戶端驗證憑證。 如需憑證設定檔的詳細資訊，請參閱 [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (System Center Configuration Manager 中的憑證設定檔)。  

## <a name="steps-to-create-a-wi-fi-profile"></a>建立 Wi-fi 設定檔的步驟  
 透過下列必要步驟以使用 [建立 Wi-Fi 設定檔精靈] 來建立 Wi-Fi 設定檔。  

-   [步驟 1：啟動 [建立 Wi-Fi 設定檔精靈]](#BKMK_Step1)  

-   [步驟 2：提供與 Wi-Fi 設定檔有關的一般資訊](#BKMK_Step2)  

-   [步驟 3：提供與無線網路有關的資訊](#BKMK_Step3)  

-   [步驟 4：設定 Wi-Fi 設定檔的安全性](#BKMK_Step4)  

-   [步驟 5：設定 Wi-Fi 設定檔的進階設定](#BKMK_Step5)  

-   [步驟 6：設定 Wi-Fi 設定檔的 Proxy 設定](#BKMK_Step6)  

-   [步驟 7：設定 Wi-Fi 設定檔的支援平台](#BKMK_Step7)  

-   [步驟 8：完成精靈](#BKMK_Step8)  

##  <a name="a-namebkmkstep1a-step-1-start-the-create-wi-fi-profile-wizard"></a><a name="BKMK_Step1"></a> 步驟 1：啟動 [建立 Wi-Fi 設定檔精靈]  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，依序展開 [相容性設定] 、[公司資源存取] ，然後按一下 [Wi-Fi 設定檔] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立 Wi-Fi 設定檔] 。  

##  <a name="a-namebkmkstep2a-step-2-provide-general-information-about-the-wi-fi-profile"></a><a name="BKMK_Step2"></a> 步驟 2：提供 Wi-Fi 設定檔的一般資訊  

1.  在 [建立 Wi-Fi 設定檔精靈] 的 **[一般]** 頁面上，輸入此 Wi-Fi 設定檔唯一的名稱和描述。 您最多可以使用 256 個字元。  

2.  如果您想要使用另一個 Wi-Fi 設定檔的設定，請選取 **[從檔案匯入現有的 Wi-Fi 設定檔項目]**。  

    > [!IMPORTANT]  
    >  請確定您匯入的 Wi-Fi 設定檔包含 Wi-Fi 設定檔的有效 XML。 當您匯入檔案時，Configuration Manager 不會驗證設定檔。  

3.  在  
                            **報告的不相容嚴重性**：指定在發現用戶端裝置上的 Wi-Fi 設定檔不相容時所報告的嚴重性層級 (例如，如果設定檔安裝失敗)。 可用的嚴重性層級如下：  

    -   **無**：不符合這項相容性規則的電腦不會回報 Configuration Manager 報告的失敗嚴重性。  

    -   **資訊**：不符合這項相容性規則的電腦會回報 Configuration Manager 報告的 [資訊] 失敗嚴重性。  

    -   **警告**：不符合這項相容性規則的電腦會回報 Configuration Manager 報告的 [警告] 失敗嚴重性。  

    -   **重大**：不符合這項相容性規則的電腦會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。  

    -   **重大事件**：不符合這項相容性規則的電腦會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。 此嚴重性層級也會在應用程式事件記錄檔中記錄為 Windows 事件。  

##  <a name="a-namebkmkstep3a-step-3-provide-information-about-the-wireless-network"></a><a name="BKMK_Step3"></a> 步驟 3：提供無線網路的相關資訊  

1.  在 [Wi-Fi 設定檔]  頁面的 [建立 Wi-Fi 設定檔精靈] 中，使用最多 32 個字元，指定無線網際網路連線的描述性名稱。 這是裝置將顯示的網路名稱。  

    > [!IMPORTANT]  
    >  Configuration Manager 不支援在網路名稱中使用單引號 (**â€˜**) 或逗號 (**,**) 字元。  

2.  在 [SSID] 中，指定您要讓裝置連線的無線網路名稱 (SSID)。 您最多可以使用 32 個字元。 SSID 名稱區分大小寫，因此，請務必正確地輸入所設定的 SSID 名稱。  

3.  如果您想要允許裝置位於無線網路範圍內時自動重新連線到該無線網路，請選取 [當這個網路在範圍內時自動連線] 。  

4.  如果您想要允許裝置能在連線到此網路時，繼續掃描其他無線網路，請選取 [在連線到此網路時，尋找其他無線網路]  
                            **當連接到此網路時尋找其他無線網路**。  

5.  如果您想要允許裝置能在網路未列於網路清單時 (因為網路已隱藏且未廣播其名稱) 仍可連線到網路，請選取 [在網路未廣播其名稱 (SSID) 時進行連線] 。  

##  <a name="a-namebkmkstep4a-step-4-configure-security-for-the-wi-fi-profile"></a><a name="BKMK_Step4"></a> 步驟 4：設定 Wi-Fi 設定檔的安全性  

> [!IMPORTANT]  
>  如果您要建立 Wi-Fi 設定檔來進行內部部署行動裝置管理，則 Configuration Manager 的最新分支只支援下列 Wi-Fi 安全性設定：  
>   
>  安全性類型： **WPA2 Enterprise** 或 **WPA2 Personal**  
> 加密類型： **AES** 或 **TKIP**  
> EAP 類型： **智慧卡或其他憑證** 或 **PEAP**  

1.  在 [建立 Wi-Fi 設定檔精靈] 的 [安全性組態]  頁面中，選取無線網路使用的安全性通訊協定，或在網路不安全時選取 [不驗證 (開放)]  。  

     僅適用於 Android 裝置：不支援使用 [WPA - Personal]、[WPA2 - Personal] 和 [WEP] 安全性類型。  

2.  選取無線網路使用的加密方法。  

3.  選取用來進行無線網路驗證的 EAP 類型。  

     僅適用於 Windows Phone 裝置：不支援 [LEAP]  和 [EAP-FAST]  的 EAP 類型。  

4.  請按一下 [設定]  以指定所選取 EAP 類型的屬性。 此選項可能不適用於選取的某些 EAP 類型。  

    > [!IMPORTANT]  
    >  當您按一下 [設定] 時會開啟一個 Windows 對話方塊。 基於此原因，您必須確定執行 Configuration Manager 主控台之電腦的作業系統支援設定選取的 EAP類型。  
    >   
    >  針對 iOS 裝置，如果您選擇非 EAP 方法進行驗證，不論您選擇的方法為何，都會使用 MS-CHAP v2 進行連線。  

5.  如果您想要儲存使用者認證，以便使用者不需要在每次登入時輸入認證，請選取 [每次登入時記住使用者認證] 。  

### <a name="for-ios-devices-only"></a>僅適用於 iOS 裝置：  
 設定 Wi-Fi 連線所需要的任何憑證資訊。 您必須設定用戶端憑證，以及信任的伺服器憑證名稱或根憑證，如下所示：  

-   **信任的伺服器憑證名稱**：如果裝置連線的伺服器使用伺服器驗證憑證來識別伺服器並協助保護通訊通道，請在該憑證的主體名稱或主體別名中輸入一個或多個名稱。 這些名稱通常是伺服器的完整網域名稱。 例如，如果伺服器憑證在憑證主體中的一般名稱是 srv1.contoso.com，則輸入 **srv1.contoso.com**。 如果伺服器憑證在主體別名中指定多個名稱，請使用分號分隔輸入的每個名稱。  

    > [!TIP]  
    >  如果您為 EAP 選取的用戶端憑證或 iOS 裝置的用戶端驗證將用來驗證遠端驗證撥入使用者服務 (RADIUS) 伺服器 (例如執行網路原則伺服器的伺服器)，您必須將 [主體別名] 設定為使用者主體名稱。  

-   **選取根憑證以進行伺服器驗證**：如果裝置連線的伺服器使用裝置不信任的伺服器驗證憑證，請選取包含伺服器憑證之根憑證的憑證設定檔，以在裝置上建立信任的憑證鏈結。  

-   **選取用戶端驗證的用戶端憑證**：如果伺服器或網路裝置需要用戶端憑證來驗證連接的裝置，選取包含用戶端驗證憑證的憑證設定檔。  

> [!NOTE]  
>  在選取根憑證和用戶端憑證之前，您必須先將其設定及部署為憑證設定檔。 如需憑證設定檔的詳細資訊，請參閱 [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (System Center Configuration Manager 中的憑證設定檔)。  

##  <a name="a-namebkmkstep5a-step-5-configure-advanced-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step5"></a> 步驟 5：設定 Wi-Fi 設定檔的進階設定  
 在 [建立 Wi-Fi 設定檔精靈] 的 [進階設定]  頁面上，指定 Wi-Fi 設定檔的進階設定，例如驗證模式、單一登入選項和美國聯邦資訊處理標準相容性。 如需這些選項的詳細資訊，請參閱您的 Windows 文件。  

> [!NOTE]  
>  視您在精靈的 [安全性設定]  頁面上選取的選項而定，進階設定可能無法使用或者有所變動。  

##  <a name="a-namebkmkstep6a-step-6-configure-proxy-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step6"></a> 步驟 6：設定 Wi-Fi 設定檔的 Proxy 設定  

1.  如果您的無線網路使用 Proxy 伺服器，請在 [建立 Wi-Fi 設定檔精靈] 的 [Proxy 設定]  頁面上，選取 [設定此 Wi-Fi 設定檔的 Proxy 設定]  核取方塊。  

2.  指定與 Proxy 伺服器與其設定相關的詳細資料。 如需詳細資訊，請參閱 Windows Server 文件。  

##  <a name="a-namebkmkstep7a-step-7-configure-supported-platforms-for-the-wi-fi-profile"></a><a name="BKMK_Step7"></a> 步驟 7：設定 Wi-Fi 設定檔的支援平台  
 在 [建立 Wi-Fi 設定檔精靈] 的 [支援的平台]  頁面上，選取您要安裝 Wi-Fi 設定檔的作業系統。 或者，按一下 [全選]  將 Wi-Fi 設定檔安裝到所有可用的作業系統。  

##  <a name="a-namebkmkstep8a-step-8-complete-the-wizard"></a><a name="BKMK_Step8"></a> 步驟 8：完成精靈  
 在精靈的 [摘要]  頁面上，檢閱精靈將採取的動作，然後完成精靈。 新的 Wi-Fi 設定檔會出現在 [資產與相容性]  工作區的 [Wi-Fi 設定檔]  節點中。  

 如需如何部署 Wi-Fi 設定檔的資訊，請參閱 [How to deploy Wi-Fi profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) (如何在 System Center Configuration Manager 中部署 Wi-Fi 設定檔)。  



<!--HONumber=Nov16_HO1-->


