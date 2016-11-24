---
title: "從商務用 Windows 市集管理應用程式 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager，從商務用 Windows 市集管理和部署應用程式。"
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e293b2ec4debf7a8513f1e3544ac234616f04d7

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理從商務用 Windows 市集購買的應用程式

適用於：System Center Configuration Manager (最新分支)

[商務用 Windows 市集](https://www.microsoft.com/business-store)是您可以在其中為您的組織尋找並個別或大量購買 Windows 應用程式的地方。 藉由將市集連線到 Configuration Manager，您就可以同步處理使用 Configuration Manager 所購買的應用程式清單、在 Configuration Manager 主控台中進行檢視，以及像是任何其他應用程式一樣進行部署。


## <a name="online-and-offline-apps"></a>線上和離線應用程式

商務用 Windows 市集支援兩種應用程式類型：

- **線上** - 此授權類型需要使用者和裝置連線到市集，以取得應用程式及其授權。 Windows 10 裝置必須已加入 Azure Active Directory 網域。
- **離線** - 組織可以快取應用程式和授權，並在其內部部署網路內直接部署，而不需要連線到市集或具有網際網路連線。

[深入了解](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview)商務用 Windows 市集。

Configuration Manager 支援在執行 Configuration Manager 用戶端的 Windows 10 裝置上，以及在向 Microsoft Intune 註冊的 Windows 10 裝置上 (又稱為混合設定)，管理商務用 Windows 市集應用程式。 Configuration Manager 提供線上和離線應用程式的下列功能。

> [!IMPORTANT]
> 若要使用這項功能，Windows 10 裝置必須執行 2015 年 11 月 (1511) 版或更新版本。

|功能|離線應用程式|線上應用程式|
|------------|------------|------------|
|將應用程式資料同步處理至 Configuration Manager<br>(每隔 24 小時同步處理一次)|[是]|是|
|從市集應用程式建立 Configuration Manager 應用程式|是|[是]|
|支援市集中的免費應用程式|[是]|是|
|支援市集中的付費應用程式|否|否|
|支援使用者或裝置集合的必要部署|是|是<sup>1</sup>|
|支援使用者或裝置集合的可用部署|是<sup>3</sup>|否<sup>2</sup>|

<sup>1</sup>只支援受 Intune 管理的裝置。 雖然不會防止您在 Configuration Manager 主控台中建立線上應用程式，再部署至受 Configuration Manager 用戶端管理的裝置，但此應用程式將無法運作。 系統會引導使用者前往應用程式市集中的相關頁面，他們必須從此位置手動安裝應用程式。

<sup>2</sup>線上應用程式只能部署並提供給受 Configuration Manager 用戶端管理之裝置的使用者或裝置集合，但是當使用者選取軟體中心內的應用程式時，系統會引導使用者前往商務用 Windows 市集，他們必須從此位置手動安裝應用程式。 不支援部署至向 Microsoft Intune 註冊的裝置。

<sup>3</sup>不支援受 Intune 管理的裝置。

> [!IMPORTANT]
> 在此版本中，如果您有內含管理中心網站和至少一個主要站台的 Configuration Manager 階層，將離線的商務用 Windows 市集應用程式部署至受 Intune 管理的裝置將會失敗。


## <a name="activate-the-windows-store-for-business-capability"></a>啟用商務用 Windows 市集功能
因為這是發行前版本功能，您必須採取下列步驟，才能將 Configuration Manager 連線到商務用 Windows 市集：

**您同意使用發行前版本功能**
1. 在 Configuration Manager 主控台的 [系統管理] 工作區中，按一下 [站台設定] > [站台]。
2. 選取階層中的頂層站台，然後開啟 [階層設定]。
3. 在 [階層設定內容] 對話方塊中，核取 [同意使用發行前功能] 方塊。
4. 按一下 [ **確定**]。

**啟用商務用 Windows 市集功能**
1. 在 Configuration Manager 主控台的 [系統管理] 工作區中，按一下 [雲端服務] > [更新與服務] > [功能]。
2. 選取 [商務用 Windows 市集整合]，然後在 [常用] 索引標籤的 [功能] 群組中，按一下 [開啟]。
3. 關閉後再開啟 Configuration Manager 主控台。
4. 您現在會在 [系統管理] 工作區的 [雲端服務] 底下，看到 [商務用 Windows 市集] 節點。

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
3.  在 [管理工具] 底下，按一下 [Add a management tool] (新增管理工具)。
4.  在 [Search for the tool by name] (依名稱搜尋工具) 中，輸入您先前在 AAD 中所建立應用程式的名稱，然後按一下 [新增]。
5.  按一下您剛才匯入之應用程式旁邊的 [啟用]。
6.  如果您想要允許購買離線授權的應用程式，請在 [管理] > [帳戶資訊]頁面中，選取 [Show Offline-Licensed Apps] (顯示離線授權的應用程式)。

**將市集帳戶新增至 Configuration Manager**

1. 請確定您已從商務用 Windows 市集至少購買一個應用程式。在 Configuration Manager 主控台的 [系統管理] 工作區中，展開 [雲端服務]，然後按一下 [商務用 Windows 市集]。
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



<!--HONumber=Nov16_HO1-->


