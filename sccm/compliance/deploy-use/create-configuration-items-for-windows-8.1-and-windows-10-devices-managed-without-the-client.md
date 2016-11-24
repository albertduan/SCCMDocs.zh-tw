---
title: "為不是使用 System Center Configuration Manager 用戶端管理的 Windows 8.1 和 Windows 10 裝置建立設定項目 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager Windows 10 設定項目管理 Windows 10 電腦的設定。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c262291a-80fe-47f3-a6d0-a605fe8b1f06
caps.latest.revision: 20
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 84914426016c049de9bdf797b02bf0cc15301a71
ms.openlocfilehash: 1691fe56b9c6fb6aa6889a4451985a1bf6c2e1b5


---
# <a name="create-configuration-items-for-windows-81-and-windows-10-devices-managed-without-the-system-center-configuration-manager-client"></a>為不是使用 System Center Configuration Manager 用戶端管理的 Windows 8.1 和 Windows 10 裝置建立設定項目

*適用對象：System Center Configuration Manager (最新分支)*


使用 System Center Configuration Manager **Windows 8.1 和 Windows 10** 設定項目，管理 Microsoft Intune 中所註冊或 Configuration Manager 透過內部部署方式管理之 Windows 8.1 和 Windows 10 裝置的設定。  

## <a name="create-a-windows-81-and-windows-10-configuration-item"></a>建立 Windows 8.1 和 Windows 10 設定項目  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [設定項目]。  

3.  在 [常用]  索引標籤上，按一下 [建立]  群組中的 [建立設定項目] 。  

4.  在 [建立設定項目精靈]  的 [一般] 頁面上，指定設定項目的名稱和選擇性描述。  

5.  在 [指定您要建立的組態項目類型] 下，選取 [Windows 8.1 和 Windows 10] 。  

6.  如果您要建立並指派類別，以協助您在 Configuration Manager 主控台中搜尋和篩選設定項目，請按一下 [類別]。  

7.  在 [支援的平台] 頁面上，選取將評估設定項目的特定 Windows 平台。  

8.  在 [裝置設定] 頁面上，選取您想要設定的設定群組。 請參閱本主題的 [Windows 8.1 和 Windows 10 組態項目設定參考](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-81-and-windows-10-configuration-item-settings-reference) 以取得詳細資訊，然後按一下 [下一步] 。  

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

##  <a name="windows-81-and-windows-10-configuration-item-settings-reference"></a>Windows 8.1 和 Windows 10 組態項目設定參考  

### <a name="password"></a>密碼  
 這些設定僅適用於執行 Windows 10 和更新版本的裝置。  

|設定|詳細資料|  
|-------------|-------------|  
|**需要裝置上的密碼設定**|支援的裝置上需要的密碼。|  
|**最小密碼長度 (字元數)**|密碼長度下限。|  
|**密碼到期天數**|密碼必須變更之前的天數。|  
|**記住的密碼數目**|防止重複使用先前用過的密碼。|  
|**抹除裝置前允許的失敗登入次數**|如果登入嘗試失敗是這個數目即抹除裝置。|  
|**鎖定裝置前的閒置時間**|指定裝置鎖定前可閒置 (沒有使用者輸入) 的時間量。|  
|**密碼複雜性**|選擇 PIN 是否可指定如 '1234'，或是否必須提供強式密碼。|  
|**密碼複雜性** - **密碼所需的複雜字集數目**|如果您選取**強式**密碼，請使用此設定來設定複雜字集所需的數目。 若為強式密碼，這至少應該設定為 [3]，表示所需的字母和數字。 如果想要強制執行另需特殊字元的密碼，例如 **(%$**，請選取 [4]。|
|**將密碼復原 PIN 傳送至 Exchange Server**|設為 [已啟用] 或 [已停用]。|  

###  <a name="device"></a>裝置  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**螢幕擷取**|允許您擷取裝置顯示的螢幕擷取畫面。<br /><br /> (僅限 Windows 10)|  
|**診斷資料提交 (Windows 8.1 和更舊版本)**|允許提交應用程式記錄檔。<br /><br /> (僅限 Windows 8.1)|  
|**診斷資料提交 (Windows 10)**|允許提交應用程式記錄檔。|  
|**地理位置**|允許裝置使用定位服務資訊。<br /><br /> (僅限 Windows 10)|  
|**複製和貼上**|使用複製和貼上在應用程式之間傳輸資料。<br /><br /> (僅限 Windows 10)|  
|**Bluetooth**|允許使用裝置藍牙功能。|  
|**可透過藍牙搜尋的模式**|允許要透過其他藍牙裝置探索的裝置。<br /><br /> (僅限 Windows 10)|  
|**藍牙通知**|允許使用藍芽通知。<br /><br /> (僅限 Windows 10)|  
|**錄音**|允許使用裝置的錄音功能。<br /><br /> (僅限 Windows 10)|  

### <a name="email-management"></a>電子郵件管理  
 這些設定適用於執行 Windows 8.1 和 Windows 10 的裝置。  

|設定|詳細資料|  
|-------------|-------------|  
|**POP 和 IMAP 電子郵件**|允許連線到使用 POP 和 IMAP 標準的電子郵件帳戶。|  
|**保留電子郵件的時間上限**|從伺服器刪除電子郵件之前的保留期限。|  
|**允許的訊息格式**|指定使用者電子郵件可否為 HTML，或僅限純文字。|  
|**純文字電子郵件 (自動下載) 的大小上限**|控制自動下載時的純文字電子郵件大小上限。|  
|**HTML 電子郵件 (自動下載) 的大小上限**|控制自動下載時的 HTML 電子郵件大小上限。|  
|**附件 (自動下載) 的大小上限**|設定自動下載的電子郵件大小上限。|  
|**行事曆同步處理**|允許將行事曆同步處理到裝置。|  
|**自訂電子郵件帳戶**|允許在裝置上使用非 Microsoft 帳戶。|  
|**在 Windows Mail 應用程式中將 Microsoft 帳戶變成選用項目**|設定此項，在 Windows Mail 中移除對 Microsoft 帳戶的需求。|  

### <a name="store"></a>市集  
 這些設定僅適用於執行 Windows 10 和更新版本的裝置。  

|設定|詳細資料|  
|-------------|-------------|  
|**應用程式市集**|允許存取裝置上的應用程式市集。|  
|**輸入密碼以存取應用程式市集**|使用者必須輸入密碼才能存取應用程式市集。|  
|**應用程式內建購買功能**|允許使用者在應用程式內購買。|  

### <a name="browser"></a>瀏覽器  
 這些設定適用於執行 Windows 8.1 和 Windows 10 的裝置。  

|設定|詳細資料|  
|-------------|-------------|  
|**允許網頁瀏覽器**|允許在裝置上使用網頁瀏覽器。|  
|**自動填寫**|使用者可以變更瀏覽器中的自動完成設定。|  
|**動態指令碼處理**|瀏覽器可以執行指令碼，例如 ActiveX 指令碼。|  
|**外掛程式**|使用者可以將外掛程式加入 Internet Explorer 中。|  
|**快顯封鎖程式**|啟用或停用瀏覽器的快顯封鎖程式。|  
|**Cookie**|允許 Cookie 儲存在裝置上。|  
|**詐騙警告**|啟用或停用潛在詐騙網站警告。|  

###  <a name="internet-explorer"></a>Internet Explorer  
 這些設定適用於執行 Windows 8.1 和 Windows 10 的裝置。  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**一律傳送「不要追蹤」標頭**|防止瀏覽資訊傳送到協力廠商站台。|  
|**內部網路安全性區域**|將安全性層級指派給內部網路安全性區域。|  
|**網際網路區域的安全性等級**|設定網際網路區域的安全性等級。|  
|**內部網路區域的安全性等級**|設定內部網路區域的安全性等級。|  
|**信任的網站區域的安全性等級**|設定信任的網站區域的安全性等級。|  
|**受限制的網站區域的安全性等級**|設定受限制的網站區域的安全性等級。|  
|**內部網路區域的命名空間**|設定要加入內部網路區域或從中移除的網站。|  
|**只輸入一個單字即可存取內部網路網站**|如果輸入無前置 HTTP 的有效站台名稱，啟用或停用允許 Internet Explorer 自動移至內部網路站台的設定：|  
|**企業模式功能表選項**|允許使用者從 Internet Explorer 的 **[工具]** 功能表啟用和停用企業模式。|  
|**記錄報告位置 (URL)**|指定啟用企業模式時要記錄的已瀏覽網站的 URL。|  
|**企業模式站台清單位置 (URL)**|當啟用企業模式時，指定要使用企業模式的網站清單位置。|  

###  <a name="cloud"></a>雲端  
 這些設定適用於執行 Windows 8.1 和 Windows 10 的裝置。  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**設定同步處理**|允許裝置之間的設定同步處理。|  
|**認證同步處理**|允許裝置之間的認證同步處理。|  
|**Microsoft 帳戶**|允許在裝置上使用 Microsoft 帳戶。|  
|**透過計量付費連線的設定同步處理**|當計量付費網際網路連線時，允許同步處理設定。|  

###  <a name="security"></a>安全性  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**未簽署的檔案安裝**|允許載入未簽署的檔案。<br /><br /> (僅限 Windows 10)|  
|**未簽署的應用程式**|允許載入未簽署的應用程式。<br /><br /> (僅限 Windows 10)|  
|**SMS 和多媒體簡訊**|允許從裝置傳送 SMS 和多媒體簡訊。<br /><br /> (僅限 Windows 10)|  
|**卸除式存放裝置**|允許在裝置上使用卸除式存放裝置，例如 SD 記憶卡。<br /><br /> (僅限 Windows 10)|  
|**相機**|允許使用裝置相機。<br /><br /> (僅限 Windows 10)|  
|**近距離無線通訊 (NFC)**|允許在裝置上使用 NFC 通訊。<br /><br /> (僅限 Windows 10)|  
|**防竊模式**|控制是否啟用 Windows 10 防竊模式。<br /><br /> (僅限 Windows 10)|  
|**設定檔**|佈建 Windows RT 裝置的 VPN 設定檔。<br /><br /> (僅限 Windows 8.1)|  
|**設定檔名稱**|佈建 Windows RT 裝置的 VPN 設定檔。<br /><br /> (僅限 Windows 8.1)|  
|**所有使用者的設定檔**|佈建 Windows RT 裝置的 VPN 設定檔。<br /><br /> (僅限 Windows 8.1)|  

###  <a name="peak-synchronization"></a>尖峰同步處理  
 這些設定僅適用於執行 Windows 10 和更新版本的裝置。  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**指定尖峰時間**|設定行動裝置同步處理的尖峰時間。|  
|**尖峰同步處理頻率**|設定在您設定的尖峰時間進行同步處理的頻率。|  
|**離峰同步處理頻率**|設定在您設定的尖峰時間以外的期間進行同步處理的頻率。|  

###  <a name="roaming"></a>漫遊  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**漫遊時管理裝置**|允許 Configuration Manager 漫遊時管理裝置。<br /><br /> (僅限 Windows 10)|  
|**漫遊時下載軟體**|漫遊時允許下載應用程式和軟體。<br /><br /> (僅限 Windows 10)|  
|**漫遊時下載電子郵件**|漫遊時允許下載電子郵件。<br /><br /> (僅限 Windows 10)|  
|**數據漫遊**|存取資料時允許網路之間的漫遊。|  

###  <a name="encryption"></a>加密  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**儲存卡加密**|搭配裝置的所有儲存卡都需要加密。<br /><br /> (僅限 Windows 10)|  
|**裝置上的檔案加密**|裝置上的檔案需要加密。|  
|**需要電子郵件簽署**|需要先簽署電子郵件，再進行傳送。|  
|**簽署演算法**|選取已簽署電子郵件的簽署演算法。|  
|**需要電子郵件加密**|需要先加密電子郵件，再進行傳送。|  
|**加密演算法**|選取用來加密電子郵件的演算法。|  

###  <a name="wireless-communications"></a>無線通訊  
 這些設定僅適用於執行 Windows 10 和更新版本的裝置。  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**無線網路連線**|啟用或停用裝置 Wi-Fi 功能。|  
|**Wi-Fi 網際網路共用功能**|讓使用者將他們的裝置用為行動熱點。|  
|**盡可能將資料卸載至 Wi-Fi**|設定此項，盡可能在裝置上使用 Wi-Fi 連線。|  
|**Wi-Fi 熱點報告**||  
|**手動設定 Wi-Fi**||  

#### <a name="to-configure-a-wireless-network-connection"></a>設定無線網路連線  

1.  在 [設定行動裝置無線通訊設定]  頁面上，按一下 [新增] 。  

2.  在 [無線網路連線]  對話方塊中，指定要在行動裝置上佈建的無線連線相關資訊：  

    |設定|詳細資訊|  
    |-------------|----------------------|  
    |**網路名稱 (SSID)**|輸入 Wi-Fi 網路的名稱。|  
    |**網路連線**|從 **[網際網路]** 或 **[工作]**選擇。|  
    |**驗證**|從下列位置選取無線連線的驗證方法：<br>- **開啟**<br>-                             **共用**<br>- **WPA**<br>- **WPA-PSK**<br>- **WPA2**<br>- **WPA2-PSK**|  
    |**資料加密**|選擇這個連線使用的加密方法。 可以選取的值會隨您選取的 **驗證** 方法而不同：<br>- **已停用**<br>- **WEP**<br>- **TKIP**<br>- **AES**|  
    |**金鑰索引**|選取搭配使用 **WEP** **[資料加密]** 設定的 **1** 至 **4**的金鑰索引。|  
    |**這個網路連線到網際網路**|如果您要提供讓無線連線的行動裝置連線到網際網路的 Proxy 設定，請選取這個選項。|  
    |**Proxy 伺服器設定**|視需要指定 **HTTP** 、 **WAP** 和 **[通訊端]**的 **[伺服器]** 和 **[連接埠]**設定。|  
    |**啟用 802.1X 網路存取**|如果您想要藉由指定 EAP 類型保障連線安全，請選取這個選項。|  
    |**EAP 類型**|從下列位置選擇要使用的 EAP 類型：<br>- **PEAP**<br>- **智慧卡或憑證**|  

3.  完成後，請按一下 [確定] 。  

### <a name="certificates"></a>憑證  
 讓您匯入憑證以安裝在行動裝置上。  

 按一下 [匯入] ，然後指定下列值：  

-   **憑證檔案** – 按一下 [瀏覽]，然後選取您要匯入且副檔名為 **.cer** 的憑證檔案。  

-   **目的地存放區** – 請從下列位置選擇一或多個目的地存放區，其中的匯入憑證會由下列加入至行動裝置：  

    -   **Root**  

    -   **CA**  

    -   **正常**  

    -   **特殊權限**  

    -   **SPC**  

    -   **對等**  

-   **角色** – 如果選取 **SPC** (軟體發行者憑證) 做為目的地存放區，請從下列位置選擇要與憑證產生關聯的角色：  

    -   **行動電信業者**  

    -   **Manager**  

    -   **已驗證的使用者**  

    -   **IT 系統管理員**  

    -   **未驗證的使用者**  

    -   **信任的佈建伺服器**  

### <a name="system-security"></a>系統安全性  

|設定|詳細資料|  
|-------------|-------------|  
|**使用者帳戶控制**|啟用或停用裝置上的 Windows 使用者帳戶控制。|  
|**網路防火牆**|啟用或停用 Windows 防火牆。<br /><br /> (僅限 Windows 8.1)|  
|**更新 (Windows 8.1 和更舊版本)**|選擇 Windows 軟體更新下載到電腦的方式。 例如，您可以自動下載更新，但是讓使用者選擇何時安裝它們。|  
|**更新的最小分類**|選擇會下載到 Windows 電腦的更新最小分類： **[無]**、 **[重要]**或 **[建議]**。|  
|**更新 (Windows 10)**|選擇 Windows 軟體更新下載到電腦的方式。 例如，您可以自動下載更新，但是讓使用者選擇何時安裝它們。<br /><br /> (僅限 Windows 10)|  
|**安裝日期**|選擇將安裝更新的日期。<br /><br /> (僅限 Windows 10)|  
|**安裝時間**|選擇將安裝更新的時間。<br /><br /> (僅限 Windows 10)|  
|**SmartScreen**|啟用或停用 Windows 智慧型檢測。|  
|**防毒保護**|選取此選項，確保裝置上已安裝防毒軟體。|  
|**防毒特徵已是最新版本**|選取此選項，確保防毒特徵碼檔案為最新。|  
|**發行前版本功能**|讓 Microsoft 能夠將發行前版本設定和功能部署至裝置。<br /><br /> (僅限 Windows 10)|  
|**手動安裝根憑證**|(僅限 Windows 10)|  

###  <a name="windows-server-work-folders"></a>Windows Server 工作資料夾  
 這些設定適用於執行 Windows 8.1 和 Windows 10 的裝置。  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**工作資料夾 URL**|設定使用者可以從他們的裝置連線到的 Windows Server 工作資料夾位置。|  

### <a name="allowed-and-blocked-apps-windows-phone-only"></a>允許及封鎖的應用程式 (僅限 Windows Phone)  
 讓您指定公司中符合規定或不符合規定且受 Intune 管理的應用程式清單。 Windows Phone 可以允許或封鎖這些應用程式的安裝。  

 您無法在同一個組態項目中，同時指定符合規定及不符合規定的應用程式。  

#### <a name="to-specify-apps-that-will-be-allowed-or-blocked"></a>指定要允許或封鎖的應用程式  

1.  在 **[允許及封鎖的應用程式清單]** 頁面上，指定下列資訊：  

    |設定|詳細資訊|  
    |-------------|----------------------|  
    |**封鎖的應用程式清單**|如果您想要指定不允許使用者安裝的應用程式清單，請選取這個選項。|  
    |**允許的應用程式清單**|如果您想要指定允許使用者安裝的應用程式清單，請選取這個選項。 任何其他應用程式將會遭到封鎖而無法安裝。|  
    |**新增**|將應用程式新增至選取的清單。 指定應用程式存放區中應用程式由您選擇的名稱 (選擇性的應用程式發行者) 和 URL。<br /><br /> 若要指定 URL，請從 Windows 市集搜尋您要使用的應用程式。<br /><br /> 開啟應用程式的頁面，然後將 URL 複製到剪貼簿。 您現在可以在允許或封鎖的應用程式清單中使用這個 URL。<br /><br /> **範例：** 在市集中搜尋 **Skype** 應用程式。 您要使用的 URL 是 **http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51**。|  
    |**編輯**|讓我們編輯所選取應用程式的名稱、發行者和 URL。|  
    |**移除**|從清單中刪除選取的應用程式。|  
    |**[匯入]**|匯入逗點分隔值檔案中所指定的應用程式清單。 請在檔案中使用「應用程式名稱, 發行者, 應用程式 URL」格式。|  

### <a name="windows-10-team"></a>Windows 10 團隊版  
 這些設定僅適用於執行 Windows 10 團隊版的裝置。  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**允許在偵測器偵測到室內有人時自動喚醒螢幕**|可在裝置感應器偵測到室內有人時自動喚醒裝置。|  
|**需要 PIN 碼以進行無線投影**|您必須先指定是否輸入 PIN 碼，才可以使用裝置的無線投影功能。|  
|**維護期間**|設定可以進行裝置更新的間隔。 您可以設定間隔的開始時間和持續時間 (從 1 到 5 小時) 。|  

### <a name="microsoft-edge"></a>Microsoft Edge  
 這些設定適用於執行 Windows 10 和更新版本的裝置。  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**允許網址列中的搜尋建議**|讓您的搜尋引擎在您輸入搜尋片語時建議網站。|  
|**允許將內部網路流量傳送到 Internet Explorer**||  
|**允許不要追蹤**|「不要追蹤」會通知網站，您不希望它們追蹤您造訪過的站台。|  
|**啟用 SmartScreen**|使用 SmartScreen，來檢查使用者下載的檔案未包含惡意程式碼。|  
|**允許快顯視窗**|允許或停用瀏覽器快顯視窗。|  
|**允許 Cookie**|允許或停用 Cookie。|  
|**允許自動填入**|允許使用 Edge 瀏覽器的自動填寫功能。|  
|**允許密碼管理員**|允許使用 Edge 瀏覽器的密碼管理員功能。|  
|**企業模式網站清單位置**|指定要尋找將在企業模式下開啟之網站清單的位置。 使用者無法編輯這份清單。|  

### <a name="windows-information-protection-formerly-enterprise-data-protection"></a>Windows 資訊保護 (原企業資料保護)

企業中員工擁有的裝置日漸增加，資料不慎從企業難以控管的應用程式和服務 (如電子郵件、社交媒體和公用雲端) 外洩的風險也更高。 比方說，員工透過個人電子郵件帳戶傳送最新的工程圖片、複製並將產品資訊貼進推文，或將進行中的銷售報表儲存到公用雲端存放裝置等情況。

Windows 資訊保護 (WIP) 有助防止這類資料外洩的可能，同時不干擾員工的體驗。 WIP 也可協助保護企業應用程式和資料，避免企業擁有的裝置與員工辦公用的個人裝置發生意外的資料外洩情況，而且不需要變更環境或其他應用程式。

 Configuration Manager WIP 設定項目可管理受 WIP 保護的應用程式清單、企業網路位置、保護等級和加密設定。

如需如何使用 Configuration Manager 設定企業資料保護的相關訊，請參閱[使用 Windows 資訊保護 (WIP) 保護您的企業資料](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)。



<!--HONumber=Nov16_HO1-->

