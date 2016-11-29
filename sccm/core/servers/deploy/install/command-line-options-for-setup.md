---
title: "安裝程式命令列選項 | System Center Configuration Manager"
description: "使用本文的資訊設定指令碼，或從命令列安裝 System Center Configuration Manager。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7d1f55786a42650395fcb66ee4917434feecb630

---
# <a name="command-line-options-for-setup-for-system-center-configuration-manager"></a>System Center Configuration Manager 的安裝程式命令列選項

*適用對象：System Center Configuration Manager (最新分支)*


 設定指令碼或從命令列安裝 System Center Configuration Manager 時，請使用下表中的資訊。  

##  <a name="a-namebkmksetupa-command-line-options-for-setup"></a><a name="bkmk_setup"></a> 安裝程式的命令列選項  
 **/DEINSTALL**  
 解除安裝網站。 您必須從網站伺服器電腦執行安裝程式。  

 **/DONTSTARTSITECOMP**  
 安裝網站，但可預防啟動網站元件管理員服務。 在啟動網站元件管理員服務之前，網站不會作用。 網站元件管理員負責安裝與啟動 SMS_Executive 服務，以及網站的其他處理程序。 在完成網站安裝後，當您啟動網站元件管理員服務時，便會安裝 SMS_Executive 以及其他網站運作所需的處理程序。  

 **/HIDDEN**  
 在安裝期間隱藏使用者介面。 此選項必須與 **/SCRIPT** 選項一起使用，且自動執行的指令碼檔必須提供所有必要選項，否則安裝程式會失敗。  

 **/NOUSERINPUT**  
 在安裝期間停用使用者輸入，但可顯示 [安裝精靈]  介面。 此選項必須與 **/SCRIPT** 選項一起使用，且自動執行的指令碼檔必須提供所有必要選項，否則安裝程式會失敗。  

 **/RESETSITE**  
 執行網站重設，其會重新設定網站的資料庫與服務帳戶。 您必須從站台伺服器上的 **&lt;Configuration Manager 安裝路徑\>\BIN\X64** 執行安裝程式。 如需網站重設的詳細資訊，請參閱 [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md) (修改 System Center Configuration Manager 基礎結構) 主題中的 [Run a site reset](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) (執行站台重設) 一節。  

 **/TESTDBUPGRADE &lt;執行個體名稱\資料庫名稱**>**  
 在網站資料庫備份上執行測試以確定可以升級。 您必須提供網站資料庫的執行個體名稱及資料庫名稱。 如果只指定資料庫名稱，則安裝程式會使用預設的執行個體名稱。  

> [!IMPORTANT]  
>  不支援在生產網站資料庫上執行此命令列選項。 在網站資料庫上進行這類升級可能會造成網站無法運作。  

 **/UPGRADE**  
 執行站台的自動升級。 當使用 /UPGRADE 時，您也必須指定產品金鑰，包括破折號 (-)。 此外，您必須指定先前下載的安裝程式必要條件檔案的路徑。  

 範例：**setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx &lt;外部元件檔案路徑\>**  

 如需安裝程式必要條件檔案的詳細資訊，請參閱本主題中的  [安裝程式下載程式](#bkmk_SetupDownloader) 。  

 **/SCRIPT &lt;安裝指令碼路徑**>**  
 執行自動安裝。當您使用 **/SCRIPT** 選項時，需要安裝程式初始設定檔案。 如需如何自動執行安裝程式的詳細資訊，請參閱[使用命令列安裝站台](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)。  

 **/SDKINST &lt;*FQDN*>**  
 在指定的電腦上安裝 SMS 提供者。 您必須提供 SMS 提供者電腦的 FQDN。 如需 SMS 提供者的詳細資訊，請參閱 [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (規劃 System Center Configuration Manager 的 SMS 提供者)。  

 **/SDKDEINST &lt;*FQDN*>**  
 在指定的電腦上解除安裝 SMS 提供者。 您必須提供 SMS 提供者電腦的 FQDN。  

 **/MANAGELANGS &lt;語言指令碼路徑**>**  
 管理原安裝網站所安裝的語言。若要使用此選項，您必須從站台伺服器上的 **&lt;Configuration Manager 安裝路徑\>\BIN\X64** 執行安裝程式，並提供包含語言設定的語言指令碼檔案位置。 如需語言安裝指令碼檔中可用語言選項的詳細資訊，請參閱本主題中的 [用以管理語言的命令列選項](#bkmk_Lang) 。  

##  <a name="a-namebkmklanga-command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a> 用以管理語言的命令列選項  
 **識別**  

-   **索引鍵名稱：** Action  

    -   **必要︰** 是  

    -   **值：**ManageLanguages  

    -   **詳細資料：**管理站台的伺服器、用戶端及行動用戶端語言支援。  

**選項**  

-   **索引鍵名稱：**AddServerLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**指定可用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的伺服器語言。 依預設使用英文版。  

-   **索引鍵名稱：**AddClientLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**指定將可用於用戶端電腦的語言。 依預設使用英文版。  

-   **索引鍵名稱：**DeleteServerLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**指定將移除且無法再用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的語言。 預設使用英文，無法移除。  

-   **索引鍵名稱：**DeleteClientLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**指定移除用戶端電腦不再使用的語言。 預設使用英文，無法移除。  

-   **索引鍵名稱：**MobileDeviceLanguage  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定是否安裝行動裝置用戶端語言。  

-   **索引鍵名稱︰**PrerequisiteComp  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 下載  

         1 = 已下載  

    -   **詳細資料：** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 0 值，安裝程式會下載檔案。  

-   **索引鍵名稱︰**PrerequisitePath  

    -   **必要︰** 是  

    -   **值：** &lt;安裝路必要條件檔案>  

    -   **詳細資料：** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑儲存下載的檔案或尋找之前下載的檔案。  

##  <a name="a-namebkmkunattendeda-unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a> 自動安裝程式指令碼檔索引鍵  
 使用以下各節有助於建立自動安裝的指令碼。 下表列出可用的安裝指令碼索引鍵、其對應的值、是否為必要、用於何種安裝類型，以及該索引鍵的簡單說明。  

### <a name="unattended-install-for-a-central-administration-site"></a>管理中心網站的自動安裝  
 使用以下詳細資料，透過使用自動安裝指令碼檔案來安裝管理中心網站。  

**識別**  

-   **索引鍵名稱：** Action  

    -   **必要︰** 是  

    -   **值︰**InstallCAS  

    -   **詳細資料：**安裝管理中心網站。  

**選項**  

-   **索引鍵名稱︰**ProductID  

    -   **必要︰** 是  

    -   **值：***xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* 或 *Eval*  

    -   **詳細資料：**指定 Configuration Manager 安裝產品金鑰，含破折號。 輸入 **Eval** 安裝 Configuration Manager 評估版。  

-   **索引鍵名稱：**SiteCode  

    -   **必要︰** 是  

    -   **值︰**&lt;站台碼>  

    -   **詳細資料：**指定可特別識別出階層中站台的三個英數字元。  

-   **索引鍵名稱：**SiteName  

    -   **必要︰** 是  

    -   **值：** &lt;站台名稱>  

    -   **詳細資料：**指定此站台的名稱。  

-   **索引鍵名稱：**SMSInstallDir  

    -   **必要︰** 是  

    -   **值︰**Configuration Manager 安裝路徑  

    -   **詳細資料：**指定 Configuration Manager 程式檔案的安裝資料夾。  

-   **索引鍵名稱：**SDKServer  

    -   **必要︰** 是  

    -   **值：**&lt;SMS 提供者的FQDN>  

    -   **詳細資料：** 指定將裝載 SMS 提供者的伺服器 FQDN。  
        您可以在初始安裝後設定站台的其他 SMS 提供者。  

-   **索引鍵名稱︰**PrerequisiteComp  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 下載  

         1 = 已下載  

    -   **詳細資料：** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 0 值，安裝程式會下載檔案。  

-   **索引鍵名稱︰**PrerequisitePath  

    -   **必要︰** 是  

    -   **值：** &lt;安裝路必要條件檔案>  

    -   **詳細資料：** 指定安裝程式必要條件檔案的路徑。 根據 PrerequisiteComp 值而定，安裝程式會使用此路徑儲存下載的檔案或尋找先前下載的檔案。  

-   **索引鍵名稱：**AdminConsole  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定是否安裝 Configuration Manager 主控台。  

-   **索引鍵名稱：**JoinCEIP  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **詳細資料：** 指定是否加入「客戶經驗改進計畫」。  

-   **索引鍵名稱：**AddServerLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**指定可用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的伺服器語言。 依預設使用英文版。  

-   **索引鍵名稱：**AddClientLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**指定將可用於用戶端電腦的語言。 依預設使用英文版。  

-   **索引鍵名稱：**DeleteServerLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**於安裝之後修改站台。  
        指定將移除且無法再用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的語言。 預設使用英文，無法移除。  

-   **索引鍵名稱：**DeleteClientLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**於安裝之後修改站台。  
        指定移除用戶端電腦不再使用的語言。 預設使用英文，無法移除。  

-   **索引鍵名稱：**MobileDeviceLanguage  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定是否安裝行動裝置用戶端語言。  

**SQLConfigOptions**  

-   **索引鍵名稱：**SQLServerName  

    -   **必要︰** 是  

    -   **值︰***SQLServerName*  

    -   **詳細資料：**指定正在執行 SQL Server 的伺服器名稱或叢集執行個體的名稱。 它會作為網站資料庫的主機。  

-   **索引鍵名稱：**DatabaseName  

    -   **必要︰** 是  

    -   **值：**&lt;站台資料庫名稱\> 或 &lt;執行個體名稱\>\&lt;站台資料庫名稱\>  

    -   **詳細資料:**  

         指定要建立或用來安裝管理中心網站資料庫的 SQL Server 資料庫的名稱。  

        > [!IMPORTANT]  
        >  如果您未使用預設執行個體，則必須指定執行個體名稱及網站資料庫名稱。  

-   **索引鍵名稱：**SQLSSBPort  

    -   **必要：** 否  

    -   **值：** &lt;SSB 埠號>  

    -   **詳細資料：**指定 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 通常 SSB 是設定為使用 TCP 連接埠 4022，但也支援其他連接埠。  

-   **索引鍵名稱：**SQLDataFilePath  

    -   **必要：** 否  

    -   **值︰**&lt;資料庫 .MDB 檔案的檔案路徑>  

    -   **詳細資料：**指定建立資料庫 .MDB 檔案的替代位置。  

-   **索引鍵名稱：**SQLLogFilePath  

    -   **必要：** 否  

    -   **值︰**&lt;資料庫 .LDF 檔案的檔案路徑>  

    -   **詳細資料：**指定建立資料庫 .LDF 檔案的替代位置。  

**CloudConnectorOptions**  

-   **索引鍵名稱：**CloudConnector  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定您是否會在這個站台安裝服務連接點。 因為服務連接點只能安裝在階層的頂層站台，子主要站台的這個值必須為 0。  

-   **索引鍵名稱：**CloudConnectorServer  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰**&lt;服務連接點伺服器 FQDN>  

    -   **詳細資料：**指定將裝載服務連接點站台系統角色之伺服器的 FQDN。  

-   **索引鍵名稱：**UseProxy  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定服務連接點是否使用 Proxy 伺服器。  

-   **索引鍵名稱：**ProxyName  

    -   **必要：**UseProxy 等於 1 時為必要  

    -   **值︰**&lt;Proxy 伺服器 FQDN>  

    -   **詳細資料：**指定服務連接點站台系統角色將使用之 Proxy 伺服器的 FQDN。  

-   **索引鍵名稱：**ProxyPort  

    -   **必要：**UseProxy 等於 1 時為必要  

    -   **值︰**&lt;通訊埠編號>  

    -   **詳細資料：**指定要使用的連接埠號碼。  

### <a name="unattended-install-for-a-primary-site"></a>主要站台的自動安裝  
按照以下詳細資料，使用自動安裝指令碼檔案來安裝主要站台。  

使用以下詳細資料，透過使用自動安裝指令碼檔案來安裝管理中心網站。  

**識別**  

-   **索引鍵名稱：** Action  

    -   **必要︰** 是  

    -   **值：**InstallPrimarySite  

    -   **詳細資料︰**安裝主要站台。  

**選項**  

-   **索引鍵名稱︰**ProductID  

    -   **必要︰** 是  

    -   **值：***xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* 或 *Eval*  

    -   **詳細資料：**指定 Configuration Manager 安裝產品金鑰，含破折號。 輸入 **Eval** 安裝 Configuration Manager 評估版。  

-   **索引鍵名稱：**SiteCode  

    -   **必要︰** 是  

    -   **值︰**&lt;站台碼>  

    -   **詳細資料：**指定可特別識別出階層中站台的三個英數字元。  

-   **索引鍵名稱：**SiteName  

    -   **必要︰** 是  

    -   **值：** &lt;站台名稱>  

    -   **詳細資料：**指定此站台的名稱。  

-   **索引鍵名稱：**SMSInstallDir  

    -   **必要︰** 是  

    -   **值︰**Configuration Manager 安裝路徑  

    -   **詳細資料：**指定 Configuration Manager 程式檔案的安裝資料夾。  

-   **索引鍵名稱：**SDKServer  

    -   **必要︰** 是  

    -   **值：**&lt;SMS 提供者的FQDN>  

    -   **詳細資料：** 指定將裝載 SMS 提供者的伺服器 FQDN。  
        您可以在初始安裝後設定站台的其他 SMS 提供者。  

-   **索引鍵名稱︰**PrerequisiteComp  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 下載  

         1 = 已下載  

    -   **詳細資料：** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 0 值，安裝程式會下載檔案。  

-   **索引鍵名稱︰**PrerequisitePath  

    -   **必要︰** 是  

    -   **值：** &lt;安裝路必要條件檔案>  

    -   **詳細資料：** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑儲存下載的檔案或尋找之前下載的檔案。  

-   **索引鍵名稱：**AdminConsole  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定是否安裝 Configuration Manager 主控台。  

-   **索引鍵名稱：**JoinCEIP  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **詳細資料：** 指定是否加入「客戶經驗改進計畫」。  

-   **索引鍵名稱：**ManagementPoint  

    -   **必要：** 否  

    -   **值：**&lt;管理點站台伺服器 FQDN>  

    -   **詳細資料︰**指定將作為管理點站台系統角色之伺服器的 FQDN。  

-   **索引鍵名稱：**ManagementPointProtocol  

    -   **必要：** 否  

    -   **值︰**HTTPS 或 HTTP  

    -   **詳細資料：**指定用於管理點的通訊協定。  

-   **索引鍵名稱：**DistributionPoint  

    -   **必要：** 否  

    -   **值：**&lt;發佈點站台伺服器 FQDN>  

    -   **詳細資料：**指定用於管理點的通訊協定。  

-   **索引鍵名稱：**DistributionPointProtocol  

    -   **必要：** 否  

    -   **值︰**HTTPS 或 HTTP  

    -   **詳細資料︰**指定用於發佈點的通訊協定。  

-   **索引鍵名稱：**RoleCommunicationProtocol  

    -   **必要︰** 是  

    -   **值：**EnforceHTTPS 或 HTTPorHTTPS  

    -   **詳細資料︰**指定是否設定所有站台系統以僅接受來自用戶端的 HTTPS 通訊，或是針對每個站台系統角色設定通訊方法。 選取進行 [EnforceHTTPS] 時，用戶端電腦必須有有效的 PKI 憑證進行用戶端授權。  

-   **索引鍵名稱：**ClientsUsePKICertificate  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不使用  

         1 = 使用  

    -   **詳細資料︰**指定用戶端是否會以用戶端 PKI 憑證來與站台系統角色通訊。  

-   **索引鍵名稱：**AddServerLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**指定可用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的伺服器語言。 依預設使用英文版。  

-   **索引鍵名稱：**AddClientLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**指定將可用於用戶端電腦的語言。 依預設使用英文版。  

-   **索引鍵名稱：**DeleteServerLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**於安裝之後修改站台。  
        指定將移除且無法再用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的語言。 預設使用英文，無法移除。  

-   **索引鍵名稱：**DeleteClientLanguages  

    -   **必要：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **詳細資料：**於安裝之後修改站台。  
        指定移除用戶端電腦不再使用的語言。 預設使用英文，無法移除。  

-   **索引鍵名稱：**MobileDeviceLanguage  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定是否安裝行動裝置用戶端語言。  

**SQLConfigOptions**  

-   **索引鍵名稱：**SQLServerName  

    -   **必要︰** 是  

    -   **值︰***SQLServerName*  

    -   **詳細資料：**指定正在執行 SQL Server 的伺服器名稱或叢集執行個體的名稱。 它會作為網站資料庫的主機。  

-   **索引鍵名稱：**DatabaseName  

    -   **必要︰** 是  

    -   **值：**&lt;站台資料庫名稱\> 或 &lt;執行個體名稱\>\&lt;站台資料庫名稱\>  

    -   **詳細資料:**  

         指定要建立或用來安裝主要網站資料庫的 SQL Server 資料庫名稱。  

        > [!IMPORTANT]  
        >  如果您未使用預設執行個體，則必須指定執行個體名稱及網站資料庫名稱。  

-   **索引鍵名稱：**SQLSSBPort  

    -   **必要：** 否  

    -   **值：** &lt;SSB 埠號>  

    -   **詳細資料：**指定 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 通常 SSB 是設定為使用 TCP 連接埠 4022，但也支援其他連接埠。  

-   **索引鍵名稱：**SQLDataFilePath  

    -   **必要：** 否  

    -   **值︰**&lt;資料庫 .MDB 檔案的檔案路徑>  

    -   **詳細資料：**指定建立資料庫 .MDB 檔案的替代位置。  

-   **索引鍵名稱：**SQLLogFilePath  

    -   **必要：** 否  

    -   **值︰**&lt;資料庫 .LDF 檔案的檔案路徑>  

    -   **詳細資料：**指定建立資料庫 .LDF 檔案的替代位置。  

**HierarchyExpansionOption**  

-   **索引鍵名稱：**CCARSiteServer  

    -   **必要：** 否  

    -   **值：**&lt;管理中心網站的 FQDN>  

    -   **詳細資料︰**指定主要站台加入 Configuration Manager 階層時要連接的管理中心網站。 您必須在安裝期間指定管理中心網站。  

-   **索引鍵名稱：**CASRetryInterval  

    -   **必要：** 否  

    -   **值︰**&lt;間隔>  

    -   **詳細資料：** 指定連線失敗後，嘗試連線至管理中心站台的重試間隔 (分鐘)。 例如，如果與管理中心網站的連線失敗，主要網站會等待您針對 CASRetryInterval 指定的分鐘數，然後重試連線。  

-   **索引鍵名稱：**WaitForCASTimeout  

    -   **必要：** 否  

    -   **值︰**&lt;*逾時*>  

         0 到 100 的值  

    -   **詳細資料：**指定主要站台連線至管理中心網站的最大逾時值 (以分鐘為單位)。 例如，如果主要網站到管理中心網站的連線失敗，主要網站會根據 CASRetryInterval 重試連線至管理中心網站，直到達到 WaitForCASTimeout 期間。 您可以指定 0 到 100 的值。  

**CloudConnectorOptions**  

-   **索引鍵名稱：**CloudConnector  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定您是否會在這個站台安裝服務連接點。 因為服務連接點只能安裝在階層的頂層站台，子主要站台的這個值必須為 0。  

-   **索引鍵名稱：**CloudConnectorServer  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰**&lt;服務連接點伺服器 FQDN\>  

    -   **詳細資料：**指定將裝載服務連接點站台系統角色之伺服器的 FQDN。  

-   **索引鍵名稱：**UseProxy  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定服務連接點是否使用 Proxy 伺服器。  

-   **索引鍵名稱：**ProxyName  

    -   **必要：**UseProxy 等於 1 時為必要  

    -   **值︰**&lt;Proxy 伺服器 FQDN>  

    -   **詳細資料：**指定服務連接點站台系統角色將使用之 Proxy 伺服器的 FQDN。  

-   **索引鍵名稱：**ProxyPort  

    -   **必要：**UseProxy 等於 1 時為必要  

    -   **值︰**&lt;通訊埠編號>  

    -   **詳細資料：**指定要使用的連接埠號碼。  

### <a name="unattended-recovery-for-a-central-administration-site"></a>管理中心網站的自動復原  
 使用下列詳細資料，以自動安裝指令碼檔案來復原管理中心網站。  

**識別**  

-   **索引鍵名稱：** Action  

    -   **必要︰** 是  

    -   **值：** RecoverCCAR  

    -   **詳細資料︰**復原管理中心網站。  

**RecoveryOptions**  

-   **索引鍵名稱：**ServerRecoveryOptions  

    -   **必要︰** 是  

    -   **值︰** 1、2 或 4  

         1 = 復原網站伺服器和 SQL Server。  

         2 = 僅復原網站伺服器。  

         4 = 僅復原 SQL Server。  

    -   **詳細資料：** 指定安裝程式只要復原站台伺服器、SQL Server 或同時復原兩者。 針對 ServerRecoveryOptions 設定以下值時，需要關聯的索引鍵：  

        -   值 = 1：您會看到可指定 **SiteServerBackupLocation** 索引鍵值的選項，藉此使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

        -   值 = 2：您會看到可指定 **SiteServerBackupLocation** 索引鍵值的選項，藉此使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

        -   值 = 4：將 **DatabaseRecoveryOptions** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原站台資料庫。  

-   **索引鍵名稱：**DatabaseRecoveryOptions  

    -   **必要：**ServerRecoveryOptions 設定值為 **1** 或 **4** 時，需要此索引鍵。  

    -   **值︰** 10、20、40、80  

         10 = 從備份還原網站資料庫。  

         20 = 使用以另一種方式手動復原的網站資料庫。  

         40 = 為網站建立新的資料庫。 若無可用網站資料庫備份，請使用此選項。 透過從其他網站複寫來復原全域和網站資料。  

         80 = 略過資料庫復原。  

    -   **詳細資料：**指定安裝程式如何復原 SQL Server 中的站台資料庫。  

-   **索引鍵名稱：**ReferenceSite  

    -   **必要：****DatabaseRecoveryOptions** 設定的值為 **40** 時，需要此索引鍵。  

    -   **值：**&lt;參照站台 FQDN>  

    -   **詳細資料︰** 若資料庫備份比變更追蹤保留期間還舊，或未使用備份復原站台，請指定管理中心所使用的參照主要站台來復原全域資料。  

         若沒有指定參照網站，且備份又比變更追蹤保留期間還舊，所有主要網站都會以來自管理中心網站的還原資料重新初始化。  

         若您並未指定參照網站，且備份是在變更追蹤保留期間內，則只會從主要網站複寫備份後的變更。 若不同主要網站間的變更發生衝突，則管理中心網站會使用第一個收到的變更。  

-   **索引鍵名稱：**SiteServerBackupLocation  

    -   **必要：** 否  

    -   **值：**站台伺服器備份組路徑&lt;>  

    -   **詳細資料︰** 指定站台伺服器備份集的路徑。 **ServerRecoveryOptions** 設定值為 **1** 或 **2**時，可選擇是否要使用此索引鍵。 指定 **SiteServerBackupLocation** 索引鍵值，藉此使用網站備份來復原網站。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

-   **索引鍵名稱：**BackupLocation  

    -   **必要：****ServerRecoveryOptions** 索引鍵的設定值為 **1** 或 **4**，且 **DatabaseRecoveryOptions** 索引鍵的設定值為 **10** 時，需要此索引鍵。  

    -   **值：**站台資料庫備份組路徑&lt;>  

    -   **詳細資料：** 指定站台資料庫備份集的路徑。  

**選項**  

-   **索引鍵名稱︰**ProductID  

    -   **必要︰** 是  

    -   **值：***xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* 或 *Eval*  

    -   **詳細資料：**指定 Configuration Manager 安裝產品金鑰，含破折號。 輸入 **Eval** 安裝 Configuration Manager 評估版。  

-   **索引鍵名稱：**SiteCode  

    -   **必要︰** 是  

    -   **值︰**&lt;站台碼>  

    -   **詳細資料：**指定可特別識別出階層中站台的三個英數字元。 您必須指定網站失敗前使用的網站碼。 如需站台碼限制的詳細資訊，請參閱本主題中的 [關於站台名稱及站台碼](#bkmk_codes) 一節。  

-   **索引鍵名稱：**SiteName  

    -   **必要：** 否  

    -   **值：** &lt;站台名稱>  

    -   **詳細資料：**指定此站台的名稱。  

-   **索引鍵名稱：**SMSInstallDir  

    -   **必要︰** 是  

    -   **值︰**&lt;onfiguraton Manager 安裝路徑*C*>  

    -   **詳細資料：**指定 Configuration Manager 程式檔案的安裝資料夾。  

-   **索引鍵名稱：**SDKServer  

    -   **必要︰** 是  

    -   **值：**&lt;SMS 提供者的FQDN>  

    -   **詳細資料：** 指定將裝載 SMS 提供者的伺服器 FQDN。 您必須指定失敗前裝載 SMS 提供者的伺服器。  

         您可以在初始安裝後設定站台的其他 SMS 提供者。 如需 SMS 提供者的詳細資訊，請參閱 [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (規劃 System Center Configuration Manager 的 SMS 提供者)。  

-   **索引鍵名稱︰**PrerequisiteComp  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 下載  

         1 = 已下載  

    -   **詳細資料：** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 **0**值，安裝程式就會下載檔案。  

-   **索引鍵名稱︰**PrerequisitePath  

    -   **必要︰** 是  

    -   **值：** &lt;安裝路必要條件檔案>  

    -   **詳細資料：** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑儲存下載的檔案或尋找之前下載的檔案。  

-   **索引鍵名稱：**AdminConsole  

    -   **必要：**此索引鍵為必要，除非 **ServerRecoveryOptions** 設定的值為 **4**。  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定是否安裝 Configuration Manager 主控台。  

-   **索引鍵名稱：**JoinCEIP  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **詳細資料：** 指定是否加入「客戶經驗改進計畫」。  

**SQLConfigOptions**  

-   **索引鍵名稱：**SQLServerName  

    -   **必要︰** 是  

    -   **值︰***SQLServerName*  

    -   **詳細資料：**指定執行將裝載站台資料庫之 SQL Server 的伺服器名稱，或叢集執行個體名稱。 您必須指定失敗前裝載網站資料庫的相同伺服器。  

-   **索引鍵名稱：**DatabaseName  

    -   **必要︰** 是  

    -   **值：**&lt;站台資料庫名稱\> 或 &lt;執行個體名稱\>\&lt;站台資料庫名稱\>  

    -   **詳細資料:**  

         指定要建立或用來安裝管理中心網站資料庫的 SQL Server 資料庫的名稱。 您必須指定失敗前所使用的相同資料庫名稱。  

        > [!IMPORTANT]  
        >  如果您未使用預設執行個體，則必須指定執行個體名稱及網站資料庫名稱。  

-   **索引鍵名稱：**SQLSSBPort  

    -   **必要︰** 是  

    -   **值：** &lt;SSB 埠號>  

    -   **詳細資料：**指定 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 通常 SSB 是設定為使用 TCP 連接埠 4022。 您必須指定失敗前所使用的相同 SSB 連接埠。  

-   **索引鍵名稱：**SQLDataFilePath  

    -   **必要：** 否  

    -   **值︰**&lt;資料庫 .MDB 檔案的檔案路徑>  

    -   **詳細資料：**指定建立資料庫 .MDB 檔案的替代位置。  

-   **索引鍵名稱：**SQLLogFilePath  

    -   **必要：** 否  

    -   **值︰**&lt;資料庫 .LDF 檔案的檔案路徑>  

    -   **詳細資料：**指定建立資料庫 .LDF 檔案的替代位置。  

**CloudConnectorOptions**  

-   **索引鍵名稱：**CloudConnector  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定您是否會在這個站台安裝服務連接點。 因為服務連接點只能安裝在階層的頂層站台，子主要站台的這個值必須為 0。  

-   **索引鍵名稱：**CloudConnecorServer  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰**&lt;服務連接點伺服器 FQDN>  

    -   **詳細資料：**指定將裝載服務連接點站台系統角色之伺服器的 FQDN。  

-   **索引鍵名稱：**UseProxy  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定服務連接點是否使用 Proxy 伺服器。  

-   **索引鍵名稱：**ProxyName  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰**&lt;Proxy 伺服器 FQDN>  

    -   **詳細資料：**指定服務連接點站台系統角色將使用之 Proxy 伺服器的 FQDN。  

-   **索引鍵名稱：**ProxyPort  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰**&lt;通訊埠編號>  

    -   **詳細資料：**指定要使用的連接埠號碼。  

### <a name="unattended-recovery-for-a-primary-site"></a>主要站台的自動復原  
 按照以下詳細資料，使用自動安裝指令碼檔案來復原主要站台。  

**識別**  

-   **索引鍵名稱：** Action  

    -   **必要︰** 是  

    -   **值︰** RecoverPrimarySite  

    -   **詳細資料︰**復原主要站台。  

**RecoveryOptions**  

-   **索引鍵名稱：**ServerRecoveryOptions  

    -   **必要︰** 是  

    -   **值︰** 1、2 或 4  

         1 = 復原網站伺服器和 SQL Server。  

         2 = 僅復原網站伺服器。  

         4 = 僅復原 SQL Server。  

    -   **詳細資料：** 指定安裝程式只要復原站台伺服器、SQL Server 或同時復原兩者。 針對 ServerRecoveryOptions 設定以下值時，需要關聯的索引鍵：  

        -   值 = 1：您會看到可指定 **SiteServerBackupLocation** 索引鍵值的選項，藉此使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

        -   值 = 2：您會看到可指定 **SiteServerBackupLocation** 索引鍵值的選項，藉此使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

        -   值 = 4：將 **DatabaseRecoveryOptions** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原站台資料庫。  

-   **索引鍵名稱：**DatabaseRecoveryOptions  

    -   **必要：**ServerRecoveryOptions 設定值為 **1** 或 **4** 時，需要此索引鍵。  

    -   **值︰** 10、20、40、80  

         10 = 從備份還原網站資料庫。  

         20 = 使用以另一種方式手動復原的網站資料庫。  

         40 = 為網站建立新的資料庫。 若無可用網站資料庫備份，請使用此選項。 透過從其他網站複寫來復原全域和網站資料。  

         80 = 略過資料庫復原。  

    -   **詳細資料：**指定安裝程式如何復原 SQL Server 中的站台資料庫。  

-   **索引鍵名稱：**SiteServerBackupLocation  

    -   **必要：** 否  

    -   **值：**站台伺服器備份組路徑&lt;>  

    -   **詳細資料:**  

         指定網站伺服器備份集的路徑。 **ServerRecoveryOptions** 設定值為 **1** 或 **2**時，可選擇是否要使用此索引鍵。 指定 **SiteServerBackupLocation** 索引鍵值，藉此使用網站備份來復原網站。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。  

-   **索引鍵名稱：**BackupLocation  

    -   **必要：****ServerRecoveryOptions** 索引鍵的設定值為 **1** 或 **4**，且 **DatabaseRecoveryOptions** 索引鍵的設定值為 **10** 時，需要此索引鍵。  

    -   **值：**站台資料庫備份組路徑&lt;>  

    -   **詳細資料：** 指定站台資料庫備份集的路徑。  

**選項**  

-   **索引鍵名稱︰**ProductID  

    -   **必要︰** 是  

    -   **值：***xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* 或 *Eval*  

    -   **詳細資料：**指定 Configuration Manager 安裝產品金鑰，含破折號。 輸入 **Eval** 安裝 Configuration Manager 評估版。  

-   **索引鍵名稱：**SiteCode  

    -   **必要︰** 是  

    -   **值︰**&lt;站台碼>  

    -   **詳細資料：**指定可特別識別出階層中站台的三個英數字元。 您必須指定網站失敗前使用的網站碼。 如需站台碼限制的詳細資訊，請參閱本主題中的 [關於站台名稱及站台碼](#bkmk_codes) 一節。  

-   **索引鍵名稱：**SiteName  

    -   **必要：** 否  

    -   **值：** &lt;站台名稱>  

    -   **詳細資料：**指定此站台的名稱。  

-   **索引鍵名稱：**SMSInstallDir  

    -   **必要︰** 是  

    -   **值︰**&lt;onfiguraton Manager 安裝路徑*C*>  

    -   **詳細資料：**指定 Configuration Manager 程式檔案的安裝資料夾。  

-   **索引鍵名稱：**SDKServer  

    -   **必要︰** 是  

    -   **值：**&lt;SMS 提供者的FQDN>  

    -   **詳細資料：** 指定將裝載 SMS 提供者的伺服器 FQDN。 您必須指定失敗前裝載 SMS 提供者的伺服器。 您可以在初始安裝後設定站台的其他 SMS 提供者。 如需 SMS 提供者的詳細資訊，請參閱 [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (規劃 System Center Configuration Manager 的 SMS 提供者)。  

-   **索引鍵名稱︰**PrerequisiteComp  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 下載  

         1 = 已下載  

    -   **詳細資料：** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 **0**值，安裝程式就會下載檔案。  

-   **索引鍵名稱︰**PrerequisitePath  

    -   **必要︰** 是  

    -   **值：** &lt;安裝路必要條件檔案>  

    -   **詳細資料：** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑儲存下載的檔案或尋找之前下載的檔案。  

-   **索引鍵名稱：**AdminConsole  

    -   **必要：**此索引鍵為必要，除非 **ServerRecoveryOptions** 設定的值為 **4**。  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定是否安裝 Configuration Manager 主控台。  

-   **索引鍵名稱：**JoinCEIP  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **詳細資料：** 指定是否加入「客戶經驗改進計畫」。  

**SQLConfigOptions**  

-   **索引鍵名稱：**SQLServerName  

    -   **必要︰** 是  

    -   **值︰***SQLServerName*  

    -   **詳細資料：**指定執行將裝載站台資料庫之 SQL Server 的伺服器名稱，或叢集執行個體名稱。 您必須指定失敗前裝載網站資料庫的相同伺服器。  

-   **索引鍵名稱：**DatabaseName  

    -   **必要︰** 是  

    -   **值：**&lt;站台資料庫名稱\> 或 &lt;執行個體名稱\>\\&lt;站台資料庫名稱\>

    -   **詳細資料:**  

         指定要建立或用來安裝管理中心網站資料庫的 SQL Server 資料庫的名稱。 您必須指定失敗前所使用的相同資料庫名稱。  

        > [!IMPORTANT]  
        >  如果您未使用預設執行個體，則必須指定執行個體名稱及網站資料庫名稱。  

-   **索引鍵名稱：**SQLSSBPort  

    -   **必要︰** 是  

    -   **值：** &lt;SSB 埠號>  

    -   **詳細資料：**指定 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 通常 SSB 是設定為使用 TCP 連接埠 4022。 您必須指定失敗前所使用的相同 SSB 連接埠。  

-   **索引鍵名稱：**SQLDataFilePath  

    -   **必要：** 否  

    -   **值︰**&lt;資料庫 .MDB 檔案的檔案路徑>  

    -   **詳細資料：**指定建立資料庫 .MDB 檔案的替代位置。  

-   **索引鍵名稱：**SQLLogFilePath  

    -   **必要：** 否  

    -   **值︰**&lt;資料庫 .LDF 檔案的檔案路徑>  

    -   **詳細資料：**指定建立資料庫 .LDF 檔案的替代位置。  

**HierarchyExpansionOptions**  

-   **索引鍵名稱：**CCARSiteServer  

    -   **必要：**查看詳細資料。  

    -   **值：**&lt;管理中心網站的站台碼>  

    -   **詳細資料︰**指定主要站台加入 Configuration Manager 階層時要連接的管理中心網站。 如果主要網站在失敗前連接至管理中心網站，則此設定為必要。 您必須指定失敗前用於管理中心網站的網站碼。  

-   **索引鍵名稱：**CASRetryInterval  

    -   **必要：** 否  

    -   **值︰**&lt;間隔>  

    -   **詳細資料：** 指定連線失敗後，嘗試連線至管理中心站台的重試間隔 (分鐘)。 例如，如果與管理中心網站的連線失敗，主要網站會等待您針對 **CASRetryInterval**指定的分鐘數，然後再次嘗試連線。  

-   **索引鍵名稱：**WaitForCASTimeout  

    -   **必要：** 否  

    -   **值︰**&lt;逾時>  

    -   **詳細資料：**指定主要站台連線至管理中心網站的最大逾時值 (以分鐘為單位)。 例如，如果主要網站連線至管理中心網站失敗，則主要網站會依據 **CASRetryInterval** 重試與管理中心網站的連線，直到達到 **WaitForCASTimeout** 期間。 您可以指定 0 到 100 的值。  

**CloudConnectorOptions**  

-   **索引鍵名稱：**CloudConnector  

    -   **必要︰** 是  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定您是否會在這個站台安裝服務連接點。 因為服務連接點只能安裝在階層的頂層站台，子主要站台的這個值必須為 0。  

-   **索引鍵名稱：**CloudConnecorServer  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰**&lt;服務連接點伺服器 FQDN>  

    -   **詳細資料：**指定將裝載服務連接點站台系統角色之伺服器的 FQDN。  

-   **索引鍵名稱：**UseProxy  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰** 0 或 1  

         0 = 不安裝  

         1 = 安裝  

    -   **詳細資料：**指定服務連接點是否使用 Proxy 伺服器。  

-   **索引鍵名稱：**ProxyName  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰**&lt;Proxy 伺服器 FQDN>  

    -   **詳細資料：**指定服務連接點站台系統角色將使用之 Proxy 伺服器的 FQDN。  

-   **索引鍵名稱：**ProxyPort  

    -   **必要：**CloudConnector 等於 1 時為必要  

    -   **值︰**&lt;通訊埠編號>  

    -   **詳細資料：**指定要使用的連接埠號碼。  



<!--HONumber=Nov16_HO1-->


