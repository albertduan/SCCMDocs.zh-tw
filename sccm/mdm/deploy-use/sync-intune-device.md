---
title: "遠端同步處理向 Intune 註冊之裝置上的原則 | Microsoft Docs"
description: "了解如何從 Configuration Manager 主控台同步處理 Intune 註冊裝置上的原則"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: 18
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dcdccc34fa55ce3d3e4459d209c7aeb74752214b
ms.openlocfilehash: c6496e9694314f1910ca944f6c083a9f3fd2bf79

---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台遠端同步處理 Intune 註冊裝置上的原則

*適用於：System Center Configuration Manager (最新分支)*


您可以從 Configuration Manager 主控台要求向 Intune 註冊之裝置的原則同步處理，而不需要求從裝置本身的公司入口網站應用程式進行同步處理。 

若要這樣做：

1.  在 [資產與合規性] > [概觀] > [裝置] 下，選取裝置。
2.  在 [遠端裝置動作] 功能表中，按一下 [Send Sync Request] (傳送同步要求)。


在五到十分鐘後，會將原則中的任何變更同步到裝置。 您可以在裝置檢視的新資料行 (稱為 [Remote Sync State] (遠端同步處理狀態)) 以及每個裝置之 [內容] 對話方塊的探索資料區段中，檢視同步要求狀態資訊。



<!--HONumber=Dec16_HO3-->


