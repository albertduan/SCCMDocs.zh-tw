---
title: "部署 Windows 用戶端 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
caps.latest.revision: 13
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: daf9ebae82eb5933e211a08d61f0c82a261d4aa7


---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦

*適用於：System Center Configuration Manager (最新分支)*

您可以使用不同的用戶端部署方法，在電腦上安裝 Configuration Manager 用戶端軟體。 請參閱 [Client installation methods in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md) (System Center Configuration Manager 中的客戶端安裝方法) 以協助您決定要使用的部署方法。  

 安裝 Configuration Manager 用戶端前，請先確定所有必要條件已就緒，而且已完成所有必要的部署設定。 如需詳細資訊，請參閱[在 System Center Configuration Manager 將用戶端部署至 Windows 電腦的必要條件](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)。  


##  <a name="a-namebkmkclientpusha-how-to-install-clients-with-client-push"></a><a name="BKMK_ClientPush"></a> 如何使用用戶端推入安裝用戶端  

 使用用戶端推入安裝，在 Configuration Manager 探索到的電腦上安裝 Configuration Manager 用戶端軟體。 您可以為網站設定用戶端推入安裝，用戶端安裝將會在網站設定的界限 (如果這些界限已設定為界限群組) 內探索到的電腦上自動執行。 或者，您可以針對特定集合或集合中的資源執行 [用戶端推入安裝精靈]，以起始用戶端推入安裝。  

 您也可以使用 [用戶端推入安裝精靈]，將 Configuration Manager 用戶端安裝到執行查詢而取得結果的裝置。 在此情況下若要順利安裝，由選定查詢傳回的其中一個項目必須是來自 [系統資源]  屬性類別的 [ResourceID] 屬性。 如需查詢的詳細資訊，請參閱 [System Center Configuration Manager 的查詢技術參考](../../../core/servers/manage/queries-technical-reference.md)。  

 如果網站伺服器無法連絡用戶端電腦或啟動安裝程序，將會每小時重複執行安裝，連續執行七天，直到安裝成功為止。  

 若要協助追蹤用戶端安裝程序，請先安裝後援狀態點網站系統，再安裝用戶端。 後援狀態點在安裝時，會在藉由用戶端推入安裝方法進行安裝時，自動指派給用戶端。 檢視用戶端部署和指派報表，以追蹤用戶端安裝程序。 此外，用戶端記錄檔會提供更詳細的疑難排解資訊，不需要安裝後援狀態點。 例如，網站伺服器上的 CCM.log 檔案會記錄網站伺服器連線至電腦時所發生的任何問題，而用戶端上的 CCMSetup.log 檔案則會記錄安裝程序。  

> [!IMPORTANT]  
>  若要順利完成用戶端推入，請確定所有必要條件已就緒。 這些會列於[在 System Center Configuration Manager 中將用戶端部署到 Windows 電腦的先決條件](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)中的＜安裝方法相依性＞一節。  

### <a name="to-configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>將網站設定為自動針對探索到的電腦使用用戶端推入

1.  在 Configuration Manager 主控台中，按一下 [系統管理]   

2.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [網站] 。  

3.  在 [網站]  清單中，選取您要為其設定自動全網站用戶端推入安裝的網站。  

4.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [用戶端安裝設定] 然後按一下 [用戶端推入安裝] 。  

5.  在 [用戶端推入安裝內容]  對話方塊的 [一般]  索引標籤上，選取 [啟用自動全網站用戶端推入安裝] 。 選取 [伺服器]、[工作站] 或 [Configuration Manager 站台系統伺服器]，以選取 Configuration Manager 應推入用戶端軟體的系統類型。 預設的選取項目為 [伺服器]  和 [工作站] 。  

6.  選取您是否要在網域控制站上，使用自動全網站用戶端推入安裝來安裝 Configuration Manager 用戶端軟體。  

7.  在 [帳戶] 索引標籤上，指定一或多個帳戶，讓 Configuration Manager 在連線至要安裝用戶端軟體的電腦時使用這些帳戶。 按一下 [建立]  圖示，輸入 [使用者名稱]  和 [密碼] ，確認密碼，然後按一下 [確定] 。 您必須指定至少一個用戶端推送安裝帳戶，在您要安裝用戶端的每部電腦上，它都必須有本機系統管理員權限。 如果您未指定用戶端推入安裝帳戶，Configuration Manager 會嘗試使用站台系統電腦帳戶，這會造成跨網域用戶端推入失敗。  

    > [!IMPORTANT]  
    >  用戶端推入安裝帳戶的密碼只能使用 38 個 (含) 以下的字元。  

    > [!NOTE]  
    >  如果您打算從次要網站使用用戶端推入安裝方法，則必須在起始用戶端推入的次要網站上指定該帳戶。  
    >   
    >  如需用戶端推入安裝帳戶的詳細資訊，請參閱下一個程序＜使用用戶端推入安裝精靈＞。  

8.  在 [安裝內容] 索引標籤上，指定安裝 Configuration Manager 用戶端時要使用的所有安裝內容。 您可以指定 Windows Installer 封裝 (Client.msi) 的安裝屬性，以及下列 CCMSetup.exe 屬性：  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     如果已針對 Configuration Manager 延伸架構，並由用戶端安裝讀取 (其中 CCMSetup 是在未使用安裝內容的情況下執行)，則在此索引標籤中指定的用戶端安裝內容便會發佈到 Active Directory 網域服務。 如需用戶端安裝內容的詳細資訊，請參閱 [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (關於 System Center Configuration Manager 中的用戶端安裝內容)。  

    > [!NOTE]  
    >  如果您在次要站台上啟用用戶端推入安裝，請確定已將 SMSSITECODE 內容設定為其父主要站台的 Configuration Manager 站台名稱。 如果已延伸 Configuration Manager 的 Active Directory 架構，您也可以將此內容設定為 AUTO，以自動尋找正確的站台指派。  

### <a name="to-use-the-client-push-installation-wizard"></a>使用用戶端推入安裝精靈

1.  在 Configuration Manager 主控台中，按一下 [系統管理]   

2.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [網站] 。  

3.  在 [網站]  清單中，選取您要為其設定自動全網站用戶端推入安裝的網站。  

4.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [用戶端安裝設定] 然後按一下 [用戶端推入安裝] 。  

5.  在 [安裝內容] 索引標籤上，指定安裝 Configuration Manager 用戶端時要使用的所有安裝內容。 您可以指定 Windows Installer 封裝 (Client.msi) 的安裝屬性，以及下列 CCMSetup.exe 屬性：  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     如果已針對 Configuration Manager 延伸架構，並由用戶端安裝讀取 (其中 CCMSetup 是在未使用安裝內容的情況下執行)，則在此索引標籤中指定的用戶端安裝內容便會發佈到 Active Directory 網域服務。 如需用戶端安裝內容的詳細資訊，請參閱 [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (關於 System Center Configuration Manager 中的用戶端安裝內容)。  

6.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

7.  在 [資產與相容性]  工作區中，選取一部或多部電腦，或選取電腦的集合。  

8.  在 [首頁]  索引標籤上，選擇下列其中一項：  

    -   如果要將用戶端安裝到單一電腦或多部電腦，請在 [裝置]  群組中，按一下 [安裝用戶端] 。  

    -   如果要將用戶端安裝到電腦的集合，請在 [集合]  群組中，按一下 [安裝用戶端] 。  

9. 在 [安裝用戶端精靈]  的 [開始之前] 頁面上檢閱資訊，然後按 [下一步] 。  

10. 在 [安裝選項]  頁面上，設定是否可以在網域控制站上安裝用戶端、是否要在具備現有用戶端的電腦上重新安裝、升級或修復，以及設定將會安裝用戶端軟體的網站名稱。 按一下 [下一步] 。  

11. 檢閱安裝設定，然後關閉精靈。  

> [!NOTE]  
>  如果網站未設定為進行用戶端推入，您可以使用精靈安裝用戶端。  

##  <a name="a-namebkmkclientsupa-how-to-install-clients-with-software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> 如何使用以軟體更新為基礎的安裝安裝用戶端  
 以軟體更新為基礎的用戶端安裝，會將 Configuration Manager 用戶端發佈到軟體更新點，以作為其他軟體更新。 此用戶端安裝方法可用來在尚未安裝用戶端的電腦上安裝 Configuration Manager 用戶端，或升級現有的 Configuration Manager 用戶端。  

 如果電腦已安裝 Configuration Manager 用戶端，Configuration Manager 會為用戶端提供可取得軟體更新的軟體更新點伺服器名稱。 此資訊會包含在用戶端原則中。  

> [!IMPORTANT]  
>  若要使用以軟體更新為基礎的安裝，您必須使用相同的 Windows Server Update Services (WSUS) 伺服器進行用戶端安裝和軟體更新。 此伺服器在主要網站必須是主動式軟體更新點。 如需詳細資訊，請參閱[安裝軟體更新點](../../../sum/get-started/install-a-software-update-point.md)。  

 如果電腦未安裝 Configuration Manager 用戶端，您必須在 Active Directory 網域服務中設定並指派群組原則物件 (GPO)，以指定電腦將從中取得軟體更新的軟體更新點伺服器名稱。  

 您無法新增命令列內容至以軟體更新為基礎的用戶端安裝。 如果您已延伸 Configuration Manager 的 Active Directory 架構，用戶端電腦會在安裝時自動查詢 Active Directory 網域服務，以取得安裝內容。  

 如果您未延伸 Active Directory 架構，便可以使用群組原則將用戶端安裝設定佈建到網站中的電腦。 這些設定會自動套用到任何以軟體更新為基礎的用戶端安裝。 如需詳細資訊，請參閱[如何佈建用戶端安裝內容 (群組原則和以軟體更新為基礎的用戶端安裝)](#BKMK_Provision) 和[如何將用戶端指派給 System Center Configuration Manager 中的站台](../../../core/clients/deploy/assign-clients-to-a-site.md)。  

 使用下列程序，將不含 Configuration Manager 用戶端的電腦設定為使用軟體更新點進行用戶端安裝和軟體更新，以及將 Configuration Manager 用戶端軟體發佈到軟體更新點。  

> [!NOTE]  
>  如果在軟體安裝後電腦處於暫止的重新啟動狀態，則以用戶端安裝為基礎的軟體更新可能會導致電腦重新啟動。  

在 Active Directory 網域服務中設定群組原則物件，以指定用戶端安裝和軟體更新的軟體更新點：  

1.  使用群組原則管理主控台來開啟新的或現有的群組原則物件。  

2.  在主控台中，依序展開 [電腦設定] 、[系統管理範本] 和 [Windows 元件] ，然後按一下 [Windows Update] 。  

3.  開啟 [指定近端內部網路 Microsoft 更新服務的位置] 設定的內容，然後按一下[已啟用] 。  

4.  在 [設定偵測更新的近端內部網路更新服務] 方塊中，指定您要使用的軟體更新點伺服器名稱和連接埠。 這些設定必須完全符合軟體更新點使用的伺服器名稱格式和連接埠：  

    -   如果 Configuration Manager 網站系統已設定為使用完整網域名稱 (FQDN)，請使用 FQDN 格式指定伺服器名稱。  

    -   如果 Configuration Manager 網站系統未設定為使用完整網域名稱 (FQDN)，請使用短名稱格式指定伺服器名稱。  

    > [!NOTE]  
    >  若要判斷軟體更新點使用的連接埠號碼，請參閱[如何判斷 WSUS 在 System Center Configuration Manager 中使用的連接埠設定](../../../sum/plan-design/plan-for-software-updates.md)。  

     範例： **http://server1.contoso.com:8530**  

5.  在 [設定近端內部網路統計伺服器] 方塊中，指定要使用的內部網路統計伺服器。 指定此伺服器沒有特定的需求。 此伺服器不一定是要與軟體更新點伺服器相同的電腦，而且如果是相同伺服器，也不一定要使用相符的格式。  

6.  將群組原則物件指派給您要安裝 Configuration Manager 用戶端及接收軟體更新的電腦。  

### <a name="to-publish-the-configuration-manager-client-to-the-software-update-point"></a>將 Configuration Manager 用戶端發佈到軟體更新點  

1.  在 Configuration Manager 主控台中，按一下 [系統管理]   

2.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [網站] 。  

3.  在 [網站]  清單中，選取您要為其設定以軟體更新為基礎之用戶端安裝的網站。  

4.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [用戶端安裝設定] 然後按一下 [以軟體更新為基礎的用戶端安裝] 。  

5.  在 [軟體更新點用戶端安裝內容]  對話方塊中，選取 [啟用以軟體更新為基礎的用戶端安裝]  以啟用此用戶端安裝方法。  

6.  如果 Configuration Manager 站台伺服器上的用戶端軟體的版本比軟體更新點上儲存的還要新，則會開啟 [偵測到較新版本的用戶端套件] 對話方塊。 按一下 [是]  將最新版本的用戶端軟體發佈到軟體更新點。  

    > [!NOTE]  
    >  如果用戶端軟體先前並未發佈到軟體更新點，此方塊將會空白。  

7.  若要完成設定軟體更新點用戶端安裝，請按一下 [確定] 。  

> [!NOTE]  
>  Configuration Manager 用戶端的軟體更新不會在有新版本時自動更新。 如果您升級網站 (其中包含新用戶端版本)，您必須重複此程序，並在步驟 6 按一下 [是]  。  

##  <a name="a-namebkmkclientgpa-how-to-install-clients-with-group-policy"></a><a name="BKMK_ClientGP"></a> 如何使用群組原則安裝用戶端  
 您可以使用 Active Directory 網域服務中的群組原則，發佈或指派 Configuration Manager 用戶端以安裝在您企業中的電腦上。 當您使用群組原則將 Configuration Manager 用戶端指派到電腦，用戶端會在電腦初次啟動時安裝。 當您使用群組原則向使用者發佈 Configuration Manager 用戶端時，用戶端會顯示在電腦 [控制台] 中的 [新增或移除程式]，讓使用者進行安裝。  

 將 Windows Installer 套件 (CCMSetup.msi) 用於以群組原則為基礎的安裝。 此檔案可在 Configuration Manager 站台伺服器的 **&lt;ConfigMgr 安裝目錄\>\bin\i386** 資料夾中找到。 您無法將內容新增至此檔案以修改安裝行為：  

> [!IMPORTANT]  
>  您必須擁有對資料夾的系統管理員權限，才能存取用戶端安裝檔案。  

-   如果 Active Directory 架構已針對 Configuration Manager 延伸，而且已選取 [站台內容] 對話方塊之 [進階] 標籤中的 [Publish this site in Active Directory Domain Services] (在 Active Directory 網域服務中發佈此站台)，則用戶端電腦會自動搜尋 Active Directory 網域服務的安裝內容。 如需已發佈安裝內容的詳細資訊，請參閱 [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md) (關於 System Center Configuration Manager 中發佈至 Active Directory 網域服務的用戶端安裝內容)。  

-   如果尚未延伸 Active Directory 架構，您可以使用本主題的以下程序，將安裝內容儲存在電腦的登錄中： [如何佈建用戶端安裝內容 (群組原則和以軟體更新為基礎的用戶端安裝)](#BKMK_Provision)。 然後，這些安裝內容會在安裝 Configuration Manager 用戶端時使用。  

 如需如何使用 Active Directory 網域服務中的群組原則安裝軟體的詳細資訊，請參閱您的 Windows Server 文件。  

##  <a name="a-namebkmkmanuala-how-to-install-clients-manually"></a><a name="BKMK_Manual"></a> 如何手動安裝用戶端  
 您可以使用 CCMSetup.exe 程式，在您企業中的電腦上手動安裝 Configuration Manager 用戶端軟體。 您可以在站台伺服器以及您站台之管理點上 Configuration Manager 安裝資料夾的 [用戶端] 資料夾中，找到此程式及其支援檔案。 這個資料夾會以  

 \\\\*&lt;站台伺服器名稱\><bpt id="p1">*</bpt>*\SMS_*&lt;站台碼\>*\Client\  

 其中 &lt;站台伺服器名稱\> 是其中一個裝載管理點的伺服器名稱，而 &lt;站台碼\> 是用戶端將隸屬的主要站台代碼。  若要從用戶端上的命令列執行 CCMSetup.exe，您必須將網路磁碟機對應到這個位置，然後執行命令。  

> [!IMPORTANT]  
>  您必須擁有對資料夾的系統管理員權限，才能存取用戶端安裝檔案。  

 CCMSetup.exe 會將所有必要的安裝條件複製到用戶端電腦，並且會呼叫 Windows Installer 套件 (Client.msi) 執行用戶端安裝。  

> [!IMPORTANT]  
>  您無法直接執行 Client.msi。  

 您可以指定 CCMSetup.exe 與 Client.msi 的命令列內容，以修改用戶端安裝的行為。 請務必先指定 CCMSetup 內容 (以 **/** 為開頭的內容)，再指定 Client.msi 內容。  

 例如，您可以指定下列命令：  

```  
CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01  
```  

 而用戶端安裝則藉由使用下列屬性來進行：  

|屬性|說明|  
|--------------|-----------------|  
|**/mp:SMSMP01**|此 CCMSetup 內容會指定管理點 SMSMP01 下載必要的安裝檔案。|  
|**/logon**|此 CCMSetup 內容會指定：當發現電腦上已有 Configuration Manager 用戶端時，應該停止安裝。|  
|**SMSSITECODE=AUTO**|此 Client.msi 內容會指定：用戶端會使用 Active Directory 網域服務，嘗試尋找要使用的 Configuration Manager 站台碼。|  
|**FSP=SMSFP01**|此 Client.msi 內容會指定：名為 SMSFP01 的後援狀態點，將會用於接收從用戶端電腦傳送的狀態訊息。|  

 如需所有 CCMSetup.exe 內容的詳細資訊，請參閱 [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (關於 Configuration Manager 中的用戶端安裝內容)  

### <a name="examples"></a>範例
 這些範例是針對內部網路上的 Active Directory 用戶端，並且使用下列值來代表站台的不同層面︰  

 **MPSERVER** = 裝載管理點的伺服器   
**FSPSERVER** = 裝載後援狀態點的伺服器  
**ABC** = 站台碼  
**contoso.com** = 網域名稱  

 所有站台系統伺服器皆以內部網路 FQDN 設定，而且站台會發佈至用戶端的 Active Directory 樹系中。  

 在用戶端電腦上，您需以本機系統管理員的身分登入，將磁碟機 (z:) 對應到\\\MPSERVER\SMS_ABC\Client，將命令提示字元切換到 z 磁碟機，然後執行下列其中一個命令。  

 **範例 1：**  

```  
CCMSetup.exe  
```  

> [!NOTE]  
>  此範例會安裝沒有其他內容的用戶端，如此用戶端便會利用發佈至 Active Directory 網域服務的用戶端安裝內容，進行自動設定。 例如，用戶端會針對站台碼 (需要在為用戶端指派而設定的界限群組中包含用戶端的網路位置)、管理點、後援狀態碼，以及用戶端是否只能透過 HTTPS 通訊等，進行自動設定。 如需可針對 Active Directory 用戶端自動設定的用戶端安裝內容詳細資訊，請參閱 [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md) (關於 System Center Configuration Manager 中發佈至 Active Directory 網域服務的用戶端安裝內容)。  

 **範例 2：**  

```  
CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com  
```  

> [!NOTE]  
>  此範例會覆寫 Active Directory 網域服務可提供的自動設定，不需要在為用戶端指派而設定的界限群組中包含用戶端的網路位置。 安裝程序會指定網站、內部網路管理點和以網際網路為基礎的管理點、接受來自網際網路連線的後援狀態點，並且使用具有最長有效期限的用戶端 PKI 憑證 (如果適用)。  

##  <a name="a-namebkmkclientlogonscripta-how-to-install-clients-with-logon-scripts"></a><a name="BKMK_ClientLogonScript"></a> 如何使用登入指令碼安裝用戶端  
 Configuration Manager 支援登入指令碼安裝 Configuration Manager 用戶端軟體。 您可以使用登入指令碼中的程式檔案 CCMSetup.exe  觸發用戶端安裝。  

 登入指令碼安裝所使用的方式，與手動用戶端安裝相同。 您可以指定 CCMSsetup.exe 的 /logon  安裝內容，如果電腦上已經有任何版本的用戶端，則此安裝內容會阻止用戶端安裝。 如此可預防每次執行登入指令碼時，重新安裝用戶端。  

 如果沒有使用 **/Source** 內容來指定安裝來源，而且沒有使用 **/MP** 內容來指定可從中取得安裝的管理點，只要已針對 Configuration Manager 延伸架構並將站台發佈到「Active Directory 網域服務」，CCMSetup.exe 便可透過搜尋「Active Directory 網域服務」來尋找管理點。 此外，用戶端可以使用 DNS 或 WINS 尋找管理點。  

##  <a name="a-namebkmkclientappa-how-to-install-clients-with-a-package-and-program"></a><a name="BKMK_ClientApp"></a> 如何使用套件及程式安裝用戶端  
 您可以使用 Configuration Manager 來建立和部署套件與程式，將您階層中所選電腦的用戶端軟體升級。 套件定義檔案會在套件內容填入一般常用值的 Configuration Manager 時一併提供。 您可以指定其他命令列內容，以自訂用戶端安裝行為。  

> [!NOTE]  
>  您無法使用這種方法升級 Configuration Manager 2007 用戶端。 請改用自動用戶端升級，這會自動建立並部署包含最新用戶端版本的套件。 如需詳細資訊，請參閱 [Upgrade clients in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) (在 System Center Configuration Manager 中升級用戶端)。  
>   
>  如需如何從舊版 Configuration Manager 用戶端移轉的詳細資訊，請參閱[規劃 System Center Configuration Manager 中的用戶端移轉策略](../../../core/migration/planning-a-client-migration-strategy.md)。  

 依照下列程序，建立可部署至 Configuration Manager 用戶端電腦的 Configuration Manager 套件和程式，以升級用戶端軟體。  

建立用戶端軟體的套件和程式  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [應用程式管理] ，然後按一下 [套件] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [從定義建立套件] 。  

4.  在 [從定義建立套件精靈]  的 [套件定義] 頁面上，從 [發行者]  下拉式清單選取 [Microsoft]  ，從 [套件定義]  清單選取 [Configuration Manager 用戶端升級]  ，然後按 [下一步] 。  

5.  在精靈的 [來源檔案]  頁面上，選取 [永遠從來源資料夾取得檔案] ，然後按 [下一步] 。  

6.  在 [從定義建立套件精靈] 的 [來源資料夾] 頁面上，選取 [網路路徑 (UNC 名稱)] 並輸入包含 Configuration Manager 用戶端安裝檔案的電腦與資料夾網路路徑。  

    > [!NOTE]  
    >  Configuration Manager 部署執行所在的電腦必須能夠存取您指定的網路資料夾。 如果電腦沒有存取權，則安裝程序將會失敗。  

7.  按 [下一步]  ，並且完成精靈。  

8.  如果想要變更任何用戶端安裝內容，您可以在 [Configuration Manager 代理程式無訊息升級內容]  程式對話方塊的 [一般]  索引標籤上，修改 CCMSetup.exe 命令列參數。 預設的安裝內容為 /noservice SMSSITECODE=AUTO 。  

9. 將套件發佈至所有您想要裝載用戶端升級套件的發佈點。 然後，您可以將套件部署到包含您要升級之 Configuration Manager 用戶端的電腦集合。  

## <a name="how-to-install-clients-to-mdm-managed-windows-devices-with-intune"></a>如何使用 Intune 將用戶端安裝至 MDM 管理的 Windows 裝置

您可以將 Configuration Manager 用戶端安裝檔案部署至使用 Microsoft Intune 註冊的電腦。 若要這樣做，您可以使用 Intune 軟體發佈者建立包含用戶端安裝檔案 **ccmsetup.msi** 的 Windows Installer (\*.msi) 應用程式。 然後，將應用程式部署到註冊的裝置上，如此即會安裝用戶端軟體。

為確保裝置在安裝用戶端軟體後維持在受管理的狀態，裝置必須在公司網路中及 Configuration Manager 站台界限內。 

> [!NOTE]
> 用戶端軟體安裝之後，裝置就會從 Intune 取消註冊。

### <a name="to-install-clients-with-intune"></a>使用 Intune 安裝用戶端：

1. 在 Intune 中，[建立應用程式](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune)包含 Configuration Manager 用戶端安裝檔案 **ccmsetup.msi**。

2. 在 Intune 軟體發佈者中使用下列命令列參數︰

  **CCMSETUPCMD="/MP:&lt;管理點的 FQDN> SMSMP=&lt;管理點的 FQDN> SMSSITECODE=&lt;您的站台碼> DNSSUFFIX=&lt;管理點的 DNS 尾碼>"**

3. [部署應用程式](/intune/deploy-use/deploy-apps-in-microsoft-intune)到已註冊的 Windows 電腦。

##  <a name="a-namebkmkclientimagea-how-to-install-clients-with-a-computer-image"></a><a name="BKMK_ClientImage"></a> 如何使用電腦映像安裝用戶端  
 您可以在用來在企業中建置電腦的主要映像電腦上，預先安裝 Configuration Manager 用戶端軟體。 若要在主要電腦上安裝用戶端，請不要為該用戶端指定網站碼。 電腦從此主要映像進行映像處理時，會包含 Configuration Manager 用戶端，且必須在安裝完成時完成站台指派。  

> [!IMPORTANT]  
>  將 Configuration Manager 用戶端指派給 Configuration Manager 站台 之後，映像的電腦才能作為 Configuration Manager 用戶端。  

 您必須移除在主要映像電腦上安裝的任何電腦特定憑證。 例如，如果您使用公開金鑰基礎結構 (PKI) 憑證，就必須針對 [電腦]  和 [使用者]  ，在映像處理電腦前移除 [個人]  存放區中的憑證。  

 如果用戶端無法查詢 Active Directory 網域服務以找出管理點，就會使用信任的根金鑰來判斷信任的管理點。 如果將所有經過映像處理的用戶端部署在相同的階層中做為主要電腦，則請保留信任的根金鑰不要移除。 如果將用戶端部署在不同的階層中，請移除信任的根金鑰，且做為最佳作法，請以新的受信任根金鑰預先佈建這些用戶端。 如需詳細資訊，請參閱  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

### <a name="to-prepare-the-client-computer-for-imaging"></a>準備進行映像處理的用戶端電腦  

1.  在主要映像電腦上手動安裝 Configuration Manager 用戶端軟體。 如需詳細資訊，請參閱 [如何手動安裝 Configuration Manager 用戶端](#BKMK_Manual)。  

    > [!IMPORTANT]  
    >  請不要在 CCMSetup.exe 命令列內容中指定用戶端的 Configuration Manager 站台碼。  

2.  在命令提示字元中輸入 **net stop ccmexec** ，以確保 **SMS Agent Host** 服務 (Ccmexec.exe) 不在母片映像的電腦上執行。  

3.  移除主要映像電腦上儲存於本機電腦存放區中的任何憑證。  

4.  如果用戶端將安裝在主要映像電腦以外的不同 Configuration Manager 階層中，請從主要映像電腦移除受信任的根金鑰。  

5.  使用映像軟體來擷取主要電腦的映像。  

6.  將映像部署到目的地電腦。  

##  <a name="a-namebkmkclientworkgroupa-how-to-install-clients-on-workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> 如何在工作群組電腦上安裝用戶端  
 Configuration Manager 支援工作群組中電腦的用戶端安裝。 使用 [如何手動安裝 Configuration Manager 用戶端](#BKMK_Manual)中指定的方法，在工作群組電腦上安裝用戶端。  

 若要在工作群組電腦上安裝 Configuration Manager 用戶端，必須滿足下列必要條件︰  

-   必須將用戶端手動安裝在每部工作群組電腦上。 安裝期間，已登入的使用者必須在工作群組電腦上具備本機系統管理權限。  

-   若要存取 Configuration Manager 站台伺服器網域的資源，必須針對該站台設定網路存取帳戶。 您可指定此帳戶做為軟體發佈元件內容。 如需詳細資訊，請參閱 [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md)。  

 支援工作群組電腦時有幾項限制：  

-   工作群組用戶端無法從 Active Directory 網域服務找到管理點，必須使用 DNS、WINS 或其他管理點。  

-   不支援全域漫遊，因為用戶端無法向 Active Directory 網域服務查詢網站資訊。  

-   Active Directory 探索方法無法探索工作群組中的電腦。  

-   您無法將軟體部署至工作群組電腦的使用者。  

-   您無法使用用戶端推入安裝方法，在工作群組電腦上安裝用戶端。  

-   工作群組用戶端無法使用 Kerberos 進行驗證，可能需要手動核准。  

-   工作群組用戶端無法設定為發佈點。 Configuration Manager 要求發佈點電腦為網域的成員。  

### <a name="to-install-the-client-on-workgroup-computers"></a>在工作群組電腦上安裝用戶端  

1.  確定您要安裝用戶端的電腦符合上述必要條件。  

2.  請遵循 [如何手動安裝 Configuration Manager 用戶端](#BKMK_Manual)一節中的指示。  

     範例 1： **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com**  

    > [!NOTE]  
    >  此範例是針對內部網路用戶端管理安裝用戶端，並指定網站碼和 DNS 尾碼來找出管理點。  

     範例 2： **CCMSetup.exe FSP=fspserver.constoso.com**  

    > [!NOTE]  
    >  此範例是要求用戶端位於界限群組中設定的網路位置，以便成功完成自動網站指派。 此命令包含伺服器 FSPSERVER 上的後援狀態點，以協助追蹤用戶端部署，並找出任何用戶端通訊問題。  

##  <a name="a-namebkmkclientinterneta-how-to-install-clients-for-internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> 如何安裝以網際網路為基礎的用戶端管理用戶端  
 對於有時位於內部網路、有時在網際網路上的用戶端，當 Configuration Manager 站台支援以網際網路為基礎的用戶端管理時，您在內部網路安裝用戶端時有兩個選項：  

-   安裝用戶端時，您可以包含 CCMHOSTNAME=&lt;以網際網路為基礎之管理點的網際網路 FQDN\> 的 Client.msi 內容，例如使用手動安裝或用戶端推入。 使用這種方法時，必須也直接將用戶端指派至網站，且無法使用自動網站指派。 此主題的 [如何手動安裝 Configuration Manager 用戶端](#BKMK_Manual) 一節提供此設定方法的範例。  

-   您可以針對內部網路用戶端管理安裝用戶端，然後將以網際網路為基礎的用戶端管理點指派到用戶端，方法是使用控制台中的 Configuration Manager 用戶端內容，或使用指令碼。 使用此方法時，您可以使用自動用戶端指派。 如需詳細資訊，請參閱此主題中的＜ [如何在安裝用戶端後，針對以網際網路為基礎的用戶端管理設定用戶端](#BKMK_ConfigureIBCM_MP) ＞一節。  

 如果您必須安裝位於網際網路的用戶端是因為用戶端為僅位於網際網路的用戶端，或是因為必須在用戶端回到內部網路前安裝，請從以下支援的方法中選擇一個：  

-   針對這些用戶端提供一個機制，暫時連線至內部網路，方法是使用虛擬私人網路 (VPN)，然後使用任何適當的用戶端安裝方法來安裝它們。  

-   使用獨立於 Configuration Manager 的安裝方法，例如將用戶端安裝來源檔封裝至您可以寄送給使用者的卸除式媒體，根據指示進行安裝。 用戶端安裝來源檔位於 Configuration Manager 站台伺服器和管理點的 &lt;安裝路徑\>\Client 資料夾中。 在媒體上納入指令碼，在用戶端資料夾上手動複製，並從此資料夾安裝用戶端，方法是使用 CCMSetup.exe 以及所有適當的 CCMSetup 命令行內容。  

> [!NOTE]  
>  Configuration Manager 不支援直接從以網際網路為基礎的管理點，或從以網際網路為基礎的軟體更新點來安裝用戶端。  

 因為透過網際網路管理的用戶端必須與以網際網路為基礎的網站系統進行通訊，請確保在安裝這些用戶端前，這些用戶端上也安裝了公開金鑰基礎結構 (PKI) 憑證。 您必須獨立於 Configuration Manager 來安裝這些憑證。 如需憑證需求的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

### <a name="to-install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>藉由指定 CCMSetup 命令行內容，在網際網路上安裝用戶端  

1.  請遵循 [如何手動安裝 Configuration Manager 用戶端](#BKMK_Manual) 一節中的指示，並且必須包含下列：  

    -   CCMSetup 命令行內容 **/source:**&lt;已複製之用戶端資料夾的本機路徑\>  

    -   CCMSetup 命令行內容 **/UsePKICert**  

    -   Client.msi 內容 **CCMHOSTNAME=**&lt;以網際網路為基礎的管理點 FQDN\>  

    -   Client.msi 內容 **SMSSIGNCERT=**&lt;已匯出之站台伺服器簽署憑證的本機路徑\>  

    -   Client.msi 內容 **SMSSITECODE=**&lt;以網際網路為基礎的管理點站台碼\>  

    > [!NOTE]  
    >  如果網站有一個以上以網際網路為基礎的管理點，您針對 CCMHOSTNAME 內容指定哪個以網際網路為基礎的管理點就不重要了。 Configuration Manager 用戶端連線至以網際網路為基礎的指定管理點時，管理點會向用戶端傳送網站中以網際網路為基礎的可用管理點清單，用戶端可從清單中選取一個管理點。 選取是以不確定的方式進行。  

2.  如果您不要讓用戶端檢查憑證撤銷清單 (CRL)，請將 CCMSetup 命令行內容指定為 **/NoCRLCheck**。  

3.  如果您使用的是以網際網路為基礎的後援狀態點，請將 Client.msi 內容指定為 **FSP=**&lt;以網際網路為基礎之後援狀態點的網際網路 FQDN\>。  

4.  如果您要針對僅在網際網路上執行的用戶端管理安裝用戶端，請將 Client.msi 內容指定為 **CCMALWAYSINF=1**。  

5.  驗證您是否要指定其他的 CCMSetup 命令行內容。 例如，如果用戶端有一個以上的有效 PKI 憑證，您就必須指定憑證選擇準則。 如需可用屬性的清單，請參閱 [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (關於 System Center Configuration Manager 中的用戶端安裝內容)。  

     範例： **CCMSetup.exe /source:D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1**  

    > [!NOTE]  
    >  此範例會從 D 磁碟上的資料夾安裝用戶端來源檔案，設定為使用用戶端 PKI 憑證，針對僅在網際網路上執行的用戶端管理選取有效期間最長的憑證，然後將用戶端指派為使用以網際網路為基礎的管理點 (稱為 SERVER1) 以及在 contoso.com 網域中以網際網路為基礎的後援狀態點，並將用戶端指派至 ABC 網站。  

###  <a name="a-namebkmkconfigureibcmmpato-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> 安裝用戶端後，設定以網際網路為基礎的用戶端管理用戶端  
 若要在安裝用戶端後指派以網際網路為基礎的管理點，請使用以下其中一種程序。 第一個程序要求進行手動安裝，因此這適合新的用戶端；若您有許多用戶端需要設定，則第二個程序更適合。  

#### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>指派 Configuration Manager 內容中以網際網路為基礎的管理點，在安裝用戶端後，針對以網際網路為基礎的用戶端管理設定用戶端  

1.  瀏覽至用戶端電腦控制台中的 [Configuration Manager]  ，然後連按兩下，開啟其內容。  

2.  在 [網際網路]  索引標籤的網際網路 FQDN 文字方塊中，輸入以網際網路為基礎的管理點的完整網域名稱。  

    > [!NOTE]  
    >  [網際網路]  索引標籤僅在用戶端具備用戶端 PKI 憑證時才能使用。  

3.  若用戶端會使用 Proxy 伺服器存取網際網路，請輸入 Proxy 伺服器設定。  

4.  按一下 [ **確定**]。  

#### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>使用指令碼安裝用戶端後，針對以網際網路為基礎的用戶端管理設定用戶端  

1.  開啟文字編輯器，例如 [記事本]。  

2.  複製下列內容並插入檔案中：  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the Internet-Based Management Point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

3.  以網際網路為基礎的管理點的網際網路 FQDN 取代 *mp.contoso.com* 。  

    > [!NOTE]  
    >  如果您必須刪除特定以網際網路為基礎的管理點，用戶端才不會設定為使用以網際網路為基礎的管理點，則請移除引號內的值，此時這一行會變成 **newInternetBasedManagementPointFQDN = ""**。  

4.  以副檔名 .vbs 儲存檔案。  

5.  使用以下其中一種方法，使用 cscript 在用戶端電腦上執行指令碼：  

    -   使用套件和程式，將檔案部署至現有 Configuration Manager 用戶端。  

    -   按兩下 Windows 檔案總管中的指令碼檔案，在現有的 Configuration Manager 用戶端上本機執行檔案。  

 您必須重新啟動用戶端，指令碼中的新設定才會生效。  

##  <a name="a-namebkmkprovisiona-how-to-provision-client-installation-properties-group-policy-and-software-update-based-client-installation"></a><a name="BKMK_Provision"></a> 如何佈建用戶端安裝內容 (群組原則和以軟體更新為基礎的用戶端安裝)  
 您可以使用 Windows 群組原則，以 Configuration Manager 用戶端安裝內容，在企業內佈建電腦。 這些內容都儲存在電腦的登錄中，安裝用戶端軟體時就會讀取。 Configuration Manager 一般不需要這個程序。 不過，部分用戶端安裝情況可能需要這個程序，例如以下狀況：  

-   您使用的是群組原則設定或以軟體更新為基礎的用戶端安裝方法，並且您未針對 Configuration Manager 延伸 Active Directory 架構。  

-   您想在特定電腦上覆寫用戶端安裝內容。  

> [!NOTE]  
>  如果 CCMSetup.exe 命令列上已提供任何安裝內容，就不會使用佈建在電腦上的安裝內容。  

 Configuration Manager 安裝媒體上提供了名為 ConfigMgrInstallation.adm 的群組原則系統管理範本，可透過安裝內容來佈建用戶端電腦。 利用下列程序，設定此範本並將其指派至組織內的電腦。  

### <a name="to-configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>使用群組原則物件設定與指派用戶端安裝內容  

1.  使用 Windows 群組原則物件編輯器將系統管理範本 ConfigMgrInstallation.adm 匯入至新增或現有的群組原則物件。  

    > [!NOTE]  
    >  您可以在 Configuration Manager 安裝媒體上的 **TOOLS\ConfigMgrADMTemplates** 資料夾內找到這個檔案。  

2.  開啟已匯入設定 [設定用戶端部署設定] 的屬性。  

3.  按一下 [已啟用] 。  

4.  在 [CCMSetup]  方塊中，輸入必要的 CCMSetup 命令列屬性。 如需所有 CCMSetup 命令行內容和其用法範例的清單，請參閱 [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (關於 System Center Configuration Manager 中的用戶端安裝內容)。  

5.  將群組原則物件指派給您要以 Configuration Manager 用戶端安裝內容來佈建的電腦。  

 如需 Windows 群組原則的資訊，請參考您的 Windows Server 說明文件。  



<!--HONumber=Dec16_HO3-->


