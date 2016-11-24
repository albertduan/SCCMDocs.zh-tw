---
title: "安裝程式參考 | System Center Configuration Manager"
description: "請檢閱此參考，協助您準備安裝 Configuration Manager 站台或階層。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 06bab7e01fee2c0b030a2879fa67fd455bf668fe


---
# <a name="reference-for-system-center-configuration-manager-setup"></a>System Center Configuration Manager 安裝程式參考

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 安裝程式會提供下列各節所詳述的數個主題連結。 下列各節中的資訊可協助您準備安裝 Configuration Manager 站台或階層，以及協助您準備好一些必須在安裝期間做出的決策：  

-   [開始之前](#bkmk_start)  

-   [評估伺服器整備程度](#bkmk_assess)  

-   [其他作業系統的用戶端](#bkmk_Addclients)  

-   [System Center Configuration Manager 的診斷和使用方式資料](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

##  <a name="a-namebkmkstarta-before-you-begin"></a><a name="bkmk_start"></a> 開始之前  
 在安裝新的 Configuration Manager 站台之前，請確定您已檢閱下列資訊，該資訊可協助您設定成功部署設計的階段：  

-   [System Center Configuration Manager 的基礎](../../../../core/understand/fundamentals.md)  

-   [規劃 System Center Configuration Manager 基礎結構](../../../plan-design/network/configure-firewalls-ports-domains.md)  

-   [準備安裝 System Center Configuration Manager 站台](prepare-to-install-sites.md)  

##  <a name="a-namebkmkassessa-assess-server-readiness"></a><a name="bkmk_assess"></a> 評估伺服器整備程度  
 在開始安裝新的站台之前，請確定您打算針對該站台使用的站台伺服器和遠端站台系統伺服器 (例如裝載站台資料庫的伺服器) 符合所有必要的組態。 文件庫中的下列主題可協助：  

-   [System Center Configuration Manager 的支援設定](../../../../core/plan-design/configs/supported-configurations.md)  

-   [必要條件檢查工具](https://technet.microsoft.com/library/mt590813.aspx#bkmk_PreqChk)  

##  <a name="a-namebkmkaddclientsa-clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> 其他作業系統的用戶端  
 您可以從 Microsoft 下載中心取得適用於下列作業系統的 Configuration Manager 用戶端軟體：  

-   Mac (Apple)  

-   UNIX  

-   Linux  

**使用下列連結來下載您使用之 Configuration Manager 版本的用戶端：**  

-   [System Center Configuration Manager (最新分支)](http://www.microsoft.com/download/details.aspx?id=47719)  

-   [System Center 2012 R2 Configuration Manager SP1 和 System Center 2012 Configuration Manager SP2](http://go.microsoft.com/fwlink/?LinkID=626550)  

-   [System Center 2012 R2 Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=316448)  

-   [System Center 2012 Configuration Manager SP1](http://www.microsoft.com/en-pk/download/details.aspx?id=36212)  

##  <a name="a-namebkmkusagea-usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> 使用情形資料層級和設定  
當您第一次安裝 System Center Configuration Manager 站台時，會在站台伺服器上使用下列預設設定，自動安裝並設定新的站台系統角色 (**服務連接點**)：  

-   **線上** 模式 (也支援離線模式)  

-   **增強** 的資料集合層級 (支援兩個其他資料集合層級：基本和完整)  

當這個角色在線上時，可讓 Microsoft 自動收集網際網路上的診斷和使用量資訊。 所收集的資訊可幫助我們：  

-   識別及疑難排解問題  

-   改善產品和服務  

-   識別適用於您所使用之 Configuration Manager 版本的 Configuration Manager 更新  

資料收集的三個層級包括：  

-   **基本** ：包含安裝和升級的相關資料，例如站台數目，以及啟用的 Configuration Manager 功能。 不會傳送任何個人識別資訊。  

-   **增強** ：除了包含 [基本] 設定的資料之外，還會傳送階層的相關資料、每項功能的使用方式 (頻率和持續時間)，以及增強的診斷資訊，例如您的伺服器在系統當機或應用程式損毀時的記憶體狀態。 不會傳送任何個人識別資料。  

-   **完整** ：除了包含 [基本] 和 [增強] 設定的資料之外，還會傳送系統檔案和記憶體快照集等進階診斷資訊。 這個選項可能包含個人識別資訊，但是我們不會使用該資訊來識別或連絡您，或者推銷廣告給您。  

如需詳細資訊，包括每個層級所收集之詳細資料的揭露，請參閱 [System Center Configuration Manager 的診斷和使用方式資料](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)。  

[System Center Configuration Manager 隱私權聲明](http://go.microsoft.com/fwlink/?LinkID=626527)



<!--HONumber=Nov16_HO1-->


