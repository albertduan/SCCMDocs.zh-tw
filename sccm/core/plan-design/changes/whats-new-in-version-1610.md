---
title: "1610 版的新功能 | Microsoft Docs"
description: "下列各節提供 System Center Configuration Manager 1610 版中的變更和推出的新功能。"
ms.custom: na
ms.date: 
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
caps.latest.revision: 40
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: 5121073a335f6722ea1e6cf7669edbf13ba3f9db

---
# <a name="what39s-new-in-version-1610-of-system-center-configuration-manager"></a>System Center Configuration Manager 1610 版的新功能

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 1610 更新最新分支，是執行版本為 1511、1602 或 1606 的原安裝站台提供的主控台內更新。


> [!TIP]  
> 若要安裝新的站台，您必須使用 Configuration Manager 的基準版本。  
>  深入了解：    
>  -   [安裝新的站台](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [在站台安裝更新](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [基準和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

下列各節提供 Configuration Manager 1610 版中的變更和推出的新功能詳細資料。  


## <a name="in-console-monitoring-of-update-installation-status"></a>更新安裝狀態的主控台內監視功能  
從 1610 版起，當您在主控台內安裝更新套件並進行監視時，還有「後續安裝」這個新的階段。 這個階段包含重新啟動重要服務，以及初始化複寫監視等工作的狀態 (只有當您的站台已更新至 1610 版時，主控台才會提供這個階段)。如需更新安裝狀態的詳細資訊，請參閱[安裝主控台內更新](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)。


## <a name="exclude-clients-from-automatic-upgrade"></a>排除自動升級用戶端
升級新版本的用戶端軟體時，您可以讓 Windows 用戶端不要升級。 若要這樣做，請在指定要排除升級的集合中納入該用戶端電腦。 針對排除集合中的用戶端，系統會忽略更新用戶端軟體的要求。  如需詳細資訊，請參閱[讓 Windows 用戶端不要升級](../../clients/manage/upgrade/exclude-clients-windows.md)。


## <a name="improvements-for-boundary-groups"></a>界限群組的改進
針對界限群組以及界限群組使用發佈點的方式，1610 版導入了一些重要變更。 這些變更可簡化內容基礎結構的設計，同時讓您更充分掌控用戶端如何及何時進行後援，以搜尋其他發佈點作為內容來源位置。 這包括內部部署和雲端架構的發佈點。
這些改進將您可能很熟悉的現今概念和行為 (例如將發佈點設定為快速或低速)，取代成更容易設定和維護的新模型。 這些變更也是未來變更的基礎，未來變更將會改進要與界限群組關聯的其他站台系統角色。

更新至 1610 版時，更新會將您目前的界限群組設定轉換為符合新的模型，讓這些變更不會干擾您現有的內容發佈設定。

如需詳細資訊，請參閱[界限群組](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-groups)。


## <a name="peer-cache-for-content-distribution-to-clients"></a>可將內容發佈至用戶端的對等快取
從 1610 版開始，用戶端的「對等快取」可協助您管理部署至遠端位置用戶端的內容。 對等快取是一個內建的 Configuration Manager 解決方案，可讓用戶端直接將其本機快取的內容與其他用戶端共用。

將啟用對等快取的用戶端設定部署至集合之後，該集合的成員就能作為同一個界限群組中其他用戶端的對等內容來源。

您也可以使用新的 [用戶端資料來源] 儀表板，來了解環境中「對等快取」內容來源的使用情況。

> [!TIP]  
> 在版本 1610，對等快取和用戶端資料來源儀表板都是發行前版本功能。 若要啟用它們，請參閱[使用更新的發行前版本功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。

如需詳細資訊，請參閱 [Configuration Manager 用戶端的對等快取](/sccm/core/plan-design/hierarchy/client-peer-cache)以及[用戶端資料來源儀表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>同時移轉多個共用的發佈點
現在，您可以使用 [重新指派發佈點] 選項，同時平行處理 Configuration Manager 程序與最多 50 個共用發佈點的重新指派。 在此版本之前，系統只能一次處理一個重新指派的發佈點。 如需詳細資訊，請參閱[同時移轉多個共用的發佈點](/sccm/core/migration/planning-a-content-deployment-migration-strategy#migrate-multiple-shared-distribution-points-at-the-same-time)。

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>可管理以網際網路為基礎之用戶端的雲端管理閘道

雲端管理閘道可讓您輕鬆管理網際網路上的 Configuration Manager 用戶端。 Microsoft Azure 有部署雲端管理閘道服務，其需要 Azure 訂閱，且會使用雲端管理閘道連接點這個新角色，連接到內部部署的 Configuration Manager 基礎結構。 在完全部署及設定好該服務後，不論用戶端是連線到內部的私人網路還是網際網路，皆可與內部部署的 Configuration Manager 站台系統角色與雲端架構發佈點進行通訊。 如需詳細資訊並了解雲端管理閘道與以網際網路為基礎之用戶端管理的比較，請參閱[管理網際網路上的用戶端](/sccm/core/clients/manage/manage-clients-internet)。

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>改進 Windows 10 版本升級原則
在此版本中，已對此原則類型做了下列改進：

- 除了向 Microsoft Intune 註冊的 Windows 10 電腦之外，您現在還可以對執行 Configuration Manager 用戶端的 Windows 10 電腦使用版本升級原則。
- 您可以在精靈中，從 Windows 10 專業版升級到與您的硬體相容的任何平台。

## <a name="manage-hardware-identifiers"></a>管理硬體識別碼
現在，您可以提供一份硬體識別碼清單，讓 Configuration Manager 在 PXE 開機及用戶端註冊時略過這些識別碼。 這麼做有助於解決下列兩個常見的問題。

1. 許多新的裝置 (如 Surface Pro 3) 不包括內建的乙太網路連接埠。 USB 至乙太網路介面卡通常用來建立作業系統部署的有線連線。 不過，基於成本和一般使用性的考量，這通常是共用介面卡。 而該介面卡的 MAC 位址是用來識別裝置，因此每個部署之間，如果沒有額外的系統管理員動作，重複使用介面卡就會產生問題。 現在，使用 Configuration Manager 最新分支 1610 版時，您可以排除這張介面卡的 MAC 位址，以在這種情況下輕鬆重複使用介面卡。
2. SMBIOS 識別碼應該是唯一的硬體識別碼，但有些專用硬體裝置會建置重複的識別碼。 雖然這種情況不像上述 USB 至乙太網路介面卡的案例那麼常見，但硬體識別碼清單亦可用來解決此問題。

如需詳細資訊，請參閱[管理重複的硬體識別碼](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers)。

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>商務用 Windows 市集與 Configuration Manager 整合的改善
此版本的變更：
- 之前，您只能從商務用 Windows 市集部署免費應用程式。 Configuration Manager 現在會另外支援部署付費線上授權應用程式 (僅適用已在 Intune 註冊的裝置)。
- 您現在可以起始商務用 Windows 市集與 Configuration Manager 之間的立即同步處理。
- 您現在可以修改從 Azure Active Directory 取得的用戶端秘密金鑰
- 您可以刪除市集的訂閱

如需詳細資訊，請參閱[使用 System Center Configuration Manager 管理從商務用 Windows 市集購買的應用程式](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)。


## <a name="policy-sync-for-intune-enrolled-devices"></a>適用於 Intune 註冊裝置的原則同步
現在，您可以透過 Configuration Manager 主控台要求進行 Intune 註冊裝置的原則同步處理，而不需從裝置本身的公司入口網站應用程式要求進行同步處理。 若要檢視同步要求狀態資訊，您可以參閱裝置檢視的 [Remote Sync State] (遠端同步處理狀態) 新資料行，以及每個裝置的 [內容] 對話方塊的探索資料區段。
如需詳細資訊，請參閱[從 Configuration Manager 主控台遠端同步處理 Intune 註冊裝置上的原則](/sccm/mdm/deploy-use/sync-intune-device)。


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>使用合規性設定來進行 Windows Defender 設定
您現在可以使用 Configuration Manager 主控台中的設定項目，在 Intune 註冊的 Windows 10 電腦上設定 Windows Defender 用戶端設定。
如需詳細資訊，請參閱[為不是使用 System Center Configuration Manager 用戶端管理的 Windows 8.1 和 Windows 10 裝置建立設定項目](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)中的 **Windows Defender** 一節。



## <a name="general-improvements-to-software-center"></a>對軟體中心的一般改進
- 使用者現在可以透過軟體中心和應用程式類別目錄來要求應用程式。
- 有助使用者了解有哪些新軟體及相關軟體的改進。

## <a name="new-columns-in-device-collection-views"></a>裝置集合檢視中的新資料行
現在，您可以在裝置集合檢視中，顯示 [IMEI] 和 [序號] (適用於 iOS 裝置) 資料行。
如需詳細資訊，請參閱[使用 IMEI 或 iOS 序號預先宣告裝置](https://docs.microsoft.com/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)。

## <a name="customizable-branding-for-software-center-dialogs"></a>可自訂軟體中心對話方塊的商標
Configuration Manager 1602 版中引進了軟體中心的自訂商標。 該商標現在已擴充到 1610 版中的所有相關對話方塊，以提供軟體中心使用者更一致的體驗。

軟體中心的自訂商標會根據下列規則套用：

1. 如果未安裝「應用程式類別目錄網站點」站台伺服器角色，則軟體中心將會顯示 [電腦代理程式] 用戶端設定之 [顯示在軟體中心的組織名稱] 中指定的組織名稱。 如需相關指示，請參閱[如何設定用戶端設定](../../clients/deploy/configure-client-settings.md)。

2. 如果未安裝「應用程式類別目錄網站點」站台伺服器角色，則「軟體中心」將會顯示「應用程式類別目錄網站點」站台伺服器角色內容中指定的組織名稱和色彩。 如需詳細資訊，請參閱[應用程式類別目錄網站點的設定選項](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#Application-Catalog-website-point)。

3. 如果已設定 Microsoft Intune 訂閱並連線到 Configuration Manager 環境，則軟體中心將會顯示 Intune 訂閱內容中指定的組織名稱、色彩及公司標誌。 如需詳細資訊，請參閱 [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription)。


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>針對必要應用程式和軟體更新部署的強制執行寬限期
在某些情況下，您可能想要提供更多時間給使用者，以在超過您設定的任何期限之後，還能安裝必要應用程式部署或軟體更新。 當電腦已關閉一段時間，而且需要安裝大量應用程式或更新部署時，通常可能會需要此設定。 例如，如果使用者剛結束休假，他們可能必須等候很長的時間，讓逾期的應用程式部署完成安裝。 為了協助解決這個問題，您現在可以藉由將 Configuration Manager 用戶端設定部署至集合，來定義施行寬限期。

若要設定寬限期，請採取下列動作：
1.      在用戶端設定的 [電腦代理程式] 頁面上，將新內容 [延後到部署期限後施行的寬限期 (小時)] 設定為 **1** 到 **120** 小時之間的值。
2.      在新的必要應用程式部署中，或在現有部署的內容中，選取 [排程] 頁面上的 [Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings] (根據使用者喜好設定，延遲強制施行此部署，最多可延後用戶端設定中所定義的寬限期) 核取方塊。 如果部署有選取此核取方塊，且其部署目標為您已部署用戶端設定的裝置，則所有部署都會使用此強制寬限期。

如果您設定施行寬限期並選取此核取方塊，一旦應用程式安裝到期，就會在使用者所設定寬限期內的第一個非營業時間進行安裝。 不過如果需要，使用者仍可隨時開啟 [軟體中心] 並安裝應用程式。 過了寬限期後，就會強制還原為逾時部署的標準行為。 [軟體更新部署精靈]、[自動部署規則精靈] 和 [內容] 頁面都已新增類似的選項。



## <a name="improved-functionality-for-required-software-dialogs"></a>所需軟體對話方塊的功能改善
當使用者收到所需軟體時，可從 [延遲並於此之後再提醒我一次:] 設定的值下拉式清單中進行選取：
- 稍後︰指定通知根據用戶端代理程式設定中所設定的通知設定進行排程。
- 固定時間︰指定通知將排程在選取的時間後再次顯示。 例如，如果使用者選取 30 分鐘，就會在 30 分鐘後再次顯示通知。

![用戶端代理程式設定中的 [電腦代理程式] 頁面](media/client-notification-settings.png)

最大延遲時間一律會以用戶端代理程式設定中每次設定部署時間表時一起設定的通知值會依據。 例如，如果將 [電腦代理程式] 頁面上的設定 [部署期限超過 24 小時，每隔下列時間通知使用者 (小時)] 設定為 10 小時，而且啟動對話方塊時還有 24 小時以上才會超過期限，則最多會有 10 小時 (但永不超過) 對使用者顯示一組延遲選項。 隨著期限將近，對話方塊會顯示愈來愈少的選項，並與部署時間表之每個元件的相關用戶端代理程式設定一致。

此外，針對高風險部署 (例如部署作業系統的工作順序)，現在會採用更入侵式的使用者通知體驗。 每次通知使用者需要重要的軟體維護時，都會在使用者的電腦上顯示類似如下的對話方塊，而不是顯示暫時性工作列通知：

![所需軟體對話方塊](media/client-toast-notification.png)


詳細資訊：
- [管理高風險部署的設定](../../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [如何設定用戶端設定](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>軟體更新儀表板
您可以使用新的軟體更新儀表板，來檢視組織裝置目前的合規性狀態，並快速分析資料查看哪些裝置有風險。 若要檢視儀表板，請瀏覽至 [監視] > [概觀] > [安全性] > [Software Updates Dashboard] (軟體更新儀表板)。

如需詳細資訊，請參閱[監視軟體更新](/sccm/sum/deploy-use/monitor-software-updates)。


## <a name="improvements-to-the-application-request-process"></a>應用程式要求程序的改進
核准安裝應用程式之後，您仍可以在 Configuration Manager 主控台中按一下 [拒絕]，選擇拒絕要求 (過去此按鈕在核准之後就無法使用)。
這個動作並不會解除安裝任何裝置上的應用程式。 不過，它會防止使用者從軟體中心安裝新的應用程式複本。

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>自動部署規則中依內容大小進行篩選
您現在可以在自動部署規則中依軟體更新的內容大小進行篩選。 例如，您可以將 [內容大小 (KB)] 篩選設定為 [< 2048]，僅下載小於 2MB 的軟體更新。 使用此篩選可防止自動下載大型軟體更新，以在網路頻寬有限時，提供簡化 Windows 下層服務的更佳支援。 如需詳細資訊，請參閱：
- [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/) (Configuration Manager 及下層作業系統上簡化的 Windows 服務)。
- [自動部署軟體更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)

#### <a name="to-configure-the-content-size-field"></a>設定內容大小欄位
若要設定 [內容大小 (KB)] 欄位，請在建立 ADR 時移至 [建立自動部署規則精靈] 中的 [軟體更新] 頁面，或移至現有 ADR 內容中的 [軟體更新] 索引標籤。

## <a name="office-365-client-management-dashboard"></a>Office 365 用戶端管理儀表板
您現在可在 Configuration Manager 主控台中使用 Office 365 用戶端管理儀表板。 若要檢視此儀表板，請移至 [軟體程式庫] > [概觀] > [Office 365 用戶端管理]。

此儀表板會顯示下列圖表：

- Office 365 用戶端數目
- Office 365 用戶端版本
- Office 365 用戶端語言
- Office 365 用戶端通道     

如需詳細資訊，請參閱[管理 Office 365 ProPlus 更新](/sccm/sum/deploy-use/manage-office-365-proplus-updates)

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>用於管理 BIOS 轉換到 UEFI 的工作順序步驟
您現在可以使用新變數 TSUEFIDrive 來自訂作業系統部署工作順序，如此一來，「重新啟動電腦」步驟就會在硬碟上準備 FAT32 磁碟分割，以便轉換成 UEFI。 下列程序提供範例，說明如何建立工作順序步驟，以準備用於將 BIO 轉換成 UEFI 的硬碟。 如需詳細資訊，請參閱[管理 BIOS 到 UEFI 轉換的工作順序步驟](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)。

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>準備 ConfigMgr 用戶端以進行擷取之工作順序步驟的改進  
「準備 ConfigMgr 用戶端」步驟現在會完全移除 Configuration Manager 用戶端，而不是只移除金鑰資訊。 當工作順序部署擷取的作業系統映像時，每次都會安裝新的 Configuration Manager 用戶端。 如需詳細資訊，請參閱[工作順序步驟](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)。



## <a name="intune-compliance-policy-charts"></a>Intune 合規性政策圖表
您現在可以在 Configuration Manager 主控台中，使用 [監視] 工作區底下的新圖表，快速檢視裝置的整體合規性及不符合規範的主要原因。 您可以按一下圖表中的區段，向下切入至該類別內的裝置清單。 如需詳細資訊，請參閱[監視合規性政策](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)。


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>針對混合式實作整合 Lookout 以保護 iOS 和 Android 裝置
Microsoft 整合 Lookout 的行動威脅防護解決方案，以透過偵測裝置上的惡意程式碼、高風險應用程式等功能，來保護 iOS 和 Android 行動裝置。 Lookout 的解決方案有助您判斷威脅等級，並可讓您進行相關設定。 您可以在 Configuration Manager 中建立合規性政策規則，依據 Lookout 的風險評估來判斷裝置的合規性。 您可以使用條件式存取原則，依據裝置合規性狀態，來允許或封鎖公司資源的存取。 若要深入了解這項整合以及它的運作方式，請參閱[根據裝置、網路和應用程式風險管理存取](/sccm/protect/deploy-use/manage-access-based-on-device-network-app-risk)。

如果使用者的 iOS 裝置不符合規範，系統會提示他們進行註冊，並要求在裝置上安裝 Lookout for Work 應用程式、加以啟用，並修補 Lookout for Work 應用程式回報的威脅之後，才能存取公司資料。 了解如何[設定和部署 Lookout for Work 應用程式](/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps)。



## <a name="new-compliance-settings-for-configuration-items"></a>設定項目的新相容性設定
我們新增了許多新設定，可供您針對各種裝置平台在設定項目中使用。 這些是先前存在於 Microsoft Intune 獨立設定中的設定，現在當您搭配使用 Intune 和 Configuration Manager 時可以使用這些設定。
如需詳細資訊，請參閱[不使用 System Center Configuration Manager 用戶端管理的裝置設定項目](/sccm/compliance/deploy-use/configuration-items-for-devices-managed-without-the-client)。

### <a name="new-settings-for-android-devices"></a>Android 裝置的新設定
#### <a name="password-settings"></a>密碼設定
- **記住密碼歷程記錄**
- **允許指紋解除鎖定**

#### <a name="security-settings"></a>安全性設定
- **儲存卡需要加密**
- **允許螢幕擷取**
- **允許提交診斷資料**

#### <a name="browser-settings"></a>瀏覽器設定
- **允許網頁瀏覽器**
- **允許自動填入**
- **允許快顯封鎖程式**
- **允許 Cookie**
- **允許動態指令碼處理**

#### <a name="app-settings"></a>應用程式設定
- **允許 Google Play 商店**

#### <a name="device-capability-settings"></a>裝置功能設定
- **允許卸除式存放裝置**
- **允許 Wi-Fi 網際網路共用功能**
- **允許使用地理位置**
- **允許 NFC**
- **允許藍芽**
- **允許語音漫遊**
- **允許數據漫遊**
- **允許 SMS/MMS 傳訊**
- **允許語音助理**
- **允許語音撥號**
- **允許複製並貼上**

### <a name="new-settings-for-ios-devices"></a>iOS 裝置的新設定
#### <a name="password-settings"></a>密碼設定
- **密碼所需的複合字元數**
- **允許簡單密碼**
- **在非使用狀態幾分鐘後需要輸入密碼**
- **記住密碼歷程記錄**

### <a name="new-settings-for-mac-os-x-devices"></a>Mac OS X 裝置的新設定
#### <a name="password-settings"></a>密碼設定
- **密碼所需的複合字元數**
- **允許簡單密碼**
- **記住密碼歷程記錄**
- **在非使用狀態幾分鐘後啟用螢幕保護**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Windows 10 Desktop 與行動裝置版裝置的新設定
#### <a name="password-settings"></a>密碼設定
- **字元集數目下限**
- **記住密碼歷程記錄**
- **裝置從閒置狀態恢復時必須輸入密碼**

#### <a name="security-settings"></a>安全性設定
- **行動裝置需要加密**
- **允許手動取消註冊**

#### <a name="device-capability-settings"></a>裝置功能設定
- **允許透過行動數據使用 VPN**
- **允許透過行動數據進行 VPN 漫遊**
- **允許重設手機**
- **允許 USB 連線**
- **允許 Cortana**
- **允許行動中心通知**

### <a name="new-settings-for-windows-10-team-devices"></a>Windows 10 團隊版裝置的新設定
#### <a name="device-settings"></a>裝置設定
- **啟用 Azure Operational Insights**
- **啟用 Miracast 無線投影**
- **選擇要顯示在歡迎畫面上的會議資訊**
- **鎖定畫面背景圖片 URL**

### <a name="new-settings-for-windows-81-devices"></a>Windows 8.1 裝置的新設定
#### <a name="applicability-settings"></a>適用性設定
- **套用所有設定至 Windows 10**

#### <a name="password-settings"></a>密碼設定
- **必要的密碼類型**
- **字元集數目下限**
- **密碼長度下限**
- **重複登入失敗多少次之後抹除該裝置**
- **在非使用狀態幾分鐘後會關閉螢幕**
- **密碼到期 (天數)**
- **記住密碼歷程記錄**
- **不得重複使用以前用過的密碼**
- **允許圖片密碼和 PIN**

#### <a name="browser-settings"></a>瀏覽器設定
- **允許自動偵測內部網路**

### <a name="new-settings-for-windows-phone-81-devices"></a>Windows Phone 8.1 裝置的新設定
#### <a name="applicability-settings"></a>適用性設定
- **套用所有設定至 Windows 10**

#### <a name="password-settings"></a>密碼設定
- **字元集數目下限**
- **允許簡單密碼**
- **記住密碼歷程記錄**

#### <a name="device-capability-settings"></a>裝置功能設定
- **允許自動連線到免費的 Wi-Fi 熱點**



<!--HONumber=Dec16_HO3-->


