---
title: "用戶端的站台系統角色 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中判斷用戶端的站台系統角色。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 17f28ff5addfbfbab251bdb72be9b405487d1403


---
# <a name="determine-the-site-system-roles-for-system-center-configuration-manager-clients"></a>為 System Center Configuration Manager 用戶端判斷站台系統角色

*適用於：System Center Configuration Manager (最新分支)*

請使用本文中的資訊，協助您判斷您需要部署 Configuration Manager 用戶端的站台系統︰  

 如需在階層中安裝必要站台系統角色之位置的詳細資訊，請參閱[為 System Center Configuration Manager 設計站台階層](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)。  

 如需如何安裝及設定您需要之站台系統角色的詳細資訊，請參閱[安裝站台系統角色](../../../../core/servers/deploy/configure/install-site-system-roles.md)。  

##  <a name="a-namebkmkdeterminempa-determine-whether-you-require-a-management-point"></a><a name="BKMK_Determine_MP"></a> 判定您是否需要管理點  
 根據預設，所有的 Windows 用戶端電腦都會使用發佈點來安裝 Configuration Manager 用戶端，並可在無發佈點可用時，切換回管理點。 不過，當您使用 CCMSetup 命令列內容 **/source:<路徑\>** 時，可在其他來源的電腦上安裝 Windows 用戶端。 例如，可能適合在網際網路上安裝用戶端。 另一種情況是在用戶端安裝期間，您想要避免在電腦和管理點之間傳送網路封包，也許是因為防火牆封鎖了安裝方法所需的連接埠，或者是因為您具備低頻寬連線。 然而，所有的用戶端都必須和管理點通訊以指派到站台，並且由 Configuration Manager 進行管理。  

 如需 CCMSetup 命令列內容 **/source:<路徑\>** 的詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端安裝內容](../../../../core/clients/deploy/about-client-installation-properties.md)。  

 當您在階層中安裝一個以上的管理點時，用戶端會根據其樹系成員資格及網路位置，自動連線到最適當的一個。 您無法在次要站台安裝一個以上的管理點。  

 Mac 電腦用戶端以及您向 Configuration Manager 註冊的行動裝置用戶端，一律需要管理點以進行用戶端安裝。 此管理點必須位於主要站台、必須設定為支援行動裝置，並且必須接受來自網際網路的用戶端連線。 這些用戶端無法使用次要站台的管理點，或連線到其他主要站台的管理點。  

##  <a name="a-namebkmkdeterminefspa-determine-whether-you-require-a-fallback-status-point"></a><a name="BKMK_Determine_FSP"></a> 判定您是否需要後援狀態點  
 您可以利用後援狀態點來監視 Windows 電腦的用戶端部署，並可在這些未受管理的電腦上識別用戶端，因為他們無法和管理點通訊。 Mac 電腦、由 Configuration Manager 註冊的行動裝置，以及藉由使用 Exchange Server 連接器進行管理的行動裝置，都未使用後援狀態點。  

> [!NOTE]  
>  監視用戶端活動及用戶端健全狀況，並不需要後援狀態點。  

 後援狀態點永遠會利用 HTTP 和用戶端通訊，該方法使用未經授權的連線，並以純文字傳送資料。 這種方式會使後援狀態點容易遭受攻擊，尤其是和以網際網路為基礎的用戶端管理搭配使用時。 若要減少攻擊介面，可經常讓伺服器執行後援狀態點，且不可將其他站台系統角色安裝在生產環境中的相同伺服器上。  

 如果下列所有條件都適用，則安裝後援狀態點：  

-   您希望將 Windows 電腦的用戶端通訊錯誤傳送到站台，即使這些用戶端電腦無法與管理點通訊。  

-   您想要使用 Configuration Manager 用戶端部署報告，因這些報告會顯示由後援狀態點傳送的資料。  

-   您擁有此站台系統角色專用的伺服器，並且用其他安全性量值進行保護，防止伺服器遭受攻擊。  

-   使用後援狀態點的好處，勝過與未授權連線以及透過 HTTP 流量傳送純文字相關聯的安全性風險。  

 如果下列條件適用時，請勿安裝後援狀態點：  

-   使用未授權連線執行網站以及傳送純文字的安全性風險，勝過識別出用戶端通訊問題的好處。  

##  <a name="a-namebkmkdeterminerspa-determine-whether-you-require-a-reporting-services-point"></a><a name="BKMK_Determine_RSP"></a> 判定您是否需要 Reporting Services 點  
 Configuration Manager 提供許多報告，協助您在 Configuration Manager 主控台監視安裝、指派及管理用戶端。 有些用戶端部署報告要求將用戶端指派到後援狀態點。  

 雖然部署用戶端不需要使用報告，而且您可以在 Configuration Manager 主控台查看某些部署資訊，或是使用用戶端記錄檔來取得詳細資訊，但用戶端報告所提供的寳貴資訊可協助監視及進行用戶端部署疑難排解。  

##  <a name="a-namebkmkdetermineenrollmentpointsa-determine-whether-you-require-an-enrollment-point-and-an-enrollment-proxy-point"></a><a name="BKMK_Determine_EnrollmentPoints"></a> 判定您是否需要註冊點和註冊 Proxy 點  
 Configuration Manager 需要使用註冊點和註冊 Proxy 點註冊行動裝置，並註冊 Mac 電腦的憑證。 如果您利用 Exchange Server 連接器管理行動裝置，或安裝行動裝置舊版用戶端 (例如 Windows CE 適用者)，或要求在 Mac 電腦上安裝 (獨立於 Configuration Manager) 時，則不需要這些站台系統角色。  

##  <a name="a-namebkmkdeterminedpa-determine-whether-you-require-a-distribution-point"></a><a name="BKMK_Determine_DP"></a> 判定您是否需要發佈點  
 雖然您不需要發佈點就能在 Windows 電腦上安裝 Configuration Manager 用戶端，Configuration Manager 會根據預設使用發佈點在 Windows 電腦上安裝用戶端來源檔案，但可切換回從管理點下載這些檔案。 不使用發佈點來安裝由 Configuration Manager 註冊的行動裝置用戶端，但如果您安裝了行動裝置舊版用戶端，就會使用發佈點安裝。 如果您將 Configuration Manager 用戶端當成部分的作業系統部署來安裝，便會儲存並從發佈點擷取作業系統映像。  

 雖然您可能不需要發佈點就能安裝大多數的 Configuration Manager 用戶端，您將會需要用發佈點在用戶端上安裝像應用程式和軟體更新程式之類的軟體。  

##  <a name="a-namebkmkdetermineapplicationcatalogpointsa-determine-whether-you-require-an-application-catalog-website-point-and-an-application-catalog-web-services-point"></a><a name="BKMK_Determine_ApplicationCatalogPoints"></a> 判定您是否需要應用程式類別目錄網站點和應用程式類別目錄 Web 服務點  
 用戶端部署不需要使用應用程式類別目錄網站點和應用程式類別目錄 Web 服務點。 不過，您可能會想要將它們當成部分用戶端部署程序來安裝，如此使用者便可在 Configuration Manager 用戶端安裝於 Windows 電腦時，立即執行下列動作：  

-   抹除其行動裝置。  

-   搜尋及安裝應用程式類別目錄的應用程式。  

-   配合 [可用] 部署目的，將應用程式部署到使用者和裝置。  



<!--HONumber=Nov16_HO1-->


