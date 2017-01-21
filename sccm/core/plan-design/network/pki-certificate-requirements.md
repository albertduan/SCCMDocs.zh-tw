---
title: "PKI 憑證需求 | System Center Configuration Manager"
description: "尋找 System Center Configuration Manager 可能需要的 PKI 憑證需求。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6a73e68-57d8-4786-842b-36669541d8ff
caps.latest.revision: 17
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fbc85f65e4ad952d40161e6f6282bb6c0796662b


---
# <a name="pki-certificate-requirements-for-system-center-configuration-manager"></a>System Center Configuration Manager 的 PKI 憑證需求

*適用對象：System Center Configuration Manager (最新分支)*

下表列出 System Center Configuration Manager 可能需要的公開金鑰基礎結構 (PKI) 憑證。 這項資訊假設已具備 PKI 憑證的基本知識。 如需逐步部署指引，請參閱[為 System Center Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)。 如需有關 Active Directory 憑證服務的詳細資訊，請參閱下列文件：  

-   Windows Server 2012： [Active Directory 憑證服務概觀](http://go.microsoft.com/fwlink/p/?LinkId=286744)  

-   Windows Server 2008： [Windows Server 2008 中的 Active Directory 憑證服務](http://go.microsoft.com/fwlink/p/?LinkId=115018)  

> [!IMPORTANT]  
>  自 2017 年 1 月 1 日起生效，Windows 將不再信任以 SHA-1 簽署的憑證。  建議您發行以 SHA-2 簽署的新伺服器及用戶端驗證憑證。  
>   
>  如需此變更的詳細資料以及可能的期限更新，請關注此部落格文章： [Windows 強制的 Authenticode 碼簽署及時間戳記](http://social.technet.microsoft.com/wiki/contents/articles/32288.windows-enforcement-of-authenticode-code-signing-and-timestamping.aspx)  

 除了 System Center Configuration Manager 在行動裝置及 Mac 電腦上註冊的用戶端憑證、Microsoft Intune 自動建立用於管理行動裝置的憑證，以及 System Center Configuration Manager 安裝在 AMT 電腦上的憑證之外，您可以使用任何 PKI 建立、部署及管理下列憑證。 不過，當您使用 Active Directory 憑證服務及憑證範本時，此 Microsoft PKI 解決方案可簡化憑證管理工作。 使用下表中的 [要使用的 Microsoft 憑證範本]  欄，可找出最符合憑證需求的憑證範本。 範本憑證只能由執行 Enterprise Edition 或 Datacenter Edition 伺服器作業系統 (例如 Windows Server 2008 Enterprise 和 Windows Server 2008 Datacenter) 的企業憑證授權單位發出。  

> [!IMPORTANT]  
>  如果您使用企業憑證授權單位和憑證範本，請勿使用第 3 版範本。 這些憑證範本會建立與 System Center Configuration Manager 不相容的憑證。 請改用第 2 版範本，同時請遵循下列指示：  
>   
>  -   Windows Server 2012 上的 CA：在憑證範本內容中的 [相容性]  索引標籤上，為 [憑證授權單位]  選項指定 **Windows Server 2003** ，並為 [憑證接收者]  選項指定 **Windows XP / Server 2003** 。  
> -   Windows Server 2008 上的 CA：當您複製憑證範本時，請在 [重複的範本]  快顯對話方塊提示您時，保留預設選擇 [Windows Server 2003 Enterprise]  。 請勿選取 [Windows Server 2008, Enterprise Edition] 。  

 利用下面各節檢視憑證需求。  

##  <a name="a-namebkmkpkicertificatesforserversa-pki-certificates-for-servers"></a><a name="BKMK_PKIcertificates_for_servers"></a> 伺服器的 PKI 憑證  

|System Center Configuration Manager 元件|憑證用途|[要使用的 Microsoft 憑證範本]|憑證中的特定資訊|System Center Configuration Manager 如何使用憑證|  
|-------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|執行 Internet Information Services (IIS) 且設定為使用 HTTPS 用戶端連線的網站系統：<br /><br /> - 管理點<br /><br /> - 發佈點<br /><br /> - 軟體更新點<br /><br /> - 狀態移轉點<br /><br /> - 註冊點<br /><br /> - 註冊 Proxy 點<br /><br /> - 應用程式類別目錄 Web 服務點<br /><br /> - 應用程式類別目錄網站點<br /><br /> - 憑證登錄點|伺服器驗證|**Web 伺服器**|**[增強金鑰使用方法]** 值必須包含 **[伺服器驗證 (1。3。6。1。5。5。7。3。1)]**。<br /><br /> 如果網站系統接受來自網際網路的連線，則 [主體名稱] 或 [主體別名] 必須包含網際網路完整網域名稱 (FQDN)。<br /><br /> 如果網站系統接受來自內部網路的連線，則根據網站系統的設定，[主體名稱] 或 [主體別名] 必須包含內部網路 FQDN (建議使用) 或電腦名稱。<br /><br /> 如果網站系統同時接受來自網際網路及內部網路的連線，則必須同時指定網際網路 FQDN 和內部網路 FQDN (或電腦名稱)，並使用 (&) 符號分隔兩個名稱。<br /><br /> **注意：**若軟體更新點只接受來自網際網路的用戶端連線，則憑證必須同時包含網際網路 FQDN 和內部網路 FQDN。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> System Center Configuration Manager 不會指定此憑證支援的金鑰長度上限。 請查閱您的 PKI 和 IIS 文件，了解此憑證的任何金鑰大小相關問題。|此憑證必須位於 [電腦] 憑證存放區的 [個人] 存放區中。<br /><br /> 此 Web 伺服器憑證可用來對用戶端驗證這些伺服器，以及使用安全通訊端層 (SSL) 加密用戶端與這些伺服器之間傳送的所有資料。|  
|雲端發佈點|伺服器驗證|**Web 伺服器**|**[增強金鑰使用方法]** 值必須包含 **[伺服器驗證 (1。3。6。1。5。5。7。3。1)]**。<br /><br /> [主體名稱] 必須包含 FQDN 格式的客戶定義服務名稱及網域，做為特定雲端架構發佈點執行個體的 [一般名稱]。<br /><br /> 私密金鑰必須可匯出。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度：2048 位元。|此服務憑證用來向 Configuration Manager 用戶端驗證雲端架構發佈點服務，以及將使用安全通訊端層 (SSL) 在它們之間傳送的所有資料加密。此憑證必須以公開金鑰憑證標準 (PKCS #12) 格式匯出，並且必須知道密碼，以便在您建立雲端架構發佈點時，可以將它匯入。<br /><br /> **注意：** 此憑證會搭配 Windows Azure 管理憑證使用。 如需此憑證的詳細資訊，請參閱 MSDN Library 之＜Windows Azure 平台＞一節中的 [如何建立管理憑證](http://go.microsoft.com/fwlink/p/?LinkId=220281) 和 [如何將管理憑證加入 Windows Azure 訂閱中](http://go.microsoft.com/fwlink/?LinkId=241722) 。|  
|執行 Microsoft SQL Server 的網站系統伺服器|伺服器驗證|**Web server**|**[增強金鑰使用方法]** 值必須包含 **[伺服器驗證 (1。3。6。1。5。5。7。3。1)]**。<br /><br /> [主題名稱] 必須包含內部網路完整網域名稱 (FQDN)。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2048 位元。|此憑證必須位於 [電腦] 憑證存放區的 [個人] 存放區中，且 System Center Configuration Manager 會自動將此憑證複製到 System Center Configuration Manager 階層中可能需要與伺服器建立信任之伺服器的 [受信任人的存放區]。<br /><br /> 這些憑證用於伺服器對伺服器驗證。|  
|SQL Server 叢集：執行 Microsoft SQL Server 的站台系統伺服器|伺服器驗證|**Web server**|**[增強金鑰使用方法]** 值必須包含 **[伺服器驗證 (1。3。6。1。5。5。7。3。1)]**。<br /><br /> [主題名稱] 必須包含叢集的內部網路完整網域名稱 (FQDN)。<br /><br /> 私密金鑰必須可匯出。<br /><br /> 當您設定 System Center Configuration Manager 使用 SQL Server 叢集時，憑證必須至少有兩年的有效期間。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2048 位元。|您在叢集中的某個節點上要求並安裝此憑證後，請匯出憑證，再將它匯入 SQL Server 叢集中每個額外的節點。<br /><br /> 此憑證必須位於 [電腦] 憑證存放區的 [個人] 存放區中，且 System Center Configuration Manager 會自動將此憑證複製到 System Center Configuration Manager 階層中可能需要與伺服器建立信任之伺服器的 [受信任人的存放區]。<br /><br /> 這些憑證用於伺服器對伺服器驗證。|  
|下列網站系統角色的網站系統監視：<br /><br /> 管理點<br /><br /> 狀態移轉點|用戶端驗證|**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]**。<br /><br /> 電腦的 [主體名稱] 欄位或 [主體別名] 欄位中必須擁有唯一的值。<br /><br /> **注意：**如果您使用多個值作為 [主體別名]，則只會使用第一個值。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2048 位元。|即使未安裝 System Center Configuration Manager 用戶端，列出的網站系統伺服器上仍必須有此憑證，如此才能監視這些網站系統角色的健全狀況並且回報網站。<br /><br /> 這些網站系統的憑證必須位於 [電腦] 憑證存放區的 [個人] 存放區中。|  
|執行 System Center Configuration Manager 原則模組與網路裝置註冊服務角色服務的伺服器。|用戶端驗證|工作站驗證|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]**。<br /><br /> 對於憑證主體或主體別名 (SAN) 並無特定需求，您可以針對多個執行網路裝置註冊服務之伺服器使用同一個憑證。<br /><br /> 支援 SHA-2 及 SHA-3 雜湊演算法。<br /><br /> 支援的金鑰長度：1024 位元及 2048 位元。||  
|已安裝發佈點的網站系統|用戶端驗證|**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]**。<br /><br /> 對於憑證主體或主體別名 (SAN) 並無特定需求，您可以針對多個發佈點使用同一個憑證。 不過，我們建議每個發佈點使用不同的憑證。<br /><br /> 私密金鑰必須可匯出。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2048 位元。|此憑證有兩種用途：<br /><br /> - 在發佈點傳送狀態訊息之前，對啟用 HTTPS 的管理點驗證發佈點。<br /><br /> - 若已選取 [為用戶端啟用 PXE 支援] 發佈點選項，憑證會傳送至電腦，這樣一來，如果作業系統部署程序中的工作順序，包含如用戶端原則抓取或傳送清查資訊等用戶端動作，用戶端電腦就能在部署作業系統期間連線到啟用 HTTPS 的管理點。<br /><br /> 此憑證僅於作業系統部署程序期間使用，不會安裝到用戶端上。 由於是暫時使用的緣故，如果不想使用多個用戶端憑證，您可以在每次部署作業系統時使用同一個憑證。<br /><br /> 此憑證必須以公開金鑰憑證標準 (PKCS #12) 格式匯出，而且必須得知密碼，才能匯入至發佈點內容。<br /><br /> **注意：** 此憑證的需求與用於部署作業系統之開機映像的用戶端憑證相同。 由於需求相同，因此您可以使用相同的憑證檔案。|  
|超出訊號範圍服務點|AMT 佈建|**Web 伺服器** (已修改)|[增強金鑰使用方法] 值必須包含 [伺服器驗證 (1.3.6.1.5.5.7.3.1)]  及下列物件識別碼： **2.16.840.1.113741.1.2.3**。<br /><br /> [主體名稱] 欄位必須包含裝載超出訊號範圍服務點的伺服器 FQDN。<br /><br /> **注意：** 如果您向外部 CA 而不是向自己的內部 CA 要求 AMT 佈建憑證，而它不支援 AMT 佈建物件識別碼 2.16.840.1.113741.1.2.3，您可以改為指定下列文字字串作為憑證主體名稱中的組織單位 (OU) 屬性： **Intel(R) Client Setup Certificate**。 除了裝載超出訊號範圍服務點的伺服器 FQDN 之外，還必須使用與上述完全相同的英文字串，大小寫須相符，而且後面沒有句號。<br /><br /> 支援的金鑰長度：1024 及 2048。 AMT 6.0 和更新版本也支援 4096 位元的金鑰長度。|此憑證位於超出訊號範圍服務點網站系統伺服器的 [電腦] 憑證存放區中的 [個人] 存放區。<br /><br /> 此 AMT 佈建憑證用來準備電腦進行超出訊號範圍的管理。<br /><br /> 您必須向提供 AMT 佈建憑證的 CA 要求此憑證，而且 Intel AMT 電腦的 BIOS 擴充功能必須設定為針對此佈建憑證使用根憑證指紋 (也稱為憑證雜湊)。<br /><br /> VeriSign 是提供 AMT 佈建憑證的外部 CA 典型範例，但您也可以使用自己的內部 CA。<br /><br /> 將憑證安裝到裝載超出訊號範圍服務點的伺服器上，該服務點必須能夠成功鏈結至憑證的根 CA (根據預設，VeriSign 的根 CA 憑證及中繼 CA 憑證惠在 Windows 安裝時一併安裝)。|  
|執行 Microsoft Intune 連接器的網站系統伺服器|用戶端驗證|不適用：Intune 會自動建立此憑證。|[增強金鑰使用方法] 值包含用戶端驗證 (1.3.6.1.5.5.7.3.2)。<br /><br /> 3 個自訂延伸模組可作為客戶 Intune 訂閱的唯一識別。<br /><br /> 金鑰大小是 2048 位元，並且使用 SHA-1 雜湊演算法。<br /><br /> **注意：** 您無法變更這些設定：此資訊僅供參考。|此憑證會在您訂閱 Microsoft Intune 時，自動要求並安裝到 Configuration Manager 資料庫。 當您安裝 Microsoft Intune 連接器時，此憑證就會安裝到執行 Microsoft Intune 連接器的網站系統伺服器上。 憑證會安裝到 [電腦] 憑證存放區中。<br /><br /> 此憑證用於使用 Microsoft Intune 連接器對 Microsoft Intune 驗證 Configuration Manager 階層。 兩者之間一律使用安全通訊端層 (SSL) 傳送資料。|  

###  <a name="a-namebkmkpkicertificatesforproxyserversa-proxy-web-servers-for-internet-based-client-management"></a><a name="BKMK_PKIcertificates_for_proxyservers"></a> 以網際網路為基礎的用戶端管理的 Proxy 網頁伺服器  
 如果網站支援以網際網路為基礎的用戶端管理，且您透過使用 SSL 終止 (橋接) 功能進行傳入網際網路連線的方式使用 Proxy Web 伺服器，則該 Proxy Web 伺服器具備下表所列的憑證需求。  

> [!NOTE]  
>  如果您使用 Proxy Web 伺服器但不使用 SSL 終止 (通道) 功能，Proxy Web 伺服器便不需 要其他憑證。  

|網路基礎結構元件|憑證用途|[要使用的 Microsoft 憑證範本]|憑證中的特定資訊|System Center Configuration Manager 如何使用憑證|  
|--------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|透過網際網路接受用戶端連線的 Proxy Web 伺服器|伺服器驗證與用戶端驗證|1. <br />                        **Web 伺服器**<br /><br /> 2. <br />                        **工作站驗證**|[主體名稱] 欄位或 [主體別名] 欄位中的網際網路 FQDN (如果您使用 Microsoft 憑證範本，則 [主體別名] 僅適用於工作站範本)。<br /><br /> 支援 SHA-2 雜湊演算法。|此憑證用於對網際網路用戶端驗證下列伺服器，以及加密用戶端及此伺服器之間使用 SSL 傳送的所有資料：<br /><br /> - 以網際網路為基礎的管理點<br /><br /> - 以網際網路為基礎的發佈點<br /><br /> - 以網際網路為基礎的軟體更新點<br /><br /> 用戶端驗證用於橋接 System Center Configuration Manager 用戶端及以網際網路為基礎之網站系統之間的用戶端連線。|  

##  <a name="a-namebkmkpkicertificatesforclientsa-pki-certificates-for-clients"></a><a name="BKMK_PKIcertificates_for_clients"></a> 用戶端的 PKI 憑證  

|System Center Configuration Manager 元件|憑證用途|[要使用的 Microsoft 憑證範本]|憑證中的特定資訊|System Center Configuration Manager 如何使用憑證|  
|-------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|Windows 用戶端電腦|用戶端驗證|**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]**。<br /><br /> 用戶端電腦的 [主體名稱] 欄位或 [主體別名] 欄位中必須包含唯一值。<br /><br /> **注意：**如果您使用多個值作為 [主體別名]，則只會使用第一個值。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2048 位元。|根據預設，System Center Configuration Manager 會在電腦憑證存放區的個人存放區中尋找電腦憑證。<br /><br /> 除了軟體更新點和應用程式類別目錄網站點外，此憑證可以在執行 IIS 的網站系統伺服器及設定使用 HTTPS 的伺服器上驗證用戶端。|  
|行動裝置用戶端|用戶端驗證|**驗證的工作階段**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]**。<br /><br /> SHA-1<br /><br /> 支援的金鑰長度上限是 2048 位元。<br /><br /> **注意：**<br /><br /> - 這些憑證的格式必須是可辨別編碼規則 (DER) 編碼二進位 X.509。<br /><br /> 不支援 Base64 編碼的 X.509 格式。|此憑證會在與行動裝置用戶端通訊的網站系統伺服器 (例如管理點和發佈點) 驗證該用戶端。|  
|部署作業系統的開機映像|用戶端驗證|**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]**。<br /><br /> 憑證的 [主體別名] 欄位或 [主體別名 (SAN)] 皆無特定需求，所有開機映像皆可使用同一個憑證。<br /><br /> 私密金鑰必須可匯出。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2048 位元。|如果作業系統部署程序中的工作順序包含擷取用戶端原則或傳送清查資訊之類的用戶端動作，便會使用憑證。<br /><br /> 此憑證僅於作業系統部署程序期間使用，不會安裝到用戶端上。 由於是暫時使用的緣故，如果不想使用多個用戶端憑證，您可以在每次部署作業系統時使用同一個憑證。<br /><br /> 您必須以公開金鑰憑證標準 (PKCS #12) 格式匯出此憑證，而且必須知道密碼，才能將憑證匯入 System Center Configuration Manager 開機映像中。<br /><br /> 此憑證是暫時提供給工作順序使用，並非用於安裝用戶端。 如果您的環境只有 HTTPS ，則用戶端必須具備可與站台通訊並且讓部署可以繼續進行的有效憑證。 用戶端憑證在用戶端加入 Active Directory 時即可自動產生，或您可以使用其他方法安裝用戶端憑證。<br /><br /> **注意：** 此憑證的需求與裝有發佈點之站台系統的伺服器憑證需求相同。 由於需求相同，因此您可以使用相同的憑證檔案。|  
|Mac 用戶端電腦|用戶端驗證|System Center Configuration Manager 註冊︰**驗證工作階段**<br /><br /> 獨立於 System Center Configuration Manager 的憑證安裝：**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]**。<br /><br /> 針對建立使用者憑證的 System Center Configuration Manager，會在憑證的 [主體] 值中自動填入註冊 Mac 電腦者的使用者名稱。<br /><br /> 若憑證安裝作業不使用 System Center Configuration Manager 註冊，而是從 System Center Configuration Manager 獨立部署電腦憑證，該憑證的 [主體] 值必須是唯一的。 例如，請指定該電腦的 FQDN。<br /><br /> 不支援 [主體別名] 欄位。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2048 位元。|此憑證會在與 Mac 用戶端電腦通訊的網站系統伺服器 (例如管理點和發佈點) 驗證該電腦。|  
|Linux 及 UNIX 用戶端電腦|用戶端驗證|**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]**。<br /><br /> 不支援 [主體別名] 欄位。<br /><br /> 私密金鑰必須可匯出。<br /><br /> 如果用戶端的作業系統支援 SHA-2，則支援 SHA-2 雜湊演算法。 如需詳細資訊，請參閱 [Planning for client deployment to Linux and UNIX computers in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md) (在 System Center Configuration Manager 中規劃 Linux 和 UNIX 電腦的用戶端部署) 中的 [About Linux and UNIX Operating Systems That do not Support SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256) (不支援 SHA-256 的 Linux 和 UNIX 作業系統) 一節。<br /><br /> 支援的金鑰長度：2048 位元。<br /><br /> **注意：** 這些憑證的格式必須是識別名編碼規則 (DER) 編碼二進位 X.509。 不支援 Base64 編碼的 X.509 格式。|此憑證會在與 Mac 用戶端電腦通訊的網站系統伺服器 (例如管理點和發佈點) 驗證該電腦。 必須以公開金鑰憑證標準 (PKCS#12) 格式匯出此憑證，而且必須知道密碼，才能在指定 PKI 憑證時將此憑證指定至用戶端。<br /><br /> 如需詳細資訊，請參閱 [Planning for client deployment to Linux and UNIX computers in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md) (在 System Center Configuration Manager 中規劃 Linux 和 UNIX 電腦的用戶端部署) 中的 [About Linux and UNIX Operating Systems That do not Support SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_SecurityforLnU) (不支援 SHA-256 的 Linux 和 UNIX 作業系統) 一節。|  
|- 下列情況適用的根憑證授權單位 (CA) 憑證：<br /><br /> - 作業系統部署<br /><br /> - 行動裝置註冊<br /><br /> - Intel AMT 型電腦 RADIUS 伺服器驗證<br /><br /> - 用戶端憑證驗證|信任來源的憑證鏈結|不適用。|標準的根 CA 憑證。|當用戶端需要將通訊伺服器的憑證鏈結到信任的來源時，必須提供根 CA 憑證。 下列情況皆適用：<br /><br /> - 部署作業系統時，以及將用戶端電腦連線至設定使用 HTTPS 之管理點的工作順序執行時。<br /><br /> - 當您註冊受 System Center Configuration Manager 管理的行動裝置時。<br /><br /> - 使用 802.1X 驗證 AMT 型電腦，且想指定 RADIUS 伺服器根憑證的檔案時。<br /><br /> 此外，如果用戶端憑證的 CA 與核發管理點憑證的 CA 屬於不同階層，必須提供用戶端的根 CA 憑證。|  
|Intel AMt 型電腦|伺服器驗證。|**Web 伺服器** (已修改)<br /><br /> 您必須設定 [用這項 Active Directory 資訊來建立] 的 [主體名稱]，然後針對 [主體名稱格式]  選取 [一般名稱] 。<br /><br /> 您必須將 [讀取]  和 [註冊]  權限授與在超出訊號範圍管理元件內容中指定的萬用安全性群組。|**[增強金鑰使用方法]** 值必須包含 **[伺服器驗證 (1。3。6。1。5。5。7。3。1)]**。<br /><br /> [主體名稱] 必須包含 AMT 型電腦的 FQDN (Active Directory 網域服務會自動提供)。|此憑證位於電腦管理控制器的非動態隨機存取記憶體中，在 Windows 使用者介面中無法看見。<br /><br /> 每部 Intel AMT 型電腦都會在 AMT 佈建及後續更新期間要求此憑證。 如果從這些電腦中移除 AMT 佈建資訊，就會撤銷此憑證。<br /><br /> 此憑證安裝在 Intel AMT 型電腦上時，會一併安裝根 CA 的憑證鏈結。 AMT 型電腦無法支援金鑰長度超過 2048 位元的 CA 憑證。<br /><br /> 將憑證安裝在 Intel AMT 型電腦上後，此憑證會對超出訊號範圍的服務點系統伺服器及執行超出訊號範圍管理主控台的電腦驗證 AMT 型電腦，並且使用傳輸層安全性 (TLS) 加密在電腦之間傳送的所有資料。|  
|Intel AMT 802.1X 用戶端憑證|用戶端驗證|**工作站驗證**<br /><br /> 您必須將 [主體名稱] 設為 [用這項 Active Directory 資訊來建立] ，然後在 [主體名稱格式]  中選取 [一般名稱] 、清除 DNS 名稱，然後選取 [使用者主要名稱 (UPN)] 為替代主體名稱。<br /><br /> 您必須將此憑證範本的權限授與在超出訊號範圍管理元件內容 [讀取]  和 [註冊]  中指定的萬用安全性群組。|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]**。<br /><br /> 主體名稱欄位必須包含 AMT 型電腦的 FQDN，主體別名則必須包含 UPN。<br /><br /> 支援的金鑰長度上限：2048 位元。|此憑證位於電腦管理控制器的非動態隨機存取記憶體中，在 Windows 使用者介面中無法看見。<br /><br /> 每部 Intel AMT 型電腦皆可在 AMT 佈建期間要求此憑證，但即使移除 AMT 佈建資訊，也不會撤銷此憑證。<br /><br /> 將憑證安裝在 AMT 型電腦上後，此憑證會對 RADIUS 伺服器驗證 AMT 型電腦，以便獲得網路存取權限。|  
|由 Microsoft Intune 註冊的行動裝置|用戶端驗證|不適用：Intune 會自動建立此憑證。|[增強金鑰使用方法] 值包含用戶端驗證 (1.3.6.1.5.5.7.3.2)。<br /><br /> 作為客戶 Intune 訂閱唯一識別的 3 個自訂延伸模組。<br /><br /> 使用者可以在註冊期間提供憑證主體的值。 不過，Intune 不會使用此值識別裝置。<br /><br /> 金鑰大小是 2048 位元，並且使用 SHA-1 雜湊演算法。<br /><br /> **注意：** 您無法變更這些設定：此資訊僅供參考。|驗證使用者使用 Microsoft Intune 註冊行動裝置時，會自動要求並安裝此憑證。 裝置上產生的憑證位於電腦存放區中，並且會對 Intune 驗證註冊的行動裝置，以便管理該裝置。<br /><br /> 由於憑證中有自訂延伸模組，因此只能驗證針對組織建立的 Intune 訂閱。|



<!--HONumber=Nov16_HO1-->


