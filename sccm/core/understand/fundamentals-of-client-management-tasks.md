---
title: "用戶端管理基礎 | Microsoft Docs"
description: "深入了解您可以執行以管理 System Center Configuration Manager 用戶端的工作。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 9648fc831e21f8a5ee6e12cfe7754933ba9f6239


---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>System Center Configuration Manager 的用戶端管理基本概念

*適用於：System Center Configuration Manager (最新分支)*

在安裝 System Center Configuration Manager 用戶端之後，您可以執行數項工作來管理用戶端。  這些工作當中，有些可透過 Configuration Manager 主控台啟動，有些則可透過 Windows 控制台中的用戶端 Configuration Manager 應用程式在用戶端上啟動或檢視。  

## <a name="the-console"></a>主控台  
 從 Configuration Manager 主控台內，您可以執行各種用戶端管理工作，其中包括下列各項︰  

-   部署應用程式、軟體更新、維護指令碼及作業系統。 您可設定在指定日期和時間之前安裝這些軟體，或將它們設定為使用者要求時即可安裝，您也可同時設定解除安裝應用程式。  

-   協助保護您的電腦不受惡意程式碼侵襲及其他安全性威脅，並在偵測到問題時通知您。  

-   定義要監視的用戶端設定配置，並針對不相容的設定加以補救。  

-   收集硬體和軟體清查資訊，其中包括在 Microsoft 監視及協調授權資訊。  

-   使用遠端控制對電腦進行疑難排解。  

-   執行電源管理設定來管理與監視電腦的電源消耗。  

若要以接近即時的方式來監視這些操作，您需使用 Configuration Manager 主控台來檢視警示和狀態資訊。 若要擷取資料和歷史趨勢，您可以使用 SQL Reporting Services 的整合式報告功能。  用戶端會將詳細資料以用戶端狀態的形式提交給站台。  用戶端狀態資訊提供有關用戶端健康情況和用戶端活動的資料，在主控台中或透過使用 Configuration Manager 的內建報表均可檢視此資訊。 此資料可協助識別沒有回應的電腦，在某些情況下還可針對問題自動加以補救。  

 如需用戶端管理工作的詳細資訊，請參閱[如何管理 System Center Configuration Manager 中的用戶端](../../core/clients/manage/manage-clients.md)和[如何在 System Center Configuration Manager 中管理 Linux 和 UNIX 伺服器的用戶端](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md)。 若要了解如何使用報表，請參閱   
            [System Center Configuration Manager 的報告簡介](../../core/servers/manage/introduction-to-reporting.md)。  

## <a name="the-windows-control-panel-app"></a>Windows 控制台應用程式  
 當您安裝 Configuration Manager 用戶端軟體時，會一併將 **Configuration Manager** 用戶端應用程式安裝在控制台中。 與軟體中心不同，此應用程式的設計對象是技術服務人員而非一般使用者。 部分設定選項需要有本機系統管理權限，同時大部分選項都需具備 Configuration Manager 的相關技術知識。 您可以使用此應用程式在用戶端上執行下列工作︰  

-   檢視用戶端內容，例如組建編號、指派的網站、通訊的管理點以及用戶端所使用的是 PKI 憑證或自我簽署憑證。  

-   確認在第一次安裝用戶端之後是否已成功下載用戶端原則，以及是否根據 Configuration Manager 主控台中所設定之用戶端設定，如預期地啟用或停用用戶端設定。  

-   啟動用戶端動作，例如當 Configuration Manager 主控台設定最近已變更，而您不想等到下次排程時間時，即可在此先下載用戶端原則。  

-   手動指派用戶端至 Configuration Manager 站台或嘗試找到網站，然後針對發佈至 DNS 的管理點指定 DNS 尾碼。  

-   設定可暫時儲存檔案的用戶端快取，並在需要磁碟空間安裝軟體時刪除快取中的檔案。  

-   針對以網際網路為基礎的用戶端管理進行設定。  

-   檢視部署至用戶端的設定基準、起始相容性評估及檢視相容性報告。  



<!--HONumber=Dec16_HO3-->


