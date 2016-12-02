---
title: Endpoint Protection | System Center Configuration Manager
description: "了解如何管理 Configuration Manager 階層中用戶端電腦的反惡意程式碼原則和 Windows 防火牆安全性。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: 11
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 30ac6f2ec03a4c0d50de700f9ce77f9e50eaf1e0


---
# <a name="endpoint-protection-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Endpoint Protection

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的 Endpoint Protection 可讓您管理 Configuration Manager 階層中用戶端電腦的反惡意程式碼原則和 Windows 防火牆安全性。  

> [!IMPORTANT]  
>  您必須獲授權才能使用 Endpoint Protection 管理 Configuration Manager 階層中的用戶端。  

 搭配使用 Endpoint Protection 與 Configuration Manager 時，具有下列優點：  

-   設定所選電腦群組的反惡意程式碼原則和 Windows 防火牆設定，以及管理其 Windows Defender 進階威脅防護  

-   使用 Configuration Manager 軟體更新來下載最新的反惡意程式碼定義檔，讓用戶端電腦保持最新狀態  

-   傳送電子郵件通知、使用主控台內監視，以及檢視報告，以在用戶端電腦上偵測到惡意程式碼時通知系統管理使用者。  

Windows 10 電腦不需要任何其他用戶端來進行 Endpoint Protection 管理。 在 Windows 8.1 和舊版的電腦上，Endpoint Protection 除了 Configuration Manager 用戶端之外還會安裝自己的用戶端。 Endpoint Protection 可以管理。 Endpoint Protection 用戶端具有下列功能：  

-   惡意程式碼和間諜軟體的偵測與補救  

-   Rootkit 偵測與補救  

-   重大漏洞評估以及自動定義和引擎更新  

-   透過網路檢查系統的網路漏洞偵測  

-   與雲端保護服務整合，以向 Microsoft 報告惡意程式碼。 當您加入這項服務時，如果在電腦上偵測到無法識別的惡意程式碼，則 Endpoint Protection 用戶端或 Windows Defender 可以從惡意程式碼防護中心下載最新定義。  

> [!NOTE]  
>  Endpoint Protection 用戶端可以安裝在執行 Hyper-V 的伺服器上，以及具有所支援作業系統的客體虛擬機器上。 為了避免占用過多的 CPU 使用量，Endpoint Protection 動作具有內建隨機延遲，可使保護服務不會同時執行。  

 此外，Configuration Manager 中的 Endpoint Protection 可讓您在 Configuration Manager 主控台中管理 Windows 防火牆設定。  

 [範例案例：使用 System Center Endpoint Protection 保護電腦免受 System Center Configuration Manager 中惡意程式碼的威脅](scenarios-endpoint-protection.md) Endpoint Protection 和 Windows 防火牆。  


## <a name="managing-malware-with-endpoint-protection"></a>使用 Endpoint Protection 管理惡意程式碼  
 Configuration Manager 中的 Endpoint Protection 可讓您建立包含 Endpoint Protection 用戶端設定的反惡意程式碼原則。 您接著可以將這些反惡意程式碼原則部署至用戶端電腦，並在 [監視] 工作區的 [Endpoint Protection 狀態] 節點中加以監視，或透過使用 Configuration Manager 報告。  

 其他資訊：  

-   [如何在 System Center Configuration Manager 中建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md) - 使用您可以設定的設定清單，來建立、部署和監視反惡意程式碼原則的設定。  

-   [如何在 System Center Configuration Manager 中監視 Endpoint Protection](monitor-endpoint-protection.md) - 監視活動報告、受感染的用戶端電腦等。  

-   [如何在 System Center Configuration Manager 中管理 Endpoint Protection 的反惡意程式碼原則及防火牆設定](endpoint-antimalware-firewall.md) - 補救用戶端電腦上找到的惡意程式碼。  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>使用 Endpoint Protection 管理 Windows 防火牆  
 Configuration Manager 中的 Endpoint Protection 提供用戶端電腦上的 Windows 防火牆基本管理。 針對每個網路設定檔，您可以設定下列設定：  

-   啟用或停用 Windows 防火牆。  

-   阻擋連入連線 (包括允許之程式清單中的連線)。  

-   當 Windows 防火牆阻擋新程式時通知使用者。  

> [!NOTE]  
>  Endpoint Protection 僅支援管理 Windows 防火牆。  


 如需如何建立和部署 Endpoint Protection 之 Windows 防火牆原則的詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立和部署 Endpoint Protection 的 Windows 防火牆原則](create-windows-firewall-policies.md)。  


## <a name="windows-defender-advanced-threat-protection"></a>Windows Defender 進階威脅防護

從 Configuration Manager 1606 版 (最新分支) 開始，Endpoint Protection 可以協助管理和監視 Windows Defender 進階威脅防護 (ATP)。 Windows Defender ATP 是新的服務，可協助企業偵測、調查和回應其網路的進階攻擊。 [Windows Defender 進階威脅防護](windows-defender-advanced-threat-protection.md)。

## <a name="endpoint-protection-workflow"></a>Endpoint Protection 工作流程  
 下圖可協助您了解在 Configuration Manager 階層中實作 Endpoint Protection 的工作流程。  

 ![Endpoint Protection 工作流程](../media/Endpoint-Protection-Workflow.gif)  

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>適用於 Mac 電腦和 Linux 伺服器的 Endpoint Protection 用戶端  
 System Center Endpoint Protection 包含適用於 Linux 和 Mac 電腦的 Endpoint Protection 用戶端。 Configuration Manager 未隨附這些用戶端；您必須改由 [Microsoft 大量授權服務中心](https://www.microsoft.com/licensing/servicecenter/default.aspx)下載下列產品。  

-   適用於 Mac 的 System Center 2012 Endpoint Protection  

-   適用於 Linux 的 System Center 2012 Endpoint Protection  


> [!IMPORTANT]  
>  您必須是 Microsoft 大量授權客戶，才能下載適用於 Linux 和 Mac 的 Endpoint Protection 安裝檔案。  

 這些產品無法從 Configuration Manager 主控台進行管理。 不過，安裝檔案隨附 System Center Operations Manager 管理組件，可讓您使用 Operations Manager 來管理適用於 Linux 的用戶端。  

 如需如何安裝和管理適用於 Linux 和 Mac 電腦之 Endpoint Protection 用戶端的詳細資訊，請使用這些產品隨附的文件 (位於 [文件]  資料夾中)。



<!--HONumber=Nov16_HO1-->

