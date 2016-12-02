---
title: "用來存取內容的帳戶 | System Center Configuration Manager"
description: "了解用戶端用來存取 System Center Configuration Manager 內容的帳戶。"
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7df9d0f-fbde-47eb-97e7-3d29536424fa
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c7d5dc2767621ac2e494d24af07ca20513d6d63f

---
# <a name="manage-accounts-to-access-content-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理用來存取內容的帳戶

適用於：System Center Configuration Manager (最新分支)

在 System Center Configuration Manager 中部署內容之前，請花點時間思考用戶端將如何從發佈點存取該內容。  

-   **網路存取帳戶** – 由用戶端用以連接到發佈點和存取內容。 用戶端預設會先嘗試其電腦帳戶  

     提取發佈點也會使用此帳戶從遠端樹系中的來源發佈點獲取內容  

-   **套件存取帳戶** - Configuration Manager 預設會將發佈點上的內容存取權授與一般存取帳戶使用者和系統管理員。 不過，您可以設定其他權限以限制存取。  

-   **多點傳送連接帳戶** – 用於作業系統部署。  

##  <a name="a-namebkmknaaa-network-access-account"></a><a name="bkmk_NAA"></a> 網路存取帳戶  
 用戶端電腦會在無法使用本機電腦帳戶存取發佈點上的內容時使用網路存取帳戶；例如，這適用於來自不受信任網域的工作群組用戶端和電腦。 當安裝作業系統的電腦沒有網域上的電腦帳戶時，此帳戶也會在作業系統部署期間使用。  

-   用戶端只會使用網路存取帳戶來存取網路上的資源  

-   您可以在每個主要站台設定多個帳戶作為網路存取帳戶使用  

-   用戶端會先嘗試使其 *computername*$ 帳戶，存取發佈點上的內容。 如果此帳戶失敗，它會接著嘗試使用網路存取帳戶。 然後，用戶端會繼續嘗試使用網路存取帳戶，即使先前已失敗亦同。  

**權限**：請為此帳戶授與存取用戶端所需內容之軟體最基本的適當權限。  

-   此帳戶必須在發佈點上具有 [從網路存取這台電腦]  權限。  

-   請在提供必要的資源存取權限的任何網域中建立此帳戶。 網路存取帳戶一律都必須包含網域名稱。 此帳戶不支援傳遞安全性。 如果您在多個網域中擁有發佈點，請在受信任網域中建立此帳戶。  

> [!TIP]  
>  為避免帳戶鎖定，請不要變更現有網域存取帳戶的密碼。 您可改為建立新帳戶，並且在 Configuration Manager 中設定新帳戶。 經過一段時間所有用戶端都已收到新帳戶的詳細資料後，從網路共用資料夾移除舊帳戶，並刪除該帳戶。  

> [!IMPORTANT]  
>  不要授與此帳戶互動式登入權限。  
>   
>  不要授與此帳戶將電腦加入網域的權限。 如果您必須在工作順序期間將電腦加入網域，請使用工作順序編輯器網域加入帳戶。  

### <a name="to-configure-the-network-access-account"></a>設定網路存取帳戶  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] >   [站台設定] >  [站台]，然後選取站台。  

2.  在 [設定] 群組中，按一下 [設定站台元件] > [軟體發佈]。  

3.  按一下 [網路存取帳戶]  索引標籤。 設定一個或多個帳戶，然後按一下 [確定] 。  

##  <a name="a-namebkmkpaaa-package-access-accounts"></a><a name="bkmk_Paa"></a> 套件存取帳戶  
 套件存取帳戶可讓您設定 NTFS 檔案系統權限，以指定可存取發佈點上套件內容的使用者和使用者群組。 Configuration Manager 預設只將存取權授與一般存取帳戶**使用者**和**系統管理員**，但您可以使用額外的 Windows 帳戶或群組控制用戶端電腦的存取。 行動裝置永遠會以匿名方式擷取套件內容，因此，行動裝置不會使用套件存取帳戶。  

 根據預設，當 Configuration Manager 將套件中的內容檔案複製到發佈點時，會將 [讀取] 權限授與本機**使用者**群組，並將 [完全控制] 授與本機**系統管理員**群組。 實際需要的權限取決於套件。 如果有用戶端位於工作群組或不受信任的樹系中，這些用戶端會使用網路存取帳戶來存取套件內容。 請使用定義的套件存取帳戶，確定網路存取帳戶擁有存取套件的權限。  

 使用網域中可存取發佈點的帳戶。 如果您在建立套件後建立或修改帳戶，則必須重新發佈套件。 更新套件不會變更套件上的 NTFS 檔案系統權限。  

 您不需要將網路存取帳戶新增為套件存取帳戶，因為 [Users]  群組的成員資格會自動新增它。 將套件存取帳戶限制為只有網路存取帳戶不會阻止用戶端存取套件。  

### <a name="to-manage-access-accounts"></a>管理存取帳戶  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，為您想要管理存取帳戶的內容類型選取下列其中一個步驟：  

    -   **應用程式**：展開 [應用程式管理] ，按一下 [應用程式] ，然後選取要管理存取帳戶的應用程式。  

    -   **套件**：展開 [應用程式管理] ，按一下 [套件] ，然後選取要管理存取帳戶的套件。  

    -   **部署套件**：展開 [軟體更新] ，按一下 [部署套件] ，然後選取要管理存取帳戶的部署套件。  

    -   **驅動程式套件**：展開 [作業系統] ，按一下 [驅動程式套件] ，然後選取要管理存取帳戶的驅動程式套件。  

    -   **作業系統映像**：展開 [作業系統] ，按一下 [作業系統映像] ，然後選取要管理存取帳戶的作業系統映像。  

    -   **作業系統安裝程式**：展開 [作業系統] ，按一下 [作業系統安裝程式] ，然後選取要管理存取帳戶的作業系統安裝程式。  

    -   **開機映像**：展開 [作業系統] ，按一下 [開機映像] ，然後選取要管理存取帳戶的開機映像。  

3.  以滑鼠右鍵按一下選取的物件，然後按一下 [管理存取帳戶] 。  

4.  在 [新增帳戶]  對話方塊中，指定將被授與存取內容權限的帳戶，然後指定與帳戶關聯的存取權限。  

    > [!NOTE]  
    >  當您新增帳戶的使用者名稱，且 Configuration Manager 找到使用該名稱的本機使用者帳戶與網域使用者帳戶時，Configuration Manager 會為網域使用者帳戶設定存取權限。  

##  <a name="a-namebkmkmultia-multicast-connection-account"></a><a name="bkmk_multi"></a> 多點傳送連線帳戶  
 針對多點傳送設定的發佈點會使用多點傳送連線帳戶，來讀取網站資料庫的資訊。  

-   指定將 Configuration Manager 資料庫連接設定為多點傳送時，所要使用的帳戶。  

-   預設會使用發佈點的電腦帳戶，但您可以改為設定使用者帳戶。  

-   只要站台資料庫位於不受信任的樹系中，就必須指定使用者帳戶。  

-   帳戶必須具有站台資料庫的 **讀取** 權限  

例如，如果您的資料中心在網站伺服器和網站資料庫以外的樹系中擁有周邊網路，您可以使用此帳戶來讀取網站資料庫的多點傳送資訊。  
如果建立了此帳戶，則在執行 Microsoft SQL Server 的電腦上建立低權限的本機帳戶。  

> [!IMPORTANT]  
>  請勿將互動登入權限授與此帳戶  



<!--HONumber=Nov16_HO1-->

