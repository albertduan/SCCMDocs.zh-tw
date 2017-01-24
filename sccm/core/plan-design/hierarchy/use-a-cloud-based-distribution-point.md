---
title: "雲端架構發佈點 | Microsoft Docs"
description: "了解搭配使用雲端發佈點與 System Center Configuration Manager 的設定和限制。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 840f7be09f234d598bc7856d53e278665808fef1


---
# <a name="use-a-cloud-based-distribution-point-with-system-center-configuration-manager"></a>使用雲端架構發佈點搭配 System Center Configuration Manager

*適用於：System Center Configuration Manager (最新分支)*

雲端發佈點是裝載於 Microsoft Azure 的 System Center Configuration Manager 發佈點。 下列資訊旨在協助您了解設定和使用雲端式發佈點的限制。

安裝主要站台並準備安裝雲端式發佈點之後，請參閱 [Install cloud-based distribution points in Microsoft Azure](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md) (在 Microsoft Azure 中安裝雲端式發佈點)。


## <a name="plan-to-use-a-cloud-based-distribution-point"></a>使用雲端式發佈點的計劃
使用雲端式發佈點時，您必須：  

-   **進行用戶端設定** 以利使用者及裝置存取內容  

-   **指定要管理內容傳輸的主要站台** 到發佈點  

-   為要儲存在發佈點上的內容量，以及要讓用戶端從發佈點傳輸的內容量**指定閾值** 。  


根據您所設定的閾值，Configuration Manager 可以在您儲存於發佈點上的內容總和量接近指定儲存量時，或者用戶端的資料傳輸量接近您定義的閾值時產生警示。  

雲端發佈點支援以下內部部署發佈點也支援的功能：  

-   您可個別管理雲端發佈點，或以發佈點群組的成員進行管理。  

-   您可將雲端發佈點用於後援內容位置。  

-   您會受到內部網路和網際網路型用戶端的支援。  


雲端發佈點提供以下額外優勢：  

-   在 Configuration Manager 將已傳送至雲端發佈點的內容傳送至 Microsoft Azure 之前，Configuration Manager 會先將內容加密。  

-   在 Microsoft Azure 中，您可以手動調整雲端服務以符合用戶端對於內容不斷變動的要求，而不需要安裝及佈建額外的發佈點。  

-   雲端發佈點支援已針對 Windows BranchCache 設定的用戶端下載內容。  


雲端發佈點有下列限制：  

-   您不能使用雲端發佈點來裝載軟體更新套件。  

-   您無法將雲端發佈點用於 PXE 或啟用多點傳送的部署。  

-   雲端發佈點不會提供給用戶端，當作使用 [執行工作順序以視需要將內容下載到本機] 部署選項部署之工作順序的內容位置。 不過，使用 [啟動工作順序之前下載所有內容到本機]  部署選項部署的工作順序可以使用雲端發佈點做為有效的內容位置。  

-   雲端發佈點並不支援從發佈點執行的套件。 所有內容都必須由用戶端進行下載，然後在本機執行。  

-   雲端發佈點不支援使用 Application Virtualization 或類似程式來串流應用程式。  

-   雲端發佈點不支援預先設置的內容。 管理發佈點的主要網站發佈管理員會將所有內容傳送至發佈點。  

-   雲端發佈點無法設定為提取發佈點。  

##  <a name="a-namebkmkprereqsclouddpa-prerequisites-for-cloud-based-distribution-points"></a><a name="BKMK_PrereqsCloudDP"></a> 雲端式發佈點的必要條件  
 雲端發佈點需符合下列使用必要條件：  

-   Microsoft Azure 訂用帳戶。  (請參閱本主題中的[關於訂閱和憑證](#BKMK_CloudDPCerts))

-   用於 Configuration Manager 主要站台伺服器對 Microsoft Azure 雲端服務通訊的自我簽署或 PKI 管理憑證。  (請參閱本主題中的[關於訂閱和憑證](#BKMK_CloudDPCerts))

-   Configuration Manager 用戶端用來連線至雲端發佈點以及使用 HTTPS 下載內容的服務憑證 (PKI)。  

-   在裝置或使用者可以從雲端發佈點存取內容之前，裝置或使用者必須先接收 [允許存取雲端發佈點]  的 [雲端服務]  用戶端設定 (設為 [是] )。 根據預設，此值是設為 [否] 。  

-   用戶端必須能夠解析雲端服務的名稱，而這需要網域名稱系統 (DNS) 命名空間中的 DNS 別名 (CNAME 記錄)。  

-   用戶端必須能夠存取網際網路以使用雲端發佈點。  

##  <a name="a-namebkmkclouddpcosta-cost-of-using-cloud-based-distribution"></a><a name="BKMK_CloudDPCost"></a> 使用雲端式發佈的成本  
 當您使用雲端發佈點時，請規劃 Configuration Manager 用戶端所執行資料儲存與下載傳輸的成本。  

 Configuration Manager 包含可協助控制成本及監視資料存取的選項：  

-   您可以控制及監視儲存於雲端服務中的內容量。  

-   您可以設定 Configuration Manager 在用戶端下載的**閾值**達到或超過每月限制時，向您發出警示。  

-   此外，您可以使用對等快取 (BranchCache) 協助減少用戶端從雲端式發佈點所傳輸的資料量。 根據預設，針對 Windows BranchCache 所設定的 Configuration Manager 用戶端可以使用雲端發佈點傳輸內容。  


**選項：**  

-   **雲端的用戶端設定**：您可以使用 **[用戶端設定]**來控制對階層中所有雲端式發佈點的存取。  

     在 [用戶端設定] 中，[雲端設定]  類別支援 [允許存取雲端發佈點] 設定。 根據預設，此設定值是設為 [否] 。 您可以為使用者和裝置啟用此設定值。  

-   **資料傳輸的閾值**︰您可以為您想要在發佈點上儲存的資料量，以及用戶端從發佈點下載的資料量，設定閾值。  

     雲端架構發佈點包含下列閾值：  

    -   **存放裝置警示閾值**：存放裝置警示閾值可設定您要儲存在雲端架構發佈點的資料或內容量上限。 您可以指定 Configuration Manager 在存放裝置警示閾值剩餘可用空間達到指定層級時產生警告警示。  

    -   **傳輸警示閾值**：傳輸警示閾值可協助您監視 30 天內從發佈點傳輸至用戶端的內容量。 傳輸警示閾值會監視過去 30 天內的資料傳輸量，並且可以在傳輸量達到您所定義的值時產生警告警示和重大警示。  

        > [!IMPORTANT]  
        >  Configuration Manager 會監視資料傳輸，但不會在資料傳輸量超出指定的傳輸警示閾值時停止傳輸資料。  

 您可以在安裝發佈點時指定每個雲端架構發佈點的閾值，也可以在安裝雲端架構的發佈點後個別編輯其內容。  

-   **警示**：您可以設定讓 Configuration Manager 根據您指定的資料傳輸閾值，引發與每個雲端式發佈點的資料傳入和傳出相關的警示。 這些警示可協助您監視資料傳輸，而且有助於決定何時該停止雲端服務以防止雲端服務使用、調整您儲存在發佈點中的內容，或是修改可以使用雲端架構發佈點的用戶端。  

     每小時的週期中，監視雲端發佈點的主要站台會從 Microsoft Azure 下載交易資料，並將其儲存於站台伺服器上的 CloudDP-&lt;ServiceName\>.log 檔。 Configuration Manager 接著會為雲端發佈點評估此資訊對儲存和傳輸的配額。 資料傳輸達到或超過指定的警告警示或重大警示容量時，Configuration Manager 便會產生相應的警示。  

    > [!WARNING]  
    >  由於系統每小時都會從 Windows Azure 下載一次資料傳輸相關資訊，因此在 Configuration Manager 存取資料並產生警示之前，資料使用量可能就已超出警示或重大閾值。  

    > [!NOTE]  
    >  雲端架構發佈點的警示因 Windows Azure 的使用量統計資料而有所不同，最長可能要 24 小時候才能使用。 如需 Windows Azure 適用的儲存體分析的資訊，包括 Windows Azure 更新使用統計資料的頻率，請參閱 MSDN 文件庫中的 [儲存體分析](http://go.microsoft.com/fwlink/p/?LinkID=275111) 。  


-   **依需求停止或啟動雲端服務**：您可以使用此選項來隨時停止雲端服務，以防止用戶端連續使用該服務。 停止雲端服務時，可立即防止用戶端繼續透過該服務下載其他內容。 此外，重新啟動雲端服務即可還原用戶端的存取權限。 例如，您可以在達到閾值時停止雲端服務。  

     停止雲端服務時，雲端服務並不會將內容從發佈點中刪除，也不會阻止網站伺服器將其他內容傳輸至雲端架構的發佈點。  

     若要停止雲端服務，請在 Configuration Manager 主控台的 [管理] 工作區，於 [雲端服務] 下選取 [雲端發佈點] 節點中的發佈點。 接下來，請按一下 [停止服務]  停止在 Windows Azure 中執行的發佈點。  

##  <a name="a-namebkmkclouddpcertsa-about-subscriptions-and-certificates-for-cloud-based-distribution-points"></a><a name="BKMK_CloudDPCerts"></a> 關於雲端式發佈點的訂閱和憑證  
 雲端發佈點需要憑證，以啟用 Configuration Manager 來管理裝載發佈點的雲端服務，以及供用戶端存取發佈點的內容。 下列提供這些憑證的概觀資訊。 如需詳細資訊，請參閱 [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md) (System Center Configuration Manager 的 PKI 憑證需求)。  

 **憑證**  

-   **站台伺服器對發佈點通訊的管理憑證**：管理憑證可在 Microsoft Azure 管理 API 與 Configuration Manager 之間建立信任關係。 此驗證可讓 Configuration Manager 在您執行如部署內容或啟動和停止雲端服務等工作時呼叫 Microsoft Azure API。 使用 Microsoft Azure 時，客戶可以建立自己的管理憑證，該憑證可以是自我簽署憑證或是由憑證授權單位 (CA) 發行的憑證：  

    -   當您針對 Configuration Manager 設定 Microsoft Azure 時，請將管理憑證的 .cer 檔案提供給 Microsoft Azure。 .cer 檔案中包含管理憑證的公用金鑰。 您必須在安裝雲端發佈點之前先將此憑證上傳至 Microsoft Azure。 此憑證可讓 Configuration Manager 存取 Microsoft Azure API。  

    -   當您安裝雲端發佈點時，請將管理憑證的 .pfx 檔案提供給 Configuration Manager。 .pfx 檔案含有用於管理憑證的私密金鑰， Configuration Manager 會將此憑證儲存於站台資料庫中。 由於 .pfx 檔案中含有私密金鑰，您必須提供密碼才能將此憑證檔案匯入 Configuration Manager 資料庫中。  

    如果您建立已自我簽署的憑證，則必須先將憑證匯出為 .cer 檔案，然後再次匯出為 .pfx 檔案。  

    您可以選擇從 Microsoft Azure SDK 1.7 指定版本 1 的 **.publishsettings** 檔案。 如需 .publishsettings 檔案的詳細資訊，請參閱 Microsoft Azure 說明文件。  

    如需詳細資訊，請參閱 MSDN 文件庫 Microsoft Azure 平台區段中的 [如何建立管理憑證](http://go.microsoft.com/fwlink/p/?LinkId=220281) 和 [如何將管理憑證新增至 Microsoft Azure 訂用帳戶](http://go.microsoft.com/fwlink/p/?LinkId=241722) 。  

-   **用戶端對發佈點通訊的服務憑證**：Configuration Manager 雲端發佈點服務憑證可在 Configuration Manager 用戶端與雲端發佈點之間建立信任關係，並且使用「透過 HTTPS 的安全通訊端層」(Secure Socket Layer (SSL) over HTTPS) 來保護用戶端從該發佈點下載的資料。  

    > [!IMPORTANT]  
    >  在服務憑證之憑證主體方塊中的一般名稱在網域中必須是唯一的，不能與任何已加入網域的裝置相同。  

   如需此憑證的部署範例，請參閱 [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) (為 System Center Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位) 主題中的 *Deploying the Service Certificate for Cloud-Based Distribution Points* (為雲端式發佈點部署服務憑證) 一節。  

##  <a name="a-namebkmktasksa-common-management-tasks-for-cloud-based-distribution-points"></a><a name="bkmk_Tasks"></a> 雲端式發佈點的常用管理工作  

-   **站台伺服器對雲端式發佈點的通訊**：當您安裝雲端式發佈點時，您必須指派一個主要站台來管理對雲端服務的內容傳輸。 這個動作等同於將發佈點網站系統角色安裝至特定網站。  

-   **用戶端對雲端式發佈點的通訊**：當裝置或裝置使用者被設定了允許使用雲端式發佈點的用戶端設定時，裝置便可以接收雲端式發佈點作為有效的內容位置：  

    -   當用戶端評估可用的內容位置時，會將雲端式發佈點視為遠端發佈點  

    -   內部網路上的用戶端只會將雲端式發佈點用作內部部署發佈點無法使用時的後援選項。  

    即使您將雲端發佈點安裝在 Microsoft Azure 的特定區域，使用雲端發佈點的用戶端也不會察覺到這些 Microsoft Azure 區域，而且會以不具決定性的方式選取雲端發佈點。 這表示如果您將雲端發佈點安裝在多個區域，而用戶端接收多個雲端發佈點做為內容位置，則用戶端可能不會使用與用戶端位於相同 Microsoft Azure 區域中的雲端發佈點。  

    可使用雲端式發佈點的用戶端會對內容位置要求使用下列順序  

    1.  已設定為使用雲端發佈點的用戶端一律會嘗試先從慣用的發佈點取得內容。  

    2.  如果部署支援此選項且遠端發佈點可以使用，則當慣用發佈點無法使用時，用戶端便會使用遠端發佈點。  

    3.  當慣用發佈點或遠端發佈點無法使用時，用戶端可能會改為從雲端發佈點取得內容。  

        > [!NOTE]  
        >  網際網路上的用戶端若是同時接收以網際網路為基礎的發佈點和雲端發佈點做為部署的內容位置，則只會嘗試從以網際網路為基礎的發佈點擷取內容。 若網際網路上的用戶端無法從以網際網路為基礎的發佈點擷取內容，此時用戶端不會嘗試存取雲端發佈點。  


  當用戶端使用雲端發佈點作為內容位置時，用戶端會使用 Configuration Manager 存取權杖將自己驗證為雲端發佈點。 如果用戶端信任 Configuration Manager 雲端發佈點憑證，則用戶端可以下載所要求的內容。  

-   **監視雲端式發佈點**：您可以監視您部署到每個雲端式發佈點的內容，還可以監視裝載該發佈點的雲端服務。  

    -   **內容**：若要監視佈署到雲端式發佈點的內容，其方式與將內容部署到內部部署發佈點相同。  

    -   **雲端服務**：Configuration Manager 會定期檢查 Windows Azure 服務，如果該服務並未啟用，或出現訂閱或憑證問題，便會產生警示。 在 Configuration Manager 主控台的 [管理] 工作區中，於 [雲端服務] 的 [雲端發佈點] 節點中，您也可以檢視發佈點的詳細資料。 您可以在此位置檢視與該發佈點相關的高階資訊，也可以選取一個發佈點，然後編輯其 [內容] 。  

    當您編輯雲端式發佈點的內容時，可以：  

    -   調整儲存體和警示的資料閾值  

    -   按照管理內部部署發佈點的方式來管理內容  

    最後，您可以檢視每個雲端架構的發佈點的訂閱識別碼、服務名稱，以及在安裝該雲端架構發佈點時指定的其他相關詳細資料，但不能進行編輯。  

-   **雲端式發佈點的備份和復原**：當您在階層中使用雲端式發佈點時，可使用下列資訊來協助您為發佈點的備份或復原做規劃：  

    -   當您使用預先定義的**備份站台伺服器**維護工作，Configuration Manager 會自動包含雲端發佈點的設定。  

    -   最佳作法是備份並儲存使用雲端架構發佈點時所用的管理憑證和服務憑證複本。 如果將管理雲端發佈點的 Configuration Manager 主要站台還原至另一台電腦，您必須先重新匯入憑證，才能繼續使用。  

-   **解除安裝雲端發佈點**：若要解除安裝雲端發佈點，請在 Configuration Manager 主控台中選取發佈點，然後選取 [刪除]。  

    當您從階層中刪除雲端發佈點時，Configuration Manager 會從 Windows Azure 中的雲端服務移除內容。  



<!--HONumber=Dec16_HO3-->


