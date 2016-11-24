---
title: "部署 App-V 虛擬應用程式 | System Center Configuration Manager"
description: "查看在您建立及部署虛擬應用程式時，必須考慮什麼事項。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
caps.latest.revision: 11
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d6e787d5968b281afe4e4b475287944563c8a77f


---
# <a name="deploy-app-v-virtual-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 部署 App-V 虛擬應用程式

*適用於：System Center Configuration Manager (最新分支)*

建立和部署虛擬應用程式時，除了建立應用程式的其他 System Center Configuration Manager 需求和程序之外，還必須考慮下列項目。  

 當您使用 Configuration Manager 來管理虛擬應用程式時，會獲得下列好處：  

-   使用單一管理基礎結構  

-   延展性、部署和內容發佈功能，例如集合和使用者裝置親和性  

-   利用 Configuration Manager 提供的進階應用程式管理功能  

-   使用 Configuration Manager 功能，例如作業系統部署、軟體和硬體清查、軟體計量及 Asset Intelligence，以支援虛擬應用程式  

如需如何使用 App-V 建立應用程式與排序的詳細資訊，請參閱 TechNet 文件庫中的 [Application Virtualization](https://technet.microsoft.com/library/cc843848.aspx) 。  

若要將虛擬應用程式部署至電腦，您必須在您的電腦上先安裝 Configuration Manager 用戶端和 App-V 用戶端。 用戶端裝置可包含桌面和可攜式電腦以及虛擬桌面基礎結構 (VDI) 用戶端。 Configuration Manager 搭配 App-V 用戶端軟體一起運作，以傳遞、尋找並啟動虛擬應用程式套件。 Configuration Manager 用戶端可管理將虛擬應用程式套件傳遞至 App-V 用戶端的程序。 App-V 用戶端便會在用戶端上執行虛擬應用程式。  

-   若要部署虛擬應用程式，您必須先使用 App-V Application Virtualization Sequencer 建立虛擬應用程式。 此排序器會監控應用程式的安裝以及設定程序，並且記錄在虛擬環境中執行應用程式所需的資訊。 您也可以使用排序器設定要將哪些檔案和設定套用至所有使用者以及使用者可以自訂哪些設定。  

-   當您將應用程式排序時，您必須將封裝儲存至 Configuration Manager 可以存取的位置。 然後，您可以建立含有此虛擬應用程式的應用程式部署。  

-   Configuration Manager 不支援使用 App-V 的共用唯讀快取功能。  

-   Configuration Manager 支援 App-V 5 中的共用內容存放區功能。  

-   當您建立虛擬應用程式的部署類型時，Configuration Manager 會使用應用程式資訊清單檔案的內容建立部署類型。 這是一種 XML 檔案，其中含有關於虛擬應用程式的資訊。 此外，Configuration Manager 會根據 App-V .osd 檔案 (其中包含有關虛擬應用程式支援的作業系統資訊) 的內容建立部署類型的需求。  

-   為了在 Configuration Manager 中部署虛擬應用程式，用戶端電腦必須安裝至少 App-V 4.6 SP1 或更新版本的用戶端。  

-   此外，您必須先使用知識庫文章 [2645225](https://support.microsoft.com/kb/2645225)中所描述的 Hotfix 更新 App-V 用戶端，才能成功部署虛擬應用程式。  
  
-   當您在 Microsoft Application Virtualization 5.0 中使用連線群組時，您已部署的虛擬應用程式便可以在用戶端電腦上共用相同的檔案系統和登錄。 不同於標準的虛擬應用程式，這些應用程式可以互相共用資料。 此外，連線群組會為其所包含的應用程式保存使用者設定。 Configuration Manager 中的 App-V 虛擬環境會用來設定用戶端電腦上的連線群組。 當已安裝應用程式或是在用戶端下次評估已安裝的應用程式時，用戶端電腦上便會建立或變更虛擬環境。 您可以設定這些應用程式的優先權，當有多個應用程式嘗試變更檔案系統或登錄值時，具有最高優先權的應用程式便會優先變更。 如需詳細資訊，請參閱[建立 App-V 虛擬環境](../../apps/deploy-use/create-app-v-virtual-environments.md)。  

##  <a name="supported-app-v-versions"></a>支援的 APP-V 版本  
 Configuration Manager 支援以下 App-V 版本︰  

-   **App-V 4.6：**若要在 Configuration Manager 中使用虛擬應用程式，用戶端電腦必須已安裝 App-V 4.6 SP1、App-V 4.6 SP2 或 App-V 4.6 SP3 用戶端。  

     您也必須先使用知識庫文章 [2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) (機器翻譯) 中所描述的 Hotfix 來更新 App-V 4.6 SP1 用戶端，才能成功部署虛擬應用程式。  

-   **App-V 5、App-V 5.0 SP1、App-V 5.0 SP2、App-V 5.0 SP3 和 App-V 5.1：** 對於 App-V 5.0 SP2，您必須安裝 [Hotfix 套件 5](https://support.microsoft.com/en-us/kb/2963211) 或使用 App-V 5.0 SP3。  

##  <a name="steps-to-manage-app-v-virtual-applications"></a>管理 App-V 虛擬應用程式的步驟  
 若要管理 App-V 虛擬應用程式，請完成下列步驟：  

-   **排序** - 排序是指使用 App-V 排序器將應用程式轉換為虛擬應用程式的程序。  

-   **建立 Configuration Manager 應用程式** – 使用 [建立部署類型精靈] 將已排序的應用程式匯入至 Configuration Manager 部署類型，以供稍後新增至應用程式。 您也可同時建立虛擬環境以允許多個虛擬應用程式共用設定。  

-   **發佈** – 發佈為使 App-V 應用程式可在 Configuration Manager 發佈點上使用的程序。  

-   **部署** – 此部署程序可確保應用程式可在用戶端電腦上使用。 亦即 App-V 完整基礎結構中所稱的串流， Configuration Manager 提供兩個部署虛擬應用程式的選項︰[串流] 和 [下載並執行]。  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Configuration Manager 虛擬應用程式傳遞方法  
 Configuration Manager 支援兩個將虛擬應用程式傳遞至用戶端的方法︰串流傳遞和本機傳遞 (下載並執行)。  

-   **串流傳遞**  

     當您使用 Configuration Manager 來管理 App-V 用戶端時，其支援透過 HTTP 或 HTTPS，從發佈點進行虛擬應用程式的串流。 透過 HTTP 或 HTTPS 進行串流已預設為啟用，其設定位於發佈點內容對話方塊。 當您將虛擬應用程式部署至用戶端電腦時，若某個使用者執行該虛擬應用程式，Configuration Manager 用戶端會與管理點連絡以決定應使用的發佈點；接著應用程式會由該發佈點進行串流。  

-   **本機傳遞 (下載並執行)**  

     當您使用此傳遞方法時，Configuration Manager 用戶端會先將整個虛擬應用程式套件下載至 Configuration Manager 用戶端快取，接著指示 App-V 用戶端由 Configuration Manager 快取點將應用程式串流至 App-V 快取。 如果您將虛擬應用程式部署至用戶端電腦，而其內容不在 App-V 快取中，App-V 用戶端會從 Configuration Manager 用戶端快取，將應用程式內容串流至 App-V 快取中，然後執行該應用程式。 應用程式成功執行之後，您可設定 Configuration Manager 用戶端於下個刪除週期刪除任何舊版的套件，或將它們保存在 Configuration Manager 用戶端快取中。  

 在決定要使用哪個 Configuration Manager 虛擬應用程式傳遞方法時，您可先進行比較︰串流傳遞時磁碟空間需求較低，而使用本機傳遞時則可保證 App-V 應用程式的可用性。 進行本機傳遞時需要增加用戶端磁碟空間，這樣可能會比串流傳遞好，這樣使用者就可以隨時從任何位置使用應用程式。  

 使用下列表格中的資訊來協助您選擇最佳的傳遞方法。  

 **串流傳遞**  

|優點|缺點|  
|----------------|-------------------|  
|此方法使用標準的網路通訊協定，從發佈點串流套件內容。<br /><br /> 虛擬應用程式的程式捷徑會叫用發佈點的連線，如此虛擬應用程式便可隨選即用。<br /><br /> 此方法適用於具有高頻寬發佈點連線的用戶端。<br /><br /> 分散於整個企業的虛擬應用程式若有更新，用戶端可於接收到通知目前版本已被取代的原則時，僅下載舊版的變更。<br /><br /> 存取權限會在發佈點定義，以避免使用者存取未獲授權的應用程式或套件。|在使用者首次執行應用程式之後，虛擬應用程式才會進行串流動作。 在此案例中，使用者會先接收虛擬應用程式的程式捷徑，接著由網路斷線，才可首次執行該虛擬應用程式。 若使用者在用戶端離線時試圖執行該虛擬應用程式，使用者將看見錯誤訊息且將無法執行該虛擬應用程式，原因是 Configuration Manager 發佈點不可用來進行應用程式的串流。 應用程式將無法使用，除非使用者重新連線至網路並執行應用程式。<br /><br /> 若要避免這種情形，您可以使用本機傳遞方法來傳遞虛擬應用程式給用戶端，或者您可以啟用以網際網路為基礎的用戶端管理以使用串流傳遞。|  

 **本機傳遞**  

|優點|缺點|  
|----------------|-------------------|  
|此標準發佈點功能可透過背景智慧型傳送服務 (BITS) 來下載套件。<br /><br /> 虛擬應用程式套件內容透過本機傳遞給用戶端，表示使用者在電腦未連線到網路時仍可執行該應用程式。<br /><br /> 此方法適用於速度較慢或不穩定的網路連線，以及偶爾才會連線到網路的電腦。<br /><br /> Configuration Manager 會在虛擬應用程式套件內容更新時，使用遠端差異壓縮 (RDC)，僅將檔案中已變更的位元組傳送給用戶端。 Configuration Manager 用戶端會依據目前版本的套件及任何傳送給用戶端的變更，使用 RDC 建立一個新的虛擬應用程式套件版本。<br /><br /> 此方法可為行動使用者或已中斷連線使用者提供應用程式恢復功能。 若虛擬應用程式是使用「安裝」動作部署，系統管理員可選擇在傳遞後將套件保存在 Configuration Manager 快取。 Configuration Manager 用戶端快取中的套件可在 App-V 用戶端將套件提取至快取時，作為一個可靠的本機串流來源。|若要將虛擬應用程式保存在 Configuration Manager 快取中，用戶端上的磁碟空間必須為虛擬應用程式套件的兩倍以上。|  

 您也可在電腦上預先安裝虛擬應用程式，接著建立該電腦的映像以用來部署至其他電腦。 不過，若虛擬應用程式套件建立在不同網站中，則不會使用二進位差異複寫將更新下載至應用程式。 此選項對於虛擬桌面基礎結構可能很有用，尤其是在您希望應用程式立即可用時，不需等到使用者登入後才下載應用程式。  

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a>將 App-V 基礎結構移轉至 Configuration Manager 和 App-V 基礎結構  
 使用下列表格中的資訊來協助您規劃將現有的 App-V 基礎結構移轉至 Configuration Manager 的虛擬應用程式管理。  

|步驟|詳細資訊|  
|----------|----------------------|  
|查看您目前的虛擬應用程式，選擇要移轉至 Configuration Manager 基礎結構的應用程式。|沒有其他資訊。|  
|評估使用者和裝置，以用於部署虛擬應用程式。|建立 Configuration Manager 集合來將使用者和裝置分組在一起，以用於部署虛擬應用程式。 如需詳細資訊，請參閱[集合簡介](/sccm/core/clients/manage/collections/introduction-to-collections)。|  
|將 App-V 5 連線群組移轉至 Configuration Manager 虛擬環境。|如需詳細資訊，請參閱此主題中的[將 App-V 5 連線群組移轉至 Configuration Manager 虛擬環境](/sccm/apps/get-started/deploying-app-v-virtual-applications#migrate-app-v-5-connection-groups-to-configuration-manager-virtual-environments)一節。|  
|調查並找出在您的 Configuration Manager 基礎結構中，是否有任何虛擬應用程式以完整應用程式存在。|為了方便管理，您可將該虛擬應用程式新增為現有完整應用程式的一個新部署類型。 如需如何建立部署類型的詳細資訊，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。|  
|建立可用來取代現有 App-V 套件的應用程式。|如需如何建立 Configuration Manager 應用程式的詳細資訊，請參閱[應用程式管理簡介](/sccm/apps/understand/introduction-to-application-management)和[建立應用程式](../../apps/deploy-use/create-applications.md)。|  
|Configuration Manager 將在首次部署虛擬應用程式之後，開始在用戶端上管理虛擬應用程式。 從此之後，該電腦上的所有 App-V 應用程式都將由 Configuration Manager 管理。|沒有其他資訊。|  
|將內容發佈至適當的發佈點，以啟用應用程式的本機傳遞。|如需詳細資訊，請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。|  
|部署應用程式到 Configuration Manager 用戶端。<br /><br /> 如果您用來建立 App-V 應用程式的排序器，是不會建立資訊清單 XML 檔案的較舊版本，您可以在較新版的排序器中開啟及儲存該應用程式，以建立檔案。 使用 Configuration Manager 部署虛擬應用程式時需要用到此檔案。<br /><br /> App-V 支援以 SoftGrid 4.1 SP1 或 4.2 版排序器建立的虛擬應用程式套件。<br /><br /> 若應用程式之前已在本機安裝，您必須先解除安裝，才能部署該應用程式的虛擬版本。|如需詳細資訊，請參閱[部署應用程式](../../apps/deploy-use/deploy-applications.md)。|  
|System Center Configuration Manager 不再支援使用包含虛擬應用程式的套件和程式。 當您從 Configuration Manager 2007 移轉至 System Center Configuration Manager 時，Configuration Manager 會將這些套件轉換成應用程式。<br /><br /> Configuration Manager 2007 公告也將轉換成下列部署類型︰<br /><br /> - 移轉不具有公告的 App-V 套件：一個使用預設部署類型設定的部署類型。<br /><br /> - 移轉具有一個公告的 App-V 套件： <br />                一個與 Configuration Manager 2007 公告使用相同設定的預設部署類型。<br /><br /> - 移轉具有多個公告的 App-V 套件：一種適用於每個  <br />                Configuration Manager 2007 公告的部署類型，會使用該公告的設定。|如需詳細資訊，請參閱[規劃將 Configuration Manager 物件移轉至 System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)。|  

##  <a name="migrate-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>將 App-V 5 連線群組移轉至 Configuration Manager 虛擬環境  
 Configuration Manager 中的 App-V 虛擬環境可允許您所部署的虛擬應用程式，共用用戶端電腦的相同檔案系統和登錄。 這表示這些應用程式之間可共用資料，有別於標準的虛擬應用程式。 當已安裝應用程式或是在用戶端下次評估已安裝的應用程式時，用戶端電腦上便會建立或修改虛擬環境。 虛擬環境類似獨立 App-V 5 中的連線群組。  

 當您將連線群組從獨立 App-V 5 移轉至 Configuration Manager 虛擬環境時，必須確保用戶端電腦上既存的連線群組受到 Configuration Manager 的適當管理，而且那些連線群組中的使用者環境也已保留。  

 使用下列程序以協助您順利將 App-V 5 連線群組轉換成 Configuration Manager 虛擬環境。  
  
### <a name="convert-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>將 App-V 5 連線群組轉換成 Configuration Manager 虛擬環境  
  
1.  為存在於 App-V 的所有應用程式建立 Configuration Manager 應用程式。  

2.  配合 [必要] 部署目的將應用程式部署到使用者或裝置。 使用者部署必須部署到在 App-V 內使用應用程式的相同使用者，電腦部署必須部署到在 App-V 內有該應用程式的相同電腦。  

3.  完成部署後，根據在獨立 App-V 中發佈的連線群組，建立相符的虛擬環境。 虛擬環境必須包含相同的封裝，尤其是按照相同順序排列的 App-V 5 部署類型。  

如需如何建立 App-V 虛擬環境的資訊，請參閱[如何在 Configuration Manager 中建立 App-V 虛擬環境](../../apps/deploy-use/create-app-v-virtual-environments.md)。  

或者，您可以在透過 Configuration Manager 部署應用程式之前，從 App-V 用戶端刪除所有連線群組。 不過，這樣可能會失去使用者儲存在 App-V 連線群組中的任何設定。  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>App-V 4.6 中的動態套件組合  
 透過動態套件組合的功能，您可以將某個虛擬應用程式套件定義為相依於另一個虛擬應用程式套件。 應用程式執行時，App-V 用戶端會在應用程式的相同虛擬環境中裝載主要套件和相依的套件。  

 若要透過 Configuration Manager 使用此功能，您必須同時部署兩個套件並且以 App-V 用戶端註冊。 為了確保相依套件內容能裝載於用戶端電腦本機上，請針對本機傳遞 (下載與執行) 設定應用程式部署。  

 如需 App-V 動態套件組合的詳細資訊，請參閱 App-V 說明文件。  

##  <a name="convert-app-v-46-applications-to-app-v-5-applications"></a>將 App-V 4.6 應用程式轉換為 App-V 5 應用程式  
 App-V 4.6 與 App-V 5 之間的應用程式封裝格式已變更。 不再支援使用 App-V 4.6 排序的應用程式。 不過，App-V 5 已提供一種可讓您轉換應用程式的套件轉換工具。 如需詳細資訊，請參閱 [App-V 5 說明文件](http://technet.microsoft.com/library/jj713472.aspx)。  

 利用下列步驟以轉換 App-V 4.6 應用程式為 App-V 5 應用程式：  

1.  轉換或重新排序 App-V 4.6 套件為 App-V 5 格式。  

2.  將 App-V 5 用戶端部署至階層內的電腦。  

3.  建立包含 App-V 5 應用程式部署類型的新應用程式，並且建立取代規則以取代 App-V 4.6 應用程式。  

4.  按照需求建立虛擬環境。  

5.  部署新的 App-V 5 應用程式至電腦。  

##  <a name="user-and-deployment-configuration-files"></a>使用者與部署組態檔案  
 使用者與部署設定檔案包含控制應用程式行為的設定。 您可以使用這些檔案以變更應用程式設定，不需重新排序應用程式。  

 標準的 App-V 5 應用程式可包含下列檔案：  

-   應用程式套件 (.appv) 檔。  

-   使用者設定檔。  

-   部署設定檔。  

 使用者設定檔包含只可以套用至登入使用者的設定。 例如，您可以編輯設定檔以變更將部署至使用者的有關應用程式捷徑的資訊。 您也可以配合多種部署類型來建立 Configuration Manager 應用程式，每種部署類型可包含不同的使用者設定檔，並使用需求規則以確保這些規則已針對相關使用者進行安裝。  

 部署設定檔包含套用至電腦的設定，例如登陸設定。 檔案也可包含將套用至所有使用者的使用者設定。  

 如果您要使用 Configuration Manager 部署 App-V 5 虛擬應用程式，則在建立 App-V 5 部署類型時，這三個檔案都必須位於相同資料夾中。 如果資料夾內有多個檔案，Configuration Manager 將使用最新的檔案。  

 如需詳細資訊，請參閱 [App-V 5 說明文件](http://technet.microsoft.com/library/jj713466.aspx)。  

##  <a name="app-v-local-interaction"></a>APP-V 本機互動  
 在部分應用程式部署案例中，應用程式會安裝在用戶端電腦本機上，而其他應用程式則會當作虛擬應用程式部署至相同的用戶端電腦。 根據預設，本機上所安裝的應用程式無法偵測到虛擬應用程式並直接與其進行通訊。 這是由 App-V 提供的應用程式獨立的指定行為。 您可以為每個應用程式啟用 App-V 用戶端的本機互動功能，以允許在用戶端電腦上執行的本端安裝應用程式能夠偵測到虛擬應用程式並直接與其進行通訊。 Configuration Manager 與 App-V 可完整支援本機互動。  

 如需 App-V 本機互動功能的詳細資訊，請參閱您的 App-V 說明文件。  

##  <a name="app-v-5-shared-content-store"></a>APP-V 5 共用內容存放區  
 Configuration Manager 支援 App-V 5 共用內容存放區功能。 如需詳細資訊，請參閱 [規劃 App-V 5.0 共用內容存放區 (SCS)](http://technet.microsoft.com/library/jj713431.aspx)。  

##  <a name="monitor-virtual-applications"></a>監視虛擬應用程式  

### <a name="virtual-application-reports"></a>虛擬應用程式報告  
 您可以使用下列報告以監視在您 Configuration Manager 環境內的 App-V：  

|報表名稱|說明|  
|-----------------|-----------------|  
|App-V 虛擬環境結果|如果選取的虛擬環境狀態與所選集合指定的狀態相符，則顯示與該環境有關的資訊 (僅限 App-V 5)。|  
|資產的 App-V 虛擬環境結果|如果選取的虛擬環境與所選虛擬環境指定的資產和任何部署類型相符，則顯示與該環境有關的資訊 (僅限 App-V 5)。|  
|App-V 虛擬環境狀態|針對選取的集合顯示所選虛擬環境的相容性資訊。 這分報告中的 [已保留]  欄顯示已經無法再套用之前設定的虛擬環境資產，但已經保留以便應用程式內的使用者設定可持續在虛擬環境中執行 (僅限 App-V 5)。|  
|具有特定虛擬應用程式的電腦|具有使用 Application Virtualization Management Sequencer 建立的指定 App-V 應用程式捷徑的電腦摘要。(僅限 App-V 4.6)。|  
|具有特定虛擬應用程式套件的電腦|顯示已安裝指定 App-V 應用程式套件的電腦清單 (僅限 App-V 4.6)。|  
|計算虛擬應用程式套件的所有執行個體|顯示所有已偵測到的 App-V 應用程式套件的計數 (僅限 App-V 4.6)。|  
|計算虛擬應用程式的所有執行個體|顯示所有已偵測到的 App-V 應用程式計數 (僅限 App-V 4.6)。|  

## <a name="log-files"></a>記錄檔  
 Configuration Manager 將有關虛擬應用程式部署的資訊記錄在記錄檔內。 如需虛擬應用程式和 Configuration Manager 應用程式管理所使用之記錄檔的資訊，請參閱 [System Center Configuration Manager 中的記錄檔](../../core/plan-design/hierarchy/log-files.md)。  

 另外，您可以在下列位置找到 App-V 用戶端的記錄：  

-   Windows Vista、Windows 7 和 Windows 8： **C:\ProgramData\Microsoft\Application Virtualization Client**  



<!--HONumber=Nov16_HO1-->


