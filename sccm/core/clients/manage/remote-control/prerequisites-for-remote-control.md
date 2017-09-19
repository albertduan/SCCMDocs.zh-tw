---
title: "遠端控制必要條件 | Microsoft Docs"
description: "取得 System Center Configuration Manager 中遠端控制的必要條件。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: a99a18bcb5c981a56e5b38eb631cfabbad8c44d7
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/14/2017
---
# <a name="prerequisites-for-remote-control-in-system-center-configuration-manager"></a>System Center Configuration Manager 中遠端控制的必要條件

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的遠端控制具有外部相依性和產品內的相依性。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性  

|相依性|詳細資訊|  
|----------------|----------------------|  
|電腦視訊卡驅動程式|請確定用戶端電腦上已安裝最新視訊驅動程式，確保最佳遠端控制效能。|  

 執行 Windows Embedded、Windows Embedded for Point of Service (POS) 和 Windows Fundamentals for Legacy PCs 的裝置不支援遠端控制檢視器，但支援遠端控制用戶端。  

 Configuration Manager 遠端控制不能用來遠端管理執行 Systems Management Server 2003 或 Configuration Manager 2007 的用戶端電腦。  

> [!NOTE]  
>  任何 Windows 服務都不需要是遠端控制的外部相依性。  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>遠端控制檢視器所支援的作業系統  
支援 Configuration Manager 主控台的所有作業系統上都支援遠端控制檢視器。 如需詳細資訊，請參閱 [System Center Configuration Manager 主控台的支援設定](../../../../core/plan-design/configs/supported-operating-systems-consoles.md)。   

## <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  

|相依性|詳細資訊|  
|----------------|----------------------|  
|必須啟用用戶端的遠端控制|根據預設，安裝 Configuration Manager 時，不會啟用遠端控制。 如需如何啟用和設定遠端控制的相關資訊，請參閱[在 System Center Configuration Manager 中設定遠端控制](../../../../core/clients/manage/remote-control/configuring-remote-control.md)。|  
|Reporting Services 點|必須先安裝 Reporting Services 點站台系統角色，才能執行遠端控制的報告。 如需詳細資訊，請參閱 [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md) (System Center Configuration Manager 中的報告)。|  
|管理遠端控制的安全性權限|存取集合資源並從 Configuration Manager 主控抬起始遠端控制工作階段：[讀取]、[讀取資源] 及 [集合] 物件的 [遠端控制] 權限。<br /><br /> [遠端工具操作員] 安全性角色包括在 Configuration Manager 中管理遠端控制所需的上述權限。<br /><br /> 如需詳細資訊，請參閱[為 System Center Configuration Manager 設定以角色為基礎的系統管理](../../../../core/servers/deploy/configure/configure-role-based-administration.md)。<br /><br /> 此外，您必須將這些使用者加入 [遠端工具] 用戶端設定中的 [遠端控制和遠端桌面的獲准檢視器] 清單，以將使用遠端控制的權限授與獲准檢視器。
