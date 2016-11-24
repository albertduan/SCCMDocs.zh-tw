---
title: "安全性基本概念 | System Center Configuration Manager"
description: "深入了解 System Center Configuration Manager 的安全層級。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cb84efcaac281aa8c9338cd69ce32054ea775de3


---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>System Center Configuration Manager 的安全性基本概念

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 的安全性包含數個層級。 第一層是由 Windows 安全性功能針對作業系統及網路所提供，包括：  

-   在 Configuration Manager 元件之間傳輸檔案的檔案共用  

-   存取控制清單 (ACL) 可確保檔案和登錄機碼的安全  

-   IPsec 可保護通訊安全  

-   群組原則可設定安全性原則  

-   DCOM 權限可用於分散式應用程式，例如 Configuration Manager 主控台  

-   Active Directory 網域服務可儲存安全性原則  

-   Windows 帳戶安全性，包括 Configuration Manager 安裝期間建立的部分群組  

然後是額外的安全性元件，例如防火牆和入侵偵測，可協助提供整個環境的全面防護。 由符合業界標準的 PKI 實作所發行之憑證可協助提供驗證、簽署和加密。  

除了 Windows 伺服器和網路基礎結構所提供的安全性之外，Configuration Manager 以數種方式控制對 Configuration Manager 主控台與其資源的存取。 依預設，只有本機系統管理員才有存取檔案和登錄機碼的權限，以在安裝 Configuration Manager 的電腦上執行主控台。  

下一層安全性以透過 Windows Management Instrumentation (WMI) 的存取為基礎，特別是 **SMS 提供者**。 「SMS 提供者」是一個 Configuration Manager 元件，授與使用者查詢站台資料庫以取得資訊的存取權。 依照預設，對提供者的存取權已限制為僅授與本機 **SMS Admins** 群組的成員。 此群組一開始僅包含已安裝 Configuration Manager 的使用者。 若要將其他帳戶權限授與給通用訊息模型 (CIM) 存放庫和 SMS 提供者，請新增其他帳戶到 SMS Admins 群組。  

最後一層安全性是基於網站資料庫中物件的權限。 依預設，您安裝 Configuration Manager 時使用的本機系統帳戶和使用者帳戶，都有權限管理站台資料庫中的所有物件。 您可使用**以角色為基礎的系統管理**，針對 Configuration Manager 主控台中的額外系統管理使用者，授與或限制權限。  

本主題的其餘部分將討論與 Configuration Manager 相關的安全性層面。  

## <a name="role-based-administration"></a>以角色為基礎的系統管理  
 Configuration Manager 使用以角色為基礎的系統管理，協助保護如集合、部署及站台等物件。 此管理模式主要針對所有網站和網站設定，定義與管理整個階層的安全性存取權設定。 安全性角色指派給系統管理使用者，而群組權限則指派給不同的 Configuration Manager 物件類型，例如可建立或變更用戶端設定的權限。 安全性範圍會針對特定物件的執行個體進行分組，這些物件由系統管理使用者負責管理，例如安裝 Microsoft Office 應用程式。 結合安全性角色、安全性範圍和集合來定義系統管理使用者可檢視與管理的物件。 Configuration Manager 安裝部分預設安全性角色以進行一般管理工作。 不過，您可建立自己的安全性角色來支援特定的業務需求。  

 如需詳細資訊，請參閱[為 System Center Configuration Manager 設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。  

## <a name="securing-client-endpoints"></a>確保用戶端端點安全  
 利用自我簽署憑證或公開金鑰基礎結構 (PKI) 憑證，來為網站系統角色的用戶端通訊確保安全性。 Configuration Manager 所偵測到位在網際網路和行動裝置上的用戶端電腦，必須使用 PKI 憑證，如此才能透過 HTTPS 來確保用戶端端點的安全性。 用戶端連線的網站系統角色可設定為透過 HTTPS 或 HTTP 用戶端通訊。 用戶端電腦一律使用最安全的可用方式來進行通訊，除非您的網站系統角色允許 HTTP 通訊時，才會轉回在內部網路上使用較不安全的 HTTP 通訊方式。  

 如需詳細資訊，請參閱 [System Center Configuration Manager 的密碼編譯控制項技術參考](../../protect/deploy-use/cryptographic-controls-technical-reference.md)。  

## <a name="configuration-manager-accounts-and-groups"></a>Configuration Manager 帳戶和群組  
 Configuration Manager 在進行大部分的站台操作時會使用**本機系統**帳戶。 不過，部分管理工作可能需要建立與維護額外帳戶。 安裝期間會建立數個預設群組和 SQL Server 角色。 不過，您可能需要手動新增電腦或使用者帳戶到這些預設的群組和角色。  

 如需詳細資訊，請參閱 [Accounts used in System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md) (System Center Configuration Manager 中使用的帳戶)。  

## <a name="privacy"></a>隱私權  
 由於企業管理產品能夠有效管理大量的用戶端，而有許多優點，但您也必須知道此軟體可能對組織中的使用者隱私權有何影響。 System Center Configuration Manager 包含許多可用來收集資料和監視裝置的工具，其中有些可能會引發對隱私權的疑慮。  

 例如，當您安裝 Configuration Manager 用戶端時，許多管理設定都會預設為啟用。 也因此導致用戶端軟體將資訊傳送到 Configuration Manager 站台。 用戶端資訊會儲存在 Configuration Manager 資料庫中，這些資訊並不會傳送到 Microsoft。 在實作 System Center Configuration Manager 之前，請考慮您的隱私權需求。  



<!--HONumber=Nov16_HO1-->


