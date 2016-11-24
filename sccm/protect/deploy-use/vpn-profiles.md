---
title: "System Center Configuration Manager 的 VPN 設定檔 | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中使用 VPN 設定檔，將 VPN 設定部署至組織中的使用者。"
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: 6
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: dda572392884c54b63af09a9fae79c1e73eb3d95


---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 VPN 設定檔

*適用對象：System Center Configuration Manager (最新分支)*


在 System Center Configuration Manager 中使用 VPN 設定檔，將 VPN 設定部署至組織中的使用者。 透過部署這些設定，即可最小化連線到公司網路上資源所需的使用者工作。  

 例如，您想要以連線至企業網路上檔案共用所需的設定佈建所有執行 iOS 作業系統的裝置。 您可以建立含有連線至企業網路所需設定的 VPN 設定檔，然後將此設定檔部署至階層中所有擁有執行 iOS 之裝置的使用者。 iOS 裝置的使用者會看見可用網路清單中的 VPN 連線，並且可以輕鬆連線至此網路。  

 當您建立 VPN 設定檔時，您可以在其中加入各種安全性設定，包括藉由使用 System Center Configuration Manager 憑證設定檔佈建的伺服器驗證憑證和用戶端驗證憑證。 如需憑證設定檔的詳細資訊，請參閱 [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (System Center Configuration Manager 中的憑證設定檔)。  

 下列各節會說明如果使用 Configuration Manager 或 Configuration Manager 搭配 Microsoft Intune，可用 VPN 設定檔設定哪些裝置。  

## <a name="vpn-profiles-when-using-configuration-manager"></a>使用 Configuration Manager 時的 VPN 設定檔  
 下表說明針對不同裝置平台可以設定的 VPN 設定檔。  

|連線類型|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|否|否|否|否|  
|**Pulse Secure**|是|否|是|是|  
|**F5 Edge Client**|[是]|否|是|是|  
|**Dell SonicWALL Mobile Connect**|[是]|否|是|[是]|  
|**Check Point Mobile VPN**|是|否|是|是|  
|**Microsoft SSL (SSTP)**|是|[是]|是|否|  
|**Microsoft Automatic**|是|[是]|是|否|  
|**IKEv2**|是|[是]|是|否|  
|**PPTP**|是|[是]|是|否|  
|**L2TP**|是|[是]|是|否|  

## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>使用 Configuration Manager 和 Intune 時的 VPN 設定檔  
 若要將設定檔部署到 iOS、Android、Windows Phone 和 Windows 8.1 裝置，這些裝置必須在 Microsoft Intune 註冊。 其他平台上的裝置也可以註冊至 Intune。 如需如何註冊的資訊，請參閱[註冊裝置以在 Intune 中管理](https://technet.microsoft.com/en-us/library/dn646962.aspx)。 本表顯示各裝置平台支援的連線類型︰  

|連線類型|iOS 與 Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop 與行動裝置版|  
|---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
|Cisco AnyConnect|是|是|否|否|否|否|是 (OMA-URI)|  
|Pulse Secure|是|[是]|是|否|是|[是]|是|  
|F5 Edge Client|是|[是]|是|否|是|[是]|是|  
|Dell SonicWALL Mobile Connect|是|[是]|是|否|是|[是]|是|  
|檢查點行動 VPN|是|[是]|是|否|是|[是]|是|  
|Microsoft SSL (SSTP)|否|否|是|[是]|是|否|否|  
|Microsoft Automatic|否|否|是|[是]|是|否|是 (OMA-URI)|  
|IKEv2|是 (自訂原則)|否|是|[是]|[是]|是|是 (OMA-URI)|  
|PPTP|是|否|是|[是]|是|否|是 (OMA-URI)|  
|L2TP|是|否|是|[是]|是|否|是 (OMA-URI)|  

### <a name="next-steps"></a>後續步驟  
 使用下列主題可協助您規劃、設定、操作及維護 Configuration Manager 中的 VPN 設定檔。  

-   [System Center Configuration Manager 中的 VPN 設定檔必要條件](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [System Center Configuration Manager 中的 VPN 設定檔安全性及隱私權](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)



<!--HONumber=Nov16_HO1-->


