---
title: "發佈站台資料 | System Center Configuration Manager"
description: "了解如何將 Configuration Manager 站台發佈至 Active Directory Domain Services。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cda87a3bdcbba342f111b68af75369ca14744441


---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>發佈 System Center Configuration Manager 的站台資料

適用於：System Center Configuration Manager (最新分支)

延伸 System Center Configuration Manager 的 Active Directory 架構後，您可以將 Configuration Manager 站台發佈至 Active Directory Domain Services (AD DS)，讓 Active Directory 電腦能夠安全地擷取受信任來源的站台資訊。 雖然基本的 Configuration Manager 功能並不需要將站台資訊發佈至 AD DS，但此設定可以減少系統管理負荷。  

-   **當站台設定為發佈至 AD DS 時**，Configuration Manager 用戶端可以針對全域類別目錄伺服器進行 LDAP 查詢，自動透過 Active Directory 發佈功能尋找管理點。  

-   **當站台未發佈到 AD DS 時**，用戶端必須具有找出預設管理點的替代機制。  

如需用戶端如何尋找管理點的資訊，請參閱[了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

## <a name="configure-sites-to-publish-to-ad-ds"></a>將站台設定為發佈到 AD DS  
 高階步驟如下：  

-   您必須在要發佈站台資料的每個目標樹系中，[擴充 System Center Configuration Manager 的 Active Directory 架構](../../../../core/plan-design/network/extend-the-active-directory-schema.md)，並確認「系統管理」容器已存在。  

-   您必須將   **System Management** 容器和其所有子物件的 **完全控制** 授與給每個會發佈資料的主要站台電腦帳戶。  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>若要啟用 Configuration Manager 站台，將站台資訊發佈至 Active Directory 樹系：  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [站台設定]  ，然後按一下 [站台] 。 選取要設定的站台以發佈其站台資料，然後在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

3.  在站台內容的 [發佈]  索引標籤中選取樹系，以便此站台將站台資料發佈至該樹系。  

4.  按一下 [確定]  儲存設定。  

 使用下列程序設定 Active Directory 樹系進行發佈：  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>若要設定 Active Directory 樹系進行發佈：  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [Active Directory 樹系] 。 如果 Active Directory 樹系探索之前已執行，您會在結果窗格中看見每個探索到的樹系。 當 Active Directory 樹系探索執行時，會探索本機樹系和任何信任的樹系。 只有不受信任的樹系必須手動新增。  

    -   若要設定之前探索過的樹系，請在結果窗格中選取樹系，然後在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容]  開啟樹系內容。 繼續進行步驟 3。  

    -   若要設定未列出的新樹系，請在 [首頁]  索引標籤的 [建立]  群組中，按一下 [新增樹系]  開啟 [新增樹系]  對話方塊。 繼續進行步驟 3。  

3.  在 [一般]  索引標籤上，完成您要探索之樹系的設定，並指定 [Active Directory 樹系帳戶] 。  

    > [!NOTE]  
    >  Active Directory 樹系探索需要通用帳戶，才能探索及發佈至不受信任的樹系。 如果您未使用網站伺服器的電腦帳戶，就只能選取通用帳戶。  

4.  如果您打算允許站台將站台資料發佈至此樹系，可在 [發佈]  索引標籤上，完成發佈至此樹系的設定。  

    > [!NOTE]  
    >  如果您讓站台發佈至樹系，就必須針對 Configuration Manager 延伸該樹系的 Active Directory 架構，而且 Active Directory 樹系帳戶必須具有該樹系中系統容器的「完全控制」權限。  

5.  當您完成此樹系的設定以搭配使用 Active Directory 樹系探索時，請按一下 [ **OK** ] 以儲存設定。  



<!--HONumber=Nov16_HO1-->


