---
title: "建立非作業系統部署的工作順序 | Configuration Manager"
description: "建立與部署作業系統無關的工作順序，例如散發軟體、更新驅動程式、編輯使用者狀態等等。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
caps.latest.revision: 6
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bc8ef5912f753031191a677d58d5e88f62b8d36a


---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立非作業系統部署的工作順序

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的工作順序是用來將環境中的各種工作自動化。 這些工作主要針對部署作業系統來進行設計和測試。  Configuration Manager 具有許多其他功能，這些功能應為您在某些案例中所使用的主要技術，像是[應用程式安裝](../../apps/understand/introduction-to-application-management.md)、[軟體更新安裝](../../sum/understand/software-updates-introduction.md)、[設定組態](../../compliance/understand/ensure-device-compliance.md)，或自訂自動化。 還有其他的 Microsoft System Center 自動化技術，例如 [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) 和 [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) 等等，都是您應該考慮的項目。  

 工作順序的厲害之處在於其彈性，以及您可以如何使用這些工作順序來設定用戶端設定、發佈軟體、更新驅動程式、編輯使用者狀態，並執行與作業系統部署無關的其他工作。 您可以建立自訂工作順序以新增任何數量的工作。 雖然支援使用基本的非作業系統部署自訂工作順序，但因為無法測試所有可能的設定，所以當您開發更複雜的工作順序時，發生問題的機會便會增加。  

 下列步驟可以在非作業系統部署自訂工作順序中使用：  

-   [檢查整備程度](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [連線到網路資料夾](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [下載套件內容](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [安裝應用程式](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [安裝套件](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [安裝軟體更新](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [重新啟動電腦](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)  

-   [執行命令列](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [執行 PowerShell 指令碼](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [設定動態變數](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [設定工作順序變數](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>後續步驟
[部署工作順序](manage-task-sequences-to-automate-tasks.md#a-namebkmkdeploytsa-deploy-a-task-sequence)



<!--HONumber=Nov16_HO1-->


