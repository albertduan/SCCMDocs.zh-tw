---
title: "設定用戶端設定 | System Center Configuration Manager"
description: "選取 System Center Configuration Manager 的用戶端設定。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9e3162e04da90748379145e37f6b378badab97d3

---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中設定用戶端設定

*適用對象：System Center Configuration Manager (最新分支)*

您是在 Configuration Manager 主控台 [管理] 工作區的 [用戶端設定] 節點中，管理 System Center Configuration Manager 的所有用戶端設定。 若您想要設定在階層中未套用任何自訂設定之所有使用者和裝置的設定，可修改預設設定。 如果您只想要將不同的設定套用至部分使用者或裝置，可建立自訂設定並將這些設定部署至集合。  

> [!NOTE]  
>  您也可以使用組態項目管理用戶端，以評估、追蹤和補救裝置的組態相容性。 如需詳細資訊，請參閱 [Ensure device compliance with System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md) (使用 System Center Configuration Manager 確保裝置相容性)。  

##  <a name="a-namebkmkdefaultclientsettingsa-how-to-configure-the-default-client-settings"></a><a name="BKMK_DefaultClientSettings"></a> 如何設定預設的用戶端設定  

 利用下列程序，為階層中的所有用戶端設定預設的用戶端設定。  

#### <a name="to-configure-the-default-client-settings"></a>設定預設的用戶端設定  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] ，然後選取 [預設用戶端設定] 。  

3.  在 [首頁]  索引標籤上，按一下 [內容] 。  

4.  在瀏覽窗格中，檢視及設定每一組設定的用戶端設定。 如需各項設定的詳細資訊，請參閱[關於 Configuration Manager 中的用戶端設定](../../../core/clients/deploy/about-client-settings.md)。  

5.  按一下 **確定** 關閉 **預設用戶端設定** 對話方塊。  

 用戶端電腦將會在下一次下載用戶端原則時進行這些設定。 若要起始單一用戶端的原則抓取，請參閱[如何管理 System Center Configuration Manager 中的用戶端](../../../core/clients/manage/manage-clients.md)中的[起始 Configuration Manager 用戶端的原則抓取](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

##  <a name="a-namebkmkcustomclientsettingsa-how-to-create-and-deploy-custom-client-settings"></a><a name="BKMK_CustomClientSettings"></a> 如何建立及部署自訂用戶端設定  
 利用下列程序設定及部署所選使用者或裝置集合的自訂設定。 當您部署這些自訂設定時，這些設定會覆寫預設用戶端設定。  

> [!NOTE]  
>  在開始此程序之前，請先確定您擁有包含這些需要自訂用戶端設定之使用者或裝置的集合。  

#### <a name="to-configure-and-deploy-custom-client-settings"></a>設定及部署自訂用戶端設定  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立自訂用戶端設定] ，然後根據您要建立裝置或使用者的自訂用戶端設定，按以下其中一個選項：  

    -   **建立自訂用戶端裝置設定**  

    -   **建立自訂用戶端使用者設定**  

4.  在 [建立自訂裝置設定]  或 [建立自訂使用者設定]  對話方塊中，指定自訂設定的唯一名稱，以及選擇性的描述。  

5.  選取一個或多個顯示設定群組的可用核取方塊。  

6.  按一下瀏覽窗格中的第一個群組設定，然後檢視及設定可用的自訂設定。 針對其餘的群組設定重複此程序。 如需各項用戶端設定的資訊，請參閱[關於 Configuration Manager 中的用戶端設定](../../../core/clients/deploy/about-client-settings.md)。  

7.  按一下 [確定]  ，關閉 [建立自訂裝置設定]  或 [建立自訂使用者設定]  對話方塊。  

8.  選取您剛才建立的自訂用戶端設定。 在 [首頁]  索引標籤的 [用戶端設定]  群組中，按一下 [部署] 。  

9. 在 [選取集合]  對話方塊中，選取包含要用自訂設定進行設定之裝置或使用者的集合，然後按一下 [確定] 。 按一下詳細資料窗格中的 [部署]  索引標籤，即可驗證所選取的集合。  

10. 檢視您剛才建立的自訂用戶端設定的順序。 如果您有多個自訂用戶端設定，則這些設定會依照其順序編號套用。 如果發生任何衝突，順序編號最小的設定會覆寫其他設定。 若要變更順序編號，請在 [首頁]  索引標籤的 [用戶端設定]  群組中，按一下 [將項目往上移]  或 [將項目往下移] 。  

 用戶端電腦將會在下一次下載用戶端原則時進行這些設定。 若要起始單一用戶端的原則抓取，請參閱[如何管理 System Center Configuration Manager 中的用戶端](../../../core/clients/manage/manage-clients.md)中的[起始 Configuration Manager 用戶端的原則抓取](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

##  <a name="a-namebkmkresultantclientsettingsa-how-to-view-resultant-client-settings"></a><a name="BKMK_ResultantClientSettings"></a> 如何檢視結果用戶端設定  
 當有多個用戶端設定部署至相同裝置、使用者或使用者群組時，設定的優先順序和組合可能會很複雜。 利用下列程序檢視所計算的結果用戶端設定。  

#### <a name="to-view-the-resultant-client-settings"></a>檢視結果用戶端設定  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [裝置] 、[使用者] 或 [使用者集合] 。  

3.  選取裝置、使用者或使用者群組，然後在 [用戶端設定]  群組中，選取 [結果用戶端設定] 。  此外，您也可以在裝置、使用者或使用者群組上按一下右鍵，選取 [用戶端設定] ，再按一下 [結果用戶端設定] 。  

4.  從左窗格選取用戶端設定，隨即顯示結果設定。  

    > [!NOTE]  
    >  若要檢視結果用戶端設定，登入的使用者必須具有用戶端設定的讀取權限。  

    > [!NOTE]  
    >  顯示的結果設定皆為唯讀。 若要修改任何設定，請使用上述程序。  



<!--HONumber=Nov16_HO1-->


