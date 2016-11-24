---
title: "必要條件檢查工具 | System Center Configuration Manager"
description: "了解如何使用必要條件檢查程式，識別並修正會封鎖實際站台或站台系統角色安裝的問題。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4c2322ed0805b5f087409ec487ebec9d7c4f10d5

---
# <a name="prerequisite-checker-for-system-center-configuration-manager"></a>System Center Configuration Manager 的必要條件檢查工具

*適用於：System Center Configuration Manager (最新分支)*


 在執行安裝程式來安裝或升級 System Center Configuration Manager 站台前，或在新的伺服器上安裝站台系統角色前，您可以使用要用來確認伺服器整備程度之 Configuration Manager 版本中的這個獨立應用程式 (**Prereqchk.exe**)。 使用必要條件檢查程式，可讓您針對會封鎖實際站台或站台系統角色安裝的問題，加以識別並修正。  

> [!NOTE]  
>  必要條件檢查程式一律會執行，其為安裝程序的一部分。  

根據預設，在必要條件檢查程式執行時：  

-   它會驗證其執行所在的伺服器  

-   系統會掃描本機電腦，檢查是否有現有的站台伺服器，並且只會執行適用於站台的檢查  

-   如果未偵測到現有站台，則會執行所有必要條件規則  

-   它會檢查規則，以確認安裝程序所需的軟體及設定都已安裝。 必要的軟體很可能需要額外的組態或軟體更新，且這些組態及更新需尚未經過必要條件檢查程式的驗證。  

-   它會將其結果記錄在電腦系統磁碟機上的 **ConfigMgrPrereq.log** 檔案中。 記錄檔可能包含未在使用者介面中顯示的其他資訊。  

當您在命令提示字元中執行必要條件檢查程式，並指定特定的命令列選項時：  

-   必要條件檢查程式只會執行與站台伺服器相關聯、或是您在命令列中指定之站台系統的檢查。  

-   若要檢查遠端電腦，您的使用者帳戶必須具有系統管理權限，而該權限需能移除電腦  

如需必要條件檢查程式所執行的必要條件檢查的詳細資訊，請參閱 [System Center Configuration Manager 的必要條件檢查清單](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md)。  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>將必要條件檢查程式複製到另一部電腦  

1.  在 Windows 檔案總管中，瀏覽至下列其中一個位置：  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  將下列檔案複製到另一部電腦的目的地資料夾：  

    -   Prereqchk.exe  

    -   Prereqcore.dll  

    -   Basesql.dll  

    -   Basesvr.dll  

    -   Baseutil.dll  

##  <a name="run-prerequisite-checker-with-default-checks"></a>利用預設檢查來執行必要條件檢查程式  

1.  在 Windows 檔案總管中，瀏覽至下列其中一個位置：  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  執行 **prereqchk.exe** ，以啟動必要條件檢查程式。   
    必要條件檢查工具會偵測現有網站，如果找到的話，會執行升級整備程度檢查。 如果未找到網站，則會執行所有檢查。 [網站類型]  欄提供與規則相關聯的網站伺服器或網站系統資訊。  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>針對所有預設檢查，從命令提示字元執行必要條件檢查程式  

1.  開啟 [命令提示字元] 視窗，並將目錄變更為下列其中一個位置：  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  輸入  **prereqchk.exe /LOCAL** 以啟動必要條件檢查程式，並在伺服器上執行所有必要條件檢查。  

## <a name="run-prerequisite-checker-from-a-command-prompt-for-specified-options"></a>針對特定選項，從命令提示字元執行必要條件檢查程式  

1.  開啟 [命令提示字元] 視窗，並將目錄變更為下列其中一個位置：  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  輸入 **prereqchk.exe**，並加上一個或多個下列命令列選項。  

    例如，若要檢查主要站台，您可能會使用下列項目：  

    -   **prereqchk.exe [/NOUI] /PRI /SQL &lt;SQL Server 的 FQDN\> /SDK &lt;SMS 提供者的 FQDN\> [/JOIN &lt;管理中心網站的 FQDN\>] [/MP &lt;管理點的 FQDN\>] [/DP &lt;發佈點的 FQDN\>]**  

    **管理中心網站伺服器：**  

    -   **/NOUI**  

         非必要 - 啟動必要條件檢查工具，但不顯示使用者介面。 在命令列中指定任何其他選項之前，必須先指定此選項。  

    -   **/CAS**  

         必要 - 確認本機電腦符合管理中心網站的需求。  

    -   **/SQL &lt;*SQL Server 的 FQDN*>**  

         必要 - 確認指定的電腦符合讓 SQL Server 裝載 Configuration Manager 站台資料庫的需求。  

    -   **/SDK &lt;*SMS 提供者的 FQDN*>**  

         必要 - 確認指定的電腦符合 SMS 提供者的需求。  

    -   **/Ssbport**  

         非必要 - 確認防火牆例外狀況有效，可允許 SSB 連接埠上的通訊。 預設的連接埠號碼為 4022。  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         非必要 - 確認符合站台安裝的最小磁碟空間需求。  

    **主要站台伺服器：**  

    -   **/NOUI**  

        非必要 - 啟動必要條件檢查工具，但不顯示使用者介面。 在命令列中指定任何其他選項之前，必須先指定此選項。  

    -   **/PRI**  

         必要 - 確認本機電腦符合主要站台的需求。  

    -   **/SQL &lt;*SQL Server 的 FQDN*>**  

         必要 - 確認指定的電腦符合讓 SQL Server 裝載 Configuration Manager 站台資料庫的需求。  

    -   **/SDK &lt;*SMS 提供者的 FQDN*>**  

         必要 - 確認指定的電腦符合 SMS 提供者的需求。  

    -   **/JOIN &lt;*管理中心網站的 FQDN*>**  

         非必要 - 確認本機電腦符合連線至管理中心站台伺服器的需求。  

    -   **/MP &lt;*管理點的 FQDN*>**  

         非必要 - 確認指定的電腦符合管理點站台系統角色的需求。 此選項只有在您使用 **/PRI** 選項時才受支援。  

    -   **/DP &lt;*發佈點的 FQDN*>**  

         非必要 - 確認指定的電腦符合發佈點站台系統角色的需求。 此選項只有在您使用 **/PRI** 選項時才受支援。  

    -   **/Ssbport**  

         非必要 - 確認防火牆例外狀況有效，可允許 SSB 連接埠上的通訊。 預設的連接埠號碼為 4022。  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         非必要 - 確認符合站台安裝的最小磁碟空間需求。  

    **次要站台伺服器：**  

    -   **/NOUI**  

         非必要 - 啟動必要條件檢查工具，但不顯示使用者介面。 在命令列中指定任何其他選項之前，必須先指定此選項。  

    -   **/SEC &lt;*次要站台伺服器的 FQDN*>**  

         必要 - 確認指定的電腦符合次要站台的需求。  

    -   **/INSTALLSQLEXPRESS**  

         非必要 - 確認可在指定的電腦上安裝 SQL Server Express。  

    -   **/Ssbport**  

         不需要 -      
        確認防火牆例外狀況有效，可允許 SQL Server Service Broker (SSB) 連接埠的通訊。 預設的連接埠號碼為 4022。  

    -   **/Sqlport**  

         非必要 - 確認防火牆例外狀況有效，可允許 SQL Server 服務連接埠的通訊，而且沒有其他具名 SQL Server 執行個體正在使用該連接埠。 預設的連接埠為 1433。  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         非必要 - 確認符合站台安裝的最小磁碟空間需求。  

    -   **/SourceDir**  

         非必要 - 確認次要站台的電腦帳戶可以存取裝載安裝程式來源檔案的資料夾。  

     **Configuration Manager 主控台：**  

    -   **/Adminui**  

         必要 - 確認本機電腦符合安裝 Configuration Manager 的需求。  

3.  在必要條件檢查程式 UI 中，必要條件檢查程式會在 [必要條件結果]  區段中建立一份探索到的問題清單。  

    -   按一下清單中的項目，即可顯示有關如何解決問題的詳細資料。  

    -   您可以在安裝站台伺服器、站台系統或 Configuration Manager 主控台之前，解決清單中所有 [錯誤] 狀態的項目。  

    -   您也可以在系統磁碟機的根目錄中開啟 **ConfigMgrPrereq.log** 檔案，以檢閱必要條件檢查程式的結果。 記錄檔可能包含未在使用者介面中顯示的其他資訊。  



<!--HONumber=Nov16_HO1-->


