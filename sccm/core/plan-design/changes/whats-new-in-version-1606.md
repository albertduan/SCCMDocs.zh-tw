---
title: "1606 的新功能 | System Center Configuration Manager"
description: "下列各節提供 System Center Configuration Manager 1606 版中的變更和推出的新功能。"
ms.custom: na
ms.date: 10/09/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
caps.latest.revision: 40
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: 8de28e112a2d7faf1d8aca9b7214498e9a65f919

---
# <a name="what39s-new-in-version-1606-of-system-center-configuration-manager"></a>System Center Configuration Manager 1606 版的新功能

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 1606 更新，是執行版本為 1511 或 1602 或 1606 的原安裝站台提供的更新。 1511 版是您用來安裝新 Configuration Manager 站台的初始基準版本。
> [!TIP]  
>  深入了解：  
>   
>  -   [安裝新的站台](/sccm/core/servers/deploy/install) (使用 1511 等基準版本)  
>  -   [在站台安裝更新](/sccm/core/servers/manage/updates) (如更新 1602 或 1606)  

 下列各節提供 Configuration Manager 1606 版中的變更和推出的新功能詳細資料。  



## <a name="a-nameupdatesandservicingaupdates-and-servicing"></a><a name="updatesandservicing"></a>更新及服務

### <a name="changes-for-the-updates-and-servicing-node"></a>更新和服務節點有所變更
Configuration Manager 主控台的更新與服務變更如下︰
> [!NOTE]
> 要安裝 1606 版後才能使用這些變更。

- **節點名稱變更：**

    在 [監視] 工作區中，[Site Servicing status] (站台服務狀態) 節點已重新命名為 [更新與服務狀態]。
- **更多安裝狀態：**

    當您檢視站台的更新安裝狀態時，主控台現在會分開顯示下列動作的詳細資料：
    - **下載** (僅適用於服務連接點站台系統角色安裝所在的頂層站台)
    - **複寫**
    - **必要條件檢查**
    - **安裝**

  此外，現在各步驟都有更詳細的資訊，包括在哪一個記錄檔中可以檢視詳細資訊。  
-   **新增在先決條件失敗時重試的選項︰**

    在 [管理] 和 [監視] 工作區的 [更新與服務] 節點，其功能區上皆包含名為 [忽略先決條件警告] 的新按鈕。

    當您從 [更新精靈] 安裝更新時未使用 [忽略先決條件警告] 的選項，但該更新安裝突然停止並處於**先決條件警告**的狀態中，您可以選取功能區上的 [忽略先決條件警告]，觸發自動接續安裝要忽略先決條件警告的這項更新。  



- **更整潔的更新檢視畫面：**

    當您檢視 [更新與服務] 節點時，您現在只會看到最近安裝的更新，以及可供安裝之任何新的更新。 若要檢視先前安裝的更新，請按一下功能區顯示的新 [歷程記錄] 按鈕。  

-   **進入生產階段前已重新命名的選項︰**

    在 [更新與服務] 節點中，原稱為 [Client options] 的按鈕現在已重新命名為 [將生產階段前用戶端升階]。


###  <a name="pre-release-features"></a>發行前版本功能
從 1606 開始，您必須同意使用 System Center Configuration Manager 中的發行前版本功能，才可以選取功能並啟用其用法。 如需詳細資訊，請參閱[使用發行前版本功能](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)。

### <a name="new-distribution-point-update-behavior"></a>新的發佈點更新行為
更新 1606 推出的變更，可在安裝未來更新時提高發佈點的可用性。

安裝更新 1606 之後，當您下次在需要自動重新安裝標準及提取發佈點站台系統角色的該站台安裝更新時，所有發佈點不會再同時離線更新。 反之，站台伺服器會使用站台的內容發佈設定，逐一將更新發佈至發佈點子集。 這樣一來，只有部分發佈點會設為離線以安裝更新。 如此可讓還沒有開始更新或已完成更新的發佈點保持線上狀態，以提供內容給用戶端。



## <a name="a-nameaccessibilitya-accessibility"></a><a name="accessibility"></a> 協助工具
自 1606 版開始，若要瀏覽到工作區的不同節點，您可以輸入節點名稱的第一個字母。 每個按鍵動作都會游標移至以該字母開頭的下一個節點，而且在使用螢幕助讀程式時，助讀程式會讀出該節點的名稱。 如需協助工具選項的詳細資訊，請參閱 [System Center Configuration Manager 的協助工具功能](../../../core/understand/accessibility-features.md)。

## <a name="a-nameadministrationaadministration"></a><a name="administration"></a>管理
Configuration Manager 主控台的管理變更如下︰
### <a name="oms-connector"></a>OMS 連接器

您現在可以將 Configuration Manager 當成集合從 System Center Configuration Manager 連接到 [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/en-us/documentation/articles/operations-management-suite-overview/)。 這樣就可以在 OMS 中顯示 Configuration Manager 部署的資料，如集合。 詳細資訊請參閱[將 Configuration Manager 的資料同步處理到 Microsoft Operations Management Suite](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md)。

OM 連接器是發行前版本的功能。 若要啟用它，請參閱[使用更新的發行前版本功能](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)。

### <a name="support-for-cache-size-in-client-settings"></a>用戶端設定的快取大小支援

您現在可以在 Configuration Manager 主控台中，使用用戶端設定在用戶端電腦上設定快取資料夾的大小。 過去只能在安裝或重新安裝用戶端軟體時，設定用戶端的快取大小 (使用 SMSCACHESIZE 屬性)。 現在可以將快取大小指定為用戶端設定 (預設或自訂)，然後將這些設定與下一個原則更新套用到用戶端，不必重新安裝用戶端。 如需詳細資訊，請參閱[設定 Configuration Manager 用戶端的用戶端快取](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache)。

## <a name="on-premises-mobile-device-management"></a>內部部署行動裝置管理

### <a name="support-for-multiple-device-management-points"></a>對多個裝置管理點的支援

內部部署行動裝置管理 (MDM) 現在支援 Windows 10 年度更新版中的一項新功能，該功能會自動設定已註冊的裝置，以提供多個可供使用的裝置管理點。 這項功能允許通常使用的裝置無法使用時，以其他裝置管理點代替。 這項功能只適用於安裝 Windows 10 年度更新版的電腦及裝置。


## <a name="application-management"></a>應用程式管理

### <a name="manage-apps-from-the-windows-store-for-business"></a>從商務用 Windows 市集管理應用程式

[商務用 Windows 市集](https://www.microsoft.com/business-store)是您可以在其中為您的組織尋找並個別或大量購買 Windows 應用程式的地方。 藉由將市集連線到 Configuration Manager，您就可以同步處理使用 Configuration Manager 所購買的應用程式清單、在 Configuration Manager 主控台中進行檢視，以及像是任何其他應用程式一樣進行部署。

如需詳細資訊，請參閱[使用 System Center Configuration Manager 管理從商務用 Windows 市集購買的應用程式](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)。

### <a name="manage-ios-volume-purchased-apps"></a>管理 iOS 大量採購應用程式

已改善管理大量採購 iOS 應用程式及使用 Configuration Manager 部署的工作流程。

如需詳細資料，請參閱[使用 Configuration Manager 管理您透過大量採購方案購買的 iOS 應用程式](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md)。

### <a name="software-center-user-interface"></a>軟體中心使用者介面

軟體中心介面已簡化，讓使用者體驗更簡單容易的瀏覽。
*  [安裝狀態] 和 [安裝的軟體] 索引標籤已合併為單一的 [安裝狀態] 索引標籤。
*  [更新]、[作業系統] 和 [應用程式] 已分隔成三個不同的索引標籤。
* 現在可以選取多個更新一次安裝，或按一下 [Install All] (全部安裝) 按鈕一次安裝所有更新。

### <a name="content-status-links"></a>內容狀態連結
檢視應用程式或套件的內容時，現在有連結帶您前往該物件的狀態。

## <a name="software-updates"></a>軟體更新

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>管理 Office 365 用戶端代理程式的用戶端設定
您現在可以使用 Configuration Manager 用戶端設定來管理 Office 365 用戶端代理程式。 在設定這項設定並部署 Office 365 更新之後，Configuration Manager 用戶端代理程式會與 Office 365 用戶端代理程式進行通訊，從發佈點下載 Office 365 更新並安裝它們。

如需詳細資訊，請參閱[使用 Configuration Manager 管理 Office 365 ProPlus 更新](../../../sum/deploy-use/manage-office-365-proplus-updates.md)。

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>手動將用戶端切換到新軟體更新點
您現在可以啟用可供 Configuration Manager 用戶端在主動式軟體更新點發生問題時切換到新軟體更新點的選項。 啟用之後，用戶端會在下次掃描時尋找另一個軟體更新點。

如需詳細資訊，請參閱[在 Configuration Manager 中規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs)。

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>提供在安裝軟體更新後重新啟動 Windows 10 用戶端的選項
如果需要重新啟動的軟體更新使用 Configuration Manager 來進行部署並安裝於電腦上，則會排定擱置重新啟動，並顯示重新啟動對話方塊。 從 Configuration Manager 版本 1606 開始，只要 Configuration Manager 軟體更新擱置重新啟動，處於 Windows 電源選項的 Windows 10 電腦上就會有 **[更新並重新啟動]**和 **[更新並關機]** 選項。 使用其中一個選項之後，在重新開機之後不會顯示重新啟動對話方塊。

如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions)。

## <a name="operating-system-deployment"></a>作業系統部署

### <a name="improvements-to-the-install-software-updates-task-sequence-step"></a>改進安裝軟體更新工作順序的步驟
[從快取掃描結果評估軟體更新] 這項新設定可讓您選擇執行完整掃描軟體更新，而不是使用快取的掃描結果。 如需詳細資訊，請參閱 [System Center Configuration Manager 的工作順序步驟](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)。

您也可以使用新的工作順序變數 **SMSTSSoftwareUpdateScanTimeout**，在「安裝軟體更新」工作順序步驟期間，控制軟體更新掃描的逾時。 預設值為 30 分鐘。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的工作順序內建變數](../../../osd/understand/task-sequence-built-in-variables.md)。

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>OSDPreserveDriveLetter 工作順序變數已被取代
從 Configuration Manager 1606 版開始，OSDPreserveDriveLetter 工作順序變數已被取代。 從 Configuration Manager 1606 版開始，Windows 安裝程式在作業系統部署期間，預設會決定使用最佳的磁碟機代號 (通常是 C:)。

如需詳細資訊，請參閱 [System Center Configuration Manager 中的工作順序內建變數](../../../osd/understand/task-sequence-built-in-variables.md)。

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>自訂 PXE 之發佈點的 RamDisk TFTP 視窗大小
您現在可以自訂 PXE 之發佈點的 RamDisk TFTP 視窗大小。 如果您已自訂網路，可能會導致開機映像下載因發生逾時錯誤而失敗，因為視窗大小太大。 自訂 RamDisk TFTP 視窗大小可讓您在使用 PXE 來滿足特定的網路需求時，將 TFTP 流量最佳化。

如需詳細資訊，請參閱[使用 System Center Configuration Manager 為作業系統部署準備站台系統角色](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)。

## <a name="compliance-settings"></a>相容性設定

### <a name="smart-lock-setting-for-android-devices"></a>Android 裝置的 SmartLock 設定
[允許 Smart Lock 和其他信任代理程式] 這項新設定已新增至 Android 和 Samsung KNOX 設定項目。

此設定可讓您控制相容 Android 裝置上的 Smart Lock 功能。 此電話功能 (有時也稱為信任代理程式) 可讓您在裝置位於受信任的位置 (例如連線到特定的藍牙裝置或靠近 NFC 標記) 時，停用或略過裝置鎖定畫面密碼。 您可以使用此設定來防止使用者設定 Smart Lock。

如需詳細資料，請參閱[如何為不是使用 System Center Configuration Manager 用戶端所管理的 Android 和 Samsung KNOX 裝置建立設定項目](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)。

## <a name="device-configuration-and-protection"></a>裝置的設定與保護

### <a name="product-name-changes"></a>產品名稱變更

* Microsoft Passport for Work 現在稱為 **Windows Hello 企業版**。
* 企業資料保護現在稱為 **Windows 資訊保護**。

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Windows Hello 企業版的部署 (Passport for Work)

您現在可以將 Windows Hello 企業版原則部署至受 Configuration Manager 用戶端管理且已加入網域的 Windows 10 裝置。

已更新 Configuration Manager 主控台以反映這些變更。

### <a name="ios-activation-lock"></a>iOS 啟用鎖定
Configuration Manager 可以協助您管理 iOS 啟用鎖定，這是 iOS 7.1 和更新版本裝置之「尋找我的 iPhone」應用程式中的功能。 啟用「啟用鎖定」時，必須先輸入使用者的 Apple ID 和密碼，才能讓所有人：
* 關閉「尋找我的 iPhone」
* 清除裝置
* 重新啟動裝置

Configuration Manager 可以透過兩種方式協助您管理啟用鎖定：

1. 在受監督裝置上啟用「啟用鎖定」。
2. 在受監督裝置上略過「啟用鎖定」。

如需詳細資訊，請參閱[使用 System Center Configuration Manager 管理 iOS 啟用鎖定](../../../mdm/deploy-use/manage-ios-activation-lock.md)。


### <a name="windows-defender-advanced-threat-protection"></a>Windows Defender 進階威脅防護

Endpoint Protection 可協助管理及監視 Windows Defender 進階威脅防護 (ATP)。 Windows Defender ATP 是新的服務，可協助企業偵測、調查和回應其網路的進階攻擊。 Configuration Manager 原則可協助您上架及監視受管理的 Windows 10 1607 版 (版本 14328)。

如需詳細資訊，請參閱 [Windows Defender 進階威脅防護](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md)。

### <a name="device-categories"></a>裝置類別
您可以建立裝置類別，如此可在您使用 Configuration Manager 與 Microsoft Intune 時自動將裝置放在裝置集合中。 使用者向 Intune 註冊裝置時，必須選擇裝置類別。 您也可以從 Configuration Manager 主控台中變更裝置類別。

如需詳細資訊，請參閱[如何使用 System Center Configuration Manager 自動將裝置分類為集合](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md)。

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>使用 IMEI 或 iOS 序號預先宣告裝置

您可以透過匯入國際站移動設備識別碼 (IMEI) 號碼或 iOS 序號，識別公司擁有的裝置。 您可以上傳一個包含裝置 IMEI 編號的逗號分隔值 (.csv) 檔案，也可以手動輸入裝置資訊。 匯入的資訊將會設定裝置清單中註冊為**公司**之裝置的**擁有權**。 每一位存取服務的使用者還是需要 Intune 授權。

如需詳細資訊，請參閱[使用 IMEI 或 iOS 序號預先宣告裝置](../../../mdm/deploy-use/predeclare-devices-with-hardware-id.md)。

### <a name="on-premises-health-attestation-service-communication"></a>內部部署健康情況證明服務通訊

您現在可以只使用內部部署基礎結構，啟用 Windows 10 電腦的健康情況證明服務監視，讓沒有網際網路存取的電腦也可以報告裝置健康情況證明 (DHA)。

如需詳細資料，請參閱 [System Center Configuration Manager 的健康情況證明](../../../core/servers/manage/health-attestation.md#How-to-enable-Health-Attestation-service-communication-on-Configuration-Manager-client-computers)。  

## <a name="remote-control"></a>遠端控制
讓使用者在遠端控制工作階段中，從共用剪貼簿傳輸內容之前，有機會接受或拒絕檔案傳輸。 使用者只需要每個工作階段授與權限一次，而檢視人員不能自我授權進行檔案傳輸。 這項新設定位在 [管理] 工作區的 [用戶端設定] 下 [預設設定] 的 [遠端工具] 面板中。



<!--HONumber=Nov16_HO1-->


