---
title: "設定 Endpoint Protection | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 的用戶端電腦上管理安全性和惡意程式碼。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 3678fd1e2ba70ad1cc03a3e0ca294901fae96255


---
# <a name="configuring-endpoint-protection-in-system-center-configuration-manager"></a>設定 System Center Configuration Manager 中的 Endpoint Protection

*適用對象：System Center Configuration Manager (最新分支)*

您要先使用本主題進行設定，才能使用 Endpoint Protection 管理 Configuration Manager 用戶端電腦的安全性和惡意程式碼。  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>如何設定 Configuration Manager 中的 Endpoint Protection  
 Configuration Manager 中的 Endpoint Protection 在產品內外皆有相依性。  

### <a name="configure-endpoint-protection-in-configuration-manager"></a>設定 Configuration Manager 中的 Endpoint Protection  
設定 Endpoint Protection 有五個步驟

|步驟|詳細資料|
|---|----|
|步驟 1|[建立 Endpoint Protection 點站台系統角色](endpoint-protection-site-role.md)：安裝 Endpoint Protection 點站台系統角色 |
|步驟 2|[設定 Endpoint Protection 警示](endpoint-configure-alerts.md)：設定 Endpoint Protection 警示以在階層發生特定安全性事件時通知系統管理員|
|步驟 3 | [設定 Endpoint Protection 用戶端的定義更新來源](endpoint-definition-updates.md)：選擇可用的方法讓用戶端電腦上的反惡意程式碼定義保持在最新狀態|
|步驟 4|[設定預設反惡意程式碼原則以及建立自訂反惡意程式碼原則](endpoint-antimalware-policies.md)：在 Endpoint Protection 用戶端安裝後，即會套用預設的反惡意程式碼原則，並在用戶端部署後的 60 分鐘內套用自訂原則。|
|步驟 5|[設定 Endpoint Protection 的自訂用戶端設定](endpoint-protection-configure-client.md)：設定 Endpoint Protection 的自訂用戶端設定以部署至電腦集合|

> [!IMPORTANT]  
>  如果您管理 Windows 10 電腦的 Endpoint Protection，則您必須設定 Configuration Manager 以更新及發佈 Windows Defender 的惡意程式碼定義。 Windows Defender 包含在 Windows 10，但是仍然必須安裝 SCEPInstall，且仍然需要 Endpoint Protection 的自訂用戶端設定 (步驟 5)。  



<!--HONumber=Dec16_HO3-->


