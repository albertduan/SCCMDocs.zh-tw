---
title: "從網際網路安裝及指派用戶端 | Microsoft Docs"
description: "從網際網路安裝及指派 System Center Configuration Manager 用戶端。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: 14
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: f604557d208b2dda9dc1c6b4c4d27d896d47695e
ms.contentlocale: zh-tw
ms.lasthandoff: 07/29/2017

---

# <a name="install-and-assign-configuration-manager-clients-from-the-internet-using-azure-ad-for-authentication"></a>從網際網路安裝及指派 Configuration Manager 用戶端並使用 Azure AD 進行驗證

您可以使用 Configuration Manager 雲端服務搭配 Azure AD 以支援下列案例：

- 從網際網路手動安裝 Configuration Manager 用戶端，並將它指派給 Configuration Manager 站台 (需要雲端管理閘道站台系統角色)。
- 使用 Azure AD 在網際網路上驗證用戶端，來存取您的 Configuration Manager 站台。 Azure AD 能取代設定及使用用戶端驗證憑證的需求。
- 深入站台中探索 Azure AD 使用者，以在集合及其他 Configuration Manager 作業中使用。

使用下列步驟可協助您完成這項作業：

- **步驟 1：設定雲端管理閘道**
- **步驟 2：在 Configuration Manager 雲端服務中設定 Azure 服務應用程式**
- **步驟 3：設定用戶端設定以使用 Azure AD 註冊 Windows 10 裝置**
- **步驟 4：使用 Azure Active Directory 身分識別安裝和註冊 Configuration Manager 用戶端**


## <a name="before-you-start"></a>開始之前

- 您必須擁有 Azure AD 租用戶。
- 您的裝置必須執行 Windows 10 並加入 Azure AD。 用戶端除了加入 Azure AD 之外，也可以加入網域。
- 除了管理點站台系統角色的[現有先決條件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)之外，您還必須確定在裝載此站台系統角色的電腦上啟用 **ASP.NET 4.5** (以及任何其他自動選取的選項)。
- 使用 Configuration Manager 來部署用戶端：
    - 為 HTTPS 模式至少設定一個管理點。
    - 設定雲端管理閘道。

## <a name="step-1-set-up-the-cloud-management-gateway"></a>步驟 1：設定雲端管理閘道

設定「雲端管理閘道」以讓用戶端從網際網路存取您的 Configuration Manager 站台，而無需使用憑證。 尋找下列主題中的說明： 

- [在 Configuration Manager 中進行雲端管理閘道規劃](/sccm/core/clients/manage/plan-cloud-management-gateway)。
- [設定 Configuration Manager 的雲端管理閘道](/sccm/core/clients/manage/setup-cloud-management-gateway)。
- [在 Configuration Manager 中監視雲端管理閘道](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway)。

## <a name="step-2-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>步驟 2：在 Configuration Manager 雲端服務中設定 Azure 服務應用程式

這會將您的 Configuration Manager 站台連線到 Azure AD，這也是本節中所有其他作業的先決條件。 

Azure AD 使用者探索可設定為*雲端管理*的一部分。 *設定要與 Configuration Manager 搭配使用的 Azure 服務*主題的步驟 **6** [建立要與 Configuration Manager 搭配使用的 Azure Web 應用程式](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp)程序中有詳細的程序說明。
    
完成此程序後，您已將 Configuration Manager 站台連線到 Azure AD。 

## <a name="step-3-configure-client-settings-to-register-windows-10-devices-with-azure-ad"></a>步驟 3：設定用戶端設定以使用 Azure AD 註冊 Windows 10 裝置

1.  使用[如何設定用戶端設定](/sccm/core/clients/deploy/configure-client-settings)中的資訊來設定下列用戶端設定 (可在 [雲端服務] 中找到) 區段。
    - **自動向 Azure Active Directory 註冊新加入 Windows 10 網域的裝置** - 設定為 [是]\ (預設值) 或 [否]。
    - **允許用戶端使用雲端管理閘道** - 設定為 [是] \(預設值) 或 [否]。
2.  將用戶端設定部署至所需的裝置集合。

若要確認裝置是否已加入 Azure AD，請在命令提示字元視窗中執行 **dsregcmd.exe /status** 命令。 如果裝置已加入 Azure AD 網域，結果中的 **AzureAdjoined** 欄位會顯示 **YES**。


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>步驟 4：使用 Azure Active Directory 身分識別安裝和註冊 Configuration Manager 用戶端

在開始之前，請先確定用戶端安裝來源檔案儲存在您想要安裝用戶端的裝置本機。 接著，參考[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually)中的指示，使用下列安裝命令列： 

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso AADCLIENTAPPID= AADRESOURCEURI=https://contososerver**

- **/NoCrlCheck**：如果您的管理點或雲端管理閘道使用非公用伺服器憑證，則用戶端可能會無法連線到 CRL 位置。
- **/Source**：本機資料夾：用戶端安裝檔的位置。
- **CCMHOSTNAME**：您網際網路管理點的名稱。 您可以從受管理用戶端上的命令提示字元執行 **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** 來找出此資訊。
- **SMSMP**：查閱管理點的名稱，管理點可能位於您的內部網路。
- **SMSSiteCode**：您 Configuration Manager 站台的站台碼。
- **AADTENANTID**、**AADTENANTNAME**：您連結到 Configuration Manager 之 Azure AD 租用戶的識別碼和名稱。 您可以從已加入 Azure AD 之裝置上的命令提示字元執行 dsregcmd.exe /status 來找出此資訊。
- **AADCLIENTAPPID**：Azure AD 用戶端應用程式識別碼。 如需有關如何尋找此資訊的說明，請參閱[使用入口網站來建立能夠存取資源的 Azure Active Directory 應用程式和服務主體](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key)。
- **AADResourceUri**：已上線之 Azure AD 伺服器應用程式的識別碼 URI。


## <a name="next-steps"></a>後續步驟

完成後，您可以繼續[監視及管理用戶端](/sccm/core/clients/manage/monitor-clients)。

