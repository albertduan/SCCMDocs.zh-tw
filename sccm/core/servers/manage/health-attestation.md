---
title: "健全狀況證明 | Microsoft Docs"
description: "深入了解可在 Configuration Manager 主控台中檢視的裝置健全狀況證明功能。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: 17
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: cb42b6f324dc0019c2109be4d91e0eab4dca4d70
ms.openlocfilehash: 9d88e93c1382d5804598f2db258f325954e328b1
ms.lasthandoff: 03/08/2017


---
# <a name="health-attestation-for-system-center-configuration-manager"></a>System Center Configuration Manager 的健康情況證明

*適用於：System Center Configuration Manager (最新分支)*

系統管理員可以在 Configuration Manager 主控台內檢視 [Windows 10 裝置健康情況證明](https://technet.microsoft.com/library/mt592023.aspx)的狀態。  由 Configuration Manager 管理的電腦和內部部署資源，以及透過 Microsoft Intune 管理的行動裝置，皆可使用這項功能。 系統管理員可以指定要透過雲端還是內部部署基礎結構來執行報告。 這麼一來，無法存取網際網路的用戶端電腦即可使用健康情況證明，來啟用和管理裝置。 系統管理員可透過裝置健康情況證明，確認用戶端電腦已啟用下列可信任的 BIOS、TPM 及開機軟體設定：  

-   開機初期啟動的反惡意程式碼 - 開機初期啟動的反惡意程式碼 (ELAM) 可在您電腦啟動時且在其他廠商驅動程式初始化之前，為它提供保護。 [如何開啟 ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker -「Windows BitLocker 磁碟機加密」是一種軟體，可讓您將存放在 Windows 作業系統磁碟區上的所有資料都加密。  [如何開啟 BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   安全開機 -「安全開機」是由電腦產業成員所開發的一種安全標準，可協助確保您的電腦只使用電腦製造商信任的軟體來開機。 [深入了解安全開機](https://technet.microsoft.com/library/hh824987.aspx)  
-   程式碼完整性 -「程式碼完整性」是一項功能，可藉由在每次將驅動程式或系統檔案載入記憶體時驗證其完整性，改進作業系統的安全性。 [深入了解程式碼完整性](https://technet.microsoft.com/library/dd348642.aspx)  


##  <a name="device-health-attestation"></a>裝置健全狀況證明  
 Configuration Manager 的裝置健康情況證明會顯示下列各項資訊：  

-   **健康情況證明狀態** - 顯示處於相容、不相容、錯誤及不明狀態的裝置比例  
-   **回報健康情況證明的裝置** - 顯示回報「健康情況證明」狀態的裝置百分比  
-   **不相容的裝置 (依用戶端類型)** - 顯示不相容之行動裝置和電腦的比例  
-   **遺失的前幾項健康情況證明設定** - 顯示遺漏健康情況證明設定的裝置數目 (依每個設定列出)  

 **需求：**  

-   執行 Win10 的用戶端裝置  
-   Windows Server 2016 ([已啟用裝置健康情況證明](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation))
-    已啟用 TPM 2  
-   解除封鎖 Configuration Manager 用戶端代理程式和 has.spserv.microsoft.com (連接埠 443) 健全狀況證明服務之間的通訊

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>如何在 Configuration Manager 用戶端電腦上啟用健康情況證明服務通訊  

1.  在 Configuration Manager 主控台中，選擇 **[系統管理]** > **[概觀]** > **[用戶端設定]**。  選取 **[電腦代理程式]** 設定索引標籤。  

2.  在 **[預設設定]** 對話方塊中，選取 **[電腦代理程式]** ，然後向下捲動到 **[啟用與健康情況證明服務之間的通訊]**。  

3.  將 **[啟用與健康情況證明服務之間的通訊]** 設定為 **[是]**，然後按一下 **[確定]**。  

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>如何在 Configuration Manager 用戶端電腦上啟用內部部署健康情況證明服務通訊


1. 在 Configuration Manager 主控台中，瀏覽至 **[系統管理]** > **[概觀]** > **[用戶端設定]**，然後將 **[使用內部部署健康情況證明服務]** 設定為 **[是]**。


2. 指定 **[內部部署健康情況證明服務 URL]**，然後按一下 **[確定]**。

## <a name="how-to-view-health-attestation"></a>如何檢視健康情況證明  


1.  若要檢視裝置健康情況證明檢視，請在 Configuration Manager 主控台中，移至 **[監視]** 工作區，按一下 **[安全性]** 節點，然後按一下 **[健康情況證明]**。  

2.  隨即會顯示「裝置健康情況證明」。  

 用戶端裝置「健康情況證明」狀態可用來定義由搭配 Microsoft Intune 的 Configuration Manager 所管理之裝置的合規性原則中的條件式存取規則。 如需詳細資訊，請參閱[管理 System Center Configuration Manager 中的裝置相容性原則](/sccm/protect/deploy-use/device-compliance-policies)。  

