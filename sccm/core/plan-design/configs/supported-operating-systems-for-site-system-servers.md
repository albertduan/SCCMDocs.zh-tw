---
title: "支援的站台系統伺服器 | System Center Configuration Manager"
description: "了解您可用來裝載 System Center Configuration Manager 站台或站台系統角色的 Windows 版本。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 00d5d8d9ce90b2da79485250d25f943ca1c4547b


---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>支援的 System Center Configuration Manager 站台系統伺服器作業系統

*適用於：System Center Configuration Manager (最新分支)*


本文詳述您可用來裝載 System Center Configuration Manager 站台或站台系統角色的 Windows 版本。


使用本主題及下列文章中的資訊︰
-   [Configuration Manager 的建議硬體](../../../core/plan-design/configs/recommended-hardware.md)
-   [Configuration Manager 的站台和站台系統必要條件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Configuration Manager 的大小和縮放比例](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016---standard-datacenter"></a>Windows Server 2016 - Standard、Datacenter
從具有 KB3186654 之 Hotfix 彙總套件的 Configuration Manager 1606 版 (或 2016 年 10 月發行的基準版本 1606) 開始，支援 Windows Server 2016。

**站台伺服器：**  

-   管理中心網站  

-   主要網站  

-   次要網站  

**站台系統伺服器：**  

-   應用程式類別目錄 Web 服務點  

-   應用程式類別目錄網站點  

-   Asset Intelligence 同步處理點  

-   憑證登錄點  

-   發佈點  

     發佈點支援數個不同的組態，各有不同需求，且在某些情況下不只支援安裝在伺服器上，也支援安裝在用戶端作業系統上。 如需發佈點可用選項的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

-   Endpoint Protection 點  

-   註冊點  

-   註冊 Proxy 點  

-   後援狀態點  

-   Reporting Services 點  

-   服務連接點  

-   網站資料庫伺服器  

     唯讀網域控制站 (RODC) 上不支援站台資料庫伺服器。 如需詳細資訊，請參閱 Microsoft 知識庫中的 [網域控制站上安裝 SQL Server 時，您可能會遇到問題](http://go.microsoft.com/fwlink/p/?LinkId=264856) 。 此外，任何網域控制站上不支援次要站台伺服器。  

-   SMS_Provider  

-   軟體更新點  

-   狀態移轉點

## <a name="windows-server-2012-r2-x64---standard-datacenter"></a>Windows Server 2012 R2 (x64) - Standard、Datacenter  
**站台伺服器：**  

-   管理中心網站  

-   主要網站  

-   次要網站  

**站台系統伺服器：**  

-   應用程式類別目錄 Web 服務點  

-   應用程式類別目錄網站點  

-   Asset Intelligence 同步處理點  

-   憑證登錄點  

-   發佈點  

     發佈點支援數個不同的組態，各有不同需求，且在某些情況下不只支援安裝在伺服器上，也支援安裝在用戶端作業系統上。 如需發佈點可用選項的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

-   Endpoint Protection 點  

-   註冊點  

-   註冊 Proxy 點  

-   後援狀態點  

-   Reporting Services 點  

-   服務連接點  

-   網站資料庫伺服器  

     唯讀網域控制站 (RODC) 上不支援站台資料庫伺服器。 如需詳細資訊，請參閱 Microsoft 知識庫中的 [網域控制站上安裝 SQL Server 時，您可能會遇到問題](http://go.microsoft.com/fwlink/p/?LinkId=264856) 。 此外，任何網域控制站上不支援次要站台伺服器。  

-   SMS_Provider  

-   軟體更新點  

-   狀態移轉點  

## <a name="windows-server-2012-x64---standard-datacenter"></a>Windows Server 2012 (x64) - Standard、Datacenter  
**站台伺服器：**  

-   管理中心網站  

-   主要網站  

-   次要網站  

**站台系統伺服器：**  

-   應用程式類別目錄 Web 服務點  

-   應用程式類別目錄網站點  

-   Asset Intelligence 同步處理點  

-   憑證登錄點  

-   發佈點  

     發佈點支援數個不同的組態，各有不同需求，且在某些情況下不只支援安裝在伺服器上，也支援安裝在用戶端作業系統上。 如需發佈點可用選項的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

-   Endpoint Protection 點  

-   註冊點  

-   註冊 Proxy 點  

-   後援狀態點  

-   Reporting Services 點  

-   服務連接點  

-   網站資料庫伺服器  

     唯讀網域控制站 (RODC) 上不支援站台資料庫伺服器。 如需詳細資訊，請參閱 Microsoft 知識庫中的 [網域控制站上安裝 SQL Server 時，您可能會遇到問題](http://go.microsoft.com/fwlink/p/?LinkId=264856) 。 此外，任何網域控制站上不支援次要站台伺服器。  

-   SMS_Provider  

-   軟體更新點  

-   狀態移轉點  

## <a name="windows-server-2008-r2-with-sp1-x64---standard-enterprise-datacenter"></a>Windows Server 2008 R2 with SP1 (x64) - Standard、Enterprise、Datacenter  
 Windows Server 2008 R2 現在屬於延伸支援，而不再屬於主流支援，如  [Microsoft 支援週期](https://support.microsoft.com/lifecycle)中詳述。 如需這些作業系統作為 Configuration Manager 站台系統伺服器的未來支援詳細資訊，請參閱 [System Center Configuration Manager 的已移除和已淘汰功能](../../../core/plan-design/changes/removed-and-deprecated-features.md)。  

**站台伺服器：**  

-   管理中心網站  

-   主要網站  

-   次要網站  

**站台系統伺服器：**  

-   應用程式類別目錄 Web 服務點  

-   應用程式類別目錄網站點  

-   Asset Intelligence 同步處理點  

-   憑證登錄點  

-   發佈點  

     發佈點支援數個不同的組態，各有不同需求，且在某些情況下不只支援安裝在伺服器上，也支援安裝在用戶端作業系統上。 如需發佈點可用選項的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

-   Endpoint Protection 點  

-   註冊點  

-   註冊 Proxy 點  

-   後援狀態點  

-   Reporting Services 點  

-   服務連接點  

-   網站資料庫伺服器  

     唯讀網域控制站 (RODC) 上不支援站台資料庫伺服器。 如需詳細資訊，請參閱 Microsoft 知識庫中的 [網域控制站上安裝 SQL Server 時，您可能會遇到問題](http://go.microsoft.com/fwlink/p/?LinkId=264856) 。 此外，任何網域控制站上不支援次要站台伺服器。  

-   SMS_Provider  

-   軟體更新點  

-   狀態移轉點  

## <a name="windows-server-2008-with-sp2-x86-x64---standard-enterprise-datacenter"></a>Windows Server 2008 (含 SP2) (x86、x64) - Standard、Enterprise、Datacenter  
 Windows Server 2008 現在屬於延伸支援，而不再屬於主流支援，如  [Microsoft 支援週期](https://support.microsoft.com/lifecycle)中詳述。 如需這些作業系統作為 Configuration Manager 站台系統伺服器的未來支援詳細資訊，請參閱 [System Center Configuration Manager 的已移除和已淘汰功能](../../../core/plan-design/changes/removed-and-deprecated-features.md)。  

**站台伺服器：**  

-   管理中心網站  

-   主要網站  

-   次要網站  

**站台系統伺服器：**  

-   應用程式類別目錄 Web 服務點  

-   應用程式類別目錄網站點  

-   Asset Intelligence 同步處理點  

-   憑證登錄點  

-   發佈點  

    -   此作業系統上的發佈點不支援多點傳送。  

    -   此作業系統上的發佈點支援 PXE，但不支援 EFI 模式的用戶端電腦透過網路開機。 支援具有 BIOS 或舊版模式 EFI 開機的用戶端電腦。  

    -   發佈點支援數個不同的組態，各有不同需求，且在某些情況下不只支援安裝在伺服器上，也支援安裝在用戶端作業系統上。 如需發佈點可用選項的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

-   Endpoint Protection 點  

-   註冊點  

-   註冊 Proxy 點  

-   後援狀態點  

-   Reporting Services 點  

-   服務連接點  

-   網站資料庫伺服器  

     唯讀網域控制站 (RODC) 上不支援站台資料庫伺服器。 如需詳細資訊，請參閱 Microsoft 知識庫中的 [網域控制站上安裝 SQL Server 時，您可能會遇到問題](http://go.microsoft.com/fwlink/p/?LinkId=264856) 。 此外，任何網域控制站上不支援次要站台伺服器。  

-   SMS_Provider  

-   軟體更新點  

-   狀態移轉點  

## <a name="windows-10-x86-x64---pro-enterprise"></a>Windows 10 (x86、x64) - 專業版、企業版  
**站台系統伺服器：**  

-   發佈點  

    -   此作業系統上的發佈點不支援 PXE。  

    -   此作業系統版本上的發佈點不支援多點傳送。  

    -   發佈點支援數個不同的組態，各有不同需求，且在某些情況下不只支援安裝在伺服器上，也支援安裝在用戶端作業系統上。 如需發佈點可用選項的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

## <a name="windows-81-x86-x64---professional-enterprise"></a>Windows 8.1 (x86、x64) - 專業版、企業版  
**站台系統伺服器：**  

-   發佈點  

    -   此作業系統上的發佈點不支援 PXE。  

    -   此作業系統版本上的發佈點不支援多點傳送。  

    -   發佈點支援數個不同的組態，各有不同需求，且在某些情況下不只支援安裝在伺服器上，也支援安裝在用戶端作業系統上。 如需發佈點可用選項的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

## <a name="windows-8-x86-x64---professional-enterprise-distribution-point"></a>Windows 8 (x86、x64) - 專業版、企業版發佈點  
**站台系統伺服器：**  

-   發佈點  

    -   此作業系統上的發佈點不支援 PXE。  

    -   此作業系統版本上的發佈點不支援多點傳送。  

    -   發佈點支援數個不同的組態，各有不同需求，且在某些情況下不只支援安裝在伺服器上，也支援安裝在用戶端作業系統上。 如需發佈點可用選項的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

## <a name="windows-7-with-sp1-x86-x64---professional-enterprise-ultimate"></a>Windows 7 (含 SP1) (x86、x64) - 專業版、企業版、旗艦版  
**站台系統伺服器：**  

-   發佈點  

    -   此作業系統上的發佈點不支援 PXE。  

    -   此作業系統版本上的發佈點不支援多點傳送。  

    -   發佈點支援數個不同的組態，各有不同需求，且在某些情況下不只支援安裝在伺服器上，也支援安裝在用戶端作業系統上。 如需發佈點可用選項的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

## <a name="the-server-core-installation-of-windows-server-2012"></a>Windows Server 2012 的 Server Core 安裝  
 除了上述的作業系統，支援 Windows Server 2012 的 Server Core 安裝以做為發佈點使用，具有下列限制：  

-   僅支援 x64  

-   此作業系統上的發佈點不支援 PXE 或多點傳送  

## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>Windows Server 2012 R2 的 Server Core 安裝  
 除了上述的作業系統，支援 Windows Server 2012 R2 的 Server Core 安裝做為發佈點使用，具有下列限制：  

-   僅支援 x64  

-   此作業系統上的發佈點不支援 PXE 或多點傳送  



<!--HONumber=Nov16_HO1-->


