---
title: "管理 Linux 和 UNIX 用戶端 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中管理 Linux 和 UNIX 伺服器上的用戶端。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
caps.latest.revision: 7
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d10b6876058d19d3a9a750a59267913d15793574


---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中管理 Linux 和 UNIX 伺服器的用戶端

適用於：System Center Configuration Manager (最新分支)

當您使用 System Center Configuration Manager 管理 Linux 和 UNIX 伺服器時，可以設定集合、維護期間和用戶端設定來協助管理伺服器。 此外，雖然 Linux 和 UNIX 的 Configuration Manager 用戶端沒有使用者介面，但是您可以強制用戶端手動輪詢用戶端原則。

##  <a name="a-namebkmkcollectionsforlnua-collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Linux 和 UNIX 伺服器的集合  
 使用集合來管理 Linux 和 UNIX 伺服器群組的方式，與使用集合來管理其他用戶端類型的方式相同。 集合可以是直接成員資格集合或查詢型集合，以識別用戶端作業系統、硬體組態或有關站台資料庫中所儲存之用戶端的其他詳細資料。 例如，您可以使用包含 Linux 和 UNIX 伺服器的集合來管理下列項目：  

-   用戶端設計  

-   軟體部署  

-   強制維護期間  

 您必須先成功收集來自用戶端的硬體清查，才能透過作業系統或發佈來識別 Linux 或 UNIX 用戶端。 如需收集硬體清查的資訊，請參閱 [System Center Configuration Manager 中的 Linux 及 UNIX 的硬體清查](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)。  

 硬體清查的預設用戶端設定包含用戶端電腦之作業系統的相關資訊。 您可以使用 **Operating System** 類別的 **Caption** 屬性來識別 Linux 或 UNIX 伺服器的作業系統。  

 您可以在 Configuration Manager 主控台之 [資產與相容性] 工作區的 [裝置] 節點中檢視有關執行 Linux 和 UNIX Configuration Manager 用戶端之電腦的詳細資料。 在 Configuration Manager 主控台的 [資產與相容性] 工作區中，您可以在 [作業系統] 欄中檢視每部電腦之作業系統的名稱。  

 根據預設，Linux 和 UNIX 伺服器是 **All Systems** 集合的成員。 建議您建立僅包含 Linux 和 UNIX 伺服器或其子集的自訂集合。 這可讓您管理作業 (例如，部署軟體，或將用戶端設定指派給適用電腦的群組)。 例如，如果您將 RHEL6 x64 電腦的軟體部署至同時包含 Windows 和 Linux 電腦的集合，部署的狀態將會顯示部分成功。 相反地，當您將軟體部署至僅包含 RHEL6 x64 電腦的集合，則可以使用狀態訊息和報告精確地識別部署成功。  

 當您建立 Linux 和 UNIX 伺服器的自訂集合時，請包含內含 Operating System 屬性之 Caption 屬性中的成員資格規則查詢。 如需建立集合的資訊，請參閱[如何在 System Center Configuration Manager 中建立集合](../../../core/clients/manage/collections/create-collections.md)。  

##  <a name="a-namebkmkmaintenancewindowsforlnua-maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Linux 和 UNIX 伺服器的維護期間  
 Linux 和 UNIX 伺服器的 Configuration Manager 用戶端支援使用維護期間。 這項支援與 Windows 型用戶端的支援相同。  

 如需如何使用維護期間的詳細資訊，請參閱[如何使用 System Center Configuration Manager 中的維護期間](../../../core/clients/manage/collections/use-maintenance-windows.md)。  

##  <a name="a-namebkmkclientsettingsforlnua-client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Linux 和 UNIX 伺服器的用戶端設定  
 設定適用於 Linux 和 UNIX 伺服器之用戶端設定的方式，與設定其他用戶端設定的方式相同。  

 根據預設， **Default Client Agent Settings** 適用於 Linux 和 UNIX 伺服器。 您也可以建立自訂用戶端設定，並將其部署至集合，這些集合包含特定用戶端作業系統或混合使用用戶端作業系統。  

 沒有僅套用至 Linux 和 UNIX 用戶端的額外用戶端設定。 不過，具有未套用至 Linux 和 UNIX 用戶端的預設用戶端設定。 Linux 和 UNIX 的用戶端僅會套用所支援功能的設定，而且會忽略未支援功能的任何設定。  

 例如，您建立可指定硬體清查排程的自訂用戶端裝置設定，然後將它指派給包含 Linux 電腦的集合。 結果是在 Linux 和 UNIX 伺服器上強制執行硬體清查排程。 接下來，您建立可啟用和設定遠端控制設定的自訂用戶端裝置設定，並將它指派給該相同集合。 結果是 Linux 和 UNIX 伺服器會忽略遠端控制設定。 原因是 Linux 和 UNIX 用戶端不支援 Configuration Manager 中的遠端控制。  

 如需設定用戶端設定的資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端設定](../../../core/clients/deploy/configure-client-settings.md)。  

##  <a name="a-namebkmkpolicyforlnua-computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a> Linux 和 UNIX 伺服器的電腦原則  
 Linux 和 UNIX 伺服器的 Configuration Manager 用戶端會定期輪詢其站台中的電腦原則，以了解要求的設定，以及檢查部署。  

 您也可以在 Linux 或 UNIX 伺服器上強制用戶端立即輪詢電腦原則。 若要立即輪詢，請在伺服器上使用 **root** 認證來執行下列命令： **/opt/microsoft/configmgr/bin/ccmexec -rs policy**。  

 電腦原則輪詢的詳細資料會輸入至共用用戶端記錄檔 ( **scxcm.log**)。  

> [!NOTE]  
>  Linux 和 UNIX 的 Configuration Manager 用戶端永遠不會要求，也不會處理使用者原則。  

##  <a name="a-namebkmkmanagelinuxcertsa-how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a> 如何管理 Linux 和 UNIX 用戶端憑證  
 在您安裝 Linux 和 UNIX 的用戶端之後，即可使用 **certutil** 工具，以使用新的 PKI 憑證來更新用戶端，以及匯入新的憑證撤銷清單 (CRL)。 當您安裝 Linux 和 UNIX 的用戶端時，這個工具位於下列位置： **/opt/microsoft/configmgr/bin/certutil**  

 若要管理憑證，請在每個用戶端上執行具有下列其中一個選項的 certutil：  

|選項|詳細資訊|  
|------------|----------------------|  
|importPFX|使用這個選項指定憑證，以取代用戶端目前所使用的憑證。<br /><br /> 當您使用 **-importPFX** 時，也必須使用 **-password** 命令列參數來提供與 PKCS#12 檔案相關聯的密碼。<br /><br /> 使用 **-rootcerts** 指定任何其他根憑證需求。<br /><br /> 範例︰**certutil -importPFX &lt;PKCS#12 憑證的路徑> -password &lt;憑證密碼\> [-rootcerts &lt;以逗號分隔的憑證清單>]**|  
|-importsitecert|使用這個選項更新管理伺服器上的站台伺服器簽署憑證。<br /><br /> 範例：**certutil -importsitecert &lt;DER 憑證的路徑\>**|  
|-importcrl|使用這個選項，利用一個或多個 CRL 檔案路徑來更新用戶端上的 CRL。<br /><br /> 範例︰**certutil importcrl &lt;以逗號分隔的 CRL 檔案路徑\>**|  



<!--HONumber=Nov16_HO1-->


