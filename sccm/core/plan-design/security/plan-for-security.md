---
title: "在 System Center Configuration Manager 中規劃安全性 | Microsoft Docs"
description: "取得 System Center Configuration Manager 的安全性最佳做法與相關資訊。"
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
caps.latest.revision: 6
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: af06fb10d905e3fe447c6cd6ed35dac10488161f
ms.openlocfilehash: 1bf519ad4593f6a08d7dc393f9fab91c70b51b25
ms.contentlocale: zh-tw
ms.lasthandoff: 01/05/2017


---
# <a name="plan-for-security-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中規劃安全性

適用於：System Center Configuration Manager (最新分支)

##  <a name="BKMK_PlanningForCertificates"></a> 規劃憑證 (自我簽署與 PKI)  
 Configuration Manager 使用自我簽署憑證及公開金鑰基礎結構 (PKI) 憑證的組合。  

 盡可能使用 PKI 憑證，因為它是安全性最佳作法。 如需 PKI 憑證需求的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../core/plan-design/network/pki-certificate-requirements.md)。 當 Configuration Manager 要求 PKI 憑證時 (例如註冊行動裝置和 Intel 主動管理技術 (AMT) 佈建期間)，您必須使用 Active Directory 網域服務和企業憑證授權單位。 對於其他所有 PKI 憑證，您必須從 Configuration Manager 獨立部署和管理這些憑證。  

 當用戶端電腦連線到以網際網路為基礎的站台系統時，也需要使用 PKI 憑證，而且當用戶端連線到執行 Internet Information Services (IIS) 的站台系統時，亦建議使用 PKI 憑證。 如需用戶端通訊的詳細資訊，請參閱 [如何在 System Center Configuration Manager 中設定用戶端通訊連接埠](../../../core/clients/deploy/configure-client-communication-ports.md)。  

 使用 PKI 時，您也可利用 IPsec 協助保護站台內站台系統之間和站台之間的伺服器對伺服器通訊，以及電腦之間其他的資料傳輸。 IPsec 實作不受 Configuration Manager 影響。  

 當無 PKI 憑證可用時，Configuration Manager 可自動產生自我簽署憑證，而 Configuration Manager 中的有些憑證一律會自我簽署。 在大部分情況下，Configuration Manager 會自動管理自我簽署憑證，您不需要採取額外動作。 一種可能的例外狀況是網站伺服器簽署憑證。 網站伺服器簽署憑證永遠會自我簽署，確保用戶端從管理點下載的用戶端原則已從網站伺服器送出，且未遭竄改。  

### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a>規劃站台伺服器簽署憑證 (已自我簽署)  
 用戶端可從 Active Directory 網域服務及用戶端推入安裝，安全地取得一份網站伺服器簽署憑證複本。 如果用戶端無法利用這些機制的其中一種來取得一份網站伺服器簽署憑證複本，當您安裝用戶端時，便可安裝網站伺服器簽署憑證，因為它是安全性最佳做法。 這對於第一次從網際網路與網站通訊的用戶端尤其重要，因為管理點若連線到不受任信的網路，很容易遭受攻擊。 如果不採用這個額外步驟，用戶端便會自動從管理點下載一份網站伺服器簽署憑證複本。  

 用戶端無法安全地取得一份網站伺服器簽署憑證複本的情況，如下所述：  

-   您未利用用戶端推入來安裝用戶端，且以下任何一項條件為 True 時：  

    -   Active Directory 架構未針對 Configuration Manager 擴充。  

    -   用戶端的網站未向 Active Directory 網域服務發佈。  

    -   用戶端來自不受信任的樹系或工作群組。  

-   當用戶端在網際網路時，您會安裝用戶端。  

##### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>安裝用戶端和一份網站伺服器簽署憑證複本  

1.  找出用戶端之主要站台伺服器上的站台伺服器簽署憑證。 此憑證是儲存在 [SMS] 憑證存放區中，主體名稱為 [站台伺服器]，易記名稱為 [站台伺服器簽署憑證]。  

2.  匯出不含私密金鑰的憑證，將檔案儲存在安全的地方，只從安全通道存取該檔案 (例如，使用伺服器訊息區 (SMB) 簽署或 IPsec)。  

3.  使用 Client.msi 內容 **SMSSIGNCERT=**&lt;完整路徑和檔案名稱\> 和 CCMSetup.exe 安裝用戶端。  

###  <a name="BKMK_PlanningForCRLs"></a> 規劃 PKI 憑證撤銷  
與 Configuration Manager 搭配使用 PKI 憑證時，規劃用戶端和伺服器如何及是否使用憑證撤銷清單 (CRL) 確認連線電腦上的憑證。 CRL 是憑證授權單位 (CA) 所建立並簽署的檔案，它有一份由 CA 簽發但撤銷的憑證清單。 例如，如果已簽發的憑證已知或有遭到洩露的可能時，CA 管理員便可以撤銷憑證。  

> [!IMPORTANT]  
>  由於 CA 簽發憑證時會將 CRL 的位置加入到憑證中，因此請確實在您部署 Configuration Manager 將使用的任何 PKI 憑證之前，先規劃 CRL。  

根據預設，IIS 一律會檢查用戶端憑證的 CRL，您無法在 Configuration Manager 中變更這項設定。 Configuration Manager 用戶端預設一律會檢查 CRL 有無站台系統。 您可以指定站台內容和 CCMSetup 內容來停用此設定。 當您在管理 Intel AMT 型電腦超出訊號範圍時，也可以針對超出訊號範圍服務點及執行超出訊號範圍管理主控台的電腦啟用 CRL 檢查。  

如果電腦使用憑證撤銷檢查，卻無法找出 CRL 時，電腦的反應就像憑證鏈中所有的憑證都已被撤銷一樣，因為無法驗證為何清單中沒有這些憑證。 在此案例中，所有需要憑證且使用 CRL 的連線皆告失敗。  

在每一次使用憑證時檢查 CRL，如此可提供比使用已撤銷之憑證更多的安全性，但同時也會造成用戶端連線延遲及額外的處理工作。 當用戶端在網際網路或在不受信任的網路上時，您更需要這項額外的安全性檢查。  

在判定 Configuration Manager 用戶端是否須檢查 CRL 之前，請先向您的 PKI 管理員查詢。之後，當以下兩項條件為 True 時，再考慮保留 Configuration Manager 中啟用的這個選項：  

-   您的 PKI 基礎結構支援 CRL，且會發佈在所有 Configuration Manager 用戶端都可找到它的地方。 請記住，如果您正在使用以網際網路為基礎的用戶端管理，且用戶端位於不受信任的樹系時，網際網路上的用戶端可能就會包含在內。  

-   檢查每一個站台系統 (其設定為使用 PKI 憑證) 連線的 CRL 需求，遠大於對用戶端更快速連線及更有效處理的需求，以及用戶端找不到 CRL 時無法連線到伺服器的風險。  

###  <a name="BKMK_PlanningForRootCAs"></a> 規劃 PKI 受信任根憑證及憑證簽發者清單  
如果您的 IIS 網站系統使用 PKI 用戶端憑證，以透過 HTTP 供用戶端驗證之用，或是透過 HTTPS 供用戶端驗證及加密之用時，您可能必須匯入根 CA 憑證，並將它當成網站內容來使用。 以下是兩個案例︰  

-   您使用 Configuration Manager 部署作業系統，且管理點只接受 HTTPS 用戶端連線。  

-   您使用未鏈結根憑證授權單位 (CA) 憑證 (受管理點信任) 的 PKI 用戶端憑證。  

    > [!NOTE]  
    >  當您從簽發用於管理點之伺服器憑證的相同 CA 階層，簽發用戶端 PKI 憑證時，您不需要指定這個根 CA 憑證。 然而，如果您使用多重 CA 階層，但不確定其是否彼此信任時，即可匯入用戶端 CA 階層所適用的根 CA。  

如果必須匯入 Configuration Manager 的根 CA 憑證，請將該憑證從簽發 CA 或從用戶端電腦匯出。 如果從簽發 CA 匯出也是根 CA 的憑證，請確保未將私密金鑰匯出。 將匯出的憑證檔案儲存在安全位置，以防遭到竄改。 當您設定站台時，必須能夠存取檔案。 如果是透過網路來存取檔案，請務必利用 SMB 簽署或 IPsece 來防止通訊內容遭到竄改。  

如果匯入的根 CA 憑證已更新，您就必須匯入更新的憑證。  

這些匯入的根 CA 憑證及每一個管理點的根 CA 憑證，會建立一份 Configuration Manager 電腦以下列方式使用的憑證簽發者清單：  

-   當用戶端連線到管理點時，管理點會確認用戶端憑證鏈結至網站憑證簽發者清單中的受信任根憑證。 如果沒這麼做，就會拒絕憑證，PKI 連線就會失敗。  

-   當用戶端選取 PKI 憑證並擁有憑證簽發者清單時，即可選取鏈結至憑證簽發者清單中之受信任根憑證的憑證。 如果沒有符合者，用戶端就不會選取 PKI 憑證。 如需用戶端憑證程序的詳細資訊，請參閱本文的[規劃 PKI 用戶端憑證選擇](#BKMK_PlanningForClientCertificateSelection)一節。  

不同於網站設定，當您註冊行動裝置及 Mac 電腦，以及設定 Intel AMT 型電腦的無線網路時，您可能也必須匯入根 CA 憑證。  

###  <a name="BKMK_PlanningForClientCertificateSelection"></a> 規劃 PKI 用戶端憑證選擇  
 如果您的 IIS 站台系統會使用 PKI 用戶端憑證，以透過 HTTP 供用戶端驗證之用，或是透過 HTTPS 供用戶端驗證及加密之用時，請規劃 Windows 用戶端如何選取可供 Configuration Manager 使用的憑證。  

> [!NOTE]  
>  有些裝置不支援憑證選擇方法。 它們反倒會自動選取第一個滿足憑證需求的憑證。 例如，Mac 電腦上的用戶端及行動裝置不支援憑證選擇方法。  

在許多情況下，預設的設定和行為即已足夠。 Windows 電腦上的 Configuration Manager 用戶端，會依此順序使用下列準則篩選多種憑證：  

1.  憑證簽發者清單：憑證鏈結至管理點所信任的根 CA。  

2.  憑證在 [個人] 預設憑證存放區中。  

3.  憑證是有效的，未撤銷，也未過期。 有效性檢查會確認私密金鑰的可存取性，以及未使用與 Configuration Manager 不相容的第 3 版憑證範本來建立憑證。  

4.  憑證具有用戶端驗證功能，或是發給電腦名稱。  

5.  憑證具有最長的有效期。  

可利用下列機制，將用戶端設定為可使用憑證簽發者清單：  

-   它會當成 Configuration Manager 網站資訊，發佈到 Active Directory 網域服務。  

-   用戶端是使用用戶端推入安裝的。  

-   用戶端在順利被指派到其網站後，會從管理點下載該清單。  

-   在用戶端安裝期間指定憑證簽發者清單，以作為 CCMCERTISSUERS 的 CCMSetup client.msi 內容。  

第一次安裝且尚未指派到網站的用戶端，不具備憑證簽發者清單，所以會略過此檢查。 如果用戶端的確擁有憑證簽發者清單，但沒有鏈結至憑證簽發者清單中受信任根憑證的 PKI 憑證時，憑證選擇會失敗，且用戶端不會繼續其他憑證選擇準則。  

在多數情況下，Configuration Manager 用戶端會正確地識別出唯一且適當的 PKI 憑證。 然而，若情況並非如此，就不需根據用戶端驗證功能來選取憑證，您可以設定其他兩種選擇方法：  

-   用戶端憑證主體名稱的部分相符字串。 這是一項不區分大小寫的配對，如果主旨欄位正在使用電腦完整網域名稱 (FQDN)，而且是根據網域尾碼選擇憑證時 (例如 **contoso.com**)，便適用此配對法。 然而，您可使用此選擇方法來識別憑證主體名稱 (用以區分與用戶端憑證存放區其他憑證的不同) 中循序字元的任何字串。  

    > [!NOTE]  
    >  您不可將主體別名 (SAN) 的部分相符字串當成網站設定來使用。 雖然您可使用 CCMSetup 為 SAN 指定部分相符字串，在以下案例中，該相符字串將會被網站內容覆寫：  
    >   
    >  -   用戶端會擷取發佈至 Active Directory 網域服務的網站資訊。  
    > -   用戶端是使用用戶端推入安裝的。  
    >   
    >  只有在您手動安裝用戶端，且用戶端不從 Active Directory 網域服務擷取網站資訊時，才使用 SAN 中的部份字串相符。 例如，這些狀況僅會適用於網際網路用戶端。  

-   用戶端憑證的主體名稱屬性值或主體別名 (SAN) 屬性值相符。 若您使用 X500 辨別名稱或符合 RFC 3280 的對等物件識別碼 (OID)，且您希望根據屬性值進行憑證選擇，則適用這個區分大小寫的相符。 您可以僅指定屬性與您要求的值來唯一識別或驗證憑證，和區別憑證存放區中的其他憑證。  

下表顯示針對用戶端憑證選擇準則 Configuration Manager 支援的屬性值。  

|OID 屬性|辨別名稱屬性|屬性定義|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|網域元件|  
|1.2.840.113549.1.9.1|E 或 E-mail|電子郵件地址|  
|2.5.4.3|CN|一般名稱|  
|2.5.4.4|SN|主體名稱|  
|2.5.4.5|SERIALNUMBER|序號|  
|2.5.4.6|C|國碼 (地區碼)|  
|2.5.4.7|L|位置|  
|2.5.4.8|S 或 ST|省份名稱|  
|2.5.4.9|STREET|街道地址|  
|2.5.4.10|O|組織名稱|  
|2.5.4.11|OU|組織單位|  
|2.5.4.12|T 或 Title|標題|  
|2.5.4.42|G 或 GN 或 GivenName|指定的名稱|  
|2.5.4.43|I 或 Initials|縮寫|  
|2.5.29.17|(沒有值)|主體替代名稱|  

若套用選取準則後有一個以上的合適憑證，您可以覆寫預設設定以選取有效期間最長的憑證，或者改為指定不選取任何憑證。 在此案例中，用戶端無法和有 PKI 憑證的 IIS 站台系統進行通訊。 用戶端會將錯誤訊息傳送至指派的後援狀態點，向您警示憑證選取失敗，如此您就可以變更或縮小憑證選擇準則。 接著，用戶端行為就會根據失敗的連線是經由 HTTPS 或 HTTP 來進行。  

-   如果失敗的連線是經由 HTTPS：用戶端會嘗試透過 HTTPS 進行連線，並使用用戶端自我簽署憑證。  

-   如果失敗的連線是經由 HTTP：用戶端會使用自我簽署用戶端憑證，透過 HTTP 重試連線。  

若要協助識別唯一 PKI 用戶端憑證，除了在 [電腦] 存放區中的 [個人] 預設值外，您也可以指定自訂存放區。 不過，您必須從 Configuration Manager 單獨建立此存放區，且必須能夠將憑證部署至此自訂存放區，並在有效期間到期前更新憑證。  

如需如何設定用戶端憑證設定的詳細資訊，請參閱[設定 System Center Configuration Manager 的安全性](../../../core/plan-design/security/configure-security.md)一文的[設定用戶端 PKI 憑證的設定](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI)一節。  

###  <a name="BKMK_PlanningForPKITransition"></a> 規劃用於 PKI 憑證和以網際網路為基礎的用戶端管理的轉換策略  
Configuration Manager 中的彈性設定選項可讓您逐漸轉換用戶端和網站，以使用 PKI 憑證來協助確保用戶端端點的安全。 PKI 憑證提供更好的安全性讓您管理網際網路用戶端。  

由於 Configuration Manager 中設定選項和選擇的數目，轉換網站的方法不只一種，如此一來，所有用戶端就都會使用 HTTPS 連線。 不過，您可以遵循這些步驟作為指引：  

1.  安裝並設定 Configuration Manager 網站，如此網站系統就會接受透過 HTTPS 和 HTTP 的用戶端連線。  

2.  設定網站內容中的 用戶端電腦通訊 索引標籤，如此 站台系統設定 就會是 **HTTP 或 HTTPS**，然後選取 使用可用的 PKI 用戶端憑證 (用戶端驗證功能。  如需詳細資訊，請參閱[設定 System Center Configuration Manager 的安全性](../../../core/plan-design/security/configure-security.md)一文的[設定用戶端 PKI 憑證的設定](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI)一節。  

3.  針對用戶端憑證試驗 PKI 首度發行。 如需部署範例，請參閱[為 Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)一文的＜部署 Windows 電腦的用戶端憑證＞一節。  

4.  使用用戶端推入安裝方法安裝用戶端。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)一文的[如何使用用戶端推入安裝 Configuration Manager 用戶端](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)一節。  

5.  使用 Configuration Manager 主控台中的報告和資訊來監控用戶端部署和狀態。  

6.  檢視 [資產與相容性]  工作區 [裝置]  節點中的 [用戶端憑證]  欄位，來追蹤有多少用戶端使用用戶端 PKI 憑證  

     您也可以在電腦上部署 Configuration Manager HTTPS 整備評估工具(**cmHttpsReadiness.exe**)，並使用報告檢視有多少電腦可以搭配使用用戶端 PKI 憑證與 Configuration Manager。  

    > [!NOTE]  
    >  安裝 Configuration Manager 用戶端時，**cmHttpsReadiness.exe** 工具是安裝在 *%windir%***\CCM** 資料夾中。 在用戶端上執行此工具時，您可以指定以下選項：  
    >   
    >  -   /Store:&lt;名稱\>  
    > -   /Issuers:&lt;清單\>  
    > -   /Criteria:&lt;準則\>  
    > -   /SelectFirstCert  
    >   
    >  這些選項分別對應至 **CCMCERTSTORE**、 **CCMCERTISSUERS**、 **CCMCERTSEL**和 **CCMFIRSTCERT** Client.msi 屬性。 如需這些選項的詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端安裝內容](../../../core/clients/deploy/about-client-installation-properties.md)。  

7.  您自信有足夠的用戶端能成功使用其用戶端 PKI 憑證透過 HTTP 進行驗證時，請依照下列步驟作業：  

    1.  將 PKI Web 伺服器憑證部署至將執行網站上其他管理點的成員伺服器，並在 IIS 中設定該憑證。 如需詳細資訊，請參閱[為 Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)一文的＜為執行 IIS 的站台系統部署網頁伺服器憑證＞一節。  

    2.  將管理點角色安裝在此伺服器上，並在 [HTTPS]  的管理點內容中設定 [用戶端連線] 選項。  

8.  監控並確認具備 PKI 憑證的用戶端藉由使用 HTTPS 來使用新的管理點。 您可以使用 IIS 記錄或效能計數器來確認此項。  

9. 重新設定其他網站系統角色以使用 HTTPS 用戶端連線。 如果您想管理網際網路上的用戶端，請確認網站系統具備網際網路 FQDN，並設定個別管理點和發佈點，以接受來自網際網路的用戶端連線。  

    > [!IMPORTANT]  
    >  設定站台系統角色以接受來自網際網路的連線前，請檢閱以網際網路為基礎的用戶端管理的規劃資訊和必要條件。 如需詳細資訊，請參閱 [Communications between endpoints in System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md) (System Center Configuration Manager 中端點之間的通訊)。  

10. 延伸用戶端與執行 IIS 之站台系統的 PKI 憑證首度發行，並按需求設定 HTTPS 用戶端連線與網際網路連線的站台系統角色。  

11. 最高安全性：您自信所有用戶端都使用用戶端 PKI 憑證進行驗證和加密時，請將網站內容變更至僅使用 HTTPS。  

 遵循此規劃來漸漸導入 PKI 憑證時，若先僅透過 HTTP 進行驗證，然後透過 HTTPS 驗證並加密，您就會降低用戶端變成不受管理的風險。 此外，您也會因 Configuration Manager 支援的最高安全性而受益。  

##  <a name="BKMK_PlanningForRTK"></a> 規劃受信任的根金鑰  
Configuration Manager 受信任根的金鑰提供 Configuration Manager 用戶端機制來確認網站系統隸屬其階層。 每個網站伺服器會產生網站交換金鑰，以與其他網站通訊。 來自階層頂層網站的網站交換金鑰稱為受信任的根金鑰。  

Configuration Manager 中受信任根金鑰的功能類似公開金鑰基礎結構的根憑證，因為由受信任根金鑰的私密金鑰所簽署的任何物件，都會沿著階層受到信任。 例如，藉由以受信任根金鑰組的私密金鑰來簽署管理點憑證，以及藉由複製用戶端可用之受信任根金鑰組的公開金鑰，用戶端可以區別出階層中的管理點與不在階層中的管理點。 用戶端使用 Windows Management Instrumentation (WMI) 將受信任根金鑰的複本儲存在 **root\ccm\locationservices** 命名空間中。  

用戶端可以使用兩種機制，自動擷取受信任根金鑰的公開複本。  

-   Active Directory 架構會針對 Configuration Manager 進行延伸、網站會發佈至 Active Directory 網域服務，而用戶端可以從全域目錄伺服器擷取此網站資訊。  

-   用戶端是使用用戶端推入安裝的。  

如果用戶端無法使用其中一種機制來擷取受信任根金鑰，就會信任由第一個與其通訊的管理點所提供的受信任根金鑰。 在此案例中，可能會將用戶端錯誤導向到攻擊者的管理點 (該管理點會接收來自 Rogue 管理點的原則)。 這很可能是狡猾攻擊者的行為，並且只會在用戶端從有效管理點擷取受信任根金鑰前的有限時間內發生。 不過，若要降低攻擊者錯誤導向用戶端至 Rogue 管理點的這種風險，您可以使用受信任根金鑰來預先佈建用戶端。  

使用以下程序預先佈建並確認 Configuration Manager 用戶端的受信任根金鑰：  

-   您可以使用檔案以受信任根金鑰預先佈建用戶端。  

-   在不使用檔案的狀況下，以受信任根金鑰預先佈建用戶端。  

-   確認用戶端上的受信任根金鑰。  

> [!NOTE]  
>  若可以從 Active Directory 網域服務取得受信任根金鑰，或使用用戶端推入來安裝用戶端，就不需要使用受信任根金鑰來預先佈建用戶端。 此外，因為 PKI 憑證建立了信任，所以當用戶端使用管理點的 HTTPS 通訊時，您不需要預先佈建用戶端。  

您可以搭配 CCMSetup.exe 使用 Client.msi 內容 **RESETKEYINFORMATION = TRUE**，從用戶端移除受信任的根金鑰。 若要取代受信任的根金鑰，請重新安裝用戶端與新的受信任根金鑰，例如使用用戶端推入，或經由使用 CCMSetup.exe 來指定 Client.msi **SMSPublicRootKey** 內容。  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a>經由使用檔案，以受信任根金鑰預先佈建用戶端  

1.  在文字編輯器中，開啟 *&lt;Configuration Manager 目錄\>***\bin\mobileclient.tcf** 檔案。  

2.  找出項目 **SMSPublicRootKey=**，從該行複製金鑰，然後在不進行任何變更的狀況下關閉檔案。  

3.  建立新的文字檔，並貼上您從 mobileclient.tcf 檔案中複製的金鑰資訊。  

4.  儲存檔案，並將該檔案放到所有電腦都可以存取的位置，但須確保檔案的安全，以避免遭到竄改。  

5.  使用接受 Client.msi 內容的任何安裝方式來安裝用戶端，並指定 Client.msi 內容 **SMSROOTKEYPATH=***&lt;完整路徑與檔案名稱\>*。  

    > [!IMPORTANT]  
    >  在安裝用戶端期間為擁有額外的安全性而指定受信任的根金鑰時，您同時也必須指定站台碼，方法是使用 Client.msi 內容 **SMSSITECODE=&lt;站台碼\>**。  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a>不使用檔案的狀況下，以受信任根金鑰預先佈建用戶端  

1.  在文字編輯器中，開啟 *&lt;Configuration Manager 目錄\>***\bin\mobileclient.tcf** 檔案。  

2.  找出項目 SMSPublicRootKey=，記下該行金鑰，或將其複製到剪貼簿上，然後在不進行任何變更的狀況下關閉檔案。  

3.  使用接受 Client.msi 內容的任何安裝方法來安裝用戶端，然後指定 Client.msi 內容 **SMSPublicRootKey=***&lt;金鑰\>*，其中 *&lt;金鑰\>* 是您從 mobileclient.tcf 複製的字串。  

    > [!IMPORTANT]  
    >  在安裝用戶端期間為擁有額外的安全性而指定受信任的根金鑰時，您同時也必須指定站台碼，方法是使用 Client.msi 內容 **SMSSITECODE=&lt;站台碼\>**。  

#### <a name="to-verify-the-trusted-root-key-on-a-client"></a>確認用戶端上的受信任根金鑰  

1.  在 [開始] 功能表上，選擇 [執行]，然後輸入 **Wbemtest**。  

2.  在 [Windows Management Instrumentation 測試器] 對話方塊中，選擇 [連線]。  

3.  在 [連線] 對話方塊的 [命名空間] 方塊中，輸入 **root\ccm\locationservices**，然後選擇 [連線]。  

4.  在 [Windows Management Instrumentation 測試器] 對話方塊的 [IWbemServices]  區段中，選擇 [列舉類別]。  

5.  在 [超級類別資訊] 對話方塊中依序選擇 [遞迴]和 [確定]。  

6.  在 [查詢結果]  視窗中向下捲動到清單結尾，然後按兩下 [TrustedRootKey ()] 。  

7.  在 [TrustedRootKey 的物件編輯器] 對話方塊中，選擇 [執行個體]。  

8.  在顯示 **TrustedRootKey** 執行個體的新 [查詢結果] 視窗中，按兩下 [TrustedRootKey=@]。  

9. 在 [TrustedRootKey=@ 的物件編輯器] 對話方塊中的 [內容] 區段，向下捲動到 [TrustedRootKey CIM_STRING]。 右側欄位中的字串是受信任根金鑰。 請確認該金鑰與檔案 *&lt;Configuration Manager 目錄\>***\bin\mobileclient.tcf** 中的 **SMSPublicRootKey** 值相符。  

##  <a name="BKMK_PlanningForSigningEncryption"></a> 規劃簽署與加密  
 針對所有用戶端通訊使用 PKI 憑證時，您不需要為協助保障用戶端資料通訊而規劃簽署與加密。 但是，如果您設定執行 IIS 的任何站台系統以允許 HTTP 用戶端連線，就必須決定如何協助站台保護用戶端通訊。  

 若要保護用戶端傳送至管理點的資料，您可以要求簽署資料。 此外，您可以要求來自使用 HTTP 之用戶端的所有已簽署資料都使用 SHA-256 演算法簽署。 雖然這個設定比較安全，但除非所有用戶端都支援 SHA-256，否則切勿啟用這個選項。 許多作業系統都可原生支援 SHA-256，但較舊的作業系統需要更新或是 Hotfix。 例如，執行 Windows Server 2003 SP2 的電腦必須安裝 [知識庫文章 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666)中所參照的 Hotfix。  

 簽署有助保護資料不受竄改，而加密則可確保資料不會洩漏。 您可以為用戶端傳送至網站內管理點的清查資料與狀況訊息啟用 3DES 加密。 您不需要在用戶端上安裝任何更新以支援此選項，但請考慮在用戶端上所需求的額外 CPU 使用量，以及執行加密與解密的管理點。  

 如需如何設定簽章和加密設定的詳細資訊，請參閱[設定System Center Configuration Manager 的安全性](../../../core/plan-design/security/configure-security.md)一文的[設定簽署及加密](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption)一節。  

##  <a name="BKMK_PlanningForRBA"></a> 規劃以角色為基礎的系統管理  
 如需詳細資訊，請參閱 [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md) (System Center Configuration Manager 的以角色為基礎的系統管理)。  

### <a name="see-also"></a>請參閱
[System Center Configuration Manager 的密碼編譯控制項技術參考](../../../protect/deploy-use/cryptographic-controls-technical-reference.md)。  

