---
title: "軟體清查 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中的軟體清查簡介。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a468ce93e9536fe3f6bf0fc191ff9764dd1c3343
ms.openlocfilehash: 401ba6e37d740310d49ab9e96112ce576d7130e4


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的軟體清查簡介

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 中的軟體清查功能，可用來收集組織中用戶端裝置上所包含之檔案的相關資訊。 此外，軟體清查可從用戶端裝置收集檔案，並將這些檔案儲存到站台伺服器。 當啟用用戶端設定中的 [在用戶端上啟用軟體清查]  設定時，會收集軟體清查。  

 在啟用軟體清查且用戶端執行軟體清查週期之後，用戶端會將清查資訊傳送至用戶端站台中的一個管理點。 管理點接著會將清查資訊轉送至 Configuration Manager 站台伺服器，再由該伺服器將清查資訊儲存到站台資料庫。 軟體清查會根據您在用戶端設定中指定的排程在用戶端上執行。  

 您可以使用多種方法來檢視 Configuration Manager 所收集的軟體清查資料。 包含以下各項：  

-   建立查詢，以根據您所指定並在裝置上找到的檔案，來傳回裝置。 如需詳細資訊，請參閱 [System Center Configuration Manager 的查詢技術參考](../../../../core/servers/manage/queries-technical-reference.md)。  

-   建立查詢式集合，該集合以您所指定並在裝置上找到的檔案為基礎。 查詢式集合成員資格會依照排程自動更新。 您可以針對許多工作 (例如軟體部署) 使用集合。 如需詳細資訊，請參閱 [System Center Configuration Manager 的集合簡介](../../../../core/clients/manage/collections/introduction-to-collections.md)。  

-   執行報告，以顯示組織中裝置上之檔案的特定詳細資料。 如需詳細資訊，請參閱 [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md) (System Center Configuration Manager 中的報告)。  

-   使用資源總管，查看從用戶端裝置清查及收集之檔案的詳細資訊。 如需詳細資訊，請參閱[如何使用資源總管檢視 System Center Configuration Manager 的軟體清查](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)。  

 當軟體清查在用戶端裝置上執行時，第一個傳回的清查報告一律是完整清查。 後續的清查報告只會包含差異清查資訊。 站台伺服器會依差異清查資訊收到的順序來進行處理。 如果遺漏某個用戶端的差異清查資訊，站台伺服器會拒絕進一步的差異清查資訊，並指示該用戶端執行完整清查週期。  

 Configuration Manager 提供雙重開機電腦的有限支援。 Configuration Manager 可以探索雙重開機電腦，但只會傳回清查時仍作用中的作業系統清查資訊。  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>向 Microsoft Intune 註冊之行動裝置的軟體清查  
 您可以收集行動裝置上所安裝之應用程式的清查。 清查的應用程式視裝置為公司所有或為個人所有而定。 若為個人裝置，將只會清查 Microsoft Intune 所管理的應用程式。  

> [!NOTE]  
>  行動裝置上所安裝之應用程式的清查會在 Configuration Manager 的硬體清查過程中收集。 如需詳細資訊，請參閱[如何為 Microsoft Intune 與 Configuration Manager 註冊的行動裝置設定硬體清查](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md)。  

 下表列出針對屬個人擁有的裝置或屬公司擁有的裝置所清查的應用程式。  

|平台|屬個人擁有的裝置|屬公司擁有的裝置|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (不含 Configuration Manager 用戶端)|僅限受管理的應用程式|僅限受管理的應用程式| 
|Windows 8.1 (不含 Configuration Manager 用戶端)|僅限受管理的應用程式|僅限受管理的應用程式|  
|Windows Phone 8|僅限受管理的應用程式|僅限受管理的應用程式|  
|Windows RT|僅限受管理的應用程式|僅限受管理的應用程式|  
|iOS|僅限受管理的應用程式|安裝在裝置上的所有應用程式|  
|Android|僅限受管理的應用程式|安裝在裝置上的所有應用程式|  



<!--HONumber=Dec16_HO3-->


