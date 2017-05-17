---
title: "Windows Defender 進階威脅防護 | Microsoft Docs"
description: "了解如何管理及監視 Windows Defender 進階威脅防護，這是幫助企業回應進階攻擊的新服務。"
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 8f4ec982a54cf3cefef310268a54850e70e2e63a
ms.openlocfilehash: 237dc9cbccb973720a633490f096aed4bc16d183
ms.contentlocale: zh-tw
ms.lasthandoff: 05/17/2017

---
# <a name="windows-defender-advanced-threat-protection"></a>Windows Defender 進階威脅防護

適用於：System Center Configuration Manager (最新分支)

從 Configuration Manager 1606 版 (最新分支) 開始，Endpoint Protection 可以協助管理和監視 Windows Defender 進階威脅防護 (ATP)。 Windows Defender ATP 是新的服務，可協助企業偵測、調查和回應其網路的進階攻擊。  深入了解 [Windows Defender ATP](http://aka.ms/technet-wdatp)。 Configuration Manager 原則可協助您上架及監視受管理的 Windows 10 1607 版 (版本 14328)。

Windows Defender ATP 是 [Windows 資訊安全中心](https://securitycenter.windows.com)的一項服務。 藉由加入及部署用戶端上架設定檔，Configuration Manager 可以監視部署狀態與 Windows Defender ATP 代理程式健全狀況。 只有執行 Configuration Manager 用戶端的電腦才支援 Windows Defender ATP。 不支援內部部署行動裝置管理及 Intune 混合式 MDM 管理的電腦。

 **先決條件**  

-   Windows Defender 進階威脅防護線上服務訂閱  

-   執行 Windows 10 1607 和更新版本的用戶端  

## <a name="how-to-create-an-onboarding-configuration-file"></a>如何建立上架設定檔  

 1.  登入 [Windows Defender ATP 線上服務](https://securitycenter.windows.com/)   

 2.  按一下 [端點管理] 功能表項目。  

 3.  選取 [System Center Configuration Manager (最新分支) 版本 1606]，然後按一下 [下載套件]。  

 4.  下載壓縮的封存檔案 (.zip)，並將內容解壓縮。

> [!IMPORTANT]
> Windows Defender ATP 設定檔包含應該受到保護的機密資訊。

## <a name="onboard-devices-for-windows-defender-atp"></a>將適用於 Windows Defender ATP 的裝置上架  

1.  在 Configuration Manager 主控台中，瀏覽至 [資產與相容性] > [概觀] > [Endpoint Protection] > [Windows Defender ATP 原則]，然後按一下 [建立 Windows Defender ATP 原則]。 [Windows Defender ATP 原則精靈] 隨即開啟。  

2.  輸入 Windows Defender ATP 原則的 [名稱] 和 [描述]，然後選取 [上架]。 按一下    

3.  **瀏覽**至您組織之 Windows Defender ATP 雲端服務租用戶所提供的設定檔。 按一下 [下一步] 。  

4.  指定為了分析而從受管理裝置收集和分享的範例檔案。  

    -   **無**   

    -   **所有檔案類型**  

     按一下    

5.  檢閱摘要並完成精靈。  

6.  您現在可以按一下 [部署]，將 Windows Defender ATP 原則部署至受管理的用戶端電腦。  

## <a name="monitor-windows-defender-atp"></a>監視 Windows Defender ATP  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視] > [概觀] > [安全性]，然後按一下 [Windows Defender ATP]。  

2.  檢閱 [Windows Defender 進階威脅防護] 儀表板。  

    -   **Windows Defender 代理程式部署狀態** – 已上架的使用中 Windows Defender ATP 原則之符合資格的受管理用戶端電腦數目和百分比  

    -   **Windows Defender ATP 代理程式健康情況** - 回報其 Windows Defender ATP 代理程式狀態的電腦用戶端百分比  

        -   **狀況良好** - 運作正常  

        -   **非使用中** - 在這段期間不會將任何資料傳送至服務  

        -   **代理程式狀態** - Windows 中未執行此代理程式的系統服務  

        -   **未上架** - 已套用原則，但代理程式尚未回報原則上架  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>如何建立及部署下架設定檔  

1.  登入 [Windows Defender ATP 線上服務](https://securitycenter.windows.com/)   

2.  按一下 [端點管理] 功能表項目。  

3.  選取 [System Center Configuration Manager (最新分支) 版本 1606]，然後按一下 [端點下架]。  

4.  下載壓縮的封存檔案 (.zip)，並將內容解壓縮。 將檔案下架的有效期限為 30 天。

5.  在 Configuration Manager 主控台中，瀏覽至 [資產與相容性] > [概觀] > [Endpoint Protection] > [Windows Defender ATP 原則]，然後按一下 [建立 Windows Defender ATP 原則]。 [Windows Defender ATP 原則精靈] 隨即開啟。  

6.  輸入 Windows Defender ATP 原則的 [名稱] 和 [描述]，然後選取 [下架]。 按一下 [下一步] 。  

7.  **瀏覽**至您組織之 Windows Defender ATP 雲端服務租用戶所提供的設定檔。 按一下 [下一步] 。  

8.  檢閱摘要並完成精靈。  

9.  您現在可以按一下 [部署]，將 Windows Defender ATP 原則部署至受管理的用戶端電腦。  

> [!IMPORTANT]
> Windows Defender ATP 設定檔包含應該受到保護的機密資訊。

[Windows Defender 進階威脅防護](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[針對 Windows Defender 進階威脅防護上線問題進行疑難排解](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)

