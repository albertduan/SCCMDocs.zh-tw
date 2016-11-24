---
title: "升級用戶端 | Windows | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中升級 Windows 電腦上的用戶端。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
caps.latest.revision: 11
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2b1600e6f04095506f18f4c2cd0988a320fbb951


---
# <a name="how-to-upgrade-clients-for-windows-computers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端

*適用於：System Center Configuration Manager (最新分支)*

您可以使用 Configuration Manager 中的用戶端安裝方法或自動用戶端升級功能，升級 Windows 電腦上的用戶端。 下列用戶端安裝方法可有效地在 Windows 電腦上升級用戶端軟體：  

-   群組原則安裝  

-   登入指令碼安裝  

-   手動安裝  

-   升級安裝  

 如果您想要使用用戶端安裝方法來升級用戶端，請在[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)中深入了解如何使用這些方法。  

> [!TIP]  
>  如果您從舊版的 Configuration Manager \(例如 Configuration Manager 2007 或 System Center 2012 Configuration Manager\) 升級伺服器基礎結構，建議您先完成伺服器升級 (包含安裝所有的最新分支更新)，然後再升級 Configuration Manager 用戶端。   最新的最新分支更新包含最新版本的用戶端，因此最好在您安裝所有要使用的 Configuration Manager 更新之後，執行用戶端升級。  

## <a name="use-automatic-client-upgrade"></a>使用自動用戶端升級  
 您也可以將 Configuration Manager 設定為當 Configuration Manager 識別出指派至 Configuration Manager 階層的用戶端版本比階層中所使用的版本低時，自動將用戶端軟體升級至最新 Configuration Manager 用戶端版本。 此案例包含當用戶端嘗試指派至 Configuration Manager 站台時，會將用戶端升級至最新版本。  

 用戶端可以在下列情況自動升級：  

-   用戶端版本比階層中使用的版本低。  

-   管理中心網站上的用戶端已安裝現有用戶端所沒有的語言組件。  

-   階層中的用戶端必要條件，與用戶端上安裝的版本不同。  

-   有一或多個用戶端安裝檔案的版本不同。  

> [!NOTE]  
>  您可以執行 [站台 - 用戶端資訊] 報告資料夾中的 [依用戶端版本列出的 Configuration Manager 用戶端計數] 報告，識別階層中不同版本的 Configuration Manager 用戶端。  

 Configuration Manager 預設會建立升級套件，其會自動傳送至階層中的所有發佈點。 如果您對管理中心網站上的用戶端套件進行變更 (例如新增用戶端語言組件)，則 Configuration Manager 會自動更新套件，並將其發佈至階層中的所有發佈點。 如果已啟用自動用戶端升級，則每個用戶端會自動安裝新的用戶端語言套件。  

> [!NOTE]  
>  Configuration Manager 不會自動將用戶端升級套件傳送至 Configuration Manager 雲端發佈點。  

 當您想要針對一小部分可能已被主要用戶端安裝方法遺漏的用戶端電腦進行升級時，自動用戶端升級就非常有用。 例如，您已完成初始用戶端升級，但某些用戶端在升級部署期間離線。 當這些電腦下次啟用時，您就可以使用此方法來升級電腦上的用戶端。  

 使用下列程序，設定自動用戶端升級。 自動用戶端升級必須在管理中心網站設定，而此設定適用於階層中的所有用戶端。  

#### <a name="to-configure-automatic-client-upgrades"></a>設定自動用戶端升級  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [網站] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [階層設定] 。  

4.  在 [階層設定內容]  對話方塊的 [用戶端升級]  索引標籤中，檢閱實際執行用戶端的版本與日期，並確定其為您想要用來升級 Windows 電腦的版本。  如果其不是您預期見到的用戶端版本，您可能需要將實際執行前用戶端升階為實際執行用戶端。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中測試進入生產階段前集合的用戶端升級](../../../../core/clients/manage/upgrade/test-client-upgrades.md)。  

5.  按一下 [使用實際執行用戶端升級階層中的所有用戶端]  ，然後在確認對話方塊中按一下 [確定]  。  

6.  如果您不想要將用戶端升級套用至伺服器，按一下 [不升級伺服器] 。  

7.  指定電腦收到用戶端原則後必須在幾天內升級用戶端。 在指定的天數內，用戶端會以隨機間隔進行升級。 這可避免大量用戶端電腦同時進行升級的情況。

    > [!NOTE]
    > 電腦必須處於執行中，才能升級用戶端。 如果電腦未在排程接收升級時執行，則不會升級。 相反地，重新啟動電腦時，排程另一個升級在允許天數內的任意時間執行。 如果這在升級的天數到期之後發生，則會排程在重新啟動電腦之後的 24 小時內的任意時間升級。
    >     
    > 基於這項行為，如果隨機排程的升級時間不在正常工作時間內，則升級經常會在工作日結束關機的電腦可能需要比預期時間還要長的時間。

8.  如果您要將用戶端安裝套件複製到已經啟用預先設置內容的發佈點，請按一下 [將用戶端安裝套件自動發佈至針對預先設置內容啟用的發佈點] 。  

9. 按一下 [確定]  儲存設定，然後關閉 [階層設定內容]  對話方塊。 用戶端接著下載原則時，就會收到這些設定。  



<!--HONumber=Nov16_HO1-->

