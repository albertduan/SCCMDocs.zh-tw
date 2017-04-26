---
title: "如何管理 Windows Device Guard | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager 來管理 Windows Device Guard。"
ms.custom: na
ms.date: 04/14/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 49599f529bb409f40caf9057989762e759f1c0ac
ms.openlocfilehash: 113dddb2939fedf24e8d489ff4443bd5e3e72c65
ms.lasthandoff: 04/18/2017


---


# <a name="device-guard-management-with-configuration-manager"></a>使用 Configuration Manager 的 Device Guard 管理

適用於：System Center Configuration Manager (最新分支)

## <a name="introduction"></a>簡介
Windows Device Guard 是一組 Windows 10 功能，其設計目的是為了保護電腦免於遭受惡意程式碼和其他未受信任軟體的攻擊。 它藉由確保只能執行您知道的已核准程式碼，來防止執行惡意程式碼。

Device Guard 包含軟體和硬體型安全性功能。 可設定的程式碼完整性是軟體型安全性層級，它會強制執行允許在電腦上執行的明確軟體清單。 可設定的程式碼完整性本身並沒有任何硬體或韌體必要條件。 以 Configuration Manager 部署的 Device Guard 原則，會在符合下述最低 Windows 版本和 SKU 需求之目標集合中的電腦上，啟用可設定的程式碼完整性原則。 (選擇性) 透過群組原則，在支援的硬體上啟用透過 Configuration Manager 部署之程式碼完整性原則的 Hypervisor 型保護。

若要深入了解 Device Guard，請閱讀 [Device Guard 部署指南](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)。

您可以使用 Configuration Manager 部署 Device Guard 原則，讓您設定 Device Guard 用來在集合中的電腦上執行的模式。 

您可以設定下列其中一種模式：

1.    **已啟用強制** - 僅允許執行信任的可執行檔。
2.    **僅稽核** - 允許執行所有可執行檔，但將執行的未受信任可執行檔記錄到本機用戶端事件記錄檔。

>[!TIP]
>在這個版本的 Configuration Manager 中，Device Guard 是發行前版本功能。 若要啟用它，請參閱 [System Center Configuration Manager 的發行前版本功能](/sccm/core/servers/manage/pre-release-features)。

### <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>當您部署 Device Guard 原則時可執行哪些項目？

Windows Device Guard 讓您強式控制可在您管理之電腦上執行的項目。 這對高安全性部門中的電腦特別有用，在這些電腦上必須禁止執行垃圾軟體。

一般而言，當您部署原則時，將會允許執行下列可執行檔：

- Windows 作業系統元件
- 硬體開發人員中心驅動程式 (具有 Windows 硬體品質實驗室簽章)
- Windows 市集應用程式
- Configuration Manager 用戶端 
- 所有透過 Configuration Manager 部署的軟體，這些是電腦在處理 Device Guard 原則之後所安裝的軟體。 
- 來自下列項目的 Windows 元件更新：
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager

>[!IMPORTANT]
>這不包括**未**內建於 Windows 的任何軟體，這些軟體不論是透過上述任何更新機制或從網際網路安裝，都會自動從網際網路或第三方軟體更新進行更新。 僅允許執行透過 Configuration Manager 用戶端部署的軟體變更。

## <a name="before-you-start"></a>開始之前

設定或部署 Device Guard 原則之前，請閱讀下列資訊：

- Device Guard 管理是 Configuration Manager 的發行前版本功能，而且可能隨時變更。
- 若要使用 Device Guard，您所管理的電腦必須執行 Windows 10 企業版 (含 Creators Update) 或更新版本。
- 在用戶端電腦上順利處理原則之後，會將 Configuration Manager 設定為該用戶端上受管理的安裝程式，而且透過 SCCM 部署的軟體會在處理原則之後自動受到信任。 Configuration Manager 在處理 Device Guard 原則之前安裝的軟體不會自動受到信任。
- 在這個發行前版本中，一旦用戶端電腦收到 Device Guard 原則的部署，就會在兩小時內隨機選擇此原則的處理時間。 
- 用戶端電腦必須連線到其網域控制站，才能順利處理 Device Guard 原則。
- Device Guard 原則的預設相容性評估排程為每隔 1 天，可在部署期間進行設定。 如果在原則處理中發現問題，將相容性評估排程設定得更短 (例如每隔 1 小時) 可能會有幫助。 此排程會指定用戶端在發生失敗時重新嘗試處理 Device Guard 原則的頻率。
- 不論您選取的強制模式為何，當您部署 Device Guard 原則時，用戶端電腦將無法執行副檔名為 .hta 的 HTML 應用程式。

## <a name="how-to-create-a-device-guard-policy"></a>如何建立 Device Guard 原則
1.    在 Configuration Manager 主控台中，按一下 [資產與合規性]。
2.    在 [資產與相容性] 工作區中，展開 [Endpoint Protection]，然後按一下 [Device Guard 原則]。
3.    在 [首頁] 索引標籤的 [建立] 群組中，按一下 [建立 Device Guard 原則]。
4.    在 [建立 Device Guard 原則精靈] 的 [一般] 頁面上，指定下列資訊：
    - **名稱** - 輸入此 Device Guard 原則的唯一名稱。 
    - **描述** - (選擇性) 輸入可協助您在 Configuration Manager 主控台中識別此原則的原則描述。
    - **強制模式** - 針對用戶端電腦上的 Device Guard，選擇下列其中一種強制方法。
        - **已啟用強制** - 僅允許執行信任的可執行檔。
        - **僅稽核** - 允許執行所有可執行檔，但將執行的未受信任可執行檔記錄到本機用戶端事件記錄檔。
5.    按一下 [下一步]，然後完成精靈。

## <a name="how-to-deploy-a-device-guard-policy"></a>如何部署 Device Guard 原則
1.    在 Configuration Manager 主控台中，按一下 [資產與合規性]。
2.    在 [資產與相容性] 工作區中，展開 [Endpoint Protection]，然後按一下 [Device Guard 原則]。
3.    從設定檔清單選取您要部署的設定檔，然後在 [首頁] 索引標籤的 [部署] 群組中，按一下 [部署]。
4.    在 [Deploy Device Guard Policy] (部署 Device Guard 原則) 對話方塊中，選取您要部署原則的目標集合，設定用戶端將評估原則的排程，最後選取用戶端是否可以在任何設定的維護期間以外評估原則。
5.    完成後，請按一下 [確定] 部署原則。 

在用戶端電腦上處理原則之後，會根據 [電腦重新啟動] 的 [用戶端設定]，在該用戶端上排程重新啟動。
**在您重新啟動用戶端電腦之前，此原則不會生效。**

## <a name="how-to-monitor-a-device-guard-policy"></a>如何監視 Device Guard 原則

使用[監視相容性設定](/sccm/compliance/deploy-use/monitor-compliance-settings)主題中的資訊，協助您監視已部署的原則，以確保已正確將它套用至所有電腦。

在用戶端電腦上使用下列記錄檔，來監視 Device Guard 原則的處理：

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

若要確認特定軟體正被封鎖或稽核，請參閱下列本機用戶端事件記錄檔。 在 [事件檢視器] 中，相關記錄檔如下所示：

1.    如需封鎖及稽核可執行檔，請使用 [應用程式及服務記錄檔] > [Microsoft] > [Windows] > [程式碼完整性] > [操作]。
2.    如需封鎖及稽核 Windows 安裝程式和指令碼檔案，請使用 [應用程式及服務記錄檔] > [Microsoft] > [Windows] > [AppLocker] > [MSI and Script] (MSI 和指令碼)。

## <a name="security-and-privacy-information-for-device-guard"></a>Device Guard 的安全性和隱私權資訊

- 在這個發行前版本中，請勿在生產環境中使用強制模式 [僅稽核] 部署 Device Guard 原則。 此模式只是為了協助您測試實驗室設定中的功能。
- 已在 [僅稽核] 模式中部署原則的裝置，或是已在 [已啟用強制] 模式中部署原則的裝置，若尚未重新啟動以強制執行原則，則很容易受到所安裝之未受信任軟體的攻擊。
在此情況下，可能會繼續允許執行軟體，即使裝置重新啟動或收到 [已啟用強制] 模式中的原則也一樣。
- 若要確保 Device Guard 原則有效，請在實驗室環境中準備裝置，部署 [已啟用強制] 原則，然後重新啟動裝置，再將裝置提供給終端使用者。
- 請勿部署 [已啟用強制] 原則，然後在稍後將 [僅稽核] 原則部署到相同的裝置。 這可能會導致允許執行未受信任的軟體。
- 當您在具有 Device Guard 原則的用戶端電腦上使用 Configuration Manager 啟用可設定的程式碼完整性時，請注意此原則**不會**防止具有本機系統管理員權限的使用者規避 Device Guard 原則，或執行未受信任的軟體。 
- 防止具有本機系統管理員權限的使用者停用可設定的程式碼完整性的唯一方法，就是部署已簽署的二進位原則，您可以透過群組原則進行部署，但 Configuration Manager 目前不支援。
- 將 Configuration Manager 設定為用戶端電腦上受管理的安裝程式會使用 AppLocker 原則。 AppLocker 只會用來識別受管理的安裝程式，所有強制作業都會透過可設定的程式碼完整性來進行。 





