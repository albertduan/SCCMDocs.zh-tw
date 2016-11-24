---
title: "選擇 Intune 獨立部署或混合式 MDM | System Center Configuration Manager"
description: "選擇要部署使用 Intune 和 Configuration Manager 的混合式行動裝置管理，還是要執行 Intune 獨立部署。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2e6ec1b2b822298d4fa6a17e2d7439167b83080a

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>在 Microsoft Intune 獨立部署與使用 System Center Configuration Manager 的混合式行動裝置管理之間進行選擇

適用於：System Center Configuration Manager (最新分支)

使用 Microsoft Intune 進行行動裝置管理 (MDM) 時，最常詢問的其中一個問題就是：「我應該部署使用 Intune 和 Configuration Manager 的混合式 MDM，還是在僅限雲端的設定中執行 Intune 獨立部署？」 這是一個重要決定，而且實作後無法輕易變更。  

 Intune 獨立部署不需要任何內部部署基礎結構，而是透過 Web 主控台進行管理。 它是敏捷式輕量型部署，廣受雲端優先組織的熱愛。  

 混合式 MDM 部署需要 Intune 和 Configuration Manager，並使用經驗豐富的 Configuration Manager 系統管理員熟悉的工具進行管理。 它提供 MDM 和傳統用戶端的「單一整合」(Single Pane of Glass) 管理，並具有在大型環境中執行的規模。  

##  <a name="what-does-intune-standalone-mean"></a>什麼是 Intune 獨立部署？  
 Intune 的核心是雲端服務。 北美洲、歐洲和亞洲都有託管的 Intune Datacenter，以為行動裝置提供安全性原則、電子郵件和 Wi-Fi 設定檔、應用程式、清查等等。  

 Intune 獨立實作不需要任何內部部署基礎結構。 所有設定、管理、部署和報告都是透過 Web 主控台執行，因此可從世界任何地方存取。  

 為了使用 Microsoft Exchange 和網路裝置註冊服務 (NDES) 等內部部署應用程式，還提供內部部署連接器以提供與 Intune 服務的連線。  

 Intune 是可以在很短的時間內建置及部署的雲端服務。  

##  <a name="what-does-hybrid-mdm-mean"></a>什麼是混合式 MDM？  
 若組織想要提高 Configuration Manager 投資、客戶需要微調控制或客戶的 Intune 規模超出限制，則可以使用透過 Intune 管理行動裝置的混合式實作。  

 混合式部署需要 Microsoft System Center 2012 Configuration Manager SP1 或更新版本。  

 Intune 服務會以服務連接點站台系統角色 (正式名稱為 Microsoft Intune Connector) 連線到 Configuration Manager，該角色會安裝在管理中心或 Configuration Manager 階層的主要站台。 一個 Intune 租用戶只能連線到一個 Configuration Manager 階層，且一個 Configuration Manager 階層只能連線到一個 Intune 租用戶。  

 在混合式 MDM 設定中，會由內部部署的 Configuration Manager 基礎結構來執行部分處理與儲存負荷。 此效率提升可讓混合式 MDM 擴充超過 Intune 獨立部署。  

 混合式部署允許使用 Configuration Manager 系統管理員熟悉的工具。 實作混合式 MDM 時，行動裝置現在可以使用進階功能，例如以角色為基礎的系統管理控制 (RBAC)、SQL Server Reporting Services (SSRS)，以及使用集合成員資格查詢的複雜裝置和使用者群組。  

##  <a name="planning-choices-and-intune-deployment-timelines"></a>規劃選擇和 Intune 部署時間表  
 Intune 創新和演進的步調很快，其每月更新提供新功能或增強功能、增強的規模、透過 Azure 入口網站的新管理主控台體驗、透過 Azure Active Directory 的動態群組等等。 因此，任何設計決策都應該考慮到產品的未來方向。  

 由於服務分短期、中期和長期開發，混合式設定目前提供的許多獨特功能會在功能上複寫至 Intune 獨立部署。  

 如果您要在獨立部署和混合式之間做決定，您應該將部署時間表列入考量。 客戶經常會歷經多次部署，反覆執行設計、建置、使用者驗收測試和試驗階段，這通常需要多個月的時間來完成，之後才會準備開始部署到生產環境。 因此，選擇 Intune 階層設計時，請考慮到要進行實際部署的時間，以及服務的短期、中期和長期方向。  

 隨著 Intune 服務持續發展，我們的目標在於簡化您的設定選擇。 未來，客戶選擇混合式 MDM 環境的唯一理由，應該是需要針對傳統用戶端和行動裝置使用單一管理主控台。  我們努力增強延展性，並新增透過 Azure 入口網站的角色型存取，以及透過更深入 Azure Active Directory 整合的動態群組，所有一切都是為了配合短期和中期服務更新。  

 最後，我們也努力確保不論您今日選擇哪種設定，都能沒有摩擦地輕鬆在混合式與獨立設定選擇之間移動。 目前若要切換 MDM 授權，除了需要 Microsoft 支援人員手動操作，還需要租用戶付出極大的心力。 為了簡化此作業，我們的目標在於允許混合式與 Intune 獨立部署共存，讓您在兩種管理類型之間移動使用者，而不需要您在這兩項設定中擇一。  這項變更也避免了必須求助支援的今日挑戰，而且不需要解除註冊後再重新註冊裝置。  

##  <a name="pros-and-cons-of-intune-standalone"></a>Intune 獨立部署的優缺點  

|優點|缺點|  
|----------|----------|  
|快速建置和部署<br /><br /> 沒有內部部署基礎結構<br /><br /> 更頻繁的更新和功能發行<br /><br /> 學習曲線很低<br /><br /> 管理主控台可供外部使用|有限的報告功能<br /><br /> 有限的安全性角色限制<br /><br /> 沒有外部工具 (例如 PowerShell 等)<br /><br /> 有限的應用程式清查<br /><br /> 基本使用者和裝置群組功能<br /><br /> 需要 Silverlight|  

##  <a name="pros-and-cons-of-hybrid-mdm"></a>混合式 MDM 的優缺點  

|優點|缺點|  
|----------|----------|  
|可擴充<br /><br /> 進階工具 (例如 Configuration Manager 主控台、PowerShell、記錄等)<br /><br /> 角色型存取控制 (RBAC)<br /><br /> 進階報告<br /><br /> MDM + 傳統用戶端的「單一整合」管理<br /><br /> 擴充應用程式清查<br /><br /> 進階使用者和裝置群組<br /><br /> 支援多個 Exchange 內部部署和 Exchange Online 連接器<br /><br /> 支援多個 NDES/CRP 角色<br /><br /> 可將裝置標記為「屬公司擁有」<br /><br /> 更佳的疑難排解功能<br /><br /> 訂閱隨附 Configuration Manager 使用者 CAL|內部部署複雜性 (設定和管理)<br /><br /> 學習曲線陡峭<br /><br /> 更新和功能發行需要維護<br /><br /> 額外的授權需求 (例如 Windows、SQL Server 等)|  

##  <a name="planning-decisions"></a>規劃決策  
 ![混合式&#45;決策](../../mdm/understand/media/hybrid-decisions.png)  

|步驟|決策|
|-|-|  
|<img src="media/hybrid-1.png" style="min-width:32px">|**您要管理多少裝置？**<br /><br /> Intune 獨立部署最多支援 50,000 部裝置。 混合式 MDM 最多支援 300,000 部裝置。<br /><br /> 如需進行任何大規模的部署 (獨立或混合式 MDM)，建議您連絡 Microsoft 帳戶小組。 您的 Microsoft 帳戶小組可協助您與 Intune 專家聯繫，以進一步討論規模與限制。|  
|![混合式&#45;2](../../mdm/understand/media/hybrid-2.png)|**是否需要微調存取控制？(RBAC)**<br /><br /> System Center 2012 Configuration Manager 新增了角色型存取控制 (RBAC)。 RBAC 可讓 Configuration Manager 系統管理員設計和部署複雜的權限集合，以限制系統管理員存取 Configuration Manager 物件和功能。<br /><br /> Intune 獨立部署只提供兩種系統管理員角色︰完整存取和唯讀存取。<br /><br /> 如果您的組織必須限制特定系統管理員存取特定使用者、裝置、功能或物件，則需要具有 RBAC 的 Configuration Manager。<br /><br /> 如果您組織的系統管理團隊人數不多，而且您不需要複雜的微調存取控制，內建安全性角色的 Intune 是最好的選擇。|  
|![混合式&#45;3](../../mdm/understand/media/hybrid-3.png)|**是否需要進階報告功能？**<br /><br /> 使用 Configuration Manager 的混合式 MDM 包含使用 SQL Server Reporting Services (SSRS) 的進階報告功能。 Configuration Manager 隨附 34 個內建 MDM 報表與超過 400 個標準 Configuration Manager 報表。 SSRS 也可讓系統管理員和商務分析師撰寫自己的自訂報表。 此外，可使用外部工具 (例如協調流程工具) 查詢 Configuration Manager 資料庫，以提供自訂警示等特定功能。 由於透過 Configuration Manager 執行報表，所有報表也會包含非 MDM 資料，例如傳統電腦清查與行動裝置清查並存。<br /><br /> Intune 獨立部署提供 9 種報表。 這些報表無法自訂，而且提供有限的輸入變數。 您可以列印報表，或是將報表匯出成 CSV 或 HTML。<br /><br /> 如果您的組織需要進階報告功能，而且具備足夠頻寬並了解如何管理 SSRS，混合式 MDM 是最好的選擇。<br /><br /> 如果您的組織需要易於使用的報告引擎和預先定義的報表，Intune 獨立部署的報告功能應已足夠。|  
|![混合式&#45;4](../../mdm/understand/media/hybrid-4.png)|**您要在無法存取網際網路的情況下管理 Windows 10 裝置嗎？**<br /><br /> 在 Configuration Manager (最新分支) 中，您可以透過 MDM 通道，只使用內部部署基礎結構來管理 Windows 10 裝置。<br /><br /> 內部部署行動裝置管理功能的設計是為了允許無法存取網際網路的用戶端進行 MDM 管理，而且主要目標是一次性使用裝置 (例如 Kiosk 裝置) 和 IoT 裝置。<br /><br /> 由於 Intune 獨立部署的僅限雲端做法，所有受管理的裝置都必須具有網際網路存取權。 如果您的組織想要透過內部部署行動裝置管理來管理 Windows 10 裝置，則需要混合式 MDM 設定。 請注意，內部部署行動裝置管理不支援同時管理網際網路和內部網路行動裝置。|  
|![混合式&#45;5](../../mdm/understand/media/hybrid-5.png)|**您需要完整應用程式清查嗎？**<br /><br /> 根據預設，Intune 獨立部署只會收集 Intune 管理及部署之應用程式的應用程式清查。 這表示清查報表不會包含 Intune 公司入口網站外部使用者已安裝的側載應用程式資訊。<br /><br /> 使用 Configuration Manager 的混合式 MDM 可讓系統管理員將特定裝置指定為「屬公司擁有」。 當裝置設定為屬公司擁有的裝置時，會收集擴充應用程式清查，並提供裝置完整應用程式清單的存取權。<br /><br /> 如果您的組織需要個人從受管理裝置安裝之應用程式的相關資訊，則需要混合式 MDM。 在根據此選擇進行決策之前，請考慮對使用者隱私權所造成的影響。|  
|![混合式&#45;6](../../mdm/understand/media/hybrid-6.png)|**您要以傳統複雜型用戶端方式來管理電腦嗎？**<br /><br /> 混合式 MDM 優於獨立設定的一點是「單一整合」管理。 這表示組織可以透過一項管理工具 (亦即 Configuration Manager 主控台)，來管理其所有桌上型電腦、伺服器和行動裝置。 此外，透過 Configuration Manager 用戶端，非行動裝置還可以使用硬體和軟體清查、軟體更新管理、軟體部署以及作業系統部署等進階管理功能。<br /><br /> 如果您的組織想要管理傳統的 Windows、Linux/UNIX 和 Mac 用戶端，Configuration Manager 是首要管理平台。<br /><br /> Intune 獨立部署也提供使用 Intune 電腦管理用戶端的傳統電腦管理 (Windows 7、8.1 和 10)。 它提供基本電腦管理，包括硬體清查、Windows Update、Endpoint Protection 和簡單軟體部署。 此用戶端不會搭配 Configuration Manager 使用，因此可用於 Intune 獨立和混合式 MDM 部署。|  
|![混合式&#45;7](../../mdm/understand/media/hybrid-7.png)|**您要管理內部部署基礎結構嗎？**<br /><br /> 任何內部部署基礎結構都會產生一定程度的管理額外負荷與複雜性。 Configuration Manager 是需要相當了解、經驗和投資，才能管理及維護其基礎結構的產品。<br /><br /> 混合式 MDM 至少需要單一 Configuration Manager 主要站台，以及資料庫角色、Reporting Services 角色和服務連接點角色。 如果需要傳統電腦管理，也可能需要管理點、發佈點、軟體更新點和應用程式類別目錄角色。 進階功能 (例如憑證部署、Mac 管理和 Endpoint Protection) 加入更多角色和複雜性。<br /><br /> Configuration Manager 階層需要進行大量管理和維護，以確保其狀況良好且運作符合需求。<br /><br /> 如果不想要有 Configuration Manager 階層的額外負荷，Intune 獨立部署是您最好的選擇。|  
|![混合式&#45;8](../../mdm/understand/media/hybrid-8.png)|**您需要外部工具嗎？**<br /><br /> Configuration Manager 是成熟的企業級產品，包含許多不使用主控台來與服務互動的方法。 混合式 MDM 部署可讓系統管理員使用 Configuration Manager SDK 或 PowerShell，以程式設計方式來管理行動裝置。 它也可讓系統管理員利用 System Center Orchestrator、PowerBI 和各種協力廠商增益集等工具。<br /><br /> 在 Intune 獨立部署中，必須透過 Silverlight 主控台執行所有系統管理，而且無法使用任何外部工具。|  
|![混合式&#45;9](../../mdm/understand/media/hybrid-9.png)|**您需要快速 MDM 功能更新嗎？**<br /><br /> 雖然 Configuration Manager (最新分支) 提供快速的更新和功能維護，但部署 Intune 等雲端服務可進一步加速生產環境部署。<br /><br /> Intune 獨立部署可能會比混合式 MDM 部署更早收到新功能。<br /><br /> 如果您的組織想要具有領先地位，Intune 獨立部署會以最及時的方式提供最新 MDM 功能。|



<!--HONumber=Nov16_HO1-->


