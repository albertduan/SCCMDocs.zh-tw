---
title: "透過網路使用軟體中心部署 Windows | Configuration Manager"
description: "您可以將作業系統部署至 Software Center，以使用新版本的 Windows 重新整理現有電腦，或將 Windows 升級至最新版本。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 189fdac38760b75eb3795348f6af4ef7e83c3f20


---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>使用軟體中心透過網路利用 System Center Configuration Manager 部署 Windows

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 中安裝作業系統的工作順序，可於軟體中心內提供。 在下列作業系統部署案例中，您可以將作業系統部署到軟體中心：  

-   [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [將 Windows 升級至最新版本](upgrade-windows-to-the-latest-version.md)  

 完成任一作業系統部署案例中的步驟，然後使用以下各節準備可在軟體中心內進行的部署。  

## <a name="configure-deployment-settings"></a>設定部署設定  
 當您想要在軟體中心內提供作業系統部署時，必須將部署設定為讓 Configuration Manager 用戶端可以使用該作業系統。 您可以在 [部署軟體精靈] 的 [部署設定]  頁面上設定此項目，或是在部署的內容之 [部署設定]  索引標籤上設定此項目。  如果是 [供下列項目使用]  設定，請設定 [只有 Configuration Manager 用戶端]  或是 [Configuration Manager 用戶端、媒體與 PXE] 。 在部署完作業系統之後，它就會顯示在目標集合成員的「軟體中心」內。  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> 將工作順序部署到電腦  
 將作業系統部署至目標集合。 如需詳細資訊，請參閱 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。 當您部署軟體中心的作業系統時，可設定部署是否為需要部署或是提供進行部署。  

-   **需要部署**：需要部署會在軟體中心內提供作業系統，而且會在設定的指派排程時自動啟動。  

-   **提供進行部署**：軟體中心內會提供作業系統，使用者可於需求時安裝該作業系統。  



<!--HONumber=Nov16_HO1-->


