---
title: "版本資訊 - Configuration Manager | Microsoft Docs"
description: "請參閱這些注意事項，以了解產品中尚未修正或 Microsoft 知識庫文章未涵蓋的緊急問題。"
ms.custom: na
ms.date: 08/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 24f30bddb345e3a08d4b655d89693c226005cb0e
ms.sourcegitcommit: 06aef618f72c700f8a716a43fb8eedf97c62a72b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2017
---
# <a name="release-notes-for-system-center-configuration-manager"></a>System Center Configuration Manager 的版本資訊

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 的產品版本資訊僅限於產品中尚未修正的緊急問題 (可透過主控台內更新)，或 Microsoft 知識庫文章中未詳述的緊急問題。  

 對於影響核心案例的已知問題，此資訊顯示於 System Center Configuration Manager 文件庫中的線上產品文件中。  

> [!TIP]  
>  本主題包含 System Center Configuration Manager 最新分支的版本資訊。 對於 System Center Configuration Manager Technical Preview 版本，請參閱 [System Center Configuration Manager 的 Technical Preview](../../../../core/get-started/technical-preview.md)。  

## <a name="setup-and-upgrade"></a>安裝與升級  

### <a name="after-you-update-a-configuration-manager-console-using-consolesetupexe-from-the-site-server-folder-recent-language-pack-changes-are-not-available"></a>使用站台伺服器資料夾中的 ConsoleSetup.exe 更新 Configuration Manager 主控台之後，無法使用最近的語言套件變更
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
使用站台伺服器安裝資料夾中的 ConsoleSetup.exe 就地更新主控台之後，可能無法使用最近安裝的語言套件。 這會在下列情況下發生：
- 您的站台是執行 1610 或 1702 版。
- 主控台是使用站台伺服器安裝資料夾中的 ConsoleSetup.exe 進行就地更新。

當發生此問題時，重新安裝的主控台不會使用所設定的最新語言套件組。 不會傳回錯誤，但主控台可以使用的語言套件將不會變更。  

**因應措施︰**將目前的主控台解除安裝，然後將主控台以全新安裝的方式重新安裝。 您可以使用站台伺服器安裝資料夾中的 ConsoleSetup.exe。 在安裝期間，請務必選取您要使用的語言套件檔。


### <a name="with-version-1702-the-default-site-boundary-group-is-configured-for-use-for-site-assignment"></a>在 1702 版中，預設的站台界限群組已設定為用於站台指派
<!--  SMS 486380   Applicability should only be to 1702. -->
在 1702 版中，預設站台界限群組的 [參考] 索引標籤上有 [使用此界限群組進行站台指派] 核取方塊 (會將站台列為「指派的站台」)，且該核取方塊會呈現灰色，讓使用者無法編輯或移除該設定。

**因應措施：**無。 您可以忽略此設定。 雖然該群組已針對站台指派啟用，但預設的站台界限群組不會用於站台指派。 在 1702 版中，此設定可確保預設的站台界限群組會和正確的站台相關聯。



### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>安裝使用 1606 版的長期維護分支站台時，會安裝最新分支站台
<!-- Consider move to core content  -->
當您使用 2016 年 10 月發行版的 1606 版基準媒體安裝長期維護分支 (LTSB) 站台時，安裝程式會改為安裝最新分支站台。 發生原因是未選取使用站台安裝來安裝服務連接點的選項。

 - 雖然不需要服務連接點，但是您必須在安裝程式期間選擇安裝它，才能安裝 LTSB 站台。

安裝程式完成之後，您可以解除安裝服務連接點。  不過，您必須擁有離線或線上模式的服務連接點才能提交遙測資料，並取得最新分支和 LTSB 站台的安全性更新。

如果您的站台安裝為最新分支站台，但您想要安裝 LTSB，則可以將站台解除安裝後，再重新安裝。 或者，您可以呼叫 [Microsoft 說明及支援](http://go.microsoft.com/fwlink/?LinkId=243064)以取得協助。  

若要確認安裝的分支，請在主控台的 [系統管理] > [站台設定] > [站台]，然後開啟 [階層設定]。 只有在站台執行 LTSB 時，才能使用將站台轉換為最新分支站台的選項。  

**因應措施：** 無。   


### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>在 Configuration Manager 主控台 [更新與服務] 節點中，更新卡在「正在下載」狀態  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
由線上服務連接點自動下載更新期間，更新可能會卡在「正在下載」狀態。 當更新下載卡住時，指示記錄檔中會顯示以下類似項目：  

DMPdownloader log：  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log：  

-   Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**因應措施**︰在站台伺服器上，修改下列登錄機碼以符合下列各項，然後重新啟動 SMS_Executive 服務，或等待下一個自動下載週期 (最多 24 小時)。  

-   **要編輯的機碼**：HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **狀態值**︰設定為 **146944** (十進位) 或 **0x00023e00** (十六進位)  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>使用來自 CD.Latest 資料夾的可轉散發檔案時，安裝程式會失敗，並顯示資訊清單驗證錯誤
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

當您透過為 1606 版建立的 CD.Latest 資料夾執行安裝程式，並使用 CD.Latest 資料夾隨附的可轉散發檔案時，安裝程式會失敗，而 Configuration Manager 安裝記錄檔中的錯誤如下︰

  - 錯誤：defaultcategories.dll 的檔案雜湊檢查失敗
  - 錯誤：資訊清單驗證失敗。 資訊清單版本有誤？

**因應措施：**請使用下列其中一種方法：
 - 在安裝期間，選擇從 Microsoft 下載最新的可轉散發檔案，而不使用 CD.Latest 資料夾隨附的可轉散發檔案。
 - 手動刪除 *cd.latest\redist\languagepack\zhh* 資料夾，然後再次執行安裝程式。


### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>服務連接工具在 SQL Server 位於遠端或停用共用記憶體時擲回例外狀況
<!-- 479223   Fixed in 1702 and later   -->
從 1606 版開始，服務連接工具會在下列其中一項正確時產生例外狀況：  
 -  站台資料庫位於裝載服務連接點並使用非標準連接埠 (1433 以外的連接埠) 之電腦的遠端
 -  站台資料庫位於與服務連接點相同的伺服器上，但已停用 SQL 通訊協定**共用記憶體**

例外狀況與下列類似：
 - 未處理的例外狀況: System.Data.SqlClient.SqlException: 建立連接至 SQL Server 時，發生網路相關或執行個體特定的錯誤。找不到或無法存取伺服器。確認執行個體名稱是否正確，以及 SQL Server 是否設定為允許遠端連線。(提供者: 具名管道提供者，錯誤: 40 - 無法開啟 SQL Server 連線) --

**因應措施**︰使用工具期間，您必須修改裝載服務連接點之伺服器的登錄，以包含 SQL Server 連接埠的相關資訊︰

   1.   使用工具之前，請編輯下列登錄機碼，並將使用中連接埠號碼新增至 SQL Server 名稱︰
    - 機碼：HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - 值：&lt;SQL Server 名稱>
    - 新增：**,&lt;連接埠>**

    例如，若要將連接埠 *15001* 新增至名為 *testserver.test.net* 的伺服器，則產生的機碼會是：***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.   將連接埠新增至登錄之後，工具應該會正常運作。  

   3.   完成工具的使用之後，針對 **-connect** 和 **-import** 步驟，請將登錄機碼變更回原始值。  


<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>用戶端部署和升級  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>用戶端安裝失敗並顯示錯誤碼 0x8007064c
<!--- SMS 486973 -->
當您將用戶端部署至 Windows 電腦時，安裝失敗。 ccmsetup.log 檔案會包含以下項目：「檔案 'C:\WINDOWS\ccmsetup\Silverlight.exe' 傳回失敗，結束代碼 1612。 安裝失敗」，並接著顯示：「InstallFromManifest 已失敗 0x8007064c」。

**因應措施：**這是由先前已安裝且已損毀的 Silverlight 版本所造成。 您可以嘗試在受影響的電腦上執行下列工具來修正此問題：[https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>作業系統部署  

### <a name="if-the-boot-image-contains-drivers-the-image-fails-to-reload-the-current-windows-pe-version-from-the-windows-assessment-and-deployment-kit-adk"></a>若開機映像包含驅動程式，映像無法從 Windows 評定及部署套件 (ADK) 重新載入目前的 Windows PE 版本
<!-- 495087 -->
您可以使用「更新發佈點精靈」，以使用最新版本 Windows PE (位於 Windows 評定及部署套件 (ADK) 的安裝目錄) 儲存之開機映像更新發佈點。 若要更新，請開啟「更新發佈點精靈」並選取 [從 Windows ADK 重新載入具備目前 PE 版本的此開機映像]。

然而，若您的開機映像包含驅動程式，則更新會失敗。 此時精靈會從 ADK 重新載入映像、顯示使用者可以關閉的例外狀況對話方塊，然後顯示成功畫面。 然而，最新的 Configuration Manager 用戶端元件將無法新增到開機映像中。 將不會更新發佈點上的開機映像

**因應措施**：執行兩次「更新發佈點精靈」。

1. 執行精靈並選取 [從 Windows ADK 重新載入具備目前 Windows PE 版本的此開機映像]。 這樣將會取得最新的 Windows PE 版本。
2. 重新執行精靈，但這次不要選取 [從 Windows ADK 重新載入具備目前 Windows PE 版本的此開機映像]。 這樣將會取得最新的用戶端二進位檔案，並更新發佈點上的開機映像。

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>根據預設，服務計劃會建立大量重複的軟體更新群組和部署  
根據預設，「建立服務計劃」精靈目前會在每個軟體更新同步處理後執行。 每次執行精靈時，它會建立新的軟體更新群組和部署。 例如，如果您的軟體更新同步處理排程一天會執行多次，「建立服務計劃」精靈每天將會建立多個幾乎相同的軟體更新群組和部署。  

**因應措施**：    
在您建立服務計劃後，開啟服務計劃的屬性，移至 **[評估排程]** 索引標籤，選取 **[依排程執行規則]**，按一下 **[自訂]**並建立自訂排程。 例如，您可以每隔 60 天執行服務計劃。  


### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>向使用者顯示高風險部署對話方塊時，就不會顯示期限較早的後續高風險對話方塊。
<!-- Fixed in 1702 and later -->
建立高風險工作部署並將其部署給使用者之後，會向使用者顯示高風險對話方塊。 如果使用者未關閉對話方塊，您可以建立和部署期限比第一個高風險部署還要早的另一個高風險部署，除非使用者關閉原始對話方塊，否則他們接收不到更新的對話方塊。 在設定的期限，仍會執行部署。

**因應措施**：  
使用者必須關閉第一個高風險部署的對話方塊，才能查看下一個高風險部署的對話方塊。



## <a name="software-updates"></a>軟體更新

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>當設定檔包含不支援的語言時，從該設定檔匯入 Office 365 用戶端設定會失敗
<!-- 489258  Fixed in 1706  -->
當您從現有的 XML 設定檔匯入 Office 365 用戶端設定，且該檔案包含 Office 365 專業增強版用戶端不支援的語言時，將會發生錯誤。 如需詳細資料，請參閱[從 Office 365 用戶端管理儀表板將 Office 365 應用程式部署至用戶端](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard)。

**因應措施**：    
在 XML 設定檔中只使用 [Office 365 專業增強版用戶端所支援的語言](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx)。  



## <a name="mobile-device-management"></a>行動裝置管理  

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>完整抹除會停用 RAM 小於 4 GB 的 Windows 10 裝置
在 RAM 小於 4 GB 的 Windows 10 RTM 裝置 (1511 前的版本) 上執行完整抹除，會導致裝置無法使用。 嘗試抹除裝置後，裝置無法啟動且停止回應。

**因應措施**︰請先確定 Windows 10 RTM 電腦至少有 4 GB 的 RAM 可用，再對裝置執行完整抹除。 若要檢視 Windows 10 裝置的版本號碼，請在命令提示字元中輸入 'winver'。 如果裝置已抹除且不再回應，請使用可開機的 Windows 10 USB 磁碟機啟動並復原裝置的存取。


### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>當使用者屬於兩個或多個部署了條款與條件原則的使用者集合時，使用者會看到多組相同的條款  
<!-- 454394    -->
當系統管理員將一組條款部署到多個使用者集合，而某個使用者是多個這些集合的成員時，該使用者在開啟公司入口網站時就會看到多個相同的條款複本。  例如，如果使用者 SampleUser 是 CompanyEmployeesFTE 和 CompanyEmployeesNA 這兩個不同使用者集合的成員，且 CompanyEmployeesFTE 和 CompanyEmployeesNA 都部署了 CompanyTerms 條款與條件，則 SampleUser 在條款接受頁面上就會看到兩組相同的 CompanyTerms。 因為使用者只能接受或拒絕全部條款，所以不可能出現使用者這邊接受條款、那邊拒絕條款的這種模稜兩可的接受狀態。 條款和條件接受報表中，每位使用者的每組條款都只有一個資料列，因此報表中沒有任何錯誤。 唯一的影響是使用者會在接受頁面上看到兩組條款。  

**因應措施**：請確定每位使用者只包含在一個部署了條款的集合中。  


### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>使用憑證驗證的 Android for Work 電子郵件設定檔不會套用到裝置
<!--  487657      -->
建立 Android for Work 電子郵件設定檔之後，有兩種驗證選項。 一種是使用者名稱和密碼，另外一種是憑證。 憑證選項目前沒有作用。 如果建立設定檔時將驗證方法設為 [憑證]，則設定檔不會套用到裝置，且系統會要求使用者手動輸入電子郵件帳戶詳細資料。

**因應措施**：無。 系統管理員必須使用 [使用者名稱和密碼] 選項，否則只能等到此問題解決為止。



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->


## <a name="endpoint-protection"></a>Endpoint Protection

### <a name="antimalware-policy-fails-to-apply-on-windows-server-2016-core"></a>反惡意程式碼原則無法套用至 Windows Server 2016 Core
<!--  Product Studio bug 485370 added 04 19 2017   Fixed in 1702 -->
反惡意程式碼原則無法套用至 Windows Server 2016 Core。  錯誤碼為 0x80070002。  ConfigSecurityPolicy.exe 遺失相依性。

**因應措施：**此問題已由在 2017 年 5 月 9 日發佈的[知識庫文章 4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) 解決。


### <a name="windows-defender-advanced-threat-protection-policies-fail-on-older-client-agents"></a>Windows Defender 進階威脅防護原則在較舊版本的用戶端代理程式上會發生失敗
<!-- Product Studio bug 462286 added  05 25 2017 and valid until July 2017 GA release      Fixed in 1610 -->
從 Configuration Manager 1610 版或更新版本的站台伺服器所建立的 Windows Defender 進階威脅防護原則，無法套用至 Configuration Manager 1606 版和較舊版本的用戶端上。  用戶端不會上線，且原則評估會回報錯誤。 Windows Defender 進階威脅防護設定中的 [部署狀態] 會顯示 [錯誤]。

**因應措施**：將 Configuration Manager 用戶端升級至 1610 版或更新版本。
