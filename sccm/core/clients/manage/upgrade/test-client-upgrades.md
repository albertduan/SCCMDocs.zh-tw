---
title: "測試進入生產階段前集合的用戶端升級 | Microsoft Docs"
description: "在 System Center Configuration Manager 中測試進入生產階段前集合的用戶端升級。"
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
caps.latest.revision: 10
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 17b36eae97272c408fce20e1f88812dafc984773
ms.openlocfilehash: bfc53760572e71814ebf0e38ea24c5c4684619ee


---
# <a name="how-to-test-client-upgrades-in-a-preproduction-collection-in-system-center-configuration-manager"></a>如何測試 System Center Configuration Manager 的進入生產階段前集合用戶端升級

*適用於：System Center Configuration Manager (最新分支)*

您可以先在進入生產階段前集合中測試新的 Configuration Manager 用戶端版本，然後用它來升級站台的其餘部分。  當您這樣做時，只會將屬於測試集合的裝置升級。 一旦測試過用戶端之後，您就可以升級該用戶端，讓站台的其餘部分都能使用新版本的用戶端軟體。

> [!NOTE]
> 若要將測試用戶端升階至生產環境，您必須以具備**系統高權限管理員**的安全性角色和**全部**的安全性範圍的使用者身分來登入。 如需詳細資訊，請參閱[以角色為基礎的系統管理基本概念](/sccm/core/understand/fundamentals-of-role-based-administration)。 您也必須登入至已連線到管理中心網站或最上層獨立主要站台的伺服器。

 測試進入生產階段前集合中的用戶端有 3 個基本步驟。  

1.  [設定自動升級用戶端使用進入生產階段前集合](#BKMK_config) 使用進入生產階段前集合。  

2.  [安裝包含新版用戶端的 Configuration Manager 更新](#BKMK_install) ，包含新版的用戶端。 在安裝期間，您要針對新的用戶端軟體指定進入生產階段前集合。  

3.  在成功測試之後，[將新用戶端升階至生產環境](#BKMK_promote)。  

> [!TIP]  
>  如果您從舊版的 Configuration Manager \(例如 Configuration Manager 2007 或 System Center 2012 Configuration Manager\) 升級伺服器基礎結構，建議先完成伺服器升級 (包含安裝所有的最新分支更新)。 這可確保您會在升級 Configuration Manager 用戶端之前具備最新版的用戶端軟體。  

##  <a name="a-namebkmkconfiga-to-configure-automatic-client-upgrades-to-use-a-preproduction-collection"></a><a name="BKMK_config"></a> 設定自動升級用戶端使用進入生產階段前集合  

1. 設定集合，內含您要在其中部署進入生產階段前用戶端的電腦。 如需如何執行此步驟的詳細資訊，請參閱[如何建立集合](..\collections\create-collections.md)。

> [!NOTE]
> 請不要在進入生產階段前集合中包含工作群組電腦。 工作群組電腦無法使用發佈點所需的驗證來存取進入生產階段前用戶端套件。   

1.  在 Configuration Manager 主控台中，開啟 [系統管理] > [站台設定] > [站台]，然後選擇 [階層設定]。  

     在 [階層設定屬性]  的 [用戶端升級] 索引標籤中：  

    -   選取 [使用進入生產階段前用戶端自動升級進入生產階段前集合的所有用戶端]   

    -   輸入要做為進入生產階段前集合的集合名稱  


##  <a name="a-namebkmkinstalla-to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a><a name="BKMK_install"></a> 安裝包含新版用戶端的 Configuration Manager 更新  

1.  在 Configuration Manager 主控台中，開啟 [系統管理] > [雲端服務] > [更新和服務]、選取 [可用] 更新，然後選擇 [安裝更新套件]  

     如需安裝更新的詳細資訊，請參閱 [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)  

2.  在安裝更新期間，在精靈的 [用戶端選項] 頁面上選取 [在進入生產階段前集合中測試]。  

3.  完成精靈的其餘部分，並安裝更新套件。  

     完成精靈之後，進入生產階段前集合中的用戶端會開始部署更新的用戶端。 您可以監視升級用戶端的部署，請前往 **[監視]** > **[用戶端狀態]** > **[進入生產階段前用戶端部署]**。 如需詳細資訊，請參閱[如何在 Configuration Manager 中設定用戶端狀態](../../../../core/clients/deploy/monitor-client-deployment-status.md)。

    > [!NOTE]
    > 在進入生產階段前集合中，裝載站台系統角色之電腦上的部署狀態可能會報告為 [不符合標準]，即使用戶端已成功部署也一樣。 當您將用戶端升階為生產階段時，就會正確報告部署狀態。

##  <a name="a-namebkmkpromotea-to-promote-the-new-client-to-production"></a><a name="BKMK_promote"></a> 將新用戶端升級到生產環境  

1.  在 Configuration Manager 主控台中，開啟 [系統管理] > [雲端服務] > [更新與服務]，然後選擇 [將生產階段前用戶端升階]。

    > [!TIP]
    > 當您監視 **[監視]** [用戶端狀態] **[進入生產階段前用戶端部署]** > **中主控台的用戶端部署時，也可以使用** > **[Promote Pre-production Client (將生產階段前用戶端升階)]**按鈕。

2.  在對話方塊中，檢閱在生產階段和生產階段前的用戶端版本，請確定指定了正確的生產階段前集合，然後按一下 **[升階]**。 在確認對話方塊中，按一下 **[是]**。  

3.  對話方塊關閉後，更新的用戶端版本將會取代您階層中目前使用的用戶端版本。 接著可以升級整個站台的用戶端。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  



<!--HONumber=Dec16_HO1-->


