---
title: "System Center Configuration Manager 中的 VPN 設定檔 | Microsoft Docs"
description: "System Center Configuration Manager 中的行動裝置 VPN 設定檔。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 32190ec39af2cf1568b3d57c2c2f25d9ff2f9e20
ms.lasthandoff: 03/06/2017

---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的行動裝置 VPN 設定檔

*適用於︰System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 中使用 VPN 設定檔，將 VPN 設定部署至組織中的行動裝置使用者。 透過部署這些設定，即可最小化連線到公司網路上資源所需的使用者工作。  

 例如，您想要以連線至企業網路上檔案共用所需的設定佈建所有執行 iOS 作業系統的裝置。 您可以建立含有連線至企業網路所需設定的 VPN 設定檔，然後將此設定檔部署至階層中所有擁有執行 iOS 之裝置的使用者。 iOS 裝置的使用者會看見可用網路清單中的 VPN 連線，並且可以輕鬆連線至此網路。  

 當您建立 VPN 設定檔時，您可以在其中加入各種安全性設定，包括藉由使用 System Center Configuration Manager 憑證設定檔佈建的伺服器驗證憑證和用戶端驗證憑證。 如需憑證設定檔的詳細資訊，請參閱 [System Center Configuration Manager 中的憑證設定檔](../../protect/deploy-use/introduction-to-certificate-profiles.md)。  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>使用 Configuration Manager 和 Intune 時的 VPN 設定檔 
 
 若要將設定檔部署到 iOS、Android、Windows Phone 和 Windows 8.1 裝置，這些裝置必須在 Microsoft Intune 註冊。 其他平台上的裝置也可以註冊至 Intune。 如需如何註冊的資訊，請參閱[註冊裝置以在 Intune 中管理](https://technet.microsoft.com/en-us/library/dn646962.aspx)。 此表格顯示各裝置平台支援的連線類型︰  

 |連線類型|iOS 與 Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop 與行動裝置版|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|是|是|否|否|否|否|是 (OMA-URI)|  
 |Pulse Secure|是|是|是|否|是|是|是|  
 |F5 Edge Client|是|是|是|否|是|是|是|  
 |Dell SonicWALL Mobile Connect|是|是|是|否|是|是|是|  
 |檢查點行動 VPN|是|是|是|否|是|是|是|  
 |Microsoft SSL (SSTP)|否|否|是|是|是|否|否|  
 |Microsoft Automatic|否|否|是|是|是|否|是 (OMA-URI)|  
 |IKEv2|是 (自訂原則)|否|是|是|是|是|是 (OMA-URI)|  
 |PPTP|是|否|是|是|是|否|是 (OMA-URI)|  
 |L2TP|是|否|是|是|是|否|是 (OMA-URI)|  

## <a name="create-vpn-profiles"></a>建立 VPN 設定檔
[如何在 System Center Configuration Manager 中建立 VPN 設定檔](../../protect/deploy-use/create-vpn-profiles.md)提供有關建立 VPN 設定檔的一般資訊。

###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>搭配使用 Configuration Manager 與 Intune 時可用的 Windows 10 VPN 功能  


> [!NOTE]  
> 使用 Windows 10 VPN 功能的 VPN 設定檔名稱不能是 Unicode，也不能包含特殊字元。


|選項|詳細資訊|連線類型|  
    |------------|----------------------|---------------------|  
    |**連線到公司 Wi-Fi 網路時略過 VPN**|裝置連線到公司 Wi-Fi 網路時，不會使用 VPN 連線。 輸入受信任的網路名稱，用於判斷裝置是否連線到公司網路。|全部|  
    |**網路流量規則**|設定將針對 VPN 連線啟用的通訊協定、本機和遠端連接埠，以及位址範圍。<br /><br /> **注意：**如果您未建立網路流量規則，則會啟用所有通訊協定、連接埠和位址範圍。 一旦您建立規則，VPN 連線便只會使用您在該項規則或其他規則中所指定的通訊協定、連接埠和位址範圍。|全部|  
    |**路由**|哪些路由會使用 VPN 連線。 請注意，建立超過 60 個路由可能會導致原則失敗。 |全部|  
    |**DNS 伺服器**|VPN 連線建立後會使用哪些 DNS 伺服器。|全部|  
    |**自動連線至 VPN 的應用程式**|您可以新增自動使用 VPN 連線的應用程式，或匯入自動使用 VPN 連線的應用程式清單。 應用程式類型將決定應用程式識別碼。 針對傳統型應用程式，提供應用程式的檔案路徑。 針對通用應用程式，提供套件系列名稱 (PFN)。 若要了解如何尋找應用程式的 PFN，請參閱[尋找個別應用程式 VPN 的套件系列名稱](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md)。 |全部|

> [!IMPORTANT]
> 建議保護由您所編譯以用於設定個別應用程式 VPN 的所有相關聯應用程式清單。 如果未經授權的使用者修改您的清單，而且您將該清單匯入個別應用程式 VPN 應用程式清單中，則您可能會授權 VPN 存取不應該存取的應用程式。 您可以保護應用程式清單的一種方法是使用存取控制清單 (ACL)。


1.  在精靈的 [驗證方法] 頁面上，指定：  

    -   **驗證方法：**選取 VPN 連線要使用的驗證方法。 可用的方法取決於連線類型，如此表格中所示。  

        |驗證方法|支援的連線類型|  
        |---------------------------|--------------------------------|  
        |**憑證**<br /><br /> **注意：**如果要使用用戶端憑證來驗證 RADIUS 伺服器 (例如網路原則伺服器)，則憑證中的主體別名必須設為使用者主體名稱。|- <br />                            Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
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
            >  對於 iOS 裝置，您所選取的 SCEP 設定檔會內嵌在 VPN 設定檔中。 對於其他平台，會加入適用性規則以確保當憑證不存在或不符合規範時，不會安裝 VPN 設定檔。  
            >   
            >  如果您指定的 SCEP 憑證不符合規範，或尚未部署，則裝置上不會安裝 VPN 設定檔。
            >  
            >  當連線類型為 [PPTP] 時，執行 iOS 的裝置僅支援 [RSA SecurID] 和 [MSCHAP v2] 作為驗證方法。 若要避免回報錯誤，請將獨立的 PPTP VPN 設定檔部署至執行 iOS 的裝置。  

        - **條件式存取**
            - 選擇 [啟用此 VPN 連線的條件式存取] 確保先測試連線至 VPN 裝置的條件式存取合規性，再連線。 [System Center Configuration Manager 中的裝置合規性原則](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md)中描述的合規性原則
            - 選擇 [以替代憑證啟用單一登入 (SSO)] 以選擇針對裝置合規性之 VPN 驗證憑證以外的憑證。 如果您選擇此選項，請提供 **EKU** (逗號分隔清單) 和**簽發者雜湊**，讓 VPN 用戶端找到正確的憑證。

         - **Windows 資訊保護** - 提供企業管理的公司身分識別，通常是貴組織的主要網域，例如 *contoso.com*。 您可以使用 "|" 字元分隔，指定貴組織擁有的多個網域。 例如 *contoso.com|newcontoso.com*。   
              如需 Windows 資訊保護的資訊，請參閱[使用 Microsoft Intune 建立 Windows 資訊保護 (WIP) 原則](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune)。   

         ![設定 VPN 的條件式存取](media/vpn-conditional-access.png)


> [!NOTE]  
> 對於某些驗證方法，您可以按一下 [設定] 以開啟 Windows 的 [內容] 對話方塊 (如果您用來執行 Configuration Manager 主控台的 Windows 版本支援此驗證方法)，並在其中設定驗證方法的內容。  


1.  如果您的 VPN 連線使用 Proxy 伺服器，請在 [建立 VPN 設定檔精靈] 的 [Proxy 設定] 頁面上，選取 [設定此 VPN 設定檔的 Proxy 設定] 核取方塊。 然後，提供 Proxy 伺服器資訊。 如需詳細資訊，請參閱 Windows Server 文件。  

    > [!NOTE]  
    >  在 Windows 8.1 電腦上，除非您使用該電腦連線至 VPN，否則 VPN 設定檔不會顯示 Proxy 資訊。  


2. 設定其他 DNS 設定 (如有必要)  
 在 [設定自動 VPN 連線] 頁面上，您可以設定下列各項：  

    -   **依需求啟用 VPN**：如果您想針對 Windows Phone 8.1 裝置設定進一步的 DNS 設定，請使用此選項。 這個設定僅適用於 Windows Phone 8.1 裝置，而且僅應該在即將部署至 Windows Phone 8.1 裝置的 VPN 設定檔上啟用。

    -   DNS 尾碼清單 (僅限 Windows Phone 8.1 裝置) - 設定將建立 VPN 連線的網域。 針對您指定的每個網域加入 DNS 尾碼、DNS 伺服器位址和下列其中之一的隨選動作：  

        -   **永不建立** - 一律不開啟 VPN 連線  

        -   **視需要建立** - 只有在裝置需要連線至資源時，才會開啟 VPN 連線  

        -   **一律建立** - 一律開啟 VPN 連線  

    -   **合併** - 將您設定的任何 DNS 尾碼複製到 [受信任的網路清單]。  

    -   **受信任的網路清單** (僅限 Windows Phone 8.1 裝置) - 一行指定一個 DNS 尾碼。 如果裝置位於受信任的網路，則不會開啟 VPN 連線。  

    -   **尾碼搜尋清單** (僅限 Windows Phone 8.1 裝置) - 一行指定一個 DNS 尾碼。 使用簡短名稱連線到網站時，將會搜尋每個 DNS 尾碼。  

     例如，您可以指定 DNS 尾碼 **domain1.contoso.com** 和 **domain2.contoso.com** ，然後瀏覽 URL **http://mywebsite**。 搜尋的位址如下：  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  僅限 Windows Phone 8.1 裝置  
    >   
    >  如果已針對佈建在裝置上的第一個設定檔選取 [透過 VPN 連線傳送所有網路流量]  選項，且 VPN 連線使用完整通道，則 VPN 連線會自動開啟。 如果您想要其他的設定檔自動開啟連線，您必須將它設定為裝置上的預設設定檔。  
    >   
    >  如果 [透過 VPN 連線傳送所有網路流量] 選項並未選取，且 VPN 連線使用分割通道處理，則 VPN 連線會在您設定路由或連線特定 DNS 尾碼的情況下自動開啟。  


1. 在 [建立 VPN 設定檔精靈] 的 [支援的平台] 頁面上，選取將安裝 VPN 設定檔的作業系統，或按一下 [全選] 在所有可用的作業系統上安裝 VPN 設定檔。  

2. 完成精靈。 新的 VPN 設定檔會顯示在 [資產與合規性] 工作區的 [VPN 設定檔] 節點中。  


**部署︰**如需有關部署 VPN 設定檔的詳細資訊，請參閱[部署 Wi-Fi、VPN、電子郵件和憑證設定檔](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)。

### <a name="next-steps"></a>後續步驟  
 使用下列主題可協助您規劃、設定、操作及維護 Configuration Manager 中的 VPN 設定檔。  

-   [System Center Configuration Manager 中的 VPN 設定檔必要條件](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [System Center Configuration Manager 中的 VPN 設定檔安全性及隱私權](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
