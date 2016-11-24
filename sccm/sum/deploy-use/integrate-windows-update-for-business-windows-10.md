---

title: "與 Windows 10 中的 Windows Update for Business 整合 | Configuration Manager"
description: "針對連線到 Windows Update 服務的裝置，您可以使用 Windows Update for Business 讓組織中的 Windows 10 裝置保持最新狀態。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c4c6e50d0e1a34653226369cffdc0bde905398fc


---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>與 Windows 10 中的 Windows Update for Business 整合

*適用於：System Center Configuration Manager (最新分支)*

商務用 Windows Update (WUfB) 可讓您組織中的 Windows 10 裝置直接連接到 Windows Update (WU) 服務，永遠掌握最新的安全性防禦措施及 Windows 功能。 Configuration Manager 能夠區分使用 WUfB 及 WSUS 取得軟體更新的 Windows 10 電腦。  

 將 Configuration Manager 用戶端設定為從 WU (包括 WUfB 或 Windows 測試人員) 接收更新時，某些 Configuration Manager 功能便無法再使用：  

-   Windows Update 相容性報告：  

    -   Configuration Manager 不會察覺發佈到 WU 的更新。 設定為從 WU 接收更新的 Configuration Manager 用戶端會將 Configuration Manager 主控台中的更新顯示為 [不明]。  

    -   整體相容性狀態的疑難排解很困難，原因是 [不明]  狀態以往僅供尚未從 WSUS 回報掃描狀態的用戶端使用。  現在則也包含從 WU 接收更新的 Configuration Manager 用戶端。  

    -   從 WU 接收更新的用戶端將無法正常使用建基於更新相容性狀態的條件式存取 (用於公司資源)，原因是其永遠無法符合 Configuration Manager 的相容性。  

    -   定義更新相容性是整體更新相容性報告的一部分，而且也無法正常運作。  定義更新相容性也是條件存取評估的一部分。  

-   建基於更新相容性狀態之 Defender 的整體 Endpoint Protection 報告由於缺少掃描資料，而不會傳回精確的結果。  

-   如果用戶端是連接 WUfB 以接收更新，Configuration Manager 就無法將 Office、IE 以及 Visual Studio 這類 Microsoft 更新部署到該用戶端。  

-   如果用戶端是連接 WUfB 以接收更新，Configuration Manager 就無法將協力廠商更新 (發行至 WSUS 且透過 Configuration Manager 管理) 部署到該用戶端。  

-   使用軟體更新基礎結構的 Configuration Manager 完整用戶端部署，將不適用於連接 WUfB 以接收更新的用戶端。  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>識別使用 WUfB 進行 Windows 10 更新的用戶端  
 使用下列程序來識別使用 WUfB 取得 Windows 10 更新和升級的用戶端、將這些用戶端設定為停止使用 WSUS 取得更新，並部署用戶端代理程式設定以停用這些用戶端的軟體更新工作流程。  

 **先決條件**  

-   執行 Windows 10 Desktop Pro 或 Windows 10 Enterprise Edition 1511 版或更新版本的用戶端  

-   [商務用 Windows Update](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) 已部署，且用戶端使用 WUfB 取得 Windows 10 更新及升級。  

#### <a name="to-identify-clients-that-use-wufb"></a>識別使用 WUfB 的用戶端  

1.  如果之前已啟用 Windows Update 代理程式，請予停用以免對 WSUS 進行掃描。   
    您可以設定登錄機碼 **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**，指出電腦要執行 WSUS 或 Windows Update 掃描。  當值為 2 時，它不會執行 WSUS 掃描。  

2.  在 Configuration Manager 資源總管的 [Windows Update] 節點下，有個新屬性 **UseWUServer**。  

3.  根據透過 WUfB 連線之所有電腦的 **UseWUServer** 屬性，建立要更新和升級的集合。  

4.  建立用戶端代理程式設定，以停用軟體更新工作流程，並將設定部署至直接連線到 WUfB 的電腦集合。  

5.  透過 WUfB 管理的電腦會在相容性狀態中顯示 [不明]，而且不會計入整體相容性百分比的一部分。  



<!--HONumber=Nov16_HO1-->


