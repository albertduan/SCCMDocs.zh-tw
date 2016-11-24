---
title: "防火牆與網域 | System Center Configuration Manager"
description: "設定防火牆、連接埠和網域，為 System Center Configuration Manager 通訊進行準備。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cd2da8ea3bf0e1351f791d88af3dcbf95f8d6be8


---
# <a name="configure-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 設定防火牆、連接埠和網域

*適用對象：System Center Configuration Manager (最新分支)*

若要準備您的網路以支援 System Center Configuration Manager，請規劃設定基礎結構 (例如防火牆) 來傳遞 Configuration Manager 所使用的通訊。  

|考量|詳細資料|  
|-------------------|-------------|  
|不同 Configuration Manager 功能所使用的**連接埠及通訊協定**。 有些連接埠為必要，其他 **網域和服務** 則可自訂。|大多數的 Configuration Manager 通訊會使用一般連接埠，例如使用連接埠 80 進行 HTTP 通訊，或使用 443 進行 HTTPS 通訊。 但[有些站台系統角色可讓您使用自訂網站](/sccm/core/plan-design/network/websites-for-site-system-servers)及自訂連接埠。<br /><br /> **部署 Configuration Manager 之前**，請先找出您打算使用並據以設定防火牆的連接埠。<br /><br /> 接著，在安裝 Configuration Manager 之後，**如果需要變更連接埠**，請記得更新裝置與網路上的防火牆，也要從 Configuration Manager 內變更連接埠設定。<br /><br /> 如需詳細資訊，請參閱： </br>- [如何設定用戶端通訊連接埠](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [Configuration Manager 中使用的連接埠](../../../core/plan-design/hierarchy/ports.md) </br>- [服務連接點的網際網路存取需求](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|站台伺服器與用戶端可能需要存取的**網域及服務** 。|Configuration Manager 功能可能需要站台伺服器及用戶端存取網際網路上的特定服務及網域，例如 Windowsudpate.microsoft.com 或 Microsoft Intune 服務。<br /><br /> 若要使用 Microsoft Intune 管理行動裝置，還必須設定對 [Intune 所需之連接埠及網域](https://docs.microsoft.com/en-us/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)的存取權。|  
|站台系統伺服器用及用戶端通訊用的**Proxy 伺服器** 。 您可以為不同的站台系統伺服器及用戶端指定不同的 Proxy 伺服器。|因為這些組態是在您安裝站台系統角色或用戶端時指定，所以您只需要記下 Proxy 伺服器組態，供日後設定站台系統角色及用戶端時的參考。<br /><br /> 若不確定部署是否需要使用 Proxy 伺服器，請參閱 [System Center Configuration Manager 中的 Proxy 伺服器支援](../../../core/plan-design/network/proxy-server-support.md)，了解可以使用 Proxy 伺服器的站台系統角色與用戶端動作。|  



<!--HONumber=Nov16_HO1-->


