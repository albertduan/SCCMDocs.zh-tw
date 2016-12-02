---
title: "管理內容的網路頻寬 | System Center Configuration Manager"
description: "設定 System Center Configuration Manager 的排程、節流及預先設置的內容。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 92a08908f284abb02ce8000122b0839c474616d7


---

##  <a name="a-namebkmkplanningforthrottlingascheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>排程及節流  
 為了協助您管理用於內容管理程序的網路頻寬，您可以使用 Configuration Manager 的內建控制項進行排程及節流，或使用預先設置的內容。  

 當您建立套件、變更內容的來源路徑，或在發佈點上更新內容時，檔案會從來源路徑複製到網站伺服器上的內容庫。 接著，會將內容從網站伺服器上的內容庫複製到發佈點上的內容庫。 當更新內容來源檔案時，若已發佈來源檔案，Configuration Manager 只會擷取新的或已更新的檔案，然後再將這些檔案傳送至發佈點。 您可以在網站對網站通訊，以及網站伺服器與遠端發佈點間，設定排程和節流控制。 當網站伺服器和遠端發佈點之間的網路頻寬在您設定排程和節流設定後仍受限時，您必須考慮在發佈點上預先設置內容。  

 在 Configuration Manager 中，您可以在遠端發佈點上設定排程並設定特定的節流設定，以判斷執行內容發佈的時間及方法。 每個遠端發佈點皆有不同的設定，可解決網站伺服器對遠端發佈點的網路頻寬限制。 用於遠端發佈點之排程及節流的控制項與標準傳送者位址的設定類似，但在此情況下，這些設定是由名為套件傳輸管理員的新元件所使用。 套件傳輸管理員會從網站伺服器 (做為主要網站或次要網站) 將內容發佈到網站系統上安裝的發佈點。 您可以在 [速率限制]  索引標籤上設定節流設定，以及在不在網站伺服器之發佈點上的 [排程]  索引標籤上設定排程設定。 這些時間設定是以傳送網站 (而不是發佈點) 的時區為基礎。  

> [!WARNING]  
>  [速率限制]  和 [排程]  索引標籤只會顯示於未安裝在網站伺服器之發佈點的內容中。  

如需為遠端發佈點設定排程及節流設定的詳細資訊，請參閱 [Install and configure distribution points for System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points) (為 System Center Configuration Manager 安裝及設定發佈點)。  

##  <a name="a-namebkmkprestagingcontentaprestaged-content"></a><a name="BKMK_PrestagingContent"></a>預先設置的內容  
 您可以預先設置內容，先將內容檔加入站台伺服器或發佈點上的內容庫，然後再發佈該內容。  

-   因為內容檔已經存在於內容庫中，所以當您發佈內容時，就不會透過網路傳送。  

-   您可以預先設置應用程式與封裝的內容檔。  

在 Configuration Manager 主控台中，您可以選取要預先設置的內容，接著使用 [建立預先設置的內容檔案精靈] 來建立壓縮的預先設置內容檔案，其中包含內容的檔案和與內容相關聯的中繼資料。 接著，您便可在站台伺服器或發佈點上手動匯入內容。  

-   當您在站台伺服器上匯入預先設置的內容檔時，該內容檔會加入站台伺服器上的內容庫，然後才會在站台伺服器資料庫中登錄。  

-   當您在發佈點上匯入預先設置的內容檔時，內容檔會加入發佈點上的內容庫，接著會將狀態訊息傳送至站台伺服器，以通知站台，發佈點上的內容已可供使用。  

您可以選擇性地將發佈點設定為 **預先設置** ，以協助管理內容發佈。 然後，當您發佈內容時，可以選擇是否要：  

-   一律在發佈點上預先設置內容  

-   預先設置封裝的初始內容，然後在內容有所更新時，使用標準內容發佈程序。  

-   一律為封裝中的內容使用標準內容發佈程序  

###  <a name="a-namebkmkdeterminetoprestagecontentadetermine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>判斷是否要預先設置內容  
 在以下案例中，請考慮為應用程式和套件預先設置內容：  

-   **限制從網站伺服器到發佈點的網路頻寬**：當排程和節流設定無法滿足您對於透過網路將內容發佈到遠端發佈點的相關需求時，請考慮在發佈點上預先設置內容。 每個發佈點皆內含 [啟用此發佈點供預先設置的內容使用]  設定，您可以在發佈點內容中設定。 當您啟用此選項時，會將發佈點識別為預先設置的發佈點，您可以選擇如何以每個套件為基礎來管理內容。  

     下列設定可在應用程式、套件、驅動程式套件、開機映像、作業系統安裝程式和映像中使用，讓您設定如何在已識別為預先設置的遠端發佈點上管理內容發佈：  

    -   **當套件指派給發佈點時，自動下載內容**：當您的套件容量較小，且排程和節流設定針對內容發佈提供足夠的控制時，請使用此選項。  

    -   **只下載內容變更至發佈點**：當您的初始封裝容量可能很大，但您預計日後對封裝中的內容更新一般來說會很少時，請使用此選項。 例如，您可能預先設置了像是 Microsoft Office 的應用程式，因為其初始封裝大小超過 700 MB，如透過網路傳送會太大。 不過，對此套件的內容更新可能會小於 10 MB，因此可接受透過網路進行發佈。 另一個範例可能是驅動程式套件，其初始套件大小很大，但累加至套件的驅動程式大小可能很小。  

    -   **將此套件中的內容手動複製到發佈點**：當您的套件容量很大 (其中包含如作業系統等內容)，而不想使用網路將內容發佈到發佈點時，請使用此套件。 當您選取此選項時，必須在發佈點上預先設置內容。  

    > [!WARNING]  
    >  上述選項適用於以每個套件為基礎的情況，並且只有在已將發佈點識別為已預先設置的情況下才能使用。 尚未識別為預先設置的發佈點會忽略這些設定。 在這種情況下，內容將一律透過網路從網站伺服器發佈到發佈點。  

-   **還原網站伺服器上的內容庫**：當網站伺服器失敗時，系統會在進行還原程序時將內容庫中包含的套件和應用程式相關資訊還原至網站資料庫，但不會還原內容庫檔案。 如果沒有可還原內容庫的檔案系統備份，您可以從其他內含所需套件及應用程式的網站建立預先設置的內容檔案，然後在復原的網站伺服器上解壓縮預先設置的內容檔案。 如需站台伺服器備份與復原的詳細資訊，請參閱 [Backup and recovery for System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery) (System Center Configuration Manager 的備份和復原)。  



<!--HONumber=Nov16_HO1-->


