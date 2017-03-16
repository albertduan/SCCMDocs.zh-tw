---
title: "建立 Android 應用程式 | Microsoft Docs"
description: "查看在您建立和部署 Android 裝置的應用程式時，必須考慮的事項。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 3d90b2cb1e255b9e8827a991779024ccecde9646
ms.lasthandoff: 03/06/2017

---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立 Android 應用程式

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 應用程式有一或多個部署類型，其中包含將軟體部署至裝置所需的安裝檔案與資訊。 部署類型也包含指定部署軟體之時間和方法的規則。  

 您可以使用下列兩種方式建立應用程式：  

-   透過讀取應用程式安裝檔案的方式自動建立應用程式和部署類型。  

-   手動建立應用程式並在之後新增部署類型。  

-   從檔案匯入應用程式。  

如需建立 Configuration Manager 應用程式與部署類型的必要步驟，請參閱[啟動建立應用程式精靈](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard)。 此外，當您建立和部署 Android 裝置的應用程式時，請記住下列考量。  

## <a name="general-considerations"></a>一般考量

Configuration Manager 支援部署下列適用於 Android 的應用程式類型：

|裝置類型|支援的檔案|
|-|-|
|Android|.apk|

支援下列部署動作：

|裝置類型|支援的動作|
|-|-|
|Android|**可用**、**必要**。 使用者必須同意安裝和解除安裝。

