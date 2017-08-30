---
title: "支援的用戶端和裝置 | Microsoft Docs"
description: "了解 System Center Configuration Manager 支援用於用戶端和裝置的作業系統。"
ms.custom: na
ms.date: 8/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
caps.latest.revision: "5"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: f9dd3b3e8f7a2878cd549bf289e1ee5536ee73fc
ms.sourcegitcommit: 974fbc4408028c8be28911e5cd646efcf47c7f15
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="supported-operating-systems-for-clients-and-devices-for-system-center-configuration-manager"></a>System Center Configuration Manager 用戶端和裝置支援的作業系統

*適用於：System Center Configuration Manager (最新分支)*


 System Center Configuration Manager 支援在各種 Windows、Mac、Linux 與 UNIX 電腦上安裝用戶端軟體。  

 **所有用戶端的需求和限制：**  

-   不支援變更任何 Configuration Manager 服務的啟動類型或 [登入身分] 設定，這麼做可能會導致重要服務無法正確執行。    

-   不支援在使用非根帳號的電腦上，安裝或執行 Linux 或 UNIX 的 Configuration Manager 用戶端或 Mac 用戶端。 這麼做可能會導致重要服務無法正確執行。  

##  <a name="windows-computers"></a>Windows 電腦  
 您可以使用 Configuration Manager 所含的 Configuration Manager 用戶端來管理下列 Windows 作業系統。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)。  

**支援的作業系統：**  


-  **Windows Server 2016**：Standard、Datacenter <sup>1</sup>
  - 從具有 KB3186654 之 Hotfix 彙總套件的 Configuration Manager 1606 版 (或 2016 年 10 月發行的基準版本 1606) 開始，支援此作業系統。  

-   **Windows Server 2012 R2** (x64)：Standard、Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64)：Standard、Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 (含 SP1)** (x64)：Standard、Enterprise、Datacenter <sup>1</sup>    

-   **Windows Storage Server 2008 R2** (x86、x64)：Workgroup、Standard、Enterprise    

-   **Windows Server 2008 (含 SP2)** (x86、x64)：Standard、Enterprise、Datacenter <sup>1</sup>    

-   **Windows 10** 如需不同 Configuration Manager 版本所支援不同 Windows 10 發行版本的詳細資料，請參閱 [Windows 10 版本支援](/sccm/core/plan-design/configs/support-for-windows-10)。

-   **Windows 8.1** (x86、x64)：專業版、企業版    

-   **Windows 8.1** (x86、x64)：專業版、企業版    

-   **Windows 7 (含 SP1)** (x86、x64)：專業版、企業版和旗艦版    

-   **Windows Server 2016 的伺服器核心安裝** (x64) <sup>2</sup>
  - 從具有 KB3186654 之 Hotfix 彙總套件的 1606 版 (或 2016 年 10 月發行的基準版本 1606) 開始，支援此作業系統。


-   **Windows Server 2012 R2 的 Server Core 安裝** (x64) <sup>2</sup>    

-   **Windows Server 2012 的 Server Core 安裝** (x64) <sup>2</sup>    

-   **Windows Server 2008 R2 的 Server Core 安裝**  
    **(無 Service Pack 或含 SP1)** (x64)    

-   **Windows Server 2008 SP2 的 Server Core 安裝** (x86、x64)  

 <sup>1</sup> Datacenter 版本受到支援，但未經 Configuration Manager 認證。 Windows Server Datacenter Edition 的特定問題沒有 Hotfix 支援。  

 <sup>2</sup> 為了支援用戶端推入安裝，執行此作業系統版本的電腦必須執行檔案和存放服務伺服器角色的檔案伺服器角色服務。 如需在 Server Core 電腦上安裝 Windows 功能的相關資訊，請參閱 Windows Server 2012 TechNet 文件庫中的[在 Server Core 伺服器上安裝伺服器角色和功能](http://go.microsoft.com/fwlink/p/?LinkId=299359)。  


##  <a name="windows-embedded-computers"></a>Windows Embedded 電腦  
 您可以藉由在裝置上安裝 Configuration Manager 用戶端軟體來管理 Windows Embedded 裝置。  如需詳細資訊，請參閱[規劃將用戶端部署至 System Center Configuration Manager 中的 Windows Embedded 裝置](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)。  

**需求和限制：**  

-   在未啟用寫入篩選器的 Windows Embedded 系統上，會支援用戶端的所有功能。  

-   針對所有功能 (電源管理除外)，支援使用下列其中一項的用戶端：  

    -   增強式寫入篩選器 (EWF)    

    -   RAM 檔案型寫入篩選器 (FBWF)    

    -   整合寫入篩選器 (UWF)  

-   所有 Windows Embedded 裝置都不支援應用程式類別目錄。  

-   您必須先在裝置上安裝 Microsoft Windows WMI 指令碼套件，才能在以 Windows XP 為基礎的 Windows Embedded 裝置上監視偵測到的惡意程式碼。 使用 Windows Embedded Target Designer 安裝這個封裝。
**WBEMDISP.DLL** 和 **WBEMDISP.TLB** 檔案必須存在，且在內嵌裝置的 **%windir%\System32\WBEM** 資料夾中註冊，以確保會報告偵測到的惡意程式碼。  

**支援的作業系統：**  

-   **Windows 10 企業版** (x86、x64)  

-   **Windows 10 IoT 企業版** (x86、x64)  

-   **Windows Embedded 8.1 Industry** (x86、x64)    

-   **Windows Embedded 8 Industry** (x86、x64)    

-   **Windows Embedded 8 Standard** (x86、x64)    

-   **Windows Embedded 8 Pro** (x86、x64)    

-   **Windows Thin PC** (x86、x64)    

-   **Windows Embedded POSReady 7** (x86、x64)    

-   **Windows Embedded Standard 7 (含 SP1)** (x86、x64)    

下列作業系統是以 Windows XP Embedded 為基礎，因此只有 Configuration Manager 1610 版與更新版本才支援。 [從 1702 版開始，就不再支援這些嵌入式作業系統](/sccm/core/plan-design/changes/removed-and-deprecated-features#client-operating-systems)。  

-   **WEPOS 1.1 (含 SP3)** (x86)    

-   **Windows Embedded POSReady 2009** (x86)    

-   **Windows Fundamentals for Legacy PCs (WinFLP)** (x86)    

-   **Windows XP Embedded SP3** (x86)    

-   **Windows Embedded Standard 2009** (x86)  

## <a name="windows-ce-computers"></a>Windows CE 電腦
 您可以使用 Configuration Manager 包含的舊版 Configuration Manager 行動裝置用戶端來管理 Windows CE 裝置。  

**需求和限制**  

-   行動裝置用戶端需要 0.78 MB 的儲存空間來安裝。 登入可能需要最多 256 KB 的額外儲存空間。    

-   這些行動裝置的功能因平台和用戶端類型而異。 如需支援之管理功能的資訊，請參閱[選擇 System Center Configuration Manager 的裝置管理解決方案](../../../core/plan-design/choose-a-device-management-solution.md)。  

**支援的作業系統：**  

-   Windows CE 7.0 (ARM 和 x86 處理器)  

**支援的語言包括：**  

-   中文 (簡體及繁體)    

-   英文 (美國)    

-   法文 (法國)    

-   德文    

-   義大利文    

-   日文  

-   韓文  

-   葡萄牙文 (巴西)  

-   俄文  

-   西班牙文 (西班牙)  

## <a name="mac-computers"></a>Mac 電腦  
 您可以使用適用於 Mac 的 Configuration Manager 用戶端管理 Mac OS X 電腦。  

 Configuration Manager 媒體不提供 Mac 用戶端安裝套件。 從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkID=525184)下載**其他作業系統的用戶端**。  

 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Mac](../../../core/clients/deploy/deploy-clients-to-macs.md)。  

**支援的版本：**  

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra )

##  <a name="linux-and-unix-servers"></a>Linux 和 UNIX 伺服器  
 您可以使用適用於 Linux 和 UNIX 的 Configuration Manager 用戶端管理 Linux 和 UNIX 電腦。  

 Configuration Manager 媒體不提供 Linux 和 UNIX 用戶端安裝套件。 從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkID=525184)下載**其他作業系統的用戶端**。 除了用戶端安裝套件之外，用戶端下載還會包括管理每部電腦上用戶端安裝的指令碼。  

**需求和限制：**  

-   若要檢閱 Linux 和 UNIX 用戶端的作業系統檔案相依性，請參閱[將用戶端部署至 Linux 和 UNIX 伺服器的必要條件](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU)。  

-   如需 Linux 或 UNIX 支援的管理功能概觀，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 UNIX 和 Linux 伺服器](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)。  

-   如需支援的 Linux 和 UNIX 版本，列出的版本會包含所有後續的次要版本。 例如，CentOS 第 6 版包括 CentOS 6.3。 同樣地，使用 Service Pack (例如 SUSE Linux Enterprise Server 11 SP1) 的作業系統支援會包含該作業系統版本的後續 Service Pack。  

-   如需用戶端安裝套件和 Universal Agent 的相關資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 UNIX 和 Linux 伺服器](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)。  

**支援的版本：**使用指定的 .tar 檔案支援下列版本。  

### <a name="aix"></a>AIX  

|||  
|-|-|  
|5.3 版 (Power)|ccm-Aix53ppc.&lt;組建\>.tar|  
|6.1 版 (Power)|ccm-Aix61ppc.&lt;組建\>.tar|  
|7.1 版 (Power)|ccm-Aix71ppc.&lt;組建\>.tar|  

### <a name="centos"></a>CentOS  

|||  
|-|-|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

### <a name="debian"></a>Debian  

|||  
|-|-|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 8 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 8 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|||  
|-|-|  
|11iv2 版 IA64|ccm-HpuxB.11.23i64.&lt;組建\>.tar|  
|11iv2 版 PA-RISC|ccm-HpuxB.11.23PA.&lt;組建\>.tar|  
|11iv3 版 IA64|ccm-HpuxB.11.31i64.&lt;組建\>.tar|  
|11iv3 版 PA-RISC|ccm-HpuxB.11.31PA.&lt;組建\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|||  
|-|-|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|||  
|-|-|  
|第 4 版 x86|ccm-RHEL4x86.&lt;組建\>.tar|  
|第 4 版 x64|ccm-RHEL4x64.&lt;組建\>.tar|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

### <a name="solaris"></a>Solaris  

|||  
|-|-|  
|第 9 版 SPARC|ccm-Sol9sparc.&lt;組建\>.tar|  
|第 10 版 x86|ccm-Sol10x86.&lt;組建\>.tar|  
|第 10 版 SPARC|ccm-Sol10sparc.&lt;組建\>.tar|  
|第 11 版 x86|ccm-Sol11x86.&lt;組建\>.tar|  
|第 11 版 SPARC|ccm-Sol11sparc.&lt;組建\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|||  
|-|-|  
|第 9 版 x86|ccm-SLES9x86.&lt;組建\>.tar|  
|第 10 版 SP1 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 10 版 SP1 x86|ccm-Universalx64.&lt;組建\>.tar|  
|第 11 版 SP1 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 11 版 SP1 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 12 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|||  
|-|-|  
|10.04 版 LTS x86|ccm-Universalx86.&lt;組建\>.tar|  
|10.04 版 LTS x64|ccm-Universalx64.&lt;組建\>.tar|  
|12.04 版 LTS x86|ccm-Universalx86.&lt;組建\>.tar|  
|12.04 版 LTS x64|ccm-Universalx64.&lt;組建\>.tar|  
|14.04 版 LTS x86|ccm-Universalx86.&lt;組建\>.tar|  
|14.04 版 LTS x64|ccm-Universalx64.&lt;版本\>.tar|  

##  <a name="mobile-devices-enrolled-by-microsoft-intune"></a>由 Microsoft Intune 註冊的行動裝置  
 如需您整合 Microsoft Intune 與 Configuration Manager 時可以管理之電腦與裝置的詳細資訊，請參閱 Microsoft Intune 文件庫中的下列兩個主題：  

-   [Microsoft Intune 的行動裝置管理功能](https://docs.microsoft.com/intune/get-started/choose-how-to-manage-devices)  
-   [Microsoft Intune 的 Windows 電腦管理功能](https://docs.microsoft.com/intune/get-started/windows-pc-management-capabilities-in-microsoft-intune)  

##  <a name="bkmk_OnpremOS"></a> 內部部署行動裝置管理  
 Configuration Manager 具有內建功能，以管理內部部署的裝置，而不需要安裝用戶端軟體。  如需詳細資訊，請參閱[在 System Center Configuration Manager 中使用內部部署基礎結構管理行動裝置](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

 **需求和限制：**  

-   您必須在階層的頂層站台設定**服務連接點**。  

**支援的作業系統：**  

- **Windows 10 專業版** (x86、x64)  

- **Windows 10 專業企業版** (x86、x64)  

- **Windows 10 IoT 企業版** (x86、x64)

- **Windows 10 行動裝置版**  

- **Windows 10 行動裝置企業版**  

- **Windows 10 IoT 行動裝置企業版**

- **適用於 Surface Hub 的 Windows 10 團隊版**

##  <a name="bkmk_ExSrvConOS"></a> Exchange Server 連接器  
Configuration Manager 支援有限制地管理連線至您 Exchange Server 的裝置，而不需要安裝 Configuration Manager 用戶端。 如需詳細資訊，請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

 **需求和限制：**  

-   當您使用具備適用於 Exchange Active Sync 之 Exchange Server 連接器的裝置，且該裝置連線到執行 Exchange Server 或 Exchange Online 的伺服器時，Configuration Manager 提供有限的行動裝置管理。  

-   如需 Configuration Manager 針對 Exchange Server 連接器所管理之行動裝置支援的管理功能詳細資訊，請參閱＜判斷如何在 Configuration Manager 中管理行動裝置＞。  

**支援的 Exchange Server 版本：**  

-   **Exchange Server 2010 SP1**  

-   **Exchange Server 2010 SP2**  

-   **Exchange Server 2013**  

-   **Exchange Online (Office 365)**：這包括 Business Productivity Online Standard Suite  
