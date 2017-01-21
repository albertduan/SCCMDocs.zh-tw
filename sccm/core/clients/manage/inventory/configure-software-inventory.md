---
title: "設定軟體清查 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中設定軟體清查和清查排除資料夾。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: cc226259-0e28-410a-94d3-223bdc948818
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5f30eb754832fcc259caf853dc33ccfcb82cf8bc


---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中設定軟體清查

*適用對象：System Center Configuration Manager (最新分支)*

您可以建立名為 **Skpswi.dat** 的隱藏檔案，並將它放在用戶端硬碟機的根目錄中，以將其排除於 System Center Configuration Manager 軟體清查之外。 您也可以將這個檔案放在您想要排除於軟體清查之外的任何資料夾結構的根目錄中。 這個程序可以用來停用單一工作站或伺服器用戶端  (例如大型檔案伺服器) 上的軟體清查。  

> [!NOTE]  
>  除非從用戶端電腦的用戶端磁碟機中刪除這個檔案，否則軟體清查不會重新清查磁碟機。  

### <a name="to-exclude-folders-from-software-inventory"></a>排除資料夾不進行軟體清查  

1.  使用 Notepad.exe，建立名為 **Skpswi.dat**的空白檔案。  

2.  在 **Skpswi.dat** 檔案上按一下滑鼠右鍵，然後按一下 [內容] 。 在 Skpswi.dat 檔案的檔案內容中，選取 [隱藏]  屬性。  

3.  將 **Skpswi.dat** 檔案放在您想要排除不進行軟體清查之每個用戶端硬碟機或資料夾結構的根目錄。  



<!--HONumber=Nov16_HO1-->


