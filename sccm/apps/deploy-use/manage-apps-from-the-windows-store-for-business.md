---
title: "管理來自商務用 Windows 市集的應用程式 | Microsoft Docs"
description: "使用 System Center Configuration Manager，從商務用 Windows 市集管理和部署應用程式。"
ms.custom: na
ms.date: 3/29/2017
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
ms.sourcegitcommit: 6accec2d356861b273b25ba2b6338d9684a46ff6
ms.openlocfilehash: f2d9da1c584f78e27e84b7f55e7ffe4dd052a27c
ms.lasthandoff: 03/29/2017

---

# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理從商務用 Windows 市集購買的應用程式
[商務用 Windows 市集](https://www.microsoft.com/business-store)是您可以在其中為您的組織尋找並個別或大量購買 Windows 應用程式的地方。 藉由將市集連線到 Configuration Manager，您就可以同步處理使用 Configuration Manager 所購買的應用程式清單、在 Configuration Manager 主控台中進行檢視，以及像是任何其他應用程式一樣進行部署。


## <a name="online-and-offline-apps"></a>線上和離線應用程式

商務用 Windows 市集支援兩種應用程式類型：

- **線上** - 此授權類型需要使用者和裝置連線到市集，以取得應用程式及其授權。 Windows 10 裝置必須已加入 Azure Active Directory 網域。
- **離線** - 組織可以快取應用程式和授權，並在其內部部署網路內直接部署，而不需要連線到市集或具有網際網路連線。

[深入了解](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview?f=255&MSPPError=-2147217396)商務用 Windows 市集。

Configuration Manager 支援在執行 Configuration Manager 用戶端的 Windows 10 裝置上，以及在向 Microsoft Intune 註冊的 Windows 10 裝置上 (又稱為混合設定)，管理商務用 Windows 市集應用程式。 Configuration Manager 提供線上和離線應用程式的下列功能。

> [!IMPORTANT]
> 若要使用這項功能，Windows 10 裝置必須執行 2015 年 11 月 (1511) 版或更新版本。


|功能|離線應用程式|線上應用程式|
|------------|------------|------------|
|將應用程式資料同步處理至 Configuration Manager<br>(每隔 24 小時同步處理一次)|[是]|是|
|從市集應用程式建立 Configuration Manager 應用程式|是|[是]|
|支援市集中的免費應用程式|[是]|是|
|支援市集中的付費應用程式|否|是|
|支援使用者或裝置集合的必要部署|是|是|
|支援使用者或裝置集合的可用部署|是|是|
|支援市集中的企業營運應用程式|是|是|

若要使用 Configuration Manager 用戶端將 線上授權的應用程式部署至 Windows 10 電腦，它們必須執行 Windows 10 Creators Update 或更新版本。

## <a name="deploying-online-apps-using-the-windows-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>使用商務用 Windows 市集在執行 Configuration Manager 用戶端的電腦部署線上應用程式
在將商務用 Windows 市集應用程式部署到執行 Configuration Manager 用戶端的電腦之前，請考慮下列各項︰

- 如需完整的功能，電腦必須執行 Windows 10 Creators Update 或更新版本。
- 電腦必須已加入 Azure Active Directory 工作場所，並在您將商務用 Windows 市集應用程式註冊為管理工具所在的相同 AAD 租用戶中。
- 當電腦使用內建的 Administrator 帳戶登入時，就無法存取商務用 Windows 市集應用程式。
- 電腦必須使用即時網際網路連線到商務用 Windows 市集。

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>執行舊版 Windows 10 電腦的注意事項
電腦若執行 Creators Update (含 Configuration Manager 用戶端) 之前的 Windows 10 版本，適用下列功能︰


- 因使用者安裝應用程式，或應用程式達到其安裝期限，或後續安裝重新評估所需部署，而強制安裝時：
    - 啟動商務用 Windows 市集應用程式將會「強制」執行該應用程式。 
    - 使用者必須從市集完成安裝，才會實際予以安裝
    - Configuration Manager 主控台中的應用程式狀態將報告為失敗，而錯誤為「Windows 市集應用程式已在用戶端電腦上開啟，正在等候使用者完成安裝。」
- 在下一個應用程式評估週期︰
    - 如果使用者從市集安裝應用程式，該應用程式將會報告狀態為 [成功]。 
    - 如果使用者未嘗試從市集安裝應用程式︰
        - 所需部署將嘗試啟動市集，並再次強制安裝應用程式。
        - 可用的部署將不會強制重新執行。

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>執行舊版 Windows 10 電腦的進一步注意事項：

- 您無法從商務用 Windows 市集部署企業營運應用程式
- 當您從市集部署付費應用程式時，將要求使用者登入市集並自行購買應用程式。
- 如果您已部署的群組原則停用存取 Windows 市集的取用者版本，即使已啟用商務用 Windows 市集，仍將無法從商務用 Windows 市集部署。


## <a name="set-up-windows-store-for-business-synchronization"></a>設定商務用 Windows 市集同步處理

**在 Azure Active Directory 中，將 Configuration Manager 登錄為 [Web 應用程式和/或 Web API] 管理工具。這會提供您一個稍後將會需要的用戶端識別碼。**
1. 在 [https://manage.windowsazure.com](https://manage.windowsazure.com) 的 [Active Directory] 節點中，選取您的 Azure Active Directory，然後按一下 [應用程式] > [新增]。
2.  按一下 [加入我的組織正在開發的應用程式]。
3.  輸入應用程式的名稱，選取 [Web 應用程式] 和/或 [Web API]，然後按一下 [下一步] 箭號。
4.  為 [登入 URL] 和 [應用程式識別碼 URI] 輸入相同的 URL。 URL 可以是任何內容，不需要解析為實際的位址。 例如，您可以輸入 *https://yourdomain/sccm*。
5.  完成精靈。

**在 Azure Active Directory 中，為登錄的管理工具建立用戶端金鑰**
1.  反白選取您剛才建立的應用程式，然後按一下 [設定]。
2.  從 [金鑰] 底下的清單中選取持續時間，然後按一下 [儲存]。 這會建立一個新的用戶端金鑰。 在您成功將商務用 Windows 市集連線到 Configuration Manager 之前，請勿離開此頁面。

**在商務用 Windows 市集中，將 Configuration Manager 設定為市集管理工具**
1.  開啟 [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools)，並在出現提示時登入。
2.  視需要接受使用條款。
3.  在 [管理工具] 底下，按一下 [Add a management tool]\(新增管理工具)。
4.  在 [Search for the tool by name]\(依名稱搜尋工具) 中，輸入您先前在 AAD 中所建立應用程式的名稱，然後按一下 [新增]。
5.  按一下您剛才匯入之應用程式旁邊的 [啟用]。
6.  如果您想要允許購買離線授權的應用程式，請在 [管理] > [帳戶資訊]頁面中，選取 [Show Offline-Licensed Apps]\(顯示離線授權的應用程式)。

**將市集帳戶新增至 Configuration Manager**

1. 請確認您已從商務用 Windows 市集至少購買一個應用程式。 在 Configuration Manager 主控台的 [系統管理] 工作區中，展開 [雲端服務]，然後按一下 [商務用 Windows 市集]。
2.  在 [常用] 索引標籤的 [商務用 Windows 市集] 群組中，按一下 [新增商務用 Windows 市集帳戶]。 
3.  從 Azure Active Directory 中，加入您的租用戶識別碼、用戶端識別碼及用戶端金鑰，然後完成精靈。
4. 完成之後，您就會在 Configuration Manager 主控台的 [商務用 Windows 市集] 清單中看到您設定的帳戶。


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>從商務用 Windows 市集應用程式建立和部署 Configuration Manager 應用程式。
1.  在 Configuration Manager 主控台的 [軟體程式庫] 工作區中，展開 [應用程式管理]，然後按一下 [市集應用程式的授權資訊]。
2.  選擇要部署的應用程式，然後在 [常用] 索引標籤的 [建立] 群組中，按一下 [建立應用程式]。
建立 Configuration Manager 應用程式以包含商務用 Windows 市集應用程式。 然後可以如處理任何其他 Configuration Manager 應用程式一樣，部署及監視此應用程式。
> [!IMPORTANT]
> 若裝置已向 Intune 註冊，只有原先註冊裝置的使用者才能使用已部署的應用程式。 其他任何使用者都無法存取此應用程式。

## <a name="monitor-windows-store-for-business-apps"></a>監視商務用 Windows 市集應用程式

在 [軟體程式庫] 工作區中，展開 [應用程式管理]，然後按一下 [市集應用程式的授權資訊]。

針對您管理的每個市集應用程式，您可以檢視應用程式的相關資訊，包括其名稱、平台、您擁有之應用程式的授權數目，以及您可以使用的授權數目。

