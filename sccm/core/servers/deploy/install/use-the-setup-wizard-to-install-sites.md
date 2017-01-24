---
title: "安裝精靈 | Microsoft Docs"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 28ce074469469b6a7c1c456da051b5f8dea43dbb

---
# <a name="use-the-setup-wizard-to-install-system-center-configuration-manager-sites"></a>使用 [安裝精靈] 安裝 System Center Configuration Manager 站台

*適用於：System Center Configuration Manager (最新分支)*


若要使用引導式使用者介面安裝新的 System Center Configuration Manager 站台，請使用 Configuration Manager 安裝精靈 (setup.exe)。 這個精靈支援安裝主要站台或管理中心網站。 您也可以使用精靈，[升級 Configuration Manager 的評估安裝](../../../../core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md)至完整授權安裝。  當您不想要使用這個精靈時，可以改成使用[安裝指令碼](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)，然後執行自動命令列安裝。

若要安裝次要站台，您必須從 Configuration Manager 主控台安裝站台。  次要站台不支援指令碼命令列安裝。

## <a name="a-namebkmkprimarya--install-a-central-administration-site-or-primary-site"></a><a name="bkmk_primary"></a>  安裝管理中心網站或主要站台
使用下列程序來安裝管理中心網站或主要站台，或將評估站台升級至完整授權 Configuration Manager 站台。   

開始站台安裝之前，請先熟悉下列各文中的詳細資料︰
 -  [準備安裝站台](../../../../core/servers/deploy/install/prepare-to-install-sites.md)
 -  [安裝站台的必要條件](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md)

如果您要將管理中心網站安裝為站台擴充案例的一部分，請先檢閱本主題的[擴充獨立主要站台](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)一節，再使用下列程序。

### <a name="a-namebkmkinstallpria---to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a>  安裝主要站台或管理中心網站

1.  在您要安裝站台的電腦上，執行 **&lt;InstallationMedia\>\SMSSETUP\BIN\X64\Setup.exe** 以啟動 [System Center Configuration Manager 安裝精靈]。  

    > [!NOTE]  
    >  如果您安裝管理中心網站以在獨立主要站台上進行擴充，或在現有階層中安裝新的子主要站台，則必須使用符合現有一或多個站台版本的安裝媒體 (原始程式檔)。  如果您所安裝的主控台內更新已變更先前安裝站台的版本，請不要使用原始安裝媒體，而是改成使用更新站台之 [CD.Latest 資料夾](../../../../core/servers/manage/the-cd.latest-folder.md)中的原始程式檔。  Configuration Manager 會要求您使用與新站台將連線之現有站台版本相符的來源檔案。  

2.  在 [ **開始之前** ] 頁面上，按 [ **下一步**]。  

3.  在 [開始使用] 頁面上，選取您要安裝的站台類型：  

     **管理中心網站** – 作為新階層的第一個站台，或擴充獨立主要站台時：  

    -   選取： **安裝 Configuration Manager 管理中心網站**  

         在此程序稍後的步驟中，我們將提供您安裝管理中心網站的選擇，以將其作為新階層的第一個站台，或安裝管理中心網站以擴充獨立主要站台。  

     **主要站台** – 作為新階層中第一個站台的獨立主要站台，或作為子主要站台：  

    -   選取： **安裝 Configuration Manager 主要站台**  

        > [!TIP]  
        >  當您想要在測試環境中安裝獨立主要站台時，通常只要選取選項 [為獨立主要站台使用一般安裝選項]  即可。 當您選取此選項時：  
        >   
        > -   安裝程式會自動將該站台設定為獨立主要站台  
        > -   使用預設安裝路徑  
        > -   為該站台資料庫使用 SQL Server 的預設執行個體本機安裝  
        > -   在站台伺服器電腦上安裝管理點與發佈點  
        > -   使用英文設定站台，且在主要站台伺服器上顯示作業系統的語言 (如果符合 Configuration Manager 支援的其中一個語言)  

4.  在 [產品金鑰] 頁面上：
    - 選擇是否將 Configuration Manager 安裝為評估版或授權版。  

      -   若選取授權版，請輸入產品金鑰，然後按一下 [下一步] 。  

      -   若選取評估版，請按一下 [下一步] 。 (您可於稍後將評估安裝升級為完整安裝。)  
    - 從 System Center Configuration Manager 的 1606 版 2016 年 10 月版基準媒體開始，您可以指定軟體保證合約的到期日。 在此頁面上，您可以選擇指定授權合約的「軟體保證到期日」，以方便提醒您該日期。 如果您未在安裝期間輸入這個項目，則稍後可以從 Configuration Manager 主控台予以指定。

      >  [!NOTE]   
      >  Microsoft 不會驗證您輸入的到期日，亦不會將這個日期用於授權驗證。  相反地，您可以將它作為到期日的提醒。 這項功能很實用，因為 Configuration Manager 會定期檢查線上提供的新軟體更新，因此您應該維持最新的軟體保證授權狀態，才能保有使用其他更新的資格。    

      如需詳細資訊，請參閱 [System Center Configuration Manager 的授權與分支](/sccm/core/understand/learn-more-editions)。

5.  在 [Microsoft 軟體授權條款]  頁面上，閱讀並接受授權條款。  

6.  在 [必要條件授權]  頁面上，閱讀並接受軟體必要條件的授權條款。  安裝程式會在需要時，於網站系統或用戶端上下載並自動安裝軟體。 您必須選取所有核取方塊，才能繼續進入下一頁。  

7.  在 [必要條件下載]  頁面上，指定安裝程式是否必須從網際網路下載最新版必要條件可轉散發檔案，或是使用先前下載的檔案：  

    -   若希望安裝程式此時下載這些檔案，請選取 [下載必要檔案]  ，並指定檔案的儲存位置。  

    -   如果您先前使用[安裝程式下載程式](../../../../core/servers/deploy/install/setup-downloader.md)下載檔案，請選取 [使用先前下載的檔案]，並指定下載資料夾。  

        > [!TIP]  
        >  若使用先前下載的檔案，請確認下載資料夾的路徑，內含最新版的檔案。  

8.  在 [伺服器語言選擇] 頁面上，選取可供 Configuration Manager 主控台和報告使用的語言。 (預設會選取英文，且無法移除。)  

9. 在 [用戶端語言選擇]  頁面上，選取可用於用戶端電腦的語言，指定是否為行動裝置用戶端啟用所有用戶端語言。 (預設會選取英文，且無法移除。)  

    > [!IMPORTANT]  
    > 當您使用管理中心網站時，請確定您在管理中心網站設定的用戶端語言包含您在每個子主要站台設定的所有用戶端語言。 原因是從發佈點安裝的用戶端可以從頂層站台存取用戶端語言，而從管理點安裝的用戶端可以從其指派的主要站台存取用戶端語言。  

10. 在 [站台和安裝設定]  頁面上，為目前所安裝的新站台，指定下列項目：  

    -   **站台碼：**[階層中的每個站台碼都不得重複](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_sitecodes)，且包含三個英數字元 (A 到 Z 以及 0 到 9)。 因為站台碼會用於資料夾名稱中，所以請勿為站台使用下列 Windows 保留名稱：    
        -   AUX  
        -   CON    
        -   NUL    
        -   PRN    
        -   SMS  

        > [!NOTE]  
        >  安裝程式不會驗證指定的站台碼是否已在使用中，或其是否為保留字。  

    -   **站台名稱：** 每個站台都需要此易記名稱，協助您識別站台。  

    -   **安裝資料夾**：此為 Configuration Manager 安裝的資料夾路徑。 安裝站台之後，即無法變更該位置，且路徑不可包含 Unicode 字元或結尾為空格。  

11. 在 [站台安裝]  頁面上，使用符合您案例的下列選項：  

    -   **我正在安裝管理中心網站：**  

         在 [管理中心網站安裝]  頁面上，選取 [安裝為新階層中的第一個站台] ，然後按 [下一步]  繼續。  

    -   **我正在將獨立主要站台擴充為擁有管理中心網站的階層：**  

         在 [管理中心網站安裝]  頁面上，選取 [將現有獨立主要站台擴充到階層中] ，指定獨立主要站台伺服器的 FQDN，然後按 [下一步]  繼續。  

         您用來安裝新管理中心網站的媒體必須符合主要站台的版本。  

    -   **我正在安裝獨立主要站台：**  

         在 [主要站台安裝]  頁面上，選取 [將主要站台安裝為獨立站台]，然後按 [下一步] 。  

    -   **我正在安裝子主要站台：**  

         在 [主要網站安裝]  頁面上選取 [將主要網站加入現有階層] ，指定管理中心網站的 FQDN，然後按 [下一步] 。  

12. 在 [資料庫資訊] 頁面上，指定下列資訊：  

    -   **SQL Server 名稱 (FQDN)：** 此設定預設會設定為該站台伺服器電腦。  

    -   **執行個體名稱：** 根據預設，若將此留白就會使用站台伺服器電腦 SQL 的預設執行個體。  

    -   **資料庫名稱：**根據預設，這設定為 CM_&lt;Sitecode\>。 可任意使用您指定的不同名稱。  

    -   **Service Broker 連接埠：** 此項目預設會設定為使用預設的 SQL Server Service Broker (SSB) 連接埠 4022，供 SQL 用於直接與其他站台的站台資料庫進行通訊。  

13. 在第二個 [資料庫資訊]  頁面上，可以指定 SQL Server 資料檔以及站台資料庫的 SQL Server 記錄檔的非預設位置：  

    -   將會提供 SQL Server 的預設檔案位置  

    -   當您使用 SQL Server 叢集時，無法使用指定非預設檔案位置的選項。  

    -   必要條件檢查程式不會對非預設的檔案位置執行可用磁碟空間檢查。  

14. 在 [SMS 提供者設定]  頁面上，為想要安裝 SMS 提供者的伺服器，指定 FQDN。  

    -   預設會指定站台伺服器。  

    -   安裝站台之後，可設定其他 SMS 提供者。  

15. 在 [用戶端通訊設定]  頁面上，選擇是否要將所有站台系統設定為僅接受來自於用戶端的 HTTPS 通訊，或為每個站台系統角色設定通訊方法。  

    -   選取 [所有站台系統角色僅接受來自用戶端的 HTTPS 通訊] 時，用戶端電腦必須具備有效的 PKI 憑證，才可進行用戶端驗證。 如需 PKI 憑證需求的詳細資訊，請參閱＜Configuration Manager 的 PKI 憑證需求＞。  

    > [!NOTE]  
    >  只有在您安裝主要站台時，才需進行此步驟。 若是安裝管理中心網站，請略過此步驟。  

16. 在 [網站系統角色]  頁面上，選擇是否要安裝管理點或發佈點。 為每個選擇要由安裝程式安裝的角色：  

    -   您必須為裝載角色的電腦輸入 **FQDN** ，然後選擇伺服器將會支援的用戶端連線方法 (HTTP 或 HTTPS)。  

    -   若在前一頁已選取 [所有站台系統角色僅接受來自用戶端的 HTTPS 通訊]  ，就會為 HTTPS 自動設定用戶端連線設定，且除非您回到先前的步驟變更設定，否則無法變更此項設定。  

    > [!NOTE]  
    >  只有在您安裝主要站台時，才需進行此步驟。 若是安裝管理中心網站，請略過此步驟。  

    > [!NOTE]  
    >  若要安裝站台系統角色，安裝程式會使用 **站台系統安裝帳戶**。 根據預設，這會使用主要站台的電腦帳戶。  此帳戶必須是遠端電腦上的本機系統管理員，才可安裝此站台系統角色。 如果此帳戶沒有必要的權限，則請取消核取站台系統角色，並稍後在設定其他帳戶用作站台系統安裝帳戶之後，從 Configuration Manager 主控台中進行安裝。  

17. 在 [使用方式資料]  頁面上，檢閱 Microsoft 收集之資料的相關資訊，然後按一下 [下一步] 。  

18. 在下列情況下，只有在安裝期間才能使用 [服務連接點設定] 頁面：  

    -   安裝獨立主要站台  

    -   安裝管理中心網站  

    > [!NOTE]  
    >  如果您要安裝子主要站台，請略過此步驟 (無法使用此頁面)。  

     如果您要將管理中心網站安裝為站台擴充案例的一部分，並且已在獨立主要站台安裝此角色，則必須從獨立主要站台解除安裝此角色。 此角色執行個體在階層中只能有一個，且只可位於該階層的頂層站台。  

     選取 [服務連接點] 的設定之後，按 [下一步]。 (安裝程式完成之後，可以從 Configuration Manager 主控台變更此設定)。  

19. 在 [設定摘要]  頁面上，檢閱您選取的設定，並於就緒時按一下 [下一步]  ，以啟動必要條件檢查程式。  

20. 在 [必要條件安裝檢查]  頁面上，將會列出可識別的所有問題。  

    -   若必要條件檢查工具找到問題，按一下清單中的項目即可查看有關如何解決問題的詳細資料。  

    -   您必須先解決每項狀態為 **失敗** 的問題，再繼續進行站台的安裝。 狀態為 **警告** 的項目應加以解決，但這些項目不會讓站台無法安裝。  

    -   解決問題之後，按一下 [執行檢查]  ，重新執行必要條件檢查程式。  

     執行必要條件檢查程式後，若沒有任何檢查收到 **失敗** 狀態時，可按一下 [開始安裝]  以啟動站台的安裝。  

    > [!TIP]  
    >  除了精靈中所提供的意見反應之外，檢視所安裝之電腦的系統磁碟機根目錄中的 **ConfigMgrPrereq.log** 檔案，也可看到必要條件問題的其他資訊。  如需安裝必要條件規則和描述的清單，請參閱 [System Center Configuration Manager 的必要條件檢查清單](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md)。  

21. 在 [安裝]  頁面上，安裝程式會顯示安裝狀態。 核心站台伺服器安裝完成時，可選擇是否要 **關閉** 安裝精靈。 當您關閉精靈時，安裝與初始站台組態會於背景繼續執行。  

    -   安裝程式完成之前，可以將 Configuration Manager 主控台連線至站台。 這個主控台會以唯讀方式連接，且可供您檢視物件與設定，但不可進行編輯。  

    -   安裝程式完成之後，將可連接能編輯物件與設定的主控台。  


## <a name="a-namebkmkexpanda-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> 擴充獨立主要站台
將獨立主要站台安裝為第一個站台時，之後可安裝管理中心網站，將該站台擴充到較大的階層。   

當您擴充獨立主要站台時，將會安裝新的管理中心網站，其使用現有獨立主要站台的資料庫作為參考。 安裝新的管理中心網站之後，獨立主要站台會作為子主要站台。


-   只有獨立主要站台才可擴充到新的階層。  

-   只有獨立主要站台才可擴充到特定的階層中。 您無法使用此選項將其他獨立主要站台加入相同的階層中。 而是應使用 [移轉]，將資料從一個階層移轉至另一個階層。  

-   將獨立站台擴充到管理中心網站的階層中之後，即可新增其他子主要站台。  

-   若要利用管理中心網站從階層中移除主要站台，您必須解除安裝主要站台。  

若要展開該站台，請使用 [System Center Configuration Manager 安裝精靈] 安裝新的管理中心網站，但請注意下列事項：  

-   安裝管理中心網站時所使用的 Configuration Manager 版本，必須要與獨立主要站台相同。  

-   在安裝精靈的 [開始使用] 頁面上，選取要安裝管理中心網站的選項。 在安裝程式稍後的階段中，將要選擇擴充現有獨立主要站台的選項。  

-   當您為新的管理中心網站設定 [用戶端語言選擇] 頁面時，所選取的用戶端語言必須與為擴充之獨立主要站台所設定的用戶端語言相同。  

-   在 [站台安裝] 頁面上，選取擴充獨立主要站台的選項。  

若要擴充獨立主要站台，請使用本文前面的*[安裝主要站台或管理中心網站](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_installpri)*程序。


## <a name="a-namebkmksecondarya-install-a-secondary-site"></a><a name="bkmk_secondary"></a> 安裝次要站台
 您可以使用 Configuration Manager 主控台來安裝次要站台。  

-   若您使用的主控台未連接至新的次要站之父站台的主要站台，則安裝該站台的命令會複寫至正確的主要站台。  

-   開始安裝站台之前，請確定您的使用者帳戶具有必要的權限，且將要裝載新的次要站台之電腦，符合所有必要條件，才可作為次要站台伺服器使用。  

-   安裝次要站台時，Configuration Manager 會將新的站台設定為使用在父主要站台所設定的用戶端通訊連接埠。  

### <a name="a-namebkmkinstallsecondarya-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a> 安裝次要站台  


1.  在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [站台設定] > [站台]，選取將成為新次要站台之父主要站台的站台。  

2.  按一下 [建立次要站台]  以啟動 [建立次要站台精靈] 。  

3.  在 [開始之前]  頁面上，確認列出的主要站台是您要使其成為新次要站台之父站台的站台，然後按一下 [下一步] 。  

4.  在 [一般]  頁面上，指定下列項目：  

    -   **站台碼：**階層中的每個站台碼都不得重複，且包含三個英數字元 (A 到 Z 以及 0 到 9)。 因為站台碼會用於資料夾名稱中，所以請勿為站台使用 Windows 的保留字：  

        -   AUX    
        -   CON    
        -   NUL    
        -   PRN  
        -   SMS  

       > [!NOTE]  
       >  安裝程式不會驗證指定的站台碼是否已在使用中，或其是否為保留字。  

    -   **站台伺服器名稱**：此為安裝新次要站台之伺服器的 FQDN。  

    -   **站台名稱**：每個站台都需要此易記名稱，協助您識別站台。  

    -   **安裝資料夾**：此為 Configuration Manager 安裝的資料夾路徑。 安裝站台之後，即無法變更該位置，且路徑不可包含 Unicode 字元或結尾為空格。  

    > [!IMPORTANT]  
    >  在此頁面指定詳細資料之後，可以按一下 [摘要]  ，為其餘的次要站台選項使用預設值，並直接前往精靈的 [摘要]  頁面。  
    >   
    >  -   當您熟悉此精靈中的預設值，而且這些預設值是您想要使用的設定時，才使用此選項。  
    >  -   使用預設設定時，界限群組不會與發佈點產生關聯。 因此，在您設定包含次要站台伺服器的界限群組之前，用戶端不會使用安裝在此次要站台作為內容來源位置的發佈點。  

5.  在 [安裝來源檔]  頁面上，選擇次要站台電腦要如何取得原始程式檔以安裝該站台。  

     當您使用儲存在網路上或儲存在次要站台電腦上的原始程式檔：  

    -   原始程式檔位置必須包含名稱為 **Redist** 的資料夾，包括所有先前使用安裝程式下載程式所下載的檔案。  

    -   如果任何來自 **Redist** 的檔案都無法使用，安裝程式將無法安裝次要站台。  

    -   次要站台電腦的電腦帳戶，必須要有原始程式檔資料夾與共用的 **讀取** 權限。  

6.  在 [SQL Server 設定]  頁面上，指定要使用的 SQL Server 版本，然後設定相關的設定。  

    > [!NOTE]  
    >  安裝開始前，安裝程式不會驗證您在此頁輸入的資訊。 在繼續之前，請確認這些設定。  

     **在次要站台電腦上安裝和設定 SQL Express 的本機複本**  

    -   **SQL Server 服務連接埠**：指定 SQL Server Express 要使用的 SQL Server 服務連接埠。 服務連接埠一般會設定為使用 TCP 連接埠 1433，不過您可以設定另一個連接埠。  

    -   **SQL Server Broker 連接埠**：指定 SQL Server Express 要使用的 SQL Server Service Broker (SSB) 連接埠。 Service Broker 一般會設定為使用 TCP 連接埠 4022，不過您可以設定不同的連接埠。 您必須指定沒有其他網站或服務在使用，且不會因防火牆限制而被封鎖的有效連接埠。  

    > [!IMPORTANT]  
    >  當 Configuration Manager 安裝 SQL Server Express 時，它會安裝不含 Service Pack 的 SQL Server Express 2012：  
    >   
    >  -   針對要支援的次要站台，在安裝之後，您必須安裝 Service Pack 2 (或更新版本) 來升級 SQL Server Express 2012。
    >  -   除此之外，如果新的次要站台安裝無法完成，但先完成了 SQL Server Express 2012 的安裝，則必須先更新 SQL Server Express 的執行個體，Configuration Manager 才可順利重試次要站台的安裝。  

     **使用現有 SQL Server 執行個體**  

    -   **SQL Server FQDN**：檢閱 SQL Server 電腦的 FQDN。 您必須使用本機 SQL Server 來裝載次要網站資料庫，且不能修改這個設定。  

    -   **SQL Server 執行個體**：指定作為次要站台資料庫使用的 SQL Server 之執行個體。 讓此選項保持空白，以使用預設執行個體。  

    -   **Configuration Manager 站台資料庫名稱**：指定用於次要站台資料庫的名稱。  

    -   **SQL Server Broker 連接埠**：指定 SQL Server 要使用的SQL Server Service Broker (SSB) 連接埠。 您必須指定沒有其他網站或服務在使用，且不會因防火牆限制而被封鎖的有效連接埠。  

    > [!TIP]  
    >  如需 System Center Configuration Manager 所支援的 SQL Server 版本清單，請參閱 [SQL Server 版本支援](../../../../core/plan-design/configs/support-for-sql-server-versions.md)。  

7.  在 [發佈點]  頁面上，為將會安裝在次要站台伺服器的發佈點進行設定。  

     **必要設定：**  

    -   **指定用戶端裝置與發佈點的通訊方法** – 選擇 HTTP 與 HTTPS。  

    -   **建立自我簽署憑證或匯入 PKI 用戶端憑證** – 選擇使用自我簽署憑證 (讓您也可允許從 Configuration Manager 用戶端非同步連接到內容庫)，或從您的 PKI 匯入憑證。  

         憑證可用於在發佈點傳送狀態訊息之前，對管理點驗證發佈點。  

         如需憑證需求的資訊，請參閱＜Configuration Manager 的 PKI 憑證需求＞。  

    **選擇性設定：**  

    -   **如果 Configuration Manager 需要，安裝及設定 IIS** - 如果伺服器尚未安裝 Internet Information Services (IIS)，則選取此設定可讓 Configuration Manager 能在伺服器上將其安裝及設定。 必須在所有發佈點上安裝 IIS。  

        > [!NOTE]  
        >  雖然這項設定是選擇性的，但 IIS 必須安裝在伺服器上，才可順利安裝發佈點。  

    -   **為此發佈點啟用及設定 BranchCache** •  

    -   **描述** – 這是發佈點的易記描述，可協助您加以辨識。  

    -   **啟用此發佈點供預先設置的內容使用**  

8.  在 [磁碟機設定]  頁面上，為次要站台發佈點指定磁碟機設定。  

     雖然 Configuration Manager 可以在前兩部磁碟機達到所設的磁碟機保留空間值時，使用其他磁碟機，但您最多只能為內容庫設定兩部磁碟機，以及為套件共用設定兩部磁碟機。 [磁碟機設定]  頁面會設定磁碟機的優先順序，以及每個磁碟機上能保留的可用磁碟空間量。  

    -   **磁碟機空間保留 (MB)**：您為此設定所設的值，可在 Configuration Manager 選擇不同磁碟機並繼續對該磁碟進行複製程序前，判斷磁碟機上的可用空間數量。 內容檔案可以跨越多個磁碟機。  

    -   **內容位置**：指定內容庫和封裝共用的內容位置。 Configuration Manager 會將內容複製到主要內容位置，直到可用空間量達到 [磁碟機空間保留 (MB)] 指定的值為止。 根據預設，內容位置會設定至 [自動] ，主要內容位置則會設定為安裝時有最多可用磁碟空間的磁碟機，以及指派磁碟機有次多可用磁碟空間的次要位置。 當主要和次要磁碟機都達到磁碟機空間保留的設定時，Configuration Manager 會選取其他具備最多可用磁碟空間的磁碟機，然後繼續進行複製程序。  

9. 在 [內容驗證]  頁面上，指定是否驗證發佈點上內容檔的完整性。  

    -   當您依照排程啟用內容驗證時，Configuration Manager 會於排程的時間起始程序，並驗證發佈點上的所有內容。  

    -   您也可以設定 **內容驗證優先順序**。  

    -   若要檢視內容驗證程序的結果，請在 Configuration Manager 主控台中瀏覽至 [監視] >  [發佈狀態] >  [內容狀態]。 每個套件類型的內容 (例如，應用程式、軟體更新套件和開機映像) 都會顯示。  

10. 在 [界限群組]  頁面上，管理指派了此發佈點的界限群組：  

    -   部署內容期間，用戶端必須存在於與發佈點關聯的界限群組之中，才能將界限群組當成內容的來源位置使用。  

    -   您可以選取 [允許內容的後援來源位置]  選項，讓這些界限群組外的用戶端在沒有可用的慣用發佈點時，退回並使用發佈點作為內容來源位置。  

     如需慣用發佈點的相關資訊，請參閱[內容管理的基本概念](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)主題。  

11. 在 [摘要]  頁面上驗證設定，然後按 [下一步]  安裝次要網站。 當精靈出現 [完成]  頁面時，即可關閉精靈。 次要站台安裝會繼續於背景執行。  


### <a name="a-namebkmkverifya-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a> 驗證次要站台安裝狀態  

1.  在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [站台設定] > [站台]。  

2.  選取您要安裝的次要站台伺服器，然後再按一下 [顯示安裝狀態] 。  

    > [!TIP]  
    >  一次安裝多個次要網站時，必要條件檢查一次只能檢查一個網站，且必須在開始檢查下一個網站前，完成前一個網站的檢查。  



<!--HONumber=Dec16_HO3-->


