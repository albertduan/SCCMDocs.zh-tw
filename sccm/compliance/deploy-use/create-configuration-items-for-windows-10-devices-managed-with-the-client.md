---
title: "如何為使用 System Center Configuration Manager 用戶端管理的 Windows 10 裝置建立設定項目 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager Windows 10 設定項目管理 Configuration Manager 用戶端所管理之 Windows 10 電腦的設定。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d5248e7262f758c2de2a1deaf42282d4e77e3e0c


---
# <a name="create-configuration-items-for-windows-10-devices-managed-with-the-system-center-configuration-manager-client"></a>為使用 System Center Configuration Manager 用戶端管理的 Windows 10 裝置建立設定項目

*適用對象：System Center Configuration Manager (最新分支)*

使用 System Center Configuration Manager **Windows 10** 設定項目管理 Configuration Manager 用戶端所管理之 Windows 10 電腦的設定。  

> [!IMPORTANT]  
>  在此版本中，如果您將 [密碼] 設定作為 **Windows 10** 類型設定項目的一部分 (針對 Configuration Manager 用戶端管理的裝置)，則當 Windows 10 裝置上的設定不存在或尚未設定時，就會誤判為相容。  
>   
>  因應措施是當您建立這些裝置的設定時，請務必在 [建立設定項目精靈] 的 [設定] 頁面上，選取 [補救不相容的設定]  。 此外，若您部署的組態基準包括含密碼設定的 Windows 10 組態項目，請選取 [部署組態基準] 對話方塊中的 [支援時補救不相容的規則]  。 使用這個因應措施時，如果找到不相容的設定，就會加以監視並進行補救。 補救之後，即會將該設定正確回報為 [相容]  ，但若發生問題，則會回報 [錯誤] 。  

## <a name="create-a-windows-10-configuration-item"></a>建立 Windows 10 設定項目  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [設定項目]。  

3.  在 [常用]  索引標籤上，按一下 [建立]  群組中的 [建立設定項目] 。  

4.  在 [建立設定項目精靈]  的 [一般] 頁面上，指定設定項目的名稱和選擇性描述。  

5.  在 [指定您要建立的組態項目類型] 下，選取 [Windows 10] 。  

6.  如果您要建立並指派類別，以協助您在 Configuration Manager 主控台中搜尋和篩選設定項目，請按一下 [類別]。  

7.  在 [支援的平台] 頁面上，選取將評估設定項目的特定 Windows 10 平台。  

8.  在 [裝置設定] 頁面上，選取您想要設定的設定群組。 請參閱本主題的 [Windows 10 設定項目的設定參考](/sccm/compliance/deploy-use/create-configuration-items-for-windows-10-devices-managed-with-the-client#windows-10-configuration-item-settings-reference)以取得詳細資訊，然後按一下 [下一步]。  

    > [!TIP]  
    >  如果未列出您想要的設定，請選取 [設定不在預設設定群組中的其他設定] 核取方塊。  

9. 在每一個設定頁面上，進行您需要的設定，並指定這些設定與裝置不相容時是否要進行補救 (如果支援的話)。  

10. 針對每個設定群組，您也可以設定下列嚴重性，以在找到不相容的設定項目時加以回報 (在 Configuration Manager 報告中)：  

    -   **無**- 不符合這項相容性規則的裝置不會回報失敗嚴重性。  

    -   **資訊** - 不符合這項相容性規則的裝置會回報 [資訊] 失敗嚴重性。  

    -   **警告** - 不符合這項相容性規則的裝置會回報 [警告] 失敗嚴重性。  

    -   **重大** - 不符合這項相容性規則的裝置會回報 [重大] 失敗嚴重性。  

    -   **重大事件** - 不符合這項相容性規則的裝置會回報 [重大] 失敗嚴重性。 這個嚴重性等級也會在應用程式事件記錄檔中記錄為 Windows 事件。  

11. 在 [平台適用性] 頁面上，檢閱是否有與您先前選取的支援平台不相容的任何設定。 您可以返回並移除這些設定，也可以繼續。  

    > [!TIP]  
    >  系統不會針對不支援的設定進行相容性評估。  

12. 完成精靈。  

 您可以在 [資產與相容性]  工作區的 [設定項目]  節點中檢視新的設定項目。  

##  <a name="windows-10-configuration-item-settings-reference"></a>Windows 10 組態項目的設定參考  

### <a name="password"></a>密碼  

|設定|詳細資料|  
|-------------|-------------|  
|**裝置上的必要密碼設定**|支援的裝置上需要的密碼。|  
|**最小密碼長度 (字元數)**|密碼字元長度下限。|  
|**密碼到期天數**|密碼必須變更之前的天數。|  
|**記住的密碼數目**|防止重複使用先前的密碼。|  
|**抹除裝置前允許的失敗登入次數**|如果登入失敗達到這個次數即會抹除裝置。|  
|**鎖定行動裝置前的閒置時間**|指定裝置閒置幾分鐘之後就會自動鎖定。|  
|**密碼複雜性**|選擇 PIN 是否可指定如 '1234'，或是否必須提供強式密碼。|  

###  <a name="device"></a>裝置  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**Bluetooth**|裝置上允許使用 Bluetooth 功能。|  

### <a name="cloud"></a>雲端  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**設定同步處理**|允許裝置之間的設定同步處理。|  
|**認證同步處理**|允許裝置之間的認證同步處理。|  
|**透過計量付費連線的設定同步處理**|當計量付費網際網路連線時，允許同步處理設定。|  

### <a name="roaming"></a>漫遊  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**數據漫遊**|存取資料時允許網路之間的漫遊。|  

### <a name="encryption"></a>加密  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**裝置上的檔案加密**|裝置上的檔案需要加密。|  

### <a name="system-security"></a>系統安全性  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**使用者帳戶控制**|設定裝置上 Windows 使用者帳戶控制的運作方式。<br />例如，您可以停用它或設定通知等級。|  
|**網路防火牆**|啟用或停用 Windows 防火牆。|  
|**SmartScreen**|啟用或停用 Windows SmartScreen。|  
|**防毒保護**|必須安裝和設定防毒軟體。|  
|**防毒特徵已是最新版本**|裝置上防毒軟體的簽章檔案必須是最新狀態。|  

### <a name="windows-information-protection-formerly-enterprise-data-protection"></a>Windows 資訊保護 (原企業資料保護)

企業中員工擁有的裝置日漸增加，資料不慎從企業難以控管的應用程式和服務 (如電子郵件、社交媒體和公用雲端) 外洩的風險也更高。 比方說，員工透過個人電子郵件帳戶傳送最新的工程圖片、複製並將產品資訊貼進推文，或將進行中的銷售報表儲存到公用雲端存放裝置等情況。

Windows 資訊保護 (WIP) 有助防止這類資料外洩的可能，同時不干擾員工的體驗。 WIP 也可協助保護企業應用程式和資料，避免企業擁有的裝置與員工辦公用的個人裝置發生意外的資料外洩情況，而且不需要變更環境或其他應用程式。

 Configuration Manager WIP 設定項目可管理受 WIP 保護的應用程式清單、企業網路位置、保護等級和加密設定。

如需如何設定 Windows 資訊保護與 Configuration Manager 的相關訊，請參閱[使用 Windows 資訊保護 (WIP) 保護您的企業資料](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)。



<!--HONumber=Nov16_HO1-->


