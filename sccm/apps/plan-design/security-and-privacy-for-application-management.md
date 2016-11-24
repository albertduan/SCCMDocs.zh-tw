---
title: "應用程式管理的安全性與隱私權 | System Center Configuration Manager"
description: "System Center Configuration Manager 的應用程式管理安全性與隱私權最佳作法。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2c954d2e0244536d74fe85ab98b0d581f7a8167f


---
# <a name="security-and-privacy-for-application-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 的應用程式管理安全性與隱私權

適用於：System Center Configuration Manager (最新分支)


##  <a name="security-best-practices-for-application-management"></a>應用程式管理的安全性最佳作法  

|安全性最佳作法|詳細資訊|  
|----------------------------|----------------------|  
|將應用程式類別目錄點設定為使用 HTTPS 連線並告知使用者有關惡意網站的資訊。|將應用程式類別目錄網站點和應用程式類別目錄 Web 服務點設定為接受 HTTPS 連線，以提供使用者已驗證的伺服器，同時傳輸的資料也將受到保護以避免遭到竄改和檢視。 告知使用者僅連線至信任的網站以協助防止社交工程攻擊。<br /><br /> 在沒有使用 HTTPS 的情況下，請勿於應用程式類別目錄中使用品牌設定選項，顯示您的組織名稱作為識別證明。|  
|使用角色隔離並在個別伺服器上安裝應用程式類別目錄網站點和應用程式類別目錄服務點。|若應用程式類別目錄網站點已遭入侵，請將其與應用程式類別目錄 Web 服務點安裝在不同的伺服器上。 這有助於保護 Configuration Manager 用戶端和 Configuration Manager 基礎結構。 這點非常重要，特別是當應用程式類別目錄網站點接受來自網際網路的用戶端連線時，此設定會讓伺服器容易遭到攻擊。|  
|教育使用者在完成使用應用程式類別目錄之後將瀏覽器視窗關閉。|若使用者以用於應用程式類別目錄的同一個瀏覽器視窗瀏覽外部網站，瀏覽器會繼續使用內部網路中信任站台所適用的安全性設定。|  
|手動指定使用者裝置親和性而非允許使用者自行找出主要裝置，同時請勿啟用基於使用方式的設定。|請勿將由使用者或裝置收集到的資訊視為已授權。 若您使用非由信任系統管理使用者指定的使用者裝置親和性來部署軟體，該軟體可能會被安裝到未獲授權接收該軟體的電腦和使用者。|  
|一律將部署設定為從發佈點下載內容，而不是直接於發佈點上執行。|當您將部署設定為從發佈點下載內容並於本機執行時，Configuration Manager 用戶端會在下載內容後驗證套件雜湊，若該雜湊與原則中的雜湊不相符，用戶端會捨棄該套件。 相較之下，若您將部署設定為直接從發佈點上執行，Configuration Manager 用戶端就不會驗證套件雜湊，這表示 Configuration Manager 用戶端安裝的軟體可能已遭竄改。<br /><br /> 如果您必須從發佈點上直接執行部署，請在發佈點上為套件使用 NTFS 最低權限，同時請使用 IPsec 以確保用戶端和發佈點之間的通道安全，以及發佈點和站台伺服器之間的通道安全。|  
|若 [以系統管理權限執行]  選項已勾選，請勿允許使用者與程式互動。|設定程式時，您可設定 [允許使用者與此程式互動]  選項，以便使用者透過使用者介面回應任何必要提示。 若該程式同時設定為 [以系統管理權限執行] ，該程式執行所在電腦上的攻擊者便可透過使用者介面在用戶端電腦上進行權限的提升。<br /><br /> 使用以 Windows Installer 為基礎的安裝程式搭配依使用者提升的權限，來進行需要系統管理認證的軟體部署，但必須在使用者不具有系統管理認證的情況下執行。 Windows Installer 依使用者提升的權限，提供您部署包含此需求的應用程式時一個最安全的方式。|  
|使用 [安裝權限]  用戶端設定，以限制使用者在安裝軟體時是否可與程式互動。|設定 [電腦代理程式]  用戶端裝置設定 [安裝權限]  以限制可使用應用程式類別目錄或軟體中心來安裝軟體的使用者類型。 例如，您可建立自訂用戶端設定，將 [安裝權限]  設為 [僅限系統管理員] 。 接著將此用戶端設定套用至伺服器集合，以避免不具有系統管理權限的使用者將軟體安裝到那些電腦上。|  
|針對行動裝置，則只能部署已簽署的應用程式|部署行動裝置應用程式時，請僅針對已由行動裝置信任的憑證授權單位 (CA) 完成程式碼簽署的應用程式進行部署。 例如：<br /><br /> - 由知名 CA (例如 VeriSign) 簽署的廠商應用程式。<br /><br /> - 您未透過 Configuration Manager 而獨立使用內部 CA 簽署的內部應用程式。<br /><br /> - 建立應用程式類型與使用簽署憑證時，您使用 Configuration Manager 簽署的內部應用程式。|  
|如果您使用 Configuration Manager 中的 [建立應用程式精靈] 簽署行動裝置應用程式，請確保簽署憑證檔案的位置和通訊通道的安全。|若要協助保護您的電腦不受提升權限和攔截式攻擊，請將簽署憑證檔案儲存在受保護的資料夾並於下列電腦之間使用 IPsec 或 SMB︰<br /><br /> - 執行 Configuration Manager 主控台的電腦。<br /><br /> - 儲存憑證簽署檔案的電腦。<br /><br /> - 儲存應用程式來源檔案的電腦。<br /><br /> 或者，請在執行 [建立應用程式精靈] 之前，不透過 Configuration Manager 而獨立簽署應用程式。|  
|實作用於保護參照電腦的存取控制。|當系統管理使用者以瀏覽參照電腦的方式在部署類型中設定偵測方法時，請確保該電腦並未遭到入侵。|  
|若系統管理使用者具有以角色為基礎的安全性角色，且該安全性角色與應用程式管理相關，請限制與監視該系統管理使用者︰<br /><br /> - **應用程式系統管理員**<br>- **應用程式作者**<br>- **應用程式部署管理員**|即使您已設定以角色為基礎的系統管理，可建立和部署應用程式的系統管理使用者所具有的權限可能比您想像的多。 例如，當系統管理使用者建立或修改應用程式時，他們可以選取安全性範圍以外的相依應用程式。|  
|當您設定 Microsoft Application Virtualization (App-V) 虛擬環境時，請選取在虛擬環境中擁有相同信任層級的應用程式。|由於 App-V 虛擬環境中旳應用程式可共用資源，例如剪貼簿，請設定虛擬環境使其選取的應用程式都擁有相同信任層級。<br /><br /> 如需詳細資訊，請參閱[建立 App-V 虛擬環境](../../apps/deploy-use/create-app-v-virtual-environments.md)。|  
|如果您部署 Mac 電腦的應用程式，請確認來源檔案是否來自可信任的來源。|CMAppUtil 工具尚未驗證來源封裝簽章，因此須確定其來自您信任的來源。 CMAppUtil 工具無法偵測檔案是否已遭竄改。|  
|若您為 Mac 電腦部署應用程式，請確保 **.cmmac** 檔案位置的安全，同時確保在將此檔案匯入 Configuration Manager 時通訊通道的安全。|由於 CMAppUtil 工具產生後，您匯入 Configuration Manager 的 **.cmmac** 檔案並未簽署或驗證，為了協助防止此檔案遭到竄改， 請將該檔案儲存在受保護的資料夾，並於下列電腦之間使用 IPsec 或 SMB：<br /><br /> - 執行 Configuration Manager 主控台的電腦。<br /><br /> - 儲存 **.cmmac** 檔案的電腦。|  
|如果您設定 Web 應用程式部署類型，請使用 HTTPS 而非 HTTP 來確保連線的安全。|如果您是使用 HTTP 連結而不是 HTTPS 連結來部署 Web 應用程式，則可將裝置重新導向到 Rogue 伺服器，而在裝置和伺服器之間傳送的資料可能會遭到竄改。|  

##  <a name="security-issues-for-application-management"></a>應用程式管理的安全性問題  

-   低權限使用者可在用戶端電腦上從用戶端快取複製檔案。  

     使用者可讀取用戶端快取，但無法寫入。 但只要有讀取權限，使用者可在不同電腦之間複製應用程式安裝檔案。  

-   低權限使用者可在用戶端電腦上修改用於記錄軟體部署記錄的檔案。  

     由於應用程式記錄資訊未受到保護，使用者可針對用於報告應用程式是否已安裝的檔案進行修改。  

-   未簽署 App-V 套件。  

     Configuration Manager 中的 App-V 套件不支援簽署，因此無法驗證內容是否來自信任來源，以及內容是否在轉換時遭到變更。 此安全性問題並沒有防護方式，請確保您遵循安全性最佳作法，從信任來源和受保護位置下載內容。  

-   已發佈的 App-V 應用程式可供電腦上的所有使用者安裝。  

     若 App-V 應用程式已在電腦上發佈，所有登入該電腦的使用者都可安裝此應用程式。 這表示在應用程式發佈後，您便無法限制可安裝應用程式的使用者。  

-   您不能限制公司入口網站的安裝權限  

     雖然您可以設定用戶端設定，將安裝權限限定於裝置的主要使用者，或只限定於本機系統管理員，但此設定對公司入口網站是沒功用的。 這可能導致因使用者安裝了不被允許安裝的應用程式，而造成權限提高。  

##  <a name="certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a>應用程式類別目錄需要 Microsoft Silverlight 5 憑證和提升權限的信任模式  
 Configuration Manager 用戶端需要 Microsoft Silverlight 5，且必須在更高的信任模式下執行，以供使用者透過應用程式類別目錄安裝軟體。 根據預設，Silverlight 會以部分信任模式執行，以防止應用程式存取使用者資料。 如果尚未安裝 Microsoft Silverlight 5，則 Configuration Manager 會自動在用戶端上予以安裝，並預設將電腦代理程式的 [允許 Silverlight 應用程式在更高的信任模式下執行] 用戶端設定設為 [是]。 此設定允許已簽署和信任的 Silverlight 應用程式要求更高的信任模式。  

 當您安裝應用程式類別目錄網站點站台系統角色時，用戶端會同時將 Microsoft 簽署憑證安裝在每部 Configuration Manager 用戶端電腦上的 [信任的發行者] 電腦憑證存放區中。 此憑證允許其所簽署之 Silverlight 應用程式在更高的信任模式下執行，讓電腦得以從應用程式類別目錄安裝軟體。 Configuration Manager 會自動管理此簽署憑證。 若要確保服務連續性，請勿手動刪除或移動此 Microsoft 簽署憑證。  

> [!WARNING]  
>  啟用用戶端設定 [允許 Silverlight 應用程式在更高的信任模式下執行]  可允許已由用戶端存放區或使用者存放區中 [信任的發行者] 電腦憑證存放區中憑證所簽署的所有 Silverlight 應用程式在更高的信任模式下執行。 用戶端設定無法特別針對 Configuration Manager 應用程式類別目錄或電腦存放區中 [信任的發行者] 憑證存放區，啟用更高的信任模式。 若惡意程式碼在 [信任的發行者] 存放區新增 Rogue 憑證，例如在使用者存放區，該惡意程式碼便可使用自己的 Silverlight 應用程式在更高的信任模式下執行。  

 將用戶端設定 [允許 Silverlight 應用程式在更高的信任模式下執行]  設為 [否] ，並無法將 Microsoft 簽署憑證從用戶端移除。  

 如需 Silverlight 信任的應用程式詳細資訊，請參閱 [Trusted Applications (信任的應用程式)](http://go.microsoft.com/fwlink/p/?LinkId=252842)。  

##  <a name="privacy-information-for-application-management"></a>應用程式管理的隱私權資訊  
 應用程式管理可讓您在階層中的任何用戶端電腦或用戶端行動裝置上，執行任何應用程式、程式或指令碼。 Configuration Manager 無法控制您所執行的應用程式、程式或指令碼的類型，或是它們所傳輸的資訊類型。 在應用程式部署程序期間，Configuration Manager 可能會於用戶端和伺服器之間，傳輸可識別裝置與登入帳戶的資訊。  

 Configuration Manager 會保存軟體部署程序的狀態資訊。 除非用戶端使用 HTTPS 來進行通訊，軟體部署狀態資訊在傳輸期間並未加密。 此狀態資訊在資料庫中並未以加密方式儲存。  

 使用 Configuration Manager 應用程式安裝，透過遠端、互動或無訊息方式在用戶端上安裝軟體時，可能需受該軟體的軟體授權條款約束 (其有別於 System Center Configuration Manager 的軟體授權條款)。 在您使用 Configuration Manager 部署軟體之前，請一律檢閱並同意軟體授權條款。  

 應用程式部署並不會預設為自動進行，而需要執行數個設定步驟才能完成。  

 另外兩個可選功能為使用者裝置親和性和應用程式類別目錄，可提升軟體部署的效率︰  

-   使用者裝置親和性可將使用者對應至裝置，以便 Configuration Manager 系統管理員將軟體部署至使用者，如此一來，該軟體即會自動安裝到使用者最常用的一部或多部電腦上。  

-   應用程式類別目錄網站可允許使用者要求軟體以進行安裝。  

 請檢視以下各節以取得有關使用者裝置親和性和應用程式類別目錄的隱私權資訊。  

 設定應用程式管理之前，請考量您的隱私權需求。  

##  <a name="user-device-affinity"></a>使用者裝置親和性  
-  Configuration Manager 可能會在用戶端與管理點站台系統之間，傳輸可識別電腦、登入帳戶及登入帳戶的使用方式摘要等資訊。  
-  除非已設定管理點要求用戶端使用 HTTPS 進行通訊，否則不會加密用戶端與伺服器之間所傳輸的資訊。  
-  電腦與登入帳戶使用方式資訊 (用來將使用者對應至裝置) 會儲存在用戶端電腦上，並傳送到管理點，然後存放在 Configuration Manager 資料庫內。 根據預設，超過 90 天的舊資訊會從資料庫刪除。 藉由設定 [刪除過時使用者裝置親和性資料]  站台維護工作，就可以設定刪除行為。
-  Configuration Manager 會保存使用者裝置親和性的狀態資訊。 除非設定用戶端使用 HTTPS 與管理點進行通訊，否則狀態資訊在傳輸過程中不會進行加密。 此資訊不會以加密形式儲存在資料庫內。  
-  電腦、登入帳戶使用資訊以及狀態資訊不會傳送到 Microsoft。  
-  用於建立使用者與裝置親和性的電腦與登入使用資訊會隨時保持啟用。 此外，使用者與系統管理使用者可以提供使用者親和性資訊。  

##  <a name="application-catalog"></a>應用程式類別目錄  
-  應用程式類別目錄可讓 Configuration Manager 系統管理員發佈任何應用程式、程式或指令碼，以供使用者執行。 Configuration Manager 無法控制類別目錄中所發佈的程式或指令碼的類型，或是它們所傳輸的資訊類型。    
-  Configuration Manager 可能會在用戶端與應用程式類別目錄站台系統角色之間，傳輸可識別電腦與登入帳戶的資訊。 除非已設定這些站台系統角色要求用戶端使用 HTTPS 進行連接，否則不會加密用戶端與伺服器之間所傳輸的資訊。  
-  應用程式核准要求的相關資訊會儲存在 Configuration Manager 資料庫中。 根據預設，取消或是拒絕的要求會在 30 天後刪除，也會連帶刪除相對應的要求歷程記錄項目。 藉由設定 [刪除過時應用程式要求資料]  站台維護工作，就可以設定刪除行為。 位於核准與擱置狀態中的應用程式的應用程式核准要求永遠不會遭到刪除。  
-  透過應用程式類別目錄傳出或傳入的資訊都不會傳送至 Microsoft。  
-  根據預設，不會安裝應用程式類別目錄。 此安裝需要數個設定步驟。  



<!--HONumber=Nov16_HO1-->

