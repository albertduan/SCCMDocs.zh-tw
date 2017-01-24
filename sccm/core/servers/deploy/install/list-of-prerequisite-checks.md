---
title: "必要條件檢查 | Microsoft Docs"
description: "檢閱 System Center Configuration Manager 可用的必要條件檢查。 包括安全性權限的檢查。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 9ace6e8fa05122924daaeceddf097ce1db12cf39


---
# <a name="list-of-prerequisite-checks-for-system-center-configuration-manager"></a>System Center Configuration Manager 的必要條件檢查清單

適用於：System Center Configuration Manager (最新分支)

下列章節詳述可用的必要條件檢查。  


 如需使用必要條件檢查工具的資訊，請參閱[必要條件檢查工具](prerequisite-checker.md)。  

##  <a name="a-namebkmksecuritya-prerequisite-checks-for-security-rights"></a><a name="BKMK_Security"></a> 安全性權限的必要條件檢查  
 下列是「先決條件檢查程式」針對安全性權限執行的先決條件檢查。  

 **管理中心網站上的系統管理員權限** - 確認執行 Configuration Manager 安裝程式的使用者帳戶具有管理中心網站電腦上的本機**系統管理員**權限。  

-   **嚴重性：** 錯誤  

-   **適用性：**  
      -   主要網站  

**擴充主要站台上的系統管理權限** - 確認執行安裝程式的使用者具有將擴充之獨立主要站台上的本機**系統管理員**權限。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站  

**站台系統上的系統管理權限** - 確認執行 Configuration Manager 安裝程式的使用者帳戶具有站台伺服器電腦上的本機**系統管理員**權限。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站  
    -   主要網站  
    -   次要網站  

**擴充主要站台上的 CAS 電腦系統管理權限** - 確認管理中心網站的電腦帳戶具有將擴充之獨立主要站台上的本機**系統管理員**權限。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站  

**連線至管理中心網站上的 SQL Server** - 確認在主要站台上執行 Configuration Manager 安裝程式以加入現有階層的使用者帳戶，具有管理中心網站上 SQL Server 執行個體的**系統管理員**角色。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   主要網站  

**站台伺服器電腦帳戶系統管理權限** - 確認站台伺服器電腦帳戶具有 SQL Server 及管理點電腦上的系統管理權限。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   主要網站  
    -   SQL Server  

**站台系統至 SQL Server 通訊** - 確認已在 Active Directory 網域服務中，針對設定要為用來裝載 Configuration Manager 站台資料庫之 SQL Server 執行個體執行 SQL Server 服務的帳戶，登錄有效的服務主體名稱 (SPN)。 Active Directory 網域服務中必須註冊有效的 SPN 才能支援 Kerberos 驗證。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   次要網站  
    -   管理點  

**SQL Server 安全性模式** - 確認已針對 Windows 驗證安全性設定 SQL Server。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   SQL Server  

**SQL Server 系統管理員權限** - 確認執行 Configuration Manager 安裝程式的使用者帳戶，具有為站台資料庫安裝選取之 SQL Server 執行個體上的**系統管理員**角色。 如果安裝程式無法存取 SQL Server 執行個體以確認權限，這項檢查也會失敗。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   SQL Server  

**參照站台的 SQL Server 系統管理員權限** - 確認執行 Configuration Manager 安裝程式的使用者帳戶，具有選取作為參照站台資料庫之 SQL Server 角色執行個體上的**系統管理員**角色。  需要有 SQL Server **sysadmin** 角色權限才能修改網站資料庫。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   SQL Server  

##  <a name="a-namebkmkdependenciesa-prerequisite-checks-for-configuration-manager-dependencies"></a><a name="BKMK_Dependencies"></a> Configuration Manager 相依性的必要條件檢查  
 以下是必要條件檢查工具針對 Configuration Manager 相依性執行的必要條件檢查。  

**目標主要網站上作用中的移轉對應**  

 確認沒有主要網站的作用中移轉對應。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站  

**使用中的複本 MP** - 檢查是否有使用中的管理點複本。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   主要網站  

**發佈點上的系統管理權限** - 確認執行安裝程式的使用者具有發佈點電腦上的本機**系統管理員**權限。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   發佈點  

**管理點上的系統管理權限** - 確認站台伺服器的電腦帳戶具有管理點及發佈點電腦上的**系統管理員**權限。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理點  

**系統管理共用 (站台系統)** - 確認站台系統電腦上有必要的系統管理共用。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理點  

**應用程式相容性** - 確認目前的應用程式與應用程式架構相容。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站  

**已啟用 BITS** - 確認管理點站台系統電腦上已安裝「背景智慧型傳送服務」(BITS)。 此檢查失敗時，表示未安裝 BITS、電腦上或遠端 IIS 主機上未安裝 IIS7 的 IIS 6 WMI 相容性元件，或是安裝程式無法確認遠端 IIS 設定，因為網站伺服器電腦上未安裝 IIS 通用元件。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理點  

**已安裝 BITS** - 確認 Internet Information Services (IIS) 中已安裝「背景智慧型傳送服務」(BITS)。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理點  

**SQL Server 上不區分大小寫定序** - 確認 SQL Server 安裝使用不區分大小寫定序，例如 SQL_Latin1_General_CP1_CI_AS。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   SQL Server  

**檢查現有的獨立主要站台，取得版本和站台碼** - 確認您打算擴充的主要站台是獨立的主要站台，並且與要安裝的管理中心網站具有相同版本的 Configuration Manager，但站台碼不同。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站  

**檢查是否有不相容的集合參考** - 在升級期間，這項檢查會確認集合只會參考相同類型的其他集合。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站  

**管理點電腦上的用戶端版本** - 確認您要安裝管理點的電腦並未安裝不同版本的 Configuration Manager 用戶端。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理點  

**SQL Server 記憶體使用量設定** - 檢查 SQL Server 是否設定為無限制記憶體使用量。 您應將 SQL Server 記憶體設為具有上限。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   SQL Server  

**專用 SQL Server 執行個體** - 檢查是否已設定專用的 SQL Server 執行個體來裝載 Configuration Manager 站台資料庫。 如果另一個網站使用執行個體，則您必須選取不同的執行個體讓新網站使用。 或者，您可以解除安裝另一個網站，或將其資料庫移至不同的 SQL Server 執行個體。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**伺服器上的現有 Configuration Manager 伺服器元件** - 確認所選取要進行站台安裝的電腦上尚未安裝站台伺服器或站台系統角色。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**SQL Server 的防火牆例外** - 檢查 Windows 防火牆是否已停用，或是否存在 SQL Server 的相關 Windows 防火牆例外。 您必須允許從遠端存取 sqlservr.exe 或必要的 TCP 連接埠。 根據預設，SQL Server 會接聽 TCP 連接埠 1433，SQL Broker Service 則使用 TCP 連接埠 4022。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站    
    -   管理點  

**SQL Server 的防火牆例外 (獨立主要站台)** - 檢查 Windows 防火牆是否已停用，或是否存在 SQL Server 的相關 Windows 防火牆例外。 您必須允許從遠端存取 sqlservr.exe 或必要的 TCP 連接埠。 根據預設，SQL Server 會接聽 TCP 連接埠 1433，SQL Broker Service 則使用 TCP 連接埠 4022。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   主要網站 (僅限獨立)  

**管理點的 SQL Server 防火牆例外** - 檢查 Windows 防火牆是否已停用，或是否存在 SQL Server 的相關 Windows 防火牆例外。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理點  

**IIS HTTPS 設定** - 確認 HTTPS 通訊協定的 Internet Information Services (IIS) 網站繫結。 當您選擇安裝需要 HTTPS 的網站角色時，必須在指定的伺服器上使用有效的 PKI 憑證設定 IIS 網站繫結。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理點    
    -   發佈點  

**IIS 服務正在執行** - 確認電腦上已安裝 Internet Information Services (IIS) 且正在執行，以安裝管理點或發佈點。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理點    
    -   發佈點  

**比對擴充主要站台的定序** - 確認您將擴充之獨立主要站台的站台資料庫與管理中心網站的站台資料庫擁有相同的定序。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站  

**已登錄 Microsoft 遠端差異壓縮 (RDC) 程式庫** - 確認已在 Configuration Manager 站台伺服器上登錄 Microsoft 遠端差異壓縮 (RDC) 程式庫。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**Microsoft Windows Installer** - 確認 Windows Installer 版本。 這項檢查失敗時，表示安裝程式無法確認版本，或安裝的版本不符合 Windows Installer 4.5 版的最低需求。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**Microsoft XML Core Services 6.0 (MSXML60)** - 確認電腦上已安裝 Microsoft Core XML Services (MSXML) 6.0 或更新版本。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站    
    -   Configuration Manager 主控台    
    -   管理點    
    -   發佈點  

**Configuration Manager 主控台的最低 .NET Framework 版本** - 檢查 Configuration Manager 主控台電腦上是否已安裝 Microsoft .NET Framework 4.0 版。 您可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/p/?LinkId=189149)下載 Microsoft .NET Framework 4.0 版。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   Configuration Manager 主控台  

**Configuration Manager 站台伺服器的最低 .NET Framework 版本** - 檢查 Configuration Manager 站台伺服器上是否已安裝 Microsoft .NET Framework 3.5 版。 對於 Windows Server 2008，則可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/p/?LinkId=185604)下載 Microsoft .NET Framework 3.5 版。 針對 Windows Server 2008 R2，您可以在伺服器管理員內以功能的形式啟用 Microsoft .NET Framework 3.5 版。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**Configuration Manager 次要站台之 SQL Server Express Edition 安裝的最低 .NET Framework 版本** - 確認在要安裝 SQL Server Express Edition 的 Configuration Manager 次要站台電腦上已安裝 Microsoft .NET Framework 4.0 版。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   次要網站  

**父/子資料庫定序** - 確認站台資料庫的定序與父站台資料庫的定序相符。 階層中的所有網站都必須使用相同的資料庫定序。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   主要網站    
    -   次要網站  

**站台伺服器上的 PowerShell 2.0** - 確認 Configuration Manager Exchange 連接器的站台伺服器上已安裝 Windows PowerShell 2.0 版或更新版本。 如需 PowerShell 2.0 的詳細資訊，請參閱 Microsoft 知識庫中的 [文章編號: 968930](http://go.microsoft.com/fwlink/p/?LinkId=226450) 。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   主要網站  

**主要 FQDN** - 確認電腦的 NetBIOS 名稱符合電腦的本機主機名稱 (FQDN 的第一個標籤)。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站    
    -   SQL Server  

**遠端連線至次要站台上的 WMI** - 檢查安裝程式是否能在次要站台伺服器上建立與 WMI 的遠端連線。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   次要網站  

**必要的 SQL Server 定序** - 確認 SQL Server 執行個體和 Configuration Manager 站台資料庫 (如有安裝) 已設定為使用 SQL_Latin1_General_CP1_CI_AS 定序，除非您使用中文作業系統並需要 GB18030 支援。  

 如需變更 SQL Server 執行個體和資料庫定序的詳細資訊，請參閱《SQL Server 2008 R2 線上叢書》中的 [設定和變更定序](http://go.microsoft.com/fwlink/p/?LinkID=234541) 。  如需啟用 GB18030 支援的資訊，請參閱 [System Center Configuration Manager 的多語系支援](../../../../core/plan-design/hierarchy/international-support.md)。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**安裝程式來源資料夾** - 確認次要站台的電腦帳戶，具有安裝程式來源資料夾及共用的 NTFS 檔案系統**讀取**權限和共用**讀取**權限。  

> [!NOTE]  
>  如果您使用系統管理共用 (例如 C$ 和 D$)，則次要網站電腦帳戶必須是電腦上的系統管理員。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   次要網站  

**安裝程式來源版本** - 確認來源資料夾中，您為次要站台安裝指定的 Configuration Manager 版本必須符合主要站台的 Configuration Manager 版本。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   次要網站  

**使用中的站台碼** - 確認您指定的站台碼尚未在 Configuration Manager 階層中使用。 您必須為此網站指定唯一的網站碼。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   主要網站  

**SMS 提供者電腦具有與站台伺服器相同的網域** - 檢查執行 SMS 提供者執行個體的電腦是否具有與站台伺服器相同的網域。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   SMS 提供者  

**SQL Server 版本** - 確認站台上 SQL Server 的版本不是 SQL Server Express。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   SQL Server  

**次要站台上的 SQL Server Express** - 確認 SQL Server Express 可以成功安裝在次要站台的站台伺服器電腦上。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   次要網站  

**次要站台電腦上的 SQL Server** - 確認次要站台電腦上已安裝 SQL Server。 不支援在遠端網站系統上安裝 SQL Server。  

> [!WARNING]  
>  這項檢查只有在您選取讓安裝程式使用現有 SQL Server 執行個體時才適用。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   次要網站  

**SQL Server 處理程序記憶體配置** - 確認 SQL Server 至少保留 8 GB 記憶體給管理中心網站和主要站台，並至少保留 4 GB 記憶體給次要站台。 如需如何使用 SQL Server Management Studio 設定記憶體固定量的詳細資訊，請參閱 [如何：設定記憶體固定量 (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759)。  

> [!NOTE]  
>  這項檢查不適用次要網站上的 SQL Server Express，其保留記憶體限於 1 GB。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   SQL Server  

**SQL Server 服務執行帳戶** - 確認 SQL Server 服務的登入帳戶不是本機使用者帳戶或 LOCAL SERVICE。 您必須將 SQL Server 服務設定為使用有效的網域帳戶、NETWORK SERVICE 或 LOCAL SYSTEM。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**SQL Server TCP 連接埠** - 確認 SQL Server 已啟用 TCP 並設定為使用靜態連接埠。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   SQL Server  

**SQL Server 版本** - 確認指定的站台資料庫伺服器上已安裝支援的 SQL Server 版本。 如需詳細資訊，請參閱 [System Center Configuration Manager 的 SQL Server 版本支援](../../../../core/plan-design/configs/support-for-sql-server-versions.md)。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   SQL Server  

**不支援的站台系統作業系統升級版本** - 進行升級時，此規則會檢查執行 Windows Server 2008 或更舊版本的電腦上是否已安裝發佈點以外的站台系統角色。  

> [!NOTE]  
>  由於這項檢查無法解析安裝在 Azure 中的站台系統角色狀態，也無法解析您在整合 Intune 與 Configuration Manager 時，為 Microsoft Intune 所使用之雲端存放裝置安裝的站台系統角色狀態，因此您可以將這些角色的警告視為誤判而予以忽略。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   主要網站    
    -   次要網站  

**擴充的主要站台上有不支援的站台系統角色「Asset Intelligence 同步處理點」** - 確認您要擴充的獨立主要站台上並未安裝 Asset Intelligence 同步處理點站台系統角色。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站  

**擴充的主要站台上有不支援的站台系統角色「Endpoint Protection 點」** - 確認您要擴充的獨立主要站台上並未安裝 Endpoint Protection 點站台系統角色。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站  

<a name="-head"></a><<<<<<< HEAD
=======

>>>>>>> 5e8e486ea74f66a92696c65e3367aec2e592b001 **擴充主要站台上有不支援的站台系統角色「Microsoft Intune 連接器」** - 確認您要擴充的獨立主要站台上並未安裝「Microsoft Intune 連接器」站台系統角色。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站  

**已安裝使用者狀態移轉工具 (USMT)** - 檢查是否已安裝 Windows 8.1 版 Windows 評定及部署套件 (ADK) 的使用者狀態移轉工具 (USMT) 元件。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站 (僅限獨立)  

**驗證 SQL Server 電腦的 FQDN** - 檢查您為 SQL Server 電腦指定的 FQDN 是否有效。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   SQL Server  

**檢查管理中心網站版本** - 檢查管理中心網站是否具有相同版本的 Configuration Manager。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   主要網站  

**確認站台伺服器發佈至 Active Directory 的權限** - 確認站台伺服器的電腦帳戶對 Active Directory 網域中的**系統管理**容器具有**完全控制**權限。 如需設定必要權限之選項的詳細資訊，請參閱[擴充 System Center Configuration Manager 的 Active Directory 架構](../../../../core/plan-design/network/extend-the-active-directory-schema.md)。  

> [!NOTE]  
>  如果您已手動確認權限，則可忽略此警告。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**已安裝 Windows 部署工具** - 檢查是否已安裝 Windows 10 版 Windows 評定及部署套件 (ADK) 的 Windows 部署工具元件。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   SMS 提供者  

**Windows 容錯移轉叢集** - 確認具有管理點或發佈點的電腦不是 Windows 叢集的一部分。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理點    
    -   發佈點  

**已安裝 Windows 預先安裝環境** - 檢查是否已安裝 Windows 10 版 Windows 評定及部署套件 (ADK) 的 Windows 預先安裝環境元件。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   SMS 提供者  

**Windows 遠端管理 (WinRM) v1.1** - 確認主要站台伺服器或 Configuration Manager 主控台電腦上已安裝 WinRM v1.1，以執行頻外管理主控台。 如需如何下載 WinRM 1.1 的詳細資訊，請參閱 Microsoft 知識庫中的 [文章編號: 936059](http://go.microsoft.com/fwlink/p/?LinkId=247166) 。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   主要網站    
    -   Configuration Manager 主控台  

**站台伺服器上的 WSUS** - 確認站台伺服器上已安裝 Windows Server Update Services (WSUS) 3.0 Service Pack 2 版。 當您在網站伺服器以外的電腦上使用軟體更新點時，必須在網站伺服器上安裝 WSUS 管理主控台。 如需 WSUS 的詳細資訊，請參閱 [Windows Server Update Services](http://go.microsoft.com/fwlink/p/?LinkID=79477) 網頁。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站  

##  <a name="a-namebkmkrequirementsa-prerequisite-checks-for-system-requirements"></a><a name="BKMK_Requirements"></a> 系統需求的必要條件檢查  
 下列是「先決條件檢查程式」針對系統需求執行的先決條件檢查。  

**Active Directory 網域功能層級檢查** - 確認 Active Directory 網域功能層級至少為 Windows Server 2008 R2。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站  

**檢查伺服器服務是否正在執行** - 確認伺服器服務是否已啟動。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**網域成員資格** - 確認 Configuration Manager 電腦是否為 Windows 網域的成員。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站    
    -   SMS 提供者    
    -   SQL Server  

**網域成員資格** - 確認 Configuration Manager 電腦是否為 Windows 網域的成員。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理點    
    -   發佈點  

**站台伺服器上的 FAT 磁碟機** - 檢查磁碟機是否是以 FAT 檔案系統進行格式化。 在使用 NTFS 檔案系統格式化的磁碟機上安裝網站伺服器元件可獲得較高的安全性。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   主要網站  

**站台伺服器上的可用磁碟空間** - 站台伺服器電腦必須至少有 5 GB 的可用磁碟空間，才能安裝站台伺服器。 如果您在同一部電腦上安裝 SMS 提供者網站系統角色，則必須有額外 1 GB 的可用空間。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**系統重新啟動擱置中** - 檢查在您執行安裝程式之前，是否有其他程式要求重新啟動伺服器。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  
    -   Configuration Manager 主控台    
    -   SMS 提供者    
    -   SQL Server    
    -   管理點    
    -   發佈點  

**唯讀網域控制站** - 唯讀網域控制站 (RODC) 上不支援站台資料庫伺服器和次要站台伺服器。 如需詳細資訊，請參閱 Microsoft 知識庫中的 [網域控制站上安裝 SQL Server 時，您可能會遇到問題](http://go.microsoft.com/fwlink/p/?LinkId=264856) 。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**架構延伸** - 判斷 Active Directory 網域服務架構是否已擴充，若已擴充，則判斷用來擴充的架構延伸版本為何。 站台伺服器安裝並不需要 Configuration Manager Active Directory 架構延伸，但建議使用它們以完整支援使用所有 Configuration Manager 功能。 如需擴充架構之優點的詳細資訊，請參閱 [Extend the Active Directory schema for System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) (擴充 System Center Configuration Manager 的 Active Directory 架構)。  

-   **嚴重性：** 警告  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站  

**站台伺服器 FQDN 長度** - 檢查站台伺服器電腦的 FQDN 長度。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站  

**不支援的 Configuration Manager 主控台作業系統** - 確認 Configuration Manager 主控台可安裝在執行支援之作業系統版本的電腦上。 如需詳細資訊，請參閱 [System Center Configuration Manager 主控台的支援作業系統](/sccm/core/plan-design/configs/supported-operating-systems-consoles)。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   Configuration Manager 主控台  

**安裝程式不支援的站台伺服器作業系統版本** - 確認伺服器上執行的是支援的作業系統。 如需詳細資訊，請參閱 [Supported operating systems for sites and clients for System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers) (適用於 System Center Configuration Manager 的站台與用戶端支援的作業系統)。  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站    
    -   次要網站    
    -   Configuration Manager 主控台    
    -   管理點    
    -   發佈點  

**檢查資料庫一致性** - 從 1602 版開始，這項檢查會確認資料庫一致性  

-   **嚴重性：** 錯誤  

-   **適用性：**  

    -   管理中心網站    
    -   主要網站  



<!--HONumber=Dec16_HO3-->


