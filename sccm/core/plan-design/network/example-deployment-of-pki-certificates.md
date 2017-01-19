---
title: "PKI 憑證部署 | Microsoft Docs"
description: "請依照逐步範例，了解建立與部署 System Center Configuration Manager 所使用 PKI 憑證的程序。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: 11
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 2db82f0572df9519b3119d4dca4f4626ae09d936


---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>為 System Center Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位

*適用於：System Center Configuration Manager (最新分支)*

此部署逐步範例使用 Windows Server 2008 憑證授權單位 (CA)，其中包含的程序可引導您完成建立及部署 System Center Configuration Manager 所使用的公開金鑰基礎結構 (PKI) 憑證。 這些程序使用企業憑證授權單位 (CA) 和憑證範本。 這些步驟僅適用於測試網路以做為概念證明。  

 由於目前沒有任何單一方法可部署必要的憑證，因此您必須參閱您的特殊 PKI 部署文件，以取得部署生產環境必要憑證所需的程序和最佳作法。 如需憑證需求的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

> [!TIP]  
>  對於「測試網路需求」一節中所記載以外的作業系統，可輕鬆調整本主題中的相關指示。 不過，如果您正在 Windows Server 2012 上執行發行 CA，系統不會要求您提供憑證範本版本。 反而會在範本內容的 [相容性]  索引標籤處指定：  
>   
>  -   **憑證授權單位**： **Windows Server 2003**  
> -   **憑證收件者**： **Windows XP / Server 2003**  

## <a name="in-this-section"></a>本節內容  
 以下各節包含逐步指示的範例，以建立及部署可搭配 System Center Configuration Manager 使用的下列憑證：  

 [測試網路需求](#BKMK_testnetworkenvironment)  

 [憑證的概觀](#BKMK_overview2008)  

 [為執行 IIS 的站台系統部署 Web 伺服器憑證](#BKMK_webserver2008_cm2012)  

 [為雲端架構的發佈點部署服務憑證](#BKMK_clouddp2008_cm2012)  

 [部署 Windows 電腦的用戶端憑證](#BKMK_client2008_cm2012)  

 [部署發佈點的用戶端憑證](#BKMK_clientdistributionpoint2008_cm2012)  

 [為行動裝置部署註冊憑證](#BKMK_mobiledevices2008_cm2012)  

 [部署 AMT 的憑證](#BKMK_AMT2008_cm2012)  

 [部署 Mac 電腦的用戶端憑證](#BKMK_MacClient_SP1)  

##  <a name="a-namebkmktestnetworkenvironmenta-test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> 測試網路需求  
 逐步指示具有下列需求：  

-   測試網路正在使用 Windows Server 2008 來執行 Active Directory 網域服務，並安裝為單一網域、單一樹系。  

-   您有一個執行 Windows Server 2008 Enterprise Edition 的成員伺服器已安裝 Active Directory 憑證服務角色，並已設定為企業根憑證授權單位 (CA)。  

-   您有一部已安裝 Windows Server 2008 (Standard Edition 或 Enterprise Edition、R2 或更新版本) 的電腦，並已指定為成員伺服器，且已安裝 Internet Information Services (IIS)。 如果您必須支援由 System Center Configuration Manager 和用戶端在網際網路上註冊的行動裝置，則此電腦將會是使用內部網路 FQDN (以支援內部網路上的用戶端連線) 和網際網路 FQDN 設定的 System Center Configuration Manager 站台系統伺服器。  

-   您有一個已安裝最新版 Service Pack 的 Windows Vista 用戶端，並且以包含 ASCII 字元的電腦名稱設定此電腦，且已加入網域中。 此電腦將會是 System Center Configuration Manager 用戶端電腦。  

-   您可以使用根網域系統管理員帳戶或企業網域系統管理員帳戶登入，並使用此帳戶進行此範例部署中的所有程序。  

##  <a name="a-namebkmkoverview2008a-overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> 憑證的概觀  
 下表列出 System Center Configuration Manager 可能需要的 PKI 憑證類型並描述其使用方式。  

|憑證需求|憑證描述|  
|-----------------------------|-----------------------------|  
|執行 IIS 的站台系統 Web 伺服器憑證|此憑證是用來加密資料以及對用戶端驗證伺服器。 它必須從 System Center Configuration Manager 外部安裝在執行 IIS 且在 System Center Configuration Manager 中設定要使用 HTTPS 的站台系統伺服器上。<br /><br /> 如需設定及安裝此憑證的步驟，請參閱本主題中的 [為執行 IIS 的站台系統部署 Web 伺服器憑證](#BKMK_webserver2008_cm2012) 。|  
|供用戶端連線到雲端架構發佈點的服務憑證|如需設定和安裝此憑證的步驟，請參閱本主題中的 [為雲端架構的發佈點部署服務憑證](#BKMK_clouddp2008_cm2012) 。<br /><br /> **重要事項：** 此憑證會與 Microsoft Azure 管理憑證搭配使用。 如需管理憑證的詳細資訊，請參閱 MSDN 文件庫「Windows Azure 平台」區段中的 [如何建立管理憑證](http://go.microsoft.com/fwlink/p/?LinkId=220281) 和 [如何將管理憑證新增至 Windows Azure 訂閱](http://go.microsoft.com/fwlink/?LinkId=241722) 。|  
|Windows 電腦的用戶端憑證|此憑證是用來對已設定為使用 HTTPS 的站台系統驗證 System Center Configuration Manager 用戶端電腦。 它也可用於管理點和狀態移轉點，以監視其在設定為使用 HTTPS 時的操作狀態。 它必須從 System Center Configuration Manager 外部安裝在電腦上。<br /><br /> 如需設定和安裝這個憑證的步驟，請參閱這個主題中的 [部署 Windows 電腦的用戶端憑證](#BKMK_client2008_cm2012) 。|  
|發佈點的用戶端憑證|此憑證有兩種用途：<br /><br /> 憑證是用來在發佈點傳送狀態訊息之前，對具備 HTTPS 功能的管理點驗證發佈點。<br /><br /> 當選取 [為用戶端啟用 PXE 支援]  散佈點選項時，憑證會傳送至 PXE 開機的電腦，使其在部署作業系統期間可連線到具備 HTTPS 功能的管理點。<br /><br /> 如需設定及安裝此憑證的步驟，請參閱本主題中的 [部署發佈點的用戶端憑證](#BKMK_clientdistributionpoint2008_cm2012) 。|  
|適用於行動裝置的註冊憑證|此憑證是用來對已設定為使用 HTTPS 的站台系統驗證 System Center Configuration Manager 行動裝置用戶端。 它必須在 System Center Configuration Manager 上安裝為行動裝置註冊的一部分，而您要選取已設定的憑證範本作為行動裝置用戶端設定。<br /><br /> 如需設定這個憑證的步驟，請參閱這個主題中的 [Deploying the Enrollment Certificate for Mobile Devices](#BKMK_mobiledevices2008_cm2012) 。|  
|Intel AMT 的憑證|有三種憑證與 Intel AMT 型電腦的超出訊號範圍管理相關：AMT 佈建憑證；AMT Web 伺服器憑證；以及適用於 802.1X 有線或無線網路的選擇性用戶端驗證憑證。<br /><br /> AMT 佈建憑證必須從超出訊號範圍服務點電腦上的 System Center Configuration Manager 進行外部安裝，然後您要在超出訊號範圍服務點內容中選取已安裝的憑證。 AMT Web 伺服器憑證和用戶端驗證憑證會在 AMT 佈建和管理期間進行安裝，而您要在超出訊號範圍管理元件內容中選取已設定的憑證範本。<br /><br /> 如需設定這些憑證的步驟，請參閱本主題中的 [部署 AMT 的憑證](#BKMK_AMT2008_cm2012) 。|  
|Mac 電腦的用戶端憑證|您可以在使用 System Center Configuration Manager 註冊時從 Mac 電腦要求並安裝此憑證，以及選取已設定的憑證範本作為行動裝置用戶端設定。<br /><br /> 如需設定這個憑證的步驟，請參閱這個主題中的 [Deploying the Client Certificate for Mac Computers](#BKMK_MacClient_SP1) 。|  

##  <a name="a-namebkmkwebserver2008cm2012a-deploying-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> 為執行 IIS 的站台系統部署 Web 伺服器憑證  
 此憑證部署的程序如下：  

-   在憑證授權單位上建立及發行 Web 伺服器憑證範本  

-   要求 Web 伺服器憑證  

-   設定 IIS 以使用 Web 伺服器憑證  

###  <a name="a-namebkmkwebserver22008a-creating-and-issuing-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> 在憑證授權單位上建立及發行 Web 伺服器憑證範本  
 此程序會建立 System Center Configuration Manager 站台系統的憑證範本，並將其新增至憑證授權單位。  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>在憑證授權單位上建立及發行 Web 伺服器憑證範本  

1.  建立一個包含成員伺服器並命名為 **ConfigMgr IIS Servers** 的安全性群組，以安裝將執行 IIS 的 System Center Configuration Manager 站台系統。  

2.  在已安裝憑證服務的成員伺服器上，以滑鼠右鍵按一下憑證授權單位主控台中的 [憑證範本]  ，並按一下 [管理]  以載入 [憑證範本]  主控台。  

3.  在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中顯示 [Web 伺服器] 的項目，然後按一下 [複製範本] 。  

4.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition] 。  

5.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱來產生 Configuration Manager 站台系統會用到的 Web 憑證，例如 **ConfigMgr Web 伺服器憑證**。  

6.  按一下 [主體名稱]  索引標籤，並確認已選取 [在要求中提供]  。  

7.  按一下 [安全性]  索引標籤，並從 [Domain Admins]  和 [Enterprise Admins]  安全性群組中移除 [註冊] 權限。  

8.  按一下 [新增] ，在文字方塊中輸入 **ConfigMgr IIS Servers** ，然後按一下 [確定] 。  

9. 選取此群組的 [註冊]  權限，但請勿清除 [讀取]  權限。  

10. 按一下 [確定] ，並關閉 [憑證範本主控台] 。  

11. 在憑證授權單位主控台中，以滑鼠右鍵按一下 [憑證範本] ，按一下 [新增] ，然後再按一下 [要發行的憑證範本] 。  

12. 在 [啟用憑證範本]  對話方塊中，選取您剛才建立的新範本 [ConfigMgr Web 伺服器憑證] ，然後按一下 [確定] 。  

13. 如果您不需要再建立及發行其他憑證，請關閉 [憑證授權單位] 。  

###  <a name="a-namebkmkwebserver32008a-requesting-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> 要求 Web 伺服器憑證  
 此程序可讓您指定將在系統伺服器內容中設定的內部網路和網際網路 FQDN 值，然後在執行 IIS 的成員伺服器上安裝 Web 伺服器憑證。  

##### <a name="to-request-the-web-server-certificate"></a>要求 Web 伺服器憑證  

1.  重新啟動執行 IIS 的成員伺服器，使用您設定的 [讀取]  和 [註冊]  權限，確認電腦可存取您建立的憑證範本。  

2.  依序按一下 **[開始]** 和 **[執行]**，然後輸入 **mmc.exe** 在空白主控台中，按一下 [檔案] ，然後按一下 [新增/移除嵌入式管理單元] 。  

3.  在 [新增或移除嵌入式管理單元]  對話方塊中，從 [可用的嵌入式管理單元]  清單中選取 [憑證] ，然後按一下 [新增] 。  

4.  在 [憑證嵌入式管理單元]  對話方塊中，選取 [電腦帳戶] ，然後按 [下一步] 。  

5.  在 [選取電腦]  對話方塊中，確定選取 [本機電腦: (執行這個主控台的電腦)]  ，然後按一下 [完成] 。  

6.  在 [新增或移除嵌入式管理單元]  對話方塊中，按一下 [確定] 。  

7.  在主控台中，展開 [憑證 (本機電腦)] ，然後按一下 [個人] 。  

8.  以滑鼠右鍵按一下 [憑證] ，按一下 [所有工作] ，然後按一下 [要求新憑證] 。  

9. 在 [ **開始之前** ] 頁面上，按 [ **下一步**]。  

10. 如果看到 [選取憑證註冊原則]  頁面，請按 [下一步] 。  

11. 在 **[要求憑證]** 頁面中，從已顯示的憑證清單中識別出 **[ConfigMgr Web Server Certificate (ConfigMgr Web 伺服器憑證)]**，然後按一下 **[需要更多資訊才能註冊此憑證。請按一下此處以設定設定值。]**。  

12. 在 [憑證內容]  對話方塊的 [主體]  索引標籤中，不要對 [主體名稱] 進行任何變更。 這表示 [主體名稱]  區段的 [值]  方塊會保留空白。 改為在 [別名]  區段中按一下 [類型]  下拉式清單，然後選取 [DNS] 。  

13. 在 [值] 方塊中，指定您將在 System Center Configuration Manager 站台系統內容中指定的 FQDN 值，然後按一下 [確定] 以關閉 [憑證內容] 對話方塊。  

     範例：  

    -   如果站台系統只接受來自內部網路的用戶端連線，則站台系統伺服器的內部網路 FQDN 會是 **server1.internal.contoso.com**：輸入 **server1.internal.contoso.com**，然後按一下 [新增] 。  

    -   如果站台將接受來自內部網路和網際網路的用戶端連線，則站台系統伺服器的內部網路 FQDN 會是 **server1.internal.contoso.com** ，且站台系統伺服器的網際網路 FQDN 會是 **server.contoso.com**：  

        1.  輸入 **server1.internal.contoso.com**，然後按一下 [新增] 。  

        2.  輸入 **server.contoso.com**，然後按一下 [新增] 。  

        > [!NOTE]  
        >  您為 System Center Configuration Manager 所指定的 FQDN 順序並不重要。 不過，您應檢查將使用憑證的所有裝置 (例如行動裝置和 Proxy Web 伺服器) 是否可使用憑證 SAN 和 SAN 中的多個值。 如果裝置對於憑證中的 SAN 值的支援受到限制，您可能必須變更 FQDN 的順序或改用主體值。  

14. 在 [要求憑證]  頁面中，從已顯示的憑證清單中識別 [ConfigMgr Web 伺服器憑證]  ，然後按一下 [註冊] 。  

15. 在 [憑證安裝結果]  頁面上，等待憑證安裝完成，然後按一下 [完成] 。  

16. 關閉 [憑證 (本機電腦)] 。  

###  <a name="a-namebkmkwebserver42008a-configuring-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> 設定 IIS 以使用 Web 伺服器憑證  
 此程序會將已安裝的憑證繫結到 IIS [預設的網站] 。  

##### <a name="to-configure-iis-to-use-the-web-server-certificate"></a>設定 IIS 以使用 Web 伺服器憑證  

1.  在已安裝 IIS 的成員伺服器上，依序按一下 [開始] 、[程式集] 、[系統管理工具] ，然後按一下 [Internet Information Services (IIS) 管理員] 。  

2.  展開 [站台] ，以滑鼠右鍵按一下 [預設的網站] ，然後選取 [編輯繫結] 。  

3.  按一下 [https]  項目，然後按一下 [編輯] 。  

4.  在 [編輯站台繫結]  對話方塊中，使用 ConfigMgr Web 伺服器憑證範本來選取您所要求的憑證，然後按一下 [確定] 。  

    > [!NOTE]  
    >  如果您不確定哪一個是正確的憑證，請選取其中一個，然後按一下 [檢視] 。 這可讓您比較所選憑證的詳細資訊與 [憑證] 嵌入式管理單元顯示的憑證。 例如，[憑證] 嵌入式管理單元會顯示過去用於要求憑證的憑證範本。 然後您可以比對使用 ConfigMgr Web 伺服器憑證範本要求的憑證的憑證指紋，以及目前在 [編輯站台繫結]  對話方塊中所選取憑證的憑證指紋。  

5.  在 [編輯站台繫結]  對話方塊中按一下 [確定]  ，然後按一下 [關閉] 。  

6.  關閉 [Internet Information Services (IIS) 管理員] 。  

 成員伺服器現在會以 System Center Configuration Manager Web 伺服器憑證進行佈建。  

> [!IMPORTANT]  
>  當您在這部電腦上安裝 System Center Configuration Manager 站台系統伺服器時，請確定您在站台系統內容中指定的 FQDN 與要求憑證時所指定的 FQDN 相同。  

##  <a name="a-namebkmkclouddp2008cm2012a-deploying-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> 為雲端架構的發佈點部署服務憑證  

> [!NOTE]  
>  雲端式發佈點的服務憑證適用於 System Center Configuration Manager SP1 及更新版本。  

 此憑證部署的程序如下：  

-   [在憑證授權單位上建立及發行自訂 Web 伺服器憑證範本](#BKMK_clouddpcreating2008)  

-   [要求自訂 Web 伺服器憑證](#BKMK_clouddprequesting2008)  

-   [匯出雲端架構發佈點的自訂 Web 伺服器憑證](#BKMK_clouddpexporting2008)  

###  <a name="a-namebkmkclouddpcreating2008a-creating-and-issuing-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> 在憑證授權單位上建立及發行自訂 Web 伺服器憑證範本  
 此程序會建立以 Web 伺服器憑證範本為基礎的自訂憑證範本。 此憑證適用於 System Center Configuration Manager 雲端架構發佈點，且私密金鑰必須可以匯出。 憑證範本建立後，就會新增至憑證授權單位。  

> [!NOTE]  
>  此程序使用的憑證範本與您為執行 IIS 的站台系統所建立的 Web 伺服器憑證範本不同，因為雖然這兩種憑證都需要伺服器驗證功能，但雲端架構發佈點的憑證還需要在的主體名稱中輸入自訂的定義值，且私密金鑰必須匯出。 基於安全性最佳作法的考量，請勿設定憑證範本為允許匯出私密金鑰，除非這是必要的設定。 雲端架構的發佈點會需要此設定，因為您必須匯入檔案形式的憑證，而不是在憑證存放區中選取。  
>   
>  藉由為此憑證建立新的憑證範本，您可以限制哪些要求憑證的電腦可以匯出私密金鑰。 在生產網路中，您可能還需要考慮為此憑證新增下列修改：  
>   
>  -   安裝憑證需要核准，以增強安全性。  
> -   延長憑證有效期間。 由於每次在憑證到期之前您都必須匯出及匯入憑證，因此延長有效期間可降低必須重複此程序的頻率。 不過，延長有效期間也會降低憑證的安全性，因為這會讓攻擊者有更多的時間將私密金鑰解密和竊取憑證。  
> -   使用憑證主體別名 (SAN) 中的自訂值可協助您在搭配 IIS 使用的標準 Web 伺服器憑證中識別此憑證。  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>在憑證授權單位上建立及發行自訂 Web 伺服器憑證範本  

1.  建立一個包含成員伺服器並命名為 **ConfigMgr Site Servers** 的安全性群組，以安裝將管理雲端架構發佈點的 System Center Configuration Manager 主要站台伺服器。  

2.  在執行憑證授權單位主控台的成員伺服器上，以滑鼠右鍵按一下 [憑證範本] ，然後按一下 [管理]  以載入憑證範本管理主控台。  

3.  在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中顯示 [Web 伺服器] 的項目，然後按一下 [複製範本] 。  

4.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition] 。  

5.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱來產生雲端架構發佈點的 Web 憑證，例如 **ConfigMgr 雲端架構發佈點憑證**。  

6.  按一下 [要求處理]  索引標籤，並選取 [允許匯出私密金鑰] 。  

7.  按一下 [安全性]  索引標籤，然後從 [Enterprise Admins]  安全性群組移除 [註冊]  權限。  

8.  按一下 [新增] ，在文字方塊中輸入 **ConfigMgr 站台伺服器** ，然後按一下 [確定] 。  

9. 選取此群組的 [註冊]  權限，但請勿清除 [讀取]  權限。  

10. 按一下 [確定]  ，並關閉 [憑證範本主控台] 。  

11. 在憑證授權單位主控台中，以滑鼠右鍵按一下 [憑證範本] ，按一下 [新增] ，然後再按一下 [要發行的憑證範本] 。  

12. 在 [啟用憑證範本]  對話方塊中，選取您剛才建立的新範本 [ConfigMgr 雲端架構發佈點憑證] ，然後按一下 [確定] 。  

13. 如果您不需要建立及發行任何其他憑證，請關閉 [憑證授權單位] 。  

###  <a name="a-namebkmkclouddprequesting2008a-requesting-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> 要求自訂 Web 伺服器憑證  
 此程序會要求自訂 Web 伺服器憑證並將其安裝到將執行站台伺服器的成員伺服器上。  

##### <a name="to-request-the-custom-web-server-certificate"></a>要求自訂 Web 伺服器憑證  

1.  在建立及設定 **ConfigMgr 站台伺服器** 安全性群組之後，使用您設定的 [讀取]  和 [註冊]  權限，重新啟動成員伺服器，以確定電腦可以存取您建立的憑證範本。  

2.  依序按一下 **[開始]** 和 **[執行]**，然後輸入 **mmc.exe** 在空白主控台中，按一下 [檔案] ，然後按一下 [新增/移除嵌入式管理單元] 。  

3.  在 [新增或移除嵌入式管理單元]  對話方塊中，從 [可用的嵌入式管理單元]  清單中選取 [憑證] ，然後按一下 [新增] 。  

4.  在 [憑證嵌入式管理單元]  對話方塊中，選取 [電腦帳戶] ，然後按 [下一步] 。  

5.  在 [選取電腦]  對話方塊中，確定選取 [本機電腦: (執行這個主控台的電腦)]  ，然後按一下 [完成] 。  

6.  在 [新增或移除嵌入式管理單元]  對話方塊中，按一下 [確定] 。  

7.  在主控台中，展開 [憑證 (本機電腦)] ，然後按一下 [個人] 。  

8.  以滑鼠右鍵按一下 [憑證] ，按一下 [所有工作] ，然後按一下 [要求新憑證] 。  

9. 在 [ **開始之前** ] 頁面上，按 [ **下一步**]。  

10. 如果看到 [選取憑證註冊原則]  頁面，請按 [下一步] 。  

11. 在 **[要求憑證]** 頁面中，從已顯示的憑證清單中識別出 **[ConfigMgr Cloud-Based Distribution Point Certificate (ConfigMgr 雲端架構發佈點憑證)]**然後按一下 **[需要更多資訊才能註冊此憑證。請按一下此處以設定設定值。]**。  

12. 在 [憑證內容]  對話方塊的 [主體]  索引標籤中，找到 [ 主體名稱] 並選取 [一般名稱]  做為 [類型] 。  

13. 在 [值]  方塊中，使用 FQDN 格式指定您選擇的服務名稱以及網域名稱。 例如： **clouddp1.contoso.com**。  

    > [!NOTE]  
    >  您指定什麼服務名稱並不重要，只要確定它在命名空間中是唯一的名稱即可。 您將使用 DNS 來建立別名(CNAME 記錄)，以將此服務名稱對應至從 Windows Azure 自動產生的識別碼 (GUID) 和 IP 位址。  

14. 按一下 [新增] ，再按一下 [確定]  以關閉 [憑證內容]  對話方塊。  

15. 在 [要求憑證]  頁面中，從已顯示的憑證清單中識別 [ConfigMgr 雲端架構發佈點憑證]  ，然後按一下 [註冊] 。  

16. 在 [憑證安裝結果]  頁面上，等待憑證安裝完成，然後按一下 [完成] 。  

17. 關閉 [憑證 (本機電腦)] 。  

###  <a name="a-namebkmkclouddpexporting2008a-exporting-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> 匯出雲端架構發佈點的自訂 Web 伺服器憑證  
 此程序會將自訂 Web 伺服器憑證匯出為檔案，使您可在建立雲端架構的發佈點時將其匯入。  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>匯出雲端架構發佈點的自訂 Web 伺服器憑證  

1.  在 [憑證 (本機電腦)]  主控台，以滑鼠右鍵按一下剛才安裝的憑證，選取 [所有工作] ，然後按一下 [匯出] 。  

2.  在 [憑證匯出精靈] 中，按 [下一步] 。  

3.  在 [匯出私密金鑰]  頁面上，選取 [是，匯出私密金鑰] ，然後按 [下一步] 。  

    > [!NOTE]  
    >  如果此選項無法使用，表示該憑證在建立時未使用匯出私密金鑰選項。 在此案例中，您無法以所需的格式匯出憑證。 您必須重新設定憑證範本以允許匯出私密金鑰，然後再次要求憑證。  

4.  在 [匯出檔案格式]  頁面上，確定已選取 [個人資訊交換 - PKCS #12 (.PFX)]  。  

5.  在 [密碼]  頁面上，指定強式密碼以保護匯出的憑證及其私密金鑰，然後按 [下一步] 。  

6.  在 [要匯出的檔案]  頁面上，指定您要匯出的檔案名稱，然後按 [下一步] 。  

7.  若要關閉精靈，請在 [憑證匯出精靈]  頁面中按一下 [完成]  ，並在確認對話方塊中按一下 [確定]  。  

8.  關閉 [憑證 (本機電腦)] 。  

9. 安全儲存檔案並確保您可以從 System Center Configuration Manager 主控台存取。  

 當您建立雲端架構的發佈點時，就可以將憑證匯入。  

##  <a name="a-namebkmkclient2008cm2012a-deploying-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> 部署 Windows 電腦的用戶端憑證  
 此憑證部署的程序如下：  

-   在憑證授權單位上建立及發行工作站驗證憑證範本  

-   使用群組原則設定工作站驗證範本的自動註冊  

-   自動註冊工作站驗證憑證，並在電腦上驗證其安裝  

###  <a name="a-namebkmkclient02008a-creating-and-issuing-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> 在憑證授權單位上建立及發行工作站驗證憑證範本  
 此程序會建立 System Center Configuration Manager 用戶端電腦的憑證範本，並將其新增至憑證授權單位。  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>在憑證授權單位上建立及發行工作站驗證憑證範本  

1.  在執行憑證授權單位主控台的成員伺服器上，以滑鼠右鍵按一下 [憑證範本] ，然後按一下 [管理]  以載入憑證範本管理主控台。  

2.  在結果窗格中，以滑鼠右鍵按一下在 [範本顯示名稱]  欄位中顯示 [工作站驗證] 的項目，然後按一下 [複製範本] 。  

3.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition] 。  

4.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱來產生 Configuration Manager 用戶端電腦會用到的用戶端憑證，例如 **ConfigMgr 用戶端伺服器憑證**。  

5.  按一下 [安全性]  索引標籤， 選取 [網域電腦]  群組，並選取 [讀取]  和 [自動註冊] 的額外權限。 請勿清除 [註冊] 。  

6.  按一下 [確定]  ，並關閉 [憑證範本主控台] 。  

7.  在憑證授權單位主控台中，以滑鼠右鍵按一下 [憑證範本] ，按一下 [新增] ，然後再按一下 [要發行的憑證範本] 。  

8.  在 [啟用憑證範本]  對話方塊中，選取您剛才建立的新範本 [ConfigMgr 用戶端憑證] ，然後按一下 [確定] 。  

9. 如果您不需要再建立及發行其他憑證，請關閉 [憑證授權單位] 。  

###  <a name="a-namebkmkclient12008a-configuring-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> 使用群組原則設定工作站驗證範本的自動註冊  
 此程序會設定群組原則在電腦上自動註冊用戶端憑證。  

##### <a name="to-configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>使用群組原則設定工作站驗證範本的自動註冊  

1.  在網域控制站上，依序按一下 [開始] 、[系統管理工具] ，然後按一下 [群組原則管理] 。  

2.  瀏覽到您的網域，以滑鼠右鍵按一下網域，然後選取 [在這個網域中建立 GPO 並連結到] 。  

    > [!NOTE]  
    >  此步驟會使用最佳作法來建立自訂設定的新群組原則，而不會編輯透過 Active Directory 網域服務所安裝的預設網域原則。 在網域層級指派此群組原則後，您就可以將其套用到網域中的所有電腦。 不過，在生產環境中，您可以限制自動註冊，使其只能透過在組織單位層級上指派群組原則在選取的電腦上註冊，或者您也可以透過安全性群組篩選網域群組原則，使其只會套用到群組中的電腦。 如果您限制自動註冊，請記得納入已設定為管理點的伺服器。  

3.  在 [新增 GPO]  對話方塊方塊中輸入新的群組原則名稱，例如 **自動註冊憑證**，按一下 [確定] 。  

4.  在結果窗格的 [已連結的群組原則物件]  索引標籤上，以滑鼠右鍵按一下新的群組原則，然後按一下 [編輯] 。  

5.  在 **[群組原則管理編輯器]**中，展開 **[電腦設定]** 下方的 **[原則]**，然後瀏覽至 **[Windows 設定]** / **[安全性設定]** / **[公開金鑰原則]**。  

6.  以滑鼠右鍵按一下名為 [憑證服務用戶端 - 自動註冊] 的物件類型，然後按一下 [內容]。  

7.  從 [設定模型]  下拉式清單中，依序選取 [已啟用] 、[更新過期的憑證，更新擱置中的憑證並刪除撤銷的憑證] 和 [根據憑證範本來更新憑證] ，然後按一下 [確定] 。  

8.  關閉 [群組原則管理] 。  

###  <a name="a-namebkmkclient22008a-automatically-enrolling-the-workstation-authentication-certificate-and-verifying-its-installation-on-computers"></a><a name="BKMK_client22008"></a> 自動註冊工作站驗證憑證，並在電腦上驗證其安裝  
 此程序會在電腦上安裝用戶端憑證，並驗證其安裝。  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>自動註冊工作站驗證憑證並在用戶端電腦上驗證其安裝  

1.  重新啟動工作站電腦，等待幾分鐘再登入。  

    > [!NOTE]  
    >  重新啟動電腦是確定憑證自動註冊是否成功的最可靠方法。  

2.  使用具有系統管理權限的帳戶登入。  

3.  在搜尋方塊中輸入 **mmc.exe**，然後按 **Enter**。  

4.  在空白的管理主控台按一下 [檔案] ，然後按一下 [新增/移除嵌入式管理單元] 。  

5.  在 [新增或移除嵌入式管理單元]  對話方塊中，從 [可用的嵌入式管理單元]  清單中選取 [憑證] ，然後按一下 [新增] 。  

6.  在 [憑證嵌入式管理單元]  對話方塊中，選取 [電腦帳戶] ，然後按 [下一步] 。  

7.  在 [選取電腦]  對話方塊中，確定選取 [本機電腦: (執行這個主控台的電腦)]  ，然後按一下 [完成] 。  

8.  在 [新增或移除嵌入式管理單元]  對話方塊中，按一下 [確定] 。  

9. 在主控台中，依序展開 [憑證 (本機電腦)] 和 [個人] ，然後按一下 [憑證] 。  

10. 在結果窗格中，確認顯示的憑證在 [使用目的]  欄中顯示 [用戶端驗證]  ，在 [憑證範本]  欄中顯示 [ConfigMgr 用戶端憑證]  。  

11. 關閉 [憑證 (本機電腦)] 。  

12. 針對成員伺服器重複執行步驟 1 到 11，以確認將設定為管理點的伺服器也有用戶端憑證。  

 電腦現在會以 System Center Configuration Manager 用戶端憑證進行佈建。  

##  <a name="a-namebkmkclientdistributionpoint2008cm2012a-deploying-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> 部署發佈點的用戶端憑證  

> [!NOTE]  
>  此憑證也可以用於不使用 PXE 開機的媒體映像，因為憑證需求是相同的。  

 此憑證部署的程序如下：  

-   在憑證授權單位上建立及發行自訂工作站驗證憑證範本  

-   要求自訂工作站驗證憑證  

-   匯出發佈點的用戶端憑證  

###  <a name="a-namebkmkclientdistributionpoint02008a-creating-and-issuing-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> 在憑證授權單位上建立及發行自訂工作站驗證憑證範本  
 此程序會為 System Center Configuration Manager 發佈點建立可匯出私密金鑰的自訂憑證範本，並將憑證範本新增至憑證授權單位。  

> [!NOTE]  
>  此程序會使用不同於您為用戶端電腦建立的憑證範本，因為雖然兩種憑證都要求用戶端驗證能力，但發佈點的憑證要求匯出私密金鑰。 基於安全性最佳作法的考量，請勿設定憑證範本為允許匯出私密金鑰，除非這是必要的設定。 發佈點要求此設定，因為您必須將憑證匯入為檔案，而不是從憑證存放區中選取它。  
>   
>  藉由為此憑證建立新的憑證範本，您可以限制哪些要求憑證的電腦可以匯出私密金鑰。 在我們的範例部署中，這些電腦將是您先前為執行 IIS 的 System Center Configuration Manager 站台系統伺服器所建立的安全性群組。 在發佈 IIS 站台系統角色的實際執行網路上，考慮為執行發佈點的伺服器建立新的安全性群組，如此就能限制只有這些站台系統伺服器可以使用憑證。 您也可以考慮針對此憑證新增下列修改：  
>   
>  -   安裝憑證需要核准，以增強安全性。  
> -   延長憑證有效期間。 由於每次在憑證到期之前您都必須匯出及匯入憑證，因此延長有效期間可降低必須重複此程序的頻率。 不過，延長有效期間也會降低憑證的安全性，因為這會讓攻擊者有更多的時間將私密金鑰解密和竊取憑證。  
> -   在憑證 [主體] 欄位或 [主體別名] (SAN) 中使用自訂值，以協助識別此憑證是否為標準的用戶端憑證。 這對於將在多個發佈點上使用相同憑證的情況特別有用。  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>在憑證授權單位建立及發行自訂工作站驗證憑證範本  

1.  在執行憑證授權單位主控台的成員伺服器上，以滑鼠右鍵按一下 [憑證範本] ，然後按一下 [管理]  以載入憑證範本管理主控台。  

2.  在結果窗格中，以滑鼠右鍵按一下在 [範本顯示名稱]  欄位中顯示 [工作站驗證] 的項目，然後按一下 [複製範本] 。  

3.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition] 。  

4.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱來產生用戶端驗證憑證，例如 **ConfigMgr 用戶端發佈點憑證**。  

5.  按一下 [要求處理]  索引標籤，並選取 [允許匯出私密金鑰] 。  

6.  按一下 [安全性]  索引標籤，然後從 [Enterprise Admins]  安全性群組移除 [註冊]  權限。  

7.  按一下 [新增] ，在文字方塊中輸入 **ConfigMgr IIS Servers** ，然後按一下 [確定] 。  

8.  選取此群組的 [註冊]  權限，但請勿清除 [讀取]  權限。  

9. 按一下 [確定]  ，並關閉 [憑證範本主控台] 。  

10. 在憑證授權單位主控台中，以滑鼠右鍵按一下 [憑證範本] ，按一下 [新增] ，然後再按一下 [要發行的憑證範本] 。  

11. 在 [啟用憑證範本]  對話方塊中，選取剛才建立的新範本 (即 [ConfigMgr 用戶端發佈點憑證] )，然後按一下 [確定] 。  

12. 如果您不需要建立及發行任何其他憑證，請關閉 [憑證授權單位] 。  

###  <a name="a-namebkmkclientdistributionpoint12008a-requesting-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> 要求自訂工作站驗證憑證  
 此程序會在執行 IIS 且將設定為發佈點的成員伺服器上，要求並安裝自訂用戶端憑證。  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>要求自訂工作站驗證憑證  

1.  依序按一下 **[開始]** 和 **[執行]**，然後輸入 **mmc.exe** 在空白主控台中，按一下 [檔案] ，然後按一下 [新增/移除嵌入式管理單元] 。  

2.  在 [新增或移除嵌入式管理單元]  對話方塊中，從 [可用的嵌入式管理單元]  清單中選取 [憑證] ，然後按一下 [新增] 。  

3.  在 [憑證嵌入式管理單元]  對話方塊中，選取 [電腦帳戶] ，然後按 [下一步] 。  

4.  在 [選取電腦]  對話方塊中，確定選取 [本機電腦: (執行這個主控台的電腦)]  ，然後按一下 [完成] 。  

5.  在 [新增或移除嵌入式管理單元]  對話方塊中，按一下 [確定] 。  

6.  在主控台中，展開 [憑證 (本機電腦)] ，然後按一下 [個人] 。  

7.  以滑鼠右鍵按一下 [憑證] ，按一下 [所有工作] ，然後按一下 [要求新憑證] 。  

8.  在 [ **開始之前** ] 頁面上，按 [ **下一步**]。  

9. 如果看到 [選取憑證註冊原則]  頁面，請按 [下一步] 。  

10. 在 [要求憑證]  頁面上，從顯示憑證的清單中選取 [ConfigMgr 用戶端發佈點憑證]  ，然後按一下 [註冊] 。  

11. 在 [憑證安裝結果]  頁面上，等待憑證安裝完成，然後按一下 [完成] 。  

12. 在結果窗格中，確認顯示的憑證在 [使用目的]  欄中顯示 [用戶端驗證]  ，在 [憑證範本]  欄中顯示 [ConfigMgr 用戶端發佈點憑證]  。  

13. 請勿關閉 [憑證 (本機電腦)] 。  

###  <a name="a-namebkmkexportclientdistributionpoint22008a-exporting-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> 匯出發佈點的用戶端憑證  
 此程序會將自訂工作站驗證憑證匯出為檔案，使其可以在發佈點內容中匯入。  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>匯出發佈點的用戶端憑證  

1.  在 [憑證 (本機電腦)]  主控台，以滑鼠右鍵按一下剛才安裝的憑證，選取 [所有工作] ，然後按一下 [匯出] 。  

2.  在 [憑證匯出精靈] 中，按 [下一步] 。  

3.  在 [匯出私密金鑰]  頁面上，選取 [是，匯出私密金鑰] ，然後按 [下一步] 。  

    > [!NOTE]  
    >  如果此選項無法使用，表示該憑證在建立時未使用匯出私密金鑰選項。 在此案例中，您無法以所需的格式匯出憑證。 您必須重新設定憑證範本以允許匯出私密金鑰，然後再次要求憑證。  

4.  在 [匯出檔案格式]  頁面上，確定已選取 [個人資訊交換 - PKCS #12 (.PFX)]  。  

5.  在 [密碼]  頁面上，指定強式密碼以保護匯出的憑證及其私密金鑰，然後按 [下一步] 。  

6.  在 [要匯出的檔案]  頁面上，指定您要匯出的檔案名稱，然後按 [下一步] 。  

7.  若要關閉精靈，請在 [憑證匯出精靈]  頁面中按一下 [完成]  ，並在確認對話方塊中按一下 [確定]  。  

8.  關閉 [憑證 (本機電腦)] 。  

9. 安全儲存檔案並確保您可以從 System Center Configuration Manager 主控台存取。  

 當您設定發佈點時，已可匯入憑證。  

> [!TIP]  
>  當您為未使用 PXE 開機的作業系統部署設定媒體映像，以及安裝必須與要求 HTTPS 用戶端連線的管理點連線之映像的工作順序時，便可以使用相同的憑證檔案。  

##  <a name="a-namebkmkmobiledevices2008cm2012a-deploying-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> 為行動裝置部署註冊憑證  
 此憑證部署需要在憑證授權單位執行單一程序，以建立及發行註冊憑證範本。  

### <a name="creating-and-issuing-the-enrollment-certificate-template-on-the-certification-authority"></a>在憑證授權單位建立及發行註冊憑證範本  
 此程序會建立 System Center Configuration Manager 行動裝置的註冊憑證範本，並將其新增至憑證授權單位。  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>在憑證授權單位建立及發行註冊憑證範本  

1.  建立一個安全性群組，其包含將在 System Center Configuration Manager 中註冊行動裝置的使用者。  

2.  在已安裝憑證服務的成員伺服器上，以滑鼠右鍵按一下憑證授權單位主控台的 [憑證範本] ，然後按一下 [管理]  以載入 [憑證範本] 管理主控台。  

3.  在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中顯示 [已驗證的工作階段] 的項目，然後按一下 [複製範本] 。  

4.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition] 。  

5.  在 [新範本的內容] 對話方塊的 [一般] 索引標籤上，輸入要為由 System Center Configuration Manager 管理之行動裝置產生註冊憑證的範本名稱，例如 **ConfigMgr 行動裝置註冊憑證**。  

6.  按一下 [主體名稱]  索引標籤，確定選取 [用這項 Active Directory 資訊來建立]  ，然後選取 [主體名稱格式:]  的 [一般名稱]  ，並清除 [在次要主體名稱中包含這些資訊]  的 [使用者主體名稱 (UPN)] 。  

7.  按一下 [安全性]  索引標籤，選取包含要註冊行動裝置之使用者的安全性群組，然後選取 [註冊] 的其他權限。 請勿清除 [讀取] 。  

8.  按一下 [確定]  ，並關閉 [憑證範本主控台] 。  

9. 在憑證授權單位主控台中，以滑鼠右鍵按一下 [憑證範本] ，按一下 [新增] ，然後再按一下 [要發行的憑證範本] 。  

10. 在 [啟用憑證範本]  對話方塊中，選取剛才建立的新範本 (即 [ConfigMgr 行動裝置註冊範本] )，然後按一下 [確定] 。  

11. 如果您不需要建立及發行其他憑證，請關閉憑證授權單位主控台。  

 您現在可以在用戶端設定中設定行動裝置註冊設定檔時，選取行動裝置註冊憑證範本。  

##  <a name="a-namebkmkamt2008cm2012a-deploying-the-certificates-for-amt"></a><a name="BKMK_AMT2008_cm2012"></a> 部署 AMT 的憑證  
 此憑證部署的程序如下：  

-   建立、發行及安裝 AMT 佈建憑證  

-   建立及發行 AMT 型電腦的 Web 伺服器憑證  

-   建立及發行 802.1X AMT 型電腦的用戶端驗證憑證  

###  <a name="a-namebkmkamtprovisioning2008a-creating-issuing-and-installing-the-amt-provisioning-certificate"></a><a name="BKMK_AMTprovisioning2008"></a> Creating, Issuing, and Installing the AMT Provisioning Certificate  
 當使用內部根 CA 的憑證指紋設定 AMT 型電腦時，可使用內部 CA 建立佈建憑證。 如果不是這種情況，而且您必須使用外部憑證授權單位時，請依照發行 AMT 佈建憑證的公司指示進行，這通常會需要從公司的公用網站要求憑證。 您也可以在 Intel vPro Expert Center 中找到所選外部 CA 的詳細指示：Microsoft vPro Manageability 網站 ([http://go.microsoft.com/fwlink/?LinkId=132001](http://go.microsoft.com/fwlink/?LinkId=132001))。  

> [!IMPORTANT]  
>  外部 CA 可能不支援 Intel AMT 佈建物件識別碼。 發生這種情況時，請使用提供 **Intel(R) Client Setup Certificate**的 OU 屬性的替代方法。  

 當您從外部 CA 要求 AMT 佈建憑證時，可將憑證安裝到將裝載超出訊號範圍服務點之成員伺服器上的電腦個人憑證存放區。  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>要求及發行 AMT 佈建憑證  

1.  建立一個安全性群組，其包含將執行超出訊號範圍服務點之站台系統伺服器的電腦帳戶。  

2.  在已安裝憑證服務的成員伺服器上，以滑鼠右鍵按一下憑證授權單位主控台的 [憑證範本] ，然後按一下 [管理]  以載入 [憑證範本]  主控台。  

3.  在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中顯示 [Web 伺服器]  的項目，然後按一下 [複製範本] 。  

4.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition] 。  

5.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入 AMT 佈建憑證範本的範本名稱，例如 **ConfigMgr AMT 佈建**。  

6.  按一下 [主體名稱]  索引標籤，選取 [用這項 Active Directory 資訊來建立] ，然後選取 [一般名稱] 。  

7.  按一下 [延伸]  索引標籤，確定已選取 [應用程式原則]  ，然後按一下 [編輯] 。  

8.  在 [編輯應用程式原則延伸]  對話方塊中，按一下 [新增] 。  

9. 在 [新增應用程式原則]  對話方塊中，按一下 [新增] 。  

10. 在 [新的應用程式原則]  對話方塊的 [名稱]  欄位中輸入 **AMT 佈建** ，然後輸入下列 **物件識別元**號碼： **2.16.840.1.113741.1.2.3**。  

11. 按一下 [確定] ，然後在 [新增應用程式原則]  對話方塊中按一下 [確定]  。  

12. 在 [編輯應用程式原則延伸]  對話方塊中按一下 [確定]  。  

13. 您現在應該可以在 [新範本的內容]  對話方塊中看到以下列示為 [應用程式原則]  的描述：[伺服器驗證]  和 [AMT 佈建] 。  

14. 按一下 [安全性]  索引標籤，並從 [Domain Admins]  和 [Enterprise Admins]  安全性群組中移除 [註冊] 權限。  

15. 按一下 [新增] ，輸入包含超出訊號範圍服務點站台系統角色之電腦帳戶的安全性群組名稱，然後按一下 [確定] 。  

16. 針對此群組選取 [註冊]  權限，但請勿清除 [讀取]  權限。  

17. 按一下 [確定] 並關閉 [憑證範本]  主控台。  

18. 在 [憑證授權單位] 中，以滑鼠右鍵按一下 [憑證範本] ，按一下 [新增] ，然後再按一下 [要發行的憑證範本] 。  

19. 在 [啟用憑證範本]  對話方塊中，選取剛才建立的新範本 (即 [ConfigMgr AMT 佈建] )，然後按一下 [確定] 。  

    > [!NOTE]  
    >  如果無法完成步驟 18 或 19，請確認您使用的是 Windows Server 2008 Enterprise Edition。 除非使用 Windows Server 2008 Enterprise Edition，否則縱然可以使用 Windows Server Standard Edition 和憑證服務來設定範本，卻無法使用修改後的憑證範本部署憑證。  

20. 請勿關閉 [憑證授權單位] 。  

 您現在可以將來自內部 CA 的 AMT 佈建憑證，安裝在超出訊號範圍服務點電腦上。  

##### <a name="to-install-the-amt-provisioning-certificate"></a>安裝 AMT 佈建憑證  

1.  重新啟動執行 IIS 的成員伺服器，確定它可以使用設定的權限存取憑證範本。  

2.  依序按一下 **[開始]** 和 **[執行]**，然後輸入 **mmc.exe** 在空白主控台中，按一下 [檔案] ，然後按一下 [新增/移除嵌入式管理單元] 。  

3.  在 [新增或移除嵌入式管理單元]  對話方塊中，從 [可用的嵌入式管理單元]  清單中選取 [憑證] ，然後按一下 [新增] 。  

4.  在 [憑證嵌入式管理單元]  對話方塊中，選取 [電腦帳戶] ，然後按 [下一步] 。  

5.  在 [選取電腦]  對話方塊中，確定選取 [本機電腦: (執行這個主控台的電腦)]  ，然後按一下 [完成] 。  

6.  在 [新增或移除嵌入式管理單元]  對話方塊中，按一下 [確定] 。  

7.  在主控台中，展開 [憑證 (本機電腦)] ，然後按一下 [個人] 。  

8.  以滑鼠右鍵按一下 [憑證] ，按一下 [所有工作] ，然後按一下 [要求新憑證] 。  

9. 在 [ **開始之前** ] 頁面上，按 [ **下一步**]。  

10. 如果看到 [選取憑證註冊原則]  頁面，請按 [下一步] 。  

11. 在 [要求憑證]  頁面上，從顯示憑證的清單中選取 [AMT 佈建]  ，然後按一下 [註冊] 。  

12. 在 [憑證安裝結果]  頁面上，等待憑證安裝完成，然後按一下 [完成] 。  

13. 關閉 [憑證 (本機電腦)] 。  

 您已安裝來自內部 CA 的 AMT 佈建憑證，並可在超出訊號範圍服務點內容中選取該憑證。  

### <a name="creating-and-issuing-the-web-server-certificate-for-amt-based-computers"></a>建立及發行 AMT 型電腦的 Web 伺服器憑證  
 利用下列程序，為 AMT 型電腦準備 Web 伺服器憑證。  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>建立及發行 Web 伺服器憑證範本  

1.  建立空白的安全性群組，其包含 System Center Configuration Manager 在 AMT 佈建期間建立的 AMT 型電腦帳戶。  

2.  在已安裝憑證服務的成員伺服器上，以滑鼠右鍵按一下憑證授權單位主控台的 [憑證範本] ，然後按一下 [管理]  以載入 [憑證範本]  主控台。  

3.  在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中顯示 [Web 伺服器] 的項目，然後按一下 [複製範本] 。  

4.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  請勿選取 [] **。**  

5.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱來產生 AMT 電腦頻外管理會用到的 Web 憑證，例如 **ConfigMgr AMT Web 伺服器憑證**。  

6.  依序按一下 [主體名稱]  索引標籤和 [用這項 Active Directory 資訊來建立] ，針對 [主體名稱格式]  選取 [一般名稱] ，然後清除替代主體名稱的 [使用者主要名稱 (UPN)]  。  

7.  按一下 [安全性]  索引標籤，並從 [Domain Admins]  和 [Enterprise Admins]  安全性群組中移除 [註冊] 權限。  

8.  按一下 [新增]  ，並輸入您為 AMT 佈建所建立的安全性群組名稱。 然後按一下 [確定]。   

9. 針對此安全性群組，選取下列 [允許]  權限：[讀取]  和 [註冊] 。  

10. 按一下 [確定] 並關閉 [憑證範本]  主控台。  

11. 在 [憑證授權單位]  主控台，以滑鼠右鍵按一下 [憑證範本] ，按一下 [新增] ，然後再按一下 [要發行的憑證範本] 。  

12. 在 [啟用憑證範本]  對話方塊中，選取剛才建立的新範本 (即 [ConfigMgr AMT Web 伺服器憑證] )，然後按一下 [確定] 。  

13. 如果您不需要建立及發行任何其他憑證，請關閉 [憑證授權單位] 。  

 您現在可以使用 AMT Web 伺服器範本，以 Web 伺服器憑證佈建 AMT 型電腦。 在超出訊號範圍管理元件內容中，選取此憑證範本。  

### <a name="creating-and-issuing-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>建立及發行 802.1X AMT 型電腦的用戶端驗證憑證  
 如果 AMT 型電腦將用戶端憑證用於 802.1X 驗證的有線或無線網路，請使用下列程序。  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>在 CA 上建立及發行用戶端驗證憑證範本  

1.  在已安裝憑證服務的成員伺服器上，以滑鼠右鍵按一下憑證授權單位主控台的 [憑證範本] ，然後按一下 [管理]  以載入 [憑證範本]  主控台。  

2.  在結果窗格中，以滑鼠右鍵按一下在 [範本顯示名稱]  欄位中顯示 [工作站驗證] 的項目，然後按一下 [複製範本] 。  

    > [!IMPORTANT]  
    >  請勿選取 [] **。**  

3.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱來產生 AMT 電腦頻外管理會用到的用戶端憑證，例如 **ConfigMgr AMT 802.1X 用戶端驗證憑證**。  

4.  按一下 [主體名稱]  索引標籤，按一下 [用這項 Active Directory 資訊來建立]  ，並針對 [主體名稱格式]  選取 [一般名稱] 。 針對替代主體名稱清除 [DNS 名稱]  ，然後選取 [使用者主要名稱 (UPN)] 。  

5.  按一下 [安全性]  索引標籤，並從 [Domain Admins]  和 [Enterprise Admins]  安全性群組中移除 [註冊] 權限。  

6.  按一下 [新增]  ，並輸入您將在超出訊號範圍管理元件內容中指定的安全性群組名稱，如此即可包含 AMT 型電腦的電腦帳戶。 然後按一下 [確定]。   

7.  針對此安全性群組，選取下列 [允許]  權限：[讀取]  和 [註冊] 。  

8.  按一下 [確定] 並關閉 [憑證範本] 主控台 (即 [certtmpl – [憑證範本]])。  

9. 在 [憑證授權單位]  管理主控台，以滑鼠右鍵按一下 [憑證範本] ，按一下 [新增] ，然後再按一下 [要發行的憑證範本] 。  

10. 在 [啟用憑證範本]  對話方塊中，選取剛才建立的新範本 (即 [ConfigMgr AMT 802.1X 用戶端驗證憑證] )，然後按一下 [確定] 。  

11. 如果您不需要再建立及發行其他憑證，請關閉 [憑證授權單位] 。  

 現在已可使用用戶端驗證憑證範本發行憑證給可用於 802.1X 用戶端驗證的 AMT 型電腦。 在超出訊號範圍管理元件內容中，選取此憑證範本。  

##  <a name="a-namebkmkmacclientsp1a-deploying-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> 部署 Mac 電腦的用戶端憑證  

> [!NOTE]  
>  Mac 電腦的用戶端憑證適用於 System Center Configuration Manager SP1 及更新版本。  

 此憑證部署需要在憑證授權單位執行單一程序，以建立及發行註冊憑證範本。  

###  <a name="a-namebkmkmacclientcreatingissuinga-creating-and-issuing-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> 在憑證授權單位建立及發行 Mac 用戶端憑證範本  
 此程序會為 System Center Configuration Manager Mac 電腦建立自訂憑證範本，並將憑證範本新增至憑證授權單位。  

> [!NOTE]  
>  此程序會使用不同於您為 Windows 用戶端電腦或發佈點所建立的憑證範本。  
>   
>  藉由為此憑證建立新的憑證範本，您可以將憑證要求限制為只有授權的使用者可以使用。  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>在憑證授權單位建立及發行 Mac 用戶端憑證範本  

1.  建立一個安全性群組，其包含系統管理使用者的使用者帳戶，而這些使用者將會使用 System Center Configuration Manager 在 Mac 電腦上註冊憑證。  

2.  在執行憑證授權單位主控台的成員伺服器上，以滑鼠右鍵按一下 [憑證範本] ，然後按一下 [管理]  以載入憑證範本管理主控台。  

3.  在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中顯示 [已驗證的工作階段] 的項目，然後按一下 [複製範本] 。  

4.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition] 。  

5.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱來產生 Mac 用戶端憑證，例如 **ConfigMgr Mac 用戶端憑證**。  

6.  按一下 [主體名稱]  索引標籤，確定選取 [用這項 Active Directory 資訊來建立]  ，然後選取 [主體名稱格式:]  的 [一般名稱]  ，並清除 [在次要主體名稱中包含這些資訊]  的 [使用者主體名稱 (UPN)] 。  

7.  按一下 [安全性]  索引標籤，並從 [Domain Admins]  和 [Enterprise Admins]  安全性群組中移除 [註冊]  權限。  

8.  按一下 [新增] ，指定您在步驟一建立的安全性群組，然後按一下 [確定] 。  

9. 選取此群組的 [註冊]  權限，但請勿清除 [讀取]  權限。  

10. 按一下 [確定]  ，並關閉 [憑證範本主控台] 。  

11. 在憑證授權單位主控台中，以滑鼠右鍵按一下 [憑證範本] ，按一下 [新增] ，然後再按一下 [要發行的憑證範本] 。  

12. 在 [啟用憑證範本]  對話方塊中，選取剛才建立的新範本 (即 [ConfigMgr Mac 用戶端憑證] )，然後按一下 [確定] 。  

13. 如果您不需要建立及發行任何其他憑證，請關閉 [憑證授權單位] 。  

 您現在可以在設定註冊的用戶端設定時，選取 Mac 用戶端憑證範本。



<!--HONumber=Dec16_HO3-->


