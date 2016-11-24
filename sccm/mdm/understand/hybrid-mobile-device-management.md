---
title: Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune
description: "了解搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理 (MDM)。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 22e673122f0f664d1240c11451b7e6db78481b26
ms.openlocfilehash: 83832465e93997a2893e024c565ee00f471036d1

---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune

*適用於：System Center Configuration Manager (最新分支)*


您可以使用 Configuration Manager 和 Microsoft Intune 管理 iOS、Windows 和 Android 裝置。 您可從 Configuration Manager 主控台來處理所有管理工作，並透過網際網路執行與 Microsoft Intune 線上服務緊密整合的其他管理工作。  您可以使用 Configuration Manager，讓使用者在其裝置上透過安全的受管理方式來存取公司資源。 使用裝置管理功能時，您可以保護公司資料，同時讓使用者能夠註冊其個人或公司擁有的裝置以便存取公司資料。 裝置管理功能：

-   淘汰或抹除裝置
-   設定包括密碼、安全性、漫遊、加密和無線通訊等相容性設定。
-   將商務營運 (LOB) 應用程式部署到裝置
-   將 App 部署到連線 Windows 市集、Windows Phone 市集、App Store 或 Google Play 的裝置。
-   收集硬體清查
-   使用內建報告來收集軟體清查

若要了解混合式 MDM 有哪些新功能，請參閱 [What's new in hybrid mobile device management](../understand/whats-new-in-hybrid-mobile-device-management.md) (混合式行動裝置管理的新功能)。

本文件假設您使用 Configuration Manager 來管理電腦，且有意搭配 Intune 來擴充 Configuration Manager 主控台以管理行動裝置。 若要了解 Intune 和混合式行動裝置管理之間的差異，請參閱 [Choose between Microsoft Intune standalone and hybrid mobile device management with System Center Configuration Manager](choose-between-standalone-intune-and-hybrid-mobile-device-management.md) (在搭配 System Center Configuration Manager 使用 Microsoft Intune 獨立或混合式行動裝置管理之間進行選擇)。

在使用 Intune 來擴充 Configuration Manager 之後，您即可註冊並管理公司擁有的裝置，或賦予使用者註冊其個人裝置的權限。 您也可以使用 Configuration Manager，搭配 Intune 來管理公司擁有的裝置。

## <a name="hybrid-mdm-enrollment"></a>混合式 MDM 註冊
若要對裝置採取混合式管理，您必須為這些裝置註冊服務。 透過裝置來進行裝置註冊的方式，取決於裝置類型、擁有權和所需的管理層級。 「自備裝置」(BYOD) 註冊方式可讓使用者註冊其個人電話、平板電腦或電腦。 公司擁有的裝置 (CYOD) 註冊方式可啟用遠端抹除、共用裝置或裝置使用者親和性這類管理案例。

 如果您使用 [Exchange ActiveSync](#mobile-device-management-with-exchange-activesync-and-configuration-manager) (不論內部部署或裝載在雲端中)，即可啟用簡單的 Intune 管理功能，而不需要註冊。 您也可以使用 [Intune 用戶端軟體](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune)來管理 Windows 電腦。

## <a name="overview-of-device-enrollment-methods"></a>裝置註冊方法概觀

 下表顯示註冊方法與支援的功能。 這些功能包括：
 - **抹除** - 將裝置重設為原廠設定，並移除所有的資料。 [淘汰裝置](../deploy-use/wipe-lock-reset-devices.md)
 - **親和性** - 將裝置與使用者相關聯。 行動應用程式管理 (MAM) 及條件式存取公司資料的必要項目。 [使用者親和性](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
 - **鎖定** - 可防止使用者移除裝置管理功能。 iOS 裝置需要處於受監管模式，才能進行鎖定。 [遠端鎖定](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

 **iOS 註冊方法**

| **方法** |  **抹除** |  **親和性**    |   **鎖定** | **詳細資料** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | 否|    [是] |   否 | [更多](../deploy-use/setup-hybrid-mdm.md#step-6-enable-platform-enrollment)|
|**[DEM](#dem)**|   否 |否 |否  | [更多](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   是 |   選擇性 |  選擇性|[更多](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| [是] |   選擇性 |  否| [更多](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Windows 和 Android 註冊方法**

| **方法** |  **抹除** |  **親和性**    |   **鎖定** | **詳細資料**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | 否|    [是] |   否 | [更多](../deploy-use/setup-hybrid-mdm.md#set-up-device-management)|
|**[DEM](#dem)**|   否 |否 |否  |[更多](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

如需可協助您判斷最佳方法的一系列問題，請參閱[選擇如何註冊行動裝置](/intune/get-started/choose-how-to-enroll-devices1)。

## <a name="byod"></a>BYOD
「自備裝置」的使用者可安裝公司入口網站應用程式，並註冊其裝置。 這可以讓使用者連線到公司網路，並加入網域或 Azure Active Directory。 針對大部分平台的許多 COD 案例，啟用 BYOD 註冊功能為必要條件。 請參閱[安裝混合式 MDM](../deploy-use/setup-hybrid-mdm.md)。 ([返回資料表](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>公司擁有的裝置
您可使用 Configuration Manager 主控台來管理公司擁有的裝置 (COD)。 iOS 裝置可以直接透過 Apple 提供的工具來進行註冊 。 系統管理員或管理員可以使用裝置註冊管理員，來註冊所有裝置類型。 您亦可將具有 IMEI 編號的裝置識別和標記為屬公司擁有，以啟用 COD 案例。

[註冊公司擁有的裝置](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>DEM
裝置註冊管理員是一種特殊的使用者帳戶，可用來註冊和管理屬公司擁有的多部裝置。 管理員可以安裝公司入口網站，並註冊多部尚無使用者的裝置。 深入了解 [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md)。 ([返回資料表](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
Apple 裝置註冊方案 (DEP) 管理功能可讓您以「無線」方式，建立原則並將其部署至透過 DEP 購買和管理的 iOS 裝置。 當使用者第一次開啟裝置並執行 iOS 設定輔助程式時，即會註冊裝置。 這個方法支援 **iOS 受監管**模式，並可啟用：
   -    鎖定的註冊
   -    條件式存取
   -    破解偵測
   -    行動應用程式管理

深入了解 [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md)。 ([返回資料表](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB-SA
USB 連接的設定輔助程式註冊。 系統管理員會建立原則，並將它匯出至 Apple Configurator。 系統會透過原則來準備已連接 USB 且公司擁有的裝置。 系統管理員必須手動註冊每部裝置。 使用者收到裝置後，可執行設定輔助程式，以註冊其裝置。 這個方法支援 **iOS 受監管**模式，並可啟用：
   -    條件式存取
   -    破解偵測
   -    行動應用程式管理

深入了解 [Setup Assistant enrollment with Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md) (使用 Apple Configurator 設定輔助程式註冊)。 ([返回資料表](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>使用 Exchange ActiveSync 和 Configuration Manager 的行動裝置管理
針對未註冊但已連接 Exchange ActiveSync (EAS) 的行動裝置，Intune 可以使用 EAS MDM 原則進行管理。 Intune 會使用 Exchange 連接器與 EAS 通訊 (不論內部部署或裝載在雲端中)。

[使用 Exchange ActiveSync 和 Intune 的行動裝置管理](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)


##  <a name="supported-device-platforms"></a>支援的裝置平台

Configuration Manager 混合式 MDM 可以管理下列裝置平台：

[!INCLUDE[../includes/mdm-supported-devices](../includes/mdm-supported-devices.md)]

## <a name="next-steps"></a>後續步驟
 - [裝置註冊的必要條件](../deploy-use/setup-hybrid-mdm.md)
 - [管理公司擁有的裝置](../deploy-use/enroll-company-owned-devices.md)



<!--HONumber=Nov16_HO1-->


