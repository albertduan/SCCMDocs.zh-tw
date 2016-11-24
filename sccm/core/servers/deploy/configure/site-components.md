---
title: "站台元件 | System Center Configuration Manager"
description: "了解如何設定站台元件，以修改站台系統角色和站台狀態報告的行為。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a0c2ff2ad2f76e7e769d49674ccf4d3efe6b4f3e


---
# <a name="site-components-for-system-center-configuration-manager"></a>System Center Configuration Manager 的站台元件

*適用於：System Center Configuration Manager (最新分支)*

在每個 System Center Configuration Manager 站台，您都可以設定站台元件，以修改站台系統角色和站台狀態報告的行為。 站台元件組態適用於站台，以及該站台上適用站台系統角色的每個執行個體。  

## <a name="about-site-components"></a>關於站台元件  
 在 Configuration Manager 主控台檢視不同站台元件的選項時，大部分選項的意義都可透過其名稱得知。 不過，下列詳細資料可協助解說某些較複雜的組態，或將您導向到其他加以解釋的內容：  

**軟體發佈：**  

-   **內容發佈設定：**  您可以進行設定以修改站台伺服器將內容傳輸到其發佈點的方式。 如果您將用於並行發佈設定的值提高，內容發佈就可以使用更多的網路頻寬。  

-   **網路存取帳戶：**如需設定及使用網路存取帳戶的資訊，請參閱[網路存取帳戶](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA)  

**軟體更新點：**  

-   如需軟體更新點元件設定選項的資訊，請參閱[安裝軟體更新點](../../../../sum/get-started/install-a-software-update-point.md)。  

**管理點：**  

-   **管理點：** 您可以將站台設定為將其管理點的相關資訊發行到 Active Directory 網域服務。  

     Configuration Manager 用戶端會使用服務位置的管理點來尋找界限群組成員資格和 PKI 憑證選取選項這類站台資訊，以及在下載軟體的站台和發佈點中尋找其他管理點。 用戶端也會使用管理點來完成站台指派，並下載用戶端原則及上傳其用戶端資訊。  

     由於用戶端用來尋找管理點的大部分安全方法都是在 Active Directory 網域服務中進行發佈，因此您通常一律選取所有可運作的管理點來發佈至 Active Directory 網域服務。 不過，這個服務位置方法需要針對 Configuration Manager 擴充架構、站台伺服器中有具適當安全性權限的 [系統管理] 容器以發佈至這個容器、Configuration Manager 站台設定為發行至 Active Directory 網域服務，而且用戶端屬於與站台伺服器相同的 Active Directory 樹系。  

     內部網路上的用戶端無法使用 Active Directory 網域服務以尋找管理點時，請使用 [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns) 發行。  

     如需服務位置的一般資訊，請參閱[了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

-   **在 DNS 中發佈選取的內部網路管理點：** 內部網路上的用戶端無法從 Active Directory 網域服務找到管理點時，請指定此選項，但用戶端可以使用 DNS 服務位置資源記錄 (SRV RR) 在其指派的站台找到管理點。  

    如果 Configuration Manager 要將內部網路管理點發行至 DNS，則必須符合下列所有條件：  

    -   您的 DNS 服務包含 8.1.2 (含) 以上版本的 BIND。  

    -   您的 DNS 伺服器已設定為自動更新，並支援服務位置資源記錄。  

    -   Configuration Manager 中管理點的指定 FQDN 在 DNS 中包含主機項目 (A 或 AAA 記錄)。  

    > [!WARNING]  
    >  用戶端若要尋找要在 DNS 中發佈的管理點，您必須指派用戶端至特定網站 (而不是使用自動網站指派) 並設定這些用戶端透過其管理點的網域尾碼來使用網站代碼。 如需詳細資訊，請參閱[如何將用戶端指派給 System Center Configuration Manager 中的站台](../../../../core/clients/deploy/assign-clients-to-a-site.md)中的[尋找管理點](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_LocatingMPs)。  

     如果 Configuration Manager 用戶端無法使用 Active Directory 網域服務或 DNS 在內部網路上尋找管理端，就會切換回使用 [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins)。 為此網站安裝的第一個管理點設定為接受在內部網路讀的 HTTP 用戶端連線時，管理點會自動發佈到 WINS。  

**狀態報告：**  

-   這些設定直接設定站台及用戶端狀態報告內含的詳細資料層級。  

**電子郵件通知：**  

-   指定帳戶和電子郵件伺服器詳細資料，讓 Configuration Manager 傳送警示的電子郵件通知。  

**集合成員資格評估：**  

-   使用此工作以設定累加式評估集合成員資格的頻率。 累加式評估只會更新已新增或變更資源的集合成員資格。  

#### <a name="to-edit-the-site-components-at-a-site"></a>在站台上編輯站台元件  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] > [站台設定] > [站台]，然後選取包含要設定之站台元件的站台。  

2.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [設定站台元件]  ，然後選取您要設定的站台元件。  

##  <a name="a-namebkmkservicemgra-use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> 使用 Configuration Manager Service Manager 管理站台元件  
您可以使用 Configuration Manager Service Manager 來控制 Configuration Manager 服務，以及檢視任一 Configuration Manager 服務或工作執行緒 (皆指 Configuration Manager 元件) 的狀態：  

-   Configuration Manager 元件可在任何站台系統上執行。  

-   管理元件的方式與您管理 Windows 中的服務一樣；您可以啟動、停止、暫停、繼續或查詢 Configuration Manager 元件。  

Configuration Manager 服務會在具有任務時執行 (通常是將設定檔寫入元件收件匣時)。 如果您必須識別出作業中的元件，您可以使用 **Configuration Manager Service Manager** 來操作各種 Configuration Manager 服務與執行緒，然後檢視 Configuration Manager 行為中所產生的變更。 例如，您可以一次停止 Configuration Manager 服務，直到消除某個特定回應為止。 如此可讓您判斷哪一種服務導致此行為。  

> [!TIP]  
>  以下程序可用來操作 Configuration Manager 元件作業。  

#### <a name="to-use-the-configuration-manager-service-manager"></a>使用 Configuration Manager Service Manager  

1.  在 Configuration Manager 主控台中，按一下 [監視] >  [系統狀態]，然後按一下 [元件狀態]。  

2.  在 [首頁]  索引標籤的 [元件]  群組中，按一下 [開始] ，然後選取 [Configuration Manager Service Manager] 。  

3.  Configuration Manager Service Manager 開啟時，連線至您要管理的網站。  

     若您看不到要管理的站台，請依序按一下 [站台] 與 [連線] ，然後輸入正確站台的站台伺服器名稱。  

4.  展開站台，然後根據您要管理之元件所在的位置，瀏覽至 [元件]  或 [伺服器]  。  

5.  在右窗格中選取一或多個元件，然後在 [元件]  功能表上按一下 [查詢]  以更新選擇狀態。  

6.  更新元件狀態後，使用 [元件]  功能表上四種以動作為基礎的選項之一，以修改元件操作。 要求動作後，您必須查詢元件，以顯示元件的新狀態。  

7.  完成修改元件操作狀態後，請關閉 Configuration Manager Service Manager。  



<!--HONumber=Nov16_HO1-->


