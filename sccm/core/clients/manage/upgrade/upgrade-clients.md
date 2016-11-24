---
title: "升級用戶端 | System Center Configuration Manager"
description: "取得如何在 System Center Configuration Manager 中升級用戶端的相關資訊。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
caps.latest.revision: 8
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1571d31af1e2697c5ecbdc709a3eea9d6e28dbf0


---
# <a name="upgrade-clients-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中升級用戶端

*適用於：System Center Configuration Manager (最新分支)*

您可以使用不同的方法，升級企業中 Windows 電腦、UNIX 和 Linux 伺服器以及 Mac 電腦上的 System Center Configuration Manager 用戶端軟體。 下列各節概列每種用戶端升級方法的優缺點，協助您判斷最適合貴組織的方法。  

> [!TIP]  
>  如果您從舊版的 Configuration Manager \(例如 Configuration Manager 2007 或 System Center 2012 Configuration Manager\) 升級伺服器基礎結構，建議您先完成伺服器升級 (包含安裝所有的最新分支更新)，然後再升級 Configuration Manager 用戶端。   最新的最新分支更新包含最新版本的用戶端，因此最好在您安裝所有要使用的 Configuration Manager 更新之後，執行用戶端升級。  

## <a name="group-policy-installation"></a>群組原則安裝  
 **支援的用戶端平台：** Windows  

 **優點**  

-   升級用戶端前不需要先探索電腦。  

-   可用於全新安裝或升級用戶端。  

-   電腦可以讀取已發佈至 Active Directory 網域服務的用戶端安裝內容。  

-   不需在目標用戶端電腦設定及維護安裝帳戶。  

 **缺點**  

-   如果升級大量用戶端，可能會使網路流量增高。  

-   如果未延伸 Configuration Manager 的 Active Directory 架構，您必須使用 [群組原則] 設定，將用戶端安裝內容新增至站台中的電腦。  

 如需詳細資訊，請參閱 [How to Install Configuration Manager Clients by Using Group Policy](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) (如何使用群組原則安裝 Configuration Manager 用戶端)。  

## <a name="logon-script-installation"></a>登入指令碼安裝  
 **支援的用戶端平台：** Windows  

 **優點**  

-   安裝用戶端前不需要先探索電腦。  

-   可用於全新安裝或升級用戶端。  

-   支援使用 CCMSetup 命令列屬性。  

 **缺點**  

-   如果在短時間內升級大量用戶端，可能會使網路流量增高。  

-   如果使用者不常登入網路，可能需花很長的時間才能在所有用戶端電腦上升級。  

 如需詳細資訊，請參閱 [How to Install Configuration Manager Clients by Using Logon Scripts](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript) (如何使用登入指令碼安裝 Configuration Manager 用戶端)。  

## <a name="manual-installation"></a>手動安裝  
 **支援的用戶端平台：** Windows、UNIX/Linux、Mac OS X  

 **優點**  

-   升級用戶端前不需要先探索電腦。  

-   可供測試之用。  

-   支援使用 CCMSetup 命令列屬性。  

 **缺點**  

-   不提供自動化功能，因此相當耗時。  

 如需詳細資訊，請參閱下列主題：  

-   [如何手動安裝 Configuration Manager 用戶端](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [如何在 System Center Configuration Manager 中升級 Linux 和 UNIX 伺服器的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

-   [如何在 System Center Configuration Manager 中升級 Mac 電腦上的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>升級安裝 (應用程式管理)  
 **支援的用戶端平台：** Windows  

> [!NOTE]  
>  您無法使用這種方法升級 Configuration Manager 2007 用戶端。 在此案例中，您可以從 Configuration Manager 2007 站台將 Configuration Manager 用戶端部署為套件，或者您可以使用自動用戶端升級以自動建立和部署含有最新用戶端版本的套件。  

 **優點**  

-   支援使用 CCMSetup 命令列屬性。  

 **缺點**  

-   將用戶端發佈至大量集合時，可能會使網路流量增高。  

-   必須先探索電腦並將電腦指派至站台，才能升級這些電腦上的用戶端軟體。  

 如需詳細資訊，請參閱 [How to Install Configuration Manager Clients by Using a Package and Program](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp) (如何使用封裝和程式安裝 Configuration Manager 用戶端)。  

## <a name="automatic-client-upgrade"></a>自動用戶端升級  

> [!NOTE]  
>  可以用來將 Configuration Manager 2007 用戶端升級至 System Center Configuration Manager 用戶端。 Configuration Manager 2007 用戶端可以指派至 Configuration Manager 站台，但是無法執行自動用戶端升級以外的任何動作。  

 **支援的用戶端平台：** Windows  

 **優點**  

-   可用於自動將站台中的用戶端保持在最新版本。  

-   系統管理使用者只需要進行最基本的管理。  

 **缺點**  

-   只能用於升級用戶端軟體，不可用於安裝新用戶端。  

-   不適合用於同時升級許多用戶端。  

-   適用於階層中指派至某個站台的所有用戶端。 不能依集合設定範圍。  

-   排程選項有限。  

 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

## <a name="client-testing"></a>用戶端測試  
 **支援的用戶端平台：** Windows  

 **優點**  

-   可用來在較小的生產前集合中測試新的用戶端版本。  

-   測試完成時，生產階段前中的用戶端會升級至生產，並跨 Configuration Manager 站台自動進行升級。  

 **缺點**  

-   只能用於升級用戶端軟體，不可用於安裝新用戶端。  

 [如何在 System Center Configuration Manager 中測試進入生產階段前集合的用戶端升級](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  



<!--HONumber=Nov16_HO1-->

