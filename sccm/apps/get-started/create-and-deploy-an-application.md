---
title: "建立和部署應用程式 | System Center Configuration Manager"
description: "建立和部署包含商務營運應用程式的應用程式，並了解如何有效地管理應用程式。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
caps.latest.revision: 15
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 12653342e2e311a9bbfc2a7aad3101c0e7f0bce0


---
# <a name="create-and-deploy-an-application-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立和部署應用程式

*適用於︰System Center Configuration Manager (最新分支)*

在本主題中，您將直接使用 System Center Configuration Manager 建立應用程式。 在此範例中，您將建立和部署一個應用程式，這個應用程式包含 Windows 電腦的商務營運應用程式 (稱為 **Contoso.msi** ) 而且必須安裝在公司內執行 Windows 10 的所有電腦上。 在過程中，您將了解有助於有效地管理應用程式的事項。  

 這個程序旨在提供如何建立和部署 Configuration Manager 應用程式的概觀。 不過，它未涵蓋您可設定或如何建立和部署其他平台之應用程式的所有選項。  

 如需與每個平台相關的特定詳細資料，請參閱下列其中一個主題︰  

-   [建立 Windows 應用程式](../../apps/get-started/creating-windows-applications.md)  
-   [建立 iOS 應用程式](../../apps/get-started/creating-ios-applications.md)  
-   [建立 Android 應用程式](../../apps/get-started/creating-android-applications.md)  
-   [建立 Windows Phone 應用程式](../../apps/get-started/creating-windows-phone-applications.md)  
-   [建立 Mac 電腦應用程式](../../apps/get-started/creating-mac-computer-applications.md)  
-   [建立 Linux 和 UNIX 伺服器應用程式](../../apps/get-started/creating-linux-and-unix-server-applications.md) 
-   [建立 Windows Embedded 應用程式](../../apps/get-started/creating-windows-embedded-applications.md) 

  
如果您已經熟悉 Configuration Manager 應用程式，則可以略過這個主題。 不過，您可以檢閱[建立應用程式](../../apps/deploy-use/create-applications.md)，來了解建立和部署應用程式時可用的所有選項。  
  
## <a name="before-you-start"></a>開始之前  

請確定您已檢閱[應用程式管理簡介](/sccm/apps/understand/introduction-to-application-management)中的資訊以備妥您的站台來安裝應用程式，而且您了解本主題中所使用的術語。  

 也請確定 **Contoso.msi** 應用程式的安裝檔案位於網路上可存取的位置。  
  
## <a name="create-the-configuration-manager-application"></a>建立 Configuration Manager 應用程式  
  
### <a name="start-the-create-application-wizard-and-create-the-application"></a>啟動建立應用程式精靈以及建立應用程式  
  
1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] > [應用程式管理] > [應用程式]。  
  
3.  在 **[首頁]** 索引標籤的 **[建立]** 群組中，按一下 **[建立應用程式]**。  

4.  在 [建立應用程式精靈]  的 [一般] 頁面上，選擇 [從安裝檔案自動偵測此應用程式的相關資訊] 。 這會將從安裝.msi 檔案中擷取的資訊預先填入精靈中的部分資訊，然後指定下列資訊：  

    -   **類型** - 選擇 [Windows Installer (\*.msi 檔案)]  

    -   **位置** - 輸入安裝檔 **Contoso.msi** 的位置 (或按一下 [瀏覽] 選取位置)。 請注意，必須以「\\\伺服器\共用\檔案」格式指定位置，Configuration Manager 才能找到安裝檔。  
  
    最後的結果會像下列螢幕擷取畫面：  
  
    ![應用程式管理精靈一般頁面](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  
  
5.  按一下 [下一步] 。 在 [匯入資訊] 頁面上，您會看到應用程式以及已匯入至 Configuration Manager 之任何相關聯檔案的相關資訊。 完成之後，請再按一次 [下一步]  。  

6.  在 [一般資訊] 頁面上，您可以提供應用程式的進一步資訊，協助您在 Configuration Manager 主控台中排序並找到它。  

     此外，[安裝程式] 欄位可讓您指定將用來在電腦上安裝應用程式的完整命令列。 您可以編輯這個檔案來新增您自己的屬性 (例如 **/q** 表示自動安裝)。  

    > [!TIP]  
    >  在匯入應用程式安裝檔時，可能已自動填入精靈的這個頁面上的部分欄位。  

     最後的畫面會像下列螢幕擷取畫面：  
  
     ![應用程式管理精靈一般資訊頁面](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  
  
7.  按一下 [  在 [摘要] 頁面上，您可以確認應用程式設定，然後完成精靈。  

 您已完成建立應用程式。 若要找到它，請在 [軟體程式庫]  工作區中，展開 [應用程式管理] ，然後按一下 [應用程式] 。 在這個範例中，您將看到：  
  
 ![最終應用程式圖形](/sccm/apps/get-started/media/Final-app-graphic.png)  
  
## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>檢查應用程式和其部署類型的內容  

現在，您已建立應用程式，可以在必要時修正應用程式設定。 若要查看應用程式內容，請選取應用程式，然後在 [首頁]  索引標籤的 [內容]  群組中按一下 [內容] 。  

 在 [<Contoso\> 應用程式內容] 對話方塊中，您將看到許多可設定來調整應用程式行為的項目。 如需可設定之所有設定的詳細資料，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。 這個範例旨在讓您只變更應用程式部署類型的某些內容。  
  
 按一下 [部署類型]  索引標籤，並選取 [Contoso 應用程式]  部署類型，然後按一下 [編輯] 。   
您會看到與下列類似的對話方塊：  
 
![應用程式管理應用程式內容頁面](/sccm/apps/get-started/media/App-management-app-properties-page.png)  
  
## <a name="add-a-requirement-to-the-deployment-type"></a>新增部署類型的需求  
 需求指定必須符合條件才可以在裝置上安裝應用程式。  您可以從內建需求中選擇，也可以建立您自己的需求。 在這個範例中，您將新增應用程式只會在執行 Windows 10 的電腦上安裝的需求。  
  
1.  從剛剛開啟的部署類型內容頁面中，按一下 [需求]  索引標籤。  

2.  按一下 [新增]  開啟 [建立需求]  對話方塊。  

3.  在 [建立需求]  對話方塊中，指定下列資訊：  

    -   **類別** - **裝置**  

    -   **條件** - **作業系統**  

    -   **規則類型** - **值**  

    -   **運算子** - **其中一個**  

    -   從作業系統清單中，選取 [Windows 10] 。  
  
    最後的對話方塊會像下列對話方塊：  
  
    ![應用程式管理需求頁面](/sccm/apps/get-started/media/App-management-requirements-page.png)  
  
4.  按一下 [確定] 關閉您開啟的每個內容頁面，並回到 Configuration Manager 主控台中的 [應用程式] 清單。  

> [!TIP]  
>  需求有助於減少您需要的 Configuration Manager 集合數目。 因為您剛才指定應用程式只能安裝在執行 Windows 10 的電腦上，所以稍後可以將這個應用程式部署至集合，而這個集合包含執行許多不同作業系統的電腦，而且應用程式只會安裝於 Windows 10 電腦上。  
  
## <a name="add-the-application-content-to-a-distribution-point"></a>將應用程式內容新增至發佈點  

若要將應用程式成功地部署至電腦，您接下來必須確定將應用程式內容複製至發佈點。 電腦將存取發佈點來安裝應用程式。  

> [!TIP]  
>  若要深入了解 Configuration Manager 中的發佈點和內容管理，請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  
  
1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [應用程式]  ，然後在應用程式清單中選取您已建立的 [Contoso 應用程式]  。  

3.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [發佈內容] 。  

4.  在 [發佈內容精靈]  的 [一般] 頁面上，確認應用程式名稱正確，然後按一下 [下一步] 。  

5.  在 [內容]  頁面上，檢閱將複製至發佈點的資訊，然後按一下 [下一步] 。  

6.  在 [內容目的地]  頁面上，按一下 [新增] 選取一個或多個發佈點或者在其上安裝應用程式內容的發佈點群組。  

7.  完成精靈。  

 您可以確認已從 [發佈狀態]  >  [內容狀態] 建立應用程式。  
  
## <a name="deploy-the-application"></a>部署應用程式  

接下來，將應用程式部署至階層中的裝置集合。 在此範例中，您會將應用程式部署至 [所有系統]  裝置集合。  

> [!TIP]  
>  請記住，因為您先前選取的需求，所以只有 Windows 10 電腦才會安裝應用程式。  
  
1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] > [應用程式管理] > [應用程式]。  
  
3.  從應用程式清單中，選取您先前建立的應用程式 ([Contoso 應用程式] )，然後在 [首頁]  索引標籤上，按一下 [部署]  群組中的 [部署] 。  

4.  在 [部署軟體精靈]  的 [一般] 頁面上，按一下 [瀏覽]  選取 [所有系統]  裝置集合。  

5.  在 [內容] 頁面上，確認已選取您想要電腦從中安裝應用程式的發佈點。  

6.  在 [部署設定] 頁面上，確認部署動作設為 [安裝]，而且部署目的設為 [必要]。  

    > [!TIP]  
    >  將部署目的設為 [必要] ，確定應用程式已安裝在符合所設定需求的電腦上。 如果您將此值設為 [可用] ，則使用者可以視需要從軟體中心安裝應用程式。  

7.  在 [排程]  頁面上，您可以設定應用程式的安裝時間。 在此範例中，選取 [可用時間之後越快越好] 。  

8.  在 [使用者經驗] 頁面上，按 [下一步] 接受預設值。  

9. 完成精靈。  

 使用下面＜監視應用程式＞  一節中的資訊，查看您應用程式部署的狀態。  
  
## <a name="monitor-the-application"></a>監視應用程式  
 在本節中，您將快速查看剛剛所部署應用程式的部署狀態。  
  
### <a name="to-review-the-deployment-status"></a>檢閱部署狀態  
  
1.  在 Configuration Manager 主控台中，按一下 [監視] > [部署]。  
  
3.  從部署清單中，選取 [Contoso 應用程式] 。  

4.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [檢視狀態] 。  

5.  選取下列其中一個索引標籤，以查看應用程式部署的其他狀態：  

    -   **成功** - 已在指出的電腦上成功安裝應用程式。  

    -   **進行中** - 尚未完成安裝應用程式。  

    -   **錯誤** - 在指出的電腦上安裝應用程式時發生錯誤。 也會顯示錯誤的進一步資訊。  

    -   **不符合需求** - 未嘗試在指出的裝置上安裝應用程式，原因是它們不符合您所設定的需求 (在此範例中，原因是它們未執行 Windows 10)。  

    -   **未知** - Configuration Manager 無法報告部署狀態。 請稍後再試。  

> [!TIP]  
>  有數種方式可以監視應用程式部署。 如需完整詳細資訊，請參閱[監視應用程式](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  
  
## <a name="end-user-experience"></a>使用者經驗  

具有執行 Windows 10 且由 Configuration Manager 所管理之電腦的使用者會看到一則訊息，告知他們必須安裝 Contoso 應用程式。 在他們接受安裝之後，將會安裝應用程式。  



<!--HONumber=Nov16_HO1-->


