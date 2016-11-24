---
title: "安裝程式下載程式 | System Center Configuration Manager"
description: "請閱讀這個獨立應用程式，設計成確保您的站台安裝使用最新版本的金鑰安裝檔案。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 574e4d450126d2c4411292b6dd52e18049d296f6

---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>System Center Configuration Manager 的安裝程式下載程式

*適用於：System Center Configuration Manager (最新分支)*

在執行安裝程式安裝或升級 System Center Configuration Manager 站台之前，您可以使用您想要安裝之 Configuration Manager 版本中的獨立應用程式 (**Setupdl.exe**) 下載安裝程式所需的已更新安裝程式檔案。  

使用更新的安裝程式檔案，便能確保您的站台安裝會使用最新版本的金鑰安裝檔案：  

-   如果您在啟動安裝程式前使用安裝程式下載程式來下載檔案，請指定要包含檔案的資料夾。  

-   您用來執行安裝程式下載程式的帳戶必須具有下載資料夾的**完全控制**權限。  

-   在您執行安裝程式來安裝或升級站台時，可以加以指引，讓其使用您先前所下載檔案的這份本機複本。 如此一來，在您開始安裝或升級站台時，安裝程式便不需連線至 Microsoft。  

-   您可以使用相同的安裝程式檔案本機複本，用於後續的站台安裝或升級作業。  

下列類型的檔案是透過安裝程式下載程式所下載：  

-   所需的必要條件可轉散發檔案  

-   語言套件  

-   安裝程式的最新產品更新  

有兩個選項可以執行安裝程式下載程式：  

## <a name="run-setup-downloader-with-the-user-interface"></a>使用使用者介面來執行安裝程式下載程式  

1.  在可存取網際網路的電腦上，開啟 Windows 檔案總管，並瀏覽至 **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

2.  按兩下 [Setupdl.exe]。 安裝程式下載程式便會開啟。  

3.  指定要裝載更新的安裝檔案的資料夾路徑，然後按一下 [下載]。 安裝程式下載程式會確認目前在下載資料夾中的檔案，並且只下載遺漏的檔案或是比現有檔案更新的檔案。 安裝程式下載程式會針對下載的語言建立子資料夾。 如果資料夾不存在，安裝程式下載程式將建立資料夾。  

4.  在磁碟機 C 的根目錄中檢視 **ConfigMgrSetup.log** 檔案，檢閱下載的結果。  

## <a name="run-setup-downloader-from-a-command-prompt"></a>從命令提示字元中執行安裝程式下載程式  

1.  開啟 [命令提示字元] 視窗，並瀏覽至 **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

2.  執行 **setupdl.exe** 開啟安裝程式下載程式。 您可以選擇性地搭配使用下列命令列選項與 setupdl.exe：  

    -   **/VERIFY**：使用此選項可驗證下載資料夾中的檔案，包括語言檔案。 在磁碟機 C 的根目錄中，檢閱 ConfigMgrSetup.log 檔案中列出的過期檔案。 如果您使用此選項，則不會下載任何檔案。  

    -   **/VERIFYLANG**：使用此選項可驗證下載資料夾中的語言檔案。 在磁碟機 C 的根目錄中，檢閱 ConfigMgrSetup.log 檔案中列出的過期語言檔案。  

    -   **/LANG**：使用此選項只會將語言檔案下載至下載資料夾。  

    -   **/NOUI**：使用此選項可啟動安裝程式下載程式，但不顯示使用者介面。 使用此選項時，您必須在命令列中指定**下載路徑**。  

    -   **&lt;下載路徑\>**：您可以指定下載資料夾的路徑，以自動啟動驗證或下載程序。 使用 **/NOUI** 選項時，必須指定下載路徑。 若未指定下載路徑，則必須在安裝程式下載程式開啟時指定路徑。 如果資料夾不存在，安裝程式下載程式將建立資料夾。  

    使用範例：  

    -   **setupd &lt;下載路徑\>**  

        -   安裝程式下載程式會啟動、驗證指定下載資料夾中的檔案，並且只下載遺漏的檔案或是比現有檔案更新的檔案  

    -   **setupdl /VERIFY &lt;下載路徑\>**  

        -   安裝程式下載程式會啟動，並驗證指定下載資料夾中的檔案  

    -   **setupdl /NOUI &lt;下載路徑\>**  

        -   安裝程式下載程式會啟動、驗證指定下載資料夾中的檔案，並且只下載遺漏的檔案或是比現有檔案更新的檔案  

    -   **setupdl /LANG  &lt;DownloadPath\>**  

        -   安裝程式下載程式會啟動、驗證指定下載資料夾中的語言檔案，並且只下載遺漏的語言檔案或是比現有檔案更新的檔案  

    -   **setupdl /VERIFY**  

        -   啟動安裝程式下載程式，然後您必須指定下載資料夾的路徑。 接下來，在您按一下 [驗證] 之後，安裝程式下載程式會驗證下載資料夾中的檔案  

3.  在磁碟機 C 的根目錄中檢視 **ConfigMgrSetup.log** 檔案，檢閱下載結果  



<!--HONumber=Nov16_HO1-->


