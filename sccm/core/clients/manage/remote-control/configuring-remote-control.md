---
title: "設定遠端控制 | Microsoft Docs"
description: "在 System Center Configuration Manager 中設定遠端控制。"
ms.custom: na
ms.date: 12/12/2016
ms.prod: configuration-manager
ms.reviewer: dudeso
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
ms.sourcegitcommit: 809c7938968b4a6efce6ef37fe7b7baf2c9dd3e7
ms.openlocfilehash: 6741c6aa11a8a7c868bff36916afe4d066b9924d


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中設定遠端控制

*適用於：System Center Configuration Manager (最新分支)*

 這個程序會說明設定遠端控制的預設用戶端設定。 這些設定會套用至階層中的所有電腦。 如果您只想讓某些電腦套用這些設定，請將自訂裝置用戶端設定指派給包含那些電腦的集合。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端設定](../../../../core/clients/deploy/configure-client-settings.md)。 

若要使用遠端協助或遠端桌面，它必須安裝及設定在執行 Configuration Manager 主控台的電腦上。 如需如何安裝及設定遠端協助或遠端桌面的詳細資訊，請參閱 Windows 文件。  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>啟用遠端控制及設定用戶端設定  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [用戶端設定] > [預設用戶端設定]。  

4.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

5.  在 [預設] 對話方塊中，選擇 [遠端工具] 。  

6.  設定遠端控制、遠端協助和遠端桌面用戶端設定。 如需您可設定的遠端工具用戶端設定清單，請參閱[遠端工具](../../../../core/clients/deploy/about-client-settings.md#remote-tools)。  

    在 [電腦代理程式]  用戶端設定中設定 [顯示於軟體中心的組織名稱]  的值，就可以變更出現在 [ConfigMgr 遠端控制]  對話方塊中的公司名稱。  

 用戶端電腦會在下一次下載用戶端原則時，使用這些設定進行設定。 若要起始單一用戶端的原則擷取，請參閱 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  

#### <a name="enable-keyboard-translation"></a>啟用鍵盤轉譯

根據預設，Configuration Manager 會將按鍵位置從檢視者的位置傳輸到共用者的位置。 如果檢視者和共用者的鍵盤設定不同，這可能會發生問題。 例如，具有英文鍵盤的檢視者會輸入"A"，但共用者的法文鍵盤會提供 "Q"。 您現在有選項可以設定遠端控制，讓字元本身從檢視者的鍵盤傳輸到共用者，以確保檢視者預期輸入的內容會抵達共用者端。

若要開啟鍵盤轉譯，請在 [Configuration Manager 遠端控制] 中，選擇 [動作]，然後選擇 [啟用鍵盤轉譯] 以傳輸按鍵位置。

> [!NOTE]
>
> ~!#@$%, 等特殊按鍵不會正確轉譯。


<!--HONumber=Dec16_HO3-->


