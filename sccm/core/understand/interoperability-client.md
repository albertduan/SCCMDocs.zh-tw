---
title: "搭配最新分支使用 Configuration Manager 延伸互通性用戶端 | Microsoft Docs"
description: "了解如何搭配使用 Configuration Manager 長期維護分支的用戶端與最新分支站台。"
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9772224be78eee2777137225a59b53b1fd77a627
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2017
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>使用適用於延伸互通性的 Configuration Manager 用戶端軟體來搭配未來的「最新分支」站台版本使用

適用於：System Center Configuration Manager (最新分支)、(長期維護分支)  

在某些案例中，您的公司原則可能不允許您定期更新某些電腦上的 Configuration Manager 用戶端。 例如，您可能需要符合變更管理原則，或裝置為關鍵任務所需。

從 Configuration Manager 更新 1610 開始，雖然您應該儘可能繼續為大部分的用戶端使用自動用戶端升級，但是您也可以安裝供長期使用的用戶端 (稱為延伸互通性用戶端 (EIC)) 以符合這些需求。

EIC 與執行 1610 或更新版本的 Configuration Manager 網站相容。 EIC 只應該用於無法頻繁更新的特定電腦，例如資訊站或收銀機裝置。 為所有其他電腦使用最新的 Configuration Manager 用戶端。

## <a name="how-this-scenario-works"></a>此案例如何運作

一般來說，當您為最新分支安裝新的主控台內更新時，用戶端即會自動更新其用戶端軟體，以便使用這些新功能。

在這類案例中，您可以使用最新分支，並接收新功能和更新。 大部分的用戶端會透過最新分支來執行用戶端軟體，並使用您安裝的每個版本來更新該用戶端軟體。 不過，您可以在不想接收用戶端軟體更新的關鍵系統子集上，安裝延伸互通性用戶端。 除非您明確地對這些用戶端部署新版用戶端軟體，否則它們不會安裝新的用戶端軟體。

>[!IMPORTANT]
>「最新分支」站台必須執行 1610 版或更新版本。

## <a name="how-to-use-the-eic"></a>如何使用 EIC

1. Configuration Manager 1606更新安裝媒體的 \SMSSETUP\Client 資料夾取得 EIC (用戶端版本 5.00.8412)。 確定您已複製整個資料夾的內容。
2. 在那些裝置上手動安裝 EIC。 [深入了解如何手動安裝用戶端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)。
3. 從用戶端升級排除該集合。

>[!TIP]
>若要在大量授權服務中心 (VLSC) 中尋找 System Center Configuration Manager 1606 版，請前往 [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) 的 [下載和金鑰] 索引標籤，並搜尋 "system center config"，然後選取 [System Center Config Mgr (最新分支與 LTSB)]。

## <a name="the-extended-interoperability-client-software"></a>延伸互通性用戶端軟體

目前的 EIC 將會繼續隨著 Configuration Manager 最新分支的更新版本而受到支援，至少到 2018 年 11 月 18 日之前都是如此。 屆時，請檢查此頁面以取得有關新 EIC 的詳細資料，或是否延長現有 EIC 支援的相關資訊。

>[!TIP]
>EIC 至少在發行日期兩年內都會受到支援 (請參閱 [System Center Configuration Manager 最新分支版本支援](/sccm/core/servers/manage/current-branch-versions-supported))。 例如，對目前 EIC 的支援是 1610 發行兩年後，也就是 2018 年 11 月 18 日。

在用戶端的支援到期之前，請針對您使用最新分支管理的裝置，規劃其上的延伸互通性用戶端更新。 若要執行此作業，請從 Microsoft 下載新版本的用戶端，然後將該更新的用戶端軟體部署到使用目前延伸互通性用戶端的裝置。

## <a name="limitations-of-the-extended-interoperability-client"></a>延伸互通性用戶端的限制

- 您無法藉由使用主控台內更新，取得延伸互通性用戶端軟體的更新。 當更新的用戶端發行時，即會提供部署更新之用戶端軟體的其他詳細資料。
- EIC 只支援軟體更新、清查，以及套件與程式。

## <a name="next-steps"></a>後續步驟

使用[如何監視用戶端](/sccm/core/clients/manage/monitor-clients)中的資訊確保用戶端已正在安裝在您要的裝置上。
