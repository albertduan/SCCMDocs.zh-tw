---
title: "軟體清查 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中的軟體清查簡介。"
ms.custom: na
ms.date: 12/26/2016
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
ms.sourcegitcommit: 9206b82eca02877c30eebf146d42bcca7290eb42
ms.openlocfilehash: c9956dd4ef94a1b109d761e44e42f512c42eb8d2


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的軟體清查簡介

適用於：System Center Configuration Manager (最新分支)

軟體清查可用來收集用戶端裝置上檔案的相關資訊。 軟體清查也可以從用戶端裝置收集檔案，並將這些檔案儲存到站台伺服器。 選擇用戶端設定中的 [在用戶端上啟用軟體清查] 設定時，會收集軟體清查，而您也可以在用戶端設定中排定作業。  

在啟用軟體清查且用戶端執行軟體清查週期之後，用戶端會將資訊傳送至用戶端站台中的一個管理點。 管理點接著會將清查資訊轉送至 Configuration Manager 站台伺服器，再由該伺服器將資訊儲存到站台資料庫。   

 以下是檢視軟體清查資料的方法︰  

-   [建立查詢](../../../../core/servers/manage/queries-technical-reference.md)，以傳回具有所指定檔案的裝置。   

-   [建立查詢](../../../../core/clients/manage/collections/introduction-to-collections.md)，以傳回具有所指定檔案的裝置。   

-   [執行報告](../../../../core/servers/manage/reporting.md)，以提供裝置上檔案的詳細資料。 

-   使用[資源總管](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)，檢查從用戶端裝置清查及收集之檔案的詳細資訊。   

 當軟體清查在用戶端裝置上執行時，第一份報告是完整清查。 後續報告只會包含差異清查資訊。 站台伺服器會依差異資訊收到的順序來進行處理。 如果遺漏用戶端的差異資訊，站台伺服器會拒絕之後的差異資訊，並指示該用戶端執行完整清查。  

 Configuration Manager 可以探索雙重開機電腦，但只會傳回清查時仍作用中的作業系統清查資訊。  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>向 Microsoft Intune 註冊之行動裝置的軟體清查  
 您可以收集行動裝置上所安裝之應用程式的清查。 清查的應用程式視裝置為公司所有或為個人所有而定。 若為個人裝置，將只會清查 Microsoft Intune 所管理的應用程式。  

> [!NOTE]  
>  行動裝置上所安裝之應用程式的清查會在[硬體清查](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md)過程中收集。  

 以下是針對個人擁有的裝置或公司擁有的裝置所清查的應用程式。  

|平台|屬個人擁有的裝置|屬公司擁有的裝置|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (不含 Configuration Manager 用戶端)|僅限受管理的應用程式|僅限受管理的應用程式| 
|Windows 8.1 (不含 Configuration Manager 用戶端)|僅限受管理的應用程式|僅限受管理的應用程式|  
|Windows Phone 8|僅限受管理的應用程式|僅限受管理的應用程式|  
|Windows RT|僅限受管理的應用程式|僅限受管理的應用程式|  
|iOS|僅限受管理的應用程式|安裝在裝置上的所有應用程式|  
|Android|僅限受管理的應用程式|安裝在裝置上的所有應用程式|  





<!--HONumber=Dec16_HO5-->


