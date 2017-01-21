---
title: "使用 Apple Configurator 搭配 Configuration Manager 進行 iOS 混合式註冊"
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 19f4880d6e7ba3da2e4bcfe725c1c806ee3b3334


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>使用 Apple Configurator 搭配 Configuration Manager 進行 iOS 混合式註冊

適用於：System Center Configuration Manager (最新分支)

當公司購買員工使用的 iOS 裝置時，可以使用 Microsoft Intune 來管理這些裝置。 您可以將 iOS 裝置用 USB 連接至執行 Apple Configurator 的 Mac 電腦，進行預先註冊。 註冊之前，您必須先在 Intune 管理主控台中準備好公司註冊裝置的 Intune 設定檔，並將它匯出至 Mac 電腦。 註冊程序會將裝置重設成出廠預設值，並完成「設定輔助程式」的程序以設定裝置。 如果單一使用者會使用專屬的 iOS 裝置來存取公司電子郵件和公司資源 (如應用程式和行事曆等)，下列為建議的程序。  

##  <a name="a-namebkmksaea-apple-configurator-enrollment-via-setup-assistant"></a><a name="BKMK_SAE"></a> 透過設定輔助程式進行 Apple Configurator 註冊  
 透過 Apple Configurator，您可以將 iOS 裝置重設成出廠預設值，以準備讓裝置的新使用者進行設定。  這個方法需要您透過 USB 將 iOS 裝置連線到 Mac 電腦，以設定公司註冊，且該方法之前提為假設您使用 Apple Configurator 2.0。  

 **先決條件**  

-   iOS 裝置的實體存取  

-   裝置序號 - [如何取得 iOS 序號](https://support.apple.com/en-us/HT204308)  

-   USB 連接線  

-   具有 [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017) 的 Mac 電腦  

#### <a name="enable-setup-assistant-enrollment-with-configuration-manager-and-intune"></a>使用 Configuration Manager 和 Intune 啟用設定助理註冊  

1.  **新增公司的裝置註冊設定檔**   
    在 Configuration Manager 主控台的 [資產與相容性] 工作區中，依序展開 [概觀]、[公司擁有的所有裝置]、[iOS]，然後按一下 [註冊設定檔]。 在 [首頁] 索引標籤上按一下 [建立設定檔]，開啟 [建立設定檔精靈]。 在下列頁面上設定：  

    1.  在 [一般]  頁面上指定下列資訊，然後按 [下一步] 。  

        -   **名稱** - 裝置註冊設定檔的名稱。 (使用者看不到)  

        -   **描述** - 裝置註冊設定檔的描述。 (使用者看不到)  

        -   **使用者親和性** – 指定裝置的註冊方式。 在大部分使用設定輔助程式的情況下，使用 [提示輸入使用者親和性] 即可。  

            -   **提示輸入使用者親和性**：該裝置必須在初始設定期間關聯到使用者，以便之後能夠以該使用者的身分存取公司資料及傳送電子郵件。  

            -   **無使用者親和性**：該裝置不會關聯到使用者。 針對執行工作而不需存取本機使用者資料的裝置，請使用此關係。 需要使用者關係的 App 會無法運作。  

    2.  在 [裝置註冊方案] 頁面上，維持不選取 [為這個設定檔設定裝置註冊方案設定] 核取方塊，然後按一下 [下一步]。  

    3.  查看摘要，然後按一下 [下一步]。  

2.  **新增要使用設定輔助程式註冊的 iOS 裝置**   
    在 Configuration Manager 主控台的 [資產與相容性] 工作區中，依序展開 [概觀]、[公司擁有的所有裝置]、[iOS]，然後按一下 [裝置資訊]。 然後按一下 [新增裝置]。 您可以使用下列兩種方式新增裝置：  

    - 您可以**上傳包含序號的 CSV 檔案** - 建立以逗號分隔值 (.csv) 的清單，其中包含兩個不含標頭的資料行，且限制每個 csv 檔案最多可有 5000 部裝置或 5 MB。 針對每個資料列，第一個儲存格填入裝置序號，第二個儲存格則可選填裝置詳細資料。

  在文字編輯器中檢視此 .csv 檔案時，其外觀大致如下：  

    ```  
    0000000,PO 1234  
    111111111,PO 1234  
    ```  

    - 您也可以**手動新增序號和詳細資料** - 輸入最多五個裝置的序號和裝置詳細資料。  

    然後按 [下一步] 。  

3.  **選取要註冊的裝置**   
    確認要註冊的裝置。 無法匯入已註冊或透過其他方法註冊的序號。 按 [下一步]  以繼續。  

4.  **指派設定檔**   
    從可用的設定檔清單中，指定要指派給新增之裝置的設定檔，檢閱 [註冊設定檔詳細資料]，然後按一下 [完成]。 手動新增的裝置可以指派給任何註冊設定檔，但是 DEP 同步處理裝置必須指派給 DEP 啟用設定檔。  

5.  **選取要部署到 iOS 裝置的設定檔**   
    在 Configuration Manager 主控台的 [資產與相容性] 工作區中，依序展開 [概觀]、[公司擁有的所有裝置]、[iOS]，按一下 [註冊設定檔]，然後選取要部署到行動裝置的裝置設定檔。 在工作列上，按一下 [匯出...] 。 複製並儲存 [設定檔 URL]。 您稍後將在 Apple Configurator 中上傳它，以定義 iOS 裝置所使用的 Intune 設定檔。  註冊設定檔 URL 自匯出後的兩週內有效。 兩週之後，您必須匯出新的 URL 檔案才能註冊 iOS 裝置。  

     若要支援 Apple Configurator 2，必須編輯 2.0 設定檔 URL。 將：  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     取代為  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```  

6.  **使用 Apple Configurator 準備裝置**   
    您必須將 iOS 裝置連接到 Mac 電腦並註冊，以進行行動裝置管理。  

    > [!WARNING]  
    >  在註冊過程，會將裝置重設為原廠設定。  

    1.  在 Mac 電腦上，開啟 [Apple Configurator 2]。  在選單列中，依序按一下 [Apple Configurator 2] 和 [偏好設定]。  

    2.  在 [偏好設定] 窗格中，按一下 [伺服器]，再按一下左側窗格下方的 [+] 符號來啟動 MDM 伺服器精靈。 按一下 [   

    3.  輸入上面步驟 5 中 MDM 伺服器的 [名稱] 和 [註冊 URL]。 按一下 [下一步] 。  

         如果收到關於 Apple TV 的信任描述檔要求，您可以放心地按下灰色的 [X] 來關閉 [信任描述檔] 選項。 您也可以放心地忽略任何「錨點憑證」的警告。 若要繼續，請按一下 [下一步] 直到精靈完成為止。  

    4.  在 [伺服器] 窗格中，按一下新伺服器的設定檔旁邊的 [編輯]。 請確認 [註冊 URL] 確實符合從 Intune 匯出的 URL。 如果不符合，請重新輸入原始的 URL，並針對從 Intune 匯出的註冊設定檔按一下 [儲存]。  

    5.  將 iOS 行動裝置連線到具有 USB 介面卡的 Apple 電腦。  

        > [!WARNING]  
        >  在註冊過程，會將裝置重設為原廠設定。 最佳做法是重設裝置並將其開機。 最佳做法是當您啟動 [設定助理] 時，裝置應顯示「哈囉」畫面。  

    6.  按一下 [準備]。 在 [準備 iOS 裝置] 窗格上，選取 [手動]，然後按一下 [下一步]。  

    7.  於 [在 MDM 伺服器中註冊] 窗格上，選取您建立之伺服器的名稱，然後按一下 [下一步]。  

    8.  於 [在 MDM 伺服器中註冊] 窗格上，選取您建立之伺服器的名稱，然後按一下 [下一步]。  

    9. 在 [建立組織] 窗格上，選擇 [組織] 或建立新的組織，然後按一下 [下一步]。  

    10. 在 [配置 iOS 設定輔助程式] 窗格上，選擇要向使用者顯示的步驟，然後按一下 [準備]。 如果出現提示，請驗證以更新信任設定。  

    11. 當 iOS 裝置準備完成時，您即可拔掉 USB 纜線。  

7.  **散發裝置**   
    裝置現在已準備好進行公司註冊。 關閉裝置電源，並將它們散發給使用者。 開啟裝置時，設定助理將會啟動並提示使用者輸入其工作或學校帳戶。



<!--HONumber=Nov16_HO1-->


