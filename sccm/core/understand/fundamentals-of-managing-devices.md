---
title: "管理裝置的基本概念 | System Center Configuration Manager"
description: "了解如何使用 System Center Configuration Manager 來管理裝置。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f4d39f31723711a7f5ec2b1aa39e81d3a3188029


---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 來管理裝置的基本概念

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 可管理兩大類裝置。

首先是**用戶端**，係指已安裝 Configuration Manager 用戶端軟體以便您進行管理的裝置 (例如工作站、膝上型電腦、伺服器及行動裝置)。   

其次是**受管理的裝置**，這些裝置可以包括用戶端，但通常是指未安裝 Configuration Manager 用戶端軟體而您透過使用 Microsoft Intune 或使用 Configuration Manager 內建的內部部署行動裝置管理來管理的行動裝置。

除了管理包含或不含 Configuration Manager 用戶端的裝置，您可以使用以使用者為中心的管理，以幫助組成群組並識別您所管理的裝置。

## <a name="managing-devices-with-the-configuration-manager-client"></a>使用 Configuration Manager 用戶端管理裝置

 用戶端管理包括一些操作，例如從裝置收集硬體或軟體清查、在裝置上安裝新軟體，或定義會根據特定組態提出報告或強制遵守特定組態的設定。 有些管理功能 (例如硬體清查) 需要裝置執行 Configuration Manager 用戶端軟體。 將軟體安裝 (部署) 到裝置這類其他操作則是所有受管理的裝置都支援。  

 若要使用 Configuration Manager 用戶端軟體來管理裝置，您必須在網路上探索裝置，然後將用戶端軟體部署 (安裝) 到該裝置，或是在新電腦上手動安裝用戶端軟體，然後讓該電腦在加入網路時加入您的站台。 若要探索尚未安裝用戶端軟體的裝置，您需執行一或多個內建的探索方法。 探索到裝置之後，您可以接著使用數種方法其中之一來安裝用戶端軟體。 如需使用探索的資訊，請參閱[為 System Center Configuration Manager 執行探索](../../core/servers/deploy/configure/run-discovery.md)。  

 探索受支援而可執行 Configuration Manager 用戶端軟體的裝置之後，您可以使用數種方法其中之一來安裝軟體。 安裝軟體並將用戶端指派給主要站台之後，您便可以開始管理裝置。  常見的安裝方法包括「用戶端推入安裝」、以軟體更新為基礎的安裝、使用「群組原則」、在電腦上手動安裝，或將用戶端納入您部署的作業系統映像中。  

 安裝用戶端之後，您可以使用集合來簡化管理裝置的工作。 集合是您所建立裝置或使用者的邏輯群組，以便您可以在共用一組通用準則的多個裝置上執行管理工作。 例如，您可能想要在 Configuration Manager 註冊的所有行動裝置上安裝行動裝置應用程式。 如果是這樣的話，您可以使用會自動排除電腦的 **[所有行動裝置]** 集合。 您可以建立自己的集合，根據業務需求將您管理的裝置進行邏輯分組。  

 如需詳細資訊，請參閱下列主題：  

-   [選擇 System Center Configuration Manager 的裝置管理解決方案](../../core/plan-design/choose-a-device-management-solution.md)  

-   [System Center Configuration Manager 中的用戶端安裝方法](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [System Center Configuration Manager 的集合簡介](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>用戶端設計  
 當您初次安裝 Configuration Manager 時，階層中的所有用戶端都會採用您可變更的預設用戶端設定。 這些用戶端設定包括組態選項，例如裝置與站台通訊的頻率、是否已啟用用戶端進行軟體更新和其他管理作業，或使用者是否可以註冊其行動裝置以便透過 Configuration Manager 進行管理。  

 如果您需要針對使用者群組或裝置群組使用不同的用戶端設定，可以建立自訂用戶端設定，然後將這些設定指派至集合。  集合的成員是設定為採用自訂設定，而您可以建立多個依您指定順序 (依數字順序) 套用的自訂用戶端設定。  如果有設定發生衝突，則順序編號最小的設定會覆寫其他設定。  

 下圖顯示如何建立及套用自訂用戶端設定的範例。  

 ![用戶端設計](media/ClientSettings.gif)  

 若要深入了解用戶端設定，請參閱  
                [如何在 System Center Configuration Manager 中設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)[關於 System Center Configuration Manager 中的用戶端設定](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>在不使用 Configuration Manager 用戶端的情況下管理裝置  
 Configuration Manager 支援管理某些尚未安裝用戶端軟體且不是透過與 Microsoft Intune 交互操作來管理的裝置。 如需詳細資訊，請參閱[在 System Center Configuration Manager 中使用內部部署基礎結構管理行動裝置](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)和[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

## <a name="user-centric-management"></a>使用者為中心的管理  
 除了裝置集合之外，還有使用者集合，其中包含 Active Directory 網域服務的使用者。 使用使用者集合時，您可以在集合成員登入的所有電腦上安裝軟體並設定 **[使用者裝置親和性]** ，讓您部署的軟體只會在指定為使用者主要裝置的裝置上進行安裝。 這些主要裝置稱為主要裝置。 使用者可以擁有一個或多個主要裝置。  

 使用者控制其軟體部署經驗的其中一種方式，就是使用電腦用戶端介面 **「軟體中心」**。 「軟體中心」會自動安裝到用戶端電腦上，並且可從使用者的 [開始] 功能表存取。 「軟體中心」可讓使用者管理自己的軟體，以及執行下列工作：  

-   安裝軟體  

-   將軟體排程在非工作時間自動安裝  

-   設定 Configuration Manager 可以在何時將軟體安裝在裝置上  

-   如果在 Configuration Manager 中已啟用遠端控制，可以設定遠端控制的存取設定  

-   如果系統管理使用者已啟用電源管理的選項，就可以設定這些選項  

 「軟體中心」中的連結可讓使用者連線至 **「應用程式類別目錄」**，並且在此瀏覽、安裝和要求軟體。 此外，「應用程式類別目錄」可讓使用者設定一些喜好設定、抹除其行動裝置，以及 (在您允許此組態的情況下) 指定自己的使用者裝置親和性主要裝置。 (其他設定使用者裝置親和性資訊的方法包括從檔案匯入資訊，以及從使用資料自動產生。)  

 由於「應用程式類別目錄」是裝載於 IIS 中的網站，因此使用者也可以從瀏覽器、內部網路或網際網路直接存取「應用程式類別目錄」。  



<!--HONumber=Nov16_HO1-->


