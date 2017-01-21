---
title: "System Center Configuration Manager Technical Preview 1610 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1610 版中可用的功能。"
ms.custom: na
ms.date: 10/21/2016
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
caps.latest.revision: 2
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c9fe6961a63495d08a3e58e3ddf46c5d316e2613
ms.openlocfilehash: 865b5078282bf240aa6a2aef5cb2662f2471fb71

---
# <a name="capabilities-in-technical-preview-1610-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1610 中的功能

適用於︰System Center Configuration Manager (Technical Preview)



本文介紹 System Center Configuration Manager Technical Preview 1610 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。      安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    


**以下是您可以使用此版本試用的新功能。**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>在自動部署規則中依內容大小進行篩選
您現在可以在自動部署規則中依軟體更新的內容大小進行篩選。 例如，您可以將 [內容大小 (KB)] 篩選設定為 [< 2048]，僅下載小於 2MB 的軟體更新。 使用此篩選可防止自動下載大型軟體更新，以在網路頻寬有限時，提供簡化 Windows 下層服務的更佳支援。 如需詳細資訊，請參閱 [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)(Configuration Manager 及下層作業系統上的簡化 Windows 服務)。

#### <a name="to-configure-the-content-size-field"></a>設定內容大小欄位
若要設定 [內容大小 (KB)] 欄位，請在建立 ADR 時移至 [建立自動部署規則精靈] 中的 [軟體更新] 頁面，或移至現有 ADR 內容中的 [軟體更新] 索引標籤。

![內容大小欄位](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>所需軟體對話方塊的功能改善
當使用者收到所需軟體時，可從 [延遲並於此之後再提醒我一次:] 設定的值下拉式清單中進行選取：
- 稍後︰指定通知根據用戶端代理程式設定中所設定的通知設定進行排程。
- 固定時間︰指定通知將排程在選取的時間後再次顯示。 例如，如果使用者選取 30 分鐘，就會在 30 分鐘後再次顯示通知。

![用戶端代理程式設定中的 [電腦代理程式] 頁面](media/computeragentsettings.png)

最大延遲時間一律會以用戶端代理程式設定中每次設定部署時間表時一起設定的通知值會依據。 例如，如果將 [電腦代理程式] 頁面上的設定 [部署期限超過 24 小時，每隔下列時間通知使用者 (小時)] 設定為 10 小時，而且啟動對話方塊時還有 24 小時以上才會超過期限，則最多會有 10 小時 (但永不超過) 對使用者顯示一組延遲選項。 隨著期限將近，對話方塊會顯示愈來愈少的選項，並與部署時間表之每個元件的相關用戶端代理程式設定一致。

此外，針對高風險部署 (例如部署作業系統的工作順序)，現在會採用更入侵式的使用者通知體驗。 每次通知使用者需要重要的軟體維護時，都會在使用者的電腦上顯示類似如下的對話方塊，而不是顯示暫時性工作列通知：

![所需軟體對話方塊](media/requiredsoftwaredialog.png)


詳細資訊：
- [管理高風險部署的設定](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [如何設定用戶端設定](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>拒絕先前核准的應用程式要求

身為系統管理員，您現在可以拒絕先前核准的應用程式要求。 拒絕後，稍後若要安裝此應用程式，使用者必須重新提交要求。 拒絕並不會解除安裝應用程式；而是會強制重新核准來自該使用者對該應用程式的任何新要求。 之前，只能針對尚未核准的應用程式要求執行應用程式要求拒絕動作。

#### <a name="try-it-out"></a>試試看
若要拒絕應用程式核准要求：

1.  在 Configuration Manager 主控台中，[建立和部署需要核准的應用程式](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/create-applications)。
2.  在用戶端電腦上，開啟 [軟體中心] 並提交應用程式要求。
3.  在 Configuration Manager 主控台中，核准應用程式要求。
4.  拒絕核准的應用程式要求︰ 在 Configuration Manager 主控台中，巡覽 [軟體程式庫] > [概觀] > [應用程式管理] > [核准要求]，然後選取您要拒絕的應用程式要求。  在功能區中，按一下 [拒絕]。

## <a name="exclude-clients-from-automatic-upgrade"></a>排除自動升級用戶端
Technical Preview 1610 引進新的設定，可讓您用來防止用戶端集合自動安裝更新版用戶端版本。  這適用於自動升級及其他方法，例如以軟體更新為基礎的升級、登入指令碼和群組原則。 這可用於需要在升級用戶端時更小心的電腦集合。 排除集合中的用戶端會略過安裝更新版用戶端軟體的要求。

### <a name="configure-exclusion-from-automatic-upgrade"></a>設定自動升級的排除範圍
若要設定自動升級的排除範圍：
1.  在 Configuration Manager 主控台中，開啟 [系統管理] > [站台設定] > [站台] 下的 [階層設定]，然後選取 [用戶端升級] 索引標籤。
2.  選取 [Exclude specified clients from upgrade] (排除升級指定的用戶端) 核取方塊，然後針對 [Exclusion collection] (排除集合)，選取您要排除的集合。 您只能選取單一集合進行排除。
3.  按一下 [確定] 以關閉並儲存設定。 然後，在用戶端更新原則之後，排除集合中的用戶端就不會再自動安裝用戶端軟體的更新。

  ![自動升級的排除範圍設定](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> 雖然使用者介面指出用戶端不會透過任何方法升級，但您可以使用兩種方法來覆寫這些設定。 用戶端推入安裝和手動用戶端安裝可用來覆寫此設定。 如需詳細資訊，請參閱下一節。


### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>如何升級排除集合中的用戶端
只要集合設定為要排除，該集合的成員只能透過兩種方法之一覆寫此排除範圍，以升級其用戶端軟體：
 - **用戶端推入安裝** - 您可以使用用戶端推入安裝來升級排除集合中的用戶端。 因為這視為系統管理員的意圖，所以允許這樣做。此方法可讓您升級用戶端，而不需要從排除範圍中移除整個集合。       
 - **手動用戶端安裝** - 您可以使用下列命令列參數搭配 ccmsetup，手動升級排除集合中的用戶端：***/ignoreskipupgrade***

  如果您嘗試手動升級屬於排除集合成員的用戶端，但未使用此參數，則用戶端不會安裝新的用戶端軟體。 如需詳細資訊，請參閱[如何手動安裝 Configuration Manager 用戶端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually)。

如需用戶端安裝方法的詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。


## <a name="see-also"></a>另請參閱
[System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)



<!--HONumber=Nov16_HO1-->


