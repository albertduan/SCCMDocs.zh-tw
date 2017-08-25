---
title: "從網際網路安裝及指派用戶端 | Microsoft Docs"
description: "從網際網路安裝及指派 System Center Configuration Manager 用戶端。"
ms.custom: na
ms.date: 8/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: "14"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 7bbcece8a7a745b3b6cc9bbd8aa283963e2b738d
ms.sourcegitcommit: 49add91eebfeaba6d1d203d3cf9927b9cacdfc8e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/08/2017
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>安裝並指派 Configuration Manager Windows 10 用戶端，並使用 Azure AD 進行驗證

您可以使用 Configuration Manager 雲端服務搭配 Azure AD 以支援下列案例：

- 在 Windows 10 裝置上從網際網路手動安裝 Configuration Manager 用戶端，並將它指派給 Configuration Manager 站台 (需要雲端管理閘道站台系統角色)。
- 使用 Azure AD 驗證用戶端，來存取您的 Configuration Manager 站台。 Azure AD 能取代設定及使用用戶端驗證憑證的需求。
- 深入站台中探索 Azure AD 使用者，以在集合及其他 Configuration Manager 作業中使用。

使用下列步驟可協助您完成這項作業：

- **步驟 1：在 Configuration Manager 雲端服務中設定 Azure 服務應用程式並設定 Azure AD 使用者探索**
- **步驟 2：設定雲端管理閘道** (針對非內部部署用戶端而言為選擇性)
- **步驟 3：設定用戶端設定以使用 Azure AD 來加入 Windows 10 裝置，並啟用用戶端以使用「雲端管理閘道」**
- **步驟 4：使用 Azure Active Directory 身分識別安裝和註冊 Configuration Manager 用戶端**


## <a name="before-you-start"></a>開始之前

- 您必須擁有 Azure AD 租用戶。
- 您的裝置必須執行 Windows 10 並已加入 Azure AD，而且必須已使用 Azure AD 身分識別登入。 用戶端除了加入 Azure AD 之外，也可以加入網域。
- 除了管理點站台系統角色的[現有先決條件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)之外，您還必須確定在裝載此站台系統角色的電腦上啟用 **ASP.NET 4.5** (以及任何其他自動選取的選項)。
- 使用 Configuration Manager 來部署用戶端：
    - 若您要使用 Azure AD (而非用戶端憑證) 來驗證，請針對 HTTPS 模式設定至少一個管理點。
        若您要使用用戶端憑證而非「雲端管理閘道」，則 HTTPS 管理點為選擇性，但建議使用。 若您要使用 Azure AD 來驗證 (不論是內部部署或網際網路用戶端)，則需要 HTTPS 管理點。
    - 若要部署網際網路用戶端，請設定「雲端管理閘道」。 針對使用 Azure AD 來進行驗證的內部部署用戶端，您不需要設定「雲端管理閘道」。


## <a name="step-1-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>步驟 1：在 Configuration Manager 雲端服務中設定 Azure 服務應用程式

這會將您的 Configuration Manager 站台連線到 Azure AD，這也是本節中所有其他作業的先決條件。 

Azure AD 使用者探索可設定為*雲端管理*的一部分。 *設定要與 Configuration Manager 搭配使用的 Azure 服務*主題的步驟 **6** [建立要與 Configuration Manager 搭配使用的 Azure Web 應用程式](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp)程序中有詳細的程序說明。
    
完成此程序後，您已將 Configuration Manager 站台連線到 Azure AD。 

## <a name="step-2-set-up-the-cloud-management-gateway"></a>步驟 2：設定雲端管理閘道

設定「雲端管理閘道」以協助啟用此主題中所述的雲端管理案例。 尋找下列主題中的說明： 

- [在 Configuration Manager 中進行雲端管理閘道規劃](/sccm/core/clients/manage/plan-cloud-management-gateway)。
- [設定 Configuration Manager 的雲端管理閘道](/sccm/core/clients/manage/setup-cloud-management-gateway)。
- [在 Configuration Manager 中監視雲端管理閘道](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway)。

## <a name="step-3-configure-client-settings-to-join-windows-10-devices-with-azure-ad-and-enable-clients-to-use-the-cloud-management-gateway"></a>步驟 3：設定用戶端設定以使用 Azure AD 來加入 Windows 10 裝置，並啟用用戶端以使用「雲端管理閘道」

1.  使用[如何設定用戶端設定](/sccm/core/clients/deploy/configure-client-settings)中的資訊來設定下列用戶端設定 (可在 [雲端服務] 中找到) 區段。
    - **允許存取雲端發佈點** - 啟用此設定以協助網際網路型裝置取得必要的內容以安裝 Configuration Manager 用戶端。 若雲端發佈點上沒有內容可用，裝置可以從已連線到雲端管理閘道的管理點擷取內容。
    - **自動向 Azure Active Directory 註冊新加入 Windows 10 網域的裝置** - 設定為 [是]\ (預設值) 或 [否]。
    - **允許用戶端使用雲端管理閘道** - 設定為 [是] \(預設值) 或 [否]。
2.  將用戶端設定部署至所需的裝置集合。 不要將這些設定部署到使用者集合。

若要確認裝置是否已加入 Azure AD，請在命令提示字元視窗中執行 **dsregcmd.exe /status** 命令。 如果裝置已加入 Azure AD 網域，結果中的 **AzureAdjoined** 欄位會顯示 **YES**。


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>步驟 4：使用 Azure Active Directory 身分識別安裝和註冊 Configuration Manager 用戶端

若要安裝用戶端，請使用[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually)中的指示，使用下列安裝命令列： 

**ccmsetup.exe /mp&#58; https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=DFD SMSMP=https://SCCMDFPSS.contoso.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011DB47 AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d17026 AADRESOURCEURI=https://contososerver**

- **/MP** – 下載來源。 若從網際網路啟動，可以設定為 CMG。
- **CCMHOSTNAME**：您網際網路管理點的名稱。 您可以從受管理用戶端上的命令提示字元執行 **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** 來找出此資訊。
- **SMSSiteCode**：您 Configuration Manager 站台的站台碼。
- **SMSMP**：查閱管理點的名稱，管理點可能位於您的內部網路。
- **AADTENANTID**、**AADTENANTNAME**：您連結到 Configuration Manager 之 Azure AD 租用戶的識別碼和名稱。 您可以從已加入 Azure AD 之裝置上的命令提示字元執行 dsregcmd.exe /status 來找出此資訊。
- **AADCLIENTAPPID**：Azure AD 用戶端應用程式識別碼。 如需有關如何尋找此資訊的說明，請參閱[使用入口網站來建立能夠存取資源的 Azure Active Directory 應用程式和服務主體](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key)。
- **AADResourceUri**：已上線之 Azure AD 伺服器應用程式的識別碼 URI。 如需詳細資訊，請參閱[設定要與 Configuration Manager 搭配使用的 Azure 服務](/sccm/core/servers/deploy/configure/azure-services-wizard)。




## <a name="next-steps"></a>後續步驟

完成後，您可以繼續[監視及管理用戶端](/sccm/core/clients/manage/monitor-clients)。
