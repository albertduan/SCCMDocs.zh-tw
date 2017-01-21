---
title: "安裝主控台 | System Center Configuration Manager"
description: "閱讀如何安裝 Configuration Manager 主控台以連線至管理中心網站或主要站台。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1483e35a397667a340605c0454c1835ec6067d9e

---
# <a name="install-system-center-configuration-manager-consoles"></a>安裝 System Center Configuration Manager 站台

*適用於：System Center Configuration Manager (最新分支)*


系統管理使用者會使用 System Center Configuration Manager 主控台來管理 Configuration Manager 環境。 每個 Configuration Manager 主控台都可以連線至管理中心網站或主要站台的資訊。 不過，您無法將 Configuration Manager 主控台連線至次要站台。


> [!NOTE]  
>  針對正在執行主控台之系統管理使用者所顯示的物件，會依指派至系統管理使用者的權限而有所不同。 如需以角色為基礎之系統管理的詳細資訊，請參閱 [System Center Configuration Manager 以角色為基礎之系統管理的基礎](../../../../core/understand/fundamentals-of-role-based-administration.md)。  

 您可以在 [安裝精靈] 的站台伺服器安裝期間，或執行獨立應用程式，來安裝 Configuration Manager 主控台。  

 請使用以下程序，利用獨立應用程式安裝 Configuration Manager 主控台。  

## <a name="to-install-a-configuration-manager-console"></a>安裝 Configuration Manager 主控台  

1.  確認執行 Configuration Manager 主控台應用程式的系統管理使用者具有以下安全性權限：  

    -   執行主控台之電腦上的**本機系統管理員** 權限。  

    -   Configuration Manager 主控台安裝檔位置的**讀取**權限。  

2.  瀏覽至下列其中一個位置：  

    -   從 Configuration Manager 來源媒體瀏覽至 **&lt;ConfigMgrSourceFiles\>\Smssetup\Bin\I386**。  

    -   在站台伺服器上，瀏覽至 **&lt;ConfigMgrSiteServerInstallationPath\>\Tools\ConsoleSetup**。  

    > [!TIP]  
    >  最佳做法是從站台伺服器，而不是從 System Center Configuration Manager 安裝媒體起始 Configuration Manager 主控台安裝。 站台伺服器安裝方法會將 Configuration Manager 主控台安裝檔案與站台的支援語言套件，複製到 **Tools\ConsoleSetup** 子資料夾。 如果您從安裝媒體安裝 Configuration Manager 主控台，則無論站台伺服器上支援的語言為何，或電腦上執行的作業系統語言設定為何，此安裝方法一律會安裝英文版。 您也可以選擇將 **ConsoleSetup** 資料夾複製到替代位置，以啟動安裝。  

3.  按兩下 [consolesetup.exe] 。 此時會開啟 Configuration Manager 主控台安裝精靈。  

    > [!IMPORTANT]  
    >  請一律使用 consolesetup.exe 安裝 Configuration Manager 主控台。 雖然 Configuration Manager 主控台可藉由執行 AdminConsole.msi 加以安裝，但此方法不會執行必要條件或相依性檢查，且安裝可能會不正確。  

4.  在開啟頁面上，按 [下一步] 。  

5.  在 [站台伺服器] 頁面上，指定 Configuration Manager 主控台要連線之站台伺服器的完整網域名稱 (FQDN)。  

6.  在 [安裝資料夾] 頁面上，指定 Configuration Manager 主控台的安裝資料夾。 資料夾路徑結尾不可有空格，路徑中不可有 Unicode 字元。  

7.  在 [客戶經驗改進計畫]  頁面上，選擇是否要加入客戶經驗改進計畫。  

8.  在 [安裝準備就緒] 頁面上，按一下 [安裝] 即可安裝 Configuration Manager 主控台。  

## <a name="to-install-a-configuration-manager-console-from-a-command-prompt"></a>從命令提示字元處安裝 Configuration Manager 主控台  

1.  在安裝 Configuration Manager 主控台的伺服器上，開啟命令提示字元視窗，並瀏覽至下列其中一個位置：  

    -   **&lt;ConfigMgrSiteServerInstallationPath\>\Tools\ConsoleSetup**  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  當您從命令提示字元安裝 Configuration Manager 主控台時，無論電腦上執行的作業系統語言設定為何，一律都會安裝英文版。 若要用其他語言安裝 Configuration Manager 主控台，您必須使用先前的程序進行安裝。  

2.  輸入 **consolesetup.exe** ，並選擇下列命令列選項。  

|  命令列選項     | 說明     |
  | :------------- | :------------- |
  |/q|自動安裝 Configuration Manager。 只有在使用此選項時，才需要 **EnableSQM**、 **TargetDir**和 **DefaultSiteServerName** 選項。|  
  |/uninstall|解除安裝 Configuration Manager 主控台。 當您搭配 **/q** 選項使用時，必須指定此選項。|  
  |LangPackDir|指定包含語言檔案的資料夾路徑。 您可以使用 **安裝程式下載程式** 來下載語言檔案。 如果未使用此選項，則安裝程式會在目前資料夾中尋找語言資料夾。 如果沒有找到語言資料夾，則安裝程式只會繼續安裝英文版。 如需詳細資訊，請參閱[安裝程式下載程式](/sccm/core/servers/deploy/install/setup-downloader)。|  
  |TargetDir|指定安裝資料夾以安裝 Configuration Manager 主控台。 只有在使用 **/q** 選項時，才需要此選項。|  
  |EnableSQM|指定是否加入客戶經驗改進計畫 (CEIP)。 使用 1 的值可加入客戶經驗改進計畫，0 的值則為不加入。 只有在使用 **/q** 選項時，才需要此選項。|  
  |DefaultSiteServerName|指定主控台開啟時所連線的網站伺服器 FQDN。 只有在使用 **/q** 選項時，才需要此選項。|  


  **使用範例：**  
  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  



<!--HONumber=Nov16_HO1-->


