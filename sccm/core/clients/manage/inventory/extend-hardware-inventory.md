---
title: "擴充硬體清查 | Microsoft Docs"
description: "了解擴充 System Center Configuration Manager 中的硬體清查的方法。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
caps.latest.revision: 10
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: cf325aec385f570b297f753f37c2c39abe93154f


---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>如何擴充 System Center Configuration Manager 中的硬體清查

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 硬體清查會使用 Windows Management Instrumentation (WMI) 從 Windows 電腦讀取裝置資訊。 WMI 是 Microsoft 的 Web 架構企業管理 (WBEM) 實作，而 WBEM 是一種用於存取企業環境中管理資訊的業界標準。 在舊版 Configuration Manager 中，您可以修改站台伺服器上的檔案 sms_def.mof 來擴充硬體清查。 這個檔案包含一份可讀取的 WMI 類別 Configuration Manager 硬體清查。 如果您編輯這個檔案，則可以啟用和停用現有類別，也會建立新的類別來進行清查。  

 Configuration.mof 檔案用來定義用戶端上要由硬體清查所清查的資料類別，而且從 Configuration Manager 2012 以來不曾變更過。 您可以建立資料類別來清查現有或自訂 WMI 儲存機制資料類別，或用戶端系統上的登錄機碼。  

 Configuration.mof 檔案也會定義並註冊存取硬體清查期間的裝置資訊的 WMI 提供者。 註冊提供者會定義要使用的提供者的類型和提供者支援的類別。  

 Configuration Manager 用戶端要求原則時 (例如，其標準用戶端原則輪詢間隔期間)，Configuration.mof 會連接到原則本文。 這個檔案是然後下載並編譯的用戶端。 當您新增、 修改或刪除 Configuration.mof 檔案中的資料類別時，用戶端會自動編譯存貨相關的資料類別不會對這些變更。 不需要採取進一步的動作，就可以清查 Configuration Manager 用戶端上的新增或修改過的資料類別。 此檔案位於主要站台伺服器上的 **<CM 安裝位置\>\Inboxes\clifiles.src\hinv\\\** 中。  

 在 Configuration Manager 中，您無法再像 Configuration Manager 2007 中一樣編輯 sms_def.mof 檔案。 相反地，您可以啟用和停用 WMI 類別，以及使用用戶端設定來新增硬體清查所收集的新類別。 Configuration Manager 提供下列方法來擴充硬體清查。  

> [!NOTE]  
>  如果您已經手動變更 Configuration.mof 檔案來新增自訂清查類別，這些變更將會在您更新到 1602 版時遭到複寫。 若要在更新之後繼續使用自訂類別，您必須在更新到 1602 版之後，將這些變更新增到 Configuration.mof 檔案的 "Added extensions" 區段。  
> 不過，您不能修改此區段以外的任何部分，因為這些區段是保留給 Configuration Manager 修改。 您可以在下列目錄中找到您自訂的 Configuration.mof 備份︰  
> **< CM 安裝目錄\>\data\hinvarchive\\**。  

|方法|詳細資訊|  
|------------|----------------------|  
|啟用或停用現有的庫存類別|您可以啟用或停用 Configuration Manager 所使用的預設清查類別，也可以建立自訂用戶端設定，讓您可以從指定的用戶端集合收集不同的硬體清查類別。 如需詳細資訊，請參閱本主題中的 [啟用或停用現有清查類別](#BKMK_Enable) 程序。|  
|加入新的庫存類別|您可以從另一部裝置的 WMI 命名空間加入新的庫存類別。 如需詳細資訊，請參閱本主題中的 [新增清查類別](#BKMK_Add) 程序。|  
|匯入和匯出硬體清查類別|您可以匯入和匯出 Managed 物件格式 (MOF) 檔案包含從清查類別 Configuration Manager 主控台。 如需詳細資訊，請參閱本主題的 [匯入硬體清查類別](#BKMK_Import) 和 [匯出硬體清查類別](#BKMK_Export) 程序。|  
|建立 NOIDMIF 檔案|使用 NOIDMIF 檔案收集 Configuration Manager 無法清查的用戶端裝置相關資訊。 例如，您可能要收集裝置的資產數字資訊存在於只要在裝置上的標籤。 NOIDMIF 清查會自動關聯於它所收集從用戶端裝置。 如需詳細資訊，請參閱本主題的 [建立 NOIDMIF 檔案](#BKMK_NOIDMIF) 。|  
|建立 IDMIF 檔案|您可使用 IDMIF 檔案，來收集組織中尚未與 Configuration Manager 用戶端建立關聯之資產的資訊，例如投影機、 影印機及網路印表機。 如需詳細資訊，請參閱本主題的 [建立 IDMIF 檔案](#BKMK_IDMIF) 。|  

## <a name="procedures-to-extend-hardware-inventory"></a>擴充硬體清查的程序  
 使用下列程序擴充硬體清查 (如上表所述)。  

 這些程序可協助您設定硬體清查的預設用戶端設定並套用至您的階層中的所有用戶端。 如果您只想要將這些設定套用至部分用戶端，請建立自訂用戶端裝置設定，並將它指派給包含您要清查之裝置的集合。 如需有關如何建立自訂用戶端設定的詳細資訊，請參閱 [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md)。  

###  <a name="a-namebkmkenablea-to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> 啟用或停用現有清查類別  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] 。  

3.  按一下 [預設用戶端設定] 。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  在 **預設用戶端設定** ] 對話方塊中按一下 **硬體清查**。  

6.  在 **裝置設定** 清單中，按一下 **設定類別**。  

7.  在 **硬體清查類別** ] 對話方塊中，選取或清除的類別和要收集的硬體清查類別屬性。 您可以展開以選取或清除該類別中的個別屬性的類別。 使用 **清查類別搜尋** 欄位搜尋個別類別。  

    > [!IMPORTANT]  
    >  將新的類別新增至 Configuration Manager 硬體清查時，收集並傳送到站台伺服器的清查檔案大小將會增加。 這可能會對網路和 Configuration Manager 站台的效能造成負面影響。 啟用只想要收集的清查類別。  

8.  按一下 **確定** 以儲存您的變更並關閉 **硬體清查類別** 對話方塊。  

###  <a name="a-namebkmkadda-to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a> 新增清查類別  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

    > [!IMPORTANT]  
    >  您只能新增清查類別從最上層伺服器階層中以及藉由修改預設的用戶端設定。 此選項無法使用。 當您建立自訂的裝置設定  

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] 。  

3.  按一下 [預設用戶端設定] 。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  在 **預設用戶端設定** ] 對話方塊中按一下 **硬體清查**。  

6.  在 **裝置設定** 清單中，按一下 **設定類別**。  

7.  在 **硬體清查類別** ] 對話方塊中按一下 **新增**。  

8.  在 **加入硬體清查類別** ] 對話方塊中按一下 **連接**。  

9. 在 **連線到 Windows Management Instrumentation (WMI)** ] 對話方塊中，指定您將從中擷取 WMI 類別以及要用來擷取類別的 WMI 命名空間的電腦名稱。 如果您想要擷取您所指定的 WMI 命名空間底下的所有類別、 按一下 **遞迴**。 如果您要連接到電腦不是本機電腦，提供有權存取 WMI 遠端電腦上的帳戶登入認證。  

10. 按一下 **[Connect]**(連線)。  

11. 在 [新增硬體清查類別] 對話方塊的 [清查類別] 清單中，選取您想要新增至 Configuration Manager 硬體清查的 WMI 類別。  

12. 如果您想要編輯選取的 WMI 類別的相關資訊，請按一下 **編輯**, ，然後在 **類別限定詞** ] 對話方塊中，提供下列資訊:  

    -   **顯示名稱** - 指定將在資源總管中顯示之類別的易記名稱。  

    -   **內容** – 指定將用來顯示 WMI 類別之每個內容的單位。  

     您也可以指定屬性做為索引鍵屬性來唯一識別每個類別的執行個體。 如果此類別定義任何索引鍵和多個執行個體的類別會報告從用戶端，只有最新發現的執行個體儲存在資料庫中。  

     當您完成設定屬性時，按一下 **確定** 關閉 **類別限定詞** 對話方塊。  

13. 按一下 [確定] 關閉 **加入硬體清查類別** 對話方塊。  

14. 按一下 **確定** 關閉 **硬體清查類別** 對話方塊。  

15. 按一下 **確定** 關閉 **預設用戶端設定** 對話方塊。  

###  <a name="a-namebkmkimporta-to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> 匯入硬體清查類別  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] 。  

3.  按一下 [預設用戶端設定] 。  

    > [!IMPORTANT]  
    >  當您修改預設的用戶端設定時您可以只匯入清查類別。 不過，您可以使用自訂用戶端設定匯入不包含結構描述變更，例如變更從現有類別的屬性資訊 **True** 至 **False**。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  在 **預設用戶端設定** ] 對話方塊中按一下 **硬體清查**。  

6.  在 **裝置設定** 清單中，按一下 **設定類別**。  

7.  在 **硬體清查類別** ] 對話方塊中按一下 **匯入**。  

8.  在 **匯入** 對話方塊中選取受管理物件格式 (MOF) 檔，您想要匯入，然後按一下 **確定**。  

9. 在 **匯入摘要** ] 對話方塊中，檢閱將匯入，然後按一下的項目 **匯入**。  

###  <a name="a-namebkmkexporta-to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> 匯出硬體清查類別  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] 。  

3.  按一下 [預設用戶端設定] 。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  在 **預設用戶端設定** ] 對話方塊中按一下 **硬體清查**。  

6.  在 **裝置設定** 清單中，按一下 **設定類別**。  

7.  在 **硬體清查類別** ] 對話方塊中按一下 **匯出**。  

    > [!NOTE]  
    >  當您匯出類別時時就會匯出所有目前選取的類別。  

8.  在 [匯出]  對話方塊中，指定您要將類別匯出至其中的管理物件格式 (MOF) 檔案，然後按一下 [儲存] 。  

## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>如何使用管理資訊檔案 (MIF 檔案) 來擴充硬體清查  
 使用管理資訊格式 (MIF) 檔案，來延伸透過 Configuration Manager 從用戶端收集到的硬體清查資訊。 硬體清查期間 MIF 檔案中儲存的資訊加入至用戶端清查報告，並儲存在網站資料庫，您可以在其中使用您使用預設用戶端清查資料的相同方式中的資料。 有兩種類型的 MIF 檔案 NOIDMIF 和 IDMIF。

> [!IMPORTANT]  
>  將資訊從 MIF 檔案新增至 Configuration Manager 資料庫之前，您必須建立或匯入其類別資訊。 如需詳細資訊，請參閱本主題中的 [新增清查類別](#BKMK_Add) 和 [匯入硬體清查類別](#BKMK_Import) 小節。  

###  <a name="a-namebkmknoidmifa-to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> 建立 NOIDMIF 檔案  
 NOIDMIF 檔案可以用來將資訊新增至 Configuration Manager 通常無法收集且與特定用戶端裝置相關聯的用戶端硬體清查。 比方說，許多公司都加上標籤與資產編號組織中的每一部電腦與手動 catalogue 這些。 當您建立 NOIDMIF 檔案時，這項資訊可以新增至 Configuration Manager 資料庫並用於查詢和報告。 如需建立 NOIDMIF 檔案的相關資訊，請參閱 Configuration Manager SDK 文件。  

> [!IMPORTANT]  
>  當您建立 NOIDMIF 檔案時，這必須以 ANSI 編碼格式儲存。 Configuration Manager 無法讀取以 UTF-8 編碼格式儲存的 NOIDMIF 檔案。  

 建立 NOIDMIF 檔案之後，這個資料夾中儲存這 *%windir%***\System32\CCM\Inventory\Noidmifs** 每個用戶端上的資料夾。 在下次排程的硬體清查週期，Configuration Manager 會從這個資料夾中的 NODMIF 檔案收集資訊。  

###  <a name="a-namebkmkidmifa-to-create-idmif-files"></a><a name="BKMK_IDMIF"></a> 建立 IDMIF 檔案  
 IDMIF 檔案可以用來將資產相關資訊新增至 Configuration Manager 通常無法清查且與特定用戶端裝置不相關的 Configuration Manager 資料庫。 例如，您可以使用 IDMIFS 收集下列項目的相關資訊：投影機，DVD 播放機、影印機或不包含 Configuration Manager 用戶端的其他設備。 如需建立 IDMIF 檔案的相關資訊，請參閱 Configuration Manager SDK 文件。  

 建立 IDMIF 檔案之後，這個資料夾中儲存這 *%windir%***\System32\CCM\Inventory\Idmifs** 用戶端電腦上的資料夾。 在下次排程的硬體清查週期，Configuration Manager 會從這個檔案收集資訊。 您必須宣告新類別，藉由新增或匯入這些檔案中包含的資訊。  

> [!NOTE]
> MIF 檔案可能包含大量資料，而且收集這項資料可能會對站台效能造成負面影響。 只在需要時才啟用 MIF 收集，並在硬體清查設定中設定 [自訂 MIF 檔案大小上限 (KB)]  選項。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的硬體清查簡介](introduction-to-hardware-inventory.md)。



<!--HONumber=Dec16_HO3-->


