---
title: "建立 iOS 應用程式 | System Center Configuration Manager"
description: "查看在您建立和部署 iOS 裝置的應用程式時，必須考慮的事項。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5420109-6538-4430-9ca6-db352ee84c2e
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4c3845635846cae183e81d0ddb9c8222dabd8929


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立 iOS 應用程式

*適用於：System Center Configuration Manager (最新分支)*

建立和部署 iOS 裝置的應用程式時，除了建立應用程式的其他 System Center Configuration Manager 需求和程序之外，還必須考慮下列項目。  

## <a name="general-considerations"></a>一般考量  
 Configuration Manager 支援部署下列應用程式類型：  

|裝置類型|支援的檔案|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> 在 System Center Configuration Manager 中，匯入 iOS 應用程式時，不需要指定內容清單 (.plist) 檔案。|  

 支援下列部署動作：  

|裝置類型|支援的動作|  
|-----------------|-----------------------|  
|iOS|可用、必要 (但使用者必須同意安裝)、解除安裝。|  

> [!IMPORTANT]  
>  使用者目前無法從適用於 iOS 的 Microsoft Intune 公司入口網站應用程式安裝公司應用程式。 這是因為 iOS App Store 中發行之應用程式的限制所致 (請參閱 App Store 審核指南的第 2 節)。 使用者可以在其裝置上瀏覽至 Intune Web 入口網站 (portal.manage.microsoft.com) 來安裝公司應用程式 (包括受管理的 App Store 應用程式及特定業務應用程式封裝)。 如需 Intune 公司入口網站應用程式所啟用的行動管理功能詳細資訊，請參閱 [Microsoft Intune 的已註冊裝置管理功能](https://technet.microsoft.com/library/dn600287.aspx)。  



<!--HONumber=Nov16_HO1-->


