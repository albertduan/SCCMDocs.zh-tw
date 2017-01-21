---
title: "透過網路使用可開機媒體部署 Windows | Configuration Manager"
description: "使用 System Center Configuration Manager 中的可開機媒體部署，以在啟動目的地電腦時部署作業系統。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f5bdba0f609f51b988dbfdc0b0c8b204405f834a


---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>透過網路利用 System Center Configuration Manager 使用可開機媒體部署 Windows

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的可開機媒體部署可讓您在啟動目的地電腦時部署作業系統。 目的地電腦啟動時，會從網路擷取工作順序、作業系統映像，以及任何其他必要的內容。 由於媒體不包含該內容，因此您可以直接更新內容，而不需要重新建立媒體。  

 在下列作業系統部署案例中使用多點傳送，可以透過網路部署作業系統：  

-   [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

-   [取代現有的電腦和傳輸設定](replace-an-existing-computer-and-transfer-settings.md)  

 完成任一作業系統部署案例中的步驟，然後使用以下各節利用可開機媒體部署作業系統。  

## <a name="configure-deployment-settings"></a>設定部署設定  
 當您使用可開機媒體啟動作業系統部署程序時，必須將部署設定為要對媒體提供作業系統。 您可以在 [部署軟體精靈] 的 [部署設定]  頁面上設定此項目，或是在部署的內容之 [部署設定]  索引標籤上設定此項目。  如果是 [供下列項目使用]  設定，請設定下列其中之一：  

-   **Configuration Manager 用戶端、媒體與 PXE**  

-   **僅媒體與 PXE**  

-   **僅媒體與 PXE (隱藏)**  

## <a name="create-the-bootable-media"></a>建立可開機媒體  
 您可以指定可開機媒體為 USB 快閃磁碟機或 CD/DVD 組。 將啟動媒體的電腦，必須能提供選項供您選擇作為可開機磁碟機。 如需詳細資訊，請參閱[建立可開機媒體](create-bootable-media.md)。  

##  <a name="a-namebkmkdeploya-install-the-operating-system-from-bootable-media"></a><a name="BKMK_Deploy"></a> 從可開機媒體安裝作業系統  
 在電腦的可開機磁碟機中插入可開機媒體，然後打開電源來安裝作業系統。  



<!--HONumber=Nov16_HO1-->


