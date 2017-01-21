---
title: "監視憑證設定檔 | System Center Configuration Manager"
description: "了解如何監視 System Center Configuration Manager 憑證設定檔的相容性狀態。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
caps.latest.revision: 7
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bb72571596e77ce3069c1f6526fb3ba00fc9ecdc


---
# <a name="how-to-monitor-certificate-profiles-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中監視憑證設定檔

*適用於：System Center Configuration Manager (最新分支)*


為階層中的使用者部署 System Center Configuration Manager 憑證設定檔之後，即可使用下列程序監視憑證設定檔的相容性狀態：  

-   [如何在 Configuration Manager 主控台中檢視相容性結果](#BKMK_console)  

-   [如何使用報告檢視相容性結果](#BKMK_Reports)  

##  <a name="a-namebkmkconsolea-how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a> 如何在 Configuration Manager 主控台中檢視相容性結果  
 使用這個程序，在 System Center Configuration Manager 主控台中檢視已部署憑證設定檔的相容性詳細資料。  

> [!NOTE]  
>  若要監視 SCEP 憑證相容性，請不要使用 Configuration Manager 主控台，而改為使用 [如何使用報告檢視相容性結果](#BKMK_Reports)中所述的報表， 也就是使用報表節點 [公司資源存取] 下的憑證報表。  
>   
>  -   憑證發行歷程記錄  
> -   憑證即將到期的資產清單  
> -   依憑證發行狀態列出的資產清單  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>在 Configuration Manager 主控台中檢視相容性結果  

1.  在 System Center Configuration Manager 主控台中，按一下 [監視]。  

2.  在 [監視]  工作區中按一下 [部署] 。  

3.  在 [部署]  清單中，選取您想要檢閱其相容性資訊的憑證設定檔部署。  

4.  在主頁面上，您可以檢閱有關憑證設定檔相容性的摘要資訊。 若要檢視更詳細的資訊，請選取憑證設定檔，然後在 [首頁]  索引標籤的 [部署]  群組中，按一下 [檢視狀態]  以開啟 [部署狀態]  頁面。  

     [部署狀態]  頁面包含下列索引標籤：  

    -   **相容**：根據受影響的資產數目，顯示憑證設定檔的相容性。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點。 這個節點包含與此憑證設定檔相容的所有使用者。 [資產詳細資料]  窗格也顯示與這個設定檔相容的使用者。 按兩下清單中的使用者以顯示其他資訊。  

        > [!IMPORTANT]  
        >  如果憑證設定檔在用戶端裝置上不適用，就不會進行評估； 不過，仍會傳回為相容。  

    -   **錯誤**：根據受影響的資產數目，顯示所選憑證設定檔部署的所有錯誤清單。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點。 這個節點包含因為這個設定檔而產生錯誤的所有使用者。 當您選取使用者時，[資產詳細資料]  窗格會顯示受到所選問題影響的使用者。 按兩下清單中的使用者以顯示與此問題有關的其他資訊。  

    -   **不相容**：根據受影響的資產數目，顯示憑證設定檔中所有不相容規則的清單。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點。 這個節點包含與這個設定檔不相容的所有使用者。 當您選取使用者時，[資產詳細資料]  窗格會顯示受到所選問題影響的使用者。 按兩下清單中的使用者以顯示與此問題有關的進一步資訊。  

    -   **未知**：顯示未回報所選憑證設定檔部署相容性的所有使用者清單，以及裝置目前用戶端狀態。  

5.  您可以在 [部署狀態]  頁面檢閱有關部署之憑證設定檔相容性的詳細資訊。 [部署]  節點下方會建立一個臨時節點以協助您更快再找到此資訊。  

     憑證的註冊狀態會以數字顯示。 請使用下表瞭解每個數字代表的意義：  

    |註冊狀態|說明|  
    |-----------------------|-----------------|  
    |0x00000001|註冊成功，且已發行憑證。|  
    |0x00000002|要求已提出，但註冊尚待處理，或要求已被認定超出訊號範圍。|  
    |0x00000004|註冊必須延後。|  
    |0x00000010|發生錯誤。|  
    |0x00000020|註冊狀態未知。|  
    |0x00000040|狀態資訊已略過。 如果 HYPERLINK "http://msdn.microsoft.com/en-us/windows/ms721572" \l "_security_certification_authority_gly" 憑證授權單位無效或尚未被選取進行監視，就可能發生此情況。|  
    |0x00000100|註冊已被拒。|  

##  <a name="a-namebkmkreportsa-how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> 如何使用報告檢視相容性結果

 System Center Configuration Manager 中的相容性設定包含內建報告，您可利用這些報告來監視憑證設定檔的相關資訊。 這些報告具有 [相容性和設定管理] 的報告類別。  

> [!IMPORTANT]  
>  當您在相容性設定的報告中使用 [裝置篩選器]  和 [使用者篩選器]  參數時，必須使用萬用字元 (%)。  

 如需如何在 System Center Configuration Manager 設定報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)。  



<!--HONumber=Nov16_HO1-->


