---
title: "規劃和設定應用程式管理 | System Center Configuration Manager"
description: "實作和設定必要的相依性以在 System Center Configuration Manager 中部署應用程式。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
caps.latest.revision: 13
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b1e21c2d6c90f02a1c616186b119b1a744d7f172


---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中規劃和設定應用程式管理

*適用對象：System Center Configuration Manager (最新分支)*

使用本主題中的資訊可協助您實作在 System Center Configuration Manager 中部署應用程式所需的相依性。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性  

|相依性|詳細資訊|  
|------------------|----------------------|  
|執行應用程式類別目錄網站點的站台系統伺服器、應用程式類別目錄 Web 服務點、管理點及發佈點均需要 Internet Information Services (IIS)。|如需這項需求的詳細資訊，請參閱[支援的設定](../../core/plan-design/configs/supported-configurations.md)。|  
|若為 Configuration Manager 註冊的行動裝置：|進行應用程式程式碼簽署以將其部署至行動裝置時，請勿使用以第 3 版範本 (Windows Server 2008 Enterprise Edition) 所產生的憑證。 此憑證範本所建立的憑證與行動裝置適用的 Configuration Manager 應用程式不相容。<br /><br /> 如果您的行動裝置應用程式使用 Active Directory 憑證服務進行應用程式程式碼簽署，請勿使用第 3 版的憑證範本。|  
|如果要自動建立使用者裝置親和性，就必須將用戶端設為稽核登入事件。|Configuration Manager 會從用戶端電腦上的本機安全性原則讀取下列兩種設定，以判定自動使用者裝置親和性：<br /><br /> **稽核帳戶登入事件**<br /><br /> **稽核登入事件**<br /><br /> 要自動建立使用者和裝置之間的關聯性，請務必在用戶端電腦上啟用這兩種設定。 您可以使用 Windows 群組原則設定這些設定。|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性   

|相依性|詳細資訊|  
|------------------|----------------------|  
|管理點|用戶端會連絡管理點，以下載用戶端原則、尋找內容，以及連線至應用程式類別目錄。<br /><br /> 如果用戶端無法存取管理點，就不能使用應用程式類別目錄。|  
|發佈點|您的階層中至少必須要有一個發佈點，才能將應用程式部署至用戶端。 站台伺服器預設會在標準安裝期間啟用一個發佈點站台。 發佈點的數量和位置因貴企業的特定需求而異。<br /><br /> 如需安裝發佈點及管理內容之方式的詳細資訊，請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。|  
|用戶端設計|許多用戶端設定會控制在用戶端上安裝應用程式的方式，以及用戶端上的一般使用者經驗。 其中包括下列用戶端設定：<br /><br /> - 電腦代理程式<br /><br /> - 電腦重新啟動<br /><br /> - 軟體部署<br /><br /> - 使用者和裝置親和性<br /><br /> 如需這些用戶端設定的詳細資訊，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md)。<br /><br /> 如需如何設定用戶端設定的資訊，請參閱[如何在 Configuration Manager 中設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。|  
|應用程式類別目錄：<br /><br /> 探索到的使用者帳戶|Configuration Manager 先探索到使用者之後，使用者才能檢視及要求應用程式類別目錄中的應用程式。 如需詳細資訊，請參閱[執行探索](/sccm/core/servers/deploy/configure/run-discovery)。|  
|使用 App-V 4.6 SP1 或更新版的用戶端執行虛擬應用程式|用戶端電腦必須安裝 App-V 4.6 SP1 或更新版本的用戶端，才能在 Configuration Manager 中順利建立虛擬應用程式。<br /><br /> 此外，您必須先使用知識庫 [文件 2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) 中說明的 Hotfix 更新 App-V 用戶端，才能順利部署虛擬應用程式。|  
|應用程式類別目錄 Web 服務點|應用程式類別目錄 Web 服務點是一個站台系統角色，可針對在應用程式類別目錄中能夠使用的軟體庫軟體提供相關資訊。<br /><br /> 如需設定此站台系統角色方式的資訊，請參閱本主題中的 [Configure Software Center and the Application Catalog (Windows PCs only)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) (設定軟體中心和應用程式類別目錄 (僅限 Windows 電腦))。|  
|應用程式類別目錄網站點|應用程式類別目錄網站點是一個站台系統角色，可提供可用軟體清單給使用者。<br /><br /> 如需設定此站台系統角色方式的資訊，請參閱本主題中的 [Configure Software Center and the Application Catalog (Windows PCs only)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) (設定軟體中心和應用程式類別目錄 (僅限 Windows 電腦))。|  
|Reporting Services 點|您必須先安裝並設定 Reporting Services 點，才能使用 Configuration Manager 中的報告管理應用程式。<br /><br /> 如需詳細資訊，請參閱 [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md) (System Center Configuration Manager 中的報告)。|  
|應用程式管理的安全性權限|您必須具備下列安全性權限，才能管理應用程式。<br /><br /> [應用程式作者] 安全性角色包括上述所有權限，在 Configuration Manager 中建立、修改及淘汰應用程式時需要這些權限。<br /><br /> **部署應用程式：**<br /><br /> [應用程式部署管理員] 安全性角色包括上述所有權限，在 Configuration Manager 中部署應用程式時需要這些權限。<br /><br /> [應用程式系統管理員]  安全性角色包含 [應用程式作者]  和 [應用程式部署管理員]  等安全性角色的所有權限。<br /><br /> 如需詳細資訊，請參閱[設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>設定軟體中心和應用程式類別目錄 (僅限 Windows 電腦)  

 在 System Center Configuration Manager 中，現在您有使用者如何變更設定以及瀏覽和安裝應用程式的兩個選項：  

-   **新的軟體中心** - 新的軟體中心擁有全新的現代化外觀，其中包含的應用程式先前只出現在 Silverlight 相依應用程式類別目錄 (使用者可用的應用程式)，而現在出現在軟體中心的 [應用程式]  索引標籤下。 應用程式類別目錄還是可以使用軟體中心之 [安裝狀態]  索引標籤下的連結進行存取。  

     您可以啟用用戶端設定 [電腦代理程式] **電腦代理程式** > **使用新的軟體中心**。  

    > [!IMPORTANT]  
    >  雖然使用者不再需要連線至「應用程式類別目錄」，但是您還是必須如下所述設定「應用程式類別目錄」網站點和「應用程式類別目錄」Web 服務點。  

-   **先前的軟體中心和應用程式類別目錄** - 根據預設，使用者會繼續連線至舊版的軟體中心以及連線至應用程式類別目錄 (需要啟用 Silverlight 功能的網頁瀏覽器) 來瀏覽可用的應用程式。  

 不論您選擇使用哪個版本，當您在 Windows 電腦上安裝 Configuration Manager 用戶端時，都會自動安裝軟體中心。  

> [!TIP]  
>  使用者看到的軟體中心版本視 Configuration Manager 用戶端設定而定。 這可讓您根據部署至集合的自訂用戶端設定來彈性地控制所使用的版本。  

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>安裝和設定應用程式類別目錄和軟體中心的步驟  

> [!IMPORTANT]  
>  在執行這些步驟之前，請確定您已符合上面所列的所有必要條件。  

|步驟|詳細資料|詳細資訊|  
|-----------|-------------|----------------------|  
|**步驟 1：** 如果您將使用 HTTPS 連線，請確定您已將 Web 伺服器憑證部署至站台系統伺服器。|將 Web 伺服器憑證部署至將執行應用程式類別目錄網站點，和應用程式類別目錄 Web 服務點的站台系統伺服器。<br /><br /> 此外，如果您要讓用戶端從網際網路存取應用程式類別目錄，請將 Web 伺服器憑證部署到至少一個管理點站台系統伺服器，並且設定該憑證用於來自網際網路的用戶端連線。|如需憑證需求的資訊，請參閱 [PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)。|  
|**步驟 2：** 如要使用用戶端 PKI 憑證與管理點連線，請將用戶端驗證憑證部署至用戶端電腦。|雖然用戶端不一定要使用用戶端 PKI 憑證連線至應用程式類別目錄，但是必須先連線到管理點，才能使用應用程式類別目錄。 在下列案例中，您必須將用戶端驗證憑證部署至用戶端電腦：<br /><br /> - 內部網路上的所有管理點均只接受 HTTPS 用戶端連線。<br /><br /> - 用戶端將從網際網路連線到「應用程式類別目錄」。|如需憑證需求的資訊，請參閱 [PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)。|  
|**步驟 3：** 安裝及設定應用程式類別目錄 Web 服務點和應用程式類別目錄網站。|您必須將這兩個站台系統角色安裝到相同站台上。 您不一定要將它們安裝到同一部站台系統伺服器上，或相同的 Active Directory 樹系中。 不過，應用程式類別目錄 Web 服務點必須與站台資料庫位於相同的樹系中。|如需站台系統角色放置的詳細資訊，請參閱[規劃站台系統伺服器和站台系統角色](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)。<br /><br /> 若要設定應用程式類別目錄 Web 服務點和應用程式類別目錄網站點，請參閱**步驟 3：安裝及設定應用程式類別目錄站台系統角色**。|  
|**步驟 4：** 設定應用程式類別目錄和軟體中心的用戶端設定。|如果您希望所有使用者擁有相同的設定，請設定預設用戶端設定。 否則，請針對特定集合設定自訂用戶端設定。|如需用戶端設定的詳細資訊，請參閱[關於 Configuration Manager 中的用戶端設定](../../core/clients/deploy/about-client-settings.md)。<br /><br /> 如需如何設定這些用戶端設定的資訊，請參閱**步驟 4：設定應用程式類別目錄和軟體中心的用戶端設定**。|  
|**步驟 5：** 確認應用程式類別目錄可運作。|您可以直接從瀏覽器或軟體中心存取應用程式類別目錄。|請參閱**步驟 5：確認應用程式類別目錄可運作**。|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>安裝及設定應用程式類別目錄和軟體中心的補充程序  
 當上表中的步驟需要補充程序時，可利用下列資訊。  

###  <a name="step-3-installing-and-configuring-the-application-catalog-site-system-roles"></a>步驟 3：安裝及設定應用程式類別目錄站台系統角色  
 這些程序會設定應用程式類別目錄的站台系統角色。 根據您要安裝新的站台系統伺服器，或是使用現有站台系統伺服器，從下列 2 項程序選擇其中之一：  

> [!NOTE]  
>  應用程式類別目錄無法安裝到次要站台或管理中心網站上。  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>安裝及設定應用程式類別目錄站台系統：新增網站系統伺服器  

1.  在 Configuration Manager 主控台中，按一下 [管理] > [站台設定] > [伺服器和站台系統角色]。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立網站系統伺服器] 。  

4.  在 [一般]  頁面上，指定網站系統的一般設定，然後按 [下一步] 。  

    > [!TIP]  
    >  如果您想要讓用戶端電腦透過網際網路存取應用程式類別目錄，請指定網際網路完整網域名稱 (FQDN)。  

5.  在 [系統角色選取]  頁面上，從可用角色清單中選取 [應用程式類別目錄 Web 服務點]  和 [應用程式類別目錄網站點]  ，然後按 [下一步] 。  

6.  完成精靈。  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>安裝及設定應用程式類別目錄站台系統：現有的網站系統伺服器  

1.  在 Configuration Manager 主控台中，按一下 [管理] > [站台設定] > [伺服器和站台系統角色]，然後選取要用於應用程式類別目錄的伺服器。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [新增網站系統角色] 。  

4.  在 [一般]  頁面上，指定網站系統的一般設定，然後按 [下一步] 。  

    > [!TIP]  
    >  如果您想要讓用戶端電腦透過網際網路存取應用程式類別目錄，請指定網際網路完整網域名稱 (FQDN)。  

5.  在 [系統角色選取]  頁面上，從可用角色清單中選取 [應用程式類別目錄 Web 服務點]  和 [應用程式類別目錄網站點]  ，然後按 [下一步] 。  

6.  完成精靈。  

 藉由使用狀態訊息和檢閱記錄檔，確認這些站台系統角色的安裝：  

1.  狀態訊息：使用元件 **SMS_PORTALWEB_CONTROL_MANAGER** 和 **SMS_AWEBSVC_CONTROL_MANAGER**。  

     例如， **SMS_PORTALWEB_CONTROL_MANAGER** 的狀態識別碼 **1015** ，確認站台元件管理員已成功安裝在應用程式類別目錄網站點。  

2.  記錄檔：搜尋 **SMSAWEBSVCSetup.log** 和 **SMSPORTALWEBSetup.log**。  

     如需更詳細的資訊，請搜尋記錄檔 **awebsvcMSI.log** 和 **portlwebMSI.log**。  

###  <a name="step-4-configuring-the-client-settings-for-the-application-catalog-and-software-center"></a>步驟 4：設定應用程式類別目錄和軟體中心的用戶端設定  
 此程序會設定應用程式類別目錄和軟體中心的預設用戶端設定，這些設定將套用至階層內所有裝置。 如果您只要將這些設定套用至部分裝置，可以建立自訂用戶端設定，並將它部署至包含將擁有特定設定之裝置的集合。 如需如何建立自訂裝置設定的詳細資訊，請參閱 [How to Create and Deploy Custom Client Settings](../../core/clients/deploy/configure-client-settings.md#BKMK_CustomClientSettings) 主題中的 [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) 一節。  

1.  在 Configuration Manager 主控台中按一下 [管理] > [用戶端設定] > [預設用戶端設定]。  

3.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

4.  檢閱並設定與使用者通知、應用程式類別目錄和軟體中心相關的設定。 例如：  

    1.  [電腦代理程式] 群組：  

        -   **預設應用程式類別目錄網站點**  

        -   **將預設應用程式類別目錄網站新增至 Internet Explorer 的信任的網站區域**  

        -   **顯示於軟體中心的組織名稱**  

            > [!TIP]  
            >  若要指定應用程式類別目錄中顯示的組織名稱及設定網站佈景主題，請使用應用程式類別目錄網站內容中的 [自訂]  索引標籤。  

        -   **使用新的軟體中心** - 如果您想要使用新的軟體中心，讓使用者瀏覽以及安裝可用的應用程式，而不需要存取應用程式類別目錄 (這需要啟用 Silverlight 功能的網頁瀏覽器)，請設為 [是]  。  

        -   **安裝權限**  

        -   **針對新部署顯示通知**  

    2.  [電源管理] 群組：  

        -   **允許使用者從電源管理排除其裝置**  

    3.  [遠端工具] 群組：  

        -   **使用者可以在軟體中心變更原則或通知設定**  

    4.  [使用者和裝置親和性] 群組：  

        -   **允許使用者定義其主要裝置**  

    > [!NOTE]  
    >  如需用戶端設定的詳細資訊，請參閱 [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md)。  

5.  按一下 [確定]  ，關閉 [預設用戶端設定]  對話方塊。  

 用戶端電腦將會在下一次下載用戶端原則時進行這些設定。 若要起始單一用戶端的原則擷取，請參閱[如何管理用戶端](../../core/clients/manage/manage-clients.md)。  

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>步驟 5：確認應用程式類別目錄可運作  
 利用下列程序確認應用程式類別目錄可運作。 您可以直接從瀏覽器或軟體中心存取應用程式類別目錄。  

> [!NOTE]  
>  應用程式類別目錄需要 Microsoft Silverlight，它會自動安裝為 Configuration Manager 用戶端必要條件。 如果您使用未安裝 Configuration Manager 用戶端的電腦直接從瀏覽器存取應用程式類別目錄，請先確認電腦上已安裝 Microsoft Silverlight。  

> [!TIP]  
>  缺少必要條件是應用程式類別目錄安裝後未能正常運作的最常見原因。 請確認應用程式類別目錄站台系統角色的的系統角色必要條件。 您可以使用[支援的設定](../../core/plan-design/configs/supported-configurations.md)主題來完成此作業。  

> [!NOTE]  
>  如果您使用網域系統管理員帳戶登入，將不會顯示來自 Configuration Manager 用戶端的訊息通知 (例如，指出新的軟體已可供使用的訊息)。  

### <a name="to-access-the-application-catalog-directly-from-a-browser"></a>直接從瀏覽器存取應用程式類別目錄  

-   在瀏覽器中，輸入應用程式類別目錄網站的位址，並確認網頁中顯示三個索引標籤：[應用程式類別目錄] 、[我的應用程式要求] 和 [我的裝置] 。  

     選取並使用下列適當的應用程式類別目錄位址，其中 <伺服器\> 是電腦名稱、內部網路 FQDN 或網際網路 FQDN：  

    -   HTTPS 用戶端連線和預設站台系統角色設定：**https://<伺服器\>/Configuration Manager 應用程式類別目錄**  

    -   HTTPS 用戶端連線和預設站台系統角色設定：**https://<伺服器\>/Configuration Manager 應用程式類別目錄**  

    -   HTTPS 用戶端連線和自訂站台系統角色設定：**https://<伺服器\>:<連接埠\>/<Web 應用程式名稱\>**  

    -   HTTPS 用戶端連線和自訂站台系統角色設定：**http://<伺服器\>:<連接埠\>/<Web 應用程式名稱\>**  

### <a name="to-access-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>從軟體中心存取應用程式類別目錄 (不會套用至新版的軟體中心)  

1.  在用戶端電腦上，按一下 **[開始]** > **[所有程式]** > **[Microsoft System Center 2012]** > **[Configuration Manager]** > **[軟體中心]**。  

2.  如果您之前設定軟體中心的組織名稱做為用戶端設定，請確認該名稱依照指定顯示。  

3.  按一下 [從應用程式類別目錄尋找其他應用程式]  ，並確認頁面中顯示三個索引標籤：[應用程式類別目錄] 、[我的應用程式要求] 和 [我的裝置] 。  

> [!WARNING]  
>  應用程式類別目錄站台系統角色安裝完成後，從軟體中心按一下 [從應用程式類別目錄尋找其他應用程式]  連結並不會立即看見應用程式類別目錄。 在用戶端下一次下載其用戶端原則，或是應用程式類別目錄站台系統角色安裝後達到 25 小時後，才能在軟體中心內看見應用程式類別目錄。  



<!--HONumber=Nov16_HO1-->


