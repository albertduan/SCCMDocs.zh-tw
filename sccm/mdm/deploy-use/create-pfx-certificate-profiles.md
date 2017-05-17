---
title: "建立 PFX 憑證設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用 PFX 檔案，產生支援加密資料交換的使用者特定憑證。"
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 26feb0b166beb7e48cb800a5077d00dbc3eec51a
ms.openlocfilehash: 27435316c6e47531ff989bc8956ca0c874131a0e
ms.contentlocale: zh-tw
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中建立 PFX 憑證設定檔

*適用於︰System Center Configuration Manager (最新分支)*

憑證設定檔與 Active Directory 憑證服務和網路裝置註冊服務角色搭配運作，以佈建受管理裝置的驗證憑證，讓使用者可以順暢地存取公司資源。 例如，您可以建立和部署憑證設定檔，以提供必要的憑證讓使用者起始 VPN 和無線網路連線。

[憑證設定檔](../../protect/deploy-use/introduction-to-certificate-profiles.md)提供有關建立及設定憑證設定檔的一般資訊。 本主題會強調說明一些與 PFX 憑證相關之憑證設定檔的特定資訊。

-  Configuration Manager 可根據需求、裝置類型和作業系統，將憑證部署至不同的憑證存放區。 使用 Intune 註冊時支援下列裝置︰

 -   iOS  

- 對於其他先決條件，請參閱[憑證設定檔先決條件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)。

## <a name="pfx-certificate-profiles"></a>PFX 憑證設定檔
System Center Configuration Manager 可讓您匯入，接著將個人資訊交換 (.pfx) 檔案佈建到使用者裝置。 PFX 檔案可用以產生使用者特定憑證，以支援加密的資料交換。

> [!TIP]  
>  您可以參閱 [如何在 Configuration Manager 中建立與部署 PFX 憑證設定檔](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)一文，以取得描述此程序的逐步解說。  

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>建立及部署個人資訊交換 (PFX) 憑證設定檔  

### <a name="get-started"></a>開始使用

1.  在 System Center Configuration Manager 主控台中，按一下 [資產與相容性]。  

2.  在 [資產與合規性] 工作區中，依序展開 [合規性設定] 和 [公司資源存取]，然後按一下 [憑證設定檔] 。  

3.  在 [常用] ** 索引標籤的 [建立] 群組中，按一下 [建立憑證設定檔]。

4.  在 [建立憑證設定檔精靈] 的 [一般] 頁面上，指定下列資訊：  

    -   **名稱**：輸入憑證設定檔的唯一名稱。 您最多可以使用 256 個字元。  

    -   **描述**：提供一段描述以說明憑證設定檔的概觀，以及可協助您在 System Center Configuration Manager 主控台中進行識別的其他相關資訊。 您最多可以使用 256 個字元。  

    -   **指定您要建立的憑證設定檔類型**：對於 PFX 憑證，請選擇：  

        -   **個人資訊交換 PKCS #12 (PFX) 設定 - 匯入**：選取此選項以匯入 PFX 憑證。  
       

### <a name="import-a-pfx-certificate"></a>匯入 PFX 憑證

若要匯入 PFX 憑證，您將需要 Configuration Manager SDK。 您為使用者匯入的任何憑證將部署到使用者註冊的所有裝置。

1. 在 [建立憑證設定檔精靈] 的 [PFX 憑證] 頁面中，指定 PFX 憑證在部署的目標裝置上的儲存位置：
    -     **安裝至信賴平台模組 (TPM) (若存在)**  
    -   **安裝至信賴平台模組 (TPM)，否則便失敗** 
    -   **安裝至 Windows Hello 企業版否則便失敗** 
    -   **安裝至軟體金鑰儲存提供者** 
2. 按一下 [下一步] 。 
3. 在精靈的 [支援的平台] 頁面中，選擇將安裝此憑證的裝置平台，然後按一下 [下一步]。
4. 使用可從下載中心取得適用於 Windows 8.1 的 SDK ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525) 來部署「建立 PFX 指令碼」。 在 Configuration Manager 2012 SP2 中加入的「建立 PFX 指令碼」，會將 SMS_ClientPfxCertificate 類別加入 SDK。 這個類別包含下列方法：  

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

   -   blob\ = The PFX base64-encrypted blob  
   -   $Password = PFX 檔案的密碼  
   -   $ProfileName = PFX 設定檔的名稱  
   -   ComputerName = 主機電腦的名稱   



### <a name="finish-up"></a>完成

1.  按 [下一步] ，檢閱 [摘要]  頁面，然後關閉精靈。  
2.  包含 PFX 檔案的憑證設定檔現在可從 [憑證設定檔]  工作區取得。 
3.  如果要顯示設定檔，在 [資產與合規性] 工作區，開啟 [合規性設定]  >  [公司資源存取]  >  [憑證設定檔]，以滑鼠右鍵按一下您想要的憑證，然後按一下 [部署]。 



## <a name="see-also"></a>請參閱
[建立新的憑證設定檔](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile)會逐步引導您完成 [建立憑證設定檔精靈]。

[部署 Wi-Fi、VPN、電子郵件和憑證設定檔](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)提供有關部署憑證設定檔的相關資訊。
