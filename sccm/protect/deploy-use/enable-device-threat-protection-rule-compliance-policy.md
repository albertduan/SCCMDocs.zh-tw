---
title: "啟用合規性原則中的裝置保護規則 | System Center Configuration Manager"
description: "啟用裝置合規性原則中的行動裝置威脅保護規則。"
ms.custom: na
ms.date: 12/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 020f43e8-738e-4a82-91be-27b10cda9665
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 498b8c02dbf1391e6331c8b9ad7b6ef0fdef22d0
ms.openlocfilehash: 319289c9b211935ba10cb6d3da386ffed3c0153e
ms.lasthandoff: 02/23/2017


---
# <a name="create-a-lookout-device-threat-protection-rule"></a>建立 Lookout 裝置威脅保護規則

*適用對象：System Center Configuration Manager (最新分支)*

## <a name="before-you-begin"></a>開始之前

具有 Lookout 行動裝置威脅保護的 Intune 可讓您偵測行動裝置威脅，並在裝置上進行風險評估。 您可以在 Configuration Manager 中建立合規性政策規則以納入風險評估來判斷裝置是否符合規範。 接著，您可以使用條件式存取原則，根據裝置合規性來允許或封鎖存取 Exchange、SharePoint 和其他服務。

若要讓 Lookout 裝置威脅偵測影響裝置的合規性原則：

-   必須啟用合規性政策的 [裝置威脅保護] 規則。

-   [Intune 系統管理員主控台] 中的 [Lookout 狀態] 必須顯示為 [作用中]。 如需如何啟用 Lookout 整合的詳細資訊和指示，請參閱[在 Intune 中啟用 Lookout MTP 連線](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune)主題。

在合規性政策中建立裝置威脅保護規則之前，建議您執行下列動作︰

1.  [設定訂閱進行 Lookout 裝置威脅保護](https://docs.microsoft.com/sccm/protect/deploy-use/set-up-your-subscription-with-lookout)

2.  [在 Intune 管理主控台中啟用 Lookout MTP 連線](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune)

3.  [設定 Lookout for Work 應用程式](https://docs.microsoft.com/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps)

>[!NOTE]
>只有在設定完成之後，才會強制執行合規性規則。

## <a name="to-create-a-device-threat-protection-rule"></a>建立裝置威脅保護規則

在 Lookout 裝置威脅保護的設定過程中，您已在 [Lookout 主控台](https://aad.lookout.com)中建立原則，將各種威脅分類為高、中與低等級。 在 Intune 合規性政策中，您將使用威脅等級來設定允許的最高威脅等級。

建立 Lookout 裝置威脅保護規則：

1.  在 Configuration Manager 主控台中，按一下 [資產與合規性] 工作區。

2.  在 [資產與合規性] 中，展開 [合規性原則]。

3.  以滑鼠右鍵按一下 [合規性政策]，然後選取 [建立合規性政策]。

4.  輸入合規性政策名稱，然後選取 [未使用 Configuration Manager 用戶端管理之裝置的合規性規則]。

5.  選取根據合規性政策所佈建的 OS 平台 (Android 4.1 和更新版本，和 (或) iOS 8 和更新版本)。

6.  在 [規則] 頁面上，按一下 [新增] 以指定符合規範裝置的規則。

7.  在 [新增規則] 頁面上，以下列資訊定義新的規則：
    1.  條件：裝置威脅保護的最高風險等級。
    
    2.  值：值必須為下列其中一項：
        1.  **無 (受保護)**：這是最安全的選項。 這表示裝置不能受到任何威脅。 如果發現任何威脅等級，則會將裝置評估為不符合規範。
        2.  **低**：如果僅存在低等級的威脅，會將裝置評估為符合規範。 任何較高等級的威脅會使裝置變成不符合規範的狀態。
        3.  **中**：如果在裝置上發現的威脅為低等級或中等級，會將裝置評估為符合規範。 如果偵測到高等級的威脅，會將裝置判斷為不符合規範。
        4.  **高**：這是最不安全的選項。 基本上這會允許所有的威脅等級，而且可能只有在您只針對報告用途而使用此解決方案時才有用。

>[!IMPORTANT]
>如果您針對 Office 365 和其他服務建立條件式存取原則，則上述的合規性評估會納入考量，並且會封鎖不符合規範的裝置存取公司資源，直到威脅解決為止。
