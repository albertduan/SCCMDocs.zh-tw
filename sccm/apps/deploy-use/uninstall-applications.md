---
title: "解除安裝應用程式 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager 解除安裝應用程式"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9f654d899a1e3e1603eccb3943ffc4d4c178e143


---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 解除安裝應用程式

*適用於：System Center Configuration Manager (最新分支)*


## <a name="introduction"></a>簡介  
  
-   指定命令列，在 [建立部署類型精靈]  的 [內容] 頁面中解除安裝部署類型內容。  

-   使用 [解除安裝] 的部署動作部署應用程式。  

> [!IMPORTANT]  
>  某些應用程式類型不支援解除安裝。  

 下表提供有關應用程式解除安裝行為的詳細資訊：  

-   當您解除安裝 Configuration Manager 應用程式時，不會自動解除安裝任何相依的應用程式。  

-   如果將使用 [解除安裝]  動作的應用程式部署至使用者，且為該電腦的所有使用者安裝該應用程式，則當使用者的帳戶沒有解除安裝應用程式的權限時，解除安裝作業可能會失敗。  

-   如果從已部署應用程式的集合中移除使用者或裝置，並不會自動從裝置移除該應用程式。  

-   部署目的為 [解除安裝]  的部署作業並不會檢查需求規則。 如果應用程式是安裝在部署執行的電腦上，則會被解除安裝。  

> [!IMPORTANT]  
>  您必須先刪除集合應用程式的任何現有部署或模擬部署，才能使用 [解除安裝] 部署動作部署該應用程式。  
  
 如需如何建立部署類型的詳細資訊，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。  
  
 如需如何部署應用程式的詳細資訊，請參閱[部署應用程式](../../apps/deploy-use/deploy-applications.md)。  
  
## <a name="uninstall-an-application"></a>解除安裝應用程式  

1.  使用下列任一方法，以解除安裝命令列設定應用程式部署類型：  

    -   在 [建立部署精靈]  的 [一般] 頁面中，選取 [自動從安裝檔案識別此部署類型的相關資訊] 選項。 如果安裝檔案中包含資訊，便會自動將解除安裝命令列新增到部署類型內容中。  

    -   在 [建立部署類型精靈]  的 [一般] 頁面中，在 [解除安裝程式]  欄位指定用於解除安裝應用程式的命令列。  

        > [!NOTE]  
        >  在 [建立部署類型精靈]  的 [一般]  頁面中，必須選取 [手動指定部署類型資訊]  選項，才會顯示 [內容] 頁面。  

    -   在 [*<部署類型名稱\>* 內容] 對話方塊的 [程式] 索引標籤中，在 [解除安裝程式] 欄位指定用於解除安裝應用程式的命令列。  

2.  部署應用程式並從 [部署軟體精靈]  中的 [部署設定]  頁面選取 [解除安裝] 部署動作。  

    > [!NOTE]  
    >  選取 [解除安裝] 部署動作時，會自動將部署目的設定為 [必要] 。  



<!--HONumber=Nov16_HO1-->


