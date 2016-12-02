---
title: "安裝站台系統角色 | System Center Configuration Manager"
description: "精靈可協助您將站台系統角色新增至站台中現有或新的站台系統伺服器。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 780ef516ddc641d53e1d2d4a5f559795cfd22cbb

---
# <a name="install-site-system-roles-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 安裝站台系統角色

*適用於：System Center Configuration Manager (最新分支)*

您可使用下列兩個 System Center Configuration Manager 主控台的精靈，來安裝站台系統角色︰  

-   **新增站台系統角色精靈**：使用此精靈可將站台系統角色新增至站台中現有的站台系統伺服器。  

-   **建立站台系統伺服器精靈**：使用此精靈可指定新伺服器做為站台系統伺服器，然後在伺服器上安裝一個或多個站台系統角色。 此精靈與 [新增站台系統角色精靈] 相同，唯一的例外是您必須在第一頁指定要使用的伺服器名稱，以及要做為安裝目標的站台。  

您在遠端電腦 (包括 SMS 提供者執行個體) 上安裝站台系統角色時，遠端電腦的電腦帳戶會新增至站台伺服器上的本機群組。 當站台安裝在網域控制站上時，站台伺服器上的群組是網域群組，而不是本機群組，且在站台系統角色電腦重新啟動，或遠端電腦帳戶 ([System Center Configuration Manager 中使用的帳戶](../../../../core/plan-design/hierarchy/accounts.md)) 的 Kerberos 票證重新整理之前，遠端站台系統角色皆無法運作。  

在安裝站台系統角色之前，Configuration Manager 會檢查目的電腦，以確保其符合您所選取的站台系統角色的必要條件。 安裝站台系統角色時：  

-   根據預設，當 Configuration Manager 安裝站台系統角色時，安裝檔會安裝到擁有最多可用磁碟空間的第一部可用 NTFS 格式化磁碟機上。 若要避免 Configuration Manager 安裝到特定磁碟機上，請建立名為 **no_sms_on_drive.sms** 的空檔案，並將它複製到磁碟機的根資料夾，再安裝站台系統伺服器。  

-   Configuration Manager 會使用**站台系統安裝帳戶**來安裝網站系統角色。 您可在執行適用之精靈時指定此帳戶，以建立新網站系統，或將系統角色新增至現有網站系統伺服器。 根據預設，此帳戶是網站伺服器電腦的本機系統帳戶，但您可指定網域使用者帳戶來當成網站系統安裝帳戶使用。 如需詳細資訊，請參閱 [System Center Configuration Manager 中使用的帳戶](../../../../core/plan-design/hierarchy/accounts.md)主題中的＜站台系統安裝帳戶＞。  

##  <a name="a-namebkmkinstalla-to-install-site-system-roles-on-an-existing-site-system-server"></a><a name="bkmk_Install"></a> 在現有站台系統伺服器上安裝站台系統角色  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [站台設定] ，按一下 [伺服器和站台系統角色] ，然後選取要用於新的站台系統角色的伺服器。  

3.  在 [首頁]  索引標籤的 [伺服器]  群組中，按一下 [新增網站系統角色] 。  

4.  在 [一般]  頁面上檢閱設定，然後按 [下一步] 。  

    > [!TIP]  
    >  若要從網際網路存取站台系統角色，請確認您指定的是網際網路 FQDN。  

5.  如果此站台系統伺服器上的站台系統角色需要 Proxy 伺服器才能連線至網際網路上的位置，則在 [Proxy]  頁面上指定 Proxy 伺服器的設定，然後按 [下一步] 。  

6.  在 [系統角色選取]  頁面上，選取要新增的站台系統角色，然後按 [下一步] 。  

7.  完成精靈。  

> [!TIP]  
>  Windows PowerShell Cmdlet New-CMSiteSystemServer 會執行與此程序相同的功能。 如需詳細資訊，請參閱 System Center 2012 Configuration Manager SP1 Cmdlet 參考文件中的 [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414)。  

## <a name="to-install-site-system-roles-on-a-new-site-system-server"></a>若要在新的站台系統伺服器上安裝站台系統角色  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [站台設定] ，然後按一下 [伺服器和站台系統角色] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立網站系統伺服器] 。  

4.  在 [一般]  頁面上，指定網站系統的一般設定，然後按 [下一步] 。  

    > [!TIP]  
    >  若要從網際網路存取新的站台系統角色，請確認您指定的是網際網路 FQDN。  

5.  如果此站台系統伺服器上的站台系統角色需要 Proxy 伺服器才能連線至網際網路上的位置，則在 [Proxy]  頁面上指定 Proxy 伺服器的設定，然後按 [下一步] 。  

6.  在 [系統角色選取]  頁面上，選取要新增的站台系統角色，然後按 [下一步] 。  

7.  完成精靈。  

> [!TIP]  
>  Windows PowerShell Cmdlet New-CMSiteSystemServer 會執行與此程序相同的功能。 如需詳細資訊，請參閱 System Center 2012 Configuration Manager SP1 Cmdlet 參考文件中的 [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414)。  



<!--HONumber=Nov16_HO1-->


