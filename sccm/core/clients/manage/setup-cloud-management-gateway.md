---
title: "設定雲端管理閘道 | Microsoft Docs"
description: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 05/01/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.translationtype: Human Translation
ms.sourcegitcommit: d5a6fdc9a526c4fc3a9027dcedf1dd66a6fff5a7
ms.openlocfilehash: 97e1bc6585cee0ff433da0ec0b60b9604cb7348f
ms.contentlocale: zh-tw
ms.lasthandoff: 05/02/2017

---

# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>設定 Configuration Manager 的雲端管理閘道

*適用於：System Center Configuration Manager (最新分支)*

從版本 1610 開始，設定 Configuration Manager 中的雲端管理閘道包含下列步驟：

## <a name="step-1-configure-required-certificates"></a>步驟 1︰設定所需的憑證

## <a name="option-1-preferred---use-the-server-authentication-certificate-from-a-public-and-globally-trusted-certificate-provider-like-verisign"></a>選項 1 (優先) - 使用公用和全球信任之憑證提供者 (如 VeriSign) 的伺服器驗證憑證

使用此方法時，用戶端會自動信任憑證，您不需要自行建立自訂的 SSL 憑證。

1. 在組織的公用網域名稱服務 (DNS) 中建立正式名稱記錄 (CNAME)，以建立雲端管理閘道服務的易記名稱別名，以便用於公開憑證。
例如，Contoso 將其雲端管理閘道服務命名為 **GraniteFalls**，在 Azure 中則是 **GraniteFalls.CloudApp.Net**。 在 Contoso 的公用 DNS contoso.com 命名空間中，DNS 系統管理員會針對真實的主機名稱 **GraniteFalls.CloudApp.net**，為 **GraniteFalls.Contoso.com** 建立新的 CNAME 記錄。
2. 接著，使用 CNAME 別名的一般名稱 (CN) 向公用提供者要求伺服器驗證憑證。
例如，Contoso 使用 **GraniteFalls.Contoso.com** 做為憑證 CN。
3. 使用此憑證在 Configuration Manager 主控台中建立雲端管理閘道服務。
    - 在 [建立雲端管理閘道精靈] 的 [設定] 頁面上新增此雲端服務的伺服器憑證時 (從「憑證檔」)，精靈會從憑證 CN 擷取主機名稱做為服務名稱，然後將該名稱附加到 **cloudapp.net** (如果是 Azure US Government Cloud 則為 **usgovcloudapp.net**) 做為在 Azure 中建立服務的「服務 FQDN」。
例如，在 Contoso 建立雲端管理閘道時，會從憑證 CN 擷取主機名稱 **GraniteFalls**，因此 Azure 中建立的實際服務為 **GraniteFalls.CloudApp.net**。

### <a name="option-2---create-a-custom-ssl-certificate-for-cloud-management-gateway-in-the-same-way-as-for-a-cloud-based-distribution-point"></a>選項 2 - 為雲端管理閘道建立自訂 SSL 憑證，其方式與為雲端架構發佈點建立憑證的方式相同

您可以透過針對雲端架構發佈點所執行的相同方式，為雲端管理閘道建立自訂 SSL 憑證。 請遵循[為雲端架構的發佈點部署服務憑證](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)中的指示，但針對下列作業採用不同的做法：

- 設定新的憑證範本時，針對您為 Configuration Manager 伺服器所設定的安全性群組，授與 [讀取] 和 [註冊] 權限。
- 當要求自訂 Web 伺服器憑證時，請針對憑證的一般名稱提供 FQDN，一般名稱以 **cloudapp.net** 結尾 (針對在 Azure 公用雲端上使用雲端管理閘道) 或以 **usgovcloudapp.net** 結尾 (針對 Azure 政府雲端)。


## <a name="step-2-export-the-client-certificates-root"></a>步驟 2︰匯出用戶端憑證的根目錄

匯出網路上所使用之用戶端憑證根目錄的最簡單方式，是在具有用戶端憑證的其中一部加入網域的電腦上開啟並複製此用戶端憑證。

> [!NOTE] 
>
> 在任何您希望利用雲端管理閘道管理的電腦上，以及裝載雲端管理閘道連接器端點的站台系統伺服器上，都需要用戶端憑證。 如果您必須將用戶端憑證新增至任何電腦，請參閱[部署 Windows 電腦的用戶端憑證](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012)。

1.  在 [執行] 視窗中，輸入 **mmc** 並按下 Return 鍵。

2.  從 [檔案] 功能表選擇 [新增/移除嵌入式管理單元...]。

3.  在 [新增或移除嵌入式管理單元] 對話方塊中，選擇 [憑證] > [新增]**&gt;** > [電腦帳戶] > [下一步] > [本機電腦] > [完成]。 

4.  移至 [憑證] &gt; [個人] &gt; [憑證]。

5.  在電腦上按兩下憑證以進行用戶端驗證，選擇 [憑證路徑] 索引標籤，然後按兩下根授權單位 (位於最上層路徑)。

6.  在 [詳細資料] 索引標籤上，選擇 [複製到檔案...]。

7.  使用預設憑證格式完成 [憑證匯出精靈]。 記下您所建立之根憑證的名稱和位置。 您將需要這些資訊在[後續步驟](#step-4-set-up-cloud-management-gateway)中設定雲端管理閘道。

## <a name="step-3-upload-the-management-certificate-to-azure"></a>步驟 3︰將管理憑證上傳至 Azure

Configuration Manager 需要 Azure 管理憑證才能存取 Azure API 及設定雲端管理閘道。 如需如何上傳管理憑證的詳細資訊和指示，請參閱 Azure 文件中的下列文章：

- [Azure 雲端服務的憑證概觀](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [上傳 Azure 管理 API 管理憑證](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>請務必複製與管理憑證相關聯的訂用帳戶 ID。 您將需要這些資訊在[接下來的步驟](#step-4-set-up-cloud-management-gateway)中於 Configuration Manager 主控台中設定雲端管理閘道。

### <a name="subordinate-ca-certificates-and-azure"></a>次級 CA 憑證和 Azure

如果您的憑證是由次級 CA (subCA) 發行，且您的企業 PKI 基礎結構不在網際網路上，請使用此程序將憑證上傳到 Azure。 

1. 在 Azure 入口網站中，設定雲端管理閘道之後，請找出雲端管理閘道服務並移至 [憑證] 索引標籤。 在那裡上傳您的 subCA 憑證。 如果您有一個以上的 subCA 憑證，您需要將它們全部上傳。 
2. 上傳憑證之後，請記錄其憑證指紋。 
3. 使用此指令碼，將憑證指紋加入至站台資料庫：
    
```

    DIM serviceCName
    DIM subCAThumbprints

    ' Verify arguments
    IF WScript.Arguments.Count <> 2 THEN
    WScript.StdOut.WriteLine "Usage: CScript UpdateSubCAThumbprints.vbs <ServiceCName> <SubCA cert thumbprints, separated by ;>"
    WScript.Quit 1
    END IF

    'Get arguments
    serviceCName = WScript.Arguments.Item(0)
    subCAThumbprints = WScript.Arguments.Item(1)

    'Find SMS Provider
    WScript.StdOut.WriteLine "Searching for SMS Provider for local site..."
    SET objSMSNamespace = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms")
    SET results = objSMSNamespace.ExecQuery("SELECT * From SMS_ProviderLocation WHERE ProviderForLocalSite = true")

    'Process the results
    FOR EACH var in results
    siteCode = var.SiteCode
    NEXT

    IF siteCode = "" THEN
    WScript.StdOut.WriteLine "Failed to locate SMS provider."
    WScript.Quit 1
    END IF

    WScript.StdOut.WriteLine "SiteCode = " & siteCode 

    ' Connect to the SMS namespace
    SET objWMIService = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms\site_" & siteCode)

    'Get instance of SMS_AzureService
    DIM query
    query = "SELECT * From SMS_AzureService WHERE ServiceType = 'CloudProxyService' AND ServiceCName = '" & serviceCName & "'"
    WScript.StdOut.WriteLine "Run WQL query: " &  query
    SET objInstances = objWMIService.ExecQuery(query)

    IF IsNull(objInstances) OR (objInstances.Count = 0) THEN
    WScript.StdOut.WriteLine "Failed to get Azure_Service instance."
    WScript.Quit 1
    END IF

    FOR EACH var IN objInstances
    SET azService = var
    NEXT

    WScript.StdOut.WriteLine "Update [SubCACertThumbprint] to " & subCAThumbprints

    'Update SubCA cert thumbprints
    azService.Properties_.item("SubCACertThumbprint") = subCAThumbprints

    'Save data back to provider
    azService.Put_

    WScript.StdOut.WriteLine "[SubCACertThumbprint] is updated successfully."
```


## <a name="step-4-set-up-cloud-management-gateway"></a>步驟 4︰設定雲端管理閘道

>[!NOTE]
>在版本 1610 中，雲端管理閘道是發行前版本的功能。 若要啟用它，請參閱[使用更新的發行前版本功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。

1. 在 Configuration Manager 主控台中，移至 [系統管理] > [雲端服務] > [雲端管理閘道]。
2. 選擇 [建立雲端管理閘道]。

3. 在 [建立雲端管理閘道] 精靈中，輸入您的 Azure 訂用帳戶 ID (從 Azure 管理入口網站複製)，並瀏覽至您用來上傳做為 Azure 管理憑證的憑證檔案。 選擇 [下一步] 然後等待一段時間，讓主控台連線到 Azure。

4. 在精靈中填寫其他詳細資料：

    - 指定將在 Azure 中執行之服務的名稱。 服務名稱必須只能是英數字元，且長度為 3 至 24 個字元。

    - 選擇您希望服務執行的 Azure 區域。

    - 指定您要針對服務使用的虛擬機器數目。 預設值為 1，但您可以針對服務執行最多 16 個虛擬機器。

    >[!NOTE]
    >如果您針對雲端管理閘道連接點使用網際網路 Proxy，您必須依照您所使用的虛擬機器數目來增加 Proxy 上連接埠的數目，由連接埠 10124 開始。

    - 指定您要從自訂 SSL 憑證匯出的私密金鑰 (.pfx 檔案)。

    - 指定從用戶端憑證匯出的根憑證。

    -   指定建立新的憑證範本時所使用的相同服務名稱 FQDN。 您必須根據您所使用的 Azure 雲端，針對 FQDN 服務名稱指定下列其中一項尾碼：

    Azure 雲端 | FQDN 首碼
    --------------|-------------
    公用 (商務) 雲端 | .cloudapp.net    
    政府雲端 | .usgovcloudapp.net

  - 清除 [驗證用戶端憑證撤銷] 旁邊的方塊 (除非您要公開發行 CRL 資訊)。

  - 完成時，請選擇 [下一步]。

5. 如果您想要使用 14 天閾值監視雲端管理閘道流量，請選擇核取方塊，以開啟臨界值警示。 然後，指定臨界值，以及引發不同警示等級的百分比。 完成時，請選擇 [下一步]。

6. 檢閱設定，然後選擇 [下一步]。 Configuration Manager 隨即開始設定服務。 在您關閉精靈之後，將需要 5 到 15 分鐘，才能在 Azure 中完整地佈建服務。 檢查新設定之雲端管理閘道的 [狀態] 資料行，以判斷服務何時就緒。

## <a name="step-5-configure-primary-site-for-client-certification-authentication"></a>步驟 5︰設定主要站台以進行用戶端憑證驗證

1. 在 Configuration Manager 主控台中，移至 [系統管理] > [站台設定] > [站台]。

2. 選取您希望透過雲端管理閘道管理之用戶端的主要站台，然後選擇 [內容]。

3. 在主要站台內容表的 [用戶端電腦通訊] 索引標籤上，核取 [使用可用的 PKI 用戶端憑證 (用戶端驗證)]。

4. 確定清除 [由用戶端檢查站台系統的憑證撤銷清單 (CRL)]。 只有您要公開發行 CRL 時才需要此選項。


## <a name="step-6-add-the-cloud-management-gateway-connector-point"></a>步驟 6︰新增雲端管理閘道連接器端點

雲端管理閘道連接器端點是用來與雲端管理閘道通訊的新站台系統角色。 若要新增雲端管理閘道連接器端點，請遵循[為 System Center Configuration Manager 新增站台系統角色](/sccm/core/servers/deploy/configure/add-site-system-roles)中的指示。

## <a name="step-7-configure-roles-for-cloud-management-gateway-traffic"></a>步驟 7︰設定雲端管理閘道流量的角色

設定雲端管理閘道的最後一個步驟就是設定站台系統角色，以接受雲端管理閘道流量。 在 Tech Preview 1606 中，雲端管理閘道只支援管理點、發佈點和軟體更新點角色。 您必須個別設定每個角色。

1. 在 Configuration Manager 主控台中，移至 [系統管理] > [站台設定] > [伺服器和站台系統角色]。

2. 針對您希望為雲端管理閘道流量設定的角色，選擇站台系統伺服器。

3. 選擇角色，然後選擇 [內容]。

4. 在角色內容表的 [用戶端連線] 底下，選擇 [HTTPS]，選擇 [允許 Configuration Manager 雲端管理閘道流量] 旁邊的核取方塊，然後選擇 [確定]。 針對其餘角色重複上述步驟。

## <a name="step-8-configure-clients-for-cloud-management-gateway"></a>步驟 8︰設定雲端管理閘道的用戶端

在雲端管理閘道和站台系統角色已完全設定並執行之後，用戶端會自動在下一次位置要求時取得雲端管理閘道服務的位置。 用戶端必須位於公司網路，以便接收雲端管理閘道服務的位置。 位置要求的輪詢週期為每 24 小時。 如果您不想等候標準排程的位置要求，您可以在電腦上重新啟動 SMS Agent Host 服務 (ccmexec.exe) 來強制執行要求。

在用戶端上設定雲端管理閘道服務的位置，用戶端就可以自動判斷它是在內部網路或者網際網路上。 如果用戶端可以連絡網域控制站或內部部署管理點，用戶端就會使用它與 Configuration Manager 通訊，否則用戶端會認為它是在網際網路上並使用雲端管理閘道服務的位置來通訊。

>[!NOTE]
> 您可以強制用戶端一律使用雲端管理閘道，無論用戶端是在內部網路或網際網路上。 若要這麼做，您必須在用戶端電腦上設定下列登錄機碼：\
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`

若要確認用戶端可以連絡 Configuration Manager，您可以在用戶端電腦上執行下列 PowerShell 命令︰

`gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate`

此命令會顯示用戶端可以連絡的管理點，包括雲端管理閘道服務。

## <a name="next-steps"></a>後續步驟

[監視雲端管理閘道的用戶端](monitor-clients-cloud-management-gateway.md)

