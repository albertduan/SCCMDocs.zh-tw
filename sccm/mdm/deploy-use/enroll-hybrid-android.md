---
title: "設定 System Center Configuration Manager 和 Microsoft Intune 的 Android 混合式裝置管理 | Microsoft Docs"
description: "準備使用 Configuration Manager 和 Intune 管理 Android 行動裝置。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: b47ecd1754a623b1b57dc5c5ecb42a6b0b64404e
ms.contentlocale: zh-tw
ms.lasthandoff: 07/29/2017

---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>以 System Center Configuration Manager 和 Microsoft Intune 設定 Android 混合式裝置管理

*適用對象：System Center Configuration Manager (最新分支)*

本主題可協助 IT 系統管理員啟用 Android 和 Android for Work 裝置的混合式註冊。 IT 系統管理員接著可以使用 System Center Configuration Manger，透過設定好的 Microsoft Intune 訂閱來管理裝置。 使用者可以從 Google Play 下載 Android 公司入口網站應用程式，以註冊 Android (包含 Samsung KNOX Standard) 和 Android for Work 裝置。

您以 Configuration Manager 系統管理員的身分，可以管理合規性設定、抹除或刪除 Android 裝置、部署應用程式，以及收集軟體和硬體清查。 如果裝置上未安裝 Android 公司入口網站應用程式，您將不會擁有清查和合規性設定等管理功能，但是仍然可以將應用程式部署到 Android 裝置。  

## <a name="enable-android-enrollment"></a>啟用 Android 註冊  
下列步驟讓 Configuration Manager 不需要工作設定檔 (亦即「傳統 Android」註冊) 即可管理 Android 裝置。

1. 請先完成[設定混合式 MDM](setup-hybrid-mdm.md) 中的必要條件和程序，再為任何平台設定註冊。  
2. 在 Configuration Manager 主控台的 [系統管理] 工作區中，選擇 [概觀] > [雲端服務] > [Microsoft Intune 訂閱]，然後選擇您的 Intune 訂閱。  
3. 在 [常用] 索引標籤的 [訂閱] 群組中，選擇 [設定平台] > [Android]。  
4. 在 [Microsoft Intune 訂閱內容] 對話方塊中，選擇 [Android] 索引標籤並選取 [啟用 Android 註冊] 方塊。  

> [!NOTE]
>  [封鎖個人擁有的裝置] 功能目前無法使用。 

 設定好之後，您必須讓使用者了解如何註冊其裝置。 請參閱[要告訴使用者關於註冊其裝置的事項](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 這項資訊適用於透過 Microsoft Intune 與 Configuration Manager 管理的行動裝置。

## <a name="enable-android-for-work-enrollment"></a>啟用 Android for Work 註冊
下列步驟可讓 Configuration Manager 使用工作設定檔管理 Android 裝置。

1. 在 https://accounts.google.com/SignUp 建立 Google 帳戶，當作您的 Android for Work 管理帳戶使用。 或者，使用與此 Intune 租用戶之所有 Android for Work 管理工作相關聯的帳戶進行登入。 此帳戶可能是管理 Android 裝置的系統管理員之間共用的 Google 帳戶。 這是您的組織在 Play for Work 主控台中管理及發行應用程式所使用的 Google 帳戶。 您會使用此帳戶來核准 Play for Work 市集中的應用程式，因此請記下帳戶名稱和密碼。
2. 將 Google 帳戶繫結至 Configuration Manager 中所管理的 Intune 租用戶，以啟用 Android 註冊：
   1. 在 Configuration Manager 主控台的 [系統管理] 工作區中，選擇 [概觀] > [雲端服務] > [Microsoft Intune 訂閱]，然後選擇您的 Intune 訂閱。
   2. 在 [常用] 索引標籤的 [訂閱] 群組中，選擇 [設定平台] > [Android for Work]。
   3. 在對話方塊中，選擇 [在 Intune 主控台中設定 Android for Work]。 Intune 主控台會在網頁瀏覽器中開啟。
   4. 使用 Intune 系統管理員認證來登入 Intune 入口網站。
   5. 選擇 [設定] 以開啟 Google Play 的 Android for Work 網站。
   6. 在 Google 的登入頁面上，輸入步驟 1 中的 Google 帳戶認證，然後提供您的公司資訊。
3. 當您返回 Intune 入口網站時，Android for Work 已啟用，並且會有三個 Android for Work 裝置註冊選項︰
   - **將所有裝置作為 Android 管理** (已停用)。 所有 Android 裝置 (包括支援 Android for Work 的裝置) 都會註冊為傳統 Android 裝置。
   - **將支援的裝置作為 Android for Work 管理** (已啟用)。 所有支援 Android for Work 的裝置都會註冊為 Android for Work 裝置。 不支援 Android for Work 的任何 Android 裝置都會註冊為傳統 Android 裝置。
   - **只為這些群組中的使用者將支援的裝置作為 Android for Work 管理**(僅為部份群組啟用)。 可讓您將 Android for Work 管理的目標設為一組有限的使用者。 只有在所選群組成員註冊支援 Android for Work 的裝置時，才將支援 Android for Work 的裝置註冊為 Android for Work 裝置。 其他所有裝置則會註冊為 Android 裝置。

> [!NOTE]
> 一項已知的問題會造成 [將這些群組中僅限使用者的受支援裝置作為 Android for Work 管理] **Android** 選項無法正常運作。 指定 Azure AD 群組中的使用者裝置將會註冊為 Android，而非 Android for Work。 若要啟用 Android for Work，您必須使用 [將所有受支援的裝置作為 Android for Work 管理] 選項。


設定好之後，您必須讓使用者了解如何註冊其裝置。 請參閱[要告訴使用者關於註冊其裝置的事項](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 這項資訊適用於透過 Microsoft Intune 與 Configuration Manager 管理的行動裝置。

繫結完成時，您會在 Intune 入口網站中看到帳戶名稱和組織名稱。 此時，您可以關閉這兩個瀏覽器。

### <a name="enroll-an-android-for-work-device"></a>註冊 Android for Work 裝置
使用者註冊 Android for Work 裝置的方式與註冊 Android 裝置類似。 使用者可以在其行動裝置上下載並安裝 Android 的「公司入口網站」應用程式。 該應用程式會提示他們在註冊的過程中建立工作設定檔。 建立工作設定檔之後，使用者必須切換到受管理的公司入口網站版本。 受管理公司入口網站會在右下角標上小型橘色公事包。

### <a name="manage-android-for-work-devices"></a>管理 Android for Work 裝置
啟用 Android for Work 註冊之後，您可以執行下列 Android for Work 裝置管理工作：
- [核准應用程式](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [建立設定項目](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [管理合規性設定](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [管理電子郵件設定檔](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [選擇性地抹除工作設定檔](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< 上一個步驟](create-service-connection-point.md)  [下一個步驟 >](set-up-additional-management.md)

