---
title: "架構延伸 | System Center Configuration Manager"
description: "延伸 Active Directory 架構以支援 System Center Configuration Manager。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f8c8533da62d215ed22f5235eefa687d5df41394


---
# <a name="schema-extensions-for-system-center-configuration-manager"></a>System Center Configuration Manager 的架構延伸

適用於：System Center Configuration Manager (最新分支)

您可以延伸 Active Directory 架構以支援 Configuration Manager。 如此一來，即可編輯樹系 Active Directory 架構以新增一個容器與數個屬性，供 Configuration Manager 站台在 Active Directory 中發佈重要資訊，以便用戶端安全存取這些資訊。  這項資訊可以簡化用戶端的部署和組態，並協助用戶端找到具有已部署內容之伺服器的站台資源，或將各種服務提供給用戶端的站台資源。  

-   不需要但建議延伸 Active Directory 架構。  

[延伸 Active Directory 架構](https://msdnstage.redmond.corp.microsoft.com/en-US/library/mt345589\(TechNet.10\).aspx)之前，您應該要熟悉 Active Directory 網域服務並熟悉 [修改 Active Directory 架構](https://technet.microsoft.com/library/cc759402\(v=ws.10\).aspx)。  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>延伸 Configuration Manager 的 Active Directory 架構時應考量的事項  

-   System Center Configuration Manager 的 Active Directory 架構延伸與 Configuration Manager 2007 和 Configuration Manager 2012 所使用的架構延伸一樣。 如果您先前延伸過任一版本的架構，則不需要再次延伸架構。  

-   延伸架構是針對整個樹系的單次無法還原動作。  

-   只有 Schema Admins 群組的成員或已委派足夠權限來修改架構的人員，才能延伸架構。  

-   雖然您可以在執行 Configuration Manager 安裝程式之前或之後延伸架構，但是建議您在開始設定站台和階層設定之前進行。  這可以簡化許多較新的組態步驟。  

-   延伸架構之後，會在整個樹系複寫 Active Directory 通用類別目錄。 因此，請規劃在複寫流量不致於對其他需要網路的程序造成不利影響時延伸架構。  

    -   在 Windows 2000 樹系中，延伸架構可能會完整同步處理整個通用類別目錄  

    -   從 Windows 2003 樹系開始，只會覆寫新增的屬性  

**未使用 Active Directory 架構的裝置和用戶端：**  

-   Exchange Server 連接器所管理的行動裝置  

-   Mac 電腦的用戶端  

-   Linux 和 UNIX 伺服器的用戶端  

-   由 Configuration Manager 註冊的行動裝置  

-   由 Microsoft Intune 註冊的行動裝置  

-   行動裝置的舊版用戶端  

-   設定只能使用網際網路用戶端管理的 Windows 用戶端  

-   Configuration Manager 偵測到位於網際網路上的 Windows 用戶端  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>受益於延伸架構的功能  
**用戶端電腦安裝與站台指派** - 在 Windows 電腦上安裝新的用戶端時，該用戶端會在 Active Directory Domain Services 中搜尋安裝內容。  

-   **因應措施：** 如果未延伸該架構，請使用下列其中一個選項提供安裝該電腦所需的組態詳細資料：  

    -   使用用戶端推入安裝。 在使用用戶端安裝方法之前，請確定符合所有必要條件。 如需詳細資訊，請參閱＜電腦用戶端的必要條件＞的＜安裝方法相依性＞一節。  

    -   **手動安裝用戶端**，並使用 CCMSetup 安裝命令列內容提供用戶端安裝內容。 其中必須包含下列項目：  

        -   在用戶端進行安裝時，透過 CCMSetup 命令列使用 CCMSetup 內容 **/mp:=&lt;管理點名稱電腦名稱\>** 或 **/source:&lt;用戶端來源檔案路徑\>**，以指定能讓電腦下載安裝檔案的管理點或來源路徑。  

        -   指定用戶端可使用的初始管理點清單，用戶端可將這些初始管理點指派至網站，然後下載用戶端原則及網站設定。 使用 CCMSetup Client.msi 內容 SMSMP 執行此動作。  

    -   **在 DNS 或 WINS 中發佈管理點** ，並且設定用戶端使用此服務位置方法。  

**用戶端與伺服器通訊的連接埠設定** - 用戶端進行安裝時，會使用 Active Directory 中所儲存的連接埠資訊進行設定。 如果您在之後變更網站的用戶端與伺服器通訊連接埠，用戶端將可自 Active Directory 網域服務取得這個新的連接埠設定。  

-   **因應措施：** 如果未延伸架構，請使用下列其中一個選項，將新的連接埠組態提供給現有的用戶端：  

    -   **重新安裝用戶端** ，方法是使用設定新連接埠的選項。  

    -   將自訂指令碼部署至更新連接埠資訊的用戶端。 如果用戶端因連接埠變更而無法與站台通訊，您便無法使用 Configuration Manager 來部署這個指令碼。 例如，您可以使用群組原則。  

**內容部署案例** - 當您在其中一個站台建立內容，然後將該內容部署至階層中的另一個站台時，接收站台必須能夠驗證已簽署內容資料的簽章。 您必須能夠存取建立此資料之來源網站的公開金鑰，才能執行此動作。 當您延伸 Configuration Manager 的 Active Directory 架構時，階層中的所有站台即可使用某個站台的公開金鑰。  

-   **因應措施：** 如果未延伸架構，請使用階層維護工具 **preinst.exe**在站台之間交換安全金鑰資訊。  

     例如，如果您打算在主要網站建立內容，然後將該內容部署至另一個主要網站之下的次要網站，則必須延伸 Active Directory 架構，使次要網站能夠取得來源主要網站的公開金鑰，否則就必須使用 preinst.exe，直接在兩個網站之間共用金鑰。  

## <a name="active-directory-attributes-and-classes"></a>Active Directory 屬性和類別  
在進行 System Center Configuration Manager 的架構延伸時，會將下列類別和屬性新增至架構，並供該 Active Directory 樹系中的所有 Configuration Manager 站台使用。  

-   屬性：  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-Ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Boundaries  
        於  

    -   cn=MS-SMS-Site-Boundaries  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   類別：  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]  
>  架構延伸可能包括繼承自舊版產品但 Configuration Manager 2015 並未使用的屬性和類別。 例如：  
>   
>  -   Attribute: cn=MS-SMS-Site-Boundaries  
> -   Class: cn=MS-SMS-Server-Locator-Point  

您可以檢視 System Center Configuration Manager 安裝媒體之 **\SMSSETUP\BIN\x64** 資料夾的 **ConfigMgr_ad_schema.LDF** 檔案，以確定上述清單是否為最新。  



<!--HONumber=Nov16_HO1-->

