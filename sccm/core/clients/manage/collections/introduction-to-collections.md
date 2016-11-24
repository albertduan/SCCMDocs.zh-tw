---
title: "集合簡介 | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中使用集合的簡介。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: 8
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 47574218dec5069205f9dba5608c6f136fb032bc


---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager 的集合簡介

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 中的集合可讓您將資源整理為可管理的單位，藉此建立組織化結構，並透過邏輯方式表示您想要執行的工作類型。 您可以使用集合，一次在多個資源上執行 Configuration Manager 作業。 下表顯示如何在 Configuration Manager 中使用集合的一些範例：  

|作業|範例|  
|---------|-------|  
|群組化資源|您可以根據組織階層建立集合，藉此以邏輯方式來群組資源。<br /><br /> 例如，您可以建立所有位在倫敦總部 Active Directory 組織單位 (OU) 之電腦的集合。 如需如何建立這種集合類型的詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立集合](../../../../core/clients/manage/collections/create-collections.md)。<br /><br /> 接著，您可以使用此集合來進行 Endpoint Protection 設定、裝置電源管理設定，或安裝 Configuration Manager 用戶端這類作業。|  
|應用程式部署|您可以建立沒有安裝 Microsoft Office 2013 之所有電腦的集合，接著將此軟體部署至該集合中的所有電腦。<br /><br /> 您也可以使用應用程式需求以執行此工作。 如需詳細資訊，請參閱[如何使用 System Center Configuration Manager 建立應用程式](../../../../apps/deploy-use/create-applications.md)。|  
|管理用戶端設定|雖然 Configuration Manager 中的預設用戶端設定套用到所有的裝置及使用者，您可以建立自訂用戶端設定，套用至裝置或使用者的集合。<br /><br /> 例如，如果您想在大多數裝置上使用遠端控制，設定預設用戶端設定以允許遠端控制，接著設定不允許遠端控制的自訂用戶端設定。 部署這些自訂用戶端設定至包含不會使用遠端控制之電腦的集合。<br /><br /> 如需如何使用用戶端設定集合的詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端設定](../../../../core/clients/deploy/about-client-settings.md)。|  
|電源管理|您所建立的每個集合都可以設定電源設定，例如，集合中的電腦處於非使用中的狀態後，多久會進入睡眠模式。<br /><br /> 如需如何搭配使用集合與電源管理的詳細資訊，請參閱[電源管理簡介](../power/introduction-to-power-management.md)。|  
|以角色為基礎的系統管理|您可以搭配集合與以角色為基礎的系統管理一起使用，來控制哪些使用者群組可以在 Configuration Manager 主控台中存取各種功能。<br /><br /> 如需如何設定以角色為基礎的系統管理集合的詳細資訊，請參閱[為 System Center Configuration Manager 設定以角色為基礎的系統管理](../../../../core/servers/deploy/configure/configure-role-based-administration.md)。|  
|維護期間|當裝置集合的成員上執行多種 Configuration Manager 作業時，維護時段可讓系統管理使用者定義時間週期。 您可以藉助維護視窗，確保用戶端組態變更發生的時段不會影響組織的產能。<br /><br /> 如需維護時段的詳細資訊，請參閱[如何使用 System Center Configuration Manager 的維護期間](../../../../core/clients/manage/collections/use-maintenance-windows.md)。|  

 大部分的管理工作需要使用一個或多個集合。 例如，您可以將軟體更新部署到裝置之前，您必須識別軟體更新之部署的集合。 雖然您可以使用內建的所有系統集合，使用此集合來執行管理工作並非最佳做法。 除了一個測試環境以外，建立自己的自訂集合，以更明確識別要管理的裝置或使用者，通常會讓您從中獲益。  

 內建和自訂的集合都會顯示在 Configuration Manager 主控台下 [資產與相容性] 工作區中的 [使用者集合] 及 [裝置集合] 節點中。  

 您最近檢視過的集合都會顯示在 Configuration Manager 主控台下 [資產與相容性]  工作區中的 [使用者]  節點及 [裝置]  節點中。  

## <a name="collection-types-in-configuration-manager"></a>Configuration Manager 中的集合類型  
 Configuration Manager 具有可用於一般作業的一些內建集合。 此外，您可以建立將資源群組化並特定至您業務需求的集合。  

### <a name="built-in-collections"></a>內建集合  
 根據預設，Configuration Manager 包含下列無法修改的集合。  

|**集合名稱**|說明|  
|-------------------------|-----------------|  
|**所有使用者群組**|包含使用 Active Directory 安全性群組探索所探索到的使用者群組。|  
|**所有使用者**|包含使用 Active Directory 使用者探索所探索到的使用者。|  
|**所有使用者及使用者群組**|包含所有使用者及所有使用者群組集合。 此集合無法修改，且包含使用者及使用者群組資源的最大範圍。|  
|**所有桌面及伺服器用戶端**|包含安裝 Configuration Manager 用戶端的伺服器及桌面裝置。 成員資格是由活動訊號探索維護。|  
|**所有行動裝置**|包含由 Configuration Manager 管理的行動裝置。 成員資格僅限於成功指派至站台或由 Exchange Server 連接器所探索到的這些行動裝置。|  
|**所有系統**|包含所有桌面和伺服器用戶端、所有行動裝置、 所有未知電腦集合，以及由 Microsoft Intune 所註冊的所有行動裝置。<br /><br /> 此集合無法修改，且包含裝置資源的最大範圍。|  
|**所有未知電腦**|包含多個電腦平台的一般電腦記錄。 您可以透過此集合使用工作順序和 PXE 開機、 可開機媒體，或預先設置的媒體以部署作業系統。|  

### <a name="custom-collections"></a>自訂集合  
 當您在 Configuration Manager 中建立自訂集合時，該集合的成員資格由一個或多個集合規則所決定。 如需如何設定集合規則的資訊，請參閱[如何在 System Center Configuration Manager 中建立集合](../../../../core/clients/manage/collections/create-collections.md)。 有四項規則可以使用：  

#### <a name="direct-rule"></a>直接規則  
 直接規則可讓您選擇要新增為集合成員的使用者或電腦。 此規則可讓您直接控制哪些資源是集合的成員。 成員資格不會自動變更，除非資源從 Configuration Manager 中移除。 Configuration Manager 必須已經探索到資源或您必須匯入資源，才可以將它們新增至直接規則集合。 直接規則集合比查詢規則集合具有更高的系統管理負荷，因為您必須手動為這個集合類型進行變更。  

#### <a name="query-rule"></a>查詢規則  
 查詢規則可依據 Configuration Manager 排程執行的查詢，來動態更新集合的成員資格。 例如，您可以在 Active Directory 網域服務中，建立屬於人力資源組織單位成員的使用者集合。 不同於直接規則集合，當您對人力資源組織單位新增或移除新使用者時，此集合的成員資格會自動更新。 查詢規則移除透過直接規則手動新增裝置到集合的系統管理負荷。 不過，它們的確減少了自行決定將哪一部電腦新增至集合的控制權。 以查詢為基礎之規則的範例包括：  

-   特定 OU 中所有的使用者  

-   所有執行 Windows 8 的電腦  

-   所有具有超過 20 GB 可用磁碟空間的電腦  

#### <a name="include-collections-rule"></a>包含集合規則  
 包含集合規則可讓您從 Configuration Manager 集合中包含另一個集合的成員。 如果包含集合的成員資格有所變更，則目前集合的成員資格會依排程由 Configuration Manager 更新。  

#### <a name="exclude-collections-rule"></a>排除集合規則  
 排除集合規則可讓您從 Configuration Manager 集合中排除另一個集合的成員。 如果排除集合的成員資格有所變更，則目前集合的成員資格會依排程由 Configuration Manager 更新。  

> [!NOTE]  
>  如果一個集合同時具有包含集合規則和排除集合規則，就會發生衝突，此時排除規則的優先順序高於包含規則。  

## <a name="incremental-collection-updates"></a>增量集合更新  
 當您啟用一個集合的累加式更新時， Configuration Manager 會定期掃描上一次集合評估至今新增或變更過的資源，並在整個集合評估中個別更新這些資源的集合成員資格。 根據預設，當您啟用累加式集合更新時，其會每隔 5 分鐘執行一次，以協助確保您收集的資料保持最新狀態，而不會造成完整集合評估的額外負荷。  

> [!NOTE]  
>  當您建立新的集合時，預設會停用累加式更新。  



<!--HONumber=Nov16_HO1-->


