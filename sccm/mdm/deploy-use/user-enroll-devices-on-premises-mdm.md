---
title: "使用者如何在 System Center Configuration Manager 中使用內部部署行動裝置管理註冊裝置"
description: "了解使用者如何在 System Center Configuration Manager 中使用內部部署行動裝置管理註冊裝置。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e390da9377adfb7f32687c6c01b35a51a3bd495b


---
# <a name="how-users-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>使用者如何在 System Center Configuration Manager 中使用內部部署行動裝置管理註冊裝置

*適用對象：System Center Configuration Manager (最新分支)*

使用 System Center Configuration Manager 內部部署行動裝置管理時，如果使用者已獲得註冊權限 (透過更新用戶端設定)，而且其裝置已安裝必要的根憑證，可與裝載所需站台系統角色的伺服器進行信任通訊，則使用者就可以註冊裝置。 如需如何設定註冊的詳細資訊，請參閱 [Set up device enrollment for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md) (設定 System Center Configuration Manager 中內部部署行動裝置管理的裝置註冊)。  

 > [!NOTE]  
>  Configuration Manager 的最新分支，支援執行下列作業系統的裝置在內部部署行動裝置管理中註冊︰  
>   
>  -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 團隊版 \(從 Configuration Manager 1602 版開始\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise

下列工作說明如何為內部部署行動裝置管理註冊及驗證電腦和裝置的註冊：  

-   [註冊 Windows 10 電腦](#bkmk_enrollDesk)  

-   [註冊 Windows 10 行動裝置](#bkmk_enrollMob)  

-   [確認裝置註冊與否](#bkmk_verify)  

##  <a name="a-namebkmkenrolldeska-enroll-a-windows-10-computer"></a><a name="bkmk_enrollDesk"></a> 註冊 Windows 10 電腦  

1.  在 Windows 10 電腦上，移至 [設定] 。  

2.  依序按一下 [帳戶] 以及 [公司存取] 。  

3.  在 [連線到公司或學校] 下的 [公司存取] 中，按一下 [連線] ，輸入您的公司電子郵件地址，然後按一下 [繼續] 。  

4.  輸入裝載註冊 Proxy 點站台系統角色的伺服器 FQDN，然後按一下 [繼續]。  

5.  在 [正在連線至服務] 中，輸入您公司電子郵件的密碼，然後按一下 [登入] 。  

6.  按一下 [略過]  以記憶登入資訊，接著經過一小段時間後，裝置即完成連線。  

##  <a name="a-namebkmkenrollmoba-enroll-a-windows-10-mobile-device"></a><a name="bkmk_enrollMob"></a> 註冊 Windows 10 行動裝置  

1.  在 Windows 10 行動裝置上，請移至 [設定] 。  

2.  依序按一下 [帳戶] 以及 [公司存取] 。  

3.  按一下 **[Connect]**(連線)。  

4.  輸入您的公司電子郵件地址，以及裝載註冊 Proxy 點站台系統角色的伺服器 FQDN。 按一下 **[Connect]**(連線)。  

5.  在下一個畫面中，輸入您的公司電子郵件地址和密碼，然後按一下 [登入] 。 經過一小段時間之後，裝置即完成註冊。 按一下 [完成] 。  

##  <a name="a-namebkmkverifya-verify-device-enrollment"></a><a name="bkmk_verify"></a> 確認裝置註冊與否  
 您可以在 Configuration Manager 主控台確認裝置已成功註冊。  

1.  啟動 Configuration Manager 主控台。  

2.  按一下 [關閉]  >  > 的站台系統角色之間進行信任通訊時，需要這個根憑證。 註冊的裝置會出現在清單中。  

## <a name="see-also"></a>另請參閱  
 [Enroll devices for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md) (在 System Center Configuration Manager 中註冊裝置以進行內部部署行動裝置管理)



<!--HONumber=Nov16_HO1-->


