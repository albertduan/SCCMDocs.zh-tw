---
title: "Windows Hello 企業版設定 | Microsoft Docs"
description: "了解如何整合 Windows Hello 企業版與 System Center Configuration Manager。"
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: 17
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: ec3d130674d606410e6da7babee126e017aff234
ms.lasthandoff: 03/04/2017


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager 的 Windows Hello 企業版設定

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 讓您整合 Windows Hello 企業版 (原 Microsoft Passport for Windows)，這是 Windows 10 裝置的另一種登入方法。 Windows Hello 企業版使用 Active Directory 或 Azure Active Directory 帳戶來取代密碼、智慧卡或虛擬智慧卡。  

Windows Hello 企業版可讓您藉由 **使用者手勢** 登入，而不使用密碼。 使用者手勢可能是簡單的 PIN、生物識別驗證或外部裝置 (例如指紋辨識器)。  

 Configuration Manager 與 Windows Hello 企業版整合的方法有兩種：  

-   您可以使用 Configuration Manager 控制使用者可以/不可用以登入的筆勢。  

-   您可以將驗證憑證儲存在 Windows Hello 企業版金鑰儲存提供者 (KSP) 中。 如需詳細資訊，請參閱[憑證設定檔](introduction-to-certificate-profiles.md)。  

- 您可以將 Windows Hello 企業版原則部署至執行 Configuration Manager 用戶端且已加入網域的 Windows 10 裝置。 下文的[在已加入網域的 Windows 10 裝置上設定 Windows Hello 企業版](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices) 對此設定有所說明。 當您使用 Configuration Manager 與 Intune (混合) 時，您可以在 Windows 10 和 Windows 10 行動裝置上設定這些設定，但不能在執行 Configuration Manager 用戶端且加入網域的裝置上設定。 如需詳細資訊，請參閱[進行 Windows Hello 企業版設定 (混合式)](../../mdm/deploy-use/windows-hello-for-business-settings.md)。

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>在已加入網域的 Windows 10 裝置上設定 Windows Hello 企業版
您有三種方式可以在已加入網域的 Windows 10 裝置上控制 Windows Hello 企業版設定︰

- 您可以建立及部署 Windows Hello 企業版設定檔。 這是建議的方法。
- 您可以使用群組原則。  
- 您可以使用 PowerShell 指令碼。

請注意，除了此設定外，您也必須部署憑證設定檔，如[設定憑證設定檔](#configure-a-certificate-profile)中所述。

### <a name="recommended-approach----configure-a-windows-hello-for-business-profile"></a>建議的方法 - 設定 Windows Hello 企業版設定檔  

在系統管理員主控台中，以滑鼠右鍵按一下 [公司資源存取] 下的 [Windows Hello 企業版設定檔]，然後選擇 [新增] 啟動設定檔精靈。 提供精靈要求的設定，檢閱及確認最後一頁的設定，然後按一下 [關閉]。 您的設定可能像以下的範例︰  

![Windows Hello 企業版設定](../media/Hello-for-Business-settings.png)

### <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>使用 Active Directory 群組原則設定 Windows Hello 企業版  

您可以使用 Active Directory 群組原則來設定 Windows 10 已加入網域的裝置，在使用者登入 Windows 時佈建使用者的 Hello 企業版認證：

1.  在 Windows Server 電腦上，開啟 [伺服器管理員]，並瀏覽至 [工具] > [群組原則管理]。    

2.  在 [群組原則管理]  對話方塊方塊中，展開您要啟用自動工作場所聯結的網域。    

3.  以滑鼠右鍵按一下 [群組原則物件] ，然後按一下 [新增] 。  

4.  在 [新增 GPO] 對話方塊中，輸入新群組原則物件的名稱，例如**啟用 Windows Hello 企業版**，然後按一下 [確定]。  

5.  在 [群組原則物件]  節點中，以滑鼠右鍵按一下您剛建立的物件，然後按一下 [編輯] 。  

6.  在 [群組原則管理編輯器] 對話方塊中，瀏覽至 [電腦設定] > [原則] > [系統管理範本] > [Windows 元件] > [Windows Hello 企業版]。  

7.  以滑鼠右鍵按一下 [啟用 Windows Hello 企業版]，然後按一下 [編輯]。   

8.  選取 [已啟用] ，按一下 [套用] ，然後按一下 [確定] 。

您現在可以將剛剛建立的群組原則物件連結到您選擇的位置。 例如：    

   AD 中的特定組織單位 (OU)，Windows 10 已加入網域的電腦將放置於此。    

   特定安全性群組，其中包含會自動向 Azure AD 註冊的 Windows 10 已加入網域電腦。    

#### <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>使用 Configuration Manager 部署 PowerShell 指令碼以設定 Windows Hello 企業版    
您也可以使用 Configuration Manager 應用程式管理，建立並部署下列 PowerShell 指令碼。    

```    
powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}"  
```  

如需 Configuration Manager 應用程式管理的詳細資訊，請參閱 [System Center Configuration Manager 的應用程式管理簡介](/sccm/apps/understand/introduction-to-application-management)。  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>設定憑證設定檔以在 Configuration Manager 中註冊 Windows Hello 企業版註冊憑證  
 若您想要使用 Windows Hello 企業版憑證式登入或使用 Microsoft Hello，請進行下列設定：  

-   Configuration Manager 憑證設定檔。  

-   在憑證設定檔中，選取使用智慧卡登入 EKU 的範本。  

 如需詳細資訊，請參閱[憑證設定檔](introduction-to-certificate-profiles.md)。  

### <a name="see-also"></a>請參閱  
 [使用 System Center Configuration Manager 保護資料和站台基礎結構](../../protect/understand/protect-data-and-site-infrastructure.md)

 [使用商務用 Windows Hello 管理身分識別驗證](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport)。  

