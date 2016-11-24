---
title: "設定憑證 | 內部部署 MDM | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中為內部部署行動裝置管理設定受信任通訊的憑證。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
caps.latest.revision: 27
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 22a01ffa8385413c9671fd282c7337cbb6e2ffa0


---
# <a name="set-up-certificates-for-trusted-communications-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 內部部署行動裝置管理需要設定註冊點、註冊 Proxy 點、發佈點及裝置管理點站台系統角色，才能與受管理的裝置進行受信任的通訊。 任何站台系統伺服器只要裝載了這當中一或多個角色，就必須有一個繫結到該系統上網頁伺服器的唯一 PKI 憑證。 此外，也必須在受管理裝置上存放與伺服器上憑證具有相同根的憑證，才能與它們建立受信任的通訊。  

 對於已加入網域的裝置，「Active Directory 憑證服務」會自動在所有裝置上安裝具有受信任根的所需憑證。 對於未加入網域的裝置，您則必須透過其他方式取得具有受信任根的有效憑證。 如果您使用站台 CA 做為受信任的根 (這個根與 Active Directory 用於已加入網域的裝置相同)，註冊點和註冊 Proxy 點的站台系統伺服器就必須有一個由該 CA 發行的憑證與它們繫結。  

 每個要受管理的裝置上也都需要安裝一個具有相同根的憑證，才能支援與站台系統角色進行受信任的通訊。 對於大量註冊的裝置，您可以將憑證包含在新增到裝置的註冊套件中，以供在使用者第一次啟動裝置時用來註冊裝置。 對於使用者註冊的裝置，您則需要透過電子郵件、Web 下載或某種其他方法來新增憑證。  

 做為未加入網域之裝置的替代方案，您可以使用知名公用 CA (例如 Verisign 或 GoDaddy) 的根來發行伺服器憑證，這樣可避免需要手動在裝置上安裝憑證，因為大多數裝置原本就信任連到使用相同公用 CA 根之伺服器的連線。 對無法透過站台 CA 在每部裝置上安裝憑證的使用者註冊裝置來說，這是一個實用的替代方案。  

> [!IMPORTANT]  
>  有許多方法可以設定進行內部部署行動裝置管理之裝置與站台系統伺服器之間受信任通訊的憑證。 本文章中提供的資訊是其中一種做法的範例。 這個方法會要求您在站台中執行已安裝「Active Directory 憑證服務」角色及「憑證授權單位和憑證授權單位網頁註冊」角色的伺服器。 如需此 Windows Server 角色的詳細資訊和指引，請參閱 [Active Directory 憑證服務](http://go.microsoft.com/fwlink/p/?LinkId=115018) 。  

 若要為內部部署行動裝置管理所需的 SSL 通訊設定 Configuration Manager 站台，請遵循下列高階步驟︰  

-   [設定用來發佈 CRL 的憑證授權單位 (CA)](#bkmk_configCa)  

-   [在 CA 上建立網頁伺服器憑證範本](#bkmk_certTempl)  

-   [要求每個站台系統角色的網頁伺服器憑證](#bkmk_requestCert)  

-   [將憑證繫結到網頁伺服器](#bkmk_bindCert)  

-   [將具有相同的根的憑證匯出為網頁伺服器憑證](#bkmk_exportCert)  

##  <a name="a-namebkmkconfigcaa-configure-the-certification-authority-ca-for-crl-publishing"></a><a name="bkmk_configCa"></a> 設定用來發佈 CRL 的憑證授權單位 (CA)  
 憑證授權單位 (CA) 預設會使用以 LDAP 為基礎的憑證撤銷清單 (CRL) 來允許已加入網域之裝置的連線。 您必須將以 HTTP 為基礎的 CRL 新增到 CA，才能讓未加入網域的裝置藉由該 CA 發行的憑證受到信任。 必須要有這些憑證，才能在裝載 Configuration Manager 站台系統角色的伺服器與已註冊內部部署行動裝置管理的裝置之間進行 SSL 通訊。  

 請依照下列步驟來設定 CA，使其自動發佈 CRL 資訊來發行憑證，以允許已加入網域和未加入網域之裝置的受信任連線：  

1.  在為您的站台執行憑證授權單位的伺服器上，按一下 **[開始]** > **[系統管理工具]** > **[憑證授權單位]**。  

2.  在 [憑證授權單位] 主控台中，於 **[CertificateAuthority]**上按一下滑鼠右鍵，然後按一下 **[內容]**。  

3.  在 CertificateAuthority 內容中，按一下 **[延伸]** 索引標籤，確定 **[選取延伸]** 是設定為 **[CRL 發佈點 (CDP)]**  

4.  選取 **http://<伺服器 DNS 名稱\>/CertEnroll/<CA 名稱\><CRL 名稱尾碼\><允許的 Delta CRL\>.crl**。 有下列三個選項：  

    -   **包含在 CRL 中。用戶端用此來尋找 Delta CRL 的位置。**  

    -   **包含在已發行憑證的 CDP 延伸中。**  

    -   **包含在已發行 CRL 的 IDP 延伸中**  

5.  按一下 [結束模組] 索引標籤，並按一下 [內容...]，然後選取 [允許憑證發佈到檔案系統]。  

6.  收到「Active Directory 憑證服務」必須重新啟動的通知時，按一下 **[確定]** 。  

7.  在 **[已撤銷的憑證]**上按一下滑鼠右鍵，按一下 **[所有工作]**，然後按一下 **[發佈]**。  

8.  在 [發佈 CRL] 對話方塊中，選取 **[只有 Delta CRL]**，然後按一下 **[確定]**。  

##  <a name="a-namebkmkcerttempla-create-the-web-server-certificate-template-on-the-ca"></a><a name="bkmk_certTempl"></a> 在 CA 上建立網頁伺服器憑證範本  
 在 CA 上發佈新 CRL 之後，下一步就是建立網頁伺服器憑證範本。 必須要有此範本，才能為裝載註冊點、註冊 Proxy 點、發佈點及裝置管理點站台系統角色的伺服器發行憑證。 這些伺服器將會是站台系統角色與已註冊裝置之間受信任通訊的 SSL 端點。    請依照下列步驟來建立憑證範本︰  

1.  建立一個名為 **ConfigMgr MDM Servers** 的安全性群組，此群組包含執行需要與已註冊裝置進行受信任通訊之站台系統的伺服器。  

2.  在 [憑證授權單位] 主控台中，於 **[憑證範本]** 上按一下滑鼠右鍵，然後按一下 **[管理]** 來載入 [憑證範本] 主控台。  

3.  在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中顯示 [Web 伺服器] 的項目，然後按一下 [複製範本] 。  

4.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition] 。 Configuration Manager 不支援將 Windows Server 2008 憑證範本用在使用 HTTPS 進行的受信任通訊。  

    > [!NOTE]  
    >  如果您使用的 CA 位於 Windows Server 2012 上，則當您按一下 **[複製範本]**時，系統並不會要求您提供憑證範本版本。 反而會在範本內容的 [相容性]  索引標籤處指定：  
    >   
    >  **憑證授權單位**： **Windows Server 2003**  
    >   
    >  **憑證收件者**： **Windows XP / Server 2003**  

5.  在 **[新範本的內容]** 對話方塊的 **[一般]** 索引標籤上，輸入範本名稱 (例如 **ConfigMgr MDM Web Server**) 來產生將在 Configuration Manager 站台系統上使用的 Web 憑證。  

6.  按一下 **[主體名稱]** 索引標籤，選取 **[用這項 Active Directory 資訊來建立]**，然後針對主體名稱格式，指定 **[DNS 名稱]**。 如果已選取 **[使用者主體名稱 (UPN)]** 核取方塊，請從次要主體名稱取消選取核取方塊。  

7.  按一下 [安全性]  索引標籤，並從 [Domain Admins]  和 [Enterprise Admins]  安全性群組中移除 [註冊] 權限。  

8.  按一下 **[新增]**，在文字方塊中輸入 **ConfigMgr IIS Servers**，然後按一下 **[確定]**。  

9. 選取此群組的 [註冊]  權限，但請勿清除 [讀取]  權限。  

10. 按一下 **[確定]** 並關閉 [憑證範本] 主控台。  

11. 在憑證授權單位主控台中，以滑鼠右鍵按一下 [憑證範本] ，按一下 [新增] ，然後再按一下 [要發行的憑證範本] 。  

12. 在 **[啟用憑證範本]** 對話方塊中，選取您剛才建立的新範本 **ConfigMgr MDM Web Server**，然後按一下 **[確定]**。  

##  <a name="a-namebkmkrequestcerta-request-the-web-server-certificate-for-each-site-system-role"></a><a name="bkmk_requestCert"></a> 要求每個站台系統角色的網頁伺服器憑證  
 已註冊進行內部部署行動裝置管理的裝置必須信任裝載註冊點、註冊 Proxy 點、發佈點和裝置管理點的 SSL 端點。  下列步驟描述如何要求 IIS 的網頁伺服器憑證。 針對每部裝載進行內部部署行動裝置管理之其中一個必要站台系統角色的伺服器 (SSL 端點)，您都必須執行此程序。  

1.  在主要站台伺服器上，以系統管理員權限開啟命令提示字元，輸入 **MMC** ，然後按 **[Enter]**。  

2.  在 MMC 中，按一下 **[檔案]** > **[新增/移除嵌入式管理單元]**。  

3.  在 [憑證] 嵌入式管理單元中，選取 **[憑證]**，按一下 **[新增]**，選取 **[電腦帳戶]**，按一下 **[下一步]**，按一下 **[完成]**，然後按一下 **[確定]** 以結束 [新增或移除嵌入式管理單元] 視窗。  

4.  在 **[個人]**上按一下滑鼠右鍵，然後按一下 **[所有工作]** > **[要求新憑證]**。  

5.  在 [憑證註冊精靈] 中，按一下 **[下一步]**，選取 **[Active Directory 註冊原則]** ，然後按一下 **[下一步]**。  

6.  選取網頁伺服器憑證旁的核取方塊 (**ConfigMgr MDM Web Server**)，然後按一下 **[註冊]**。  

7.  註冊完憑證之後，按一下 **[完成]**。  

 由於每部伺服器都需要唯一的網頁伺服器憑證，因此針對每部裝載進行內部部署行動裝置管理之其中一個必要站台系統角色的伺服器，您必須重複執行此程序。  如果一部伺服器裝載了所有站台系統角色，您就只需要要求一個網頁伺服器憑證。  

##  <a name="a-namebkmkbindcerta-bind-the-certificate-to-the-web-server"></a><a name="bkmk_bindCert"></a> 將憑證繫結到網頁伺服器  
 新憑證現在必須繫結到每部裝載內部部署行動裝置管理必要站台系統角色之站台系統伺服器的網頁伺服器。 請為每部裝載註冊點和註冊 Proxy 點站台系統角色的伺服器，依照下列步驟執行操作。 如果一部伺服器裝載了所有站台系統角色，您就只需要依照這些步驟執行一次。 您不需要為發佈點和裝置管理點站台系統角色執行此工作，因為它們在註冊時會自動收到必要的憑證。  

1.  在裝載註冊點、註冊 Proxy 點、發佈點或裝置管理點的伺服器上，按一下 **[開始]** > **[系統管理工具]** > **[IIS 管理員]**。  

2.  在 [連線] 底下，瀏覽到並以滑鼠右鍵按一下 [預設的網站]，然後按一下 [編輯繫結...]  

3.  在 [站台繫結] 對話方塊中，按一下 [https]，然後按一下 [編輯...]  

4.  在 [編輯站台繫結] 對話方塊中，選取您剛才註冊加入 **[SSL 憑證]**的憑證，按一下 **[確定]**，然後按一下 **[關閉]**。  

5.  在 [IIS 管理員] 主控台的 [連線] 底下，選取網頁伺服器，然後在右邊的 [動作] 窗格中，按一下 **[重新啟動]**。  

##  <a name="a-namebkmkexportcerta-export-the-certificate-with-the-same-root-as-the-web-server-certificate"></a><a name="bkmk_exportCert"></a> 將具有相同的根的憑證匯出為網頁伺服器憑證  
 「Active Directory 憑證服務」通常會在所有已加入網域的裝置上安裝來自 CA 的必要憑證。 但未加入網域的裝置如果沒有來自根 CA 的憑證，則無法與站台系統角色進行通訊。 若要取得裝置與站台系統角色通訊所需的憑證，您可以從繫結到網頁伺服器的憑證進行匯出。  

 請依照下列步驟來匯出網頁伺服器憑證的根憑證。  

1.  在 [IIS 管理員] 中，按一下 [預設的網站]，然後在右邊的 [動作] 面板中，按一下 [繫結...]  

2.  在 [站台繫結] 對話方塊中，按一下 [https]，然後按一下 [編輯...]  

3.  請確定已選取網頁伺服器憑證，然後按一下 [檢視...]  

4.  在網頁伺服器憑證的內容中，按一下 **[憑證路徑]**，按一下憑證路徑最上層的根，然後按一下 **[檢視憑證]**。  

5.  在根憑證的內容中，按一下 [詳細資料]，然後按一下 [複製到檔案...]  

6.  在 [憑證匯出精靈] 中，按一下 **[下一步]**。  

7.  確定在格式選取 **[DER 編碼二進位 X.509 (.CER)]** 格式，然後按一下 **[下一步]**。  

8.  針對檔案名稱，按一下 [瀏覽...]，並選擇要儲存憑證檔案的位置，且為檔案命名，然後按一下 [儲存]。  

     要註冊的裝置必須能夠存取此檔案才能匯入根憑證，因此您需選擇一個大多數電腦和裝置都可存取的一般位置，或是可以現在將它儲存到一個方便的位置 (例如 C 磁碟機)，之後再將它移到一般位置。  

     收到「Active Directory 憑證服務」必須重新啟動的通知時，按一下 **[下一步]**之裝置與站台系統伺服器之間受信任通訊的憑證。  

9. 檢閱設定，然後按一下 **[完成]** 。  



<!--HONumber=Nov16_HO1-->


