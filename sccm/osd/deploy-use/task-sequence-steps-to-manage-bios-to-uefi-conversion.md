---
title: "用於管理 BIOS 轉換到 UEFI 的工作順序步驟 | Configuration Manager"
description: "了解如何自訂作業系統部署工作順序，以準備轉換到 UEFI 的 FAT32 磁碟分割。"
ms.custom: na
ms.date: 11/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c92d88517b4e1d54add489a53cd34b0f23be0c4c
ms.openlocfilehash: 04951b3ed50206941850ddcc893fcf9c9596f89f


---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>用於管理 BIOS 轉換到 UEFI 的工作順序步驟
從 Configuration Manager 1610 版開始，您現在可以使用新變數 TSUEFIDrive 來自訂作業系統部署工作順序，如此一來，[重新啟動電腦] 步驟就會在硬碟上準備用於轉換成 UEFI 的 FAT32 磁碟分割。 下列程序提供範例，說明如何建立工作順序步驟，以準備用於將 BIO 轉換成 UEFI 的硬碟。

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>若要準備用於轉換成 UEFI 的 FAT32 磁碟分割：
在安裝作業系統的現有工作順序中，您將新增具有執行 BIOS 轉換成 UEFI 之步驟的新群組。

1. 在擷取檔案和設定的步驟之後，以及安裝作業系統的步驟之前，建立新的工作順序群組。 例如，在 [擷取檔案和設定] 之後，建立名為 **BIOS-to-UEFI** 的群組。
2. 在新群組的 [選項] 索引標籤中，新增工作順序變數作為條件，其中 **_SMSTSBootUEFI** **不等於** **true**。 當電腦已在 UEFI 模式時，這會防止執行群組中的步驟。

   ![BIOS to UEFI 群組](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. 在新群組底下，新增 [重新啟動電腦] 工作順序步驟。 在 [指定重新啟動後執行的項目] 中，選取 [指派給此工作順序的開機映像] 以在 Windows PE 中啟動電腦。  
4. 在 [選項] 索引標籤上，新增工作順序變數作為條件，其中 **_SMSTSInWinPE 等於 false**。 如果電腦已在 Windows PE 中，這會防止執行此步驟。

    ![重新啟動電腦步驟](../../core/get-started/media/restart-in-windows-pe.png)
5. 新增啟動 OEM 工具的步驟，以將韌體從 BIOS 轉換成 UEFI。 這通常會是 [執行命令列] 工作順序步驟，其中包含啟動 OEM 工具的命令列。
6.  新增 [格式化和分割磁碟] 工作順序步驟，對硬碟進行分割與格式化。 在此步驟中，執行下列動作：
    1.  安裝作業系統之前，先建立將轉換成 UEFI 的 FAT32 磁碟分割。 選擇 [GPT] 作為 [磁碟類型]。

       ![格式化和分割磁碟步驟](../media/format-and-partition-disk.png)
    2.  移至 FAT32 的 [磁碟分割內容]。 在 [變數] 欄位中輸入 **TSUEFIDrive**。 當工作順序偵測到此變數時，它會準備 UEFI 轉換，再重新啟動電腦。

       ![磁碟分割內容](../../core/get-started/media/partition-properties.png)
    3. 建立工作順序引擎用來儲存其狀態及存放記錄檔的 NTFS 磁碟分割。
7.  新增 [重新啟動電腦] 工作順序步驟。 在 [指定重新啟動後執行的項目] 中，選取 [指派給此工作順序的開機映像] 以在 Windows PE 中啟動電腦。  



<!--HONumber=Jan17_HO1-->


