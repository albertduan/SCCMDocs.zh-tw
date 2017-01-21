---
title: "建立 PFX 憑證設定檔 | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中使用 PFX 檔案，產生支援加密資料交換的使用者特定憑證。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0185ab18-663d-468a-ba54-4f3f232fd4d2
caps.latest.revision: 5
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4a4025325e635061cb99caed9cdb07390e90ea90


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中建立 PFX 憑證設定檔

*適用於︰System Center Configuration Manager (最新分支)*


System Center Configuration Manager 可讓您將個人資訊交換 (.pfx) 檔案佈建到使用者裝置。 PFX 檔案可用以產生使用者特定憑證，以支援加密的資料交換。 您可以在 Configuration Manager 中建立或匯入 PFX 憑證。 使用 System Center Configuration Manager，匯入的或新的 PFX 憑證可以部署到 iOS、Android 和 Windows 10 裝置。 這些檔案接著可以部署到多部裝置來支援以使用者為基礎的 PKI 通訊。  

> [!TIP]  
>  您可以參閱 [如何在 Configuration Manager 中建立與部署 PFX 憑證設定檔](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)一文，以取得描述此程序的逐步解說。  

## <a name="create-and-deploy-personal-information-exchange-pfx-certificate-profiles"></a>建立及部署個人資訊交換 (PFX) 憑證設定檔  

#### <a name="how-to-create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>如何建立及部署個人資訊交換 (PFX) 憑證設定檔  

1.  在 System Center Configuration Manager 主控台中，按一下 [資產與相容性]。  

2.  在 [資產與相容性]  工作區中，依序展開 [相容性設定] 和 [公司資源存取] ，然後按一下 [憑證設定檔] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立憑證設定檔] 。 [建立憑證設定檔精靈]  隨即開啟。  

4.  在 [建立憑證設定檔精靈]  的 [一般]  頁面上，指定下列資訊：  

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

8.  包含 PFX 檔案的憑證設定檔現在可從 [憑證設定檔]  工作區取得。 在  工作區的 [相容性設定]  >  >  ，按一下滑鼠右鍵將新的憑證部署到使用者集合。  

9. 使用可從下載中心取得，適用於 Windows 8.1 的 SDK ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525)來部署「建立 PFX 指令碼」。 在 Configuration Manager 2012 SP2 中加入的「建立 PFX 指令碼」，會將 SMS_ClientPfxCertificate 類別加入 SDK。 這個類別包含下列方法：  

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



<!--HONumber=Nov16_HO1-->


