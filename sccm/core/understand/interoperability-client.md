---
title: "搭配使用最新分支與延伸互通性用戶端 | Microsoft Docs"
description: "了解如何搭配使用 Configuration Manager 長期維護分支的用戶端與最新分支站台。"
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: 0
author: robstackmsft
ms.author: robstack
Robots: NOINDEX,NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 30d0177dc7fcc7f39d00c48067130d587435bf2d
ms.lasthandoff: 12/16/2016

---
# <a name="use-the-client-software-from-the-version-1606-baseline-media-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>使用來自 1606 版基準媒體的用戶端軟體，以保障與未來版本的最新分支站台的延伸互通性

適用於：System Center Configuration Manager (最新分支)、(長期維護分支)  

您可以藉由下列方式，取得並使用適用於 Windows 電腦 Configuration Manager 用戶端軟體 (client.msi)，來管理屬於最新分支站台的裝置：透過 System Center 2016 隨附的 1606 版基準 DVD 媒體取得，或透過 System Center Configuration Manager (最新分支和長期維護分支 1606) 版本取得。 此用戶端稱為延伸互通性用戶端。

## <a name="how-this-scenario-works"></a>這類案例的運作方式如下：
一般來說，當您為最新分支安裝新的主控台內更新時，用戶端即會自動更新其用戶端軟體，以便使用這些新功能。

在這類案例中，您可以使用最新分支，並接收新功能和更新。 大部分的用戶端會透過最新分支來執行用戶端軟體，並使用您安裝的每個版本來更新該用戶端軟體。 不過，您可以在不想接收用戶端軟體更新的關鍵系統子集上，安裝延伸互通性用戶端。 除非您明確地對這些用戶端部署新版用戶端軟體，否則它們不會安裝新的用戶端軟體。

當您安裝新版的 Configuration Manager 時，最新分支 1610 版即會提供如何避免最新分支用戶端自動更新的詳細資訊。

最新分支站台必須執行 1606 版或更新版本。

## <a name="the-extended-interoperability-client-software"></a>延伸互通性用戶端軟體
當您搭配最新分支站台使用來自 System Center 2016 或 System Center Configuration Manager (最新分支和長期維護分支 1606) 版本的延伸互通性用戶端時，支援的用戶端版本為自 2016 年 10 月 12 日上市後的兩年期間。

在用戶端的支援到期之前，請針對您使用最新分支管理的裝置，規劃其上的延伸互通性用戶端更新。 若要執行此作業，請從 Microsoft 下載新版本的用戶端，然後將該更新的用戶端軟體部署到使用目前延伸互通性用戶端的裝置。

**延伸互通性用戶端的限制：**
-     您無法藉由使用主控台內更新，取得延伸互通性用戶端軟體的更新。 當更新的用戶端發行時，即會提供部署更新之用戶端軟體的其他詳細資料。

## <a name="identify-the-client-version-you-use"></a>識別您所使用的用戶端版本
以下是適用於最新分支和 LTSB 的主要用戶端版本：

|用戶端版本|分支和版本 |  
|----------------|---------------------|
|5.00.8325.xxxx |    - 最新分支 1511|
|5.00.8355.xxxx    |- 最新分支 1602|
|5.00.8412.1307    |- 最新分支 1606 </br> - 最新分支 1606 與 1606 Hotfix 彙總套件 (KB3186654)</br>- 來自 1606 版基準媒體的延伸互通性用戶端|  

在用戶端上，您可以透過 Configuration Manager 控制台小程式的 [一般] 索引標籤來檢視用戶端版本。

在小程式的 [元件] 索引標籤上，某些元件會顯示不同的值。 例如，針對用戶端版本 8412.1307，某些元件可能會列為 5.00.8412.**1000** 或 5.00.8412.**1006**。  對某些元件來說，末四碼數不同是正常現象，並不表示元件更新至目前用戶端版本失敗。

