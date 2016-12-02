---
title: "用戶端設定 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager 的管理主控台，選取用戶端設定。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: 15
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: cbe052891c55dd0c0d58c6e65d783314b0ec8ce9

---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>關於 System Center Configuration Manager 中的用戶端設計

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中所有的用戶端設定，都是在 Configuration Manager 主控台 [管理] 工作區的 [用戶端設定] 節點中管理。 Configuration Manager 會提供一組預設設定。 當您修改預設用戶端設定時，這些設定會套用至階層中的所有用戶端。 您也可以設定自訂用戶端設定，當您將這些設定指派給集合時，會覆寫預設用戶端設定。 如需如何設定用戶端設定的詳細資訊，請參閱 [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md)。  

 許多用戶端設定完全一目了然。 使用以下各節取得有關用戶端設定的詳細資訊，您可能需要某些資訊才能設定這些用戶端設定。  

##  <a name="a-namebkmkbitsa-background-intelligent-transfer"></a><a name="BKMK_BITS"></a> 背景智慧型傳送  

-   **限制 BITS 背景傳送的最大網路頻寬**  

     如果此選項設定為 [True] 或 [是]，則 Configuration Manager 用戶端就會使用 BITS 頻寬節流設定。  

-   **節流時段開始時間**  

     以本機時間指定 BITS 節流時段的開始時間。  

-   **節流時段結束時間**  

     以本機時間指定 BITS 節流時段的結束時間。 如果此值與 [節流時段開始時間] 相同，則會永遠啟用 BITS 節流。  

-   **節流時段的最大傳輸速率 (Kbps)**  

     指定可由 Configuration Manager 用戶端在指定的 BITS 節流時段使用的最大傳輸速率 (Kbps)。  

-   **允許在節流時段以外進行 BITS 下載**  

     選取此選項，以允許在節流時段以外下載 BITS。 此選項允許 Configuration Manager 用戶端在指定的時段之外使用獨立的 BITS 設定。  

-   **節流時段以外的最大傳輸速率 (Kbps)**  

     指定可由 Configuration Manager 用戶端在指定的 BITS 節流時段以外時使用的最大傳輸速率 (Kbps)。 此選項只能在您選取以允許在指定時段以外的 BITS 節流時設定。  

##  <a name="a-namebkmkclientpolicydevicesettingsa-client-policy"></a><a name="BKMK_ClientPolicyDeviceSettings"></a> 用戶端原則  

-   **用戶端原則輪詢間隔 (分鐘)**  

     指定下列 Configuration Manager 用戶端下載用戶端原則的頻率：  

    -   Windows 電腦 (例如，桌上型電腦、伺服器、膝上型電腦)  

    -   Configuration Manager 註冊的行動裝置  

    -   Mac 電腦  

    -   執行 Linux 或 UNIX 的電腦  

-   **啟用用戶端的使用者原則輪詢**  

     當您將此設定設為 [True] 或 [是]，且 Configuration Manager 找到使用者時，電腦上的 Configuration Manager 用戶端會接收使用者所登入的目標應用程式和程式。 如需如何探索使用者的詳細資訊，請參閱 [Active Directory User Discovery in Configuration Manager](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) (Configuration Manager 中的 Active Directory 使用者探索)。  

     由於應用程式類別目錄會從網站伺服器接收使用者可用的軟體清單，此設定不需要設定為 [True]  或 [是]  ，以便讓使用者查看，並從應用程式類別目錄要求應用程式。 不過，若此設定為 [False]  或 [否] 時，當使用者使用應用程式類別目錄時，下列各項將不會運作：  

    -   使用者不可安裝在應用程式類別目錄中看到的應用程式。  

    -   使用者將不會看到有關其應用程式核准要求的通知。 反之，他們必須重新整理應用程式類別目錄，並檢查核准狀態。  

    -   使用者將不會針對已發佈至應用程式類別目錄，接收應用程式的修訂和更新。 不過，他們將會在應用程式類別目錄中看到應用程式的變更資訊。  

    -   如果您在用戶端從應用程式類別目錄安裝應用程式後移除應用程式部署，用戶端會繼續檢查應用程式是否已安裝，最多 2 天的時間。  

     此外，當此設定為 [False]  或 [否] 時，使用者將不會接收您部署至使用者的必要應用程式，或包含於使用者原則中的其他管理操作。  

     此設定會在使用者的電腦位於內部網路和網際網路時套用到使用者；如果您也想啟用網際網路上的使用者原則，它必須設定為 [True]  或 [是]  。  

-   **從網際網路用戶端啟用使用者原則要求**  

     當用戶端和網站是針對以網際網路為基礎的用戶端管理所設定，而且您將此選項設定為 [True]  或 [是]  ，同時兩者皆套用下列條件時，使用者會在他們的電腦位於網際網路上時接收使用者原則：  

    -   [啟用用戶端的使用者原則輪詢]  用戶端設定為 [True]  或者 [在用戶端上啟用使用者原則]  設定為 [是] 。  

    -   以網際網路為基礎的管理點，可以使用 Windows 驗證 (Kerberos 或 NTLM) 成功驗證使用者。  

     如果將此選項保留為 [False]  或 [否] ，或任一個條件失敗，位於網際網路上的電腦將只會接收電腦原則。 在此案例中，使用者仍可從以網際網路為基礎的應用程式類別目錄查看、要求及安裝應用程式。 如果此設定為 [False]  或 [否]  ，但是 [啟用用戶端的使用者原則輪詢]  設定為 [True]  或者 [在用戶端上啟用使用者原則]  設定為 [是] ，除非電腦連線至內部網路，否則使用者將無法接收使用者原則。  

     如需管理網際網路用戶端的詳細資訊，請參閱 [System Center Configuration Manager 中端點之間的通訊](../../../core/plan-design/hierarchy/communications-between-endpoints.md)中的[從網際網路或未受信任之樹系進行用戶端通訊的考量](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。  

    > [!NOTE]  
    >  使用者的應用程式核准要求並不需要使用者原則或使用者驗證。  

##  <a name="a-namebkmkcompliancea-compliance-settings"></a><a name="BKMK_Compliance"></a> Compliance Settings  

-   **排程相容性評估**  

     按一下 [排程]  以建立預設排程，其會在使用者部署設定基準時會顯示給他們看。 此值可以在 [部署設定基準]  對話方塊中，針對各個基準進行設定。  

-   **啟用使用者資料和設定檔**  

     如果您想要將使用者資料和設定檔組態項目部署至階層中的 Windows 8 電腦，請選取 [是]  。  

     如需使用者資料和設定檔的詳細資訊，請參閱 [How to create user data and profiles configuration items in System Center Configuration Manager](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) (如何在 System Center Configuration Manager 中建立使用者資料和設定檔設定項目)。  

##  <a name="a-namebkmkcomputeragentdevicesettingsa-computer-agent"></a><a name="BKMK_ComputerAgentDeviceSettings"></a> 電腦代理程式  

-   **預設應用程式類別目錄網站點**  

     Configuration Manager 會使用此設定，從軟體中心連接使用者與應用程式類別目錄。 您可以依其 NetBIOS 名稱或 FQDN，指定裝載應用程式類別目錄網站點的伺服器，指定自動偵測，或指定自訂部署的 URL。 大部分情況下，自動偵測是最佳選擇，因為它提供下列優點：  

    -   如果網站包含應用程式類別目錄網站點，用戶端會自動從其網站指定應用程式類別目錄網站點。  

    -   針對 Rogue 伺服器提供保護，因為針對 HTTPS 所設定內部網路上的應用程式類別目錄網站點喜好設定，會高於未針對 HTTPS 所設定的應用程式類別目錄網站點。  

    -   當用戶端是針對內部網路和以網際網路為基礎的用戶端管理所設定，便可在這些用戶端位於網際網路時，為其指定以網際網路為基礎的應用程式類別目錄網站點，以及當這些用戶端位於內部網路時，為其指定以內部網際網路為基礎的應用程式類別目錄網站點。  

     自動偵測不保證會為用戶端指定最接近它們的應用程式類別目錄網站點。 您可能會因為下列原因而決定使用 [自動偵測]  ：  

    -   您可以手動為用戶端設定最接近的伺服器，或確定它們未連線至位於慢速網路連線的伺服器。  

    -   您想要控制哪些用戶端可以連線至哪些伺服器。 這可能基於測試、效能或商務因素。  

    -   您不想要等待至 25 小時，或使用不同的應用程式類別目錄網站點設定用戶端的網路變更。  

     如果您指定的是應用程式類別目錄網站點，而不是使用自動偵測，請指定 NetBIOS 名稱 (而不是內部網路 FQDN) 來協助降低當它們連線至內部網路上的應用程式類別目錄時，系統提示使用者提供認證的可能性。 若要使用 NetBIOS 名稱，必須滿足下列條件：  

    -   NetBIOS 名稱是在應用程式類別目錄網站點內容中指定的。  

    -   您在相同網域中使用 WINS 或所有用戶端，做為應用程式類別目錄網站點。  

    -   應用程式類別目錄網站點是針對 HTTP 用戶端連線所設定，或者是針對 HTTPS 用戶端連線所設定，而 Web 伺服器憑證包含 NetBIOS 名稱。  

     通常，系統會在 URL 包含 FQDN，而不是當 URL 為 NetBIOS 名稱時，提示使用者輸入認證。 當使用者從網際網路連線時，可預期系統永遠會提示使用者輸入認證，因為此連線必須使用網際網路 FQDN。 當使用者位於網際網路上時，系統會提示使用者輸入認證，以確定執行應用程式類別目錄網站點的伺服器可以連線至使用者帳戶的網域控制站，以便讓使用者使用 Kerberos 進行驗證。  

    > [!NOTE]  
    >  自動偵測的運作方式：  
    >   
    >  用戶端建立對管理點的服務位置要求。 如果與用戶端相同的網站包含應用程式類別目錄網站點，便會將此伺服器指定給用戶端，做為使用的應用程式類別目錄伺服器。 如果網站包含一個以上可用的應用程式類別目錄網站點，便會優先使用已啟用 HTTPS 的伺服器，再使用未啟用 HTTPS 的伺服器。 進行此篩選後，會為所有用戶端指定其中一個伺服器，作為應用程式類別目錄使用；Configuration Manager 不會在多部伺服器之間進行負載平衡。 若用戶端的網站未包含應用程式類別目錄網站點，管理點會無法確定要從階層傳回哪個應用程式類別目錄網站點。  
    >   
    >  當用戶端位於內部網路時，若已選取之應用程式類別目錄網站點是以應用程式類別目錄 URL 的 NetBIOS 名稱進行設定，便會為用戶端指定此 NetBIOS 名稱，而不是內部網路 FQDN。 當偵測到用戶端位於網際網路上時，只會為用戶端指定網際網路 FQDN。  
    >   
    >  用戶端會每隔 25 小時或偵測到網路變更時，建立此服務位置要求。 例如，若用戶端從內部網路移至網際網路，而且用戶端可以找到以網際網路為基礎的管理點，則以網際網路為基礎的管理點會為用戶端指定以網際網路為基礎的應用程式類別目錄網站點伺服器。  

-   **將預設應用程式類別目錄網站新增至 Internet Explorer 的信任的網站區域**  

     如果此選項設定為 [True]  或 [是] ，則會自動將目前的預設應用程式類別目錄網站 URL 新增至用戶端上 Internet Explorer 的信任網站區域。  

     此設定可確保不啟用受保護模式的 Internet Explorer 設定。 如果已啟用受保護模式，Configuration Manager 用戶端可能會無法從應用程式類別目錄安裝應用程式。 根據預設，信任的網站區域也支援使用者登入應用程式類別目錄，此動作需要進行 Windows 驗證。  

     如果您將此選項保持為 [False]，則 Configuration Manager 用戶端可能無法從應用程式類別目錄安裝應用程式，除非在另一個具有用戶端使用應用程式類別目錄 URL 的區域設定了這些 Internet Explorer 設定。  

    > [!NOTE]  
    >  每當 Configuration Manager 將預設的應用程式類別目錄新增至信任的站台區域，Configuration Manager 會移除 Configuration Manager 先前新增的預設應用程式類別目錄 URL，再增加新項目。  
    >   
    >  如果已在其中一個安全性區域中指定 URL，則 Configuration Manager 無法新增 URL。 在此案例中，您必須從其他區域移除 URL，或手動設定必要的 Internet Explorer 設定。  

-   **允許 Silverlight 應用程式在更高的信任模式下執行**  

     如果使用者執行 Configuration Manager 用戶端，並且使用應用程式類別目錄，則此設定必須設定為 [是]。  

     如果您變更此設定，此設定會在使用者下一次載入瀏覽器或重新整理目前開啟的瀏覽器視窗時生效。  

     如需此設定的詳細資訊，請參閱 [Security and Privacy for Application Management in Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md) (Configuration Manager 的應用程式管理安全性與隱私權) 中的 [Certificates for Silverlight 5 and Elevated Trust Mode Required for the Application Catalog](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5) (應用程式類別目錄需要 Microsoft Silverlight 5 憑證和更高的信任模式)。  

-   **顯示於軟體中心的組織名稱**  

     輸入使用者會在軟體中心看到的名稱。 此商標資訊可協助使用者將此應用程式識別為信任的來源。  

-   **使用新的軟體中心**  

     啟用時，這些用戶端設定的所有目標用戶端電腦都會使用新的軟體中心，這個軟體中心會顯示先前只可在 Silverlight 相依應用程式類別目錄中存取的使用者可用應用程式。  

     不過，仍然需要應用程式類別目錄網站點和應用程式類別目錄 Web 服務點站台系統角色，才能讓使用者可用的應用程式出現在軟體中心內。  

     如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃和設定應用程式管理](../../../apps/plan-design/plan-for-and-configure-application-management.md)。  

-   **安裝權限**  

    > [!WARNING]  
    >  此設定適用於應用程式類別目錄和軟體中心。 當使用者使用公司入口網站時，此設定不會有效用。  

     設定使用者如何起始軟體安裝、軟體更新和工作順序：  

    -   **所有使用者**：使用「來賓」以外的任何權限登入用戶端電腦的使用者，可以起始軟體安裝、軟體更新和工作順序。  

    -   **僅系統管理員**：登入用戶端電腦的使用者必須是本機系統管理員群組的成員，才能起始軟體安裝、軟體更新和工作順序。  

    -   **僅系統管理員和主要使用者**：登入用戶端電腦的使用者必須是本機系統管理員群組的成員或是電腦的主要使用者，才能起始軟體安裝、軟體更新和工作順序。  

    -   **無使用者**：登入用戶端電腦的使用者皆無法起始軟體安裝、軟體更新和工作順序。 電腦所需的部署務永遠會在期限前安裝，且使用者無法從應用程式類別目錄或軟體中心起始軟體安裝。  

-   **重新啟動時暫停輸入 BitLocker PIN**  

     如果已在電腦上設定 BitLocker PIN 項目，此選項可以在軟體安裝後重新啟動電腦時，略過輸入 PIN 的需求。  

    -   **永遠**：Configuration Manager 會在安裝需要重新啟動的軟體，以及起始電腦重新啟動後暫停在下一次電腦啟動時輸入 PIN 的 BitLocker 需求。 此設定僅適用於由 Configuration Manager 起始的電腦重新啟動，並且於使用者重新啟動電腦時，不會暫停輸入 BitLocker PIN 的需求。 BitLocker PIN 輸入需求會在 Windows 啟動後繼續作用。  

    -   **永不**：在下一次安裝需要重新啟動的軟體後電腦啟動時，Configuration Manager 不會暫停輸入 PIN 的 BitLocker 需求。 在此案例中，除非使用者輸入 PIN 完成標準啟動程序及載入 Windows，否則無法完成軟體安裝。  

-   **其他軟體會管理應用程式和軟體更新的部署**  

     只有在下列其中一個條件成立時，才能啟用此選項：  

    -   您可以使用需要啟用此設定的廠商解決方案。  

    -   您可以使用 Configuration Manager 軟體部署套件 (SDK) 來管理用戶端代理程式通知，以及應用程式及軟體更新的安裝。  

    > [!WARNING]  
    >  如果您在任一情況適用時選取此選項，則不會在用戶端上安裝軟體更新和必要的應用程式。 此設定不會防止使用者從應用程式類別目錄安裝應用程式，或防止在用戶端電腦上安裝套件和程式，以及工作順序。  

-   **PowerShell 執行原則**  

     設定 Configuration Manager 用戶端執行 Windows PowerShell 指令碼的方式。 這些指令碼通常用於偵測設定項目的相容性設定，但也可以在部署時傳送，以做為標準的指令碼。  

    -   **略過**：Configuration Manager 用戶端會略過用戶端電腦上的 Windows PowerShell 設定，使得未經簽署的指令碼得以執行。  

    -   **限制**：Configuration Manager 用戶端會使用用戶端電腦上目前的 Windows PowerShell 設定，判斷是否可以執行未經簽署的指令碼。  

    -   **所有已簽署項目**：Configuration Manager 用戶端只會執行經由受信任發行者簽署的指令碼。 此項限制與用戶端電腦上目前的 Windows PowerShell 設定無關。  

     這個選項至少需要 Windows PowerShell 2.0 版，且預設值為 [所有已簽署項目] 。  

    > [!TIP]  
    >  如果未經簽署的指令碼因為此項用戶端設定而無法執行，Configuration Manager 會透過下列方式回報此錯誤：  
    >   
    >  -   錯誤識別碼 **0X87D00327** 和**未簽署指令碼**的描述，會在 Configuration Manager 主控台的 [監視] 工作區中列為部署狀態錯誤。  
    > -   [0X87D00327]  的錯誤碼和描述，以及 [未簽署指令碼]  或 [0X87D00320]  和 [尚未安裝指令碼裝載]  在報告中具有 [探索錯誤]  ，例如 [資產的設定基準中設定項目的錯誤詳細資料] 。  
    > -   **Script is not signed (Error: 87D00327; Source: CCM)** 檔案中的訊息 **DcmWmiProvider.log** 。  

-   **停用期限隨機設定**  

     此設定可判斷用戶端是否使用最多兩個小時的啟用延遲，以便在期限到達時安裝必要的軟體更新。 預設會停用啟用延遲功能。  

     對於虛擬桌面基礎結構 (VDI) 案例，此延遲時間有助於分散 CPU 處理執行，以及電腦的資料傳送，而該電腦具有多部執行 Configuration Manager 用戶端的虛擬機器。 即使您未使用 VDI，若許多用戶端同時安裝相同的更新，可能會增加網站伺服器上的 CPU 使用量、使發佈點速度變慢，以及大幅降低可用的網路頻寬。  

     如果在設定期限到達時必須在沒有延遲的情況下安裝所需的軟體更新，請針對此設定選取 [是]  。  

##  <a name="a-namebkmkcomputerrestartdevicesettingsa-computer-restart"></a><a name="BKMK_ComputerRestartDeviceSettings"></a> 電腦重新啟動  
 當您指定這些電腦重新啟動設定時，請確定持續時間中短暫的重新啟動通知間隔值和最終倒數間隔值比套用至電腦的維護期間短。  

 如需維護時段的詳細資訊，請參閱[如何使用 System Center Configuration Manager 的維護期間](../../../core/clients/manage/collections/use-maintenance-windows.md)。  

##  <a name="a-namebkmkendpointprotectiondevicesettingsa-endpoint-protection"></a><a name="BKMK_EndpointProtectionDeviceSettings"></a> Endpoint Protection  

-   **在用戶端電腦上管理 Endpoint Protection 用戶端**  

     如果您想在階層中的電腦上管理現有的 Endpoint Protection 用戶端，請選取 [True] 或 [是]。  

     如果您已安裝 Endpoint Protection 用戶端，且想要使用 Configuration Manager 進行管理，請選取此選項。  

     此外，如果您想要建立指令碼以解除安裝現有的反惡意程式碼解決方案、安裝 Endpoint Protection 用戶端，以及使用 Configuration Manager 應用程式或套件及程式部署此指令碼，請選取此選項。  

-   **在用戶端電腦上安裝 Endpoint Protection 用戶端**  

     請選取 [True] 或 [是]，在尚未安裝的用戶端電腦上安裝並啟用 Endpoint Protection 用戶端。  

    > [!NOTE]  
    >  如果已安裝 Endpoint Protection 用戶端，選取 [False]  或 [否]  將不會解除安裝 Endpoint Protection 用戶端。 若要解除安裝 Endpoint Protection 用戶端，請將 [在用戶端電腦上管理 Endpoint Protection 用戶端]  用戶端設定設為 [False]  或 [否] ，然後部署套件和程式以解除安裝 Endpoint Protection 用戶端。  

-   **針對具有寫入篩選器的 Windows Embedded 裝置，認可 Endpoint Protection 用戶端安裝 (需要重新啟動)**  

     選取 [是]  以便在 Windows Embedded 裝置上停用寫入篩選器，並重新啟動裝置。 這麼做就表示認可該裝置上的安裝。  

     如果指定的是 [否]  ，則會在裝置重新啟動時已清除的暫時重疊上安裝用戶端。 在此案例中，Endpoint Protection 用戶端會等到其他安裝認可裝置的變更後，才被認可。 這是預設設定。  

-   **安裝 Endpoint Protection 用戶端後抑制任何必要的電腦重新啟動**  

     安裝 Endpoint Protection 用戶端之後，如有必要，請選取 [True] 或 [是] 來抑制電腦重新啟動。  

    > [!IMPORTANT]  
    >  如果 Endpoint Protection 用戶端需要電腦重新啟動，且此設定配置為 [False] ，則會執行重新啟動，而不管是否已設定任何維護期間。  

-   **使用者可以延遲必要的重新啟動以完成 Endpoint Protection 安裝的允許期限 (小時)**  

     指定使用者可以延遲電腦重新啟動的時數 (如果在安裝 Endpoint Protection 用戶端後需要)。 這個選項只有在 [安裝 Endpoint Protection 用戶端後抑制任何必要的電腦重新啟動] 選項設為 [False] 時才可以設定。  

-   **針對用戶端電腦上的初始定義更新停用替代來源 (例如 Microsoft Windows Update、Microsoft Windows Server Update Services 或 UNC 路徑)**  

     如果您想要 Configuration Manager 在用戶端電腦上只安裝初始定義更新，請選取 [True] 或 [是]。 此設定有助於在定義更新的初始安裝期間避免不必要的網路連線，並可降低網路頻寬。  

##  <a name="a-namebkmkhardwareinventorydevicesettingsa-hardware-inventory"></a><a name="BKMK_HardwareInventoryDeviceSettings"></a> 硬體清查  

-   **自訂 MIF 檔案大小上限 (KB)**  

     指定大小上限 (以 KB 為單位)，允許在硬體清查週期進行期間，從用戶端收集各個自訂的管理資訊格式 (MIF) 檔案。 如果有任何 MIF 檔案超過此大小，則不會由 Configuration Manager 硬體清查處理。 您可以指定介於 1 和 5,000 KB 之間的大小。 根據預設，此值設為 250 KB。 此設定不會影響一般硬體清查資料檔案的大小。  

    > [!NOTE]  
    >  此設定僅適用於預設用戶端設定。  

-   **硬體清查類別**  

     在 Configuration Manager 中，您可以延伸從用戶端收集的硬體資訊，不需手動編輯 sms_def.mof 檔案。 如果您想要擴充 Configuration Manager 硬體清查，請按一下 [設定類別]。 如需詳細資訊，請參閱 [How to configure hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/configure-hardware-inventory.md) (如何設定 System Center Configuration Manager 中的硬體清查)。  

-   **收集 MIF 檔案**  

     使用此設定，指定是否要在硬體清查期間從 Configuration Manager 用戶端收集管理資訊格式 (MIF) 檔案。  

     對於要由硬體清查收集的 MIF 檔案，必須位於用戶端電腦的正確位置。 根據預設，這些檔案應位於以下位置：  

    -   IDMIF 檔案應位於 Windows\System32\CCM\Inventory\Idmif 資料夾中。  

    -   NOIDMIF 檔案應位於 Windows\System32\CCM\Inventory\Noidmif 資料夾中。  

    > [!NOTE]  
    >  此設定僅適用於預設用戶端設定。  

##  <a name="a-namebkmkmeteredinternetconnetionssettingsa-metered-internet-connections"></a><a name="BKMK_MeteredInternetConnetionsSettings"></a> 計量付費網際網路連線  
 您可以管理 Windows 8 用戶端電腦與 Configuration Manager 站台在使用計量付費網際網路連線時的通訊方式。 在您處於計量付費網際網路連線時，網際網路提供者有時會根據您傳送和接收的資料量來收取費用。  

> [!NOTE]  
>  在下列案例中，不會將已設定的用戶端設定套用至 Windows 8 用戶端電腦：  
>   
>  -   位於漫遊資料連線的電腦：Configuration Manager 用戶端不會執行任何需要將資料傳送至 Configuration Manager 站台的作業。  
> -   Windows 網路連線內容設定為非計量付費：Configuration Manager 用戶端會以非計量付費網際網路連線運作，並傳送資料至 Configuration Manager 站台。  

-   **計量付費網際網路連線上的用戶端通訊**  

     從下拉式清單中選擇下列其中一個 Windows 8 用戶端電腦：  

    -   **允許**：允許所有用戶端透過計量付費網際網路進行通訊，除非用戶端裝置使用的是漫遊資料連線。  

    -   **限制**：只有下列用戶端通訊允許透過計量付費網際網路連線進行：  

        -   擷取用戶端原則  

        -   傳送至網站的用戶端狀態訊息  

        -   使用應用程式類別目錄提出軟體安裝要求  

        -   必要的部署 (到達安裝期限時)  

        > [!IMPORTANT]  
        >  如果使用者從軟體中心或應用程式類別目錄起始軟體安裝，這些動作皆允許執行，而不管計量付費網際網路連線設定為何。  

         如果達到計量付費網際網路連線的資料傳送限制，用戶端便不再嘗試與 Configuration Manager 站台通訊。  

    -   **封鎖**：Configuration Manager 用戶端不會在位於計量付費網際網路連線時，嘗試與 Configuration Manager 站台通訊。 這是預設值。  

##  <a name="a-namebkmkpowmgmtdevicesettingsa-power-management"></a><a name="BKMK_PowMgmtDeviceSettings"></a> 電源管理  

-   **允許使用者從電源管理排除其裝置**  

     從下拉式清單選取 [True]  或 [是]  ，以允許軟體中心的使用者將他們的電腦從所有設定的電源管理設定中排除。  

-   **啟用喚醒 Proxy**  

     指定 [是]  ，以便在其針對單點傳播封包設定時補充網站的網路喚醒設定。  

     如需喚醒 Proxy 的詳細資訊，請參閱 [Plan how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md) (規劃如何在 System Center Configuration Manager 中喚醒用戶端)。  

    > [!WARNING]  
    >  請勿在不了解運作方式並在測試環境中進行評估的情況下，於生產網路中啟用喚醒 Proxy。  

-   **喚醒 Proxy 連接埠號碼 (UDP)**  

     為主管電腦用於傳送喚醒封包至睡眠電腦的連接埠號碼保留預設值，或變更為您所選擇的值。  

     當您設定 [喚醒 Proxy 的 Windows 防火牆例外]  選項時，會自動為執行 Windows 防火牆的用戶端設定此處指定的連接埠號碼。 如果用戶端執行不同的防火牆，您必須手動將其設定為允許此設定所指定的 UDP 連接埠號碼。  

-   **網路喚醒連接埠號碼 (UDP)**  

     除非您已在網站 [內容] 的 [連接埠]  索引標籤中變更網路喚醒 (UDP) 連接埠號碼，否則請保留預設值 9。  

    > [!IMPORTANT]  
    >  此號碼必須符合 [內容] 中的號碼。 如果您在一個位置變更這個號碼，則不會在另一個位置進行自動更新。  

##  <a name="a-namebkmkremotetoolsdevicesettingsa-remote-tools"></a><a name="BKMK_RemoteToolsDeviceSettings"></a> 遠端工具  

-   **在用戶端上啟用遠端控制** 的錯誤碼和描述，以及 [未簽署指令碼] **防火牆例外設定檔**  

     選取是否要針對接收這些用戶端設定的所有用戶端電腦，啟用 Configuration Manager 遠端控制。 按一下 [設定]  以啟用遠端控制，並可選擇設定防火牆設定，以允許在用戶端電腦上使用遠端控制。  

     遠端控制預設為停用。  

    > [!IMPORTANT]  
    >  如果未設定防火牆，遠端控制可能無法正確運作。  

-   **使用者可以在軟體中心變更原則或通知設定**  

     選取使用者是否可以從軟體中心內變更遠端控制選項。  

-   **允許遠端控制無人看管的電腦**  

     選取系統管理員是否可以使用遠端控制來存取登出或鎖定的用戶端電腦。 當此設定停用時，只能對登入和解除鎖定的電腦進行遠端控制。  

-   **提示使用者提供遠端控制權限**  

     選取用戶端電腦是否會先顯示詢問使用者權限的訊息，再允許遠端控制工作階段。  

-   **將遠端控制權限授與本機系統管理員群組**  

     選取起始遠端控制連線之伺服器上的本機系統管理員，是否可以建立用戶端電腦的遠端控制工作階段。  

-   **允許的存取層級**  

     指定允許的遠端控制存取的層級。 您可以選擇：  

    -   完全控制  

    -   僅限檢視  

    -   無  

-   **獲准檢視器**  

     按一下 [設定檢視器]  以開啟 [設定用戶端設定]  對話方塊，並指定可與用戶端電腦建立遠端控制工作階段的 Windows 使用者名稱。  

-   **在工作列上顯示工作階段通知圖示**  

     選取此選項，在用戶端電腦的工作列上顯示圖示，以表示遠端控制作業階段目前作用中。  

-   **顯示工作階段連線列**  

     選取此選項，在用戶端電腦上顯示高可見度的工作階段連線列，以表示遠端控制作業階段目前作用中。  

-   **在用戶端上播放音效**  

     選取此選項，使用音效來表示用戶端電腦上的遠端控制工作階段為作用中。 您可以在工作階段連線或中斷連線時播放音效，或者在工作階段進行期間重複播放音效。  

-   **管理未請求遠端協助設定**  

     選取此選項，讓 Configuration Manager 管理未請求的遠端協助工作階段。  

     未請求遠端協助工作階段，即是用戶端電腦的使用者未要求協助以起始工作階段。  

-   **管理請求遠端協助設定**  

     選取此選項，讓 Configuration Manager 管理請求的遠端協助工作階段。  

     請求遠端協助工作階段，即是用戶端電腦的使用者傳送要求給系統管理員尋求遠端協助。  

-   **遠端協助的存取層級**  

     選取要指派給在 Configuration Manager 主控台起始之遠端協助工作階段的存取層級。  

    > [!NOTE]  
    >  用戶端電腦上的使用者必須授與權限，才能進行遠端協助工作階段。  

-   **管理遠端桌面設定**  

     選取此選項，讓 Configuration Manager 管理電腦的遠端桌面工作階段。  

-   **允許獲准的檢視器使用遠端桌面連線進行連線**  

     選取此選項，讓獲准檢視器清單中指定的使用者得以加入至用戶端電腦上的遠端桌面本機使用者群組。  

-   **在執行 Windows Vista 作業系統和更新版本的電腦上需要網路層級驗證**  

     如果您想要使用網路層級驗證來與執行 Windows Vista 作業系統和更新版本的用戶端電腦建立遠端桌面連線，請選取這個更安全的選項。 網路層級驗證最初所需的遠端電腦資源較少，因為它會在建立遠端桌面連線之前完成使用者驗證。 此方法更安全，因為它可協助保護電腦不受惡意使用者或軟體的影響，同時也可以降低遭到拒絕服務攻擊的風險。  

##  <a name="a-namebkmksoftwaredeploymentdevicesettingsa-software-deployment"></a><a name="BKMK_SoftwareDeploymentDeviceSettings"></a> 軟體部署  

-   **排程部署的重新評估**  

     設定排程，讓 Configuration Manager 重新評估所有部署的需求規則。 預設值為每 7 天執行一次。  

    > [!IMPORTANT]  
    >  建議您不要將此值變更為比預設值低的值，因為這麼做可能會對您的網路及用戶端電腦效能造成負面影響。  

     您也可以在 [控制台] 中，於 **Configuration Manager** 的 [動作] 索引標籤選取 [應用程式部署評估週期] 動作，從 Configuration Manager 用戶端電腦起始這個動作。  

##  <a name="a-namebkmksoftinventorydevicesettingsa-software-inventory"></a><a name="BKMK_SoftInventoryDeviceSettings"></a> 軟體清查  

-   **清查報告詳細資料**  

     指定要清查的檔案資訊層級。 您只可以清查與檔案相關的詳細資料、與產品相關聯之檔案的詳細資料，或可清查與檔案相關的所有資訊。  

-   **清查這些檔案類型**  

     如果想要指定要清查的檔案類型，請按一下 [設定類型]  ，然後在 [設定用戶端設定]  對話方塊中設定下列設定：  

    > [!NOTE]  
    >  如果有多個自訂用戶端設定套用到電腦，便會將各個設定所傳回的清查合併。  

    -   按一下 [新增] 圖示新增新檔案類型至清查，然後在 [已清查的檔案內容]  對話方塊中指定下列資訊：  

    -   **名稱** – 提供您要清查的檔案名稱。 您可以使用 [*] **\*** 字元來表示任何文字字串，以及使用 []  字元來表示任何單一字元。 例如，若您想要清查所有副檔名為 .doc 的檔案，請指定檔案名稱 **\*.doc**。  

    -   **位置** – 按一下 [設定]  開啟 [路徑內容]  對話方塊。 您可以將軟體清查設定為搜尋所有用戶端硬碟的指定檔案、搜尋指定的路徑 (例如 **C:\Folder**) 或指定的變數 (例如 *%windir%*)，而且您也可以搜尋指定路徑下的所有子資料夾。  

    -   **排除加密和壓縮檔案** – 當您選取此選項時，將不會清查任何已壓縮或已加密的檔案。  

    -   **排除 Windows 資料夾中的檔案** – 當您選取此選項時，將不會清查 Windows 資料夾及其子資料夾中的檔案。  

    -   按一下 [確定]  以關閉 [已清查的檔案內容]  對話方塊。  

    -   新增您要清查的所有檔案，然後按一下 [確定]  以關閉 [設定用戶端設定]  對話方塊。  

-   **收集檔案**  

     如果您想要從用戶端電腦收集檔案，請按一下 [設定檔案]  再設定下列各項：  

    > [!NOTE]  
    >  如果有多個自訂用戶端設定套用到電腦，便會將各個設定所傳回的清查合併。  

    -   在 [設定用戶端設定]  對話方塊中，按一下新增圖示以新增要收集的檔案。  

    -   在 [收集到的檔案內容]  對話方塊中，提供下列資訊：  

    -   **名稱** – 提供您要收集的檔案名稱。 您可以使用 [*] **\*** 字元來表示任何文字字串，以及使用 []  字元來表示任何單一字元。  

    -   **位置** – 按一下 [設定]  開啟 [路徑內容]  對話方塊。 您可以將軟體清查設定為搜尋您要收集的所有用戶端硬碟檔案、搜尋指定的路徑 (例如 **C:\Folder**) 或指定的變數 (例如 *%windir%*)，而且您也可以搜尋指定路徑下的所有子資料夾。  

    -   **排除加密和壓縮檔案** – 當您選取此選項時，將不會收集任何已壓縮或已加密的檔案。  

    -   **當檔案大小總計超過下列大小時停止檔案收集 (KB)** – 指定檔案大小 (以 KB 為單位)，使 [名稱]  下所指定的檔案在超過該大小時將不再被收集。  

        > [!NOTE]  
        >  站台伺服器會收集所收集檔案中最近五個變更的版本，並將它們儲存在 *&lt;Configuration Manager 安裝目錄\>***\Inboxes\Sinv.box\Filecol** 目錄中。 如果自從上次收集軟體清查以來未變更檔案，則不會再收集該檔案。  
        >   
        >  軟體清查不會收集大於 20 MB 的檔案。  
        >   
        >  [設定用戶端設定]  對話方塊中的 [所有收集到的檔案的大小上限 (KB)]  值會顯示所有已收集檔案的大小上限。 達到此大小時，將會停止檔案收集。 已收集的檔案會保留並傳送到網站伺服器。  

        > [!IMPORTANT]  
        >  如果您將軟體清查設定為收集許多大檔案，可能會對您的網路和網站伺服器的效能造成負面影響。  

         如需如何檢視收集到之檔案的資訊，請參閱 [How to use Resource Explorer to view software inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) (如何在 System Center Configuration Manager 中使用資源總管檢視軟體清查)。  

    -   按一下 [確定]  以關閉 [收集到的檔案內容]  對話方塊。  

    -   新增您要收集的所有檔案，然後按一下 [確定]  以關閉 [設定用戶端設定]  對話方塊。  

-   **設定名稱**  

     軟體清查期間，系統會從安裝在網站內的用戶端上的檔案的標頭資訊擷取製造商名稱與產品名稱。 因為這些名稱並未在標頭資訊中標準化，在資源總管內檢視軟體清查資訊或執行查詢時，有時會顯示相同製造商或產品的不同版本名稱。 如果您想標準化這些顯示名稱，請按一下 [設定名稱]  ，然後在 [設定用戶端設定]  對話方塊中設定下列項目：  

    -   **名稱類型：** 軟體清查收集有關製造商與產品的資訊。 從下拉式選單選取您想要設定 [製造商]  或 [產品] 的顯示名稱。  

    -   **顯示名稱：** 指定您想要的顯示名稱，以取代 [已清查的名稱]  清單中的名稱。 您可以按一下 [新增] 圖示以指定新的顯示名稱。  

    -   **已清查的名稱** ：按一下新增圖示加入新的已清查名稱，它將會在軟體清查中以 [顯示名稱]  清單中選取的名稱來取代。 您可以新增將被取代的多個名稱。  

##  <a name="a-namebkmksoftwareupdatesdevicesettinga-software-updates"></a><a name="BKMK_SoftwareUpdatesDeviceSetting"></a> 軟體更新  

-   **啟用用戶端上的軟體更新**  

     使用這項設定以啟用 Configuration Manager 用戶端上的軟體更新。 如果您清除此設定，Configuration Manager 會從用戶端移除現有部署原則。 重新啟用這項設定時，用戶端會下載目前的部署原則。  

    > [!IMPORTANT]  
    >  清除這項設定時，NAP 與倚賴軟體更新裝置設定的相容性設定原則將不再有作用。  

-   **軟體更新掃描排程**  

     使用此設定以指定用戶端啟動軟體更新相容性評估掃描的頻率。 相容性評估掃描可判斷用戶端上軟體更新的狀態 (例如，必要或是已安裝)。 如需相容性評估的詳細資訊，請參閱 [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance) (軟體更新相容性評估)。  

     系統會根據預設值使用簡易排程，每 7 天就會進行一次相容性掃描。 您可以選擇建立自訂排程以指定確切的開始日期與時間，選擇是否使用 UTC 或本機時間，並且設定一週內的特定日期為週期性間隔。  

    > [!NOTE]  
    >  如果您指定的間隔少於 1 天，Configuration Manager 將自動預設為 1 天。  

    > [!WARNING]  
    >  用戶端電腦上的實際開始時間是開始時間加上最多 2 小時的隨機時數。 這樣可避免用戶端電腦啟動掃描並同時連線至主動式軟體更新點伺服器上的 Windows Server Update Services (WSUS)。  

-   **排程部署重新評估**  

     使用此設定值以設定軟體更新用戶端代理程式重新評估軟體更新的頻率，以取得 Configuration Manager 用戶端電腦上的安裝狀態。 如果在用戶端電腦上找不到之前安裝的軟體更新，但其為必要的更新時，系統會重新安裝這些更新。 您必須根據公司的軟體更新相容性原則、使用者是否有能力解除安裝軟體更新，並考量每個部署重新評估週期所造成的一些網路和用戶端電腦 CPU 活動來調整部署重新評估排程。 根據預設值，系統會使用簡易排程，每 7 天就會進行部署重新評估掃描一次。  

    > [!NOTE]  
    >  如果您指定的間隔少於 1 天，Configuration Manager 將自動預設為 1 天。  

-   **當達到任何軟體的更新期限時，安裝更新期限在指定期間內的所有其他軟體更新部署**  

     使用此設定以安裝必要部署中的所有軟體更新，且其更新期限位於指定的期間內。 當達到必要軟體更新部署的更新期限時，安裝會在用戶端上啟動以進行部署中的軟體更新。 此設定會決定是否需要同時啟動其他必要部署中定義的軟體更新安裝，這些部署的設定期限也位於指定的期間內。  

     使用此設定可加速必要軟體更新的軟體更新安裝，並可提高安全性、減少顯示通知以及減少系統在用戶端電腦重新啟動的次數。 根據預設不會啟用此設定。  

-   **期限在這段時間內的所有擱置中部署也會安裝的一段時間**  

     使用此設定以指定先前設定的時間範圍。 您可以輸入的值為 1 到 23 小時以及 1 到 365 天。 根據預設，這項設定設定為 7 天。  

##  <a name="a-namebkmkuserdeviceaffinitydevicesettingsa-user-and-device-affinity"></a><a name="BKMK_UserDeviceAffinityDeviceSettings"></a> 使用者和裝置親和性  

-   **使用者裝置親和性使用閾值 (分鐘)**  

     指定 Configuration Manager 建立使用者裝置親合型對應之前的分鐘數。  

-   **使用者裝置親和性使用閾值 (天)**  

     指定衡量使用親和性閾值的天數。  

    > [!NOTE]  
    >  例如，若指定的 [使用者裝置親和性使用閾值 (分鐘)]  為 **60** 分鐘，且 [使用者裝置親和性閾值 (天)]  為 **5** 天，則使用者在 5 天內必須使用該裝置 60 分鐘，才會自動建立使用者裝置親和性。  

-   **從使用資料自動設定使用者裝置親和性**  

     選取 [True] 或 [是]，讓 Configuration Manager 得以根據所收集的使用量資訊，自動建立使用者裝置親和性。  

## <a name="client-cache-settings"></a>用戶端快取設定

- **設定用戶端快取大小**

  Windows 電腦使用用戶端快取資料夾儲存用以安裝應用程式和程式的暫存檔案。 從 1606 版開始，選取 [是] 使用 [最大快取大小] 的設定來指定用戶端快取資料夾大小。 如果設為 [否]，則用戶端快取資料夾的預設值為 5120 MB。

  於用戶端安裝期間可以設定其他用戶端快取內容。 如需詳細資訊，請參閱 [Configure the Client Cache for Configuration Manager Clients](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache)。

- **最大快取大小 (MB)**

  從 1606 版開始，以 MB 為單位指定用戶端快取資料夾的大小上限。

- **最大快取大小 (磁碟百分比)** (從 1606 版開始)

  從 1606 版開始，以磁碟百分比指定用戶端快取資料夾的大小上限。

##  <a name="a-namebkmkmobiledevicesusersettingsa-mobile-devices"></a><a name="BKMK_MobileDevicesUserSettings"></a> 行動裝置  

-   **行動裝置註冊設定檔**  

     設定這項設定前，您必須先為行動裝置使用者設定 [允許使用者註冊行動裝置]  設定為 [True] 。 然後，您可以按一下 [設定設定檔]  以指定包含有關在註冊程序使用的憑證範本、包含註冊點與註冊 Proxy 點的網站以及將在註冊後管理裝置的網站等資訊的註冊設定檔。  

    > [!IMPORTANT]  
    >  設定這項選項之前，確定您已經為行動裝置註冊設定憑證範本。  

##  <a name="a-namebkmkenrollmentusersettingsa-enrollment"></a><a name="BKMK_EnrollmentUserSettings"></a> 註冊  

-   **行動裝置註冊設定檔**  

     設定此設定前，您必須先為註冊使用者設定 [允許使用者註冊行動裝置和 Mac 電腦]  設定為 [是] 。 然後，您可以按一下 [設定設定檔]  以指定包含有關在註冊程序使用的憑證範本、包含註冊點與註冊 Proxy 點的網站以及將在註冊後管理裝置的網站等資訊的註冊設定檔。  

    > [!IMPORTANT]  
    >  設定這項選項之前，確定您已經為行動裝置註冊或 Mac 用戶端憑證註冊設定憑證範本。  

##  <a name="a-namebkmkuserdeviceaffinityusersettingsa-user-and-device-affinity"></a><a name="BKMK_UserDeviceAffinityUserSettings"></a> 使用者和裝置親和性  

-   **允許使用者定義其主要裝置**  

     指定是否允許使用者從應用程式類別目錄的 [我的裝置]  索引標籤識別其主要裝置。  



<!--HONumber=Nov16_HO1-->

