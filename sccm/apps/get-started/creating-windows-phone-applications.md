---
title: "建立 Windows Phone 應用程式 | Microsoft Docs"
description: "查看在您建立和部署 Windows Phone 裝置的應用程式時，必須考慮的事項。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 866113ff-efd0-40d2-ac3a-2edd49732a24
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 557888d1f1f899e3198c430bbe5ccdd44178f824
ms.openlocfilehash: 5cd1ba42afd13e98565d24d1ec8a3ee209e8532c


---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立 Windows Phone 應用程式

*適用於：System Center Configuration Manager (最新分支)*

建立和部署 Windows Phone 裝置的應用程式時，除了建立應用程式的其他 System Center Configuration Manager 需求和程序之外，還必須考慮下列項目。  

## <a name="general-considerations"></a>一般考量  
 Configuration Manager 支援部署下列應用程式檔案類型：  

|裝置類型|支援的檔案類型|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap、.appx、.appxbundle|  

 支援下列部署動作：  

|裝置類型|支援的動作|  
|-----------------|-----------------------|  
|Windows Phone 8 和 Windows Phone 8.1|可用、必要、解除安裝|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>使用取代方式部署最新 Windows Phone 公司入口網站應用程式的步驟  
 下表提供用於建立及部署最新 Windows Phone 8 公司入口網站應用程式的步驟、詳細資料和更多資訊。  

|步驟|詳細資訊|  
|----------|----------------------|  
|**步驟 1：** 取得最新的公司入口網站應用程式。|下載 [Windows Phone 8 公司入口網站應用程式](http://go.microsoft.com/fwlink/?LinkId=268440)。|  
|**步驟 2：** 使用您的 Symantec 憑證簽署公司入口網站應用程式。|如需如何簽署公司入口網站應用程式的相關資訊，請參閱[以 System Center Configuration Manager 和 Microsoft Intune 來設定 Windows Phone 及 Windows 10 行動裝置版混合式裝置管理](../../mdm/deploy-use/enroll-hybrid-windows.md)。|  
|**步驟 3：**使用最新版公司入口網站應用程式建立新的應用程式，並指定取代關聯性。|如需詳細資訊，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)和[修改和取代應用程式](../../apps/deploy-use/revise-and-supersede-applications.md)。|  
|**步驟 4：**將應用程式新增至 [Microsoft Intune 訂閱精靈]。|如需詳細資訊，請參閱[以 System Center Configuration Manager 和 Microsoft Intune 來設定 Windows Phone 及 Windows 10 行動裝置版混合式裝置管理](../../mdm/deploy-use/enroll-hybrid-windows.md)。|  
|**步驟 5：**刪除在您將公司入口網站應用程式新增到 [Microsoft Intune 訂閱精靈] 時自動建立的部署。|Microsoft Intune 訂閱已建立此應用程式的自動部署，因為此部署不會支援取代。|  
|**步驟 6：**建立應用程式的新部署。 在 [部署軟體精靈] 的 [部署設定] 頁面上，勾選 [自動升級任何會取代此應用程式的版本]。|使用您以取代關聯性建立的應用程式，建立含取代的新部署。|  
|**步驟 7 (選用)：**依預設，取代應用程式會在 7 天後安裝於裝置上。 若要更快將公司入口網站應用程式部署到先前註冊的裝置，可以將 [排程部署的重新評估] 設定變更為較低的值。<br /><br /> 如果將這個值設定成比預設值低的值，可能會對您的網路及用戶端電腦效能造成負面影響。|沒有其他資訊。|  



<!--HONumber=Dec16_HO3-->


