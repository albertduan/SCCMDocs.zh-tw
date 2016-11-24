---
title: "設定遠端控制 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中設定遠端控制。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aea35afe970e20bc2b22f9ae3f413a3c735caae1


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中設定遠端控制

*適用對象：System Center Configuration Manager (最新分支)*

您必須先執行下列設定步驟，才能使用 System Center Configuration Manager 的遠端控制。  

## <a name="how-to-enable-remote-control-and-configure-client-settings"></a>如何啟用遠端控制及設定用戶端設定  
 這個程序會說明設定遠端控制的預設用戶端設定，並套用至階層中的所有電腦。 如果您只想某些電腦套用這些設定，請建立自訂裝置用戶端設定，並將它指派給包含要在遠端控制工作階段中使用的電腦集合。 如需如何建立自訂裝置設定的詳細資訊，請參閱 [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md) (如何在 System Center Configuration Manager 中設定用戶端設定)。  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>啟用遠端控制及設定用戶端設定  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] 。  

3.  按一下 [預設用戶端設定] 。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  在 [預設]   對話方塊中，按一下 [遠端工具] 。  

6.  設定您需要的遠端控制、遠端協助和遠端桌面用戶端設定。 如需您可設定的遠端控制用戶端設定清單，請參閱[關於 Configuration Manager 中的用戶端設定](../../../../core/clients/deploy/about-client-settings.md#BKMK_RemoteToolsDeviceSettings)主題的[遠端工具](../../../../core/clients/deploy/about-client-settings.md)一節。  

    > [!NOTE]  
    >  在 [電腦代理程式]  用戶端設定中設定 [顯示於軟體中心的組織名稱]  的值，就可以變更出現在 [ConfigMgr 遠端控制]  對話方塊中的公司名稱。  

    > [!IMPORTANT]  
    >  若要使用遠端協助或遠端桌面，它必須安裝及設定在執行 Configuration Manager 主控台的電腦上。 如需如何安裝及設定遠端協助或遠端桌面的詳細資訊，請參閱 Windows 文件。  

7.  按一下 [確定]  ，關閉 [預設設定]  對話方塊。  

 用戶端電腦會在下一次下載用戶端原則時，使用這些設定進行設定。 若要起始單一用戶端的原則擷取，請參閱 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  



<!--HONumber=Nov16_HO1-->


