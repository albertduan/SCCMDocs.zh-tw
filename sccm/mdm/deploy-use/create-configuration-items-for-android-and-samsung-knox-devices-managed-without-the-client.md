---
title: "建立使用 Intune 進行管理之 Android 與 Samsung KNOX Standard 裝置的設定項目 | Microsoft Docs"
description: "使用 System Center Configuration Manager Android 和 Samsung KNOX Standard 設定項目，管理裝置的設定。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 67ea4d2a7c9753aa406a84157930564213b6cc0a
ms.lasthandoff: 03/06/2017


---
# <a name="create-configuration-items-for-android-and-samsung-knox-standard-devices-managed-with-intune"></a>建立使用 Intune 進行管理之 Android 與 Samsung KNOX Standard 裝置的設定項目

*適用於︰System Center Configuration Manager (最新分支)*

使用 System Center Configuration Manager [Android 和 Samsung KNOX] 設定項目，管理 Microsoft Intune 中所註冊或 Configuration Manager 透過內部部署方式管理之 Android 和 Samsung KNOX Standard 裝置的設定。  

## <a name="create-an-android-and-samsung-knox-standard-configuration-item"></a>建立 Android 和 Samsung KNOX Standard 設定項目  

1.  在 Configuration Manager 主控台中，按一下 [資產與合規性] > [合規性設定] > [設定項目]。  

3.  在 [常用] 索引標籤上，按一下 [建立] 群組中的 [建立設定項目]。  

4.  在 [建立設定項目精靈] 的 [一般]頁面上，指定設定項目的名稱和選擇性描述。  

5.  在 [指定您要建立的組態項目類型] 下，選取 [Android 和 Samsung KNOX]。  

6.  如果您要建立並指派類別，以協助您在 Configuration Manager 主控台中搜尋和篩選設定項目，請按一下 [類別]。  

7.  在 [支援的平台] 頁面上，選取將評估設定項目的特定 Android 或 Samsung KNOX Standard 平台。  

8.  在 [裝置設定] 頁面上，選取您想要設定的設定群組。 請參閱本主題的 [Android 和 Samsung KNOX Standard 設定項目設定參考](#android-and-samsung-knox-standard-configuration-item-settings-reference)以取得詳細資料，然後按一下 [下一步]。  

    > [!TIP]  
    >  如果未列出您想要的設定，請選取 [設定不在預設設定群組中的其他設定] 核取方塊。  

9. 在每一個設定頁面上，進行您需要的設定，並指定這些設定與不符合裝置規範時是否要進行補救 (如果支援的話)。  

10. 針對每個設定群組，您也可以設定下列嚴重性，以在找到不符合規範的設定項目時加以回報 (在 Configuration Manager 報告中)：  

    -   **無**- 不符合此合規性規則的裝置不會回報失敗嚴重性。  

    -   **資訊** - 不符合此合規性規則的裝置會回報 [資訊] 失敗嚴重性。  

    -   **警告** - 不符合此合規性規則的裝置會回報 [警告] 失敗嚴重性。  

    -   **重大** - 不符合此合規性規則的裝置會回報 [重大] 失敗嚴重性。  

    -   **重大事件** - 不符合此合規性規則的裝置會回報 [重大] 失敗嚴重性。   

11. 在 [平台適用性] 頁面上，檢閱是否有與您先前選取的支援平台不相容的任何設定。 您可以返回並移除這些設定，也可以繼續。  

    > [!TIP]  
    >  系統不會針對不支援的設定進行合規性評估。  

12. 完成精靈。  

 您可以在 [資產與合規性] 工作區的 [設定項目] 節點中檢視新的設定項目。  

##  <a name="android-and-samsung-knox-standard-configuration-item-settings-reference"></a>Android 和 Samsung KNOX Standard 設定項目設定參考  

### <a name="password"></a>密碼  
 這些設定適用於 Android 和 Samsung KNOX Standard 裝置。  

|設定|詳細資料|  
|-------------|-------------|  
|**裝置需要密碼設定**|支援的裝置上需要的密碼。|  
|**最小密碼長度 (字元數)**|密碼長度下限。|  
|**密碼到期天數**|密碼必須變更之前的天數。|  
|**記住的密碼數目**|防止重複使用先前用過的密碼。|  
|**抹除裝置前允許的失敗登入次數**|如果登入嘗試失敗是這個數目即抹除裝置。|  
|**鎖定裝置前的閒置時間**|選取裝置未使用多長時間後即會將其鎖定。|
|**密碼品質**|選取所需的密碼複雜性等級以及是否可以使用生物特徵辨識裝置。|  
|**允許 Smart Lock 和其他信任代理程式**|可讓您控制相容 Android 裝置上的 Smart Lock 功能。 此電話功能 (有時也稱為信任代理程式) 可讓您在裝置位於受信任的位置 (例如連線到特定的藍牙裝置或靠近 NFC 標記) 時，停用或略過裝置鎖定畫面密碼。 您可以使用此設定來防止使用者設定 Smart Lock。|
|用於解除鎖定的指紋 (KNOX 5.0+)|讓使用者使用指紋來解鎖相容的裝置。|

###  <a name="device"></a>裝置  
 這些設定僅適用於 Samsung KNOX Standard 裝置。  

|設定名稱|詳細資料|  
|------------------|-------------|
|**語音撥號**|啟用或停用裝置上的語音撥號功能。|
|**語音助理**|允許使用裝置上的語音助理軟體。|
|**螢幕擷取**|讓使用者將畫面擷取成影像。|
|**診斷資料提交**|允許裝置將診斷資訊送出至 Google。|
|**地理位置**|允許裝置使用位置資訊。|
|**複製和貼上**|允許使用裝置上的複製和貼上功能。|  
|**重設為原廠設定**|允許使用者在裝置上重設為原廠設定。|  
|**應用程式之間的剪貼簿共用**|使用剪貼簿在應用程式之間複製並貼上。|
|**Bluetooth**|允許使用裝置的藍牙功能。|

### <a name="store"></a>市集
|設定|詳細資料|  
|-------------|-------------|  
|**應用程式市集**|允許存取裝置上的 Google Play Store 應用程式。|

### <a name="browser"></a>瀏覽器
|設定|詳細資料|  
|-------------|-------------|
|**允許網頁瀏覽器**|指定是否能夠使用裝置的預設網頁瀏覽器。|
|**自動填寫**|允許使用網頁瀏覽器的自動填寫功能。|
|**動態指令碼處理**|允許裝置網頁瀏覽器使用動態指令碼處理。|
|**快顯封鎖程式**|允許在網頁瀏覽器中使用快顯封鎖程式。|
|**Cookie**|允許裝置網頁瀏覽器使用 Cookie。|

### <a name="cloud"></a>雲端  
 這些設定僅適用於 Samsung KNOX Standard 裝置。  

|設定|詳細資料|  
|-------------|-------------|  
|**Google 備份**|允許使用 Google 備份。|  
|**Google 帳戶自動同步處理**|允許自動同步處理 Google 帳戶設定。|  



### <a name="security"></a>安全性  

|設定|詳細資料|  
|-------------|-------------|  
|**SMS 和多媒體簡訊**|允許在裝置上使用 SMS 和多媒體簡訊。|
|**抽取式存放裝置**|允許裝置使用抽取式存放裝置 (如 SD 記憶卡)。|
|**相機**|允許使用裝置相機。<br /><br /> 適用於 Android 和 Samsung KNOX Standard 裝置。|  
|**近距離無線通訊 (NFC)**|若裝置支援，則允許使用近距離無線通訊的操作。|
|**YouTube**|允許在裝置上使用 YouTube 應用程式。<br /><br /> 僅適用於 Samsung KNOX Standard 裝置。|  
|**關閉電源**|允許關閉裝置電源。<br /><br /> 僅適用於 Samsung KNOX Standard 裝置。|

### <a name="roaming"></a>漫遊
|設定|詳細資料|  
|-------------|-------------|
|**語音漫遊**|當裝置使用行動電話通訊網路時允許語音漫遊。|
|**數據漫遊**|當裝置使用行動電話通訊網路時允許數據漫遊。|

### <a name="encryption"></a>加密  
 這些設定適用於 Android 和 Samsung KNOX Standard 裝置。  

|設定|詳細資料|  
|-------------|-------------|  
|**儲存卡加密**|指定是否必須加密裝置儲存卡。|
|**裝置上的檔案加密**|行動裝置上的檔案需要加密。|  

### <a name="wireless-communications"></a>無線通訊
|設定|詳細資料|  
|-------------|-------------|
|**無線網路連線**|允許使用裝置的 Wi-Fi 功能。|
|**Wi-Fi 網際網路共用功能**|允許在裝置上使用 Wi-Fi 網際網路共用功能。|


### <a name="kiosk-mode-samsung-knox-standard-only"></a>Kiosk 模式 (僅限 Samsung KNOX Standard)  
 Kiosk 模式允許您限制裝置只能執行某些特定功能。 例如，您可以允許裝置只執行您指定的一個受管理應用程式，也可以停用裝置上的音量按鈕。 這些設定可能用於裝置的展示模型，或是專用來只執行一個功能的裝置 (例如銷售點裝置)。  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-standard-device"></a>設定適用於 Samsung KNOX Standard 裝置的 Kiosk 模式  

在 [建立設定項目精靈] 的 [為 Samsung KNOX 裝置設定 Kiosk 模式設定] 頁面上，指定下列資訊：  

- **選取應用程式** - 按一下 [瀏覽] 選取 Configuration Manager Android 應用程式 (副檔名為 **.apk**)，以在裝置處於 Kiosk 模式時允許執行此類型的應用程式。 不允許在裝置上執行其他應用程式。
- **音量按鈕** - 啟用或停用裝置上的音量按鈕。
- **螢幕睡眠及喚醒按鈕** - 啟用或停用裝置上的螢幕睡眠喚醒按鈕。|  

###  <a name="compliant-and-noncompliant-apps-android"></a>符合規範和不符合規範的應用程式 (Android)  
 讓您指定公司中符合規範或不符合規範的 Android 應用程式清單。 您可以接著使用報告來顯示安裝了不符合規範之應用程式的裝置，以及關聯的使用者。  

 您無法在同一個組態項目中，同時指定符合規範和不符合規範的應用程式。  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>指定符合規範或不符合規範的應用程式清單  

1.  在 [符合規範和不符合規範的應用程式 (Android)]  頁面上，指定下列資訊：  

    |設定|詳細資訊|  
    |-------------|----------------------|  
    |**不符合規範的應用程式清單**|如果您想要指定使用者安裝時將回報為不符合規範的應用程式清單，請選取這個選項。|  
    |**符合規範的應用程式清單**|如果您想要指定允許使用者安裝的應用程式清單，請選取這個選項。 任何其他安裝的應用程式都會回報為不符合規範。|  
    |**新增**|將應用程式新增至選取的清單。 指定應用程式存放區中應用程式由您選擇的名稱 (選擇性的應用程式發行者) 和 URL。<br /><br /> 若要指定 URL，請從 [Google Play 的 [應用程式] 區段](https://play.google.com/store/apps)搜尋您要使用的應用程式。<br /><br /> 開啟應用程式的頁面，然後將 URL 複製到剪貼簿。 您現在可以使用在符合規範或不符合規範的應用程式清單中使用此 URL。<br /><br /> **範例：**在 Google Play 中搜尋 **Microsoft Office Mobile**。 您要使用的 URL 是 **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**。|  
    |**編輯**|讓您編輯所選取應用程式的名稱、發行者和 URL。|  
    |**移除**|從清單中刪除選取的應用程式。|  
    |**匯入**|匯入逗點分隔值檔案中所指定的應用程式清單。 請在檔案中使用「應用程式名稱, 發行者, 應用程式 URL」格式。|  

2.  完成之後，按一下 [下一步]。 包含符合規範和不符合規範之應用程式設定的設定項目，必須部署到使用者集合。

 您也可以使用下列其中一個報告監視符合規範和不符合規範的應用程式：  

-   **指定使用者之不符合規範的應用程式和裝置清單** - 顯示安裝了不符指定原則之應用程式的使用者和裝置相關資訊。  

-   **具有不符合規範之應用程式的使用者摘要** - 顯示安裝了不符合指定原則之應用程式的使用者相關資訊。  

 如需如何使用報告的資訊，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)。  

