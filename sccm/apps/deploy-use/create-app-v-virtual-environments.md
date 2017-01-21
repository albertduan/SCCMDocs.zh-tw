---
title: "建立 App-V 虛擬環境 | System Center Configuration Manager"
description: "使用 Microsoft Application Virtualization 建立虛擬環境，讓應用程式可以彼此共用資料。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 625ea93d855089f6dbbdcc8368032e61b8a1ba0b


---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中建立 App-V 虛擬環境

*適用於︰System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的 Microsoft Application Virtualization (App-V) 虛擬環境可讓部署的虛擬應用程式在用戶端 Windows 電腦上共用同一個檔案系統和登錄。 這表示這些應用程式之間可共用資料，有別於標準的虛擬應用程式。 當已安裝應用程式或是在用戶端下次評估已安裝的應用程式時，用戶端電腦上便會建立或修改虛擬環境。 您可以排序這些應用程式，當有多個應用程式嘗試修改檔案系統或登錄值時，順序最高的應用程式便會優先修改。  

> [!IMPORTANT]  
>  請勿完全依賴 App-V 虛擬環境所提供的安全性保護，例如防範惡意程式碼。  

 請使用以下程序在 Configuration Manager 中建立 App-V 虛擬環境。  

## <a name="create-an-app-v-virtual-environment"></a>建立 App-V 虛擬環境  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] > [應用程式管理] > [App-V 虛擬環境]。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立虛擬環境] 。  

4.  在 [建立虛擬環境]  對話方塊中，指定下列資訊：  

    -   **名稱** - 指定虛擬環境的唯一名稱，不可超過 128 個字元。  

    -   **描述** - 選擇性指定虛擬環境的描述。  

5.  按一下 [新增]  ，將新的部署類型新增至該虛擬環境。 您至少必須新增一種部署類型。  

6.  在 [新增應用程式]  對話方塊中，指定一個最多包含 128 個字元的 [群組名稱]  ，此名稱將可代表已新增至虛擬環境中的應用程式群組。  

7.  按一下 [新增] ，選取要新增至該群組的 App-V 5 應用程式及部署類型，然後按一下 [確定] 。  

8.  當有多個應用程式嘗試修改同一個虛擬環境中的檔案系統或登錄設定時，您可以在 [新增應用程式]  對話方塊中按一下 [升序]  或 [降序]  以指定應用程式的的優先順序。  

9. 按一下 [確定]  返回 [建立虛擬環境]  對話方塊。  

10. 完成新增群組後，按一下 [確定]  建立虛擬環境。 新的虛擬環境會顯示在 Configuration Manager 主控台的 [APP-V 虛擬環境] 節點中。 您可以使用 [App-V 虛擬環境狀態] 報告來監視虛擬環境的狀態。  

    > [!NOTE]  
    >  當已安裝應用程式或是在用戶端下次評估已安裝的應用程式時，便會在用戶端電腦上新增或修改該虛擬環境。  



<!--HONumber=Nov16_HO1-->


