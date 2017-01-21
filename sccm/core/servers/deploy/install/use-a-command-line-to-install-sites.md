---
title: "命令列安裝 | System Center Configuration Manager"
description: "了解如何從命令提示字元執行 System Center Configuration Manager 安裝程式，以進行各種站台安裝。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ea097188351cd60a13659e2860c5e0a2bac2c069

---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>使用命令提示字元來安裝 System Center Configuration Manager 站台

*適用於：System Center Configuration Manager (最新分支)*

 您可以選擇從命令提示字元執行 System Center Configuration Manager 安裝程式，以進行各種站台安裝。

 ## <a name="supported-tasks-for-command-line-installs"></a>支援的命令列安裝工作
 這種執行安裝程式的方法支援下列站台安裝和站台維護工作︰

-   **從命令列安裝管理中心網站或主要站台：**  
  檢視[安裝程式的命令列選項](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

 -  **修改管理中心網站或主要站台所使用的語言：**  
    若要修改站台所安裝的語言，必須從命令列 (包括行動裝置語言) 進行：  

     -   從站台伺服器的 **&lt;ConfigMgrInstallationPath\>\Bin\X64** 執行安裝程式
     -   使用 **/MANAGELANGS** 命令列選項
     -   指定語言指令碼檔，其會指定您要新增或移除的語言。  

    例如，使用下列命令語法：**setupwpf.exe /MANAGELANGS &lt;語言指令檔\>**  

    若要建立語言指令檔，請使用[用以管理語言的命令列選項](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)中的資訊  

 -  **使用安裝指令檔進行自動站台安裝或站台復原：**  
    您可以從命令列執行安裝程式，並指示安裝程式使用安裝指令碼，然後執行站台自動安裝。 您也可以使用此選項來復原站台。    

    若要搭配指令碼與安裝程式一起使用：  

    -   使用命令列選項 **/SCRIPT** 執行安裝程式，並指定指令檔  

    -   必須使用必要的金鑰與值設定指令碼檔  

    如需自動安裝管理中心網站或主要站台，指令檔必須設定下列區段：  

    -   識別    
    -   選項    
    -   SQLConfigOptions    
    -   HierarchyOptions    

    -   CloudConnectorOptions  

    若要復原站台，您必須使用指令檔的下列區段：  

    -   識別  

    -   復原

     如需備份及復原的詳細資訊，請參閱＜備份及復原 Configuration Manager＞主題中的＜自動站台復原指令碼檔金鑰＞一節。  

    檢視[自動安裝指令檔索引鍵](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended)以取得要在自動安裝指令檔中使用的索引鍵和值清單。  

## <a name="about-the-command-line-script-file"></a>關於命令列指令檔  

 若要自動安裝 Configuration Manager，您可以使用命令列選項 **/SCRIPT** 執行安裝程式，並指定包含安裝選項的指令碼檔。 這個方法支援下列工作：  

-   安裝管理中心網站  

-   安裝主要站台  

-   安裝 Configuration Manager 主控台  

-   復原站台  

> [!NOTE]  
>  您無法使用自動執行指令碼檔，將評估網站升級為 Configuration Manager 的授權安裝。  

**建立指令碼**：  
當您[執行安裝程式以透過使用者介面安裝站台](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)時，會自動建立安裝指令碼。  確認精靈 [摘要]  頁面上的設定：  

-   安裝程式會建立指令碼 **%TEMP%\ConfigMgrAutoSave.ini**。  您可以在使用前先重新命名這個檔案，但它副檔名必須保留為 .ini 檔案。  

-   自動安裝指令碼包含您在精靈中選取的設定。  

-   建立指令碼後，您就可以修改指令碼以安裝階層中的其他網站。  

-   然後即可使用此指令碼來執行 Configuration Manager 的自動安裝。  

指令碼檔提供的資訊與 [安裝精靈] 提示的資訊相同，但沒有預設值。   
所有值必須針對適用於您所使用之安裝類型的安裝識別碼進行指定。  

當安裝程式建立自動安裝指令碼時，會填入您在安裝期間輸入的產品金鑰值。 此值可以是有效的產品金鑰，若是安裝 Configuration Manager 的評估版，則為 EVAL。 指令碼中所填入的產品金鑰值，可用來完成必要條件檢查。  

當安裝程式啟動實際的網站安裝時，會再次寫入自動建立的指令碼，以清除所建立指令碼中的產品金鑰值。 為新站台的自動安裝使用指令碼之前，可以編輯指令碼，以提供有效的產品金鑰，或指定 Configuration Manager 的評估安裝。  

**指令碼包含區段名稱、索引鍵名稱和值：**  

-   必要的區段金鑰名稱，取決於指令碼處理的安裝類型。  

-   區段中金鑰的順序與檔案內區段的順序都不重要。  

-   金鑰不區分大小寫  

-   提供金鑰的值時，金鑰名稱後必須加上等號 (=) 與金鑰的值。  

> [!TIP]  
>  若要檢視一組完整選項，請參閱[安裝程式和指令碼的命令列選項](../../../../core/servers/deploy/install/command-line-options-for-setup.md)。  

## <a name="to-use-the-script-setup-command-line-option"></a>若要使用 /SCRIPT 安裝命令列選項：

-   您必須使用安裝指令碼檔，並在 **/SCRIPT** 安裝命令列選項後面，指定檔案名稱。  

    -   檔案名稱的副檔名，必須是 **.ini** 。  

    -   當您參考命令提示字元的安裝設定檔時，必須提供檔案的完整路徑。 例如，若您將安裝初始設定檔命名為 Setup.ini，並將其儲存在 C:\Setup 資料夾中，則請在命令提示字元處輸入：  **setup /script c:\setup\setup.ini**  

-   執行安裝程式的帳戶，在電腦上必須具有系統管理認證。 使用自動安裝指令瑪執行安裝程式時，請使用 **Run as administrator**啟動命令提示字元。  



<!--HONumber=Nov16_HO1-->


