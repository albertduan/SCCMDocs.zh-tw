---
title: "規劃 SMS 提供者 | System Center Configuration Manager"
description: "深入了解 SMS 提供者如何協助您管理 System Center Configuration Manager。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bdf7b9b4ab9e9da25bf32891381f61c94ef28285


---
# <a name="plan-for-the-sms-provider-for-system-center-configuration-manager"></a>規劃 System Center Configuration Manager 的 SMS 提供者

*適用對象：System Center Configuration Manager (最新分支)*

若要管理 System Center Configuration Manager，您可以使用連接至 **SMS 提供者**執行個體的 Configuration Manager 主控台。 根據預設，SMS 提供者會在安裝站台時，一併安裝在管理中心網站或主要站台。  


##  <a name="a-namebkmkplansmsprova-about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> 關於 SMS 提供者  
 SMS 提供者是 Windows Management Instrumentation (WMI) 提供者，會指派網站之 Configuration Manager 資料庫的**讀取**與**寫入**權限：  

-   **SMS Admins**  群組提供對 SMS 提供者的存取。 Configuration Manager 會自動在站台伺服器和每個 SMS 提供者電腦上，建立這個安全性群組。  

-   每個管理中心網站和主要網站上至少需要一個 SMS 提供者。  您可以視需要安裝額外的提供者。  

-   次要網站不支援 SMS 提供者。  


每個 Configuration Manager 主控台、資源總管、工具與自訂指令碼都會使用 SMS 提供者，如此 Configuration Manager 系統管理使用者即可存取儲存在資料庫中的資訊。 SMS 提供者不會與 Configuration Manager 用戶端互動。 Configuration Manager 主控台連線至網站時，Configuration Manager 主控台會查詢站台伺服器上的 WMI，以找出要使用的 SMS 提供者執行個體。  

 SMS 提供者會協助強制執行 Configuration Manager 安全性。 它僅會傳回執行 Configuration Manager 主控台之系統管理使用者獲授權可檢視的資訊。  

> [!IMPORTANT]  
>  裝載網站之 SMS 提供者的每一部電腦離線時，Configuration Manager 主控台會無法連線至該網站的資料庫。  

 如需如何管理 SMS 提供者的詳細資訊，請參閱 [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) 中的 [Manage the SMS Provider](../../../core/servers/manage/modify-your-infrastructure.md)。  

 **安裝 SMS 提供者的先決條件：**  

 支援 SMS 提供者：  

-   電腦所在的網域，必須與網站伺服器和網站資料庫網站系統間具備雙向信任。  

-   電腦不可擁有來自不同網站的網站系統角色。  

-   電腦不可擁有來自任何網站的 SMS 提供者。  

-   電腦必須執行支援網站伺服器的作業系統。  

-   電腦的可用磁碟空間至少必須要有 650 MB，才可支援隨 SMS 提供者一併安裝的 Windows 自動化部署套件 (Windows ADK) 元件。 如需 Windows ADK 與 SMS 提供者的詳細資訊，請參閱本主題中的 [SMS 提供者的作業系統部署需求](#BKMK_WAIKforSMSProv) 一節。  

##  <a name="a-namebkmklocationa-sms-provider-locations"></a><a name="bkmk_location"></a> SMS 提供者位置  
 安裝網站時，安裝程式會自動安裝網站的第一個 SMS 提供者。 您可以為 SMS 提供者指定以下任何一個受支援的位置：  

-   網站伺服器電腦  

-   網站資料庫電腦  

-   未裝載 SMS 提供者或網站系統角色來自不同網站的伺服器等級的電腦。  


若要檢視網站上所安裝每個 SMS 提供者的位置，請檢視網站 [內容]  對話方塊的 [一般]  索引標籤。  

 每個 SMS 提供者支援來自多個請求的同時連線。 這些連線的唯一限制是 SMS 提供者電腦上可用伺服器連線的數目，以及 SMS 提供者電腦上的可用資源以服務連線請求。  

 安裝網站後，您可以再次在網站伺服器上執行安裝程式，以變更現有 SMS 提供者的位置，或在該網站上安裝其他 SMS 提供者。 您在一台電腦上只能安裝一個 SMS 提供者，並且電腦上不能安裝來自一個以上網站的 SMS 提供者。  

 請參考下列資訊來了解在每個受支援位置上安裝「SMS 提供者」的優缺點：  


**Configuration Manager 站台伺服器**  

-   **優點：**  

    -   SMS 提供者不使用網站資料庫電腦的系統資源。  

    -   除了網站伺服器或網站資料庫電腦外，此位置也可提供比位於電腦上的 SMS 提供者更好的效能。  

-   **缺點：**  

    -   SMS 提供者會使用網站伺服器操作專用的系統和網路資源。  


**裝載網站資料庫的 SQL Server**  

-   **優點：**  

    -   SMS 提供者並不使用網站伺服器上的網站系統資源。  

    -   若有足夠伺服器資源可以使用，此位置可提供三個位置中最佳的效能。  

-   **缺點：**  

    -   SMS 提供者會使用網站資料庫操作專用的系統和網路資源。  

    -   當網站資料庫裝載在 SQL Server 的叢集執行個體上時，這個位置就不會是一個選項。  


**網站伺服器或網站資料庫電腦以外的電腦**  

-   **優點：**  

    -   SMS 提供者不使用網站伺服器或網站資料庫電腦資源。  

    -   此類型的位置可讓您部署額外 SMS 提供者，以提供高使用性的連線。  

-   **缺點：**  

    -   SMS 提供者效能可能會因為協調網站伺服器與網站資料庫電腦所需的額外網路流量而降低。  

    -   必須讓網站資料庫電腦與所有安裝 Configuration Manager 主控台的電腦一直都能存取此伺服器。  

    -   此位置可使用其他服務專用的系統資源。  

##  <a name="a-namebkmksmsprovlanguagesa-about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a> 關於 SMS 提供者的語言  
 SMS 提供者操作時顯示的語言可與安裝該 SMS 提供者之電腦的語言不同。  

 系統管理使用者或 Configuration Manager 使用 SMS 提供者處理請求時，SMS 提供者會嘗試傳回格式符合提出請求之電腦的作業系統語言的資料。 SMS 提供者不會將資訊從一種語言翻譯成另一種語言。 相反地，傳回的資料在 Configuration Manager 主控台上顯示時，資料顯示的語言會根據物件來源和儲存類型而定。  

 當物件的資料儲存在資料庫時，可用的語言會依據以下項目而定：  

-   Configuration Manager 建立的物件會使用多國語言的支援，儲存在資料庫中。 儲存物件時使用的語言，是您執行安裝程式時在建立物件的網站上所設定的語言。 這些物件在 Configuration Manager 主控台中顯示時，會以提出請求之電腦的顯示語言顯示 (若物件可使用該語言)。 若不能以提出請求之電腦的顯示語言來顯示物件，則會以預設語言顯示，亦即英文。  

-   系統管理使用者建立的物件會使用用來建立物件的語言，儲存在資料庫中。 這些物件會在 Configuration Manager 主控台中以相同語言顯示。 SMS 提供者無法翻譯這些物件，並且也沒有多個語言選項。  

##  <a name="a-namebkmkmultismsprova-use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a> 使用多重 SMS 提供者  
 網站完成安裝後，您可以為網站安裝額外的 SMS 提供者。 若要安裝額外的 SMS 提供者，請在站台伺服器上執行 Configuration Manager 安裝程式。 若以下任何一項為真，請考慮安裝額外的 SMS 提供者：  

-   您會有許多執行 Configuration Manager 主控台的系統管理使用者，並且同時連線至一個網站。  

-   您將使用可能引入經常呼叫 SMS 提供者的 Configuration Manager SDK 或其他產品。  

-   您想要確保 SMS 提供者的高可用性。  


網站上安裝多個 SMS 提供者，並提出連線要求時，網站會以不確定的方式指派每個新連線要求，以便使用安裝的 SMS 提供者。 您無法指定 SMS 提供者位置搭配使用特定的連線工作階段。  

> [!NOTE]  
>  考量每個 SMS 提供者位置的優缺點，並以您無法控制哪個 SMS 提供者將用於每個新連線的資訊來平衡這些考量。  

例如，首次將 Configuration Manager 主控台連線到某個網站時，連線會查詢站台伺服器上的 WMI，以便以不確定的方式找出主控台將使用的 SMS 提供者執行個體。 在 Configuration Manager 主控台工作階段結束前，Configuration Manager 主控台會持續使用這個特定的 SMS 提供者執行個體。 若因 SMS 提供者電腦在網路上無法使用，導致工作階段結束，則當您重新連線 Configuration Manager 主控台時，網站會以不確定的方式指派 SMS 提供者電腦至新的連線工作階段。 其可能會指派給無法使用的相同 SMS 提供者電腦。 若發生這種狀況，您可以嘗試重新連線 Configuration Manager 主控台，直到指派可用的 SMS 提供者電腦為止。  

##  <a name="a-namebkmkaboutsmsadminsa-about-the-sms-admins-group"></a><a name="BKMK_AboutSMSAdmins"></a> 關於 SMS Admins 群組  
 您可使用 SMS Admin 群組提供 SMS 提供者系統管理使用者存取權限。 網站安裝時，會在網站伺服器上以及安裝 SMS 提供者的每台電腦上，自動建立群組。 關於 SMS Admins 群組的其他資訊：  

-   當電腦是成員伺服器時，會將 SMS Admins 群組建立為本機群組。  

-   當電腦是網域控制站時，會將 SMS Admins 群組建立為網域本機群組。  

-   在電腦上解除安裝 SMS 提供者時，不會將 SMS Admins 群組從電腦中移除。  


使用者帳戶必須是 SMS Admins 群組的成員，然後使用者才能成功連線至 SMS 提供者。 您在 Configuration Manager 主控台中設定的每個系統管理使用者，會自動新增到每部站台伺服器上的 SMS Admins 群組，以及階層中的每部 SMS 提供者電腦。 從 Configuration Manager 主控台刪除系統管理使用者時，該使用者會從每部站台伺服器上的 SMS Admins 群組與階層中每部 SMS 提供者電腦中移除。  

使用者成功連線至 SMS 提供者後，以角色為基礎的系統管理會決定使用者可以存取或管理的 Configuration Manager 資源。  

您可以使用 WMI 控制 MMC 嵌入式管理單元來檢視和設定 SMS Admins 群組權限。 根據預設，[所有人]  都具有 [執行方法] 、[提供者寫入] 和 [啟用帳戶]  的權限。 使用者連線至 SMS 提供者後，會根據其以角色為基礎的系統管理安全性權限 (如 Configuration Manager 主控台中所定義)，授與該使用者存取網站資料庫中資料的權限。 將明確授與 SMS Admins 群組在 **Root\SMS** 命名空間的 **啟用帳戶** 和 **遠端啟用** 。  

> [!NOTE]  
>  每位使用遠端 Configuration Manager 主控台的系統管理使用者，在站台伺服器電腦和 SMS 提供者電腦上都需要 [遠端啟用 DCOM] 權限。 儘管您可以將這些權限授與任何使用者或群組，但最佳作法是將這些權限授與 SMS Admins 群組，以簡化系統管理。 如需詳細資訊，請參閱 [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) 主題中的 [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) 一節。  


##  <a name="a-namebkmksmsprovnamespacea-about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a> 關於 SMS 提供者命名空間  
WMI 架構會定義 SMS 提供者的結構。 架構命名空間會描述 SMS 提供者架構內 Configuration Manager 資料的位置。 下表包含 SMS 提供者所使用的一些常見命名空間。  

|命名空間|說明|  
|---------------|-----------------|  
|Root\SMS\site_&lt;站台碼\>|SMS 提供者，廣泛為 Configuration Manager 主控台、資源總管、Configuration Manager 工具以及指令碼所用。|  
|Root\SMS\SMS_ProviderLocation|提供網站 SMS 提供者電腦的位置。|  
|Root\CIMv2|在硬體和軟體清查時，針對 WMI 命名空間資訊所清查的位置。|  
|Root\CCM|Configuration Manager 用戶端設定原則和用戶端資料。|  
|root\CIMv2\SMS|由清查用戶端代理程式收集的清查報告類別的位置。 這些設定是由用戶端在電腦原則評估時編譯，而且是以電腦的用戶端設定配置為基礎。|  

##  <a name="a-namebkmkwaikforsmsprova-operating-system-deployment-requirements-for-the-sms-provider"></a><a name="BKMK_WAIKforSMSProv"></a> SMS 提供者的作業系統部署需求  
SMS 提供者需要在執行 SMS 提供者的電腦上安裝下列外部相依性，讓您利用 Configuration Manager 主控台來使用作業系統部署工作功能：  

-   8.1 版 Windows 評定及部署套件  

 管理作業系統部署時，Windows ADK 可允許 SMS 提供者完成包括下列的各種工作：  

-   檢視 WIM 檔案詳細資料  

-   新增驅動程式檔案至現有的開機映像  

-   建立開機 .ISO 檔  


Windows ADK 安裝可能在每台安裝 SMS 提供者的電腦上，最多會需要 650 MB 的可用磁碟空間。 這個大量的磁碟空間是 Configuration Manager 安裝 Windows PE 開機映像的必要條件。  



<!--HONumber=Nov16_HO1-->


