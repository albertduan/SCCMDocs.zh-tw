---
title: "以角色為基礎的系統管理基本概念 | System Center Configuration Manager"
description: "使用以角色為基礎的系統管理，控制 Configuration Manager 和您管理之物件的系統管理權限。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3e70794144caa5a1993cc65089b1076476fc6106


---
# <a name="fundamentals-of-role-based-administration-for-system-center-configuration-manager"></a>System Center Configuration Manager 以角色為基礎之系統管理的基礎

*適用於：System Center Configuration Manager (最新分支)*

有了 System Center Configuration Manager，您會使用以角色為基礎的系統管理，以安全存取 Configuration Manager，以及所管理的物件，像是集合、部署與站台。   了解本主題所介紹的概念後，您可以[為 System Center Configuration Manager 設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。  

 此以角色為基礎的系統管理模型主要針對所有站台與站台設定，使用下列項目來定義與管理整個階層的安全性存取設定：  

-   **安全性角色** -指派給系統管理使用者，用以提供這些使用者 (或使用者群組) 不同的 Configuration Manager 物件權限，例如建立或變更用戶端設定的權限。  

-   **安全性範圍** - 會針對物件的特定執行個體進行分組，這些物件由系統管理使用者負責管理，例如安裝 Microsoft Office 2010 的應用程式。  

-   **集合** - 這是您指定使用者群組與裝置資源，以供系統管理使用者管理的方式。  

 安全性角色、安全性範圍與集合的組合，可讓您隔離符合組織需求的系統管理指派，並同時定義使用者的系統管理範圍 (也就是使用者可在您 Configuration Manager 部署中檢視及管理的內容)。  

**以角色為基礎的系統管理提供下列好處：**  

-   站台不會作為系統管理界限使用  

-   您可以為階層建立系統管理使用者，且只需為他們指派安全性一次。  

-   所有安全性指派皆會複寫，並可在整個階層使用。  

-   有數個內建安全性角色可用以指派典型的系統管理工作，且您可以建立專屬的自訂安全性角色，以支援您特定的業務需求  

-   系統管理使用者只會看到其有權限管理的物件  

-   您可以稽核系統管理安全性動作。  

在您設計並實作 Configuration Manager 的系統管理安全性時，您會使用下列項目來建立系統管理使用者的**系統管理範圍**：  

-   [安全性角色](#bkmk_Planroles)  

-   [集合](#bkmk_planCol)  

-   [安全性範圍](#bkmk_PlanScope)  

 系統管理範圍控制系統管理使用者可在 Configuration Manager 主控台內檢視的物件，以及使用者對這些物件的權限。 以角色為基礎的系統管理會將設定複製到階層內的每個網站作為全域資料，然後套用至所有系統管理連線。  

> [!IMPORTANT]  
>  網站間複寫延遲可避免網站接收以角色為基礎的系統管理變更。 如需如何監視站台間資料庫複寫的詳細資訊，請參閱 [System Center Configuration Manager 中的站台間資料傳輸](../../core/servers/manage/data-transfers-between-sites.md)主題。  

##  <a name="a-namebkmkplanrolesa-security-roles"></a><a name="bkmk_Planroles"></a> 安全性角色  
 使用安全性角色以授與安全權限給系統管理使用者。 安全性角色實際上是指派給系統管理使用者以執行其系統管理工作的一組安全性權限。 這些安全權限定義系統管理使用者可執行的系統管理動作，以及針對特定物件類型所授與的權限。 最佳作法是指派可提供最低權限的安全性角色。  

 Configuration Manager 有數個內建安全性角色以支援典型的系統管理工作分組，您可以建立專屬的自訂安全性角色以支援您特定的業務需求。 內建的安全性角色的範例：  

-   **系統高權限管理員**：此安全性角色可授與 Configuration Manager 的所有權限。  

-   **資產分析師**：此安全性角色允許系統管理使用者檢視使用 Asset Intelligence、軟體清查、硬體清查以及軟體計量所收集的資料。 系統管理使用者可以建立計量規則與 Asset Intelligence 類別、系列以及標籤。  

-   **軟體更新管理員**：此安全性角色授與用以定義並部署軟體更新的權限。 與此角色先關聯的系統管理角色可以建立集合、軟體更新群組、部署、範本並且啟用網路存取保護 (NAP) 的軟體更新。  

> [!TIP]  
>  您可以檢視內建安全性角色清單與您在 Configuration Manager 主控台建立的自訂安全性角色，包括角色的說明。 若要進行檢視，請在 [系統管理]  工作空間中，展開 [安全性] ，然後選取 [安全性角色] 。  

 每個安全性角色針對不同的物件類型有特定的權限。 例如， **應用程式系統管理員** 安全性角色具有下列的應用程式權限： **核准**、 **建立**、 **刪除**、 **修改**、 **修改資料夾**、 **移動物件**、 **讀取/部署**、 **設定安全性範圍**。 您無法變更內建安全性角色的權限，但您可以複製角色、進行變更，然後將這些變更另存為新的自訂安全性角色。 您也可以匯入從另一個階層匯出的安全性角色 (例如，從測試網路匯出)。 檢閱安全性角色與其權限以判定您是否要使用內建安全性角色，或是您必須建立您自己的自訂安全性角色。  

 **利用下列步驟協助您規劃安全性角色：**  

1.  辨識系統管理使用者在 Configuration Manager 中執行的工作。 這些工作可與一或多個管理工作群組相關，例如部署應用程式與套件、部署相容性所適用的作業系統與設定、設定網站與安全性、稽核、遠端控制電腦以及收集清查資料。  

2.  將這些系統管理工作對應到一個或多個內建安全性角色。  

3.  如果部分的系統管理使用者要執行多個安全性角色的工作，請將多個安全性角色指派給這些系統管理使用者，而不要建立結合多個工作的新安全性角色。  

4.  如果您辨識的工作無法對應到內建安全性角色，請建立並測試新的安全性角色。  

如需如何建立與設定以角色為基礎的系統管理安全性角色之詳細資訊，請參閱[為 System Center Configuration Manager 設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)主題中的[建立自訂安全性角色](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)與[設定安全性角色](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole)。  

##  <a name="a-namebkmkplancola-collections"></a><a name="bkmk_planCol"></a> 集合  
 集合可用來指定系統管理使用者可檢視或管理的使用者與電腦資源。 例如，如果系統管理使用者要部署應用程式或是執行遠端控制，則必須指派使用者安全性角色，以取得授與包含這些資源的集合的存取權限。 您可以選取使用者或裝置集合。  

 如需有關集合的詳細資訊，請參閱 [System Center Configuration Manager 的集合簡介](../../core/clients/manage/collections/introduction-to-collections.md)。  

 設定以角色為基礎的系統管理之前，檢查您是否必須基於下列原因建立新集合:  

-   功能性組織。 例如，區分伺服器與工作站的集合。  

-   地理對齊方式。 例如，區分北美與歐洲的集合。  

-   安全性需求和商務程序。 例如，區分生產與測試電腦的集合。  

-   組織對齊方式。 例如，區分每個業務單位的集合。  

如需如何針對以角色為基礎的系統管理來設定集合的詳細資訊，請參閱[為 System Center Configuration Manager 設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)主題中的[設定集合以管理安全性](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl)。  

##  <a name="a-namebkmkplanscopea-security-scopes"></a><a name="bkmk_PlanScope"></a> 安全性範圍  
 使用安全性範圍以提供系統管理使用者存取安全性物件。 安全性範圍為已命名的安全物件集，以群組身分指派至系統管理使用者。 所有安全物件都必須指派給一個或多個安全性範圍。 Configuration Manager 具有兩個內建安全性範圍︰  

-   **全部**：此內建安全性範圍可授與所有範圍的存取權。 您無法指派物件至此安全性範圍。  

-   **預設**：根據預設，所有物件都會使用此內建安全性範圍。 首次安裝 Configuration Manager 時，所有物件都會被指派至此安全性範圍。  

如果您想限制系統管理使用者可查看與管理的物件，您必須建立與使用您專屬的自訂安全性範圍。 安全性範圍不支援階層結構而且不可為巢狀。 安全性範圍可包含一個或多個物件類型，包括下列各項：  

-   警示訂閱  

-   應用程式  

-   開機映像  

-   界限群組  

-   設定項目  

-   自訂用戶端設定  

-   發佈點及發佈點群組  

-   驅動程式套件  

-   全域條件  

-   移轉作業  

-   作業系統映像  

-   作業系統安裝套件  

-   套件  

-   查詢  

-   網站  

-   軟體計量規則  

-   軟體更新群組  

-   軟體更新套件  

-   工作順序套件  

-   Windows CE 裝置設定項目和套件  

有部分物件無法包含在安全性範圍中，因為這些物件只能透過安全性角色來確保安全性。 這些物件的系統管理存取權無法限制為可用物件的子集合。 例如，您的系統管理使用者可能會建立僅限於特定網站使用的界限群組。 由於界限物件不支援安全性範圍，因此您無法為此使用者指派安全性範圍，以限制其只能存取可能與該網站相關聯的界限。 由於界限物件無法與安全性範圍產生關聯，指派包含界限物件存取權的安全性角色給使用者時，該使用者可存取階層中的所有界限。  

不受安全性範圍限制的物件包括下列物件:  

-   Active Directory 樹系  

-   系統管理使用者  

-   警示  

-   反惡意程式碼原則  

-   界限  

-   電腦關聯  

-   預設用戶端設計  

-   部署範本  

-   裝置驅動程式  

-   Exchange Server 連接器  

-   移轉網站對網站對應  

-   行動裝置註冊設定檔  

-   安全性角色  

-   安全性範圍  

-   網站位址  

-   網站系統角色  

-   軟體標題  

-   軟體更新  

-   狀態訊息  

-   使用者裝置親和性  

必須限制個別物件執行個體的存取時，請建立安全性範圍。 例如：  

-   您的系統管理使用者群組必須能夠查看生產應用程式而非測試應用程式。 為生產應用程式建立一個安全性範圍，並為測試應用程式建立另一個範圍。  

-   不同的系統管理使用者針對某些物件類型的執行個體需要不同的存取權限。 例如，系統管理使用者群組要求特定軟體更新群組的 [讀取]  權限，另一個系統管理使用者群組則需要其他軟體更新群組的 [修改]  與 [刪除]  權限。 針對這些軟體更新群組建立不同的安全性範圍。  

如需如何針對以角色為基礎的系統管理來設定安全性範圍的詳細資訊，請參閱[為 System Center Configuration Manager 設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)主題中的[設定物件的安全性範圍](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope)。  



<!--HONumber=Nov16_HO1-->


