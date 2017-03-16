---
title: "建立 PFX 憑證設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用 PFX 檔案，產生支援加密資料交換的使用者特定憑證。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: eddecee8886296fb6132d7477afebbfc7fd280d1
ms.lasthandoff: 03/06/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中建立 PFX 憑證設定檔

*適用於︰System Center Configuration Manager (最新分支)*

憑證設定檔與 Active Directory 憑證服務和網路裝置註冊服務角色搭配運作，以佈建受管理裝置的驗證憑證，讓使用者可以順暢地存取公司資源。 例如，您可以建立和部署憑證設定檔，以提供必要的憑證讓使用者起始 VPN 和無線網路連線。

[憑證設定檔](../../protect/deploy-use/introduction-to-certificate-profiles.md)提供有關建立及設定憑證設定檔的一般資訊。 本主題會強調說明一些與行動裝置管理相關之憑證設定檔的特定資訊。

- 憑證設定檔為執行 iOS、Windows 8.1、Windows RT 8.1、Windows 10 Desktop 與行動裝置版和 Android 的裝置，提供憑證註冊以及從企業憑證授權單位 (CA) 更新憑證的功能。 然後，這些憑證就可以用於 Wi-Fi 和 VPN 連線。

-  若要部署使用 SCEP 的憑證設定檔，您必須在執行 Windows Server 2012 R2 的伺服器上使用「Active Directory 憑證服務」角色安裝 NDES 的原則模組，以及可供需要憑證之裝置存取的作用中 NDES。 針對由 Microsoft Intune 註冊的裝置，則需要可以從網際網路存取的 NDES，例如遮蔽式子網路 (亦稱為 DMZ)。

-  Configuration Manager 可根據需求、裝置類型和作業系統，將憑證部署至不同的憑證存放區。 支援下列裝置和作業系統：
 -   Windows RT 8.1  
 -   Windows 8.1  
 -   Windows Phone 8.1  
 -   Windows 10 Desktop 與行動裝置版  
 -   iOS  
 -   Android  
 > [!IMPORTANT]  
 >  若要將設定檔部署到 Android、iOS、Windows Phone 和已註冊的 Windows 8.1 或更新版本的裝置，必須在 [Microsoft Intune 註冊](https://technet.microsoft.com/en-us/library/dn646962.aspx)這些裝置。   

- 對於其他先決條件，請參閱[憑證設定檔先決條件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)。

## <a name="pfx-certificate-profiles"></a>PFX 憑證設定檔
System Center Configuration Manager 可讓您將個人資訊交換 (.pfx) 檔案佈建到使用者裝置。 PFX 檔案可用以產生使用者特定憑證，以支援加密的資料交換。 您可以在 Configuration Manager 中建立或匯入 PFX 憑證。 使用 System Center Configuration Manager，匯入的或新的 PFX 憑證可以部署到 iOS、Android 和 Windows 10 裝置。 這些檔案接著可以部署到多部裝置來支援以使用者為基礎的 PKI 通訊。  

> [!TIP]  
>  您可以參閱 [如何在 Configuration Manager 中建立與部署 PFX 憑證設定檔](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)一文，以取得描述此程序的逐步解說。  

### <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>建立及部署個人資訊交換 (PFX) 憑證設定檔  

1.  在 System Center Configuration Manager 主控台中，按一下 [資產與合規性]。  

2.  在 [資產與合規性] 工作區中，依序展開 [合規性設定] 和 [公司資源存取]，然後按一下 [憑證設定檔] 。  

3.  在 [常用] ** 索引標籤的 [建立] 群組中，按一下 [建立憑證設定檔]。 [建立憑證設定檔精靈] 隨即開啟。  

4.  在 [建立憑證設定檔精靈] 的 [一般] 頁面上，指定下列資訊：  

    -   **名稱**：輸入憑證設定檔的唯一名稱。 您最多可以使用 256 個字元。  

    -   **描述**：提供一段描述以說明憑證設定檔的概觀，以及可協助您在 System Center Configuration Manager 主控台中進行識別的其他相關資訊。 您最多可以使用 256 個字元。  

    -   **指定您要建立的憑證設定檔類型**：選擇下列其中一個憑證設定檔類型：  

        -   **信任的 CA 憑證**：當使用者或裝置必須驗證其他裝置時，如果您要部署信任的根憑證授權單位 (CA) 或中繼 CA 憑證以組成信任的憑證鏈結，請選取此憑證設定檔類型。 例如，裝置可能是遠端驗證撥入使用者服務 (RADIUS) 伺服器或虛擬私人網路 (VPN) 伺服器。 在建立 SCEP 憑證設定檔之前，您還必須設定信任的 CA 憑證設定檔。 在此情況中，信任的 CA 憑證設定檔必須是發行憑證至使用者或裝置之 CA 的受信任根憑證。  

        -   **簡單憑證註冊通訊協定 (SCEP) 設定**：如果您使用簡單憑證註冊通訊協定和網路裝置註冊服務角色服務來要求使用者或裝置的憑證，請選取此憑證設定檔類型。  

        -   **個人資訊交換 -- PKCS #12 (PFX) 設定 -- 匯入**：選取此選項以匯入 PFX 憑證。  

5.  在 [建立憑證設定檔精靈]  的 [憑證內容]  視窗中，指定 PFX 憑證在目標裝置上的儲存位置。  

    -   **安裝至信賴平台模組 (TPM) (若存在)**  

    -   **安裝至信賴平台模組 (TPM)，否則便失敗**  

    -   **安裝至軟體金鑰儲存提供者**  

     按一下 [下一步] 。  

6.  在 [建立憑證設定檔精靈]  的 [支援的平台]  視窗中，指定哪個作業系統或平台可以接收匯入的 PFX 檔案。  

    -   **Windows 10**  

    -   **iPhone**  

    -   **iPad**  

    -   **Android**  

7.  按 [下一步] ，檢閱 [摘要]  頁面，然後關閉精靈。  

8.  包含 PFX 檔案的憑證設定檔現在可從 [憑證設定檔]  工作區取得。 在 [資產與合規性] 工作區，移至 [合規性設定] > [公司資源存取] > [憑證設定檔]，並按一下滑鼠右鍵將新的憑證部署到使用者集合。  

9. 使用可從下載中心取得適用於 Windows 8.1 的 SDK ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525) 來部署「建立 PFX 指令碼」。 在 Configuration Manager 2012 SP2 中加入的「建立 PFX 指令碼」，會將 SMS_ClientPfxCertificate 類別加入 SDK。 這個類別包含下列方法：  

    -   ImportForUser  

    -   DeleteForUser  

     範例指令碼：  

    ```  
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  

    ```  

     下列指令碼變數必須修改才能用於您的指令碼：  

    -   <blob\> = PFX base64 加密的 Blob  

    -   $Password = PFX 檔案的密碼  

    -   $ProfileName = PFX 設定檔的名稱  

    -   ComputerName = 主機電腦的名稱  

### <a name="see-also"></a>請參閱
[建立新的憑證設定檔](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile)會逐步引導您完成 [建立憑證設定檔精靈]。

[部署 Wi-Fi、VPN、電子郵件和憑證設定檔](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)提供有關部署憑證設定檔的相關資訊。

