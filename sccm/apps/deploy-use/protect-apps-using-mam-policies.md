---
title: "使用行動應用程式管理原則來保護應用程式 | System Center Configuration Manager"
description: "修改您部署之應用程式的功能，讓這些應用程式符合公司的相容性和安全性原則。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b7936-a5ca-45c5-8bef-10424eb2e091
caps.latest.revision: 13
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: dfbf6b2001e3259abb7246ab463682b0ead4f4e8


---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>使用 System Center Configuration Manager 中的行動應用程式管理原則來保護應用程式

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 應用程式管理原則可讓您修改所部署之應用程式的功能，以協助使其符合公司的相容性和安全性原則。 例如，您可以限制受限應用程式中的剪下、複製及貼上作業，或將應用程式設定成只能在受管理瀏覽器中開啟所有的網頁連結。 應用程式管理原則支援：  

-   執行 Android 4 和更新版本的裝置。  

-   執行 iOS 7 和更新版本的裝置。  

除了受管理的裝置，也可以使用行動應用程式管理原則來保護不受 Intune 管理之裝置上的應用程式。 您可以使用這項新功能，對連線到 Office 365 服務的應用程式套用行動應用程式管理原則。 連線到內部部署 Exchange 或 SharePoint 的應用程式不支援這項功能。  
若要使用這項新功能，您必須使用 Azure 預覽入口網站。 下列主題可協助您開始使用：  
-   [在 Azure 入口網站中開始使用行動應用程式管理原則](https://technet.microsoft.com/library/mt627830.aspx)  
-   [使用 Microsoft Intune 建立及部署行動應用程式管理原則](https://technet.microsoft.com/library/mt627829.aspx)  

與 Configuration Manager 中的設定項目和基準不同的是，您不用直接部署應用程式管理原則。 而是將原則與您想要限制的應用程式部署類型建立關聯。 當應用程式部署類型已部署並安裝在裝置上時，您指定的設定將會生效。  

若要將限制套用至應用程式，應用程式必須加入 Microsoft Intune 應用程式軟體開發套件 (SDK)。 有兩種方法可以取得這種類型的應用程式：  

-   **使用受原則管理的應用程式** (Android 及 iOS)：已內建 App SDK。 若要加入此類型的應用程式，請從應用程式市集 (例如 iTunes Store 或 Google Play) 指定應用程式的連結。 這種類型的應用程式不需要進行任何處理。 如需適用於 iOS 和 Android 裝置之受原則管理的應用程式清單，請參閱 [Microsoft Intune 行動應用程式管理原則的受管理應用程式](https://technet.microsoft.com/en-us/library/dn708489.aspx)。  

-   **使用「包裝的」應用程式** (Android 及 iOS)：應用程式透過使用 **Microsoft Intune App Wrapping Tool**重新封裝，以包含 App SDK。 此工具通常用來處理內部建立的公司應用程式。 它不能用來處理從應用程式市集下載的應用程式。 請參閱 [使用 Microsoft Intune App Wrapping Tool 準備 iOS 應用程式以利行動應用程式管理](https://technet.microsoft.com/en-us/library/dn878028.aspx) 和 [使用 Microsoft Intune App Wrapping Tool 準備 Android 應用程式以利行動應用程式管理](https://technet.microsoft.com/en-us/library/mt147413.aspx)。  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>以行動應用程式管理原則建立及部署應用程式  
  
##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>步驟 1：取得受原則管理的應用程式連結，或者建立包裝的應用程式  

-   **取得受原則管理之應用程式的連結** - 從應用程式市集尋找並記下您要部署之受原則管理的應用程式的 URL。  

     例如 iPad 版 Microsoft Word 應用程式的 URL 為 **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  

-   **若要建立包裝的應用程式** - 請使用 [準備將 iOS 應用程式交由 Microsoft Intune App Wrapping Tool 進行行動應用程式管理](https://technet.microsoft.com/en-us/library/dn878028.aspx) 和 [準備將 Android 應用程式交由 Microsoft Intune App Wrapping Tool 進行行動應用程式管理](https://technet.microsoft.com/en-us/library/mt147413.aspx) 這兩個主題中的資訊，來建立包裝的應用程式。  

     此工具會建立處理過的應用程式和相關聯的資訊清單檔案。 當您在建立包含此應用程式的 Configuration Manager 應用程式時，會使用這些檔案。  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>步驟 2：建立包含應用程式的 Configuration Manager 應用程式  
 建立 Configuration Manager 應用程式的程序會有所不同，取決於您使用的是受原則管理的應用程式 (外部連結)，或是使用透過 Microsoft Intune App Wrapping Tool for iOS (iOS 的應用程式套件) 所建立的應用程式。 使用下列其中一個程序建立 Configuration Manager 應用程式。  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] > [應用程式管理] > [應用程式]。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立應用程式]  以開啟 [建立應用程式精靈]。  

4.  在 [一般]  頁面上，選取 [從安裝檔案自動偵測此應用程式的相關資訊] 。  

5.  在 **[類型]** 下拉式清單中，選取 **[iOS 的應用程式套件 (\*.ipa 檔)]**。  

6.  按一下 [瀏覽]  以選取您要匯入的應用程式套件，然後按 [下一步] 。  

7.  在 [一般資訊]  頁面上，輸入您想要使用者在公司入口網站看見的說明文字與類別資訊。  

8.  完成精靈。  

 新應用程式顯示在 [軟體程式庫]  工作區的 [應用程式]  節點中。  
  
### <a name="create-an-application-containing-a-link-to-a-policy-managed-app"></a>建立內含受管理原則應用程式連結的應用程式  
  
1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] > [應用程式管理] > [應用程式]。  
  
3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立應用程式]  以開啟 [建立應用程式精靈]。  

4.  在 [一般]  頁面上，選取 [從安裝檔案自動偵測此應用程式的相關資訊] 。  

5.  在 [類型]  下拉式清單中，選取下列其中一項：  

    -   針對 iOS： **App Store 上的 iOS 應用程式封裝**  

    -   針對 Android： **Google Play 上的 Android 應用程式封裝**  

6.  輸入應用程式的 URL (來自步驟 1)，然後按 [下一步] 。  

7.  在 [一般資訊]  頁面上，輸入您想要使用者在公司入口網站看見的說明文字與類別資訊。  

8.  完成精靈。  

 新應用程式顯示在 [軟體程式庫]  工作區的 [應用程式]  節點中。  

##  <a name="step-3-create-an-application-management-policy"></a>步驟 3：建立應用程式管理原則  
 接下來，您會建立應用程式管理原則並將其與應用程式產生關聯。 您可以建立一般或受管理的瀏覽器原則。  
  
1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] > [應用程式管理] > [應用程式管理原則]。  
3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立應用程式管理原則] 。  

4.  在 [一般]  頁面上，輸入該原則的名稱和描述，然後按 [下一步] 。  

5.  在 [原則類型]  頁面上選取平台並針對此原則選取原則類型，然後按 [下一步] 。 目前有下列原則類型可供使用：  

    -   **一般**：[一般] 原則類型可讓您修改所部署之應用程式的功能，以協助使其符合貴公司的相容性和安全性原則。 例如，您可以限制受限制應用程式內的剪下、複製及貼上作業。  

    -   **受管理的瀏覽器**：設定要允許或封鎖受管理的瀏覽器開啟 URL 清單。 [受管理的瀏覽器] 原則類型可讓您修改 Intune Managed Browser 應用程式的功能。 這是讓您能夠管理使用者可執行之動作的網頁瀏覽器，包括他們可以瀏覽的網站，以及如何在瀏覽器內開啟內容連結。 深入了解  [iOS 的 Intune Managed Browser 應用程式](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) 和 [Android 的 Intune Managed Browser 應用程式](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en)。  

6.  在 [iOS 原則]  或 [Android 原則]  頁面上，視需要設定下列值，然後按 [下一步] 。 選項可能會視您設定原則的裝置類型而不同。  

|值|詳細資訊|  
|-----------|----------------------|  
|**限制要在公司管理的瀏覽器中顯示網頁內容**|啟用這項設定時，會在受管理的瀏覽器中開啟應用程式中的任何連結。 您必須將此應用程式部署到裝置，此選項才會運作。|  
|**防止 Android 備份** 或 **防止 iTunes 和 iCloud 備份**|停用從應用程式備份任何資訊。|  
|**允許應用程式將資料傳送到其他應用程式**|指定此應用程式可以將資料傳送過去的應用程式。 您可以選擇不允許資料傳送到任何應用程式、只允許傳送至其他受限制的應用程式，或允許傳送到任何應用程式。<br /><br /> 針對 iOS 裝置，若要避免受管理與未受管理應用程式之間的文件傳送，您必須也設定及部署行動裝置安全性原則來停用 [在其他未受管理的應用程式中允許受管理的文件] 設定。<br /><br /> 如果您選取只允許傳送到其他受限制的應用程式，Intune PDF 和影像檢視器 (如果已部署) 會用來開啟個別類型的內容。|  
|**允許應用程式接收來自其他應用程式的資料**|指定此應用程式可以接收其資料的應用程式。 您可以選擇不允許來自任何應用程式的資料傳輸、只允許來自其他受限制應用程式的傳輸，或允許來自任何應用程式的傳輸。|  
|**避免「另存新檔」**|停用在任何使用此原則的應用程式中使用 [另存新檔]  選項。|  
|**限制與其他應用程式的剪下、複製和貼上**|指定如何與應用程式搭配使用剪下、複製和貼上作業。 從下列選項進行選擇：<br /><br /> **封鎖** – 不允許在此應用程式與其他應用程式之間進行剪下、複製和貼上的作業。<br /><br /> **原則管理應用程式** – 僅允許此應用程式與其他受限制的應用程式之間的剪下、複製和貼上作業。<br /><br /> **原則管理應用程式與貼上** – 從此應用程式剪下或複製的資料，只允許貼到其他受限制的應用程式。 允許從任何應用程式剪下或複製資料貼上到此應用程式。<br /><br /> **任何應用程式** - 與這個應用程式的剪下、複製和貼上作業沒有任何限制。|  
|**需要簡單的 PIN 碼才能存取**|需要使用者輸入他們指定的 PIN 碼才能使用此應用程式。 會要求使用者在第一次執行應用程式時設定。|  
|**PIN 重設之前的嘗試次數**|指定使用者必須重設 PIN 之前可以嘗試的 PIN 輸入次數。|  
|**需要公司認證才能存取**|要求使用者必須輸入其公司的登入資訊，才能存取應用程式。|  
|**需要裝置符合公司原則才能存取**|只允許在裝置未越獄或 root 時使用應用程式。|  
|**重新檢查存取需求前等候時間 (分鐘)**|在 [逾時]  欄位中，指定啟動應用程式之後，重新檢查應用程式存取需求之前的時間間隔。<br /><br /> 在 [離線寬限期]  欄位中，如果裝置已離線，請指定重新檢查應用程式存取需求之前的時間間隔。|  
|**加密應用程式資料**|指定此應用程式相關聯的所有資料都將加密，包括儲存在外部的資料，例如 SD 卡。<br /><br /> **iOS 的加密**<br /><br /> 針對與 Configuration Manager 行動應用程式管理原則相關聯的應用程式，資料會使用作業系統所提供的裝置層級加密在靜止時加密。 您可以透過裝置 PIN 碼原則 (必須由 IT 管理員設定) 來啟用。 需要 PIN 碼時，資料將會根據行動應用程式管理原則中的設定加密。 如 Apple 文件 [iOS 7 所使用的模組經 FIPS 140-2 認證](http://support.apple.com/en-us/HT202739)中所述。<br /><br /> **Android 的加密**<br /><br /> 針對與 Configuration Manager 行動應用程式管理原則相關聯的應用程式，加密由 Microsoft 所提供。 資料會在檔案 I/O 作業期間，根據行動應用程式管理原則中的設定，以同步方式加密。 Android 上的受管理應用程式使用 CBC 模式的 AES-128 加密，並利用平台的密碼編譯程式庫。 加密方法未經 FIPS 140-2 認證。 裝置儲存空間上的內容將一律加密。|  
    |**封鎖螢幕擷取** (僅限 Android 裝置)|指定在使用此應用程式時，裝置的螢幕擷取功能會遭到封鎖。|  

7.  在 [受管理的瀏覽器]  頁面上，選取是否允許受管理的瀏覽器只在清單中開啟 URL或封鎖受管理的瀏覽器從清單中開啟 URL，並管理清單中的 URL，然後按 [下一步] 。  

    > [!WARNING]  
    >  如需詳細資訊，請參閱[使用受管理的瀏覽器原則管理網際網路存取](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md)。  
  
8.  完成精靈。  

 新原則會顯示在 [軟體程式庫]  工作區的 [應用程式管理原則]  節點中。  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>步驟 4：建立應用程式管理原則與部署類型間的關聯  
 
 當您針對需要應用程式管理原則的應用程式建立部署類型時，Configuration Manager 會在關聯的應用程式進行部署時，識別應用程式的管理原則必須連結到此部署類型，並提示您將其與應用程式管理原則產生關聯。 針對受管理的瀏覽器，則必須同時與一般和受管理的瀏覽器原則產生關聯。 如需詳細資訊，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。  
  
> [!IMPORTANT]  
>  如果已部署應用程式，則新部署類型的部署會失敗，直到建立此關聯為止。 您可以在應用程式之 [內容]  中的 [應用程式管理]  索引標籤上建立關聯。  

> [!IMPORTANT]  
>  針對執行早於 iOS 7.1 之作業系統的裝置，應用程式解除安裝時不會移除相關聯的原則。  
>   
>  如果裝置並未從 Configuration Manager 註冊，原則就不會從應用程式中移除。 即使之後解除安裝並重新安裝應用程式，已套用原則的應用程式將會保留原則設定。  

##  <a name="step-5-monitor-the-app-deployment"></a>步驟 5：監視應用程式部署  
 建立並部署與行動應用程式管理原則相關聯的應用程式之後，您可以監視應用程式並解決任何原則衝突。  
  
1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] > [概觀] > [部署]。  
  
3.  選取部署後，在 [首頁]  索引標籤上按一下 [內容] 。  

4.  在部署的詳細資料窗格中，按一下 [相關物件]  下的 [應用程式的管理原則] 。  

 如需監視應用程式的詳細資訊，請參閱[監視應用程式](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  

##  <a name="how-policy-conflicts-are-resolved"></a>如何解決原則衝突  
 第一次部署到使用者或裝置時，如果行動應用程式管理原則有衝突，衝突的特定設定值會從部署到應用程式的原則移除，應用程式會使用內建的衝突值。  

 後續部署到應用程式或使用者時，如果行動應用程式管理原則有衝突，衝突的特定設定值將不會在已部署至應用程式的行動應用程式管理原則中更新，且應用程式會使用該設定現有的值。  

 在裝置或使用者收到兩個衝突原則的情況下，會適用下列行為：  

-   如果原則已部署至裝置，則不會覆寫現有的原則設定。  

-   如果原則尚未部署到裝置，而已部署兩個衝突的設定，則會使用裝置內建的預設設定。  

##  <a name="available-policy-managed-apps"></a>可用的原則管理應用程式  
 如需適用於 iOS 和 Android 裝置之受原則管理的應用程式清單，請參閱 [Microsoft Intune application partners](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune-partners) (Microsoft Intune 應用程式合作夥伴)。  



<!--HONumber=Nov16_HO1-->


