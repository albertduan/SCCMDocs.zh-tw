---
title: "建立工作順序以升級作業系統 | Configuration Manager"
description: "System Center Configuration Manager 中的工作順序可以將作業系統從 Windows 7 或更新版本自動升級至 Windows 10。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fe70a3bfddcc0638a27eccb04324c4e6e2ace1d4


---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中建立工作順序以升級作業系統

*適用於︰System Center Configuration Manager (最新分支)*

使用 System Center Configuration Manager 中的工作順序，將目的地電腦上的作業系統從 Windows 7 或更新版本自動升級至 Windows 10。 您建立的工作順序，會參考要安裝在目的地電腦上的作業系統映像，以及其他任何內容，例如應用程式或要安裝的軟體更新。 升級作業系統的工作順序是[將 Windows 升級至最新版本](upgrade-windows-to-the-latest-version.md)案例的一部分。  

##  <a name="a-namebkmkupgradeosa-create-a-task-sequence-to-upgrade-an-operating-system"></a><a name="BKMK_UpgradeOS"></a> 建立工作順序以升級作業系統  
 若要將電腦上的作業系統升級至 Windows 10，您可以建立工作順序，並在 [建立工作順序精靈] 中選取 [從升級套件升級作業系統]  。 該精靈會加入升級作業系統、套用軟體更新以及安裝應用程式的步驟。 建立工作順序之前，必須備妥下列事項：  

-   **必要**  

     - Configuration Manager 主控台中必須提供 Windows 10 [作業系統升級套件](../get-started/manage-operating-system-upgrade-packages.md)。  

-   **必要 (如果有用到)**  

    -   [軟體更新](../../sum/get-started/synchronize-software-updates.md)必須在 Configuration Manager 主控台中進行同步處理。  

    -   Configuration Manager 主控台中必須新增[應用程式](../../apps/deploy-use/create-applications.md)。  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>建立升級作業系統的工作順序  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序]  啟動 [建立工作順序精靈]。  

4.  在 [建立新的工作順序]  頁面上，按一下 [從升級套件升級作業系統] ，然後按一下 [下一步] 。  

5.  在 [工作順序資訊]  頁面上指定下列設定，然後按 [下一步] 。  

    -   **工作順序名稱**：指定識別工作順序的名稱。  

    -   **描述**：指定工作順序所執行工作之說明。  

6.  在 [升級 Windows 作業系統]  頁面上，指定下列設定，然後再按一下 [下一步] 。  

    -   **升級套件**：指定包含作業系統升級來源檔案的升級套件。 查看 [內容]  窗格的資訊，可確認已選取正確的升級套件。 如需詳細資訊，請參閱[管理作業系統升級套件](../get-started/manage-operating-system-upgrade-packages.md)。  

    -   **版本索引**：如果套件中有多個作業系統版本索引，請選取所需的版本索引。 依預設，會選取第一個項目。  

    -   **產品金鑰**：指定要安裝之 Windows 作業系統的產品金鑰。 您可以指定編碼的大量授權金鑰和標準產品金鑰。 如果您使用非編碼的產品金鑰，則必須以破折號 (-) 分隔字元，每 5 個字元為一組。 例如： *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*。 當大量授權版本進行升級時，不需要產品金鑰。 只有在零售版的 Windows 版本升級時，才需要產品金鑰。  

7.  在 [包含更新]  頁面上，指定要安裝必要的軟體更新、所有軟體更新或不安裝軟體更新，然後按 [下一步] 。 如果您指定安裝軟體更新，Configuration Manager 只會將目標軟體更新安裝至目的地電腦為其成員的集合。  

8.  在 [安裝應用程式]  頁面上，指定要安裝在目的地電腦上的應用程式，然後按 [下一步] 。 如果您指定多個應用程式，也可以指定工作順序在特定應用程式安裝失敗時繼續執行。  

9. 完成精靈。  

## <a name="download-package-content-task-sequence-step"></a>下載套件內容的工作順序步驟  
 在下列案例中的 [升級作業系統] 步驟之前，可以使用[下載套件內容](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)步驟：  

-   您使用可同時搭配 x86 和 x64 平台使用的單一升級工作順序。 若要執行此作業，請在 **準備升級** 群組中加入兩個 **下載套件內容** 步驟，這些步驟設有條件，可偵測用戶端架構，僅下載適用的作業系統升級套件。 將每個 **下載套件內容** 步驟設定為使用相同的變數，並使用該變數來代表 **升級作業系統** 步驟中的媒體路徑。  

-   若要動態下載適用的驅動程式套件，請使用兩個 **下載套件內容** 步驟，並設定條件來偵測每個驅動程式套件適用的硬體類型。 將每個 [下載封裝內容]  步驟設定成使用相同的變數，並使用這個變數來表示 [升級作業系統]  步驟之 [驅動程式] 區段中的 [分段內容]  值。  

   > [!NOTE]
   > 有多個套件時，Configuration Manager 會在變數名稱後面加上數值尾碼。 例如，如果您指定 %mycontent% 變數作為自訂變數，這會是所有參照內容儲存位置的根目錄 (可以是多個套件)。 當您在後續步驟 (例如 [升級作業系統]) 中參考此變數時，會使用加上數值尾碼的變數。 在這個範例中，%mycontent01% 或 %mycontent02% 中的數字會與套件在這個步驟中列出的順序對應。

## <a name="optional-post-processing-task-sequence-steps"></a>選擇性的後續處理工作順序步驟  
 建立工作順序之後，可新增其他步驟來解除安裝出現已知相容性問題的應用程式，或新增重新啟動電腦之後要執行的後續處理動作，如此即已成功升級為 Windows 10。 在工作順序的後續處理群組中新增下列其他步驟。  

> [!NOTE]  
>  因為這個工作順序並非線性順序，所以根據是否成功升級用戶端電腦，或者是否必須將用戶端電腦復原成啟動所用的作業系統版本，會出現不同的步驟，而可能影響工作順序的結果。  

## <a name="optional-rollback-task-sequence-steps"></a>選擇性的復原工作順序步驟  
 重新啟動電腦之後若升級程序出錯，安裝程式會將升級復原為先前的作業系統，而工作順序會繼續執行復原群組中的任何步驟。 建立工作順序之後，可對復原群組新增選擇性的步驟。  

## <a name="folder-and-files-removed-after-computer-restart"></a>在重新啟動電腦之後移除的資料夾和檔案  
 如果將作業系統升級至 Windows 10 的工作順序以及工作順序中的所有其他步驟完成，則除非重新啟動電腦，否則不會移除後置處理和復原指令碼。  這些指令檔未包含機密資訊。  



<!--HONumber=Nov16_HO1-->


