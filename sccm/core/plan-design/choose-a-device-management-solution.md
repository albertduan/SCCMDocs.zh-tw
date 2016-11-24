---
title: "選擇 System Center Configuration Manager 的裝置管理解決方案"
description: "了解 System Center Configuration Manager 為管理電腦、伺服器和裝置所提供的解決方案。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: 14
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b64135826dd49c594167999aebd322fa3ed61345


---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>選擇 System Center Configuration Manager 的裝置管理解決方案

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 提供不同的解決方案來管理電腦、伺服器和裝置。 您可以根據您需要管理的裝置平台以及您需要的管理功能，來選擇最適合的解決方案。  


##  <a name="a-namebkmkoverviewa-overview-of-device-management-solutions"></a><a name="bkmk_overview"></a> 裝置管理解決方案概觀  
 下列選項可用來使用 Configuration Manager 管理電腦和裝置：  

-   **使用 Configuration Manager 用戶端管理裝置**  

     這個選項 (需要在要管理的每個裝置上安裝 Configuration Manager 用戶端應用程式) 提供最多的功能來管理您環境中的電腦、伺服器和其他裝置。 這個選項是 Configuration Manager 透過產品歷史提供裝置管理的傳統方式。  

     如需此解決方案的詳細資訊，請參閱 [System Center Configuration Manager 中的用戶端安裝方法](/sccm/core/client/deploy/plan/client-installation-methods)。  

-   **使用內部部署 Configuration Manager 基礎結構管理行動裝置**  

     這個選項使用內建於特定裝置平台之作業系統的裝置管理功能。 雖然內部部署行動裝置管理不具有用戶端管理的完整功能，但是提供更輕的觸控方式來進行使用內部部署 Configuration Manager 資源連接和管理裝置的管理。 目前只有 Windows 10 電腦和 Windows 10 行動裝置支援內部部署行動裝置管理。  

     如需此解決方案的詳細資訊，請參閱[在 System Center Configuration Manager 中使用內部部署基礎結構管理行動裝置](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

-   **使用 Microsoft Intune (混合式) 管理行動裝置**  

     此選項稱為混合式行動裝置管理。  它使用 Microsoft Intune 註冊和管理裝置，而不是使用 Configuration Manager 內部部署資源。 雖然是由 Intune 管理裝置，但是您會在 Configuration Manager 主控台中控制管理工作。 這個選項支援所有主要行動裝置作業系統 (包括 Windows 10 Mobile、Windows Phone、iOS 和 Android)。 它也提供您組織中 Windows 8.1 和 Windows 10 電腦的管理。  

     如需此解決方案的詳細資訊，請參閱[搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理 (MDM)](../../mdm/plan-design/hybrid-mobile-device-management.md)。  

-   **使用 Exchange 管理行動裝置**  

     這個選項 (使用 Exchange Server 連接器將多部 Exchange Server 連線到 Configuration Manager)，並集中管理可連線到 Exchange ActiveSync 的裝置。 您可以從 Configuration Manager 主控台設定 Exchange 行動裝置管理功能，例如遠端裝置抹除，以及多部 Exchange Server 的設定控制。  

     如需此解決方案的詳細資訊，請參閱 [使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

 您可以單獨使用這些裝置管理解決方案，也可以將它們搭配使用。 例如，您可以使用用戶端管理方式來涵蓋如何管理您組織中的電腦和伺服器，也可以使用 Intune 管理來涵蓋行動裝置。 透過這種方式來合併使用方式，您可以涵蓋所有裝置管理需求，並從 Configuration Manager 主控台完全控制它。  

##  <a name="a-namebkmkcomp1a-compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a><a name="bkmk_comp1"></a> 根據支援的行動裝置平台比較裝置管理解決方案  

|平台|使用 Configuration Manager 用戶端|Configuration Manager 與 Microsoft Intune (混合式)|內部部署行動裝置管理|使用 Exchange 的 Configuration Manager|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||是||是|  
|iOS||是||是|  
|Mac OS X|是|||是|  
|UNIX/Linux|是|||是|  
|Windows 10|是|[是]|[是]|是|  
|Windows 10 Mobile||是|[是]|是|  
|Windows (舊版本)|是|[是]||是|  
|Windows CE|是 (具有行動裝置舊版用戶端)|||是|  
|Windows Embedded|是||||  
|Windows Phone||是||是|  
|Windows Server|是|||是|  

 如需支援平台的完整清單，請參閱 [System Center Configuration Manager 用戶端和裝置支援的作業系統](configs\supported-operating-systems-for-clients-and-devices.md)。

##  <a name="a-namebkmkcomp2a-compare-mobile-device-management-solutions-based-on-management-functionality"></a><a name="bkmk_comp2"></a> 根據管理功能比較行動裝置管理解決方案  

|管理功能|使用 Configuration Manager 用戶端|Configuration Manager 與 Microsoft Intune (混合式)|內部部署行動裝置管理|使用 Exchange 的 Configuration Manager|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|行動裝置與 Configuration Manager 之間使用互相驗證和 SSL 加密資料傳輸的公開金鑰基礎結構 (PKI) 安全性|是|[是]|是||  
|用戶端安裝|是||||  
|透過網際網路支援|是||||  
|探索|是|||是|  
|硬體清查|是|[是]|[是]|是|  
|軟體清查|是|||是|  
|設定|是|[是]|[是]|是|  
|軟體部署|是|[是]|是||  
|透過後援狀態點進行監視|是||||  
|管理點的連線|是||是||  
|發佈點的連線|是|[是]|是||  
|封鎖 Configuration Manager|是|[是]|是||  
|隔離和封鎖 Exchange Server (及 Configuration Manager)||||[是]|  
|遠端抹除|是|[是]|[是]|是|  



<!--HONumber=Nov16_HO1-->


