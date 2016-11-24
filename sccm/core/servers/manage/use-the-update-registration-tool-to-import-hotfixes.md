---
title: "更新註冊工具 | System Center Configuration Manager"
description: "了解何時以及如何使用更新註冊工具，將更新手動匯入 Configuration Manager 主控台。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 176c1d7055ae8706b92886d59d8a048dd867c18b


---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-system-center-configuration-manager"></a>使用更新註冊工具將 Hotfix 匯入 System Center Configuration Manager

*適用於：System Center Configuration Manager (最新分支)*

Configuration Manager 的某些更新無法從 Microsoft 雲端服務取得，只能從頻外取得。 用以解決特定問題的有限版本 Hotfix 就是一例。   
當您必須安裝頻外版本且更新或 Hotfix 檔案名稱的結尾是 **update.exe** 副檔名時，請使用**更新註冊工具**，將更新手動匯入 Configuration Manager 主控台。 此工具可讓您擷取更新套件並傳送到站台伺服器，然後向 Configuration Manager 主控台註冊該項更新。  

 如果 Hotfix 檔案具有 **.exe** 副檔名 (而非 **update.exe**)，請參閱[使用 Hotfix 安裝程式來安裝 System Center Configuration Manager 更新](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)。  

> [!NOTE]  
>  本主題提供有關如何安裝可更新 System Center Configuration Manager 之 Hofix 的一般指引。 如需有關特定 Hotfix 或更新的詳細資料，請參閱「Microsoft 支援服務」中其對應的知識庫 (KB) 文章。  

 **使用更新註冊工具的必要條件：**  

-   只有結尾是 **.update.exe** 副檔名的頻外更新可以藉由此工具來安裝。  

-   此工具是獨立式工具，其中您可以直接從 Microsoft 取得個別的更新  

-   此工具並不倚賴服務連接點的模式  

-   此工具必須在裝載服務連接點的電腦上執行  

-   執行此工具的電腦 (服務連接點電腦) 必須安裝 .NET Framework 4.52  

-   您用來執行此工具的帳戶，必須具有裝載服務連接點之電腦 (此工具執行所在的電腦) 的「本機系統管理員」權限。  

-   您用來執行此工具的帳戶必須具有裝載服務連接點之電腦上下列資料夾的「寫入」權限：**&lt;ConfigMgr 安裝目錄\>\EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>使用更新註冊工具  

1.  在裝載服務連接點的電腦上：  

    -   以系統管理權限開啟命令提示字元，然後將目錄變更至包含 **&lt;產品\>-&lt;產品版本\>-&lt;知識庫文章識別碼\>-ConfigMgr.Update.exe** 的位置。  

2.  執行下列命令來啟動更新註冊工具︰  

    -   **&lt;產品\>-&lt;產品版本\>-&lt;知識庫文章識別碼\>-ConfigMgr.Update.exe**  

    註冊 Hotfix 之後，它會在 24 小時內於主控台中顯示為新的更新。  您可以使用下列其中一項操作來加速此程序︰  

    -   使用版本 1511 時︰在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [雲端服務] > [更新與服務]，然後選取 [Start update discovery process immediately] (立即開始更新探索程序)。  這會在完成註冊程序時立即開始匯入 Hotfix，讓它可供在主控台中使用。  

    -   使用版本 1602 和更新版本時︰在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [雲端服務] > [更新與服務]，然後按一下 [檢查更新]。  

    更新註冊工具會將其動作記錄到本機電腦上的 .log 檔案中。 此記錄檔的名稱與 Hotfix .exe 檔案相同，並且會寫入 **%SystemRoot%/Temp** 資料夾中。  

     註冊更新之後，您便可以關閉更新註冊工具。  

3.  開啟 Configuration Manager 主控台，然後瀏覽至 **[系統管理]** > **[雲端服務]** > **[更新及服務]**。 已匯入的 Hotfix 現在已可供安裝。 如需安裝更新的相關資訊，請參閱[安裝適用於 System Center Configuration Manager 的主控台內更新](../../../core/servers/manage/install-in-console-updates.md)。  



<!--HONumber=Nov16_HO1-->


