---
title: "設定硬體清查 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中設定所有用戶端或集合的硬體清查。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 41bf42228e41785a05359c08e8dfedae48d50e30


---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*適用對象：System Center Configuration Manager (最新分支)*

請使用下列步驟設定您站台的 System Center Configuration Manager 硬體清查。  

 此程序可設定硬體清查的預設用戶端設定，並套用到階層中的所有用戶端。 如果您只想要將這些設定套用至部分用戶端，請建立自訂裝置用戶端設定，並將它指派給包含您要設定硬體清查之裝置的集合。 如需如何建立自訂裝置設定的詳細資訊，請參閱 [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md) (如何在 System Center Configuration Manager 中設定用戶端設定)。  

> [!NOTE]  
>  如果用戶端裝置收到來自多組用戶端設定的硬體清查設定，則當用戶端報告硬體清查時，會將每組設定的硬體清查類別合併。  

### <a name="to-configure-hardware-inventory"></a>若要設定硬體清查  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] 。  

3.  按一下 [預設用戶端設定] 。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  在 [預設設定]  對話方塊中，按一下 [硬體清查] 。  

6.  在 [裝置設定]  清單中，設定下列項目：  

    -   [在用戶端上啟用硬體清查] - 從下拉式清單中選取 **True**。  

    -   [硬體清查排程] - 指定用戶端收集硬體清查的時間間隔。 您可以使用預設值 **7 天** ，或按一下 [排程]  設定自訂的間隔。  

7.  設定您需要的任何其他用戶端設定。 如需可供設定的硬體清查用戶端設定清單，請參閱[關於 Configuration Manager 中的用戶端設定](../../../../core/clients/deploy/about-client-settings.md)主題的[硬體清查](../../../../core/clients/deploy/about-client-settings.md#BKMK_HardwareInventoryDeviceSettings)一節。  

8.  按一下 [確定]  ，關閉 [預設設定]  對話方塊。  

 在下次下載用戶端原則時，用戶端裝置會使用這些設定來進行設定。 若要起始單一用戶端的原則擷取，請參閱 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  



<!--HONumber=Nov16_HO1-->


