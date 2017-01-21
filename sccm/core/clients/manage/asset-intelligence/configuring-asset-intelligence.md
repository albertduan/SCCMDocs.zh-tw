---
title: "設定 Asset Intelligence | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中設定 Asset Intelligence。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 43e04a447b03885286c6c7201afb4d1b7a10aa91


---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>設定 System Center Configuration Manager 中的 Asset Intelligence

*適用對象：System Center Configuration Manager (最新分支)*

您必須完成一些設定步驟，才能使用 System Center Configuration Manager 中的 Asset Intelligence 清查及管理整個企業的軟體授權使用量。  

## <a name="steps-to-configure-asset-intelligence"></a>設定 Asset Intelligence 的步驟  
 若要收集 Asset Intelligence 報告所需的清查資料，您必須啟用硬體清查用戶端代理程式。 如需啟用硬體清查用戶端代理程式的資訊，請參閱 [How to extend hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md) (如何擴充 System Center Configuration Manager 中的硬體清查)。  

|步驟|詳細資料|更多資訊|  
|----------|-------------|----------------------|  
|**步驟 1**：啟用 Asset Intelligence 硬體清查報告類別|第一次安裝 Configuration Manager 時不會啟用 Asset Intelligence 資訊收集。 若要啟用 Asset Intelligence，您必須啟用至少一個 Asset Intelligence 報告所依賴的必要硬體清查報告類別。|如需詳細資訊，請參閱本主題的 [Enable Asset Intelligence hardware inventory reporting classes](#BKMK_EnableAssetIntelligence)程序。|  
|**步驟 2**：安裝 Asset Intelligence 同步處理點|Asset Intelligence 同步處理點站台系統角色可用來將 Configuration Manager 站台連線至 System Center Online，以同步處理 Asset Intelligence 類別目錄資訊。 Asset Intelligence 同步處理點僅可安裝在位於 Configuration Manager 階層最上層站台的站台系統中，而且需要使用 TCP 連接埠 443 存取網際網路才能與 System Center Online 同步。<br /><br /> 除了下載新的 Asset Intelligence 類別目錄資訊，Asset Intelligence 同步處理點還可以將自訂軟體項目資訊上傳至 System Center Online 以便分類。 Microsoft 會將所有上傳至 System Center Online 的軟體項目分類為公用資訊。 因此，請確認您自訂的軟體項目不含機密或專利資訊。 如需要求軟體產品分類的詳細資訊，請參閱[要求未分類的軟體產品型錄更新](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate)。|如需詳細資訊，請參閱本主題的 [Install an Asset Intelligence Synchronization Point](#BKMK_InstallAssetIntelligenceSynchronizationPoint)程序。|  
|**步驟 3**：啟用成功登入事件的稽核|系統提供四種 Asset Intelligence 報告，以顯示在用戶端電腦上收集到的 Windows 安全性事件記錄檔資訊。 如果未將安全性事件記錄檔設定為記錄所有成功登入事件，這些報告就不會包含任何資料，即使已啟用適當的硬體清查報告類別亦同。 若要啟用硬體清查用戶端代理程式以清查支援這些報告所需的資訊，您必須先修改用戶端上的 Windows 安全性事件記錄檔設定，以記錄所有成功的登入事件，並啟用 **SMS_SystemConsoleUser** 硬體清查報告類別。|如需詳細資訊，請參閱本主題的 [Enable auditing of success logon events](#BKMK_EnableSuccessLogonEvents)程序。|  
|**步驟 4**：匯入軟體授權資訊|[匯入軟體授權精靈] 可用來將 Microsoft 大量授權 (MVLS) 資訊和一般授權聲明書匯入 Asset Intelligence 類別目錄中。<br /><br /> MVLS 授權聲明書包含 Microsoft 產品的授權權益或購買的授權數量相關資訊。<br /><br /> 一般授權聲明書包含購買之任何發行者的授權資訊。|如需詳細資訊，請參閱本主題的 [Import software license information](#BKMK_ImportSoftwareLicenseInformation)程序。|  
|**步驟 5**：設定 Asset Intelligence 維護工作|下列是 Asset Intelligence 的相關維護工作。 預設會啟用這兩個維護工作並設定預設排程。<br /><br /> **使用清查資訊檢查應用程式標題**：此維護工作會檢查軟體清查中回報的軟體項目與 Asset Intelligence 類別目錄中的軟體項目是否一致。<br /><br /> **摘述已安裝的軟體資料**：此維護工作會提供在 [資產與相容性]  工作區 [Asset Intelligence]  節點下 [已清查的軟體]  節點中顯示的資訊。 執行工作時，Configuration Manager 會收集所有已清查的主要站台軟體項目計數。|如需詳細資訊，請參閱本主題的 [Configure Asset Intelligence maintenance tasks](#BKMK_ConfigureMaintenanceTasks)程序。|  

> [!NOTE]  
>   **摘述已安裝的軟體資料** 只可用於主要站台維護工作。  

## <a name="supplemental-procedures-for-configuring-asset-intelligence"></a>設定 Asset Intelligence 的補充程序  
 請使用上表步驟的下列資訊。  

###  <a name="a-namebkmkenableassetintelligencea-enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 若要在 Configuration Manager 站台中啟用 Asset Intelligence，您必須啟用一或多個 Asset Intelligence 硬體清查報告類別。 您可以在 [Asset Intelligence]  首頁上啟用類別，或是透過 [管理]  工作區中 [用戶端設定]  節點的用戶端設定屬性，來啟用類別。 使用下列其中一個程序啟用 Asset Intelligence 硬體清查報告類別。  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>若要從 Asset Intelligence 首頁啟用 Asset Intelligence 硬體清查報告類別  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性]。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] 。  

3.  在 [首頁]  索引標籤的 [Asset Intelligence]  群組中，按一下 [編輯清查類別] 。 隨即開啟 [編輯清查類別]  對話方塊。  

4.  若要啟用 Asset Intelligence 報告，請選取 [啟用所有 Asset Intelligence 報告類別]  ，或選取 [僅啟用選取的 Asset Intelligence 報告類別] ，然後從顯示的類別中選取至少一個報告類別。  

    > [!NOTE]  
    >  在用戶端掃描並傳回硬體清查之後，透過此程序啟用之硬體清查類別的相關 Asset Intelligence 報告才會顯示資料。  

5.  按一下 [確定]  以啟用 Asset Intelligence 硬體清查報告類別。  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>若要從用戶端設定屬性啟用 Asset Intelligence 硬體清查報告類別  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] ，然後選取 [預設用戶端設定] 。  

    > [!NOTE]  
    >  如果您已建立自訂用戶端設定，則可以選取自訂用戶端設定，而不是預設用戶端設定。  

3.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。 隨即開啟 [用戶端設定內容]  對話方塊。  

4.  按一下 [硬體清查] ，然後按一下 [設定類別] 。 隨即開啟 [硬體清查類別]  對話方塊。  

5.  按一下 [依類別篩選] ，然後按一下 [Asset Intelligence 報告類別] 。 系統僅會以 Asset Intelligence 硬體清查類別來重新整理類別清單。  

6.  從 Asset Intelligence 報告類別的清單中，選取一個以上的報告類別。  

    > [!NOTE]  
    >  在用戶端掃描並傳回硬體清查之後，透過此程序啟用之硬體清查類別的相關 Asset Intelligence 報告才會顯示資料。  

7.  按一下 [確定]  以啟用 Asset Intelligence 硬體清查報告類別。  

###  <a name="a-namebkmkinstallassetintelligencesynchronizationpointa-install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  
 您可以使用下列程序來安裝 Asset Intelligence 同步處理點站台系統角色。  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>若要安裝 Asset Intelligence 同步處理點站台系統角色  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [伺服器和網站系統角色] 。  

3.  使用相關步驟，將 Asset Intelligence 同步處理點站台系統角色新增至新的或現有的網站系統伺服器：  

    -   **新增站台系統伺服器**：在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立站台系統伺服器] 。 隨即開啟 [建立網站系統伺服器精靈]。  

        > [!NOTE]  
        >  根據預設，當 Configuration Manager 安裝站台系統角色時，安裝檔會安裝到擁有最多可用硬碟空間的第一部可用 NTFS 格式化硬碟機上。 若要避免 Configuration Manager 安裝到特定磁碟機上，請建立名為 No_sms_on_drive.sms 的空檔案，並將它複製到磁碟機的根資料夾，再安裝站台系統伺服器。  

    -   **現有的站台系統伺服器**：在您要安裝 Asset Intelligence 同步處理點站台系統角色的伺服器上按一下。 按一下伺服器時，就會在詳細資料窗格中顯示已經安裝在該伺服器上的站台系統角色清單。  

         在 [首頁]  索引標籤的 [伺服器]  群組中，按一下 [新增網站系統角色] 。 隨即開啟 [新增網站系統角色精靈]。  

4.  在 [一般]  頁面上，指定網站系統伺服器的一般設定。 將 Asset Intelligence 同步處理點新增到現有的站台系統伺服器時，請確認之前設定的值。  

5.  在 [系統角色選取]  頁面上，從可用角色清單中選取 [Asset Intelligence 同步處理點]  ，然後按一下 [下一步] 。  

6.  在 [Asset Intelligence 同步處理點連線設定]  頁面上，按一下 [下一步] 。  

     預設會選取 [使用這個 Asset Intelligence 同步處理點]  設定，因此無法在此頁面上進行設定。 System Center Online 僅接受使用 TCP 連接埠 443 的網路流量，因此您無法在精靈的這個頁面上設定 [SSL 連接埠號碼]  。  

7.  您也可以選擇指定 System Center Online 驗證憑證檔案 (.pfx) 的路徑，然後按一下 [下一步] 。 一般來說，您不需要指定憑證路徑，因為站台角色安裝期間會自動佈建連線憑證。  

8.  在 [Proxy 伺服器設定]  頁面上，指定 Asset Intelligence 同步處理點是否要在連線 System Center Online 以同步處理類別目錄時使用 Proxy 伺服器，以及是否要使用認證連接 Proxy 伺服器，然後按一下 [下一步] 。  

    > [!WARNING]  
    >  如果必須使用 Proxy 伺服器才能連線 System Center Online，則在針對 Proxy 伺服器驗證所設的使用者帳戶密碼過期時，可能也會刪除連線憑證。  

9. 在 [同步處理排程]  頁面上，指定是否要同步處理 Asset Intelligence 類別目錄的排程。 如果您啟用同步處理排程，則可以指定簡易或自訂同步處理排程。 在排定的同步處理期間，Asset Intelligence 同步處理點會連線 System Center Online 以擷取最新的 Asset Intelligence 類別目錄。 您可以在 Configuration Manager 主控台中手動同步處理 Asset Intelligence 類別目錄中的 Asset Intelligence 節點。 如需手動同步處理 Asset Intelligence 類別目錄的步驟，請參閱 [System Center Configuration Manager 中的 Asset Intelligence 作業](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)中的[手動同步處理 Asset Intelligence 類別目錄](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog)一節。  

10. 在 [新增站台角色精靈] 的 [摘要]  頁面中，確認已指定的設定都正確後再繼續進行。 若要變更任何設定，請按一下 [上一步]  直到返回適當的頁面，即可進行變更，並返回 [摘要]  頁面。  

###  <a name="a-namebkmkenablesuccesslogoneventsa-enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 使用下列程序來設定電腦的安全性原則登入設定，以啟用成功登入事件的稽核。  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>使用本機安全性原則啟用成功登入事件記錄  

1.  在 Configuration Manager 用戶端電腦上，按一下 [開始]，指向 [系統管理工具]，然後按一下 [本機安全性原則]。  

2.  在 [本機安全性原則]  對話方塊的 [安全性設定] 下方，展開 [本機原則] ，然後按一下 [稽核原則] 。  

3.  在 [結果] 窗格中，按兩下 [稽核登入事件] ，確認選取 [成功]  核取方塊，然後按一下 [確定] 。  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>使用 Active Directory 網域安全性原則啟用成功登入事件記錄  

1.  在網域控制站電腦上，按一下 [開始] ，指向 [系統管理工具] ，然後按一下 [網域安全性原則] 。  

2.  在 [本機安全性原則]  對話方塊的 [安全性設定] 下方，展開 [本機原則] ，然後按一下 [稽核原則] 。  

3.  在 [結果] 窗格中，按兩下 [稽核登入事件] ，確認選取 [成功]  核取方塊，然後按一下 [確定] 。  

###  <a name="a-namebkmkimportsoftwarelicenseinformationa-import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 下列章節說明使用 [匯入軟體授權精靈] 將 Microsoft 和一般軟體授權資訊匯入 Configuration Manager 站台資料庫的必要程序。 當您從授權聲明檔案將軟體授權資訊匯入站台資料庫時，站台伺服器電腦帳戶需具備 NTFS 檔案系統與用來匯入軟體授權資訊之檔案共用的 [完全控制]  權限。  

> [!IMPORTANT]  
>  將軟體授權資訊匯入站台資料庫時，即會覆寫現有的軟體授權資訊。 請確定您搭配 [匯入軟體授權精靈] 使用的軟體授權資訊檔案，其中包含所有必要軟體授權資訊的完整清單。  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>若要將軟體授權資訊匯入 Asset Intelligence 類別目錄  

1.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] 。  

2.  在 [首頁]  索引標籤的 [Asset Intelligence]  群組中，按一下 [匯入軟體授權] 。 隨即開啟 [匯入軟體授權精靈]。  

3.  在 [歡迎使用]  頁面，按 [下一步] 。  

4.  在 [匯入]  頁面上，指定要匯入 Microsoft 大量授權 (MVLS) 檔案 (.xml 或 .csv) 或一般授權聲明檔案 (.csv)。 如需建立一般授權聲明檔案的詳細資訊，請參閱本主題稍後的 [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) 。  

    > [!WARNING]  
    >  若要下載 .csv 格式的 MVLS 檔案，以匯入 Asset Intelligence 類別目錄，請參閱 [Microsoft 大量授權服務中心](http://go.microsoft.com/fwlink/p/?LinkId=226547)。 若要存取這項資訊，您必須在該網站上註冊帳戶。 如需如何取得 .xml 格式之 MVLS 檔案的相關資訊，請連絡您的 Microsoft 客戶代表。  

5.  輸入授權聲明檔案的 UNC 路徑，或按一下 [瀏覽]  以選取網路共用資料夾和檔案。  

    > [!NOTE]  
    >  您應妥善保護共用的資料夾，以防止授權資訊檔案受到未經授權的存取，且執行精靈之電腦的電腦帳戶必須擁有包含授權匯入檔案之共用的 [完全控制] 權限。  

6.  在 [摘要]  頁面上，確認已指定的資訊無誤再繼續進行。 若要進行任何變更，請按一下 [上一步]  回到 [匯入]  頁面。  

###  <a name="a-namebkmkcreategenerallicensestatementa-create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 您也可以手動建立以逗號分隔之檔案格式 (.csv) 的授權匯入檔案，將一般授權聲明匯入 Asset Intelligence 類別目錄中。  

> [!NOTE]  
>  雖然只有 [名稱] 、[發行者] 、[版本] 和 [EffectiveQuantity]  欄位必須包含資料，但授權匯入檔案第一個資料列上的所有欄位都必須輸入。 所有日期欄位應顯示為下列格式：月/日/年，例如 08/04/2008。  

 Asset Intelligence 會使用產品名稱和產品版本來比對您在一般授權聲明中指定的產品，而不是發行者名稱。 您在一般授權聲明中使用的產品名稱必須與儲存在站台資料庫中的產品名稱完全相符。 Asset Intelligence 會採用一般授權聲明中指定的 **EffectiveQuantity** 數目來和 Configuration Manager 清查中找到的安裝產品數目進行比較。  

> [!TIP]  
>  若要取得儲存在 Configuration Manager 站台資料庫中的完整產品名稱清單，您可以在站台資料庫上執行下列查詢：SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE。  

 您可以指定產品的正確版本，或指定部分版本，例如僅指定主要版本。 下列範例產生的版本結果符合特定產品之一般授權聲明的版本項目。  

|一般授權聲明項目|比對站台資料庫項目|  
|-------------------------------------|------------------------------------|  
|名稱："MySoftware"，ProductVersion0:"2"|ProductName0: "Mysoftware", ProductVersion0: "2.01.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.02.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.10.1234"|  
|名稱："MySoftware"，版本："2.05"|ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"|  
|名稱："MySoftware"，版本："2"<br /><br /> 名稱："MySoftware"，版本："2.05"|匯入期間發生錯誤。 若有多個項目符合相同的產品版本，則匯入會失敗。|  

 下列程序描述使用 Microsoft Excel 來建立一般授權聲明匯入檔案的程序。  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>若要使用 Microsoft Excel 建立一般授權聲明匯入檔案  

1.  開啟 Microsoft Excel，並建立新的試算表。  

2.  在新試算表的第一個資料列，輸入所有軟體授權資料欄位名稱。  

3.  在新試算表的第二個和後續資料列，輸入所需的軟體授權資訊。 請務必確認要匯入之每個軟體授權的所有必要軟體授權資料欄位，都有輸入後續資料列中。 試算表中輸入的軟體項目名稱，必須與執行硬體清查之後用戶端電腦的資源總管中顯示的軟體項目相同。  

4.  在 [檔案]  功能表上，按一下 [另存新檔] ，然後將檔案儲存成 .csv 格式。  

5.  將 .csv 檔案複製到用來將軟體授權資訊匯入 Asset Intelligence 類別目錄的檔案共用。  

6.  在 Configuration Manager 主控台中，使用 [匯入軟體授權精靈] 匯入新建立的 .csv 授權資訊檔案。  

7.  執行 Asset Intelligence **授權 15A - 協力廠商軟體對帳報告**，確認授權資訊已成功匯入 Asset Intelligence 類別目錄。  

> [!NOTE]  
>  如需可用於測試用途的一般軟體授權檔案的範例，請參閱 [Example Asset Intelligence general license import file in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md) (System Center Configuration Manager 中的 Asset Intelligence 一般授權匯入檔範例)。  

#### <a name="sample-table-to-describe-software-licenses"></a>描述軟體授權的範例資料表  
 當建立一般授權聲明匯入檔案時，下表的資訊可用來描述要匯入 Asset Intelligence 類別目錄的軟體授權。  

|欄名|資料類型|必要|範例|  
|-----------------|---------------|--------------|-------------|  
|Name|最多 255 個字元|是|軟體項目|  
|發行者|最多 255 個字元|是|軟體發行者|  
|版本|最多 255 個字元|是|軟體項目版本|  
|語言|最多 255 個字元|是|軟體項目語言|  
|EffectiveQuantity|整數值|是|購買的授權數量|  
|PONumber|最多 255 個字元|否|採購單資訊|  
|ResellerName|最多 255 個字元|否|轉銷商資訊|  
|DateOfPurchase|日期值，格式如下：MM/DD/YYYY|否|授權採購日期|  
|SupportPurchased|位元值|否|0 或 1：輸入 0 表示 Yes，輸入 1 表示 No|  
|SupportExpirationDate|日期值，格式如下：MM/DD/YYYY|否|購買支援的結束日期|  
|註解|最多 255 個字元|否|選擇性註解|  

###  <a name="a-namebkmkconfiguremaintenancetasksa-configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 下列為 Asset Intelligence 提供的維護工作：  

-   **使用清查資訊檢查應用程式標題**：此維護工作會檢查軟體清查中回報的軟體項目與 Asset Intelligence 類別目錄中的軟體項目是否一致。 預設會啟用這項工作並排程於星期六凌晨 12:00 之後、 上午 5:00 之前執行。 這項維護工作僅適用於 Configuration Manager 階層的頂層站台。  

-   **摘述已安裝的軟體資料**：此維護工作會提供在 [資產與相容性]  工作區 [Asset Intelligence]  節點下 [已清查的軟體]  節點中顯示的資訊。 執行工作時，Configuration Manager 會收集所有已清查的主要站台軟體項目計數。 預設會啟用這項工作並排程於每天凌晨 12:00 之後、 上午 5:00 之前執行。 這項維護工作僅適用於主要站台。  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>若要設定 Asset Intelligence 維護工作  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [網站] 。  

3.  選取要在其中設定 Asset Intelligence 維護工作的站台。  

    > [!NOTE]  
    >   **摘述已安裝的軟體資料** 只可用於主要站台維護工作。  

4.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [站台維護] 。 隨即出現所有可用的站台維護工作清單。  

5.  選取想要的維護工作，然後按一下 [編輯]  修改設定。  

6.  啟用和設定維護工作。 若要將站台作業的干擾降到最低，建議您將時段設為站台的離峰時間。 該時段即為可執行工作的時間間隔。 您可在 [工作內容]  對話方塊中以 [由此開始]  和 [最晚的開始時間]  來指定時段。  

    > [!WARNING]  
    >  您可以選取目前的日期，並將 [由此開始]  時間設為目前時間過後幾分鐘，以立即啟動工作。  

7.  按一下 [確定]  儲存設定。 現在，即會根據排程來執行工作。  

    > [!NOTE]  
    >  若第一次嘗試時無法執行工作，Configuration Manager 會嘗試重新執行工作直到工作執行成功，或直到可執行工作的時段已過為止。  



<!--HONumber=Nov16_HO1-->


