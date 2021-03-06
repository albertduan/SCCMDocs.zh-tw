---
title: "封裝和程式"
titleSuffix: Configuration Manager
description: "支援使用套件和程式或應用程式搭配 System Center Configuration Manager 的部署。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
caps.latest.revision: "8"
caps.handback.revision: "0"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 7712721167edad5808c46827f68fc32a2b890bfd
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2017
---
# <a name="packages-and-programs-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的封裝和程式

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 會繼續支援 Configuration Manager 2007 中使用的套件和程式。 在您部署以下項目時，使用封裝和程式的部署可能會比使用應用程式的部署適合：  

- Linux 和 UNIX 伺服器應用
- 並未在電腦上安裝應用程式的程式碼，如重組電腦磁碟機的程式碼。
- 不需要持續監視的「一次性」指令碼  
- 依週期性排程執行且無法使用全域評估的指令碼

當您移轉舊版 Configuration Manager 的套件時，您可以將它們部署在 Configuration Manager 階層中。 移轉完成之後，封裝會出現在 [軟體程式庫]  工作區的 [封裝]  節點中。

修改和部署這些套件的方式，與使用軟體發佈相同。 [從定義匯入套件精靈] 會保留在 Configuration Manager 中，以匯入舊版套件。 從 Configuration Manager 2007 移轉至 Configuration Manager 階層時，公告會轉換成部署。  

> [!NOTE]  
>  您可以使用 Microsoft System Center Configuration Manager Package Conversion Manager，將套件和程式轉換成 Configuration Manager 應用程式。  
>   
>  如需詳細資訊，請參閱 [Configuration Manager Package Conversion Manager](https://technet.microsoft.com/library/hh531519.aspx)。  

套件可以使用 Configuration Manager 的一些新功能 (包括發佈點群組和監視)。 Microsoft Application Virtualization (App-V) 應用程式無法使用 Configuration Manager 中的套件和程式進行發佈。 若要發佈虛擬應用程式，您必須將它們建立為 Configuration Manager 應用程式。  

##  <a name="create-a-package-and-program"></a>建立套件和程式  
 使用下列其中一個程序，協助您建立或匯入套件和程式。  

### <a name="create-a-package-and-program-using-the-create-package-and-program-wizard"></a>使用建立封裝和程式精靈建立封裝和程式  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [套件]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立套件]。  

4.  在 **封裝** 頁面 **建立套件和程式精靈**, ，指定下列資訊：  

    -   **名稱**：指定套件的名稱，不可超過 50 個字元。  

    -   **描述**：指定這個套件的描述，不可超過 128 個字元。  

    -   **製造商**：(選擇性) 指定製造商名稱，以協助您在 Configuration Manager 主控台中識別套件。 這個名稱不可超過 32 個字元。

    -   **語言**：(選擇性) 指定套件的語言版本，不可超過 32 個字元。  

    -   **版本**：(選擇性) 指定套件的版本號碼，不可超過 32 個字元。

    -   **此套件包含來源檔案**：這個設定指出套件是否需要來源檔案存在於用戶端裝置上。 根據預設，會清除此核取方塊且 Configuration Manager 不會使用套件的發佈點。 選取這個核取方塊時，會使用發佈點。  

    -   **來源資料夾**：如果套件包含來源檔案，請選擇 [瀏覽] 以開啟 [設定來源資料夾] 對話方塊，然後指定套件的來源檔案位置。  

        > [!NOTE]  
        >  站台伺服器的電腦帳戶必須具有所指定來源資料夾的讀取權。  

5.  在 [建立套件和程式精靈] 的 [程式類型] 頁面上，選取要建立的程式類型，然後選擇 [下一步]。 您可以建立電腦或裝置的程式，也可以略過這個步驟，稍後再建立程式。  

    > [!TIP]  
    >  若要為現有的套件建立新程式，請先選取套件。 然後，在 [首頁] 索引標籤的 [套件] 群組中，選擇 [建立程式] 開啟 [建立程式精靈]。  

6.  使用下列其中一個程序建立標準程式或裝置程式。  

    #### <a name="create-a-standard-program"></a>建立標準程式  

  1.  在 [建立套件和程式精靈] 的 [程式類型] 頁面上，選擇 [標準程式]，然後選擇 [下一步]。     

    2.  在 [標準程式] 頁面上，指定下列資訊：  

        -   **名稱：** 指定程式名稱最多 50 個字元。  

            > [!NOTE]  
            >  程式名稱必須是唯一在封裝內。 建立程式之後，您無法修改它的名稱。  

        -   **命令列**：輸入用來啟動這個程式的命令列，或選擇 [瀏覽] 瀏覽至檔案位置。  

            如果檔案名稱沒有指定的副檔名，則 Configuration Manager 會嘗試使用 .com、.exe 和 .bat 作為可能的副檔名。  

             在用戶端上執行程式時，Configuration Manager 會依序在套件內、本機 Windows 資料夾中和本機 %路徑% 中搜尋命令列檔案名稱。 如果找不到檔案，程式就會失敗。  

        -   **啟動資料夾**(選擇性)：指定要在其中執行程式的資料夾，不可超過 127 個字元。 此資料夾可以是用戶端上的絕對路徑，或是含有套件之發佈點資料夾的相對路徑。

        -   **執行**：指定程式將在用戶端電腦上執行的模式。 選取下列其中一項：  

            -   **標準**：系統與程式的預設值為基礎的標準模式中執行的程式。 此為預設模式。  

            -   **最小化**：程式會在用戶端裝置上執行最小化。 使用者可能會在工作列通知區域中看到安裝活動。  

            -   **最大化**：程式會在用戶端裝置上執行最大化。 使用者會看到所有的安裝活動。  

            -   **隱藏**：在用戶端裝置上隱藏程式的執行。 使用者不會看到任何安裝活動。  

        -   **程式可執行**：指定只有使用者登入時才能執行程式、只有無使用者登入時才能執行程式，還是不論使用者是否登入用戶端電腦都執行程式。  

        -   **執行模式**：指定以系統管理權限還是以目前登入的使用者權限執行程式。  

        -   **允許使用者檢視程式安裝並與其互動**：使用這個設定 (如果可用的話)，指定是否允許使用者與程式安裝互動。 只有在針對 [程式可執行] 選取 [只有在沒有使用者登入時] 或 [無論使用者是否登入] 以及針對 [執行模式] 選取 [以系統管理權限執行] 時，才能使用這個核取方塊。  

        -   **磁碟機模式**：指定如何在網路上執行這個程式的相關資訊。 選擇下列其中一項：  

            -   **以 UNC 名稱執行**：指定以通用命名慣例 (UNC) 名稱執行程式。 這是預設設定。  

            -   **需要磁碟機代號**：指定程式需要完整限定其位置的磁碟機代號。 針對此設定，Configuration Manager 可以在用戶端上使用任何可用的磁碟機代號。  

            -   **需要特定磁碟機代號**：指定程式要求您指定完整限定其位置的特定磁碟機代號 (例如 **Z:**)。 如果用戶端上已使用指定的磁碟機代號並不會執行程式。  

        -   **重新連線到在記錄檔的發佈點上**：使用此核取方塊來指出在使用者登入時用戶端電腦是否重新連線到發佈點。 根據預設，會清除此核取方塊。  

  3.  在 [建立套件和程式精靈] 的 [需求] 頁面上，指定下列資訊：  

        -   **先執行其他程式**：使用此設定來識別在執行此套件及程式之前要執行的套件及程式。  

        -   **平台需求**：選取 [此程式可以在任何平台上執行] 或 [此程式僅能在指定的平台上執行]，然後選擇用戶端必須執行才能安裝套件和程式的作業系統。  

        -   **預估的磁碟空間**：指定軟體程式在電腦上執行所需的磁碟空間量。 這可以指定為 **未知** (預設值) 或大於或等於零的整數。 如果指定值，則也必須指定值的單位。  

        -   **允許的執行時間上限 (分鐘)**：指定程式預期在用戶端電腦上執行的時間上限。 這可以指定為 **未知** (預設值) 或大於零的整數數字。  

             根據預設，此值設為 120 分鐘。  

            > [!IMPORTANT]  
            >  如果使用維護期間作為此程式執行的集合，則若 [允許的執行時間上限] 比排程的維護期間長，便會發生衝突。 不過，如果執行時間上限設為 [未知]，則程式會在維護期間開始執行，並視需要在維護期間結束之後繼續執行。 如果使用者將執行時間上限設定為超過任何可用維護期間長度的特定期間，則不執行程式。  

             如果此值設定為 [未知]，則 Configuration Manager 會將允許的執行時間上限設定為 12 小時 (720 分鐘)。  

            > [!NOTE]  
            >  如果超過執行時間上限 (由使用者設定或設定為預設值)，Configuration Manager 會在選取 [以系統管理權限執行] 且未選取 [允許使用者檢視程式安裝並與其互動] 時停止程式。  

  4.  選擇 [下一步]。  

    #### <a name="create-a-device-program"></a>建立裝置程式  

  1.  在 [建立套件和程式精靈] 的 [程式類型] 頁面上，選取 [適用於裝置的程式]，然後按一下 [下一步]。  

  2.  在 [適用於裝置的程式] 頁面上，指定下列資訊：  

        -   **名稱**：指定程式的名稱，不可超過 50 個字元。  

            > [!NOTE]  
            >  程式名稱必須是唯一在封裝內。 建立程式之後，您無法修改它的名稱。  

        -   **註解**(選擇性)：指定這個裝置程式的註解，不可超過 127 個字元。  

        -   **下載資料夾**：指定 Windows CE 裝置上要儲存套件來源檔案的資料夾名稱。 預設值為 **\Temp\\\**。  

        -   **命令列**：輸入用來啟動這個程式的命令列，或選擇 [瀏覽] 瀏覽至檔案位置。  

        -   **在下載資料夾中執行命令列**：選取這個選項，從先前指定的下載資料夾中執行程式。  

        -   **從此資料夾執行命令列**：選取這個選項，指定從中執行程式的不同資料夾。  

    3.  在 [需求] 頁面中，指定下列資訊：  

        -   **預估的磁碟空間**：指定軟體所需的磁碟空間量。 這會先顯示給行動裝置的使用者，使用者才可安裝程式。  

        -   **下載程式**：指定可以將這個程式下載至行動裝置時的相關資訊。 您可以指定 [盡快] 、[僅透過高速網路] 或 [僅當裝置銜接底座時] 。  

        -   **其他需求**：指定這個程式的任何其他需求。 這些會先顯示給使用者，使用者才可安裝軟體。 例如，您可以通知它們之前需要關閉所有其他應用程式執行程式的使用者。  

  4.  選擇 [下一步]。  

  7.  在 [摘要] 頁面上，檢閱將採取的動作，然後完成精靈。  

 確認新的套件和程式顯示在 [軟體程式庫] 工作區的 [套件] 節點中。  

## <a name="create-a-package-and-program-from-a-package-definition-file"></a>從封裝定義檔中建立封裝和程式  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [套件]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [從定義建立套件]。  

4.  在 [從定義建立套件精靈] 的 [套件定義] 頁面上，選擇現有的套件定義檔，或選擇 [瀏覽] 開啟新的套件定義檔。 指定新的套件定義檔之後，請從 [套件定義] 清單中選取它，然後選擇 [下一步]。  

5.  在 [來源檔案] 頁面上，指定套件和程式之任何必要來源檔案的相關資訊，然後選擇 [下一步]。  

6.  如果套件需要來源檔案，請在 [來源資料夾] 頁面上指定要從中取得來源檔案的位置，然後選擇 [下一步]。  

7.  在 [摘要] 頁面上，檢閱將採取的動作，然後完成精靈。 新的套件和程式會顯示在 [軟體程式庫] 工作區的 [套件] 節點中。  

 如需套件定義檔的詳細資訊，請參閱本主題的[關於套件定義檔的格式](/sccm/apps/deploy-use/packages-and-programs#about-the-package-definition-file-format)。  

##  <a name="deploy-packages-and-programs"></a>部署套件和程式  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [套件]。  

2.  選取您想要部署的套件，然後在 [首頁] 索引標籤的 [部署] 群組中，選擇 [部署]。  

3.  在 [部署軟體精靈] 的 [一般] 頁面上，指定您想要部署的套件和程式名稱、您想要部署套件和程式的集合，以及部署的選擇性註解。  

     選取 **使用此集合相關聯的預設發佈點群組** 如果您想要將封裝內容儲存在集合預設發佈點群組。 如果您未建立所選取集合與發佈點群組的關聯，就無法使用此選項。  

4.  在 [內容] 頁面選擇 [新增]，然後選取要部署與此套件及程式相關聯之內容的發佈點或發佈點群組。  

5.  在 [部署設定] 頁面上，選擇此部署的用途，再指定喚醒封包的選項與付費連線︰  

    -   **用途**：您可以選擇：  

        -   **可用**：如果應用程式部署至使用者，使用者即可看見應用程式目錄中的已發佈套件和程式，且可以依需要求它。 如果套件和程式部署至裝置，使用者會在軟體中心內看到它，並可以隨選安裝它。  

        -   **必要**：根據設定的排程，自動部署套件和程式。 不過，使用者可以追蹤的套件和程式的部署狀態並將它安裝在期限之前使用軟體中心。  

    -   **傳送喚醒封包**：若部署目的設定為 [必要] ，且選取此選項，則會在安裝部署前將喚醒封包傳送到電腦上，以便在到達安裝期限時將電腦從睡眠狀態喚醒。 您可以使用此選項之前，必須設定電腦的網路喚醒。  

    -  **允許計量付費網際網路連線上的用戶端在安裝期限之後下載內容 (可能會產生額外費用)**：如有必要請選取此選項。  

    > [!NOTE]  
    >  當您部署套件及程式時，無法使用 **[將軟體預先部署至使用者的主要裝置]** 選項。  

6.  在 [排程] 頁面上，設定此套件和程式的部署時間，或可供用戶端裝置使用的時間。  

     這個頁面上的選項會因部署動作設定為 [可用] 或 [必要] 而有所不同。  

7.  如果部署目的設定為 [必要]，請從 [重新執行行為] 下拉式功能表中設定程式的重新執行行為。 選擇下列選項：  

    |重新執行行為|詳細資訊|  
    |--------------------|----------------------|  
    |永遠不會重新執行已部署的程式|程式不會在用戶端上重新執行，即使程式原本失敗或程式檔案變更也是一樣。|  
    |永遠重新執行程式|排程部署時，會一律在用戶端上重新執行程式，即使已經成功執行該程式。 這項功能在使用中的程式會更新，例如防毒軟體的週期性部署時很有用的。|  
    |如果先前嘗試失敗的重新執行|程式只有在前次嘗試執行失敗後，才會在排程部署時重新執行。|  
    |如果在先前的嘗試成功重新執行|程式只有過去曾在用戶端上成功執行後，才會重新執行。 在您使用可定期更新程式的週期性公告時，這十分有用，而且每次更新都需要成功安裝先前的更新。|  

8. 在 [使用者經驗]  頁面上，指定下列資訊：  

    -   **允許使用者不論指派均執行程式**：啟用時，使用者可以從 [軟體中心] 中安裝這個軟體，而不論任何排程的安裝時間。  

    -   **軟體安裝**：允許在任何已設定的維護期間以外的時間安裝軟體。  

    -   **系統重新啟動 (如果是完成安裝所需)**：如果軟體安裝需要重新啟動裝置才能完成，允許在任何已設定的維護期間以外的時間進行這個作業。  

    -   **Embedded 裝置**：當您將套件和程式部署到已啟用寫入篩選器的 Windows Embedded 裝置時，您可以指定在暫時重疊上安裝套件和程式，並於稍後再認可變更。 或者，在安裝期限或維護期間認可變更。 當您在安裝期限或維護期間認可變更時，需要重新啟動裝置才能保存裝置的變更。  

        > [!NOTE]  
        >  當您部署的封裝或程式到 Windows Embedded 裝置時，請確定裝置已設定的維護視窗集合的成員。 如需如何利用維護時段，將應用程式部署至 Windows Embedded 裝置的詳細資訊，請參閱[建立 Windows Embedded 應用程式](../../apps/get-started/creating-windows-embedded-applications.md)。  

9. 在 [發佈點]  頁面上，指定下列資訊：  

    -   **部署選項**：指定用戶端在執行程式內容時應該採取的動作。 您可以在用戶端位於快速網路界限或低速或不可靠的網路界限時指定行為。  

    -   **允許用戶端與同一個子網路上其他用戶端共用內容**：選取此選項可允許用戶端從已經下載並快取內容之網路上的其他用戶端來下載內容，以減少網路上的負載。 這個選項會利用 Windows BranchCache 並可以在執行 Windows Vista SP2 電腦上使用及更新版本。  

    -   **允許用戶端使用內容的後援來源位置**：  

        -  **1610 前的版本**：您可以選取 [允許內容的後援來源位置] 核取方塊，讓位於這些界限群組以外的用戶端回復，並在沒有其他發佈點可用時，將發佈點當成內容的來源位置使用。

        - **從 1610 版開始**：您無法再設定 [允許內容的後援來源位置]。  相反地，您可以設定界限群組之間的關聯性，以決定用戶端何時可以開始搜尋其他界限群組中的有效內容來源位置。

10. 在 [摘要] 頁面上，檢閱將採取的動作，然後完成精靈。  

     選取部署時，即可在 [監視]  工作區的 [部署]  節點以及封裝部署索引標籤的詳細資料窗格中檢視部署。 如需詳細資訊，請參閱本主題的[監視套件和程式](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs)。  

> [!IMPORTANT]  
>  如果您已在 [部署軟體精靈] 的 [發佈點] 頁面上設定 [從發佈點執行程式] 選項，請不要清除 [將此套件中的內容複製到發佈點上的套件共用] 選項，因為這樣會無法從發佈點執行套件。  

##  <a name="monitor-packages-and-programs"></a>監視套件和程式  
 若要監視套件和程式部署，請使用用來監視應用程式的相同程序 (如[監視應用程式](/sccm/apps/deploy-use/monitor-applications-from-the-console)中所述)。  

 套件和程式也包含數份內建報告，可讓您監視套件和程式部署狀態的相關資訊。 這些報表都有的報表類別目錄 **軟體散發 – 套件和程式** 和 **軟體散發 – 套件和程式的部署狀態**。  

 如需如何在 Configuration Manager 設定報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)。  

##  <a name="manage-packages-and-programs"></a>管理套件和程式  
 在 [軟體程式庫] 工作區中，展開 [應用程式管理] 選擇 [套件]，然後選擇您想要管理的套件，再從下表中選擇管理工作：  

|工作|詳細資訊|  
|----------|----------------------|  
|**建立預先設置的內容檔案**|開啟 [建立預先設置的內容檔案精靈]，讓您建立包含套件內容可手動匯入至另一個網站的檔案。 這是在您有站台伺服器與發佈點之間的低的網路頻寬的情況下很有用。|  
|**建立程式**|開啟 [建立程式精靈]，讓您建立處理此套件的新程式。|  
|**匯出**|開啟 [匯出套件精靈]，讓您將選取的套件及其內容匯出至檔案。<br /><br /> 如需如何匯入套件和程式的資訊，請參閱本主題的[建立套件和程式](/sccm/apps/deploy-use/packages-and-programs#create-packages-and-programs)。|  
|**部署**|開啟 [部署軟體精靈]，讓您將選取的套件和程式部署到集合。 如需詳細資訊，請參閱本主題的[部署套件和程式](/sccm/apps/deploy-use/packages-and-programs#deploy-packages-and-programs)。|  
|**發佈內容**|開啟 [發佈內容精靈]，讓您將與套件和程式相關聯的內容傳送到選取的發佈點或發佈點群組。|  
|**更新發佈點**|使用所選取封裝和程式的最新內容來更新發佈點。|  

##  <a name="about-the-package-definition-file-format"></a>關於套件定義檔的格式  
 套件定義檔是指令碼，可用來使用 Configuration Manager 協助自動化建立套件和程式。 它們提供 Configuration Manager 建立套件和程式所需要的全部資訊，套件來源檔案的位置除外。 每個套件定義檔都是使用 .ini 檔格式並包含下列區段的 ASCII 或 UTF-8 文字檔：  

###  <a name="pdf"></a>[PDF]  
 本章節會將檔案識別封裝定義檔。 它包含下列資訊:  

-   **版本**：指定檔案使用的套件定義檔案格式的版本。 這會對應到寫入的 System Management Server (SMS) 或 Configuration Manager 版本。 這是必要項目。  

###  <a name="package-definition"></a>[封裝定義]  
 指定套件和程式的內容。 它提供下列資訊：  

-   **名稱**：封裝，最多 50 個字元的名稱。  

-   **版本** (選擇性)：套件的版本，不可超過 32 個字元。  

-   **圖示**(選擇性)：包含要用於此套件圖示的檔案。 如果指定，此圖示會取代 Configuration Manager 主控台中的預設套件圖示。

-   **發行者**:封裝，最多 32 個字元的 「 發行者 」。

-   **語言**：封裝，最多 32 個字元的語言版本。

-   **註解**(選擇性)：套件的相關註解，不可超過 127 個字元。

-   **ContainsNoFiles**:這個項目指出來源與封裝相關聯。  

-   **程式**：為此套件定義的程式。 每個程式名稱會對應至 **[程式]** 這個封裝定義檔中的一節。  

     範例：  

     `Programs=Typical, Custom, Uninstall`  

-   **MIFFileName**:包含封裝狀態的 最多 50 個字元的管理資訊格式 (MIF) 檔案的名稱。  

-   **MIFName**:最多 50 個字元 (適用於 MIF 比對) 封裝的名稱。  

-   **MIFVersion**:最多 32 個字元 (適用於 MIF 比對) 封裝的版本號碼。  

-   **MIFPublisher**:最多 32 個字元 (適用於 MIF 比對) 封裝的軟體發行者。  

###  <a name="program"></a>[程式]  
 針對 [Package Definition] 區段的 **Programs** 項目中所指定的每個程式，套件定義檔必須包含可定義該程式的 [Program] 區段。 每個程式 」 一節會提供下列資訊：  

-   **名稱**：程式最多 50 個字元的名稱。 此項目必須是唯一在封裝內。 這個名稱用定義廣告時。 用戶端電腦上的程式名稱所示 **執行已公告程式** 控制台 中。  

-   **圖示**(選擇性)：指定包含要用於此程式之圖示的檔案。 如果指定，此圖示會取代 Configuration Manager 主控台中的預設程式圖示，並在公告程式時顯示在用戶端電腦上。

-   **註解**(選擇性)：有關程式的註解，不可超過 127 個字元。

-   **CommandLine**：指定程式的命令列，不可超過 127 個字元。 此命令為相對於套件來源資料夾。

-   **StartIn**：指定程式的工作資料夾，不可超過 127 個字元。 這個項目可以是用戶端電腦上的絕對路徑，或套件來源資料夾的相對路徑。

-   **執行**：指定程式會執行的程式模式。 您可以指定 **最小化**, ， **最大化**, ，或 **隱藏**。 如果不包含這個項目，則會以一般模式執行程式。  

-   **AfterRunning**：指定在程式順利完成之後發生的任何特殊動作。 可用選項有 **SMSRestart**, ， **ProgramRestart**, ，或 **SMSLogoff**。 如果不包含這個項目，程式就不執行特殊動作。  

-   **EstimatedDiskSpace**：指定軟體程式在電腦上執行所需的磁碟空間量。 這可以指定為 **未知** (預設值) 或大於或等於零的整數。 如果指定值，則也必須指定值的單位。  

     範例：  

     `EstimatedDiskSpace=38MB`  

-   **EstimatedRunTime**：指定程式預期在用戶端電腦上執行的預估期間 (分鐘)。 這可以指定為 **未知** (預設值) 或大於零的整數數字。  

     範例：  

     `EstimatedRunTime=25`  

-   **SupportedClients**：指定這個程式執行所在的處理器和作業系統。 指定的平台必須以逗號分隔。 如果不包含這個項目，就會停用這個程式的支援平台檢查。  

-   **SupportedClientMinVersionX**、**SupportedClientMaxVersionX**：指定 **SupportedClients** 項目中指定的作業系統版本號碼的開始到結束範圍。  

     範例：  

    ```  
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999   
    ```  

-   **AdditionalProgramRequirements**(選擇性)：提供用戶端電腦的任何其他資訊或需求，不可超過 127 個字元。

-   **CanRunWhen**：指定程式在用戶端電腦上執行所需的使用者狀態。 可用的值為 **UserLoggedOn**, ， **NoUserLoggedOn**, ，或 **AnyUserStatus**。 預設值是 **UserLoggedOn**。  

-   **UserInputRequired**：指定程式是否需要與使用者互動。 可用的值為 **True** 或 **False**。 預設值是 **True**。 此項目設定為 **False** 如果 **CanRunWhen** 未設定為 **UserLoggedOn**。  

-   **AdminRightsRequired**：指定程式是否需要電腦上的系統管理認證才能執行。 可用的值為 **True** 或 **False**。 預設值是 **False**。 此項目設定為 **True** 如果 **CanRunWhen** 未設定為 **UserLoggedOn**。  

-   **UseInstallAccount**：指定程式在用戶端電腦上執行時是否使用用戶端軟體安裝帳戶。 根據預設，這個值是 **False**。 此值也是 **False** 如果 **CanRunWhen** 設為 **UserLoggedOn**。  

-   **DriveLetterConnection**：指定程式是否需要與發佈點上套件檔案的磁碟機代號連線。 您可以指定 **True** 或 **False**。 預設值為 **False**，可讓程式使用通用命名慣例 (UNC) 連線。 這個值設定為 **True** 時，將會使用下一個可用的磁碟機代號 (從 Z: 開始，並往回處理)。  

-   **SpecifyDrive**(選擇性)：指定程式連線到發佈點上套件檔案所需的磁碟機代號。 此規格會強制使用指定的磁碟機代號給用戶端連線到發佈點。

-   **ReconnectDriveAtLogon**：指定電腦是否在使用者登入時重新連線到發佈點。 可用的值為 **True** 或 **False**。 預設值是 **False**。  

-   **DependentProgram**：指定這個套件中必須在目前程式之前執行的程式。 此項目使用下列格式：**DependentProgram**=<**程式名稱>**；其中 **<程式名稱\>** 是在套件定義檔案中為該程式輸入的**名稱**。 如果不有任何相依的程式，將此項目保留空白。  

     範例：  

     DependentProgram = Admin  
    DependentProgram =  

-   **指派**：指定如何將程式指派給使用者。 此值可以是 **FirstUser** (只有第一位登入的使用者才會執行程式) 或 **EveryUser** (每位登入用戶端的使用者都會執行程式)。 當 **CanRunWhen** 未設定為 **UserLoggedOn**, ，此項目設定為 **FirstUser**。  

-   **停用**：指定是否可以向用戶端公告這個程式。 可用的值為 **True** 或 **False**。 預設值為 **False**。  
