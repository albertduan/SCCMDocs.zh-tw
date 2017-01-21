---
title: "System Center Configuration Manager 隱私權聲明 - Configuration Manager Cmdlet 程式庫"
description: "了解 Microsoft 如何收集和使用 System Center Configuration Manager Cmdlet 程式庫的相關資料。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 88d11aaed4a0e6575cb859f5dfc3ac425bd2bf38


---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>System Center Configuration Manager 隱私權聲明 - Configuration Manager Cmdlet 程式庫

*適用於：System Center Configuration Manager (最新分支)*

本隱私權聲明涵蓋 System Center Configuration Manager Cmdlet 程式庫的功能。  

## <a name="usage-data"></a>使用方式資料  
 **此功能的作用：**   
您可利用 System Center Configuration Manager Cmdlet 程式庫，透過 Windows PowerShell Cmdlet 與指令碼，來管理 Configuration Manager 階層。 Cmdlet 程式庫會收集有關您如何使用程式庫中內含 Cmdlet 的資訊，以找出趨勢及使用習慣。  Cmdlet 程式庫也會收集您使用 Cmdlet 時所遇到的錯誤類型與數目。  

 **收集、處理或傳輸的資訊：**   
收集的使用方式資料包括啟動、停止及終止 Cmdlet、執行已被取代的 Cmdlet，以及與 Cmdlet 相關之 SMS 提供者作業的活動指標。 這項資訊不具個人識別性質。  收集的錯誤資訊包括 Cmdlet 所傳回的錯誤，以及例外狀況錯誤的錯誤詳細資料。 某些錯誤詳細資料報表可能會不小心包含了個人識別資料，例如連接至您電腦的裝置序號。 Cmdlet 程式庫會篩選錯誤報表中內含的資訊，並會以匿名方式處理資訊，在將資訊傳輸給 Microsoft 之前，移除掉可識別的個人資訊。  

 **資訊的用途：**   
我們可使用這項資訊，改善所提供的產品與服務之品質、安全性與完整性。  

 **選擇/控制：**   
預設會啟用此使用方式資料功能。 System Center Configuration Manager Cmdlet 程式庫包含兩個登錄機碼可控制這項功能。  

 若要完全退出，您需要設定這兩個登錄機碼值，每個 Windows 事件追蹤 (ETW) 提供者各一個登錄機碼值：  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (且不使用磁碟機提供者的使用方式資料)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (且不使用 Cmdlet 的使用方式資料)  

 使用方式資料設定的變更，只對進行變更的電腦有效。  

 如需如何設定使用方式資料 (集合) 的詳細資訊，請參閱 [System Center Configuration Manager Cmdlet 程式庫文件](https://technet.microsoft.com/en-us/library/dn958404.aspx)。  

## <a name="update-check"></a>更新檢查  
 **此功能的作用：**   
System Center Configuration Manager Cmdlet 程式庫會每天自動檢查是否有程式庫更新，並會通知您下載更新的程式庫。  

 **收集、處理或傳輸的資訊：**   
Cmdlet 程式庫更新檢查會從 Microsoft 下載中心下載小型的文字檔，以進行版本檢查。   這個檔案不會儲存在本機。  Cmdlet 程式庫不會自動升級軟體。  

 **資訊的用途：**   
我們可使用這項資訊，改善所提供的產品與服務之品質、安全性與完整性。  

 **選擇/控制：**   
預設會啟用 [更新檢查]。  System Center Configuration Manager Cmdlet 程式庫包含這些 Cmdlet 以控制更新通知功能：  

-   `Get-CMCmdletUpdateCheck` 可取得更新功能組態，並會指出使用者原則是否已遭到系統原則的覆寫。  

-   `Send-CMCmdletUpdateCheck` 可供您執行非排程的更新檢查。 非排程的檢查不會考慮原則設定。  

-   `Set-CMCmdletUpdateCheck` 會以使用者為單位或以系統為單位，來設定更新檢查設定。 您必須以系統管理員的身分執行，才可進行系統設定。  

 您可以在 [System Center Configuration Manager Cmdlet 程式庫文件](https://technet.microsoft.com/en-us/library/dn958404.aspx)中找到如何設定更新檢查的詳細資訊。  



<!--HONumber=Nov16_HO1-->


