---
title: "安裝雲端架構發佈點 | Microsoft Docs"
description: "了解該如何在 Microsoft Azure 中開始使用雲端發佈點。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: aba573b2822568236c006e7af19b421639faa8bc

---
# <a name="install-cloud-based-distribution-points-in-microsoft-azure-for-system-center-configuration-manager"></a>在 Microsoft Azure 中，安裝 System Center Configuration Manager 的雲端架構發佈點

*適用於：System Center Configuration Manager (最新分支)*

在 Microsoft Azure 中，您可以安裝 System Center Configuration Manager 的雲端架構發佈點。 如果您不熟悉雲端架構的發佈點，請先參閱[使用雲端架構發佈點](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)再繼續。

 在安裝之前，請確定您擁有必要的憑證檔案：  

-   匯出至 .cer 檔及 .pfx 檔的 Microsoft Azure 管理憑證。  

-   匯出至 .pfx 檔的 Configuration Manager 雲端架構發佈點服務憑證。  

    > [!TIP]
    >   如需這些憑證的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)主題中的＜雲端架構發佈點＞一節。 如需雲端式發佈點服務憑證的部署範例，請參閱[為 System Center Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)中的*為雲端架構的發佈點部署服務憑證*。  


 安裝雲端架構發佈點之後，Microsoft Azure 會自動為服務產生 GUID，並將此 GUID 附加至 **cloudapp.net**的 DNS 尾碼。 您必須使用此 GUID 設定 DNS 的 DNS 別名 (CNAME 記錄)，以便將您在 Configuration Manager 雲端架構發佈點服務憑證中定義的服務名稱對應至自動產生的 GUID。  

 如果您使用 Proxy Web 伺服器，可能需要設定 Proxy 設定才能與裝載發佈點的雲端服務進行通訊。  

##  <a name="a-namebkmkconfigwindowsazureandinstalldpa-configure-microsoft-azure-and-install-cloud-based-distribution-points"></a><a name="BKMK_ConfigWindowsAzureandInstallDP"></a> 設定 Microsoft Azure 及安裝雲端架構的發佈點  
 使用下列程序設定 Microsoft Azure 以支援發佈點，然後在 Configuration Manager 中安裝雲端架構的發佈點。  

#### <a name="to-configure-a-cloud-service-in-microsoft-azure-for-a-distribution-point"></a>若要在 Microsoft Azure 中設定發佈點的雲端服務  

1.  開啟 Web 瀏覽器前往 Microsoft Azure 管理入口站台，網址為 https://manage.windowsazure.com，然後存取您的 Microsoft Azure 帳戶。  

2.  按一下 [託管服務、儲存體帳戶和 CDN]，然後選取 [管理憑證]。  

3.  以滑鼠右鍵按一下您的訂閱，然後選取 [加入憑證] 。  

4.  指定包含所匯出 Microsoft Azure 管理憑證的 .cer 檔做為 **憑證檔案**以用於此雲端服務，然後按一下 [確定] 。  

 管理憑證會載入 Microsoft Azure 中，而現在您可以安裝雲端架構的發佈點。  

#### <a name="to-install-a-cloud-based-distribution-point-for-configuration-manager"></a>若要安裝 Configuration Manager 的雲端架構發佈點  

1.  完成前述程序中的步驟，設定 Microsoft Azure 中雲端服務的管理憑證。  

2.  在 Configuration Manager 主控台的 [系統管理] 工作區中展開 [雲端服務]，選取 [雲端發佈點]，然後在 [常用] 索引標籤上按一下 [建立雲端發佈點]。  

3.  在 [建立雲端發佈點精靈] 的 [一般]  頁面上，設定下列各項：  

    -   指定您 Microsoft Azure 帳戶的 [訂用帳戶 ID]  。  

        > [!TIP]  
        >  您可以在 Microsoft Azure 管理入口站台中找到您的 Microsoft Azure 訂用帳戶 ID。  

    -   指定 [管理憑證] 。 按一下 [瀏覽]  指定包含所匯出 Microsoft Azure 管理憑證的 .pfx 檔，然後輸入憑證的密碼。 您可以選擇從 Microsoft Azure SDK 1.7 指定版本 1 的 .publishsettings 檔案。  

4.  按一下 [下一步]，Configuration Manager 即會連線到 Microsoft Azure 以驗證管理憑證。  

5.  在 [設定]  頁面上完成下列設定，然後按 [下一步] ：  

    -   針對 [地區] ，選取您要建立裝載此發佈點之雲端服務的 Microsoft Azure 地區。  

    -   針對 [憑證檔案]，請指定包含所匯出 Configuration Manager 雲端式發佈點服務憑證的 .pfx 檔案，然後輸入密碼。  

        > [!NOTE]  
        >  [服務 FQDN]  方塊會自動從憑證的 [主體名稱] 填入，且大部分情況下您不需要進行編輯。 例外狀況是，如果您在測試環境中使用萬用字元憑證，其中主機名稱並未指定，如此一來，多部擁有相同 DNS 尾碼的電腦就能使用憑證。 在此案例中，憑證 [主體] 會包含類似 **CN=\*.contoso.com** 的值，而 Configuration Manager 會顯示您必須指定正確的 FQDN 訊息。 按一下 [確定]  關閉訊息，然後在 DNS 尾碼前面輸入特定名稱，以提供完整的 FQDN。 例如，您可以新增 **clouddp1** 指定完整服務 FQDN **clouddp1.contoso.com**。 在您的網域中，服務 FQDN 必須是唯一的，	不符合任何加入網域的裝置。  
        >   
        >  萬用字元憑證僅在測試環境中支援。  

6.  在 [警示] 頁面上，設定儲存體配額、傳輸配額，以及您想讓 Configuration Manager 產生警示的配額百分比，然後按一下 [下一步]。  

7.  完成精靈。  

 精靈會為雲端架構發佈點建立新的託管服務。 關閉精靈後，您可以在 Configuration Manager 主控台中或是藉由在主要站台伺服器上監視 **CloudMgr.log** 檔案的方式，監視雲端架構發佈點的安裝進度。 您也可以在 Microsoft Azure 管理入口站台中監視雲端服務的佈建。  

> [!NOTE]  
>  在 Microsoft Azure 中佈建新的發佈點可能需要長達 30 分鐘的時間。 佈建儲存體帳戶之前，**CloudMgr.log** 檔案中會重複出現下列訊息：**Waiting for check if container exists.Will check again in 10 seconds (等候檢查容器是否存在。10 秒後將再次檢查)**。 然後服務便會建立及設定。  

 您可以使用下列方法識別雲端架構發佈點安裝已完成：  

-   在 Microsoft Azure 管理入口站台中，雲端架構發佈點的 [部署]  狀態顯示為 [就緒] 。  

-   在 Configuration Manager 主控台的 [系統管理] 工作區中，[階層設定] 與 [雲端] 節點的雲端式發佈點顯示狀態為 [就緒]。  

-   Configuration Manager 會顯示 SMS_CLOUD_SERVICES_MANAGER 元件的狀態訊息識別碼 **9409**。  

##  <a name="a-namebkmkconfigdnsforclouddpsa-configure-name-resolution-for-cloud-based-distribution-points"></a><a name="BKMK_ConfigDNSforCloudDPs"></a> 設定雲端架構發佈點的名稱解析  
 在用戶端可以存取雲端架構發佈點之前，他們必須能夠將雲端架構發佈點的名稱解析到 Microsoft Azure 所管理的 IP 位址。 用戶端會分兩個階段執行此動作：  

1.  它們會將您連同 Configuration Manager 雲端架構發佈點服務憑證一併提供的服務名稱，對應到您的 Microsoft Azure 服務 FQDN。 這個 FQDN 包含 GUID 及 **cloudapp.net**的 DNS 尾碼。 GUID 是在您安裝雲端架構發佈點後自動產生的。 您可以參照雲端服務儀表板中的 [站台 URL]  ，在 Microsoft Azure 管理入口站台中查看完整的 FQDN。 範例站台 URL 是 **http://d1594d4527614a09b934d470.cloudapp.net**。  

2.  他們會將 Microsoft Azure 服務 FQDN 解析到 Microsoft Azure 配置的 IP 位址。 在 Microsoft Azure 入口站台的雲端服務儀表板也可識別此 IP 位址，稱為 [公用虛擬 IP 位址 (VIP)] 。  

若要將您連同 Configuration Manager 雲端架構發佈點服務憑證 (例如 **clouddp1.contoso.com**) 一併提供的服務名稱對應到 Microsoft Azure 服務 FQDN (例如 **d1594d4527614a09b934d470.cloudapp.net**)，則網際網路上的 DNS 伺服器必須擁有一個 DNS 別名 (CNAME 記錄)。 然後，用戶端可使用網際網路上的 DNS 伺服器，將 Microsoft Azure 服務 FQDN 解析到 IP 位址。  

##  <a name="a-namebkmkconfigproxyforclouda-configure-proxy-settings-for-primary-sites-that-manage-cloud-services"></a><a name="BKMK_ConfigProxyforCloud"></a> 為管理雲端服務的主要站台設定 Proxy 設定值  
 當您與 Configuration Manager 搭配使用雲端服務時，管理雲端架構發佈點的主要站台必須能夠使用主要站台電腦的**系統**帳戶，連線到 Microsoft Azure 管理入口網站。 此連線是利用主要站台伺服器電腦上的預設網頁瀏覽器而建立的。  

 在管理雲端架構發佈點的主要站台伺服器上，可能必須設定 Proxy 設定值，才能讓主要站台存取網際網路和 Microsoft Azure。  

 使用下列程序，在 Configuration Manager 主控台為主要站台伺服器設定 Proxy 設定值。  

> [!TIP]  
>  您也可以使用 [新增站台系統角色精靈]，在主要站台伺服器上安裝新的站台系統角色時設定 Proxy 伺服器 。  

#### <a name="to-configure-proxy-settings-for-the-primary-site-server"></a>為主要站台伺服器設定 Proxy 設定值  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [站台設定] ，按一下 [伺服器和站台系統角色] ，然後選取管理雲端架構發佈點的主要站台伺服器。  

3.  在詳細資料窗格中，用滑鼠右鍵按一下 [站台系統] ，再按一下 [內容] 。  

4.  在 [站台系統內容] 中，選取 [Proxy] 索引標籤，然後為這個主要站台伺服器設定 Proxy 設定值。  

5.  按一下 [確定]  儲存新的 Proxy 伺服器設定。  



<!--HONumber=Dec16_HO3-->


