---
title: "用戶端安裝內容 | System Center Configuration Manager"
description: "了解 System Center Configuration Manager 中的用戶端安裝內容。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: 15
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 3987e6a66f9c0f52da8ce9a8c29e35836d2a2bcb

---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>關於 System Center Configuration Manager 中的用戶端安裝內容

*適用對象：System Center Configuration Manager (最新分支)*

您可以使用 System Center Configuration Manager CCMSetup.exe 命令，在企業的電腦上手動安裝 Configuration Manager 用戶端軟體。  

##  <a name="a-nameaboutccmsetupa-about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> 關於 CCMSetup.exe  
 CCMSetup.exe 命令會從指定的管理點或從指定的來源位置下載所有必要的檔案，以完成用戶端安裝。 這些檔案可能包含下列各項：  

-   安裝 Configuration Manager 用戶端軟體的 Windows Installer 套件 Client.msi。  

-   Microsoft Background Intelligent Transfer Service (BITS) 安裝檔案 (如有必要)。  

-   Windows Installer 安裝檔案 (如有必要)。  

-   Configuration Manager 用戶端的更新和修正程式 (如有必要)。  

> [!NOTE]  
>  在 Configuration Manager 中不能直接執行 Client.msi 檔案。  

 CCMSetup.exe 提供了多個命令列內容，可自訂安裝行為。 此外，您也可以在 CCMSetup.exe 命令列上指定可修改 Client.msi 行為的內容。  

> [!IMPORTANT]  
>  您必須先指定所有必要的 CCMSetup 內容，才能指定 Client.msi 的內容。  

 CCMSetup.exe 及其支援的檔案位於 Configuration Manager 站台伺服器之 Configuration Manager 安裝資料夾的 [Client] 資料夾中。 這個資料夾會以 **&lt;站台伺服器名稱\>\SMS_&lt;站台碼\>\Client** 路徑，與網路共用。  

 在命令列提示字元，CCMSetup.exe 命令會使用下列格式：  

 **CCMSetup.exe [&lt;Ccmsetup 內容\>] [&lt;client.msi 安裝內容>]**  

 範例：  

 **CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01**  

 此範例命令會執行下列動作：  

-   指定名為 SMSMP01 的管理點，要求發佈點清單以下載用戶端安裝來源檔案。  

-   指定如果電腦上已存在 Configuration Manager 用戶端版本，則應停止安裝程序。  

-   指示 client.msi 將用戶端指派為網站碼 S01。  

-   指示 client.msi 使用名為 SMSFP01 的後援狀態點。  

> [!NOTE]  
>  如果內容包含空白字元，請使用引號 ("") 將其括住。  

 下表所述的內容可用於修改 CCMSetup.exe 的安裝行為。  

> [!IMPORTANT]  
>  如果您已擴充 Configuration Manager 的 Active Directory 架構，許多用戶端安裝內容會在 Active Directory 網域服務中發佈，並自動由 Configuration Manager 用戶端讀取。 如需 Active Directory 網域服務中發佈的用戶端安裝內容清單，請參閱 [關於 System Center Configuration Manager 中發佈至 Active Directory 網域服務的用戶端安裝內容](about-client-installation-properties-published-to-active-directory-domain-services.md)。  

##  <a name="a-namebkmkccmsetupcommandlinea-ccmsetupexe-command-line-properties"></a><a name="BKMK_CCMSetupCommandLine"></a> CCMSetup.exe 命令列內容  

-   **/?**  

     開啟 [CCMSetup]  對話方塊，顯示 ccmsetup.exe 的命令列內容。  

     範例： **ccmsetup.exe /?**  

-   **/source:&lt;路徑\>**  

     指定要下載安裝檔案的位置。 您可以使用本機或 UNC 安裝路徑。 檔案可利用伺服器訊息區 (SMB) 通訊協定進行下載。  

    > [!NOTE]  
    >  您可以在命令列中多次使用 **/source** 內容，以指定用於下載安裝檔案的替代位置。  

    > [!IMPORTANT]  
    >  若要使用 **/source** 命令列內容，用於用戶端安裝的 Windows 使用者帳戶必須具有安裝位置的讀取權限。  

     範例：**ccmsetup.exe /source:"\\\computer\folder"**  

-   **/mp:&lt;電腦\>**  

     指定電腦連線的來源管理點，如此電腦就可以找到最接近的發佈點下載用戶端安裝檔案。 如果沒有發佈點或電腦在 4 小時後仍無法從發佈點下載檔案，用戶端便會從指定的管理點下載檔案。  

     電腦會根據用戶端連線的網站系統角色設定，透過 HTTP 或 HTTPS 連線下載檔案。 如果已設定 BITS 節流，則會使用 BITS 節流進行下載。 如果所有發佈點和管理點只針對 HTTPS 用戶端連線進行設定，您必須確認用戶端電腦具備有效的公開金鑰基礎結構 (PKI) 用戶端憑證。  

    > [!NOTE]  
    >  您可以使用 **/mp** 命令列內容指定多個管理點，如此若電腦無法連線到第一個管理點，便會嘗試連線到下一個管理點，以此類推。 當您指定多個管理點時，可使用分號分隔這些值。  

    > [!IMPORTANT]  
    >  此內容只適用於指定初始管理點，以便讓電腦尋找接近的來源，以供下載用戶端安裝檔案。 其並未指定用戶端在安裝後被指派的管理點。 您可以指定任何網站中的任何 Configuration Manager 管理點，為電腦提供可讓其下載用戶端安裝檔案的發佈點清單。  

     例如，當您使用電腦名稱時： **ccmsetup.exe /mp:SMSMP01**  

     例如，當您使用 FQDN 時： **ccmsetup.exe /mp:smsmp01.contoso.com**  

    > [!TIP]  
    >  如果用戶端使用 HTTPS 連線至管理點，您通常需要針對此選項指定 FQDN，而不是電腦名稱。 您所指定的值必須包含在管理點的 PKI 憑證主體或主體別名。 雖然 Configuration Manager 僅支援此 PKI 憑證中的電腦名稱在內部網路進行連線，但基於安全性最佳做法，建議使用 FQDN。  

-   **/retry:&lt;分鐘\>**  

     指定若 CCMSetup.exe 無法下載安裝檔案時重試的間隔時間。 預設值為 [10]  分鐘。 CCMSetup 會持續重試，直到達到 downloadtimeout  安裝內容所指定的限制為止。  

     範例： **ccmsetup.exe /retry:20**  

-   **/noservice**  

     防止 CCMSetup 以服務的形式執行。 當 CCMSetup 以服務的形式執行時，會在電腦本機系統帳戶的內容中執行，如此可能會沒有足夠的權限存取安裝程序所需的網路資源。 當您指定 **/noservice** 選項時，CCMSetup.exe 會在您用於啟動安裝程序的使用者帳戶內容中執行。 此外，如果您使用指令碼執行含 **/service** 內容的 CCMSetup.exe，則 CCMSetup.exe 會在服務啟動後結束，而且可能會因為 CCMSetup 服務執行用戶端安裝而無法正確回報安裝詳細資料。 如果未指定此命令列內容，將會根據預設使用 **/service** 。  

     範例： **ccmsetup.exe /noservice**  

-   **/service**  

     指定 CCMSetup 應以使用本機系統帳戶的服務形式執行。  

     範例： **ccmsetup.exe /service**  

-   **/uninstall**  

     指定應解除安裝 Configuration Manager 用戶端軟體。 如需詳細資訊，請參閱 [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md)。  

     範例： **ccmsetup.exe /uninstall**  

-   **/logon**  

     指定若已安裝任何版本的 Configuration Manager 或 Configuration Manager 用戶端，則應停止用戶端安裝。  

     範例： **ccmsetup.exe /logon**  

-   **/forcereboot**  

     如果是完成用戶端安裝所必需時，指定 CCMSetup 應強制讓用戶端電腦重新啟動。 如果未指定此選項，CCMSetup 會在需要重新啟動時結束，然後在下一次手動重新啟動時繼續進行。  

     範例： **CCMSetup.exe /forcereboot**  

-   **/Bitspriority:&lt;優先順序\>**  

     指定當透過 HTTP 連線下載用戶端安裝檔案時的下載優先順序。 可能值如下所示：  

    -   FOREGROUND  

    -   HIGH  

    -   NORMAL  

    -   LOW  

     預設值為 NORMAL。  

     範例： **ccmsetup.exe /BITSPriority:HIGH**  

-   **/downloadtimeout:&lt;分鐘\>**  

     指定 CCMSetup 在放棄下載前，嘗試下載用戶端安裝檔案的時間長度 (以分鐘為單位)。 預設值為 [1440]  分鐘 (1 天)。  

     範例： **ccmsetup.exe /downloadtimeout:100**  

-   **/UsePKICert**  

     指定此內容時，用戶端會使用包含用戶端驗證的 PKI 憑證 (如果憑證可用)。 如果找不到有效的憑證，用戶端會回復為使用 HTTP 連接及自我簽署的憑證。 若未指定此選項，用戶端會使用自我簽署憑證，同時所有與網站系統的通訊都會透過 HTTP 進行。  

    > [!NOTE]  
    >  在某些情況下，您不需要在安裝用戶端時，將此內容指定為使用 PKI 用戶端憑證。 這些情況包括使用用戶端推入和以軟體更新點為基礎的用戶端安裝來安裝用戶端。 不過，當您手動安裝用戶端並使用 **/mp** 內容來指定設定為只接受 HTTPS 用戶端連線的管理點時，就必須指定此內容。 您還必須在安裝僅能進行網際網路通訊的用戶端時，利用 CCMALWAYSINF=1 內容指定此內容 (搭配以網際網路為基礎的管理點和網站碼的內容)。 如需以網際網路為基礎之用戶端管理的詳細資訊，請參閱 [System Center Configuration Manager 中端點之間的通訊](../../plan-design/hierarchy/communications-between-endpoints.md)中的[從網際網路或未受信任之樹系的用戶端通訊考量](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。  

     範例： **CCMSetup.exe /UsePKICert**  

-   **/NoCRLCheck**  

     指定用戶端不需要在利用 PKI 憑證透過 HTTPS 進行通訊時，檢查憑證撤銷清單 (CRL)。  

     若未指定此選項，用戶端會先檢查 CRL，再使用 PKI 憑證建立 HTTPS 連線。  

     如需用戶端 CRL 檢查的詳細資訊，請參閱 [Plan for Security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) 中的[Plan for security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)。  

     範例： **CCMSetup.exe /UsePKICert /NoCRLCheck**  

-   **/config:&lt;檔\>**  

     指定包含用戶端安裝內容的文字檔名稱。 除非您同時指定 **/noservice** CCMSetup 內容，否則這個檔案必須位於 CCMSetup 資料夾中，即 32 位元或 64 位元作業系統的 %Windir%\\Ccmsetup 資料夾。 如果指定 **/noservice** 內容，此檔案必須與您執行之 CCMSetup.exe 位於相同的資料夾。  

     範例：**CCMSetup.exe /config:&lt;檔名稱.txt\>**  

     使用站台伺服器電腦上 &lt;Configuration Manager 目錄\>\\bin\\&lt;平台\> 資料夾中的 mobileclienttemplate.tcf 檔案，以提供正確的檔案格式。 此檔案也包含註解格式的資訊，其與各區段及使用方式相關。 在 [用戶端安裝] 區段中的下列文字後方指定用戶端安裝內容： **Install=INSTALL=ALL**。  

     [用戶端安裝] 區段項目的範例： **Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100**  

-   **/skipprereq:&lt;檔名\>**

     指定 CCMSetup.exe 不可在安裝 Configuration Manager 用戶端時安裝指定的必要條件程式。  

     範例： **CCMSetup.exe /skipprereq:silverlight.exe** 或 **CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe**  

    > [!NOTE]  
    >  此內容支援輸入多個值。 使用分號字元 (;) 分隔每一個值。  

-   **/forceinstall**  

     指定將解除安裝所有現有的用戶端，然後再安裝新的用戶端。  

-   **/Excludefeatures:&lt;功能\>**  

     指定 CCMSetup.exe 不會在安裝 Configuration Manager 用戶端時安裝指定的功能。  

     範例： **CCMSetup.exe /ExcludeFeatures:ClientUI** 不會在用戶端上安裝軟體中心。  

    > [!NOTE]  
    >  在此版本， **ClientUI** 是 **/ExcludeFeatures** 內容唯一支援的值。  

##  <a name="a-nameccmsetupreturncodesa-ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> CCMSetup.exe 傳回碼  
 CCMSetup.exe 命令會在命令完成時提供下列傳回碼。 若要疑難排解執行命令的問題，請檢視用戶端電腦上的 ccmsetup.log 檔案，來判斷關於傳回碼問題的內容和其他詳細資料。  

|傳回碼|意義|  
|-----------------|-------------|  
|0|成功|  
|6|錯誤|  
|7|需要重新開機|  
|8|安裝程式已在執行中|  
|9|必要條件評估失敗|  
|10|安裝程式資訊清單雜湊驗證失敗|  

##  <a name="a-nameclientmsipropsa-clientmsi-properties"></a><a name="clientMsiProps"></a> Client.msi 內容  
 下列內容可以修改 client.msi 的安裝行為。 如果您使用用戶端推入安裝方法，您也可以在 [用戶端推入安裝內容]  對話方塊的 [用戶端]  索引標籤中指定內容。  

-   **CCMALWAYSINF**  

     設為 1 指定用戶端一定要是以網際網路為基礎，而且永遠不會連線到內部網路。 用戶端的連線類型會顯示 [永遠為網際網路] 。  

     此內容應搭配 CCMHOSTNAME 使用，用於指定以網際網路為基礎之管理點的 FQDN。 此內容也應與 CCMSetup 內容 /UsePKICert 和網站碼搭配使用。  

     如需以網際網路為基礎之用戶端管理的詳細資訊，請參閱 [System Center Configuration Manager 中端點之間的通訊](../../plan-design/hierarchy/communications-between-endpoints.md)中的[從網際網路或未受信任之樹系的用戶端通訊考量](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。  

     範例： **CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC**  

-   **CCMCERTISSUERS**  

     指定憑證簽發者清單，此清單內含 Configuration Manager 站台信任的受信任根憑證 (CA) 授權單位的憑證。  

     如需憑證簽發者清單，以及憑證選取程序期間，用戶端如何使用清單的詳細資訊，請參閱 [Plan for Security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) 中的 [Plan for security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)。  

     根 CA 憑證中的主體屬性會區分大小寫。 這些屬性可使用逗號 (,) 或分號 (;) 分隔。 您可以使用分隔線來指定多個根 CA 憑證。 範例：  

     **CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &amp;#124; CN=Litware Corporate Root CA; O=Litware, Inc.”**  

    > [!TIP]  
    >  參考站台伺服器電腦上 &lt;Configuration Manager 目錄\>\bin\\&lt;平台\> 資料夾中的 mobileclient.tcf 檔案，複製針對站台設定的 **CertificateIssuers=&lt;字串\>**。  

-   **CCMCERTSEL**  

     指定如果用戶端有一個以上的憑證可搭配 HTTPS 通訊使用 (包含用戶端驗證能力的有效憑證) 時的憑證選擇準則。  

     您可以在 [主體名稱] 或 [主體別名] 中搜尋完全相符的項目 (使用 **Subject:**) 或在 [主體名稱] 或 [主體別名] 中搜尋部分相符的項目 (使用 **SubjectStr:**)。 範例：  

     **CCMCERTSEL="Subject:computer1.contoso.com"** 可搜尋 [主體名稱] 或 [主體別名] 中含完全符合電腦名稱 "computer1.contoso.com" 的憑證。  

     **CCMCERTSEL="SubjectStr:contoso.com"** 可搜尋 [主體名稱] 或 [主體別名] 中含 "contoso.com" 的憑證。  

     您也可以在 [主體名稱] 或 [主體替代名稱] 屬性中使用物件識別碼 (OID) 或辨別名稱屬性，例如：  

     **CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"** 會搜尋表示為物件識別碼以及名稱為 Computers 的組織單位屬性。  

     **CCMCERTSEL="SubjectAttr:OU = Computers"** 會搜尋表示為辨別名稱以及已命名電腦的組織單位屬性。  

    > [!IMPORTANT]  
    >  如果您使用 [主體名稱] 方塊，則 **Subject:** 選取準則值的比對程序會區分大小寫，而 **SubjectStr:** 選取準則值的比對程序則不會區分大小寫。  
    >   
    >  如果您使用 [主體別名] 方塊，則 **Subject:** 選取準則值和 **SubjectStr:** 選取準則值的比對程序則不會區分大小寫。  

     憑證選取時，您可以使用的完整屬性清單會列於 [PKI 憑證選擇準則支援的屬性值](#BKMK_attributevalues)。  

     如果有一個以上的憑證符合搜尋，而且 CCMFIRSTCERT 內容已設定為 1，則會選取有效期最長的憑證。  

-   **CCMCERTSTORE**  

     如果用於 HTTPS 通訊的用戶端憑證並未位於電腦存放區中預設的 [個人]  憑證存放區，請指定替代的憑證存放區名稱。  

     範例： **CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"**  

-   **CCMFIRSTCERT**  

     如果設為 1，此內容會指定用戶端應選取有效期最長的 PKI 憑證。 如果您使用的是網路存取保護設定和 IPsec 強制，可能需要此設定。  

     範例： **CCMSetup.exe /UsePKICert CCMFIRSTCERT=1**  

-   **CCMHOSTNAME**  

     如果是透過網際網路管理用戶端，則指定以網際網路為基礎之管理點的 FQDN。  

     請勿指定此選項搭配 SMSSITECODE=AUTO 的安裝內容。 以網際網路為基礎的用戶端，必須直接指派給以網際網路為基礎的網站。  

     範例： **CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"**  

-   **CCMHTTPPORT**  

     指定用戶端在透過 HTTP 與網站系統伺服器通訊時應使用的連接埠。  

     如果未指定連接埠，則會使用預設值 80。  

     範例： **CCMSetup.exe CCMHTTPPORT=80**  

-   **CCMHTTPSPORT**  

     指定用戶端在透過 HTTPS 與網站系統伺服器通訊時應使用的連接埠。 如果未指定連接埠，則會使用預設值 443。  

     範例： **CCMSetup.exe /UsePKICert CCMHTTPSPORT=443**  

-   **SMSPUBLICROOTKEY**  

     指定 Configuration Manager 無法從 Active Directory 網域服務擷取的受信任根金鑰 。 此內容適用於使用 HTTP 和 HTTPS 用戶端通訊的用戶端。 如需詳細資訊，請參閱 [Plan for Security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 中的 [Plan for security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)。  

     範例：**CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>**  

-   **SMSROOTKEYPATH**  

     用於重新安裝 Configuration Manager 受信任根金鑰。 指定包含受信任根金鑰之檔案的完整路徑和檔案名稱。 此內容適用於使用 HTTP 和 HTTPS 用戶端通訊的用戶端。 如需詳細資訊，請參閱 [Plan for Security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 中的 [Plan for security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)。  

     範例：CCMSetup.exe **SMSROOTKEYPATH=&lt;完整路徑和檔案名稱\>**  

-   **RESETKEYINFORMATION**  

     如果 Configuration Manager 用戶端使用錯誤的 Configuration Manager 受信任根金鑰，而且無法連絡受信任管理點以接收新的受信任根金鑰的有效複本時，您必須使用此內容手動移除舊的受信任根金鑰。 這種情況通常會在您將用戶端從某個網站階層移至另一個網站階層時發生。 此內容適用於使用 HTTP 和 HTTPS 用戶端通訊的用戶端。  

     範例： **CCMSetup.exe RESETKEYINFORMATION=TRUE**  

-   **CCMDEBUGLOGGING**  

     啟用偵錯記錄。 這些值可以設定為 0 (關閉) 或 1 (開啟)。 預設值為 0。 如此可讓用戶端記錄低階資訊，這些資訊有助於疑難排解問題。 基於最佳作法，請避免在實際執行的網站使用此內容，因為可能會產生過多記錄，不容易在記錄檔中找到相關資訊。 CCMENABLELOGGING 必須設為 TRUE 才會啟用偵錯記錄。  

     範例： **CCMSetup.exe CCMDEBUGLOGGING=1**  

-   **CCMENABLELOGGING**  

     如果此內容設為 TRUE 則啟用記錄。 預設會啟用記錄。 記錄檔會儲存在 Configuration Manager 用戶端安裝資料夾的 [Logs] 資料夾中。 根據預設，此資料夾為 %Windir%\CCM\Logs。  

     範例： **CCMSetup.exe CCMENABLELOGGING=TRUE**  

-   **CCMLOGLEVEL**  

     指定要寫入 Configuration Manager 記錄檔的詳細資料數目。 指定從 0 到 3 的整數範圍，其中 0 是最詳細的記錄，而 3 只記錄錯誤。 預設為 1。  

     範例： **CCMSetup.exe CCMLOGLEVEL=3**  

-   **CCMLOGMAXHISTORY**  

     當 Configuration Manager 記錄檔的大小達到 250000 位元組 (或是由 CCMLOGMAXSIZE 內容所指定的值) 時，會將記錄檔重新命名以作為備份，並建立新的記錄檔。  

     此內容可指定要保留多少個舊版的記錄檔。 預設值為 1。 如果這個值設定為 0，則不會保留舊的記錄檔。  

     範例： **CCMSetup.exe CCMLOGMAXHISTORY=0**  

-   **CCMLOGMAXSIZE**  

     指定最大的記錄檔大小 (以位元組為單位)。 當記錄成長到所指定的大小時，會將其重新命名為歷程記錄檔案，並建立新的檔案。 此內容必須設定為至少 10000 個位元組。 預設值為 250000 個位元組。  

     範例： **CCMSetup.exe CCMLOGMAXSIZE=300000**  

-   **CCMALLOWSILENTREBOOT**  

     指定電腦允許重新啟動下列用戶端安裝 (如有必要)。  

    > [!IMPORTANT]  
    >  即使目前有使用者登入，電腦也會重新啟動，但不顯示警告。  

     範例： **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

-   **DISABLESITEOPT**  

     如果設定為 TRUE，則停用擁有用戶端電腦上系統管理認證的一般使用者，其在用戶端電腦的 [控制台] 中使用 Configuration Manager 變更 Configuration Manager 用戶端指派站台的能力。  

     範例： **CCMSetup.exe DISABLESITEOPT=TRUE**  

-   **DISABLECACHEOPT**  

     如果設定為 TRUE，則停用擁有用戶端電腦上系統管理認證的一般使用者，其在用戶端電腦的 [控制台] 中使用 Configuration Manager 變更 Configuration Manager 用戶端快取資料夾設定的能力。  

     範例： **CCMSetup.exe DISABLECACHEOPT=TRUE**  

-   **SMSCACHEDIR**  

     指定用戶端電腦上用戶端快取資料夾的位置，此位置用於儲存暫存檔。 根據預設，此位置為 *%Windir \ccmcache*。  

     範例： **CCMSetup.exe SMSCACHEDIR="C:\Temp"**  

     此內容可搭配 SMSCACHEFLAGS 內容使用，以進一步控制用戶端快取位置。  

     範例： **CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE** 會在用戶端的最大可用磁碟機上，安裝用戶端快取資料夾。  

-   **SMSCACHEFLAGS**  

     設定用於儲存暫存檔的 Configuration Manager 快取資料夾。 您可以個別或合併使用 SMSCACHEFLAGS 內容，並使用分號分隔。 如果未指定此內容，則會根據 SMSCACHEDIR 內容安裝用戶端快取資料夾，該資料夾不會壓縮，而 SMSCACHESIZE 值則是當作資料夾的大小 (以 MB 為單位) 來使用。  

     為用戶端快取資料夾指定進一步的安裝詳細資料。 您可以指定下列內容：  

    -   PERCENTDISKSPACE：以總磁碟空間的百分比指定資料夾大小。 如果您指定這個內容，則也必須以要使用的百分比值指定 SMSCACHESIZE 內容。  

    -   PERCENTFREEDISKSPACE：以可用磁碟空間的百分比指定資料夾大小。 如果您指定這個內容，則也必須以要使用的百分比值指定 SMSCACHESIZE 內容。 例如，若磁碟的可用空間為 10 MB，而 SMSCACHESIZE 指定為 50，則資料夾大小會設定為 5 MB。 您不能使用這個內容搭配 PERCENTDISKSPACE 內容使用。  

    -   MAXDRIVE：指定資料夾應該安裝在最大的可用磁碟上。 如果已使用 SMSCACHEDIR 內容指定路徑，則會忽略這個值。  

    -   MAXDRIVESPACE：指定資料夾應安裝在最多可用空間的磁碟機上。 如果已使用 SMSCACHEDIR 內容指定路徑，則會忽略這個值。  

    -   NTFSONLY：指定資料夾只可安裝在以 NTFS 檔案系統進行格式化的磁碟機。 如果已使用 SMSCACHEDIR 內容指定路徑，則會忽略這個值。  

    -   COMPRESS：指定資料夾應保持壓縮格式。  

    -   FAILIFNOSPACE：指定如果沒有足夠的空間可安裝該資料夾，則應移除用戶端軟體。  

    > [!NOTE]  
    >  您可以藉由使用分號各自分隔，為此內容指定多個內容。  

     如果未指定此內容，則會根據 SMSCACHEDIR 內容建立用戶端快取資料夾，不會壓縮資料夾，而且資料夾大小會是 SMSCACHESIZE 內容中指定的大小。  

     範例： **CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS**  

    > [!NOTE]  
    >  當您升級現有的用戶端時，會忽略此設定。  

-   **SMSCACHESIZE**  

     > [!IMPORTANT]
     > 在 Configuration Manager 1606 版中，新的用戶端設定可用於指定用戶端快取資料夾大小。 加入這些用戶端設定實際上會取代使用 SMSCACHESIZE 作為 client.msi 內容來指定用戶端快取大小。 如需詳細資訊，請參閱[快取大小的用戶端設定](about-client-settings.md#client-cache-settings)。  

     對於 1602 和更早版本，SMSCACHESIZE 指定用戶端快取資料夾的大小 (以 MB 為單位)，如果使用 PERCENTDISKSPACE 或 PERCENTFREEDISKSPACE 內容，則以百分比指定。 如果未設定此內容，資料夾預設的大小上限為 5120 MB。 您可以指定的最小值為 1 MB。  

    > [!NOTE]  
    >  如果必須下載的新套件會導致資料夾超過大小上限，而且資料夾無法清除以取得足夠的可用空間時，則套件下載會失敗，而且不會執行程式或應用程式。  

     當您升級現有的用戶端，以及當用戶端下載軟體更新時，會忽略此設定。  

     範例： **CCMSetup.exe SMSCACHESIZE=100**  

    > [!NOTE]  
    >  如果您重新安裝用戶端，則無法使用 SMSCACHESIZE 或 SMSCACHEFLAGS 安裝內容將快取大小設定為比先前設定更小的值。 如果您嘗試這麼做，則您的值會遭到忽略，且快取大小會自動設為上一個設定的大小。  
    >   
    >  例如，若您使用預設快取大小 5120 MB 安裝用戶端，然後再使用快取大小 100 MB 重新安裝用戶端，則重新安裝的用戶端快取資料夾大小會設為 5120 MB。  


-   **SMSCONFIGSOURCE**  

     指定 Configuration Manager 安裝程式檢查組態設定的位置和順序。 此內容是包含一個或多個字元的字串，每一個字元都定義了特定的設定來源。 單獨或合併使用字元值 R、P、M 和 U，如下列範例所示：  

    -   R：檢查登錄中的組態設定。  

         如需 [在登錄中儲存用戶端安裝內容](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision)的資訊，請按一下這裡。  

    -   P：檢查命令提示字元處所提供的安裝屬性中的組態設定。  

    -   M：使用 Configuration Manager 用戶端軟體升級舊版用戶端時，檢查現有設定。  

    -   U：將已安裝的用戶端升級至較新的版本 (且使用指派的站台碼)。  

     根據預設，用戶端安裝會先使用 `PU` 檢查安裝內容，再檢查現有的設定。  

     範例： **CCMSetup.exe SMSCONFIGSOURCE=RP**  

-   **SMSDIRECTORYLOOKUP**  

     指定用戶端是否可以使用 Windows 網際網路名稱服務 (WINS) 尋找接受 HTTP 連線的管理點。 用戶端在 Active Directory 網域服務或 DNS 中找不到管理點時，會使用此方法。  

     此內容與用戶端是否使用 WINS 進行名稱解析無關。  

     您可以為此內容設定兩個不同的模式：  

    -   NOWINS：對此屬性而言，這是最安全的設定，可避免用戶端在 WINS 中尋找管理點。  當您使用此設定時，用戶端必須使用替代方法來找出內部網路上的管理點，例如 Active Directory 網域服務或使用 DNS 發行。  

    -   WINSSECURE：在此模式中，使用 HTTP 通訊的用戶端可以使用 WINS 尋找管理點。 不過，用戶端必須擁有受信任根金鑰的複本，才能順利與管理點連線。 如需詳細資訊，請參閱 [Plan for Security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 中的 [Plan for security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)。  

     如果未指定此內容，則會使用預設值 WINSSECURE。  

     範例： **CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS**  

-   **SMSSIGNCERT**  

     指定網站伺服器上匯出自我簽署憑證的完整路徑和 .cer 檔案名稱。  

     此憑證是儲存在 [SMS]  憑證存放區中，主體名稱為 [網站伺服器]  ，易記名稱為 [網站伺服器簽署憑證] 。  

     範例：**CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;完整路徑和檔案名稱\>**  

-   **SMSMP**  

     指定 Configuration Manager 用戶端要使用的初始管理點。  

    > [!IMPORTANT]  
    >  如果管理點只接受透過 HTTPS 進行用戶端連線 (不允許 HTTP 用戶端連線)，您必須使用 https:// 作為管理點名稱的首碼。  

     範例： **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

     範例： **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

     範例： **CCMSetup.exe SMSMP=https://smsmp01.contoso.com**  

-   **SMSSITECODE**  

     指定要指派 Configuration Manager 用戶端的目標 Configuration Manager 站台。 這可以是三個字元的網站碼或單字 AUTO。 如果指定 AUTO，或者未指定此內容，用戶端會嘗試從 Active Directory 網域服務或從指定的管理點判斷其 Configuration Manager 站台指派。  

    > [!NOTE]  
    >  如果您也指定了以網際網路為基礎的管理點 (CCMHOSTNAME)，就不要使用 AUTO。 在此案例中，您必須直接將用戶端指派至其網站。  

     範例： **CCMSetup.exe SMSSITECODE=XZY**  

-   **CCMINSTALLDIR**  

     識別用於安裝 Configuration Manager 用戶端檔案的資料夾。 如果未設定此內容，會將用戶端軟體安裝在 *%Windir%*\CCM 資料夾中。 無論將這些檔案安裝在何處， Ccmcore.dll 檔案一律安裝在 *%Windir%\System32* 資料夾中。 此外，在 64 位元的作業系統上，Ccmcore.dll 檔案一律安裝在 *%Windir%*\SysWOW64 資料夾中，以支援 32 位元的應用程式，這些應用程式會使用 Configuration Manager 軟體開發人員套件 (SDK) 的 32 位元版 Configuration Manager 用戶端 API。  

     範例： **CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"**  

-   CCMADMINS  

     指定一個或多個 Windows 使用者帳戶或群組，授與用戶端設定和原則的存取權限。 這適用於 Configuration Manager 系統管理員在用戶端電腦上沒有本機系統管理認證的情況。 您可以指定帳戶清單 (以分號分隔)。  

     範例： **CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"**  

-   **FSP**  

     指定後援狀態點，這些狀態點會接收及處理 Configuration Manager 用戶端電腦所傳送的狀態訊息。  

     如需後援狀態點的詳細資訊，請參閱[為 System Center Configuration Manager 用戶端判斷站台系統角色](plan/determine-the-site-system-roles-for-clients.md) 中的[判定您是否需要後援狀態點](plan/determine-the-site-system-roles-for-clients.md#BKMK_Determine_FSP)。  

     範例： **CCMSetup.exe FSP=SMSFP01**  

-   **DNSSUFFIX**  

     指定用戶端的 DNS 網域以尋找在 DNS 中發佈的管理點。 當找到管理點時，會通知用戶端有關階層中的其他管理點。 意思就是，使用 DNS 發佈而找到的管理點不一定要來自用戶端的網站，它可以是階層中的任何管理點。  

    > [!NOTE]  
    >  如果用戶端在相同網域，您不必指定此內容為已發佈的管理點。 在此案例中，會自動使用用戶端的網域來搜尋管理點的 DNS。  

     如需發佈為 Configuration Manager 用戶端服務位置方法之 DNS 的詳細資訊，請參閱[了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)中的[服務位置以及用戶端如何判斷其指派的管理點](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

    > [!NOTE]  
    >  根據預設，Configuration Manager 並未啟用 DNS 發佈功能。  

     範例： **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com**  

-   **CCMEVALINTERVAL**  

     指定用戶端健全狀況評估工具 (ccmeval.exe) 執行的頻率。 您可以指定從 **1** 分鐘到 **1440** 分鐘的值。 如果您並未指定此內容，或者指定的值不正確，則會每天執行一次評估。  

-   **CCMEVALHOUR**  

     指定用戶端健全狀況評估工具 (ccmeval.exe) 執行的時數。 您可以指定介於 **0** (午夜) 和 **23** (晚上 11 點) 之間的值。 如果您並未指定此內容，或者指定的值不正確，則會在午夜執行評估。  

-   **IGNOREAPPVVERSIONCHECK**  

     指定在安裝用戶端之前不檢查 Microsoft Application Virtualization (App-V) 版本是否符合最低需求。  

    > [!IMPORTANT]  
    >  如果安裝 Configuration Manager 用戶端而未安裝 App-V，則無法部署虛擬應用程式。  

     範例： **CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE**  

-   **NOTIFYONLY**  

     指定將報告用戶端狀態，但不補救在 Configuration Manager 用戶端中找到的問題。  

     範例： **CCMSetup.exe NOTIFYONLY=TRUE**  

     如需詳細資訊，請參閱 [如何在 System Center Configuration Manager 中設定用戶端狀態](configure-client-status.md)。  

##  <a name="a-namebkmkattributevaluesa-supported-attribute-values-for-the-pki-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> PKI 憑證選擇準則支援的屬性值  
 Configuration Manager 支援下列 PKI 憑證選擇準則屬性值：  

|OID 屬性|辨別名稱屬性|屬性定義|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|網域元件|  
|1.2.840.113549.1.9.1|E 或 E-mail|電子郵件地址|  
|2.5.4.3|CN|一般名稱|  
|2.5.4.4|SN|主體名稱|  
|2.5.4.5|SERIALNUMBER|序號|  
|2.5.4.6|C|國碼 (地區碼)|  
|2.5.4.7|L|位置|  
|2.5.4.8|S 或 ST|省份名稱|  
|2.5.4.9|STREET|街道地址|  
|2.5.4.10|O|組織名稱|  
|2.5.4.11|OU|組織單位|  
|2.5.4.12|T 或 Title|標題|  
|2.5.4.42|G 或 GN 或 GivenName|指定的名稱|  
|2.5.4.43|I 或 Initials|縮寫|  
|2.5.29.17|(沒有值)|主體替代名稱|  



<!--HONumber=Nov16_HO1-->


