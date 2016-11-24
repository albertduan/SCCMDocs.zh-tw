---
title: "建立 Exchange ActiveSync 電子郵件設定檔 | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中建立和設定與 Microsoft Intune 搭配運作的電子郵件設定檔。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 15f0fd50-e196-44e5-b435-234d7ff6a5cd
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 613ed15742322e2eb90eec3c9f493e3b1755d93a


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Exchange ActiveSync 電子郵件設定檔

*適用於︰System Center Configuration Manager (最新分支)*

電子郵件設定檔可與 Microsoft Intune 搭配運作，讓您使用 Exchange ActiveSync 為裝置佈建電子郵件設定檔和限制。 這可讓您的使用者只需以最少的安裝步驟，即可存取其裝置上的公司電子郵件。  

 您可以使用電子郵件設定檔設定下列裝置類型：  

-   執行 Windows Phone 8 的裝置  

-   執行 Windows Phone 8.1 的裝置  

-   執行 Windows 10 Mobile 的裝置  

-   執行 iOS 5、iOS 6、iOS 7 和 iOS 8 的 iPhone 裝置  

-   執行 iOS 5、iOS 6、iOS 7 和 iOS 8 的 IPad 裝置  

> [!IMPORTANT]  
>  若要將設定檔部署到 iOS、Android Samsung KNOX、Windows Phone 和 Windows 8.1 或 Windows 10 裝置，這些裝置必須註冊 Intune。 如需如何取得已註冊裝置的相關資訊，請參閱 [使用 Microsoft Intune 管理行動裝置](https://technet.microsoft.com/en-us/library/dn646962.aspx)。  

 除了在裝置上設定電子郵件帳戶外，您也可以設定連絡人、行事曆和工作的同步處理設定。  

 當您建立電子郵件設定檔時，可以在其中加入各種安全性設定，包括使用 System Center Configuration Manager 憑證設定檔所佈建的識別憑證、加密憑證和簽署憑證。 如需憑證設定檔的詳細資訊，請參閱 [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (System Center Configuration Manager 中的憑證設定檔)。    


## <a name="create-a-new-exchange-activesync-email-profile"></a>建立新的 Exchange ActiveSync 電子郵件設定檔  

啟動建立 Exchange ActiveSync 電子郵件設定檔精靈  

1.  在 System Center Configuration Manager 主控台中，按一下 [資產與相容性]。  

2.  在 [資產與相容性]  工作區中，依序展開 [相容性設定] 和 [公司資源存取] ，然後按一下 [電子郵件設定檔] 。  

3.  在 [常用]  索引標籤上，按一下 [建立]  群組中的 [建立 Exchange ActiveSync 設定檔] 。 

4.  遵循精靈指示   

### <a name="to-configure-exchange-activesync-settings-for-the-exchange-activesync-email-profile"></a>進行 Exchange ActiveSync 電子郵件設定檔的 Exchange ActiveSync 設定  

1.  在 [建立 Exchange ActiveSync 電子郵件設定檔精靈] 的 [Exchange ActiveSync]  頁面上，指定下列資訊：  

    -   **Exchange ActiveSync 主機** ：指定託管 Exchange ActiveSync 服務之公司 Exchange Server 的主機名稱。  

    -   **帳戶名稱** ：指定要在使用者裝置上向使用者顯示之電子郵件帳戶的顯示名稱。  

    -   **帳戶使用者名稱** ：選取用戶端裝置上電子郵件帳戶使用者名稱的設定方式。 您可以從下拉式清單中選取下列其中一個選項：  

        -   **使用者主體名稱** ：使用完整使用者主體名稱登入 Exchange。  

        -   **sAMAccountName** ：使用  

        -   **主要 SMTP 位址** ：使用使用者主要 SMTP 位址登入 Exchange。  

    -   **電子郵件地址** ：選取每個用戶端裝置上使用者電子郵件地址的產生方式。 您可以從下拉式清單中選取下列其中一個選項：  

        -   **主要 SMTP 位址** ：使用使用者主要 SMTP 位址登入 Exchange。  

        -   **使用者主體名稱** ：使用完整使用者主體名稱做為電子郵件地址。  

    -   **帳戶網域** ：請選擇下列其中一個選項：  

        -   **從 Active Directory 取得**  

        -   **自訂**  

         只有當選取 [帳戶使用者名稱]  下拉式清單中的 **sAMAccountName** 時，這個欄位才適用。  

    -   **驗證方法** ：請選擇下列其中一個驗證方法，用來驗證 Exchange ActiveSync 連線：  

        -   **憑證** ：要用來驗證 Exchange ActiveSync 連線的身分識別憑證。  

        -   **使用者名稱和密碼** ：裝置使用者必須提供用來連線至 Exchange ActiveSync 的密碼 (使用者名稱已設定為電子郵件設定檔的一部分)。  

    -   **身分識別憑證** ：按一下 [選取]  ，然後選取要用於身分識別的憑證。  

        > [!NOTE]  
        >  您必須先將身分識別憑證設定為簡單憑證註冊通訊協定 (SCEP) 憑證設定檔，才能選取身分識別憑證。 如需憑證設定檔的詳細資訊，請參閱 [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (System Center Configuration Manager 中的憑證設定檔)。  

         只有當選取 [驗證方法]  下方的 [憑證] 時，才能使用這個選項。  

    -   **使用 S/MIME** ：使用 S/MIME 加密傳送外寄電子郵件。 這個選項僅適用於 iOS 裝置。  

    -   **加密憑證** ：按一下 [選取]  ，然後選取要用於加密的憑證。 這個選項僅適用於 iOS 裝置。  

        > [!NOTE]  
        >  您必須先將加密憑證設定為簡單憑證註冊通訊協定 (SCEP) 憑證設定檔，才能選取加密憑證。 如需憑證設定檔的詳細資訊，請參閱 [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (System Center Configuration Manager 中的憑證設定檔)。  

         只有當選取 [使用 S/MIME] 時，才能使用這個選項。  

    -   **簽署憑證** ：按一下 [選取]  ，然後選取要用於簽署的憑證。 這個選項僅適用於 iOS 裝置。  

        > [!NOTE]  
        >  您必須先將簽署憑證設定為簡單憑證註冊通訊協定 (SCEP) 憑證設定檔，才能選取簽署憑證。 如需憑證設定檔的詳細資訊，請參閱 [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (System Center Configuration Manager 中的憑證設定檔)。  

         只有當選取 [使用 S/MIME] 時，才能使用這個選項。  

###   <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>進行 Exchange ActiveSync 電子郵件設定檔的同步處理設定。  

1.  在 [建立 Exchange ActiveSync 電子郵件設定檔精靈] 的 [設定同步處理設定]  頁面上，指定下列資訊：  

    -   **排程** ：選取裝置用來同步處理 Exchange Server 資料的排程。 這個選項僅適用於 Windows Phone 裝置。 從下列選項進行選擇：  

        -   **未設定** ：不會強制執行同步處理排程。 這個選項可讓使用者設定自己的同步處理排程。  

        -   **郵件送達時** ：電子郵件和行事曆項目等資料送達時，會自動進行同步處理。  

        -   **15 分鐘** ：每隔 15 分鐘會自動同步處理電子郵件和行事曆項目等資料。  

        -   **30 分鐘** ：每隔 30 分鐘會自動同步處理電子郵件和行事曆項目等資料。  

        -   **60 分鐘** ：每隔 60 分鐘會自動同步處理電子郵件和行事曆項目等資料。  

        -   **手動** ：裝置使用者必須手動起始同步處理。  

    -   **要同步處理的電子郵件天數** ：從下拉式清單中，選取您想要同步處理電子郵件的天數。 選擇下列其中一個值：  

        -   **未設定** ：不會強制執行設定。 這個選項可讓使用者設定要下載至其裝置的電子郵件數目。  

        -   **無限制** ：同步處理所有可用的電子郵件。  

        -   **1 天**  

        -   **3 天**  

        -   **1 週**  

        -   **2 週**  

        -   **1 個月**  

    -   **允許將郵件移至其他電子郵件帳戶** ：選取這個選項可讓使用者在其裝置上所設定的不同帳戶之間移動電子郵件訊息。 這個選項僅適用於 iOS 裝置。  

    -   **允許從協力廠商應用程式傳送電子郵件** ：選取這個選項可讓使用者從特定非預設的協力廠商電子郵件應用程式傳送電子郵件。 這個選項僅適用於 iOS 裝置。  

    -   **同步處理最近使用的電子郵件地址** ：選取這個選項可同步處理裝置上最近使用的電子郵件地址清單。 這個選項僅適用於 iOS 裝置。  

    -   **使用 SSL** ：選取這個選項可在傳送電子郵件、接收電子郵件，以及與 Exchange Server 通訊時，使用安全通訊端層 (SSL) 通訊。  

    -   **要同步處理的內容類型** ：選取您想要與裝置同步處理的內容類型。 這個選項僅適用於 Windows Phone 裝置。 從下列選項進行選擇：  

        -   **電子郵件**  

        -   **連絡人**  

        -   **行事曆**  

        -   **工作**  

###  <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>指定 Exchange ActiveSync 電子郵件設定檔的支援平台。  
 
1.  在 [建立 Exchange ActiveSync 電子郵件設定檔精靈] 的 [支援的平台]  頁面上，選取將安裝電子郵件設定檔的作業系統，或按一下 [全選]  在所有可用的作業系統上安裝電子郵件設定檔。  

2.  完成精靈。

如需如何部署 Exchange ActiveSync 電子郵件設定檔的相關資訊，請參閱[如何在 System Center Configuration Manager 中部署設定檔](deploy-wifi-vpn-email-cert-profiles.md)。  



<!--HONumber=Nov16_HO1-->


