---
title: "安裝案例 | System Center Configuration Manager"
description: "了解在進行更新或升級時，安裝新 Configuration Manager 階層的技術。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 90a802cbdfd6d0acd60ec462ffbf2a08c012eaeb


---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>System Center Configuration Manager 安裝簡化案例

適用於：System Center Configuration Manager (最新分支)

隨著 System Center Configuration Manager 最新分支更新版本的發行，不論要將新階層安裝到更新版本 (例如 1602 更新)，或從 Microsoft System Center 2012 Configuration Manager 進行升級，都提供了可簡化程序的新案例。  

支援的案例包括：  

**安裝新的 System Center Configuration Manager 最新分支階層**以執行更新版本：  

-   您只要在安裝頂層站台後緊接著安裝更新，即可將該站台升級到您將使用的更新版本。 接著，您可以將其他站台直接安裝到該更新版本。  

-   此案例略過將其他站台安裝到基準層級的步驟，避免了必須再將它們更新到所要使用之更新版本的情況。  

-   此案例略過將用戶端安裝到基準版本的步驟，避免了在您更新到較新版本時還必須重新安裝用戶端的情況。  

**將 Microsoft System Center 2012 Configuration Manager 基礎結構升級**至 System Center Configuration Manager 的更新版本：  

-   您需先將管理中心網站和每個主要站台手動升級到基準版本 (例如 1511)，才能安裝更新版本 (例如 1602)。  

-   在主要站台執行您要使用的更新版本之後，您才需要將次要站台從 Microsoft System Center 2012 Configuration Manager 升級。  

-   在主要站台執行您要使用的更新版本之後，您才需要將用戶端從 Microsoft System Center 2012 Configuration Manager 升級。  

## <a name="scenario---install-a-new-hierarchy-to-an-update-version"></a>案例 - 將新階層安裝到更新版本  
在此範例案例中，您將使用 System Center Configuration Manager 的基準版本 (版本 1511) 來安裝階層的第一個站台。 接著，您需在部署其他站台或用戶端之前，先安裝 1602 更新。  

-   由於您打算使用更新版本 (例如 1602) 而不是停留在基準版本 (例如 1511)，因此您不需要安裝其他站台再將它們升級，或是安裝用戶端再將它們升級。  

-   您不需以版本 1511 安裝次要站台，然後再將它們升級到 1602。 取而代之的是，您將在主要站台執行 1602 之後，再安裝它們。  

**請依下列順序進行：**  

1.  **使用基準媒體來安裝新階層的頂層站台**。  

    -   您只能使用基準媒體來安裝新階層的第一個站台。  

    -   例如，使用基準版本 1511 來安裝頂層站台。 請參閱[使用安裝精靈安裝站台](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)。  

    在此步驟之後，您的頂層站台就會執行版本 1511。  

2.  **使用主控台內更新，將您的頂層站台更新到較新的版本**。  

    -   在安裝任何子站台或用戶端之前，先將您的頂層站台更新到您打算使用的更新版本。  

    -   例如，您可以將執行版本 1511 的頂層站台更新到版本 1602。 請參閱 [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)。  

    在此步驟之後，您的頂層站台就會執行版本 1602。  

3.  **在管理中心網站底下安裝新的子主要站台。**  

    -   使用管理中心網站伺服器上 [CD.Latest] 資料夾中的安裝媒體來安裝子主要站台。  (請參閱 [System Center Configuration Manager 的 CD.Latest 資料夾](../../../../core/servers/manage/the-cd.latest-folder.md))。  

        -   必須使用此來源媒體，才能確保新的子主要站台與管理中心網站的版本相符。  

    在此步驟之後，新的子主要網站就會執行版本 1602。  

4.  **在每個主要站台，使用主控台內選項來安裝新的次要站台**。  

    -   如果您未在主要站台版本為 1511 時安裝次要站台，就不需要升級次要站台。  

    -   取而代之的是，您將安裝執行版本 1602 的新次要站台。 請參閱[使用安裝精靈安裝站台](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)中的*安裝次要站台*。  

    在此步驟之後，新次要站台就會安裝妥當並執行版本 1602。  

5.  **在主要站台安裝新的用戶端。**  

    -   如果您未在主要站台版本為 1511 時安裝用戶端，就不需要將用戶端從 1511 升級到 1602。  

    -   取而代之的是，您將安裝執行版本 1602 的新用戶端。 請參閱 [Deploy clients in System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md) (在 System Center Configuration Manager 中部署用戶端)。  

    在此步驟之後，新用戶端就會安裝妥當並執行版本 1602。  

## <a name="scenario---upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>案例 - 將 System Center 2012 Configuration Manager 升級到 System Center Configuration Manager 最新分支的更新版本  
在此範例案例中，您將把 Microsoft System Center 2012 Configuration Manager 基礎結構升級到 System Center Configuration Manager 的更新版本，例如版本 1602。  

-   在您安裝版本 1602 的更新之前，必須先將管理中心網站和每個主要站台升級到基準版本 1511。  

-   次要站台和用戶端無須升級或安裝 1511。 反之，它們會直接從 Microsoft System Center 2012 Configuration Manager 移轉為 System Center Configuration Manager 版本 1602。  

**請依下列順序進行：**  

1.  **將 Microsoft System Center 2012 Configuration Manager 的頂層站台升級**為最新分支的基準版本 (例如版本 1511)，方法是使用 System Center Configuration Manager 來源媒體。 請參閱[升級至 System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。  

    -   就像傳統升級案例一樣，您一律是先升級階層的頂層站台，然後再升級子站台。  

    在此步驟之後，您的頂層站台就會執行 1511。  

2.  將**您階層中的每個子主要站台升級** 到該相同基準版本。  

    -   當您從 Microsoft System Center 2012 Configuration Manager 升級時，必須將每個主要站台手動升級到最新分支的基準版本。  

    -   您目前還不需升級次要站台。  

    在此步驟之後，每個站台就會執行版本 1511。  

3.  **設定子主要站台的維護時段**。 將所有主要站台升級到基準版本之後，請規劃設定維護期間以控制這些站台安裝基礎結構更新的時間。 請參閱 [How to use maintenance windows in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md) (如何在 System Center Configuration Manager 中使用維護期間)。  (維護期間在版本 1511 中稱為服務保留時間。)  

    -   子主要站台會自動安裝您在管理中心網站所安裝的相同更新。  

    -   次要站台不會自動安裝新版本，必須從主控台內以手動方式升級。  

    > [!NOTE]  
    >  如果您使用版本 1511 而想要使用服務保留時間，您必須先安裝來自 [Microsoft 知識庫文章 3142341](http://support.microsoft.com/kb/3142341)的 Hotfix。 當您安裝 1602 更新時，便會解決此問題。  

    在此步驟之後，當您在管理中心網站上安裝更新時，子主要站台將只有在其維護期間允許的情況下，才會安裝該更新。  

4.  **在您的頂層站台安裝更新版本**。 這會更新您的頂層站台。 在管理中心網站安裝更新版本之後，除非被維護時段封鎖，否則每個子主要站台都會自動安裝更新。  

    -   例如，您可以將頂層站台從版本 1511 更新到版本 1602。 請參閱 [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)  

    在此步驟之後，您的管理中心網站和每個主要站台就會執行版本 1602。  

5.  **升級次要站台。** 在主要站台安裝更新並執行版本 1602 之後，您需使用主控台中選項來升級次要站台。  

    -   這會將次要站台從 Microsoft System Center 2012 Configuration Manager 直接升級到您在主要站台上安裝的更新版本。  

    -   如需升級次要站台的詳細資訊，請參閱[升級至 System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) 中的[升級站台](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade)。  

6.  **升級用戶端。** 請使用[如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)中的資訊。  

    -   這會將用戶端從 Microsoft System Center 2012 Configuration Manager 直接升級到您在主要站台上安裝的更新版本。  

    在此步驟之後，用戶端就會升級到版本 1602，而不需先升級到版本 1511。



<!--HONumber=Nov16_HO1-->


