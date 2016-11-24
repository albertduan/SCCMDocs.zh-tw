---
title: "模擬應用程式部署 | System Center Configuration Manager"
description: "評估部署類型的偵測方法、需求和相依性，而不需要安裝應用程式。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a7d9267d35b58fdc6a01b869eb739e9c721db4a4


---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 模擬應用程式部署

*適用於：System Center Configuration Manager (最新分支)*

您可以使用模擬部署來測試將應用程式部署到電腦的適用性，而無須實際安裝或解除安裝應用程式。 模擬部署會評估部署類型的偵測方法、需求和相依性，並且在 [監視]  工作區的 [部署]  節點中回報結果。 請使用本主題中的程序，在 System Center Configuration Manager 中模擬應用程式部署。  

> [!NOTE]  
>  您不能在行動裝置集合中使用模擬部署。  
>   
>  如果某個應用程式的模擬部署正在使用中，就不能以 [解除安裝]  為部署目的來部署該應用程式。  
  
使用下列程序，設定模擬應用程式部署：
  
1.  在 Configuration Manager 主控台中選取下列其中一項：  

    -   使用者集合。  

    -   裝置集合。  

    -   Configuration Manager 應用程式。  

2.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [模擬部署] 。  

3.  在 [模擬應用程式部署精靈] 中指定下列資訊：  

    -   **應用程式** - 按一下 [瀏覽]  ，然後選取要用於建立模擬部署的應用程式。  

    -   **集合** - 按一下 [瀏覽]  ，然後選取要用於模擬部署的集合。  

    -   **動作** - 從下拉式清單中選取要模擬所選應用程式的安裝或解除安裝作業。  

    -   **使用或不使用使用者登入自動部署** - 如果勾選此選項，無論使用者是否登入用戶端，用戶端都會評估模擬部署。  

4.  按 [下一步] ，檢閱 [摘要]  頁面中的資訊，然後完成精靈以建立模擬應用程式部署。  

5.  模擬應用程式會出現在 [監視]  工作區的 [部署]  節點中，目的為 [模擬] 。 如需如何監視應用程式部署的詳細資訊，請參閱[從 System Center Configuration Manager 主控台監視應用程式](../../apps/deploy-use/monitor-applications-from-the-console.md)。  



<!--HONumber=Nov16_HO1-->


