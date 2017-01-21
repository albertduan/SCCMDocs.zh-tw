---
title: "報表作業和維護 | Configuration Manager"
description: "了解 System Center Configuration Manager 中管理報告及報告訂閱的詳細資料。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2473aef3b5c9be51f45039735e975d1c0ca86277


---
# <a name="operations-and-maintenance-for-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的報告作業和維護

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中用於報告的基礎結構就緒後，您通常會執行一些作業來管理報告及報告訂閱。  

##  <a name="a-namebkmkmanagereportsa-manage-configuration-manager-reports"></a><a name="BKMK_ManageReports"></a> 管理 Configuration Manager 報告  
 Configuration Manager 提供超過 400 種預先定義的報告，可幫助您收集、組織及呈現有關組織內使用者、硬體和軟體清查、軟體更新、應用程式、站台狀態，以及其他 Configuration Manager 作業的資訊。 您可以依原樣使用預先定義的報告，也可以修改報告以因應您的需求。 您也可以建立自訂的模型式和 SQL 式報告，以因應您的需求。 下列各節可協助您規劃 Configuration Manager 報告。  

###  <a name="a-namebkmkrunreporta-run-a-configuration-manager-report"></a><a name="BKMK_RunReport"></a> 執行 Configuration Manager 報告  
 Configuration Manager 中的報表會儲存在 SQL Server Reporting Services，並從 Configuration Manager 站台資料庫擷取報表中轉譯的資料。 您可以存取在 Configuration Manager 主控台或使用報表管理員中，您在 web 瀏覽器來存取報表。 您可以在可存取執行 SQL Server Reporting Services 電腦的任何電腦上開啟報告，但是您必須有足夠的權限才能檢視報告。 當您執行報告時，報告標題、描述及類別會以本機作業系統的語言顯示。  

> [!NOTE]  
>  某些非英文語言的字元可能無法在報告中正確顯示。  在這種情況下，您可以使用 Web 架構的報表管理員或透過遠端系統管理員主控台來檢視報告。  

> [!WARNING]  
>  若要執行報告，您必須具有 [站台]  權限的 [讀取]  權限，以及針對特定物件設定的 [執行報告]  權限。  

> [!NOTE]  
>  報表管理員是 Web 式報告存取和管理工具，可透過 HTTP 連線用來管理遠端位置上的單一報表伺服器執行個體。 您可以使用報表管理員進行操作工作，例如檢視報告、修改報告內容，以及管理相關聯的報告訂閱。 本主題提供在報表管理員中檢視報告和修改報告內容的步驟，如需有關報表管理員所提供其他選項的詳細資訊，請參閱《SQL Server 2008 線上叢書》中的 [報表管理員](http://go.microsoft.com/fwlink/p/?LinkId=224916) 。  

 您可以使用下列程序來執行 Configuration Manager 報表。  

##### <a name="to-run-a-report-in-the-configuration-manager-console"></a>在 [組態管理員] 主控台中執行報表  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [報告] ，然後按一下 [報告]  列出可用的報告。  

    > [!IMPORTANT]  
    >  在這個版本的 Configuration Manager 中，[所有內容] 報告只會顯示套件，不會顯示應用程式。  

    > [!TIP]  
    >  如果未列出任何報告，請確認是否已安裝並設定 Reporting Services 點。 如需詳細資訊，請參閱[設定報告](configuring-reporting.md)。  

3.  選取您要執行的報告，然後在 [首頁]  索引標籤的 [報告群組]  區段中，按一下 [執行]  開啟報告。  

4.  如果有必要的參數，請指定參數，然後按一下 [檢視報告] 。  

#### <a name="to-run-a-report-in-a-web-browser"></a>若要在 Web 瀏覽器中執行報告  

1.  在 Web 瀏覽器中，輸入報表管理員的 URL，例如 **http:\/\/Server1\/Reports**。 您可以判斷報表管理員 URL 上 **報表管理員 URL** 頁面 Reporting Services 組態管理員中。  

2.  按一下報表管理員中的 Configuration Manager 報告資料夾，例如 **ConfigMgr\_CAS**。  

    > [!TIP]  
    >  如果未列出任何報告，請確認是否已安裝並設定 Reporting Services 點。 如需詳細資訊，請參閱[設定報告](configuring-reporting.md)。  

3.  按一下您要執行之報告的報告類別，然後按一下報告的連結。 報告會在報表管理員中開啟。  

4.  如果有必要的參數，請指定參數，然後按一下 [檢視報告] 。  

###  <a name="a-namebkmkmodifyreportpropertiesa-modify-the-properties-for-a-configuration-manager-report"></a><a name="BKMK_ModifyReportProperties"></a> 修改 Configuration Manager 報告的內容  
 您可以在 Configuration Manager 主控台中檢視報告的內容，例如報告名稱和描述，但是若要變更內容，請使用報表管理員。 利用下列程序修改 Configuration Manager 報告的內容。  

#### <a name="to-modify-report-properties-in-report-manager"></a>若要在報表管理員中修改報表內容  

1.  在 Web 瀏覽器中，輸入報表管理員的 URL，例如 **http:\/\/Server1\/Reports**。 您可以判斷報表管理員 URL 上 **報表管理員 URL** 頁面 Reporting Services 組態管理員中。  

2.  按一下報表管理員中的 Configuration Manager 報告資料夾，例如 **ConfigMgr\_CAS**。  

    > [!TIP]  
    >  如果未列出任何報告，請確認是否已安裝並設定 Reporting Services 點。 如需詳細資訊，請參閱[設定報告](configuring-reporting.md)。  

3.  按一下您要修改內容之報告的報告類別，然後按一下報告的連結。 報告會在報表管理員中開啟。  

4.  按一下 [內容]  索引標籤。 您可以修改報告名稱和描述。  

5.  完成時，按一下 [套用] 。 報告內容會儲存在報告伺服器上，而且 Configuration Manager 主控台會針對報告擷取更新的報告內容。  

###  <a name="a-namebkmkeditreporta-edit-a-configuration-manager-report"></a><a name="BKMK_EditReport"></a> 編輯 Configuration Manager 報告  
 當現有 Configuration Manager 報告未擷取必要的資訊，或未提供您需要的配置或設計時，您可以在報表產生器中編輯報告。  

> [!NOTE]  
>  您也可以選擇複製現有的報告，方法是開啟報告進行編輯，然後按一下 [另存新檔]  ，將它儲存成新的報告。  

> [!IMPORTANT]  
>  使用者帳戶必須具有 [站台修改]  權限，以及與您要修改之報告相關聯的特定物件上的 [修改報告]  權限。  

> [!IMPORTANT]  
>  當 Configuration Manager 升級為較新版本時，新報告會覆寫預先定義的報告。 如果您修改預先定義的報告，則必須先備份報告再安裝新版本，然後在 Reporting Services 中還原報告。 如果您要對預先定義的報告進行大幅變更，請考慮改為建立新報告。 您在升級站台之前建立的新報告不會被覆寫。  

 利用下列程序編輯 Configuration Manager 報告的內容。  

#### <a name="to-edit-report-properties"></a>若要編輯報告的內容  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [報告] ，然後按一下 [報告]  列出可用的報告。  

3.  選取您要修改的報告，然後在 [首頁]  索引標籤的 [報告群組]  區段中，按一下 [編輯] 。 出現提示時，輸入您的使用者名稱和密碼，然後按一下 [確定] 。 如果電腦上未安裝報告產生器，則會提示您進行安裝。 按一下 [執行]  安裝報告產生器，其為修改及建立報告時所需。  

4.  在報告產生器中，修改適當的報告設定，然後按一下 [儲存]  將報告儲存至報告伺服器。  

###  <a name="a-namebkmkcreatemodelbasedreporta-create-a-model-based-report"></a><a name="BKMK_CreateModelBasedReport"></a> 建立模型式報告  
 模型式報告可讓您以互動方式選取要包含在報告中的項目。 如需建立自訂報表模型的詳細資訊，請參閱[在 SQL Server Reporting Services 中建立 System Center Configuration Manager 的自訂報表模型](creating-custom-report-models-in-sql-server-reporting-services.md)。  

> [!IMPORTANT]  
>  使用者帳戶必須具有 [站台修改]  權限才能建立新報告。 使用者只能在使用者具有 [修改報告]  權限的資料夾中建立報告。  

 您可以使用下列程序建立模型式的 Configuration Manager 報表。  

#### <a name="to-create-a-model-based-report"></a>建立模型式報告  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [報告]  ，然後按一下 [報告] 。  

3.  在 [首頁]  索引標籤的 [建立]  區段中，按一下 [建立報告]  開啟 [建立報告精靈] 。  

4.  在 [資訊]  頁面上，進行下列設定：  

    -   **類型：** 選取 [模型式報告] ，使用 Reporting Services 模型在報表產生器中建立報告。  

    -   **名稱**：指定報告的名稱。  

    -   **描述**：指定報告的描述。  

    -   **伺服器**：顯示您要建立此報告所在的報告伺服器名稱。  

    -   **路徑**：按一下 [瀏覽]  指定您要儲存報告的資料夾。  

     按一下 [下一步] 。  

5.  在 [模式選擇]  頁面上，於清單中選取要用來建立此報告的可用模型。 當您選取報表模型時，[預覽]  區段會顯示所選取報表模型提供的 SQL Server 檢視和實體。  

6.  在 [摘要]  頁面上，檢閱設定。 按一下 [上一步] 變更設定，或按一下 [下一步] 在 Configuration Manager 中建立報告。  

7.  在 [確認]  頁面上，按一下 [關閉]  結束精靈，然後開啟報告產生器進行報告設定。 出現提示時，輸入您的使用者名稱和密碼，然後按一下 [確定] 。 如果電腦上未安裝報告產生器，則會提示您進行安裝。 按一下 [執行]  安裝報告產生器，其為修改及建立報告時所需。  

8.  在 Microsoft 報表產生器中，建立報告配置、在可用的 SQL Server 檢視中選取資料、新增參數至報告等。 如需有關使用報告產生器建立新報告的詳細資訊，請參閱&lt;報告產生器說明&gt;。  

9. 按一下 [執行]  執行報告。 確認報告提供您預期的資訊。 按一下 [設計]  返回 [設計] 檢視修改報告 (如有需要)。  

10. 按一下 [儲存]  將報告儲存至報告伺服器。 您可以在 [監視]  工作區的 [報告]  節點中，執行和修改新報告。  

###  <a name="a-namebkmkcreatesqlbasedreporta-create-a-sql-based-report"></a><a name="BKMK_CreateSQLBasedReport"></a> 建立 SQL 式報告  
 SQL 式報告可讓您擷取 Report SQL Statement 為基礎的資料。  

> [!IMPORTANT]  
>  當您為自訂報告建立 SQL 陳述式時，請不要直接參照 SQL Server 資料表。 請改為從站台資料庫參照 Reporting SQL Server 檢視 \(開頭為 v\_ 的檢視名稱\)。 您也可以從站台資料庫參考公開預存程序 \(開頭為 sp\_ 的預存程序名稱\)。  

> [!IMPORTANT]  
>  使用者帳戶必須具有 [站台修改]  權限才能建立新報告。 使用者只能在使用者具有 [修改報告]  權限的資料夾中建立報告。  

 您可以使用下列程序建立 SQL 式的 Configuration Manager 報表。  

#### <a name="to-create-a-sql-based-report"></a>建立 SQL 式報告  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [報告] ，然後按一下 [報告] 。  

3.  在 [首頁]  索引標籤的 [建立]  區段中，按一下 [建立報告]  開啟 [建立報告精靈] 。  

4.  在 [資訊]  頁面上，進行下列設定：  

    -   **類型**：選取 [SQL 式報告]，使用 SQL 陳述式在報表產生器中建立報告。  

    -   **名稱**：指定報告的名稱。  

    -   **描述**：指定報告的描述。  

    -   **伺服器**：顯示您要建立此報告所在的報告伺服器名稱。  

    -   **路徑**：按一下 [瀏覽]  指定您要儲存報告的資料夾。  

     按一下 [下一步] 。  

5.  在 [摘要]  頁面上，檢閱設定。 按一下 [上一步] 變更設定，或按一下 [下一步] 在 Configuration Manager 中建立報告。  

6.  在 [確認]  頁面上，按一下 [關閉]  結束精靈，然後開啟報告產生器進行報告設定。 出現提示時，輸入您的使用者名稱和密碼，然後按一下 [確定] 。 如果電腦上未安裝報告產生器，則會提示您進行安裝。 按一下 [執行]  安裝報告產生器，其為修改及建立報告時所需。  

7.  在 Microsoft 報表產生器中，為報告提供 SQL 陳述式或使用可用 SQL Server 檢視中的資料行建立 SQL 陳述式，新增參數至報告等。  

8.  按一下 [執行]  執行報告。 確認報告提供您預期的資訊。 按一下 [設計]  返回 [設計] 檢視修改報告 (如有需要)。  

9. 按一下 [儲存]  將報告儲存至報告伺服器。 您可以在 [監視]  工作區的 [報告]  節點中，執行新報告。  

##  <a name="a-namebkmkmanagereportsubscriptionsa-manage-report-subscriptions"></a><a name="BKMK_ManageReportSubscriptions"></a> 管理報告訂閱  
 SQL Server Reporting Services 中的報告訂閱可讓您設定以電子郵件自動傳遞指定的報告，或依排程的間隔傳遞至檔案共用。 使用 System Center 2012 Configuration Manager 中的 [建立訂閱精靈] 來設定報告訂閱。  

###  <a name="a-namebkmkreportsubscriptionfilesharea-create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a><a name="BKMK_ReportSubscriptionFileShare"></a> 建立報告訂閱，將報告傳遞至檔案共用  
 當您建立報告訂閱將報告傳遞至檔案共用時，報告會以指定的格式複製到您指定的檔案共用。 您一次只能訂閱和要求傳遞一份報告。  

 與報告伺服器所裝載和管理的報告不同的是，傳遞至共用資料夾的報告為靜態檔案。 針對報告定義的互動功能對於做為檔案儲存在檔案系統上的報告沒有作用。 互動功能會做為靜態項目呈現。 如果報告包含圖表，則會使用預設呈現方式。 如果報告連結至另一個報告，連結會轉譯為靜態文字。 如果您要在傳遞的報告中保留互動功能，請改用電子郵件傳遞。 如需電子郵件傳遞的詳細資訊，請參閱本主題稍後的 [建立報告訂閱以使用電子郵件傳遞報告](#BKMK_ReportSubscriptionEmail) 章節。  

 當您建立使用檔案共用傳遞的訂閱時，必須指定現有資料夾做為目的地資料夾。 報告伺服器不會在檔案系統上建立資料夾。 您建立的資料夾必須可透過網路連線存取。 您在訂閱中指定目的地資料夾時，請使用 UNC 路徑，而且不要包含資料夾路徑中的結尾反斜線。 例如，目的地資料夾的有效 UNC 路徑為：\\\\&lt;伺服器名稱\>\\reportfiles\\operations\\2011。  

 報告可用各種不同的檔案格式呈現，例如 MHTML 或 Excel。 若要以特定檔案格式儲存報告，請在建立訂閱時選取轉譯格式。 例如，選擇 Excel 會將報告儲存為 Microsoft Excel 檔。 雖然您可以選取任何支援的轉譯格式，但是有些格式在轉譯為檔案時，會比其他格式效果更好。  

 利用下列程序建立報告訂閱將報告傳遞至檔案共用。  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>若要建立報告訂閱將報告傳遞至檔案共用  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [報告]  ，然後按一下 [報告]  列出可用的報告。 您可以選取報告資料夾，僅列出與該資料夾相關聯的報告。  

3.  選取您要新增至訂閱的報告，然後在 [首頁]  索引標籤的 [報告群組]  區段中，按一下 [建立訂閱]  開啟 [建立訂閱精靈] 。  

4.  在 [訂閱傳遞]  頁面上，進行下列設定：  

    -   報告傳遞者：選取 [Windows 檔案共用]  將報告傳遞至檔案共用。  

    -   **檔案名稱**：指定報告的檔案名稱。 根據預設，報告檔案不會包含副檔名。 選取 [建立時新增副檔名]  ，根據轉譯格式自動新增此報告的副檔名。  

    -   **路徑**：指定您要傳遞這份報告的目標現有資料夾 UNC 路徑 \(例如 \\\\&lt;伺服器名稱\>\\&lt;伺服器共用\>\\&lt;報告資料夾\>\)。  

        > [!NOTE]  
        >  稍後在此頁面上指定的使用者名稱必須可存取此伺服器共用，而且具有目的地資料夾的「寫入」權限。  

    -   **轉譯格式**：為報告檔案選取下列其中一種格式：  

        -   **包含報告資料的 XML 檔案**：以可延伸標記語言格式儲存報告。  

        -   **CSV \(逗號分隔\)**：以逗號分隔值格式儲存報告。  

        -   **TIFF 檔案**：以標記的影像檔案格式儲存報告。  

        -   **Acrobat \(PDF\) 檔案**：以 Acrobat 可攜式文件格式儲存報告。  

        -   **HTML 4.0**：將報告儲存為只能在支援 HTML 4.0 的瀏覽器中檢視的網頁。 Internet Explorer 5 和更新版本都支援 HTML 4.0。  

            > [!NOTE]  
            >  如果您的報告中包含影像，HTML 4.0 格式不會將影像納入檔案中。  

        -   **MHTML \(網頁封存\)**：以 MIME HTML 格式 \(mhtml\) 儲存報告，此格式可於多種 Web 瀏覽器中檢視。  

        -   **RPL 轉譯器**：以報告頁面配置 \(RPL\) 格式儲存報告。  

        -   **Excel**：將報告儲存為 Microsoft Excel 試算表。  

        -   **Word**：將報告儲存為 Microsoft Word 文件。  

    -   **使用者名稱**：指定具有目的地伺服器共用和資料夾之存取權限的 Windows 使用者帳戶。 使用者帳戶必須能夠存取此伺服器共用，且具有目的地資料夾的「寫入」權限。  

    -   **密碼**：指定 Windows 使用者帳戶的密碼。 在 [確認密碼] 中，再次輸入密碼。  

    -   選取下列其中一個選項，設定目的地資料夾中存在相同名稱的檔案時的行為：  

        -   **使用較新的版本覆寫現有的檔案**：指定報告檔案已存在時，新版本覆寫該檔案。  

        -   **不覆寫現有的檔案**：指定報告檔案已存在時，不採取任何動作。  

        -   **加入較新的版本時，遞增檔案名稱**：指定報告檔案已存在時，新報告的檔案名稱會新增一個號碼，以便與其他版本作區分。  

    -   **描述**：指定報告訂閱的描述。  

     按一下 [   

5.  在 [訂閱排程]  頁面上，為報告訂閱選取下列其中一個傳遞排程選項：  

    -   **使用共用排程**：共用排程是之前定義的排程，可供其他報告訂閱使用。 選取此核取方塊，然後選取清單中的共用排程 (如果已有指定的排程)。  

    -   **建立新排程**：設定此報告執行的排程，包括此訂閱的間隔、開始時間和日期，以及結束日期。  

6.  在 [訂閱參數]  頁面，指定自動執行此報告時使用的參數。 如果報告沒有參數，則不會顯示此頁面。  

7.  在 [摘要]  頁面上檢閱報告訂閱設定。 按一下 [上一步]  變更設定，或按 [下一步]  建立報告訂閱。  

8.  在 [完成]  頁面上，按一下 [關閉]  結束精靈。 確認報告訂閱已成功建立。 您可以在 [監視]  工作區的 [報告]  下，於 [訂閱]  節點中檢視及修改告訂閱。  

###  <a name="a-namebkmkreportsubscriptionemaila-create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="BKMK_ReportSubscriptionEmail"></a> 建立報告訂閱以使用電子郵件傳遞報告  
 當您建立報告訂閱使用電子郵件傳遞報告時，電子郵件會傳送至您設定的收件者，而報告會做為附件包含在其中。 報告伺服器不會驗證電子郵件地址，或是從電子郵件伺服器取得電子郵件地址。 您必須事先得知要使用的電子郵件地址。 根據預設，您可以用電子郵件將報告寄給組織內外任何有效的電子郵件帳戶。 您可以選取下列其中一個電子郵件傳遞選項，或兩個都選取：  

-   傳送通知及所產生報告的超連結。  

-   傳送內嵌或附加的報告。 轉譯格式和瀏覽器會決定報告為內嵌或附加。 如果您的瀏覽器支援 HTML 4.0 和 MHTML，而且您選取 MHTML \(網頁封存\) 轉譯格式，則報告會內嵌為訊息的一部分。 所有其他轉譯格式 \(CSV、PDF、Word 等\) 都會將報告作為附件傳遞。 Reporting Services 不會在傳送報告之前檢查附件或訊息的大小。 如果附件或訊息超過電子郵件伺服器允許的上限，報告就不會傳遞。  

> [!IMPORTANT]  
>  您必須在 Reporting Services 中設定電子郵件設定，才能使用 [電子郵件]  傳遞選項。 如需有關在 Reporting Services 中設定電子郵件設定的詳細資訊，請參閱《SQL Server 線上叢書》中的 [設定報表伺服器的電子郵件傳遞](http://go.microsoft.com/fwlink/p/?LinkId=226668) 。  

 利用下列程序建立報告訂閱使用電子郵件傳遞報告。  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-by-email"></a>若要建立報告訂閱使用電子郵件傳遞報告  

-   在 Configuration Manager 主控台中，按一下 [監視] 。  

-   在 [監視]  工作區中，展開 [報告]  ，然後按一下 [報告]  列出可用的報告。 您可以選取報告資料夾，僅列出與該資料夾相關聯的報告。  

-   選取您要新增至訂閱的報告，然後在 [首頁]  索引標籤的 [報告群組]  區段中，按一下 [建立訂閱]  開啟 [建立訂閱精靈] 。  

-   在 [訂閱傳遞]  頁面上，進行下列設定：  

    -   **報告傳遞者**：選取 [電子郵件] 將報告作為電子郵件訊息中的附件傳遞。  

    -   **收件者**：指定要傳送此報告的有效目標電子郵件地址。  

        > [!NOTE]  
        >  您可以輸入多個電子郵件收件者，並以分號分隔每個電子郵件地址。  

    -   **副本**：選擇性地指定要複製此報告的目標電子郵件地址。  

    -   **密件副本**：選擇性地指定要傳送匿名報告副本的目標電子郵件地址。  

    -   **回覆**：指定收件者回覆電子郵件訊息時使用的回覆地址。  

    -   **主旨**：指定訂閱電子郵件地址的主旨列。  

    -   **優先順序**：選取此電子郵件訊息的優先順序旗標。 選取 [低] 、[普通] 或 [高] 。 Microsoft Exchange 會使用優先順序設定來設定旗標，表示電子郵件訊息的重要性。  

    -   **註解**：指定要新增至訂閱電子郵件訊息本文的文字。  

    -   **描述**：指定此報告訂閱的描述。  

    -   **包含連結**：在電子郵件訊息的本文中包含所訂閱報告的 URL。  

    -   **包含報告**：指定將報告附加至電子郵件訊息。 附加報告所採用的格式是在 [轉譯格式]  清單中指定。  

    -   **轉譯格式**：為附加的報告選取下列其中一種格式：  

        -   **包含報告資料的 XML 檔案**：以可延伸標記語言格式儲存報告。  

        -   **CSV \(逗號分隔\)**：以逗號分隔值格式儲存報告。  

        -   **TIFF 檔案**：以標記的影像檔案格式儲存報告。  

        -   **Acrobat \(PDF\) 檔案**：以 Acrobat 可攜式文件格式儲存報告。  

        -   **MHTML \(網頁封存\)**：以 MIME HTML 格式 \(mhtml\) 儲存報告，此格式可於多種 Web 瀏覽器中檢視。  

        -   **Excel**：將報告儲存為 Microsoft Excel 試算表。  

        -   **Word**：將報告儲存為 Microsoft Word 文件。  

-   在 [訂閱排程]  頁面上，為報告訂閱選取下列其中一個傳遞排程選項：  

    -   **使用共用排程**：共用排程是之前定義的排程，可供其他報告訂閱使用。 選取此核取方塊，然後選取清單中的共用排程 (如果已有指定的排程)。  

    -   **建立新排程**：設定此報告將執行的排程，包括此訂閱的間隔、開始時間和日期，以及結束日期。  

-   在 [訂閱參數]  頁面，指定自動執行此報告時使用的參數。 如果報告沒有參數，則不會顯示此頁面。  

-   在 [摘要]  頁面上檢閱報告訂閱設定。 按一下 [上一步]  變更設定，或按 [下一步]  建立報告訂閱。  

-   在 [完成]  頁面上，按一下 [關閉]  結束精靈。 確認報告訂閱已成功建立。 您可以在 [監視]  工作區的 [報告]  下，於 [訂閱]  節點中檢視及修改告訂閱。  



<!--HONumber=Nov16_HO1-->


