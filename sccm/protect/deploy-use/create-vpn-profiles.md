---
title: "如何在 System Center Configuration Manager 中建立 VPN 設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中建立 VPN 設定檔。"
ms.custom: 
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: 15
author: nbigman
caps.handback.revision: 0
ms.author: nbigman
ms.manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8a5dc7361da34f3e6b926acd35c72c0c0767ce70
ms.openlocfilehash: 73b8d28deb6e2c57c92ead2f0fee4d7a2d92f5d4


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中建立 VPN 設定檔

*適用於：System Center Configuration Manager (最新分支)*

適用於不同裝置平台之連線類型的資訊，描述於 [System Center Configuration Manager 中的 VPN 設定檔](../../protect/deploy-use/vpn-profiles.md)。  

針對協力廠商 VPN 連線，請先發佈 VPN 應用程式，再部署 VPN 設定檔。 如果您未部署應用程式，則系統會在使用者嘗試連線至 VPN 時提示他們進行這項作業。 若要了解如何部署應用程式，請參閱[使用 System Center Configuration Manager 部署應用程式](../../apps/deploy-use/deploy-applications.md)。

### <a name="create-a-vpn-profile"></a>建立 VPN 設定檔   

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [合規性設定] > [公司資源存取] > [VPN 設定檔]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立 VPN 設定檔]。  


1.  完成 [一般] 頁面。 ，並注意下列事項：  

    - 請勿在 VPN 設定檔名稱中使用字元 \\/:*?<>&#124;, 或空格字元。 Windows Server VPN 設定檔不支援這些字元。  

     -   選取 [從檔案匯入現有的 VPN 設定檔項目] 匯入已匯出至 XML 檔案的 VPN 設定檔資訊 (僅限 Windows 8.1 和 Windows RT)。  

1.  在 [連線] 頁面上，指定：  

    -   **連線類型**︰選擇 VPN 連線類型。 您可以從下表中，選擇連線類型。  

    -   **伺服器清單**：新增要用於 VPN 連線的新伺服器。 根據連線類型而定，您可以新增一或多部 VPN 伺服器，並指定預設伺服器。  

        > [!NOTE]  
        >  執行 iOS 的裝置並不支援使用多部 VPN 伺服器。 如果您設定多部 VPN 伺服器，然後將 VPN 設定檔部署至 iOS 裝置，則只會使用預設伺服器。  

     下表提供連線類型的選項。 如需詳細資訊，請參閱您的 VPN 伺服器文件。  

    |選項|詳細資訊|連線類型|  
    |------------|----------------------|---------------------|  
    |**領域**|您想要使用之驗證領域的名稱。 驗證領域就是 Pulse Secure 連線類型所使用的驗證資源群組。|Pulse Secure|  
    |**角色**|有權存取此連線的使用者角色。|Pulse Secure|  
    |**登入群組或網域**|您想要連線之登入群組或網域的名稱。|Dell SonicWALL Mobile Connect|  
    |**指紋**|將用來確認是否可以信任 VPN 伺服器的字串 (例如 "Contoso Fingerprint Code")。<br /><br /> 指紋可以是：<br /><br /> - 傳送至用戶端，讓它知道信任連線時呈現該相同指紋的任何伺服器。<br /><br /> - 如果裝置還沒有指紋，則會提示使用者信任所連線的 VPN 伺服器，同時顯示指紋 (使用者手動驗證指紋，並選擇 [信任] 連線)。|檢查點行動 VPN|  
    |**透過 VPN 連線傳送所有網路流量**|如果未選取此選項，您可以針對連線 (如 **Microsoft SSL (SSTP)**、 **Microsoft Automatic**、 **IKEv2**、 **PPTP** 和 **L2TP** 連線類型) 指定其他路由，這稱為分割或 VPN 通道。<br /><br /> 只有公司網路的連線會透過 VPN 通道傳送。 當您連線至網際網路上的資源時不會使用 VPN 通道。|全部：|  
    |**連線特定 DNS 尾碼**|連線的連線特定網域名稱系統 (DNS) 尾碼。|- <br />                            Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**連線到公司 Wi-Fi 網路時略過 VPN**|裝置連線到公司 Wi-Fi 網路時，不會使用 VPN 連線。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
    |**連線到家用 Wi-Fi 網路時略過 VPN**|裝置連線到家用 Wi-Fi 網路時，不會使用 VPN 連線。|全部：|  
    |**每個應用程式 VPN (iOS 7 及更新版本、Mac OS X 10.9 及更新版本)**|將這個 VPN 連線與 iOS 應用程式產生關聯，以在執行應用程式時開啟連線。 部署應用程式時，您可以將 VPN 設定檔與該應用程式產生關聯。|- <br />                        Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
    |**自訂 XML (選用)**|指定設定 VPN 連線的自訂 XML 命令。<br /><br /> 範例：<br /><br /> 針對 **Pulse Secure**：<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> 針對 **CheckPoint Mobile VPN**：<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> 針對 **Dell SonicWALL Mobile Connect**：<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> 針對 **F5 Edge Client**：<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> 如需如何撰寫自訂 XML 命令的詳細資訊，請參閱相關製造商的 VPN 文件。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  

    ###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>搭配使用 Configuration Manager 與 Intune 時可用的 Windows 10 VPN 功能  


    > [!NOTE]  
    > 使用 Windows 10 VPN 功能的 VPN 設定檔名稱不能是 Unicode，也不能包含特殊字元。


    |選項|詳細資訊|連線類型|  
    |------------|----------------------|---------------------|  
    |**連線到公司 Wi-Fi 網路時略過 VPN**|裝置連線到公司 Wi-Fi 網路時，不會使用 VPN 連線。 輸入受信任的網路名稱，用於判斷裝置是否連線到公司網路。|全部：|  
    |**網路流量規則**|設定將針對 VPN 連線啟用的通訊協定、本機和遠端連接埠，以及位址範圍。<br /><br /> **注意：** 如果您未建立網路流量規則，則會啟用所有通訊協定、連接埠和位址範圍。 一旦您建立規則，VPN 連線便只會使用您在該項規則或其他規則中所指定的通訊協定、連接埠和位址範圍。|全部：|  
    |**路由**|哪些路由會使用 VPN 連線。 請注意，建立超過 60 個路由可能會導致原則失敗。 |全部：|  
    |**DNS 伺服器**|VPN 連線建立後會使用哪些 DNS 伺服器。|全部：|  
    |**自動連線至 VPN 的應用程式**|您可以新增自動使用 VPN 連線的應用程式，或匯自動使用 VPN 連線的入應用程式清單。 應用程式類型將決定應用程式識別碼。 針對桌面應用程式，提供應用程式的檔案路徑。 針對通用應用程式，提供套件系列名稱 (PFN)。 若要了解如何尋找應用程式的 PFN，請參閱[尋找個別應用程式 VPN 的套件系列名稱](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md)。 |全部：|

    > [!IMPORTANT]
    > 建議保護由您所編譯以用於設定個別應用程式 VPN 的所有相關聯應用程式清單。 如果未經授權的使用者修改您的清單，而且您將該清單匯入個別應用程式 VPN 應用程式清單中，則您可能會授權 VPN 存取不應該存取的應用程式。 您可以保護應用程式清單的一種方法是使用存取控制清單 (ACL)。


1.  在精靈的 [驗證方法] 頁面上，指定：  

    -   **驗證方法：**選取 VPN 連線要使用的驗證方法。 可用的方法取決於連線類型，如此表格中所示。  

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

        -   **每次登入時記住使用者認證**：記住使用者認證，以便使用者不需在每次登入時都要輸入認證。  

        -   **選取用戶端憑證以進行用戶端驗證** - 選取先前建立的用戶端 [SCEP 憑證](introduction-to-certificate-profiles.md)，用來驗證 VPN 連線。   

            > [!NOTE]  
            >  如為 iOS 裝置，您所選取的 SCEP 設定檔會內嵌在 VPN 設定檔中。 對於其他平台，會加入適用性規則以確保當憑證不存在或不符合標準時，不會安裝 VPN 設定檔。  
            >   
            >  如果您指定的 SCEP 憑證不符合標準，或尚未部署，則裝置上不會安裝 VPN 設定檔。
            >  
            >  當連線類型為 [PPTP] 時，執行 iOS 的裝置僅支援 [RSA SecurID] 和 [MSCHAP v2] 作為驗證方法。 若要避免回報錯誤，請將獨立的 PPTP VPN 設定檔部署至執行 iOS 的裝置。  

        - **條件式存取**
            - 選擇 [啟用此 VPN 連線的條件式存取] 確保先測試連接至 VPN 裝置的條件式存取合規性，再連接。 [System Center Configuration Manager 中的裝置合規性政策](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md)中描述的合規性政策
            - 選擇 [以替代憑證啟用單一登入 (SSO)] 以選擇針對裝置合規性之 VPN 驗證憑證以外的憑證。 如果您選擇此選項，請提供 **EKU** (逗號分隔清單) 和**簽發者雜湊**，讓 VPN 用戶端找到正確的憑證。

         - **Windows 資訊保護** - 提供企業管理的公司身分識別，通常是貴組織的主要網域，例如 *contoso.com*。 您可以使用 "|" 字元分隔，指定貴組織擁有的多個網域。 例如 *contoso.com|newcontoso.com*。   
            如需 Windows 資訊保護的資訊，請參閱[使用 Microsoft Intune 建立 Windows 資訊保護 (WIP) 原則](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune)。   

         ![設定 VPN 的條件存取](../media/vpn-conditional-access.png)


        > [!NOTE]  
        >
        >對於某些驗證方法，您可以按一下 [設定] 開啟 Windows 的 [內容] 對話方塊 (如果您用來執行 Configuration Manager 主控台的 Windows 版本支援此驗證方法)，並在其中設定驗證方法的內容。  


1.  如果您的 VPN 連線使用 Proxy 伺服器，請在 [建立 VPN 設定檔精靈]  的 [Proxy 設定] 頁面上，選取 [設定此 VPN 設定檔的 Proxy 設定]  核取方塊。 然後，提供 Proxy 伺服器資訊。 如需詳細資訊，請參閱 Windows Server 文件。  

    > [!NOTE]  
    >  在 Windows 8.1 電腦上，除非您使用該電腦連線至 VPN，否則 VPN 設定檔不會顯示 Proxy 資訊。  


2. 設定其他 DNS 設定 (如有必要)  
 在 [設定自動 VPN 連線] 頁面上，您可以設定下列各項：  

    -   **依需求啟用 VPN**：如果您想針對 Windows Phone 8.1 裝置，設定進一步的 DNS 設定，請使用此選項。 這個設定僅適用於 Windows Phone 8.1 裝置，而且僅應該在即將部署至 Windows Phone 8.1 裝置的 VPN 設定檔上啟用。

    -   DNS 尾碼清單 (僅限 Windows Phone 8.1 裝置) - 設定將建立 VPN 連線的網域。 針對您指定的每個網域加入 DNS 尾碼、DNS 伺服器位址和下列其中之一的隨選動作：  

        -   **永不建立** - 永遠不開啟 VPN 連線  

        -   **視需要建立** - 只有在裝置需要連線至資源時，才會開啟 VPN 連線  

        -   **一律建立** - 永遠開啟 VPN 連線  

    -   **合併** - 將您設定的任何 DNS 尾碼複製到 [受信任的網路清單]。  

    -   **受信任的網路清單** (僅限 Windows Phone 8.1 裝置) - 一行指定一個 DNS 尾碼。 如果裝置位於受信任的網路，則不會開啟 VPN 連線。  

    -   **尾碼搜尋清單** (僅限 Windows Phone 8.1 裝置) - 一行指定一個 DNS 尾碼。 使用簡短名稱連線到網站時，將會搜尋每個 DNS 尾碼。  

     例如，您可以指定 DNS 尾碼 **domain1.contoso.com** 和 **domain2.contoso.com** ，然後瀏覽 URL **http://mywebsite**。 搜尋的位址如下：  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  僅限 Windows Phone 8.1 裝置  
    >   
    >  如果已針對佈建在裝置上的第一個設定檔選取 [透過 VPN 連線傳送所有網路流量]  選項，且 VPN 連線使用完整通道，則 VPN 連線會自動開啟。 如果您想要其他的設定檔自動開啟連線，您必須將其設為裝置上的預設設定檔。  
    >   
    >  如果 [透過 VPN 連線傳送所有網路流量]  選項並未選取，且 VPN 連線使用分割通道，則 VPN 連線會在您設定路由或連線特定 DNS 尾碼的情況下自動開啟。  


1. 在 [建立 VPN 設定檔精靈]  的 [支援的平台] 頁面上，選取將安裝 VPN 設定檔的作業系統，或按一下 [全選]  在所有可用的作業系統上安裝 VPN 設定檔。  

2. 完成精靈。 新的 VPN 設定檔會顯示在 [資產與相容性]  工作區的 [VPN 設定檔]  節點中。  

### <a name="next-steps"></a>後續步驟

- 針對協力廠商 VPN 連線，請先發佈 VPN 應用程式，再部署 VPN 設定檔。 如果您未部署應用程式，則系統會在使用者嘗試連線至 VPN 時提示他們進行這項作業。 若要了解如何部署應用程式，請參閱[使用 System Center Configuration Manager 部署應用程式](../../apps/deploy-use/deploy-applications.md)。

- 部署 VPN 設定檔 (如[如何在 System Center Configuration Manager 中部署設定檔](deploy-wifi-vpn-email-cert-profiles.md)中所述)。  



<!--HONumber=Dec16_HO5-->


