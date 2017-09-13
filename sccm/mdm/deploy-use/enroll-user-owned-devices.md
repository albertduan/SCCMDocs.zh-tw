---
title: "使用 Configuration Manager 註冊使用者擁有的裝置以進行混合式部署 | Microsoft Docs"
description: "了解使用 Configuration Manager 註冊使用者擁有的裝置以進行混合式部署的不同方法。"
ms.custom: na
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
caps.latest.revision: "13"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 56bd6bfd900a8ecbb149392de62889970ddedb60
ms.sourcegitcommit: 40f2a4e3cc546e6bfd10f195a8e87af2b0780928
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2017
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>使用 Configuration Manager 註冊使用者擁有的裝置以進行混合式部署

*適用於：System Center Configuration Manager (最新分支)*

使用者擁有的裝置可以經由註冊接受管理，這個程序通常稱為「攜帶您自己的裝置」或簡稱「BYOD」。 使用者可以藉由安裝公司入口網站應用程式或在裝置 (iOS、macOS 及 Android) 上登入，或將公司或學校帳戶新增到裝置並加入網域 (Windows)，來完成這個程序。 這個程序會向 Intune 註冊裝置，提供使用者受 Intune 管理的資源存取權，並讓 Intune 管理某些裝置設定，像是要求 PIN。

若要讓裝置接受管理，您必須使用系統管理員的身份[設定行動裝置管理](setup-hybrid-mdm.md)及[啟用註冊](enable-platform-enrollment.md)。 註冊一經啟用，使用者即可註冊他們自己的裝置。 如需與使用者共用的考量及步驟，請參閱[如何指導使用者使用 Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate)。

購買裝置的公司或學校可以利用能讓您[管理公司所屬裝置](enroll-company-owned-devices.md)的計劃。
