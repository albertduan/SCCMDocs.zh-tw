---
title: "將您的 MDM 授權單位變更為 Intune"
description: "了解如何將 MDM 授權單位從 Configuration Manager (混合式) 變更為 Intune 獨立部署。"
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/14/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.openlocfilehash: 12218472aa3f06ae041134f6cc092430e406c542
ms.sourcegitcommit: 948644072bd158b156f782a4376bcd50fac7c73a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/14/2017
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>將您的 MDM 授權單位變更為 Intune 獨立部署

*適用於：System Center Configuration Manager (最新分支)*    

您可以將設定自 Configuration Manager 主控台的現有 Microsoft Intune 租用戶 (混合式 MDM) 變更為 Intune 獨立部署。 將租用戶層級的 MDM 授權單位變更為 Intune，是僅限雲端設定中[將混合式 MDM 使用者和裝置移轉至 Intune 獨立部署](migrate-hybridmdm-to-intunesa.md)程序的最後階段。    

> [!Important]    
> 若要在不先將混合式 MDM 使用者移轉至 Intune 的情況下變更您的 MDM 授權單位，請參閱[變更您的 MDM 授權單位](change-mdm-authority.md)。

本主題中的步驟會將租用戶的 MDM 授權單位變更為 Intune，並會移轉尚未移轉到 Intune 獨立部署的所有裝置。 本主題提供的資訊，是關於如何將設定自 Configuration Manager 主控台的現有 Microsoft Intune 租用戶 (混合式) 變更為 Intune 獨立部署，並假設您已完成下列步驟：
- 已使用 [Intune 資料匯入工具](migrate-import-data.md)將 Configuration Manager 物件匯入到 Intune。 
- [已備妥使用者移轉所需的 Intune](migrate-prepare-intune.md)，以確保使用者和其裝置在移轉後可繼續受到管理。
- [已變更特定使用者的 MDM 授權單位 (混合式 MDM 授權單位)](migrate-mixed-authority.md)，以開始從 Azure 入口網站管理使用者裝置。


## <a name="users-and-devices-that-have-not-been-migrated"></a>尚未移轉的使用者和裝置
您已經移轉許多使用者並測試過 Intune 功能，以確定一切符合預期。 因此，您的原則、設定檔與應用程式等已在 Intune 中設定，而且已徹底測試過裝置上的物件。 在 MDM 授權單位變更之後，您的租用戶層級原則應該就不需要新的設定。 不過，對於先前尚未移轉的使用者和裝置，請檢閱下列有關 MDM 授權單位變更後會如何的資訊：    
- 在裝置簽入服務並完成同步處理之前，很可能需要經歷一些轉換時間 (最多 8 小時)。
- 裝置在變更後必須與服務連線，新的 MDM 授權單位 (Intune 獨立部署) 的設定才能取代裝置上的現有設定。
- 部分來自先前 MDM 授權單位 (混合式) 的基本設定 (例如設定檔)，將會在裝置上保留最多 7 天。 
- 裝置若無關聯的使用者 (通常發生在 iOS 裝置註冊計劃或大量註冊的案例)，便不會移轉至新的 MDM 授權單位。 針對這些裝置，您需要連絡支援人員來取得協助，以便將這些裝置移至新的 MDM 授權單位。

## <a name="prerequisites"></a>先決條件
檢閱下列資訊以準備變更 MDM 授權單位：
- 您必須有 Configuration Manager 1610 版或更新版本，才有變更 MDM 授權單位的選項可供選擇。
- 在變更 MDM 授權單位之前，請務必將 Intune/EMS 授權指派給所有目前由混合式 MDM 管理的使用者。 在變更 MDM 授權單位之後，擁有授權可確保使用者及其裝置會由 Intune 獨立部署所管理。 如需詳細資訊，請參閱[將 Intune 授權指派給您的使用者帳戶](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)。
- 請確定已指派 Intune/EMS 授權給系統管理使用者帳戶。

### <a name="change-the-mdm-authority-to-intune"></a>將 MDM 授權單位變更為 Intune
使用下列程序，將租用戶層級的 MDM 授權單位變更為 Intune。

1.  在 Configuration Manager 主控台中，移至 [系統管理] &gt; [概觀] &gt; [雲端服務] &gt; [Microsoft Intune 訂閱]，然後刪除現有的 Intune 訂閱。
2.  選取 [將 MDM 授權單位變更為 Microsoft Intune]，然後按一下 [下一步]。

    ![移除 Microsoft Intune 訂閱對話方塊](media/mdm-change-delete-subscription.png)
3.  登入您原本在 Configuration Manager 中設定 MDM 授權單位時所使用的 Intune 租用戶。
4.  按一下 [下一步] ，並完成精靈。
5.  MDM 授權單位已重設完畢。 Intune 訂閱應該不會再顯示於 Configuration Manager 主控台的 [Microsoft Intune 訂閱] 節點中。
6.  使用您先前使用的 Intune 租用戶登入 [Azure 入口網站中的 Intune](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/overview)。    

  > [!Important]    
  > 請勿使用 Intune 傳統主控台。 您必須登入 Azure 入口網站中的 Intune。
7.  確認 MDM 授權單位已變更為 **Microsoft Intune**。 

## <a name="next-steps"></a>後續步驟
完成 MDM 授權單位的變更之後，請檢閱下列資訊：
- 變更 MDM 授權單位期間，應該不會對使用者造成明顯影響。 
- 您不必重新設定租用戶層級原則。 
- 變更 MDM 授權單位之後，您可以從 Azure 入口網站中的 Intune 編輯租用戶層級原則。
-  在您變更 MDM 授權單位之後，請執行下列步驟以確認新裝置已成功註冊至新的授權單位：   
    - 註冊新裝置
    - 確定新註冊的裝置顯示在 Intune 中。
    - 從管理主控台對裝置執行某個動作 (例如遠端鎖定)。 如果成功，便代表該裝置已由新的 MDM 授權單位管理。
- 如果您在特定裝置上遇到問題，可以將該裝置解除註冊並重新註冊，來盡快使它們連線至新的授權單位並受到管理。
- 對於先前尚未移轉的使用者和裝置：
    - 確認裝置現在於 [裝置] 刀鋒視窗中已顯示為受管理裝置。 MDM 授權單位變更後，這些裝置必須簽入服務並完成同步處理才會顯示。 
    - 當 Intune 服務偵測到租用戶的 MDM 授權單位已變更之後，將會向所有已註冊的裝置傳送通知訊息，以要求簽入服務並進行同步處理 (有別於一般的排程簽入)。 因此，當租用戶的 MDM 授權單位從混合式變更為 Intune 獨立部署之後，所有電源已開啟並處於線上的裝置都會連線至服務，接收新的 MDM 授權單位，並從此由 Intune 獨立部署管理。 這些裝置的管理和保護將不會有任何中斷。
    - 於 MDM 授權單位變更期間 (或於結束後立即) 關閉電源或離線的裝置，將會在開啟電源並上線之後，連線至處於新 MDM 授權單位之下的服務並進行同步處理。  
    - 使用者可以透過從裝置手動啟動服務簽入，來快速變更至新的 MDM 授權單位。 使用者可以使用公司入口網站應用程式並起始裝置合規性檢查，來輕鬆完成簽入。
    - 從 MDM 授權單位變更到裝置簽入服務這段期間，裝置會有一段過渡時間是處於離線狀態。 為了協助確保裝置在此期間能獲得保護並持續運作，下列設定檔將會在裝置上保留最多 7 天 (或直到裝置與新的 MDM 授權單位連線，並接收會覆寫現有設定的新設定為止)：
        - 電子郵件設定檔
        - VPN 設定檔
        - 憑證設定檔
        - Wi-Fi 設定檔
        - 組態設定檔
    - 請連絡支援人員，以協助變更未與使用者關聯之裝置的 MDM 授權單位。 
