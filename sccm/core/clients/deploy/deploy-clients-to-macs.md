---
title: "部署 Mac 用戶端 | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中將用戶端部署至 Mac 電腦。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: eae9e76085a95cb09fe01a32fd4b57294bc1cc20


---
# <a name="how-to-deploy-clients-to-macs-in-system-center-configuration-manager"></a>How to deploy clients to Macs in System Center Configuration Manager

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 中，進行 Mac 電腦的用戶端安裝和管理需要公開金鑰基礎結構 (PKI) 憑證。 Configuration Manager 可以使用含有企業憑證授權單位 (CA) 的 Microsoft 憑證服務和 Configuration Manager 註冊點，以及註冊 Proxy 點站台系統角色來要求並安裝使用者用戶端憑證。 或者，如果憑證符合 Configuration Manager 的需求，您可以單獨從 Configuration Manager 要求及安裝電腦憑證。 PKI 憑證會使用相互驗證及加密的資料傳送，對 Mac 電腦和 Configuration Manager 站台之間的通訊進行加密。  

> [!IMPORTANT]  
>  Configuration Manager Mac 用戶端一律會執行憑證撤銷檢查，和在 Windows 上執行的 Configuration Manager 用戶端不一樣的是，您不能停用此憑證撤銷清單 (CRL) 檢查功能。  
>   
>  如果 Mac 用戶端因為找不到 CRL 而無法確認伺服器憑證的憑證撤銷狀態，它們將無法順利連線至 Configuration Manager 站台系統，例如管理點和發佈點。 特別是在不同樹系中用於發行憑證授權單位的 Mac 用戶端，請檢查您的 CRL 設計以確定 Mac 用戶端可以找到並連線到 CRL 發佈點 (CDP) 以確保網站系統伺服器的連線。  

 您必須先決定要如何安裝用戶端憑證，才能在 Mac 電腦上安裝 Configuration Manager 用戶端：  

-   利用 CMEnroll 工具並依照本主題下一節中的步驟，使用 Configuration Manager 註冊。 註冊程序不支援自動憑證更新，所以您必須在安裝的憑證到期前，先重新註冊 Mac 電腦。  

-   使用與 Configuration Manager 獨立的憑證要求和安裝方法。 如需這種安裝方法的詳細資訊，請參閱本主題中的 [Use a certificate request and installation method that is independent from Configuration Manager](#BKMK_ManualCertifcateInstallation) 一節。  

> [!NOTE]  
>  如需 Mac 用戶端憑證需求及其他支援 Mac 電腦所需 PKI 憑證的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

 Mac 用戶端會自動指派給管理它們的 Configuration Manager 站台。 即使通訊受限於內部網路，Mac 用戶端還是會安裝為僅限網際網路的用戶端。 此用戶端設定表示當您將這些網站系統角色設定為允許來自網際網路的用戶端連線時，它們將會與其指派的網站內的網站系統角色 (管理點和發佈點) 通訊。 Mac 電腦不會與其指派的網站以外的網站系統角色通訊。  

> [!IMPORTANT]  
>  Configuration Manager Mac 用戶端無法用於連線到設定為使用資料庫複本的管理點。 如需資料庫複本的資訊，請參閱 [System Center Configuration Manager 管理點的資料庫複本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

 依照以下各節來安裝、設定及管理用於 Configuration Manager 的 Mac 電腦：  

-   [為 Mac 安裝及設定用戶端的步驟](#InstallSteps)  

-   [Uninstalling the Mac client](#uninstallMacClient)  

-   [Renewing the Mac client certificate](#BKMK_Renew)  

-   [Use a certificate request and installation method that is independent from Configuration Manager](#BKMK_ManualCertifcateInstallation)  

##  <a name="a-nameinstallstepsa-steps-to-install-and-configure-the-client-for-macs"></a><a name="InstallSteps"></a> 為 Mac 安裝及設定用戶端的步驟  

> [!IMPORTANT]  
>  請先確定您的 Mac 電腦符合必要條件，再執行這些步驟。 如需詳細資訊，請參閱 [Mac 的支援作業系統](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)。  

### <a name="step-1-deploy-a-web-server-certificate-to-site-system-servers"></a>步驟 1：將 Web 伺服器憑證部署至站台系統伺服器  
 這些站台系統可能已擁有其他 Configuration Manager 用戶端的這個憑證。 如果不是如此，請將 Web 伺服器憑證部署至裝載下列網站系統角色的電腦：  

-   管理點  

-   發佈點  

-   註冊點  

-   註冊 Proxy 點  

> [!IMPORTANT]  
>  Web 伺服器憑證必須包含網站系統內容中指定的網際網路 FQDN。  
>   
>  這並不代表伺服器必須能夠從網際網路存取才支援 Mac 電腦。 如果您不需要以網際網路為基礎的用戶端管理，您可以將網際網路 FQDN 指定為內部網路 FQDN 值。  

 如需建立及安裝此 Web 伺服器憑證的部署範例，請參閱[為執行 IIS 的站台系統部署 Web 伺服器憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)。  

> [!IMPORTANT]  
>  請確定您在管理點、發佈點和註冊 Proxy 點的 Web 伺服器憑證中，指定站台系統的網際網路 FQDN 值。  

### <a name="step-2-deploy-a-client-authentication-certificate-to-site-system-servers"></a>步驟 2：將用戶端驗證憑證部署至站台系統伺服器  
 這些網站系統可能已擁有 Configuration Manager 功能的這個憑證。 如果不是如此，請將用戶端驗證憑證部署至裝載下列網站系統角色的電腦：  

-   管理點  

-   發佈點  

 如需建立及安裝管理點用戶端憑證的部署範例，請參閱[部署 Windows 電腦的用戶端憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)。  

 如需建立及安裝管理點用戶端憑證的部署範例，請參閱[部署發佈點的用戶端憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)。  

### <a name="step-3-prepare-the-client-certificate-template-for-macs"></a>步驟 3：準備 Mac 的用戶端憑證範本。  

> [!NOTE]  
>  若要執行 Configuration Manager 註冊工具，您必須擁有 Active Directory 使用者帳戶。  

 憑證範本必須擁有將在 Mac 電腦上註冊憑證之使用者帳戶的 [讀取]  和 [註冊]  權限。  

 請參閱[部署 Mac 電腦的用戶端憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1)。  

### <a name="step-4-configure-the-management-point-and-distribution-point"></a>步驟 4：設定管理點和發佈點  
 為管理點設定下列選項：  

-   HTTPS  

-   允許用戶端從網際網路連線  

    > [!NOTE]  
    >  此設定值是管理 Mac 電腦所必備。 然而，這並不代表網站系統伺服器必須能夠從網際網路存取。  

-   允許行動裝置和 Mac 電腦使用此管理點  

 雖然在 Mac 電腦上安裝用戶端不需要用到發佈點，但是如果要在安裝 Configuration Manager 用戶端後將軟體部署到這些 Mac 電腦，您必須設定發佈點，以允許用戶端從網際網路連線。  

 此程序會將現有的管理點及發佈點設定為支援 Mac 電腦。 請確定已使用網際網路 FQDN 設定執行管理點和發佈點的網站系統伺服器，再開始執行此程序。 如果這些網站系統伺服器不支援以網際網路為基礎的用戶端管理，您可以將內部網路 FQDN 指定為網際網路 FQDN 值。 此外，這些網站系統角色必須位於主要網站中。  

##### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>設定管理點及發佈點以支援 Mac  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [網站設定] ，選取 [伺服器和網站系統角色] ，然後選取裝載要設定之網站系統角色的伺服器。  

3.  在詳細資料窗格中，以滑鼠右鍵按一下 [管理點] ，按一下 [角色內容] ，然後在 [管理點內容]  對話方塊中設定下列選項，再按一下 [確定] ：  

    1.  選取 [HTTPS] 。  

    2.  選取 [僅允許網際網路用戶端連線]  或 [允許內部網路和網際網路用戶端連線] 。 即使無法從網際網路存取網站系統伺服器，這些選項仍必須在網站系統內容中指定網際網路 FQDN 。  

    3.  選取 [允許行動裝置和 Mac 電腦使用此管理點] 。  

4.  在詳細資料窗格中，以滑鼠右鍵按一下 [發佈點] ，按一下 [角色內容] ，然後在 [發佈點內容]  對話方塊中設定下列選項，再按一下 [確定] ：  

    -   選取 [HTTPS] 。  

    -   選取 [僅允許網際網路用戶端連線]  或 [允許內部網路和網際網路用戶端連線] 。 即使無法從網際網路存取網站系統伺服器，這些選項仍必須在網站系統內容中指定網際網路 FQDN 。  

    -   按一下 [匯入憑證] ，瀏覽匯出的用戶端發佈點憑證檔案，然後指定密碼。  

5.  針對主要網站中您要搭配 Mac 電腦使用的所有管理點和發佈點，重複執行此程序的步驟 2 到 4。  

### <a name="step-5-configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>步驟 5：設定註冊 Proxy 點和註冊點  
 您必須在相同網站中安裝這兩種網站系統角色，但不需要在相同網站系統伺服器或相同 Active Directory 樹系中安裝它們。  

 如需站台系統角色放置和考量的詳細資訊，請參閱[為 System Center Configuration Manager 規劃站台系統伺服器和站台系統角色](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)中的[站台系統角色](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)。  

 這些程序會設定網站系統角色以支援 Mac 電腦。 根據您是否要安裝新網站伺服器以支援 Mac 電腦，或是使用現有的網站系統伺服器，從這些程序中選擇其中一種程序來執行：  

-   [安裝和設定註冊站台系統：新的站台系統伺服器](#BKMK_HowtoInstallEnrollmentSiteSystems_new)  

-   [安裝和設定註冊站台系統：現有的站台系統伺服器](#BKMK_HowtoInstallEnrollmentSiteSystems_existing)  

####  <a name="a-namebkmkhowtoinstallenrollmentsitesystemsnewa-to-install-and-configure-the-enrollment-site-systems-new-site-system-server"></a><a name="BKMK_HowtoInstallEnrollmentSiteSystems_new"></a> 安裝和設定註冊站台系統：新的站台系統伺服器  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [伺服器和網站系統角色]   

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立網站系統伺服器] 。  

4.  在 [一般]  頁面上，指定網站系統的一般設定，然後按 [下一步] 。  

    > [!IMPORTANT]  
    >  請確定即使無法從網際網路存取網站系統伺服器，您仍有指定網際網路 FQDN 值。 如果您因為網站系統伺服器無法從網際網路存取而沒有網際網路 FQDN，您可以將內部網路 FQDN 指定為網際網路 FQDN。 Mac 電腦永遠會連線到網際網路 FQDN，即使其位於內部網路亦是如此。  

5.  在 [系統角色選取]  頁面上，從可用角色的清單中選取 [註冊 Proxy 點]  和 [註冊點]  ，然後按 [下一步] 。  

6.  在 [註冊 Proxy 點]  頁面檢閱設定值，並進行所需的變更，然後按 [下一步] 。  

7.  在 [註冊點設定]  頁面檢閱設定值，並進行所需的變更，然後按 [下一步] 。  

8.  完成精靈。  

####  <a name="a-namebkmkhowtoinstallenrollmentsitesystemsexistinga-to-install-and-configure-the-enrollment-site-systems-existing-site-system-server"></a><a name="BKMK_HowtoInstallEnrollmentSiteSystems_existing"></a> 安裝和設定註冊站台系統：現有的站台系統伺服器  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [網站設定] ，選取 [伺服器和網站系統角色] ，然後選取您要用於支援 Mac 電腦的伺服器。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [新增網站系統角色] 。  

4.  在 [一般]  頁面上，指定網站系統的一般設定，然後按 [下一步] 。  

    > [!IMPORTANT]  
    >  請確定即使無法從網際網路存取網站系統伺服器，您仍有指定網際網路 FQDN 值。 如果您因為網站系統伺服器無法從網際網路存取而沒有網際網路 FQDN，您可以將內部網路 FQDN 指定為網際網路 FQDN。 Mac 電腦永遠會連線到網際網路 FQDN，即使其位於內部網路亦是如此。  

5.  在 [系統角色選取]  頁面上，從可用角色的清單中選取 [註冊 Proxy 點]  和 [註冊點]  ，然後按 [下一步] 。  

6.  在 [註冊 Proxy 點]  頁面檢閱設定值，並進行所需的變更，然後按 [下一步] 。  

7.  在 [註冊點設定]  頁面檢閱設定值，並進行所需的變更，然後按 [下一步] 。  

8.  完成精靈。  

### <a name="step-6-optional-install-the-reporting-services-point"></a>步驟 6：選用：安裝 Reporting Services 點  
 如果要執行 Mac 電腦的報告，請安裝 Reporting Services 點。  

 如需安裝及設定 Reporting Services 點方式的詳細資訊，請參閱[在 Configuration Manager 中設定報告](../../../core/servers/manage/configuring-reporting.md)。  

### <a name="step-7-configure-client-settings-for-enrollment"></a>步驟 7：設定註冊時使用的用戶端設定  
 您必須使用預設用戶端設定來設定 Mac 電腦的註冊；您無法使用自訂用戶端設定。  

 如需用戶端設定的詳細資訊，請參閱 [About client settings in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md)。  

 Configuration Manager 需要使用此步驟才能在 Mac 電腦上要求及安裝憑證。  

##### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>為 Configuration Manager 設定預設用戶端設定，以註冊 Mac 的憑證  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] 。  

3.  按一下 [預設用戶端設定] 。  

    > [!IMPORTANT]  
    >  您不能使用自訂用戶端設定進行註冊設定，您必須使用預設用戶端設定。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  選取 [註冊]  區段，然後設定下列使用者設定：  

    1.  **允許使用者註冊行動裝置和 Mac 電腦：是**  

    2.  **註冊設定檔：** 按一下 [設定設定檔] 。  

6.  在 [行動裝置註冊設定檔]  對話方塊中，按一下 [建立] 。  

7.  在 [建立註冊設定檔]  對話方塊中，輸入此註冊設定檔的名稱，然後設定 [管理網站碼] 。 選取包含要管理 Mac 電腦之管理點的 Configuration Manager 主要站台。  

    > [!NOTE]  
    >  如果您無法選取網站，請確認網站內至少有一個管理點已設定為支援行動裝置。  

8.  按一下 [加入] 。  

9. 在 [新增行動裝置的憑證授權單位]  對話方塊中， 選取負責發行憑證給 Mac 電腦的憑證授權單位 (CA) 伺服器，然後按一下 [確定] 。  

10. 於 [建立註冊設定檔]  對話方塊中， 選取您於步驟 3 所建立的 Mac 電腦憑證範本，然後按一下 [確定] 。  

11. 按一下 [確定]  關閉 [註冊設定檔]  對話方塊，接著按一下 [確定]  關閉 [預設用戶端設定]  對話方塊。  

    > [!TIP]  
    >  若要變更用戶端原則間隔，請使用 [用戶端原則]  用戶端設定群組中的 [用戶端原則輪詢間隔]  用戶端設定。  

 所有使用者必須先完成這些設定，以供下次下載用戶端原則時使用。 若要起始單一用戶端的原則擷取，請參閱[起始 Configuration Manager 用戶端的原則抓取](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

 除了註冊用戶端設定，請確定您已設定下列 Configuration Manager 用戶端裝置設定︰  

-   **硬體清查**：啟用並設定此用戶端設定，以從 Mac 和 Windows 用戶端電腦收集硬體清查。 如需詳細資訊，請參閱[如何擴充 System Center Configuration Manager 中的硬體清查](../../../core/clients/manage/inventory/extend-hardware-inventory.md)。  

-   **相容性設定**：啟用並設定此用戶端設定，以於 Mac 和 Windows 用戶端電腦上評估和補救設定。 如需詳細資訊，請參閱[規劃和設定相容性設定](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)。  

> [!NOTE]  
>  如需 Configuration Manager 用戶端設定的詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端設定](../../../core/clients/deploy/configure-client-settings.md)。  

### <a name="step-8-download-the-client-source-files-for-macs"></a>步驟 8：下載 Mac 的用戶端來源檔案  
 您必須先下載並安裝下列程式，才能在 Mac 上安裝和管理 Configuration Manager 用戶端︰  

-   **Ccmsetup**：使用此應用程式在組織的 Mac 電腦上安裝 Configuration Manager 用戶端。  

-   **CMDiagnostics**：使用此工具在組織的 Mac 電腦上收集與 Configuration Manager 用戶端相關的診斷資訊。  

-   **CMUninstall**：使用此工具在組織的 Mac 電腦上解除安裝 Configuration Manager 用戶端。  

-   **CMAppUtil**：使用此工具來轉換 Apple 應用程式套件的格式，以部署為 Configuration Manager 應用程式。  

-   **CMEnroll**：使用此工具來要求並安裝 Mac 電腦的用戶端憑證，才能安裝 Configuration Manager 用戶端。  

> [!IMPORTANT]  
>  為 Mac 電腦安裝新的用戶端時，您可能必須同時安裝 Configuration Manager 更新，以反映 Configuration Manager 主控台中的新用戶端資訊。  

##### <a name="to-download-and-install-the-mac-os-x-client-files"></a>下載並安裝 Mac OS X 用戶端檔案  

1.  下載 Mac OS X 用戶端檔案套件 **ConfigmgrMacClient.msi**，並將它儲存到執行 Windows 的電腦中。  

     Configuration Manager 安裝媒體並未提供這個檔案。 您可以從 [Microsoft Download Center (Microsoft 下載中心)](http://go.microsoft.com/fwlink/?LinkID=525184)下載此檔案。  

2.  在 Windows 電腦上執行剛才下載的 **ConfigmgrMacClient.msi** 檔案，將 Mac 用戶端套件 Macclient.dmg 解壓縮至本機磁碟機 (預設為 **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**)。  

3.  將 Macclient.dmg 檔案複製到 Mac 電腦上的資料夾。  

4.  在 Mac 電腦上執行剛才下載的 Macclient.dmg 檔案，將檔案解壓縮至本機磁碟機的資料夾。  

5.  於該資料夾中，確保檔案 Ccmsetup 和 CMClient.pkg 已解壓縮，並且已建立命名為 Tools 的資料夾，其中包含 CMDiagnostics、CMUninstall、CMAppUtil 和 CMEnroll 工具。  

### <a name="step-9-install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>步驟 9：在 Mac 上安裝用戶端，然後註冊用戶端憑證  
 此程序將安裝用戶端，接著使用 CMEnroll 工具來要求並安裝 Mac 電腦的用戶端憑證，您才能使用 Configuration Manager 來管理此電腦。  

 您可以使用 Mac [電腦註冊精靈] 註冊用戶端，而不需要使用 CMEnroll 工具。 如需詳細資訊，請參閱下列程序。  

##### <a name="to-install-the-client-and-enroll-the-certificate-by-using-the-cmenroll-tool"></a>使用 CMEnroll 工具來安裝用戶端與註冊憑證  

1.  在 Mac 電腦上，導覽至您由 Microsoft Download Center 下載並解壓縮的 Macclient.dmg 檔案內容資料夾位置。  

2.  請輸入下列命令列︰ **sudo ./ccmsetup**  

3.  請等候直至您看見 [已完成安裝]  訊息。 雖然安裝程式會顯示必須重新啟動的訊息，不過您並不需要重新啟動，請繼續執行下一個步驟。  

4.  從 Mac 電腦上的 [工具] 資料夾中輸入下列命令：**sudo ./CMEnroll -s &lt;註冊 Proxy 伺服器名稱> -ignorecertchainvalidation -u &lt;使用者名稱'>**  

    > [!NOTE]  
    >  用戶端安裝之後，Mac [電腦註冊精靈] 便會開啟以協助您註冊 Mac 電腦。 若要使用此方法註冊用戶端，請參閱本主題的 [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) 。  

     然後您會收到輸入 Active Directory 使用者帳戶密碼的提示。  

    > [!IMPORTANT]  
    >  當您輸入此命令時，您實際上會收到輸入兩個密碼的提示：第一個提示是針對執行命令的進階使用者帳戶。 第二個提示是針對 Active Directory 使用者帳戶。 提示外觀看似相同，所以請確認是否以正確順序輸入密碼。  

     使用者名稱的格式可以如下︰  

    -   '網域\名稱'。 例如：'contoso\mnorth'  

    -   'user@domain'. 例如： 'mnorth@contoso.com'  

     使用者名稱和對應密碼必須符合 Active Directory 使用者帳戶，並具有 Mac 用戶端憑證範本的讀取和註冊權限。  

     範例：若註冊 Proxy 點伺服器命名為 **server02.contoso.com**，且 **contoso\mnorth** 的使用者名稱已獲授與 Mac 用戶端憑證範本的權限，請輸入如下︰**sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!IMPORTANT]  
    >  如果使用者名稱包含任何 **&lt;>"+=,** 字元，註冊會失敗。  
    >   
    >  若要修正此問題，請使用不包含這些字元的使用者名稱來取得超出訊號範圍的憑證。  

    > [!NOTE]  
    >  若要讓使用者能體驗更順暢的使用經驗，您可以編寫安裝步驟和命令列，讓使用者只需要輸入使用者名稱和密碼。  

5.  請等候直至您看見 [已順利註冊]  訊息。  

6.  若要將註冊的憑證限制到 Configuration Manager，請在 Mac 電腦上開啟終端機視窗，並進行下列變更︰  

    1.  輸入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    2.  在 [金鑰鏈存取]  對話方塊中的 [金鑰鏈]  區段，按一下 [系統] 後，再於 [類別]  區段按一下 [金鑰] 。  

    3.  展開金鑰以檢視用戶端憑證。 若找到您剛安裝的憑證及其私密金鑰，請按兩下該金鑰。  

    4.  在 [存取控制]  索引標籤上，選取 [允許存取前先確認] 。  

    5.  瀏覽至 **/Library/Application Support/Microsoft/CCM**，選取 [CCMClient] ，然後按一下 [新增] 。  

    6.  按一下 [儲存變更]  並關閉 [金鑰鏈存取]  對話方塊。  

7.  重新啟動 Mac 電腦。  

 於 Mac 電腦 [系統偏好設定]  開啟 Configuration Manager  項目，驗證用戶端安裝是否已順利完成。 您也可更新和檢視 [所有系統]  集合，確認此集合中已顯示該 Mac 電腦為受管理用戶端。  

> [!TIP]  
>  若要為該 Mac 用戶端疑難排解任何問題，您可使用 Mac OS X 用戶端套件隨附的 CMDiagnostics 程式來收集下列診斷資訊︰  
>   
>  -   執行中處理程序清單  
> -   Mac OS X 作業系統版本  
> -   與 Configuration Manager 用戶端相關的 Mac OS X 當機報告 (其中包含 **CCM\*.crash** 和 **System Preference.crash**)。  
> -   由 Configuration Manager 用戶端安裝所建立的用料表 (BOM) 檔案和內容清單 (.plist) 檔案。  
> -   資料夾 /Library/Application Support/Microsoft/CCM/Logs 的內容。  
>   
>  CmDiagnostics 收集的資訊會新增至 ZIP 檔案，該檔案儲存於電腦桌面上且命名為 cmdiag-<主機名稱\>**-**<日期和時間\>.zip。  

####  <a name="a-namebkmkenrollr2a-to-enroll-the-client-by-using-the-mac-computer-enrollment-wizard"></a><a name="BKMK_EnrollR2"></a> To enroll the client by using the Mac Computer Enrollment Wizard  

1.  在完成安裝用戶端後，[電腦註冊精靈] 便會開啟。 按 [下一步]  以繼續歡迎頁面。  

    > [!NOTE]  
    >  如果精靈沒有開啟，或是如果您意外關閉精靈，請從 [Configuration Manager]  喜好設定頁面按一下 [註冊]  ，開啟精靈。  

2.  在精靈的下一頁，指定下列資訊︰  

    -   **使用者名稱** - 可用的使用者名稱格式如下︰  

        -   '網域\名稱'。 例如：'contoso\mnorth'  

        -   'user@domain'. 例如： 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  當您使用電子郵件地址填入 [使用者名稱] 欄位時， Configuration Manager 會自動使用電子郵件地址的網域名稱和註冊 Proxy 點伺服器的預設名稱來填入 [伺服器名稱] 欄位。 如果此網域名稱與伺服器名稱並不符合註冊 Proxy 點伺服器名稱，您必須告知使用者可用的正確名稱，使用者才能在註冊 Mac 電腦時輸入此名稱。  

         使用者名稱和對應密碼必須符合 Active Directory 使用者帳戶，並具有 Mac 用戶端憑證範本的讀取和註冊權限。  

    -   **密碼** - 輸入與指定的使用者名稱相對應的密碼。  

    -   **伺服器名稱** - 輸入註冊 Proxy 點伺服器的名稱。  

3.  按 [下一步]  以繼續，然後完成精靈。  

##  <a name="a-nameuninstallmacclienta-uninstalling-the-mac-client"></a><a name="uninstallMacClient"></a> Uninstalling the Mac client  
 若要解除安裝 Mac 用戶端，請使用您從網路下載之 Mac 用戶端檔案隨附的 CMUninstall 指令檔。 利用下列程序，協助您從 Mac 電腦解除安裝 Configuration Manager 用戶端。  

#### <a name="to-uninstall-the-mac-client"></a>解除安裝 Mac 用戶端  

1.  在 Mac 電腦上開啟終端機視窗，並導覽至您由 Microsoft Download Center 下載後並解壓縮的 macclient.dmg 檔案內容資料夾位置。  

2.  導覽至 Tools 資料夾並輸入下列命令列︰  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  **-c** 屬性指示用戶端在解除安裝作業的同時移除用戶端當機記錄和記錄檔。 這是選用的方法，但也是最佳作法，可避免您將來重新安裝用戶端時造成混淆。  

3.  如有必要，您可以手動移除 Configuration Manager 所使用的用戶端驗證憑證，或者予以撤銷。 CMUnistall 不會移除或撤銷此憑證。  

##  <a name="a-namebkmkrenewa-renewing-the-mac-client-certificate"></a><a name="BKMK_Renew"></a> Renewing the Mac client certificate  
 請使用下列其中一種方法更新 Mac 用戶端憑證：  

-   [Renewing the Mac client certificate by using the Renew Certificate Wizard](#BKMK_UI)  

-   [Renewing the Mac client certificate manually](#BKMK_Man)  

###  <a name="a-namebkmkuia-renewing-the-mac-client-certificate-by-using-the-renew-certificate-wizard"></a><a name="BKMK_UI"></a> Renewing the Mac client certificate by using the Renew Certificate Wizard  
 請依照下列程序來設定並使用 Configuration Manager 中的 [更新憑證精靈]。  

##### <a name="to-renew-the-mac-client-certificate-by-using-the-renew-certificate-wizard"></a>使用更新憑證精靈更新 Mac 用戶端憑證  

1.  在 ccmclient.plist 檔案中設定下列值，控制更新憑證精靈開啟的時機：  

    > [!IMPORTANT]  
    >  您必須將這些值設定為字串。 如果您將這些值設定為整數資料類型 (使用 **-int** 屬性)，系統不會讀取這些值。  

    -   **RenewalPeriod1** - 指定使用者可以更新憑證的第一個更新間隔 (以秒為單位)。 預設值為 3,888,000 秒 (45 天)。  

        > [!NOTE]  
        >  如果 **RenewalPeriod1** 已設定成大於或等於 300 秒，就會使用設定的值。  如果設定的值大於 0 且小於 300 秒，則會使用預設值 45 天。  

    -   **RenewalPeriod2** - 指定使用者可以更新憑證的第二個更新間隔 (以秒為單位)。 預設值為 259,200 秒 (3 天)。  

        > [!NOTE]  
        >  如果 **RenewalPeriod2** 已設定成大於或等於 300 秒且小於或等於 **RenewalPeriod1**，將會使用設定的值。 如果 **RenewalPeriod1** 大於 3 天， **RenewalPeriod2**就會使用 3 天的值。  如果 **RenewalPeriod1** 小於 3 天，則 **RenewalPeriod2** 會設為和 **RenewalPeriod1**相同的值。  

    -   **RenewalReminderInterval1** - 指定在第一個更新間隔期間向使用者顯示更新憑證精靈的頻率 (以秒為單位)。 預設值為 86,400 秒 (1 天)。  

        > [!NOTE]  
        >  如果 **RenewalReminderInterval1** 大於 300 秒且小於 **RenewalPeriod1**設定的值，則會使用設定的值。 否則，將會使用預設值 1 天。  

    -   **RenewalReminderInterval2** - 指定在第二個更新間隔期間向使用者顯示更新憑證精靈的頻率 (以秒為單位)。 預設值為 28,800 秒 (8 小時)。  

        > [!NOTE]  
        >  如果 **RenewalReminderInterval2** 大於 300 秒、小於或等於 **RenewalReminderInterval1** ，且小於或等於 **RenewalPeriod2**，則會使用設定的值。 否則會使用 8 小時的值。  

     **範例：** 如果值保留為其預設值，在憑證到期前的 45 天，精靈會每隔 24 小時開啟。  在憑證到期 3 天內，精靈會每隔 8 小時開啟。  

     **範例：** 使用下列命令列，或使用指令碼，將第一個更新間隔設定為 20 天。  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  當更新憑證精靈開啟時，[使用者名稱]  和 [伺服器名稱]  欄位通常已預先填入，因此使用者只需要輸入密碼即可更新憑證。  

    > [!NOTE]  
    >  如果精靈沒有開啟，或是如果您意外關閉精靈，請從 [Configuration Manager]  喜好設定頁面按一下 [更新]  ，開啟精靈。  

###  <a name="a-namebkmkmana-renewing-the-mac-client-certificate-manually"></a><a name="BKMK_Man"></a> Renewing the Mac client certificate manually  
 Mac 用戶端憑證的一般有效期為 1 年。 Configuration Manager 不會自動更新在註冊期間所要求的使用者憑證，因此您必須使用下列程序來手動更新憑證。  

> [!IMPORTANT]  
>  如果憑證到期，您必須解除安裝 Mac 用戶端，然後再重新安裝以及重新註冊。  

 此程序會移除在為同一台 Mac 電腦要求新憑證時需用到的 SMSID。 完成新憑證要求之後，將自動用於 Configuration Manager。  

> [!IMPORTANT]  
>  移除和取代用戶端 SMSID 時，在從 Configuration Manager 主控台刪除用戶端之後，任何已儲存的用戶端記錄 (例如清查) 都將刪除。  

##### <a name="to-renew-the-mac-client-certificate-manually"></a>手動更新 Mac 用戶端憑證  

1.  針對需要更新使用者憑證的 Mac 電腦建立一個裝置集合，接著將 Mac 電腦新增至該集合。  

    > [!WARNING]  
    >  Configuration Manager 不會監視為 Mac 電腦所註冊的憑證有效期間。 您必須在 Configuration Manager 以外個別進行監視，找出要新增到此集合的 Mac 電腦。  

2.  在 [資產與相容性]  工作區內，開啟 [建立設定項目精靈] 。  

3.  在精靈的 [一般]  頁面上，指定下列資訊︰  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **類型：Mac OS X**  

4.  在精靈的 [支援的平台]  頁面上，確定已選取所有 Mac OS X 版本。  

5.  在精靈的 [設定]  頁面上，按一下 [新增]  ，然後在 [建立設定]  對話方塊中，指定下列資訊：  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **設定類型︰指令碼**  

    -   **資料類型︰字串**  

6.  在 [建立設定]  對話方塊的 [探索指令碼] 中，按一下 [新增指令碼]  以指定指令碼探索已設定 SMSID 的 Mac 電腦。  

7.  在 [編輯探索指令碼]  對話方塊中，輸入下列殼層指令碼：  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  按一下 [確定]  以關閉 [編輯探索指令碼]  對話方塊。  

9. 在 [建立設定]  對話方塊中，為 [補救指令碼 (選用)] 按一下 [新增指令碼]  以指定指令碼在 Mac 電腦上找到 SMSID 時將其移除。  

10. 在 [建立補救指令碼]  對話方塊中，輸入下列殼層指令碼：  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. 按一下 [確定]  以關閉 [建立補救指令碼]  對話方塊。  

12. 在精靈的 [相容性規則]  頁面上，按一下 [新增] ，然後在 [建立規則]  對話方塊中，指定下列資訊：  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **選取的設定︰** 按一下 [瀏覽]  ，然後選取您先前指定的探索指令碼。  

    -   在 **下列值** 的欄位中，輸入 **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**。  

    -   啟用 [當此設定不相容時，執行指定的補救指令碼] 選項。  

13. 完成建立設定項目精靈。  

14. 建立包含您剛才建立之設定項目的設定基準，並且將此基準部署到您在步驟 1 建立的裝置集合。  

     如需如何建立並部署設定基準的詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立設定基準](../../../compliance/deploy-use/create-configuration-baselines.md)與[如何在 System Center Configuration Manager 中部署設定基準](../../../compliance/deploy-use/deploy-configuration-baselines.md)。  

15. 對於已移除 SMSID 的 Mac 電腦，請執行下列命令來安裝新的憑證︰  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     收到提示時，請提供進階使用者帳戶的密碼以執行命令，然後再提供 Active Directory 使用者帳戶的密碼。  

16. 若要將註冊的憑證限制到 Configuration Manager，請在 Mac 電腦上開啟終端機視窗，並進行下列變更︰  

    1.  輸入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    2.  在 [金鑰鏈存取]  對話方塊中的 [金鑰鏈]  區段，按一下 [系統] 後，再於 [類別]  區段按一下 [金鑰] 。  

    3.  展開金鑰以檢視用戶端憑證。 若找到您剛安裝的憑證及其私密金鑰，請按兩下該金鑰。  

    4.  在 [存取控制]  索引標籤上，選取 [允許存取前先確認] 。  

    5.  瀏覽至 **/Library/Application Support/Microsoft/CCM**，選取 [CCMClient] ，然後按一下 [新增] 。  

    6.  按一下 [儲存變更]  並關閉 [金鑰鏈存取]  對話方塊。  

17. 重新啟動 Mac 電腦。  

##  <a name="a-namebkmkmanualcertifcateinstallationa-use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a><a name="BKMK_ManualCertifcateInstallation"></a> Use a certificate request and installation method that is independent from Configuration Manager  
 若不使用 Configuration Manager 註冊，而選擇在 Configuration Manager 以外個別要求並安裝用戶端憑證，所需的設定步驟可能稍有不同︰  

1.  執行步驟 1、2、4、6 (選用) 和 8。  

2.  請勿執行步驟 3、5、7 和 9。  

3.  使用下列指示來安裝用戶端。  

#### <a name="to-install-the-client-certificate-independently-from-configuration-manager-and-install-the-client"></a>不透過 Configuration Manager 獨立安裝用戶端憑證及安裝用戶端  

1.  若要在不透過 Configuration Manager 的情況下獨立安裝用戶端憑證，請使用您所選憑證部署方法隨附的指示，來要求並安裝 Mac 電腦的用戶端憑證。  

2.  導覽至您由 Microsoft Download Center 下載後並解壓縮的 macclient.dmg 檔案內容資料夾位置。  

3.  輸入下列命令列：**sudo ./ccmsetup -MP <管理點網際網路 FQDN\> -SubjectName <憑證主體值\>**  

    > [!IMPORTANT]  
    >  憑證主體值區分大小寫，請依憑證詳細資料中所顯示正確輸入。  

     範例：若站台系統內容中的網際網路 FQDN 為 **server03.contoso.com**，而 Mac 用戶端憑證使用 FQDN **mac12.contoso.com** 作為憑證主體的一般名稱，請輸入︰**sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  請等候直至您看見 [已完成安裝]  訊息，再重新啟動 Mac 電腦。  

5.  若要確保此憑證可供 Configuration Manager 存取，請在 Mac 電腦上開啟終端機視窗，並進行下列變更︰  

    1.  輸入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    2.  在 [金鑰鏈存取]  對話方塊中的 [金鑰鏈]  區段，按一下 [系統] 後，再於 [類別]  區段按一下 [金鑰] 。  

    3.  展開金鑰以檢視用戶端憑證。 若找到您剛安裝的憑證及其私密金鑰，請按兩下該金鑰。  

    4.  在 [存取控制]  索引標籤上，選取 [允許存取前先確認] 。  

    5.  瀏覽至 **/Library/Application Support/Microsoft/CCM**，選取 [CCMClient] ，然後按一下 [新增] 。  

    6.  按一下 [儲存變更]  並關閉 [金鑰鏈存取]  對話方塊。  

6.  如果您有多個憑證含有相同的主體值，您必須指定憑證序號以識別您要用於 Configuration Manager 用戶端的憑證。 若要這樣做，請使用下列命令：**sudo defaults write com.microsoft.ccmclient SerialNumber -data "<序號\>"**。  

     例如： **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 於 Mac 電腦 [系統偏好設定]  開啟 Configuration Manager  項目，驗證用戶端安裝是否已順利完成。 您也可更新和檢視 [所有系統]  集合，確認此集合中已顯示該 Mac 電腦為受管理用戶端。  

### <a name="renewing-the-mac-client-certificate"></a>更新 Mac 用戶端憑證  
 更新 Mac 電腦上的電腦憑證之前，請使用下列程序︰  

 此程序會移除用戶端在 Mac 電腦上使用新憑證或更新的憑證時需用到的 SMSID。  

> [!IMPORTANT]  
>  移除和取代用戶端 SMSID 時，在從 Configuration Manager 主控台刪除用戶端之後，任何已儲存的用戶端記錄 (例如清查) 都將刪除。  

##### <a name="to-renew-the-mac-client-certificate"></a>更新 Mac 用戶端憑證  

1.  針對需要更新電腦憑證的 Mac 電腦建立一個裝置集合，接著將 Mac 電腦新增至該集合。  

2.  在 [資產與相容性]  工作區內，開啟 [建立設定項目精靈] 。  

3.  在精靈的 [一般]  頁面上，指定下列資訊︰  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **類型：Mac OS X**  

4.  在精靈的 [支援的平台]  頁面上，確定已選取所有 Mac OS X 版本。  

5.  在精靈的 [設定]  頁面上，按一下 [新增]  ，然後在 [建立設定]  對話方塊中，指定下列資訊：  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **設定類型︰指令碼**  

    -   **資料類型︰字串**  

6.  在 [建立設定]  對話方塊的 [探索指令碼] 中，按一下 [新增指令碼]  以指定指令碼探索已設定 SMSID 的 Mac 電腦。  

7.  在 [編輯探索指令碼]  對話方塊中，輸入下列殼層指令碼：  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  按一下 [確定]  以關閉 [編輯探索指令碼]  對話方塊。  

9. 在 [建立設定]  對話方塊中，為 [補救指令碼 (選用)] 按一下 [新增指令碼]  以指定指令碼在 Mac 電腦上找到 SMSID 時將其移除。  

10. 在 [建立補救指令碼]  對話方塊中，輸入下列殼層指令碼：  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. 按一下 [確定]  以關閉 [建立補救指令碼]  對話方塊。  

12. 在精靈的 [相容性規則]  頁面上，按一下 [新增] ，然後在 [建立規則]  對話方塊中，指定下列資訊：  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **選取的設定︰** 按一下 [瀏覽]  ，然後選取您先前指定的探索指令碼。  

    -   在 **下列值** 的欄位中，輸入 **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**。  

    -   啟用 [當此設定不相容時，執行指定的補救指令碼] 選項。  

13. 完成建立設定項目精靈。  

14. 建立包含您剛才建立之設定項目的設定基準，並且將此基準部署到您在步驟 1 建立的裝置集合。  

     如需如何建立和部署設定基準的詳細資訊，請參閱[如何在 System Center Configuration Manager 建立設定基準](../../../compliance/deploy-use/create-configuration-baselines.md)。  

15. 在已移除 SMSID 的 Mac 電腦上安裝新憑證後，執行下列指令以設定用戶端使用新憑證：  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. 如果您有多個憑證含有相同的主體值，則必須指定憑證序號以識別您要用於 Configuration Manager 用戶端的憑證。 若要這樣做，請使用下列命令：**sudo defaults write com.microsoft.ccmclient SerialNumber -data "<序號\>"**。  

     例如： **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. 重新啟動 Mac 電腦。  



<!--HONumber=Nov16_HO1-->


