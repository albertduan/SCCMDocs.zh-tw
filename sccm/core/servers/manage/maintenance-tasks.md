---
title: "維護工作 | System Center Configuration Manager"
description: "了解要針對 Configuration Manager 站台和階層執行哪些維護工作，以及何時執行這些工作。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ac47f1b88a89a42bb51b87b36147b731e37a5824


---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>System Center Configuration Manager 的維護工作

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 站台與階層需要定期維護與監視，才能持續提供有效的服務。 定期維護可確保硬體、軟體與 Configuration Manager 資料庫能持續正確且有效率地運作。 最佳化效能可大幅降低失敗的風險。  

 若要設定警示，並使用狀態系統監視 Configuration Manager 的健全狀況，請參閱[使用 System Center Configuration Manager 的警示和狀態系統](../../../core/servers/manage/use-alerts-and-the-status-system.md)。  

-   [維護工作](#bkmk_MTs)  

##  <a name="a-namebkmkmtsa-maintenance-tasks"></a><a name="bkmk_MTs"></a> 維護工作  
 執行定期維護非常重要，因為這能確保正確的網站運作。 維護記錄以記錄執行維護的日期、執行者以及工作執行時與維護相關的意見。  

### <a name="when-to-perform-common-maintenance-tasks"></a>執行常見維護工作的時機  
 若要維護網站，請考慮每日、每週執行定期維護，並針對某些工作排定更有規律的排程。 常見維護可包括內建維護工作與其他工作，如帳戶維護，以維護其遵守您的公司原則。  

 使用以下資訊作為指南，協助您規劃執行不同維護工作的時機。 使用這些清單作為起始點，並新增任何您可能需要的額外工作。  

**每日工作**   
以下是您可考慮每天執行的維護工作：  

-   確認排程每日執行的預先定義維護工作都成功執行  

-   檢查 Configuration Manager 資料庫狀態  

-   檢查站台伺服器狀態  

-   檢查 Configuration Manager 站台系統收件匣中是否有檔案積存狀況  

-   檢查站台系統狀態  

-   檢查站台系統上的作業系統事件記錄檔  

-   檢查站台資料庫電腦上的 SQL Server 錯誤記錄檔  

-   檢查系統效能  

-   檢查 Configuration Manager 警示  

**每週工作**   
以下是您可考慮每週執行的維護工作：  

-   確認排程每週執行的預先定義維護工作都成功執行。  

-   從站台系統刪除不必要檔案  

-   如有必要，產生並發佈使用者報告  

-   備份應用程式、安全性與系統事件記錄檔，並將之清除  

-   檢查站台資料庫大小，並確認站台資料庫伺服器上有足夠的磁碟空間，讓站台資料庫有成長空間  

-   根據您的 SQL Server 維護規劃，在站台資料庫上執行 SQL Server 資料庫維護  

-   檢查所有站台系統上的可用磁碟空間  

-   在所有站台系統上執行磁碟重組工具  

**定期工作**   
某些工作並不需要在每日或每週維護時執行，但對於確保整體網站健全狀態來說，仍然十分重要，且能確保安全性與嚴重損壞修復規劃都是最新的。 以下是您可以考慮定期 (但不是每日或每週) 執行的維護工作：  

-   根據您的安全性規劃，若有必要，變更帳戶與密碼  

-   檢閱維護規劃，以驗證確實根據已設定的站台組態，正確且有效率的排程已排程維護工作  

-   檢閱 Configuration Manager 階層設計，找出必要的變更之處  

-   檢查網路效能，確保沒有出現會影響網站運作的變更  

-   驗證影響網站運作的 Active Directory 設定並未變更。 例如，驗證指派至用來作為 Configuration Manager 站台界限之 Active Directory 站台的子網路並未變更  

-   檢閱嚴重損壞修復規劃，找出任何必要變更  

-   根據測試實驗室中的嚴重損壞修復來執行站台復原，方法是使用由 [備份站台伺服器] 維護工作所建立之最新備份的備份複本  

-   檢查硬體，找出任何錯誤或可用的硬體更新  

-   檢查站台整體健全狀況  

###  <a name="a-namebkmkusemtsa-maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a> 維護站台資料庫的操作健全狀況  
 在 Configuration Manager 站台與階層執行您排程與設定的工作時，站台元件會持續將資料新增到 Configuration Manager 資料庫中。 隨著資料量增加，資料庫內的資料庫效能與資料庫內的可用磁碟空間也會減少。 您可以設定網站維護工作移除您不需要的老舊資料。  

 Configuration Manager 提供預先定義的維護工作，您可以藉由這些工作維護 Configuration Manager 資料庫的健全狀況。 在每個網站上，並非可用所有的維護工作。根據預設，會啟用某些維護工作，某些則不會，但所有工作都支援您可設定何時執行的排程。  

 大部分維護工作都會定期從 Configuration Manager 資料庫移除過時資料。 移除不需要的資料來降低資料庫大小也能改善資料庫效能與整體性，並提升網站與階層效率。 其他工作，如 [重建索引] ，可協助維護資料庫效率，此外，如 [備份網站伺服器]  之類的其他工作，則可協助您針對嚴重損壞修復做好準備。  

> [!IMPORTANT]  
>  規劃刪除資料工作的排程時，請考慮該資料跨階層的使用狀況。 在某個站台上執行刪除資料的工作時，會從 Configuration Manager 資料庫移除資訊，而這也會變更階層內所有站台的複寫。 這會影響依賴該資料的其他工作。 例如，在管理中心網站上，您可能會設定每月執行一次 [探索] 以識別出非用戶端電腦，並規劃在探索後的兩週內，在這些電腦上安裝 Configuration Manager 用戶端。 不過，在階層內的某個網站上，某位系統管理員設定每七天執行一次 [刪除過時探索資料] 工作，結果在探索非用戶端電腦的七天後，這些電腦皆已從 Configuration Manager 資料庫刪除。 回到管理中心網站，您準備好要在第 10 天於這些新電腦上推入安裝 Configuration Manager 用戶端。 不過，因為最近執行了 [刪除過時探索資料] 工作，並刪除 7 天以上的資料，導致您無法在資料庫上找到這些探索到的電腦。  

安裝 Configuration Manager 站台後，請檢閱可用的維護工作，並啟用進行操作所需要的工作。 檢閱每個工作的預設排程，並在必要時根據您的階層與環境修改排程以微調維護工作。 雖然每個工作的預設排程應能滿足絕大多數的環境，但仍請監視站台與資料庫的效能，並適時微調工作，以提升部署的效率。 規劃定期檢閱網站與資料庫效能，並重設維護工作與其排程以維護效率。  

#### <a name="configure-maintenance-tasks"></a>設定維護工作  
 每個 Configuration Manager 站台都支援協助維護站台資料庫操作效率的維護工作。 根據預設，每個網站中啟用數個維護工作和所有工作都支援獨立的排程。 維護工作個別設定每個站台和套用至資料庫在該網站。不過，某些工作，例如 **刪除過時的探索資料**, ，會影響在階層中的所有站台可用的資訊。  

 只有您可以在站台中設定的維護工作才會顯示在 Configuration Manager 主控台中。 如需站台類型的完整維護工作清單，請參閱 [System Center Configuration Manager 的維護工作參考](../../../core/servers/manage/reference-for-maintenance-tasks.md)  

 使用下列程序來協助您設定維護工作的一般設定。  

###### <a name="to-configure-maintenance-tasks-for-configuration-manager"></a>若要設定 Configuration Manager 的維護工作  

1.  在 Configuration Manager 主控台中，巡覽至 [系統管理] > [站台設定] >[站台]。  

2.  選取包含您想要設定的維護工作的網站。  

3.  在 **Home** 索引標籤的 **設定** 群組中，按一下 **站台維護**, ，然後選取您想要設定的維護工作。  

    > [!TIP]  
    >  只可使用的工作在選取的站台會顯示。  

4.  若要設定工作，請按一下 **編輯**, ，確保 **啟用這項工作** 核取方塊已選取和設定工作執行的排程。 如果工作也會刪除舊的資料，設定在工作執行時將會從資料庫刪除資料的存在時間。 按一下 **確定** 來關閉工作 **屬性**。  

    > [!NOTE]  
    >  針對 **刪除過時的狀態訊息**, ，設定的設定狀態篩選規則時刪除的資料存在時間。  

5.  若要啟用或停用工作而不需要編輯工作內容，請按一下 **啟用** 或 **停用** ] 按鈕。 變更的按鈕標籤視工作的目前組態而定。  

6.  當您完成設定維護工作時，按一下 **確定** 若要完成此程序。



<!--HONumber=Nov16_HO1-->


