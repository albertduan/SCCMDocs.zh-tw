---
title: "建立和部署裝置相容性原則"
titleSuffix: Configuration Manager
description: "了解如何在 System Center Configuration Manager 中建立和部署裝置相容性原則。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
robots: noindex
ms.openlocfilehash: bf0099cdf4df1b7421a257e910c8682e63f8ee1e
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2017
---
# <a name="create-and-deploy-a-device-compliance-policy"></a>建立和部署裝置相容性原則

*適用於︰System Center Configuration Manager (最新分支)*


## <a name="create-a-compliance-policy"></a>建立相容性原則

1.  在 System Center Configuration Manager 主控台中，選擇 [資產與相容性]。

2.  在 [資產與合規性] 工作區中，展開 [合規性設定]，然後選擇 [合規性原則]。

3.  在 [常用] 索引標籤的 [建立] 群組中，選擇 [建立合規性原則]。

4.  在 [建立合規性原則精靈] 的 [一般] 頁面上，指定下列資訊：

  * **名稱**。 輸入合規性政策的唯一名稱。 您最多可以使用 256 個字元。

  * **描述**。 輸入一段描述以提供 VPN 設定檔的概觀，以及協助在 Configuration Manager 主控台中進行識別。 您最多可以使用 256 個字元。

  * **合規性原則類型**。 根據裝置是否受 Configuration Manager 管理，來選取您想要建立的原則類型。 這適用於版本或更新版本。<br /><br /> 針對受 Intune 管理的裝置，請選擇 **[Compliance rules for devices managed without configuration manager client (不使用 Configuration Manager 用戶端來管理之裝置的相容性規則)]** 選項。 當您選取此選項時，也可以選取要套用此原則的平台類型。

  * **報告的不符合規範嚴重性**。 指定在這個合規性政策評估為不符合規範時所報告的嚴重性等級。 可用的嚴重性層級如下：

     * **無**： 不符合這項相容性規則的裝置不會回報 Configuration Manager 報告的失敗嚴重性。
     * **資訊**： 不符合這項相容性規則的裝置會回報 Configuration Manager 報告的 [資訊] 失敗嚴重性。   
     * **警告**： 不符合這項相容性規則的裝置會回報 Configuration Manager 報告的 [警告] 失敗嚴重性。
     * **重大**： 不符合這項相容性規則的裝置會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。
     * **重大事件**： 不符合這項相容性規則的裝置會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。 此嚴重性層級也會在應用程式事件記錄檔中記錄為 Windows 事件。      

5.  在 [支援的平台] 頁面上，選擇這項合規性原則評估所在的裝置平台，或選擇 [全選] 選擇所有裝置平台。 支援的平台為：Windows 7、Windows 8.1 和 Windows 10；Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2，和 Windows Server 2016。

6.  在 [規則]  頁面上，您可以定義一或多項規則，以定義裝置必須具備才能評估為相容的設定。 當您建立相容性原則時，預設會啟用一些規則，但您可以編輯或刪除這些規則。 如需所有規則的完整清單，請參閱本主題稍後的＜合規性原則規則＞一節。

  > [!NOTE]  
  >  在 Windows 電腦上，Windows 作業系統 8.1 版會回報為 6.3，而不是 8.1。 如果 Windows 的 OS 版本規則設為 Windows 8.1，則即使裝置具有 Windows 8.1，還是會回報為不符合規範。 請確定您針對最低和最高 OS 規則所設的 Windows「回報」版本是正確的。 版本號碼必須符合 **winver** 命令所傳回的版本。 Windows Phone 沒有這個問題；版本會如預期般回報為 8.1。 針對具備 Windows 10 作業系統的 Windows 電腦，版本應該設定為 **10.0**，加上 **winver** 命令所傳回的 OS 組建編號。

7.  在精靈的 [摘要] 頁面上，請檢閱您所做出的設定，然後完成精靈。

 新的原則會顯示在 [資產與合規性] 工作區的 [合規性原則] 節點中。

## <a name="deploy-a-compliance-policy"></a>部署相容性原則

1.  在 Configuration Manager 主控台中，選擇 [資產與相容性]。

2.  在 [資產與合規性] 工作區中，展開 [合規性設定]，然後選擇 [合規性原則]。

3.  在 [常用] 索引標籤的 [部署] 群組中，選擇 [部署]。

4.  在 [部署合規性原則] 對話方塊中，選擇 [瀏覽] 以選取要部署原則的使用者集合。

     此外，您可以選取選項以在原則不符合規範時產生警示，並設定針對此原則評估合規性的排程。

5.  完成之後，請選擇 [確定]。

## <a name="monitor-the-compliance-policy"></a>監視相容性原則

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>在 Configuration Manager 主控台中檢視相容性結果

1.  在 Configuration Manager 主控台中，選擇 [監視]。

2.  在 [監視] 工作區中，選擇 [部署]。

3.  在 [部署]  清單中，選取您要檢閱相容性資訊的相容性原則部署。

4.  您可以在主頁面檢閱有關原則部署相容性的摘要資訊。 若要檢視更詳細的資訊，請選取部署，然後在 [常用] 索引標籤的 [部署] 群組中，選擇 [檢視狀態] 以開啟 [部署狀態] 頁面。

    [部署狀態] 頁面包含下列索引標籤：

    -   **符合規範**。 根據受影響的資產數目，顯示原則的合規性。 您可以選擇規則，以在 [資產與合規性] 工作區的 [使用者] 或 [裝置] 節點下方建立臨時節點，其中包含符合這項規則的所有使用者或裝置。 [資產詳細資料] 窗格會顯示符合原則的使用者或裝置。 按兩下清單中的使用者或裝置以顯示其他資訊。

    -   **錯誤**： 根據受影響的資產數目，顯示所選原則部署所有錯誤的清單。 您可以選擇規則，以在 [資產與合規性] 工作區的 [使用者] 或 [裝置] 節點下方建立臨時節點，其中包含因這項規則而產生錯誤的所有使用者或裝置。 當您選取使用者或裝置時，[資產詳細資料] 窗格會顯示受到問題影響的使用者或裝置。 按兩下清單中的使用者或裝置以顯示該問題的其他資訊。

    -   **不符合規範**。 根據受影響的資產數目，顯示原則內所有不符合規範規則的清單。 您可以選擇規則，以在 [資產與合規性] 工作區的 [使用者] 或 [裝置] 節點下方建立臨時節點，其中包含不符合這項規則的所有使用者或裝置。 當您選取使用者或裝置時，[資產詳細資料] 窗格會顯示受到問題影響的使用者或裝置。 按兩下清單中的使用者或裝置以顯示該問題的進一步資訊。

    -   **未知**。 顯示未針對所選原則部署報告合規性的所有使用者和裝置的清單，以及裝置目前的用戶端狀態。

#### <a name="to-monitor-the-compliance-status-of-an-individual-device"></a>監視個別裝置的合規性狀態

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] 工作區。

2.  選擇 [裝置]。

3.  以滑鼠右鍵按一下其中一個資料行以啟用更多資料行。

  您可以新增下列資料行︰

  - **Azure Active Directory 裝置識別碼**。  裝置在 Azure Active Directory 中的唯一識別碼。

  - **合規性錯誤詳細資料**。  端對端程序發生問題時的錯誤訊息詳細資料。 如果這個資料行空白，即表示找不到任何錯誤，並且已成功回報合規性狀態。

  - **合規性錯誤位置**。  合規性失敗的位置詳細資料。 如果這個資料行空白，即表示找不到任何錯誤，並且已成功回報合規性狀態。 合規性程序可能失敗的位置範例︰ 
      - ConfigMgr 用戶端
      - 管理點
      - Intune
      - Azure Active Directory
<br></br>
  - **合規性評估時間**。 上一次檢查合規性的時間。

  - **合規性設定時間**。 上一次合規性更新至 Azure Active Directory 的時間。

  - **條件式存取符合規範**。  電腦是否符合條件式存取原則的規範。

  > [!IMPORTANT]
  > 預設不會顯示這些資料行。

#### <a name="to-view-intune-compliance-policies-charts"></a>檢視 Intune 合規性政策圖表
1. 從 Configuration Manager 1610 版開始，在 Configuration Manager 主控台中，選擇 [監視]。

2. 在 [監視] 工作區中，移至 [概觀] > [合規性設定] > [合規性政策]。

   下列圖表隨即會出現：

    - **整體裝置合規性**。 顯示針對所有合規性原則的整體裝置合規性。
    - **不符合規範的主要原因**。 顯示裝置不符合規範的主要原則。

3. 選擇任一圖表中的區段，以向下鑽研至該類別內的裝置清單。

#### <a name="to-view-a-health-attestation-report"></a>檢視健康情況證明報告

1.  從 Configuration Manager 1602 版開始，在 Configuration Manager 主控台中，選擇 [監視]。

2.  若要依裝置合規性狀態檢視裝置目前狀態的摘要報告，請選擇 [安全性]，然後選擇 [健康情況證明]。

3.  若要檢視列出所有裝置和所有健康情況證明屬性的報告，請選擇 [安全性]，然後選擇 [健康情況證明]。

## <a name="compliance-policy-rules"></a>合規性原則規則
* **行動裝置需要密碼設定**。 您可以要求使用者輸入密碼以存取其裝置。

  **支援於：**
    * Windows Phone 8 或更新版本
    * iOS 6 或更新版本
    * Android 4.0+
    * Samsung KNOX Standard 4.0 或更新版本

* **需要密碼以解鎖閒置的裝置** (1602 更新)。 您可以要求使用者輸入密碼以存取鎖定的裝置。

  **支援於：**
  * Windows Phone 8 或更新版本
  * iOS 6 或更新版本
  * Android 4.0+
  * Samsung KNOX Standard 4.0 或更新版本

* **非使用狀態多少分鐘後需要密碼** (1602 更新)。 您可以指定使用者必須重新輸入密碼之前的閒置時間。 請將值設定為其中一個可用的選項：1 分鐘、5 分鐘、15 分鐘、30 分鐘、1 小時。

  此規則必須與 [需要密碼以解鎖閒置的裝置] 搭配使用。 在此所設定的值將會決定裝置被視為閒置和鎖定的時機。 當 [需要密碼以解鎖閒置的裝置] 設定為 **True** 時，使用者必須輸入密碼以存取鎖定的裝置。

  **支援於：**
  * Windows Phone 8 或更新版本
  * Windows RT/8.1
  * iOS 6 或更新版本
  * Android 4.0+
  * Samsung KNOX Standard 4.0 或更新版本

* **需要自動更新** (1602 更新)。 您可以要求具有 Windows 8.1 或更新版本的裝置自動安裝更新，您也可以指定更新的類別。

  值應該設定為 [無] 以防止自動安裝、設定為 [建議] 以自動安裝所有建議的更新，或設定為 [重要] 以僅安裝分類為重要的更新。

  **支援於：**
  * Windows Phone 8 或更新版本

* **允許簡單密碼**。 您可以讓使用者建立簡單密碼，例如 "1234" 或 "1111"。 預設會停用此設定。

  **支援於：**
  * Windows Phone 8 或更新版本
  * iOS 6 或更新版本

* **密碼長度下限**。 您可以指定使用者密碼至少必須含有的數字或字元數 (預設為 6)。

  **支援於：**
  * Windows Phone 8 或更新版本
  * Windows 8.1
  * iOS 6 或更新版本
  * Android 4.0+
  * Samsung KNOX Standard 4.0 或更新版本

  >[!NOTE]
  >對於執行 Windows 並使用 Microsoft 帳戶保護的裝置，若 [密碼長度下限] 超過 8 個字元，或 [字元集數目下限] 大於 2，合規性原則將無法正確進行評估。

* **在行動裝置上執行檔案加密**。 您可以要求裝置必須加密以連線至資源。 執行 Windows Phone 8 的裝置會自動加密。 如有設定 [行動裝置需要密碼設定] ，執行 iOS 的裝置會加密。 預設會啟用此設定。

  **支援於：**
  * Windows Phone 8 或更新版本
  * Windows 8.1
  * iOS 6 或更新版本
  * Android 4.0+
  * Samsung KNOX Standard 4.0 或更新版本

* **裝置不得經過越獄或 Root**。 如果您啟用此設定，已越獄 (iOS) 或已 Root (Android) 的裝置將無法符合規範。 預設會停用此設定。

  **支援於：**
  * iOS 6 或更新版本
  * Android 4.0+
  * Samsung KNOX Standard 4.0 或更新版本

* **電子郵件設定檔必須由 Intune 管理**。 當您將此選項設定為 [是] 時，裝置必須使用部署到裝置的電子郵件設定檔。 電子郵件設定檔未部署到與相容性原則目標使用者群組相同的使用者群組，則使用者的裝置將被視為不相容。

  如果使用者已經在裝置上設定符合部署到該裝置之 Intune 電子郵件設定檔的電子郵件帳戶，該裝置一樣為不相容。 在此情況下，Intune 無法覆寫使用者所佈建的設定檔，因此也無法加以管理。 使用者可以藉由移除現有的電子郵件設定，並讓 Intune 安裝受管理的電子郵件設定檔，來恢復裝置的合規性。

  如需電子郵件設定檔的詳細資訊，請參閱 [將電子郵件設定檔與 Microsoft Intune 搭配使用，以存取公司電子郵件](https://technet.microsoft.com/library/dn800672.aspx)。 預設會停用此設定。

  **支援於：**
  * iOS 6 或更新版本

* **電子郵件設定檔**。 若選取 [電子郵件帳戶必須由 Intune 管理]，請選擇 [選取] 以選擇必須用來管理裝置的電子郵件設定檔。 電子郵件設定檔必須在裝置上。

  **支援於：**
  * iOS 6 或更新版本

* **最低 OS 需求**。 當裝置不符合您所指定的最低 OS 版本需求時，它會回報為不符合規範。 隨即會顯示具有如何升級之資訊的連結。 使用者可以選擇升級其裝置，並可於升級之後存取公司資源。

  **支援於：**
  * Windows Phone 8 或更新版本
  * Windows 8.1
  * iOS 6 或更新版本
  * Android 4.0+
  * Samsung KNOX Standard 4.0 或更新版本

* **允許的最高 OS 版本**。 當裝置使用的 OS 版本比您在規則中所指定的版本還要新時，系統便會封鎖對公司資源的存取權，並要求使用者連絡其 IT 系統管理員。在您變更規則以允許該 OS 版本之前，此裝置無法用來存取公司資源。

  **支援於：**
  * Windows Phone 8 或更新版本
  * Windows 8.1
  * iOS 6 或更新版本
  * Android 4.0+
  * Samsung KNOX Standard 4.0 或更新版本

* **需要裝置回報狀況良好** (1602 更新)。 您可以設定規則來要求 Windows 10 裝置必須在新的或現有的合規性原則中回報為狀況良好。 如果您啟用此設定，系統將會透過「健康情況證明服務」(HAS)，針對下列資料點評估 Windows 10 裝置：

  - **已啟用 BitLocker**。 開啟 BitLocker 時，裝置能夠在系統已關閉或進入休眠狀態的情況下，保護存放在磁碟機中的資料來防止未經授權的存取。

   「Windows BitLocker 磁碟機加密」會將存放在 Windows 作業系統磁碟區上的所有資料都加密。 BitLocker 使用 TPM 來協助保護 Windows 作業系統和使用者資料。 它能協助確保電腦不受竄改，即使該電腦是處於無人看管、遺失或遭竊的情況。
   
   如果電腦配備相容的 TPM，BitLocker 就會使用 TPM 來鎖定保護資料的加密金鑰。 因此，必須等到 TPM 驗證電腦的狀態之後，才能存取金鑰。

  - **已啟用程式碼完整性**。 程式碼完整性是一項功能，會在每次將驅動程式或系統檔案載入記憶體時，驗證其完整性。 程式碼完整性能偵測是否有未簽署的驅動程式或系統檔案被載入到核心中。 它也能偵測系統檔案是否被由具有系統管理員權限的使用者帳戶所執行的惡意軟體所變更。

  - **已啟用安全開機**。 啟用安全開機時，會強迫系統以原廠信任的狀態啟動。 此外，啟用安全開機時，用來啟動電腦的核心元件必須具有該裝置製造商所信任的正確密碼編譯簽章。 UEFI 韌體會在讓電腦啟動之前先驗證此簽章。 如果有任何檔案已遭竄改並破壞其簽章，系統將無法啟動。

  - **已啟用初期啟動反惡意程式碼**。 此設定僅適用於電腦。 開機初期啟動的反惡意程式碼 (ELAM) 可在您網路中的電腦啟動時且在其他廠商驅動程式初始化之前，為電腦提供保護。
  
   此規則預設為關閉。

  如需 HAS 服務運作方式的資訊，請參閱 [Health Attestation CSP](https://msdn.microsoft.com/library/dn934876.aspx)(健康情況證明 CSP)。

  **支援於：**
  * Windows 10 和 Windows 10 行動裝置版

- **無法安裝在裝置上的應用程式**。 如果使用者安裝來自系統管理員不符合規範應用程式清單的應用程式，他們會在嘗試存取公司電子郵件和其他支援條件式存取的公司資源時被封鎖。 此規則在將應用程式新增至系統管理員所定義的不符合規範清單時，需要應用程式名稱和應用程式識別碼。也可以新增應用程式發行者，但它不是必要項目。

    **支援於：**
      * iOS 6 或更新版本
      * Android 4.0+
      * Samsung KNOX Standard 4.0 或更新版本
<br></br>
* **必要的密碼類型**。 指定使用者必須建立英數密碼還是數值密碼。 如果是英數密碼，您還需指定密碼必須包含的字元集數目下限。 字元集共有四種：小寫字母、大寫字母、符號和數字。

    **支援於：**
    * Windows Phone 8 或更新版本
    * Windows 8.1+
    * iOS 6 或更新版本
<br></br>
* **封鎖裝置上的 USB 偵錯**。 您不需要進行此設定，因為 Android for Work 裝置上已停用 USB 偵錯。

    **支援於：**
    * Android 4.0+
    * Samsung KNOX Standard 4.0 或更新版本
<br></br>
* **封鎖來自不明來源的應用程式**。 要求裝置必須防止來自不明來源的應用程式安裝。 您不需要進行此設定，因為 Android for Work 裝置一律會限制來自不明來源的安裝。

    **支援於：**
    * Android 4.0+
    * Samsung KNOX Standard 4.0 或更新版本
<br></br>
* **需要對應用程式進行威脅掃描**。 此設定會指定在裝置上啟用 [驗證應用程式] 功能。 

    **支援於：**
    * Android 4.2 到 4.4
    * Samsung KNOX Standard 4.0 或更新版本

### <a name="find-an-app-id"></a>尋找應用程式識別碼

應用程式識別碼是能在 Apple 與 Google 應用程式服務內唯一識別該應用程式的識別碼。 其中一個範例是 com.contoso.myapp。 尋找應用程式識別碼：

- **Android**
    - 您可以在用來建立應用程式的 Google Play 商店 URL 中找到應用程式識別碼。 範例應用程式識別碼如下︰*…?id=com.companyname.appname&hl=en*

- **iOS**
    1. 在 iTunes Store URL 中尋找類似以下範例的識別碼：*/id875948587?mt=8*

    2. 在網頁瀏覽器中，移至下列 URL，並以您剛剛找到的識別碼 (在此為先前的範例識別碼) 取代 URL 上的號碼：https://itunes.apple.com/lookup?id=875948587

    3. 下載並開啟文字檔案。
  
    4. 搜尋文字 **bundleId**。

    範例應用程式識別碼如下︰"*bundleId*":"*com.companyname.appname*" 

