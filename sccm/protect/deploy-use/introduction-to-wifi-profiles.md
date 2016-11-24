---
title: "Wi-Fi 設定檔簡介 | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中使用 Wi-Fi 設定檔，將無線網路設定部署至組織中的使用者。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 86725460-c2f3-49ed-90aa-6b2724d34d69
caps.latest.revision: 8
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 30fefb291a6fccb630d5e3272ce7266339c9139c


---
# <a name="introduction-to-wi-fi-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Wi-Fi 設定檔簡介

適用於：System Center Configuration Manager (最新分支)

在 System Center Configuration Manager 中使用 Wi-Fi 設定檔，將無線網路設定部署至組織中的使用者。 透過部署這些設定，即可最小化連線到無線網路所需的使用者工作。  

 例如，您已安裝名稱為 **Contoso Wi-Fi**的新 Wi-Fi 網路。 您現在想要使用連線至此網路所需的設定來佈建執行 iOS 作業系統的所有裝置。 您可建立 Wi-Fi 設定檔，以包含連線至 **Contoso Wi-Fi** 無線網路所需的設定。 接著，您可以將此設定檔部署至階層中持有 iOS 裝置的所有使用者。 iOS 裝置使用者可在無線網路清單中看見公司網路，並且可直接連線至該網路。  

 您可以使用 Wi-Fi 設定檔設定下列裝置類型：  

-   執行 Windows 8.1 32 位元的裝置  

-   執行 Windows 8.1 64 位元的裝置  

-   執行 Windows RT 8.1 的裝置  

-   執行 Windows Phone 8.1 的裝置  

-   執行 Windows 10 Desktop 或 Windows 10 行動裝置版的裝置  

-   執行 iOS 5、iOS 6、iOS 7 與 iOS 8 的 iPhone 裝置  

-   執行 iOS 5、iOS 6、iOS 7 與 iOS 8 的 iPad 裝置  

-   執行第 4 版的 Android 裝置  

> [!IMPORTANT]  
>  若要將設定檔部署到 Android、iOS、Windows Phone 和已註冊的 Windows 8.1 及更新版本的裝置，必須在 Microsoft Intune 註冊這些裝置。 如需如何取得已註冊裝置的相關資訊，請參閱 [使用 Microsoft Intune 管理行動裝置](https://technet.microsoft.com/library/dn646962.aspx)。  

 建立 Wi-Fi 設定檔時，您可以加入多種安全性設定。 這些安全性設定包括使用 Configuration Manager 憑證設定檔佈建的伺服器驗證和用戶端驗證憑證。 如需憑證設定檔的詳細資訊，請參閱 [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (System Center Configuration Manager 中的憑證設定檔)。  



<!--HONumber=Nov16_HO1-->


