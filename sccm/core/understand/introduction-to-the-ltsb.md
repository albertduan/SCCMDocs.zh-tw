---
title: "長期維護分支簡介 | System Center Configuration Manager"
description: "了解 System Center Configuration Manager 的長期維護分支。"
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2a45cfb3e00d8078fbf45bdc8a2668b7dd0a62c6
ms.openlocfilehash: 926d1b1299e7851bd1d9168237859c5cd7a65abe


---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager 的長期維護分支簡介

適用於：System Center Configuration Manager (長期維護分支)

您可以使用本主題來了解 Configuration Manager 長期維護分支 (LTSB)，並了解此分支的相關文件。


LTSB 是以最新分支 1606 版為基礎的不同 Configuration Manager 分支。 相較於最新分支，LTSB 的[功能有限](#features-that-are-not-available-in-the-ltsb-of-configuration-manager)。 它是專為[已接受軟體保證 (SA) 或對等的訂閱權限失效](/sccm/core/understand/learn-more-editions#software-assurance-and-the-ltsb)的客戶精心設計。

**授權概觀：**   
如果客戶具有 System Center Configuration Manager 授權的作用中軟體保證 (SA) 或自 2016 年 10 月 1 日起的對等訂閱權限，即有權使用 2016 年 10 月發行的 System Center Configuration Manager 1606 版。 如果客戶具有自 2016 年 10 月 1 日起的 System Center Configuration Manager 權限，則在安裝時會發現最新分支和長期維護分支 (LTSB) 這兩個授權選項。

**授權詳細資料：**  
[您可參閱此連結，了解透過 Microsoft 大量授權方案購買之產品的完整條款及條件](http://go.microsoft.com/fwlink/?LinkId=800052)。

如果客戶擁有 System Center Configuration Manager 的永久權限 ，或可接受 SA 或訂閱於 10 月 1 日之後失效，則可在失效當下安裝 System Center Configuration Manager LTSB 版。
- 如需 System Center Configuration Manager 軟體保證和授權需求的資訊，請參閱 [System Center Configuration Manager licensing and branches](learn-more-editions.md) (System Center Configuration Manager 授權和分支)。
-   如需不同分支之間的差異詳細資訊，請參閱 [Which branch of Configuration Manager should I use](which-branch-should-i-use.md) (應該使用的 Configuration Manager 分支)。

若要安裝新的站台或從支援的 System Center 2012 Configuration Manager 站台升級至 LTSB，您可以使用 1606 版基準媒體。 這個基準媒體是 Microsoft System Center 2016 或 System Center Configuration Manager (最新分支和長期維護分支 1606) 版本 DVD 的一部分。 可安裝 LTSB 的基準媒體也可用來安裝 Configuration Manager 的 1606 版最新分支。 若要了解基準媒體，請參閱[基準和更新版本](/sccm/core/servers/manage/updates#baseline-and-update-versions)。

如需如何安裝 LTSB 站台的資訊，請參閱 [Install and Upgrade for the Long-Term Servicing Branch](install-the-ltsb.md) (安裝和升級長期維護分支)。 如需如何取得 System Center 2016 的資訊，請參閱 [System Center 2016 文件](https:\technet.microsoft.com\system-center-docs\System-Center-2016)。

> [!IMPORTANT]
> 同一個階層中的所有站台必須執行相同的分支。 同一個階層中的不同站台不支援混合使用 LTSB 和最新分支架構。
>
> 同樣地，當您使用復原功能時，必須將站台或站台資料庫還原為其原始的分支。 您無法將最新分支站台資料庫復原為 LTSB 安裝，反之亦然。


## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Configuration Manager 的 LTSB 未提供的功能
相較於最新分支，LTSB 具有下列支援限制：

- 不會接收新功能的更新。
- 不支援新增 Microsoft Intune 訂閱，因此無法使用下列項目：
  - 混合式 MDM 設定的 Intune
  - 內部部署 MDM
-   不支援使用 Windows 10 服務儀表板、服務計畫，亦不支援 Windows 10 最新分支 (CB) 和最新商務分支 (CBB)
- 不支援 Windows 10 LTSB 和 Windows Server 的未來版本
-   不支援 Asset Intelligence
-   不支援雲端發佈點
-   不支援將 Exchange Online 的支援作為 Exchange Connector
-   不支援任何發行前版本功能


雖然 LTSB 不包含這些功能的支援，但 Configuration Manager 主控台仍會顯示部分功能，只是無法選取或使用。

此外，如果新增的作業系統是設為受最新分支的支援，該系統就不受 LTSB 支援。

## <a name="documentation-for-the-ltsb"></a>LTSB 的文章
由於 LTSB 是以最新分支 1606 版為依據，因此您使用的 LTSB 文件是[適用於最新分支的線上文件](https://docs.microsoft.com/sccm/)，其中包含 LTSB 的特定注意事項和限制，如下列主題所識別：  

-   [長期維護分支簡介](introduction-to-the-ltsb.md) - (本主題)

-   [應該使用的 Configuration Manager 分支](which-branch-should-i-use.md) – 提供 System Center Configuration Manager 不同分支的資訊，以讓您安裝最符合需求的分支。

-   [安裝長期維護分支](install-the-ltsb.md) - 如何安裝新的 LTSB 站台，或將 System Center 2012 Configuration Manager 站台升級至 LTSB。

-   [將長期維護分支升級至最新分支](convert-to-current-branch.md) – 如何將 LTSB 安裝轉換為最新分支安裝。

-   [System Center Configuration Manager 授權和分支](learn-more-editions.md) – 提供 System Center Configuration Manager 軟體保證和相關授權需求的資訊。
-   [支援的長期維護分支設定](supported-configurations-for-ltsb.md) - 您可搭配 LTSB 使用的作業系統及相依產品 (例如 SQL Server) 之需求與版本。


為了協助您辨別特定文件適用於哪些分支，請使用下列指南：  
-   如果主題有「適用於：最新分支」的標題，即表示適用於最新分支和長期維護分支 (但部分主題可能只適用於較新版本的最新分支)。

-   為了識別出不適用於 LTSB 的部分主題，在 1606 版最新分支以後所導入的功能和變更會以「自 1610 版起」的類似文字來表明。 由於這些項目是在 1606 版最新分支以後所導入的，因此不適用於 LTSB。

### <a name="similarities-between-the-current-branch-and-the-ltsb"></a>最新分支和 LTSB 之間的相似處
LTSB 是以最新分支 1606 版為基礎 (除了 Intune 整合及雲端相關功能等例外狀況)，因此這兩個分支的規劃部署、設定及管理等大部分工作都相同。

例如，LTSB 支援與最新分支相同數目的站台、站台類型、用戶端，以及一般的基礎結構。 因此，您可以參閱最新分支中的站台和階層規劃與設計主題，以作為指南。 同樣地，針對兩個分支所支援的功能 (例如軟體更新或作業系統部署)，您可以參閱最新分支文件中的相關章節，其中含有無法存取在 1606 版最新分支以後所導入之變更的注意事項。


## <a name="how-to-identify-your-branch-and-version"></a>如何識別您的分支和版本
當您檢視 Configuration Manager 站台的版本資訊時，也可確認分支。

若要檢查站台的版本，請移至主控台左上角的 [關於 System Center Configuration Manager]，其中 [站台版本] 會顯示為 **5.0.8412.1000**。

若要確認站台的分支 (為 LTSB 或最新分支)，請移至主控台的 [系統管理] > [站台設定] > [站台]，並開啟 [階層設定]。  如果其中具有可以轉換為最新分支的作用中選項，即表示站台執行 LTSB 版本。 當站台執行最新分支時，此選項即會呈現灰色。

如需 Configuration Manager 不同版本的資訊，請參閱 [Configuration Manager 的更新](/sccm/core/servers/manage/updates)主題中的**基準和更新版本**。

## <a name="exceptions-for-using-the-ltsb"></a>使用 LTSB 的例外狀況
### <a name="updates-and-servicing-of-the-ltsb"></a>LTSB 的更新及服務
LTSB 僅提供重大安全性更新的主控台內更新。

不過，主控台會顯示後續最新分支版本的定期更新相關資訊。 這些更新不會提供給 LTSB，因此無法下載及安裝。

為了支援重大安全性修正的主控台內更新，LTSB 站台需要使用[服務連接點](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。 您可以在離線或線上模式中，設定此站台系統角色 (進行方式與最新分支一樣)。 LTSB 會收集並送出與最新分支相同的遙測和使用方式資料。

如最新分支所述，LTSB 支援使用 Hotfix 安裝程式和更新註冊工具。

如需更新和服務的一般資訊，請參閱 [Configuration Manager 的更新](/sccm/core/servers/manage/updates)。

### <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>站台擴充和 CD.Latest 資料夾的變更
在執行 LTSB 並安裝新的管理中心網站以擴充獨立主要站台時，您必須使用來自 1606 版基準媒體的安裝程式和來源檔案   (若是最新分支，則要執行並使用來自 CD.Latest 資料夾的安裝程式和來源檔案)。

雖然您無法從 CD.Latest 資料夾執行安裝程式以進行站台擴充，但可以繼續使用 CD.Latest 資料夾進行站台復原，並用其來安裝新的子主要站台 (若您的第一個 LTSB 站台為管理中心網站的話)。

如需站台擴充的詳細資訊，請參閱[使用安裝精靈安裝站台](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)[擴充獨立主要站台](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site)。
如需 CD.Latest 資料夾的詳細資訊，請參閱 [CD.Latest 資料夾](/sccm/core/servers/manage/the-cd.latest-folder)。



<!--HONumber=Nov16_HO1-->


