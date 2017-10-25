---
title: "透過匯入憑證詳細資料建立 PFX 憑證設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用 PFX 檔案，產生支援加密資料交換的使用者特定憑證。"
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: "5"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: c8346d04c7cd9761291824f5d30f09fab9acbcf9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-pfx-certificate-profiles-by-importing-certificate-details"></a>如何透過匯入憑證詳細資料建立 PFX 憑證設定檔

適用於：System Center Configuration Manager (最新分支)


您可以從這裡了解如何透過匯入來自外部憑證的認證來建立憑證設定檔。  

[憑證設定檔](../../protect/deploy-use/introduction-to-certificate-profiles.md)提供有關建立及設定憑證設定檔的一般資訊。 本主題會強調說明一些與 PFX 憑證相關之憑證設定檔的特定資訊。

-  Configuration Manager 具有適用於不同裝置及作業系統的一系列憑證存放區。  它們包括：

 -   iOS 和 MacOS/OSX
 -   Android 和 Android for Work
 -   Windows 10，包括 Windows 10 行動裝置版。

若要深入了解，請參閱[憑證設定檔必要條件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)。

## <a name="pfx-certificate-profiles"></a>PFX 憑證設定檔
System Center Configuration Manager 可讓您匯入憑證認證，接著將個人資訊交換 (.pfx) 檔案佈建到使用者裝置。 PFX 檔案可用以產生使用者特定憑證，以支援加密的資料交換。

> [!TIP]  
>  您可以參閱 [如何在 Configuration Manager 中建立與部署 PFX 憑證設定檔](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)一文，以取得描述此程序的逐步解說。  

## <a name="create-import-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>建立、匯入及部署個人資訊交換 (PFX) 憑證設定檔  

### <a name="get-started"></a>開始使用

1.  在 System Center Configuration Manager 主控台中，按一下 [資產與相容性]。  
2.  在 資產與合規性 工作區中，依序展開 合規性設定 和 公司資源存取，然後按一下憑證設定檔 。  

3.  在 [常用] ** 索引標籤的 [建立] 群組中，按一下 [建立憑證設定檔]。

4.  在 [建立憑證設定檔精靈] 的 [一般] 頁面上，指定下列資訊：  

    -   **名稱**：輸入憑證設定檔的唯一名稱。 您最多可以使用 256 個字元。  

    -   **描述**：提供一段描述以說明憑證設定檔的概觀，以及可協助您在 System Center Configuration Manager 主控台中進行識別的其他相關資訊。 您最多可以使用 256 個字元。  

    -   **指定您要建立的憑證設定檔類型**：針對 PFX 憑證，請選擇下列其中一個選項：  

        -   **個人資訊交換 PKCS #12 (PFX) 設定 - 匯入**：透過以程式設計方式匯入現有憑證的資訊來建立憑證設定檔。  

        -   **個人資訊交換 - PKCS #12 (PFX) 設定 - 建立**：使用由憑證授權單位所提供的認證建立 PFX 憑證設定檔。  若要深入了解，請參閱[如何使用憑證授權單位建立 PFX 憑證設定檔](../../mdm/deploy-use/create-pfx-certificate-profiles.md)。


### <a name="create-a-pfx-certificate-profile-for-the-imported-credentials"></a>針對已匯入的認證建立 PFX 憑證設定檔

若要匯入 PFX 憑證，請使用 Configuration Manager SDK 部署「建立 PFX」指令碼。 

已匯入的憑證會於稍後部署至已註冊的裝置。

1. 在 [建立憑證設定檔精靈] 的 [PFX 憑證] 頁面上，指定裝置金鑰儲存提供者針對下列項目的安裝位置：
    -   **安裝至信賴平台模組 (TPM) (若存在)**  
    -   **安裝至信賴平台模組 (TPM)，否則便失敗** 
    -   **安裝至 Windows Hello 企業版否則便失敗** 
    -   **安裝至軟體金鑰儲存提供者** 
2. 按一下 [下一步] 。 
3. 在精靈的 支援的平台 頁面上，選擇支援的裝置平台，然後按一下下一步。

### <a name="finish-the-profile"></a>完成設定檔

1.  按 [下一步] ，檢閱 [摘要]  頁面，然後關閉精靈。  
2.  包含 PFX 檔案的憑證設定檔現在可從 [憑證設定檔]  工作區取得。 
3.  如果要顯示設定檔，在 [資產與合規性] 工作區，開啟 [合規性設定]  >  [公司資源存取]  >  [憑證設定檔]，以滑鼠右鍵按一下您想要的憑證，然後按一下 [部署]。 

### <a name="deploy-a-create-pfx-script"></a>部署「建立 PFX」指令碼

使用 [Configuration Manager SDK](http://go.microsoft.com/fwlink/?LinkId=613525) 部署「建立 PFX」指令碼。 

在 Configuration Manager 2012 SP2 中加入的「建立 PFX 指令碼」，會將 SMS_ClientPfxCertificate 類別加入 SDK。 這個類別包含下列方法：  

    -   `ImportForUser`  

    -   `DeleteForUser`  

下列範例會將認證匯入至 PFX 憑證設定檔。

``` powershell
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

若要使用此範例，請更新下列指令碼變數：  

   -   **blob**\：PFX base64 加密的 Blob  
   -   **$Password**：PFX 檔案的密碼  
   -   **$ProfileName**：PFX 設定檔的名稱  
   -   **ComputerName**：主機電腦的名稱   

## <a name="see-also"></a>請參閱
[建立新的憑證設定檔](../../protect/deploy-use/create-certificate-profiles.md)會逐步引導您完成 [建立憑證設定檔精靈]。

[如何透過匯入憑證詳細資料建立 PFX 憑證設定檔](../../mdm/deploy-use/create-pfx-certificate-profiles.md)

[部署 Wi-Fi、VPN、電子郵件和憑證設定檔](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)會描述如何部署憑證設定檔。