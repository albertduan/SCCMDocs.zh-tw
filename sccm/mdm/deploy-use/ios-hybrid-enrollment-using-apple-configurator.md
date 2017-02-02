---
title: "註冊 iOS 裝置 Apple Configurator - Configuration Manager | Microsoft Docs"
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 12/16/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: 6c6e9edbc7b2fca3d1be4feabb238efab80465fa


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>使用 Apple Configurator 搭配 Configuration Manager 進行 iOS 混合式註冊

適用於：System Center Configuration Manager (最新分支)

當公司購買員工使用的 iOS 裝置時，可以使用 Microsoft Intune 來管理這些裝置。 若要準備公司擁有的 iOS 裝置以進行註冊，您可以在 Configuration Manager 主控台中設定註冊設定檔，然後匯出設定檔 URL 以供 Apple Configurator 使用。 準備 iOS 裝置進行註冊的方式是使用 USB 纜線將它連接到 Mac 電腦，以及使用 Apple Configurator 進行設定。 Apple Configurator 會將裝置重設為原廠設定，並新增註冊設定檔，以在使用者第一次將裝置開機並執行設定助理程序時註冊裝置。

如果單一使用者會使用專屬的 iOS 裝置來存取公司電子郵件和公司資源 (如應用程式和行事曆等)，下列為建議的程序。  

## <a name="prerequisites"></a>先決條件  

-   iOS 裝置的實體存取  

-   裝置序號 - [如何取得 iOS 序號](https://support.apple.com/en-us/HT204308)  

-   具有 [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017) 的 Mac 電腦  

-   用來將裝置連接至 Mac 電腦的 USB 纜線  

## <a name="step-1-add-a-corporate-owned-device-enrollment-profile"></a>步驟 1：新增公司擁有的裝置註冊設定檔

1.  在 Configuration Manager 主控台中，移至 [資產與合規性] > [概觀] > [公司擁有的所有裝置] > [iOS] > [註冊設定檔]。 按一下 [建立設定檔]，開啟 [建立設定檔精靈]。 在下列頁面上設定：  

2.  在 [一般]  頁面上，指定下列資訊：  

    -   **名稱** (使用者看不到)  

    -   **描述** (使用者看不到)  

    -   **使用者親和性** – 指定裝置的註冊方式。 在大部分使用設定輔助程式的情況下，使用 [提示輸入使用者親和性] 即可。  

        -   **提示輸入使用者親和性**：該裝置必須在初始設定期間關聯到使用者，以便之後能夠以該使用者的身分存取公司資料及傳送電子郵件。  

        -   **無使用者親和性**：該裝置不會關聯到使用者。 針對執行工作而不需存取本機使用者資料的裝置，請使用此關係。 需要使用者關係的 App 會無法運作。

    按 [下一步]  以繼續。  

3.  在 [裝置註冊方案] 頁面上，維持不選取 [為這個設定檔設定裝置註冊方案設定] 核取方塊，然後按一下 [下一步]。  

4.  檢閱摘要，然後按一下 [下一步] 建立註冊設定檔。 按一下 [關閉] 以完成精靈。 您現在已經可以新增您想要註冊之裝置的 IMEI 編號或序號。  

## <a name="step-2-predeclare-devices-to-enroll-with-setup-assistant"></a>步驟 2：預先宣告要使用設定助理註冊的裝置

在此步驟中，您提供硬體識別碼 (IMEI 或序號) 清單，將裝置預先宣告為公司擁有的裝置。

如需詳細資訊，請參閱[使用 IMEI 和 iOS 序號預先宣告裝置](predeclare-devices-with-hardware-id.md)。 當您完成該工作時，請返回此頁面，繼續進行下一個步驟。

## <a name="step-3-export-the-profile-to-deploy-to-ios-devices"></a>步驟 3：匯出要部署到 iOS 裝置的設定檔

1.  在 Configuration Manager 主控台中，移至 [資產與合規性] > [概觀] > [公司擁有的所有裝置] > [iOS] > [註冊設定檔]。

2.  選取要部署到行動裝置的註冊設定檔，然後按一下 [匯出...]。

3.  在您可編輯的檔案中，複製並儲存 [設定檔 URL]。   

4.  若要支援 Apple Configurator 2，必須編輯 2.0 設定檔 URL。 取代 URL 的下列部分︰  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     取代為  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  儲存已編輯的設定檔 URL。 在[下節](#step-4-prepare-the-device-with-apple-configurator)中，您將使用它在 Apple Configurator 中新增註冊設定檔 URL。  

> [!NOTE]
> 註冊設定檔 URL 自匯出後的兩週內有效。 兩週之後，您必須匯出新的 URL，才能註冊 iOS 裝置。

## <a name="step-4-prepare-the-device-with-apple-configurator"></a>步驟 4：使用 Apple Configurator 準備裝置

若要準備 iOS 裝置以進行註冊，您可以將每個裝置連接到 Mac 電腦，並將註冊設定檔上傳至其中。  

> [!WARNING]  
>  Apple Configurator 會抹除裝置，並將其重設為原廠設定。  

1.  在 Mac 電腦上，開啟 [Apple Configurator 2]。  

2.  在功能表列中，按一下 [Apple Configurator 2] > [偏好設定]。  

2.  在 [偏好設定] 窗格中，按一下 [伺服器]，再按一下左側窗格下方的 [+] 符號來啟動 MDM 伺服器精靈。 按一下 [下一步] 。  

3.  輸入[先前](#step-3-export-the-profile-to-deploy-to-ios-devices)儲存的 [名稱] 和 [註冊 URL]。 按一下 [下一步] 。  

   > [!NOTE]
   > 如果您收到關於 Apple TV 之信任設定檔需求的警告，您可以放心地按一下灰色 [X] 來取消 [信任設定檔] 選項。 您也可以放心地忽略任何「錨點憑證」的警告。

   若要繼續，請按一下 [下一步] 直到精靈完成為止。  

4.  在 [伺服器] 窗格中，按一下新伺服器的設定檔旁邊的 [編輯]。 請確認 [註冊 URL] 確實符合您先前輸入的 URL。 如果 URL 不同，請重新輸入 URL，然後按一下 [儲存]。  

5.  使用 USB 纜線，將 iOS 裝置連接到 Mac 電腦。  

  > [!WARNING]  
  >  這個程序會將裝置重設為原廠設定。 連接裝置之前，請重設裝置，並將其開機。 最佳做法是裝置應該先顯示「哈囉」畫面，再繼續進行。  

6.  按一下 [準備]。 在 [準備 iOS 裝置] 窗格上，選取 [手動]，然後按一下 [下一步]。  

7.  在 [Enroll in MDM Server] (在 MDM 伺服器中註冊) 窗格上，選取您建立的伺服器名稱，然後按一下 [下一步]。  

9. 在 [建立組織] 窗格上，選擇 [組織] 或建立新的組織，然後按一下 [下一步]。  

10. 在 [Configure iOS Setup Assistant] (設定 iOS 設定助理) 窗格上，選擇要呈現給使用者的步驟，然後按一下 [準備]。 如果出現提示，請驗證以更新信任設定。  

11. 完成時，即可拔掉 USB 纜線。  

重複適用於您想要準備進行註冊之所有裝置的這些步驟。

## <a name="step-5-distribute-devices"></a>步驟 5：散發裝置

裝置現在已準備好進行公司註冊。 關閉裝置電源，並將它們散發給使用者。 開啟裝置時，設定助理將會啟動並提示使用者輸入其工作或學校帳戶，來開始註冊。



<!--HONumber=Jan17_HO4-->


