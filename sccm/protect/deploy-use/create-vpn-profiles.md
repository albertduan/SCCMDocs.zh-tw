---
title: "如何在 System Center Configuration Manager 中建立 VPN 設定檔"
description: "了解如何在 System Center Configuration Manager 中建立 VPN 設定檔。"
ms.custom: na
ms.date: 10/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: 15
caps.handback.revision: 0
ms.author: nbigman
ms.manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: e215b33ca24370ddd0e1b892d6ebe559023852a2
ms.openlocfilehash: ccea5cb46bf69dbb88f6fcb217a73c7939be0b02


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中建立 VPN 設定檔

*適用於︰System Center Configuration Manager (最新分支)*


> [!NOTE]  
>
> - 如需適用於不同裝置平台之連線類型的資訊，請參閱 [System Center Configuration Manager 中的 VPN 設定檔](../../protect/deploy-use/vpn-profiles.md)。  
> - 針對協力廠商 VPN 連線，請先發佈 VPN 應用程式，再部署 VPN 設定檔。 如果您未部署應用程式，則系統會在使用者嘗試連線至 VPN 時提示他們進行這項作業。 若要了解如何部署應用程式，請參閱[使用 System Center Configuration Manager 部署應用程式](../../apps/deploy-use/deploy-applications)。

### <a name="start-the-create-vpn-profile-wizard"></a>啟動 [建立 VPN 設定檔精靈]  

1.  在 System Center Configuration Manager 主控台中，按一下 [資產與相容性]。  

2.  在 System Center Configuration Manager 主控台的 [資產與相容性] 工作區中，依序展開 [相容性設定] 和 [公司資源存取]，然後按一下 [VPN 設定檔]。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立 VPN 設定檔] 。  

### <a name="provide-general-information-about-the-vpn-profile"></a>提供與 VPN 設定檔有關的一般資訊  

1.  在 [建立 VPN 設定檔精靈]  的 [一般] 頁面上，指定下列資訊：  

    -   **名稱** - 輸入 VPN 設定檔的唯一名稱 (最多 256 個字元)。  

        > [!IMPORTANT]  
        >  請勿在 VPN 設定檔名稱中使用字元 \\/:*?<>&#124;, 或空格字元，因為 Windows Server VPN 設定檔不支援這些字元。  

    -   **描述** - 輸入可協助您在 System Center Configuration Manager 主控台中尋找設定檔的描述 (最多 256 個字元)。  

    -   **從檔案匯入現有的 VPN 設定檔項目** - 選取此選項可顯示 [匯入 VPN 設定檔] 頁面。 在此頁面中，您可以匯入之前已匯出至 XML 檔案 的 VPN 設定檔資訊 (僅限 Windows 8.1 和 Windows RT 作業系統)。  

### <a name="provide-connection-information-for-the-vpn-profile"></a>提供 VPN 設定檔的連線資訊  

1.  在精靈的 [連線]  頁面上，指定下列資訊：  

    -   **連線類型：** 從下拉式清單中選取 VPN 連線的連線類型。 您可以從顯示支援平台的下表中，選擇連線類型。  

        > [!IMPORTANT]  
        >  您應該先安裝所需的協力廠商 VPN 應用程式，才能使用部署至裝置的 VPN 設定檔。 您可以使用[如何使用 System Center Configuration Manager 建立應用程式](../../apps/deploy-use/create-applications.md)主題中的資訊，協助您使用 System Center Configuration Manager 來部署應用程式。  

    -   **伺服器清單：** 按一下 [新增]  加入要用於 VPN 連線的新伺服器。 根據連線類型而定，您可以新增一部或多部 VPN 伺服器，並指定哪部伺服器是預設伺服器。  

        > [!NOTE]  
        >  執行 iOS 的裝置並不支援使用多部 VPN 伺服器。 如果您設定多部 VPN 伺服器，然後將 VPN 設定檔部署至 iOS 裝置，則只會使用預設伺服器。  

     根據您選取的連線類型，可能會顯示下表中的其他選項。 如需詳細資訊，請參閱您的 VPN 伺服器文件。  

    |選項|詳細資訊|連線類型|  
    |------------|----------------------|---------------------|  
    |**領域**|指定您想要使用之驗證領域的名稱。 驗證領域就是 Pulse Secure 連線類型所使用的驗證資源群組。|Pulse Secure|  
    |**角色**|指定有權存取此連線之使用者角色的名稱。|Pulse Secure|  
    |**登入群組或網域**|指定您想要連線之登入群組或網域的名稱。|Dell SonicWALL Mobile Connect|  
    |**指紋**|指定將用來確認是否信任 VPN 伺服器的字串 (例如 "Contoso Fingerprint Code")。<br /><br /> 指紋可以是：<br /><br /> - 傳送至用戶端，讓它知道信任連線時呈現該相同指紋的任何伺服器。<br /><br /> - 如果裝置還沒有指紋，則會提示使用者信任所連線的 VPN 伺服器，同時顯示指紋 (使用者手動驗證指紋，並按一下 [信任] 連線)。|檢查點行動 VPN|  
    |**透過 VPN 連線傳送所有網路流量**|如果未選取此選項，您可以針對連線 (如 **Microsoft SSL (SSTP)**、 **Microsoft Automatic**、 **IKEv2**、 **PPTP** 和 **L2TP** 連線類型) 指定其他路由，這稱為分割或 VPN 通道。<br /><br /> 只有公司網路的連線會透過 VPN 通道傳送。 當您連線至網際網路上的資源時不會使用 VPN 通道。|全部：|  
    |**連線特定 DNS 尾碼**|或者，您也可以為連線指定連線特定的網域名稱系統 (DNS) 尾碼。|- <br />                            Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**連線到公司 Wi-Fi 網路時略過 VPN**|指定裝置連線到公司 Wi-Fi 網路時，不會使用 VPN 連線。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
    |**連線到家用 Wi-Fi 網路時略過 VPN**|指定裝置連線到家用 Wi-Fi 網路時，不會使用 VPN 連線。|全部：|  
    |**每個應用程式 VPN (iOS 7 及更新版本、Mac OS X 10.9 及更新版本)**|如果您想要這個 VPN 連線與 iOS 應用程式產生關聯，以在執行應用程式時開啟連線，請選取此選項。 部署應用程式時，您可以將 VPN 設定檔與該應用程式產生關聯。|- <br />                        Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
    |**自訂 XML (選用)**|可讓您指定設定 VPN 連線的自訂 XML 命令。<br /><br /> 範例：<br /><br /> 針對 **Pulse Secure**：<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> 針對 **CheckPoint Mobile VPN**：<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> 針對 **Dell SonicWALL Mobile Connect**：<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> 針對 **F5 Edge Client**：<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> 如需如何撰寫自訂 XML 命令的詳細資訊，請參閱相關製造商的 VPN 文件。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  

####   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>搭配使用 Configuration Manager 與 Intune 時可用的 Windows 10 VPN 功能  


> [!NOTE]  
> 使用 Windows 10 VPN 功能的 VPN 設定檔名稱不能是 Unicode，也不能包含特殊字元。


|選項|詳細資訊|連線類型|  
|------------|----------------------|---------------------|  
|**連線到公司 Wi-Fi 網路時略過 VPN**|指定裝置連線到公司 Wi-Fi 網路時，不會使用 VPN 連線。 輸入受信任的網路名稱，受信任的網路名稱將用於判斷裝置是否連線到公司網路。|全部：|  
|**網路流量規則**|設定將針對 VPN 連線啟用的通訊協定、本機和遠端連接埠，以及位址範圍。<br /><br /> **注意：** 如果您未建立網路流量規則，則會啟用所有通訊協定、連接埠和位址範圍。 一旦您建立規則，VPN 連線便只會使用您在該項規則或其他規則中所指定的通訊協定、連接埠和位址範圍。|全部：|  
|**路由**|哪些路由會使用 VPN 連線。 請注意，建立超過 60 個路由可能會導致原則失敗。 |全部：|  
|**DNS 伺服器**|VPN 連線建立後會使用哪些 DNS 伺服器。|全部：|  
|**自動連線至 VPN 的應用程式**|您可以新增自動使用 VPN 連線的應用程式，或匯自動使用 VPN 連線的入應用程式清單。 應用程式類型將決定應用程式識別碼。 針對桌面應用程式，提供應用程式的檔案路徑。 針對通用應用程式，提供套件系列名稱 (PFN)。 若要了解如何尋找應用程式的 PFN，請參閱[尋找個別應用程式 VPN 的套件系列名稱](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md)。 |全部：|

> [!IMPORTANT]
> 建議保護由您所編譯以用於設定個別應用程式 VPN 的所有相關聯應用程式清單。 如果未經授權的使用者修改您的清單，而且您將該清單匯入個別應用程式 VPN 應用程式清單中，則您可能會授權 VPN 存取不應該存取的應用程式。 您可以保護應用程式清單的一種方法是使用存取控制清單 (ACL)。


### <a name="configure-the-authentication-method-for-the-vpn-profile"></a>設定 VPN 設定檔的驗證方法  

1.  在精靈的 [驗證方法]  頁面上，指定下列資訊：  

    -   **驗證方法：** 在下拉式清單中，選取 VPN 連線要使用的驗證方法。 根據您之前選取的連線類型，下拉式清單中的項目可能會有所不同。 可用的驗證方法和支援的連線類型已列於下表中。  

        |驗證方法|支援的連線類型|  
        |---------------------------|--------------------------------|  
        |**憑證**<br /><br /> **注意：** 如果要使用用戶端憑證來驗證 RADIUS 伺服器 (例如網路原則伺服器)，則憑證中的主體別名必須設為使用者主體名稱。|- <br />                            Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**使用者名稱和密碼**|- <br />                            Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**Microsoft Protected EAP (PEAP)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Microsoft Secured Password (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**智慧卡或其他憑證**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** (僅 iOS)|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**使用電腦憑證**|IKEv2|  

         根據您選取的選項，可能會要求您指定進一步的資訊，例如：  

        -   **在每次登入時記住使用者認證**：選取此選項，確保記住使用者認證，讓使用者不必每次建立連線時都輸入認證。  

        -   **選取用戶端憑證以進行用戶端驗證** - 選取先前建立的用戶端 SCEP 憑證，用來驗證 VPN 連線。 如需如何在 System Center Configuration Manager 中使用憑證設定檔的詳細資訊，請參閱 [System Center Configuration Manager 中的憑證設定檔](introduction-to-certificate-profiles.md)。  

            > [!NOTE]  
            >  如為 iOS 裝置，您所選取的 SCEP 設定檔會內嵌在 VPN 設定檔中。 對於其他平台，會加入適用性規則以確保當憑證不存在或不符合標準時，不會安裝 VPN 設定檔。  
            >   
            >  如果您指定的 SCEP 憑證不符合標準，或尚未部署，則裝置上不會安裝 VPN 設定檔。
            >  
            >  當連線類型為 [PPTP] 時，執行 iOS 的裝置僅支援 [RSA SecurID] 和 [MSCHAP v2] 作為驗證方法。 若要避免回報錯誤，請將獨立的 PPTP VPN 設定檔部署至執行 iOS 的裝置。  

               - [條件式存取] 和 [企業資料保護主要網域] 設定，只有在未使用 Intune 的情況下使用 Configuration Manager 時才予以支援，並且可以選擇 [進階] 進行存取。
        
        ![設定 VPN 的條件存取](../media/vpn-conditional-access.png)

        -   對於某些驗證方法，您可以按一下 [設定] 開啟 Windows 的 [內容] 對話方塊 (如果您用來執行 System Center Configuration Manager 主控台的 Windows 版本支援此驗證方法)，並在其中設定驗證方法的內容。  

### <a name="configure-proxy-settings-for-the-vpn-profile"></a>設定 VPN 設定檔的 Proxy 設定  

1.  如果您的 VPN 連線使用 Proxy 伺服器，請在 [建立 VPN 設定檔精靈]  的 [Proxy 設定] 頁面上，選取 [設定此 VPN 設定檔的 Proxy 設定]  核取方塊。  

2.  指定與 Proxy 伺服器與其設定相關的詳細資料。 如需詳細資訊，請參閱 Windows Server 文件。  

> [!NOTE]  
>  在 Windows 8.1 電腦上，除非您使用該電腦連線至 VPN，否則 VPN 設定檔不會顯示 Proxy 資訊。  


### <a name="configure-further-dns-settings-if-required"></a>設定其他 DNS 設定 (如有必要)  
 在精靈的 [設定自動 VPN 連線]  頁面上，您可以設定下列設定：  

-   **依需求啟用 VPN**：如果您想針對 Windows Phone 8.1 裝置，在精靈的這個頁面上設定進一步的 DNS 設定，請選取此選項。

> [!Note]  
> 這個設定僅適用於 Windows Phone 8.1 裝置，而且僅應該在即將部署至 Windows Phone 8.1 裝置的 VPN 設定檔上啟用。


-   DNS 尾碼清單 (僅限 Windows Phone 8.1 裝置) - 設定將建立 VPN 連線的網域。 針對您指定的每個網域加入 DNS 尾碼、DNS 伺服器位址和下列其中之一的隨選動作：  

    -   **永不建立** - 永遠不開啟 VPN 連線  

    -   **視需要建立** - 只有在裝置需要連線至資源時，才會開啟 VPN 連線  

    -   **一律建立** - 永遠開啟 VPN 連線  

-   **合併** - 將您設定的任何 DNS 尾碼複製到 [受信任的網路清單]。  

-   **受信任的網路清單** (僅限 Windows Phone 8.1 裝置) - 一行指定一個 DNS 尾碼。 如果裝置位於受信任的網路，則不會開啟 VPN 連線。  

-   **尾碼搜尋清單** (僅限 Windows Phone 8.1 裝置) - 一行指定一個 DNS 尾碼。 使用簡短名稱連線到網站時，將會搜尋您指定的每個 DNS 尾碼。  

     例如，您可以指定 DNS 尾碼 **domain1.contoso.com** 和 **domain2.contoso.com** ，然後瀏覽 URL **http://mywebsite**。 搜尋的位址如下：  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

> [!NOTE]  
>  僅限 Windows Phone 8.1 裝置  
>   
>  如果已針對佈建在裝置上的第一個設定檔選取 [透過 VPN 連線傳送所有網路流量]  選項，且 VPN 連線使用完整通道，則 VPN 連線會自動開啟。 如果您想要其他的設定檔自動開啟連線，您必須將其設為裝置上的預設設定檔。  
>   
>  如果 [透過 VPN 連線傳送所有網路流量]  選項並未選取，且 VPN 連線使用分割通道，則 VPN 連線會在您設定路由或連線特定 DNS 尾碼的情況下自動開啟。  


### <a name="configure-supported-platforms-for-the-vpn-profile"></a>設定 VPN 設定檔的支援平台  
 支援的平台就是要安裝 VPN 設定檔的作業系統。  

在 [建立 VPN 設定檔精靈]  的 [支援的平台] 頁面上，選取將安裝 VPN 設定檔的作業系統，或按一下 [全選]  在所有可用的作業系統上安裝 VPN 設定檔。  

### <a name="complete-the-wizard"></a>完成精靈  
 在精靈的 [摘要] 頁面上，檢閱要採取的動作，然後選擇 [完成]。 新的 VPN 設定檔會顯示在 [資產與相容性]  工作區的 [VPN 設定檔]  節點中。  

### <a name="next-steps"></a>後續步驟

- 針對協力廠商 VPN 連線，請先發佈 VPN 應用程式，再部署 VPN 設定檔。 如果您未部署應用程式，則系統會在使用者嘗試連線至 VPN 時提示他們進行這項作業。 若要了解如何部署應用程式，請參閱[使用 System Center Configuration Manager 部署應用程式](../../apps/deploy-use/deploy-applications)。

- 部署 VPN 設定檔 (如[如何在 System Center Configuration Manager 中部署設定檔](deploy-wifi-vpn-email-cert-profiles.md)中所述)。  



<!--HONumber=Nov16_HO1-->


