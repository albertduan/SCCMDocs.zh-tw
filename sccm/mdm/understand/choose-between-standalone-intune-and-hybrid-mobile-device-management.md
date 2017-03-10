---
title: "選擇 Intune 獨立部署或混合式 MDM | Microsoft Docs"
description: "選擇要部署使用 Intune 和 Configuration Manager 的混合式行動裝置管理，還是要執行 Intune 獨立部署。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 84e3896dd05a8c157f4e94625b0eca60aacc11d3
ms.openlocfilehash: 8f2625aadfd0aed92d9922c7e3c0d3d166a78cdd
ms.lasthandoff: 02/25/2017

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>在 Microsoft Intune 獨立部署與使用 System Center Configuration Manager 的混合式行動裝置管理之間進行選擇

*適用於：System Center Configuration Manager (最新分支)*

使用 Microsoft Intune 進行行動裝置管理 (MDM) 時，最常詢問的其中一個問題就是：「我應該整合 Intune 和 Configuration Manager (混合式 MDM)，還是在僅限雲端的設定中執行 Intune 獨立部署？」 為了回答這個問題，您應仔細比較這兩個選項，並考慮 Intune 獨立部署在 2017 年初推出的更新。

## <a name="what-is-intune-standalone"></a>什麼是 Intune 獨立部署？

Intune 獨立部署是僅限雲端的 MDM 解決方案，不需要任何內部部署資源，而是透過可從世界各地存取的 Web 主控台進行管理。 北美洲、歐洲和亞洲都有託管的 Intune Datacenter。 因為 Intune 是雲端服務，所以您可以在相對較短的時間範圍內將 Intune 管理部署到您的裝置。 如果您的組織移到雲端，您也可以選擇 Intune 獨立部署。

## <a name="what-is-hybrid-mdm-with-configuration-manager"></a>什麼是搭配 Configuration Manager 的混合式 MDM？

混合式 MDM 解決方案使用 Intune 作為將原則、設定檔和應用程式傳遞至裝置的傳遞通道，但使用 Configuration Manager 內部部署基礎結構來儲存和管理內容以及管理裝置。 如果您已投入相當大的心力在 Configuration Manager，並想要進行擴充以管理行動裝置，您可以選擇混合式 MDM。 混合式實作提供「單一整合」(Single Pane of Glass) 控制，這表示您可以使用相同的內部部署基礎結構和系統管理主控台透過 Intune 來管理行動裝置，以及透過傳統 Configuration Manager 用戶端來管理電腦和伺服器。

## <a name="whats-coming-to-intune-standalone-in-early-2017"></a>Intune 獨立部署在 2017 年初的未來動態

如果您想在獨立部署與混合式部署之間進行選擇，您應考慮 Intune 獨立部署在 2017 年初推出的功能。 今日，混合式 MDM 具有數項進階功能，這些功能是某些客戶在過去一直選擇使用混合式 MDM 而不是 Intune 獨立部署來管理其裝置的原因：

-   以程式設計方式存取 (API) - SDK 和 PowerShell 管理選項。

-   自訂報告 - 建立自訂報告。

-   角色型存取控制 - 根據指派的角色來限制管理功能的存取。

-   規模 - 部署和管理超過 100,000 部行動裝置。

-   單一整合 - 使用同一個主控台來管理傳統電腦用戶端及 Intune 管理的裝置。

如果您想立即開始規劃 Intune 部署，並有幾個月的時間可進行試驗、驗收測試和部署，您現在可以考慮選擇 Intune 獨立部署，並知道未來雲端服務更新將包含更多功能。 在 2017 年上半年，Intune 獨立部署將會收到更新，這些更新提供搭配 Configuration Manager 之混合式部署的許多進階功能。 Intune 獨立部署即將移至 Microsoft Azure 雲端平台，該平台提供增強的延展性，並可讓您透過 Azure 入口網站進行角色型存取、進行自訂報告，以及透過 Azure Graph API 以程式設計方式存取。

您可以在混合式部署與 Intune 獨立部署之間進行切換，但需要來自 Microsoft 支援人員的協助與操作。 變更管理授權單位之後，您也必須取消註冊再重新註冊所有裝置。  Microsoft 正在努力改善未來服務更新中切換設定的體驗。

