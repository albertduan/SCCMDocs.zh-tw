---
title: "管理來自商務用 Windows 市集的應用程式 | Microsoft Docs"
description: "使用 System Center Configuration Manager，從商務用 Windows 市集管理和部署應用程式。"
ms.custom: na
ms.date: 11/19/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3847a85c11d7b72b84095ba9add563bdf5c49a75
ms.openlocfilehash: 605cdd01d767dda3467198f5e6539448f9b559f6

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理從商務用 Windows 市集購買的應用程式

*適用於：System Center Configuration Manager (最新分支)*

您可以在[商務用 Windows 市集](https://www.microsoft.com/business-store)中尋找適用於組織的 Windows 應用程式，並個別購買或大量購買。 將市集與 Configuration Manager 連線時，您即可將購買的應用程式清單與 Configuration Manager 同步處理、在 Configuration Manager 主控台中進行檢視，並依照任何其他應用程式的一般方法進行部署。


## <a name="online-and-offline-apps"></a>線上和離線應用程式

商務用 Windows 市集支援兩種應用程式類型：

- **線上**--此授權類型需要使用者和裝置連線到市集，以取得應用程式及其授權。 Windows 10 裝置必須已加入 Azure Active Directory 網域。
- **離線**--組織可以快取應用程式和授權，並在其內部部署網路內直接部署；不需要連線到市集，也不需要網際網路連線。

深入了解[商務用 Windows 市集](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview)。

Configuration Manager 支援在下列裝置上管理商務用 Windows 市集應用程式：執行 Configuration Manager 用戶端的 Windows 10 裝置以及已註冊 Microsoft Intune 的 Windows 10 裝置 (混合設定)。 Configuration Manager 提供線上和離線應用程式的下列功能。

> [!IMPORTANT]
> 若要使用這些功能，Windows 10 裝置必須執行 2015 年 11 月 (1511) 版或更新版本。

|功能|離線應用程式|線上應用程式|
|------------|------------|------------|
|將應用程式資料同步處理至 Configuration Manager<br>(每隔 24 小時會同步處理一次，或者，您可以起始立即同步處理)|是|是|
|從市集應用程式建立 Configuration Manager 應用程式|是|[是]|
|支援市集中的免費應用程式|是|是<sup>1</sup>|
|支援市集中的付費應用程式|否|是<sup>1</sup>|
|支援使用者或裝置集合的必要部署|是|是<sup>1</sup>|
|支援使用者或裝置集合的可用部署|是<sup>2</sup>|否|

<sup>1</sup>僅支援受 Intune 管理的裝置。 雖然您仍可在 Configuration Manager 主控台中建立線上應用程式，再將其部署至受 Configuration Manager 用戶端管理的裝置，但此部署會失敗。 系統會引導使用者前往應用程式市集中的相關頁面，以手動安裝應用程式。

<sup>2</sup>僅支援受 Configuration Manager 用戶端管理的裝置。

<!--- ## Activate the Windows Store for Business capability
Because this is a pre-release feature, before you can connect Configuration Manager to the Windows Store for Business, you must take the following steps:

**Give your consent to use pre-release features**
1. In the **Administration** workspace of the Configuration Manager console, choose **Site Configuration** > **Sites**.
2. Select the top-level site in your hierarchy, then, open **Hierarchy Settings**.
3. In the **Hierarchy Settings Properties** dialog box, check the box, **Consent to use Pre-Release** features.
4. Choose **OK**.

**Activate the Windows Store for Business capability**
1. In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Features**.
2. Select **Windows Store for Business Integration**, and then in the **Home** tab, in the **Features** group, choose **Turn on**.
3. Close and re-open the Configuration Manager console.
4. You'll now see the node **Windows Store for Business** in the **Administration** workspace under **Cloud Services**. --->

## <a name="set-up-windows-store-for-business-synchronization"></a>設定商務用 Windows 市集同步處理

> [!IMPORTANT]
> 設定 Configuration Manager 和商務用 Windows 市集之間的連線時，您必須提供一個資料夾來存放從市集同步處理的應用程式內容。
若要保障此資料夾的安全且其內容可順利部署到裝置，請確定下列權限都已就緒：
-   使用 **Computer$** 帳戶時，安裝服務連接點站台系統角色 (階層中的頂層站台) 的電腦，必須具有指定資料夾的讀取和寫入權限。
-   應用程式作者必須具有指定資料夾的讀取權限。
-   裝載 SMS 提供者執行個體的每部電腦，其 **Computer$** 帳戶必須能夠使用您指定的資料夾。


在 Azure Active Directory 中，將 Configuration Manager 註冊為 [Web 應用程式] 或 [Web API] 管理工具。 這會提供您一個稍後將會需要的用戶端識別碼。
1. 在 Active Directory 節點 ([https://manage.windowsazure.com](https://manage.windowsazure.com)) 中，選取您的 Azure Active Directory，然後選擇 [應用程式] > [新增]。
2.  選擇 [加入我的組織正在開發的應用程式]。
3.  輸入應用程式的名稱，選取 [Web 應用程式] 和/或 [Web API]，然後選擇 [下一步]。
4.  為 [登入 URL] 和 [應用程式識別碼 URI] 輸入相同的 URL。 URL 可以是任何內容，不需要解析為實際的位址。 例如，您可以輸入 *https://yourdomain/sccm*。
5.  完成精靈。

在 Azure Active Directory 中，為已註冊的管理工具建立用戶端金鑰。
1.  反白顯示您剛才建立的應用程式，然後選擇 [設定]。
2.  從 [金鑰] 底下的清單中選取持續時間，然後選擇 [儲存]。 這會建立一個新的用戶端金鑰。 在您成功將商務用 Windows 市集連線到 Configuration Manager 之前，請不要離開此頁面。

在商務用 Windows 市集中，將 Configuration Manager 設為市集管理工具。
1.  開啟 [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools)，並在出現提示時登入。
2.  視需要接受使用條款。
3.  在 [管理工具] 底下，選擇 [Add a management tool] (新增管理工具)。
4.  在 [Search for the tool by name] (依名稱搜尋工具) 中，輸入您先前在 Azure Active Directory 中所建立應用程式的名稱，然後選擇 [新增]。
5.  選擇您剛才匯入之應用程式旁邊的 [啟用]。
6.  如果您想要允許購買離線授權的應用程式，請在 [管理] > [帳戶資訊] 頁面中，選取 [Show Offline-Licensed Apps] (顯示離線授權的應用程式)。

將市集帳戶新增至 Configuration Manager。

1. 請確認已從商務用 Windows 市集至少購買一個應用程式。 在 Configuration Manager 主控台的 [管理] 工作區中，展開 [雲端服務]，然後選擇 [商務用 Windows 市集]。
2.  在 [常用] 索引標籤的 [商務用 Windows 市集] 群組中，選擇 [新增商務用 Windows 市集帳戶]。
3.  從 Azure Active Directory 中，加入您的租用戶識別碼、用戶端識別碼及用戶端祕密金鑰，然後完成精靈。
4. 完成之後，您就會在 Configuration Manager 主控台的 [商務用 Windows 市集] 清單中看到您設定的帳戶。

變更要在應用程式類別目錄中顯示的應用程式語言，以供使用者下載。

1.  在 Configuration Manager 主控台的 [管理] 工作區中，選擇 [雲端服務] > [更新與服務] > [商務用 Windows 市集]。
2.  選取您的商務用 Windows 市集帳戶，然後選擇 [內容]。
3.  選取 [語言]。
4.  新增或移除應用程式類別目錄中會顯示的語言。 選取將會提供給使用者的預設應用程式類別目錄語言。

>[!IMPORTANT]
>在此版本中，如果您變更的語言需要同步處理，則必須重新啟動站台伺服器上的 SMS Executive 服務，語言設定才會生效。


從 Azure Active Directory 修改用戶端祕密金鑰。

1.  在 Configuration Manager 主控台的 [管理] 工作區中，選擇 [雲端服務] > [更新與服務] > [商務用 Windows 市集]。
2.  選取您的商務用 Windows 市集帳戶，然後選擇 [內容]。
3.  在 [商務用 Windows 市集帳戶內容] 對話方塊的 [用戶端祕密金鑰] 欄位中，輸入新的金鑰，然後選擇 [驗證]。 驗證後，選擇 [套用]，然後關閉對話方塊。

## <a name="synch-apps-from-the-store-with-configuration-manager"></a>將來自市集的應用程式與 Configuration Manager 同步處理

每隔 24 小時會同步處理一次，或者，您可以透過下列程序起始立即同步處理：

1. 在 Configuration Manager 主控台的 [管理] 工作區中，選擇 [雲端服務] > [更新與服務] > [商務用 Windows 市集]。
3.  在 [常用] 索引標籤的 [同步] 群組中，選擇 [立即同步]。
4.  您所購買的應用程式就會出現在 [應用程式管理] 工作區的 [市集應用程式的授權資訊] 節點中。


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>從商務用 Windows 市集應用程式建立和部署 Configuration Manager 應用程式

此程序假設您已從商務用 Windows 市集取得至少一個免費應用程式，或購買至少一個付費的線上授權應用程式。

1.  在 Configuration Manager 主控台的 [軟體程式庫] 工作區中，展開 [應用程式管理]，然後選擇 [市集應用程式的授權資訊]。
2.  選擇要部署的應用程式，然後在 [常用] 索引標籤的 [建立] 群組中，選擇 [建立應用程式]。
建立 Configuration Manager 應用程式以包含商務用 Windows 市集應用程式。 然後可以如處理任何其他 Configuration Manager 應用程式一樣，部署及監視此應用程式。

> [!IMPORTANT]
> 若裝置已向 Intune 註冊，只有原先註冊裝置的使用者才能使用已部署的應用程式。 其他使用者都無法使用此應用程式。

## <a name="monitor-windows-store-for-business-apps"></a>監視商務用 Windows 市集應用程式

在 [軟體程式庫] 工作區中，展開 [應用程式管理]，然後選擇 [市集應用程式的授權資訊]。

針對您管理的每個市集應用程式，您可以檢視應用程式的相關資訊，包括其名稱、平台、您擁有之應用程式的授權數目，以及您可以使用的授權數目。



<!--HONumber=Dec16_HO3-->


