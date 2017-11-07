---
title: "Windows Hello 企業版設定"
titleSuffix: Configuration Manager
description: "了解如何整合 Windows Hello 企業版與 System Center Configuration Manager。"
ms.custom: na
ms.date: 09/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: "17"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 195a5f8e595b6a8597e8c8c8d9046c5864f46526
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2017
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager 的 Windows Hello 企業版設定

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 讓您整合 Windows Hello 企業版 (原 Microsoft Passport for Windows)，這是 Windows 10 裝置的另一種登入方法。 Windows Hello 企業版使用 Active Directory 或 Azure Active Directory 帳戶來取代密碼、智慧卡或虛擬智慧卡。  

Windows Hello 企業版可讓您藉由 **使用者手勢** 登入，而不使用密碼。 使用者手勢可能是簡單的 PIN、生物識別驗證或外部裝置 (例如指紋辨識器)。

[深入了解 Windows Hello 企業版 (英文)](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)

 Configuration Manager 與 Windows Hello 企業版整合的方法有兩種：  

-   您可以使用 Configuration Manager 控制使用者可以/不可用以登入的筆勢。  

-   您可以將驗證憑證儲存在 Windows Hello 企業版金鑰儲存提供者 (KSP) 中。 如需詳細資訊，請參閱[憑證設定檔](introduction-to-certificate-profiles.md)。  

- 您可以將 Windows Hello 企業版原則部署至執行 Configuration Manager 用戶端且已加入網域的 Windows 10 裝置。 下文的[在已加入網域的 Windows 10 裝置上設定 Windows Hello 企業版](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices) 對此設定有所說明。 當您搭配 Microsoft Intune 使用 Configuration Manager (混合式) 時，您可以在 Windows 10 與 Windows 10 Mobile 裝置上設定這些設定。 如需詳細資訊，請參閱[進行 Windows Hello 企業版設定 (混合式)](../../mdm/deploy-use/windows-hello-for-business-settings.md)。

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>在已加入網域的 Windows 10 裝置上設定 Windows Hello 企業版
您可以透過建立並部署 Windows Hello 企業版設定檔，以控制已加入網域之 Windows 10 裝置上的 Windows Hello 企業版設定。 這是建議的方法。


若您是使用憑證式驗證，您也必須部署憑證設定檔，如[設定憑證設定檔](#configure-a-certificate-profile)所述。 若您是使用金鑰式驗證，則不需要部署憑證設定檔。

## <a name="configure-a-windows-hello-for-business-profile"></a>設定 Windows Hello 企業版設定檔  

在 Configuration Manager 主控台中，以滑鼠右鍵按一下 [公司資源存取] 下的 [Windows Hello 企業版設定檔]，然後選擇 [新增] 啟動設定檔精靈。 提供精靈要求的設定，檢閱及確認最後一頁的設定，然後按一下 [關閉]。 您的設定可能像以下的範例︰  

![Windows Hello 企業版設定](../media/Hello-for-Business-settings.png)

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>設定憑證設定檔以在 Configuration Manager 中註冊 Windows Hello 企業版註冊憑證  
 若您想要使用 Windows Hello 企業版憑證式登入，請進行下列設定：  

-   Configuration Manager 憑證設定檔。  

-   在憑證設定檔中，選取使用智慧卡登入 EKU 的範本。  

-   如果您打算將憑證設定檔儲存在 Windows Hello 企業版金鑰容器中，且憑證設定檔使用「智慧卡登入」EKU，您必須為金鑰註冊設定下列權限，以確保能夠正確驗證憑證。
您必須先建立 **Key Admins** 群組，然後將所有Configuration Manager 管理點電腦新增為此群組的成員。

某些設定可能不需要您設定權限，或可能需要您進行進一步的設定。 如需更多說明，請參閱下列表格：

|||||
|-|-|-|-|
|Windows 用戶端版本|Configuration Manager 1602 或 1606|Configuration Manager 1610|Configuration Manager 1702 或更新版本|
|Windows 10 年度更新版|不需要 Hotfix<br><br>不需要權限<br><br>不需要更新 Windows 結構描述|不需要 Hotfix (請參閱＜警告＞)<br><br>不需要權限<br><br>不需要更新 Windows 結構描述|設定權限<br><br>套用 Windows Server 2016 結構描述道 Active Directory|
|Windows 10 Creators Update 或更新版本|不支援|安裝[此 Hotfix](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)<br><br>設定權限<br><br>套用 Windows Server 2016 結構描述道 Active Directory|設定權限<br><br>套用 Windows Server 2016 結構描述道 Active Directory|

> [!WARNING]
> 雖然 Configuration Manager 1610 與 Windows 10 年度更新版不需要該 [Hotfix](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)，系統可能會安裝它。  若該 Hotfix 已安裝，您必須設定權限並套用 Windows Server 2016 結構描述到 Active Directory。

## <a name="to-configure-permissions"></a>設定權限

1.  以網域系統管理員身分 (或對等的認證) 登入網域控制站或管理工作站。
2.  開啟 [Active Directory 使用者和電腦]。
3.  在瀏覽窗格中，以滑鼠右鍵按一下網域名稱，然後按一下 [內容]。
4.  在 [<domain name> 內容] 對話方塊的 [安全性] 索引標籤上，按一下 [進階]。 如果未顯示 [安全性] 索引標籤，請從 [Active Directory 使用者和電腦] 的 [檢視] 功能表，開啟 [進階功能]。
5.  按一下 [新增] 。
6.  在 [<domain name> 的權限項目] 對話方塊中，按一下 [選取主體]。
7.  在 [選取使用者、電腦、服務帳戶或群組] 對話方塊中，於 [輸入要選取的物件名稱] 文字方塊輸入 **Key Admins**。  按一下 [ **確定**]。
8.  在 [套用至] 清單中，選取 [子系使用者物件]。
9.  捲動至頁面底部，然後按一下 [全部清除]。
10. 在 [屬性] 區段中，選取 [讀取 msDS-KeyCredentialLink]。
11. 按三次 [確定] 以完成工作。


## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱[憑證設定檔](introduction-to-certificate-profiles.md)。  




