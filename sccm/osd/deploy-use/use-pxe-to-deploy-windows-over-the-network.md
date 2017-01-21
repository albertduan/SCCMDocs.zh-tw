---
title: "使用 PXE 透過網路部署 Windows | Microsoft Docs"
description: "使用 PXE 起始作業系統部署來重新整理電腦的作業系統，或在新電腦上安裝新的 Windows 版本。"
ms.custom: na
ms.date: 12/07/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
caps.latest.revision: 19
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3f44505c977b511223a083a960f871371c0ff133
ms.openlocfilehash: b22cdbd42693078caa47f41182ce73ea881c3515


---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>利用 System Center Configuration Manager 使用 PXE 透過網路來部署 Windows

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的 PXE 起始作業系統部署，可讓用戶端電腦透過網路要求與部署作業系統。 在這種作業系統部署案例中，會將作業系統映像和 x86 及 x64 Windows PE 開機映像傳送至設定接受 PXE 開機要求的發佈點。  

> [!NOTE]  
>  當您建立僅以 x64 BIOS 電腦為目標的作業系統部署時，x64 開機映像和 x86 開機映像在發佈點上都必須為可用狀態。  

 在下列作業系統部署案例中，您可以使用 PXE 起始作業系統部署：  

-   [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

 完成任一作業系統部署案例中的步驟，然後使用下列章節準備 PXE 起始部署。  

##  <a name="a-namebkmkconfigurea-configure-at-least-one-distribution-point-to-accept-pxe-requests"></a><a name="BKMK_Configure"></a> 將至少一個發佈點設定為接受 PXE 要求  
 若要將作業系統部署至發出 PXE 開機要求的 Configuration Manager 用戶端，您必須使用設定為回應 PXE 開機要求的其中一個或多個發佈點。  如需在發佈點上啟用 PXE 的步驟，請參閱[設定發佈點接受 PXE 要求](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)。  

## <a name="prepare-a-pxe-enabled-boot-image"></a>準備啟用 PXE 的開機映像  
 若要使用 PXE 以部署作業系統，您必須擁有 x86 和 x64 的支援 PXE 開機映像，以發佈到一個或多個支援 PXE 的發佈點。 使用資訊在開機映像上啟用 PXE，並將開機映像發佈到發佈點：  

-   若要在開機映像上啟用 PXE，請從開機映像內容中的 [資料來源]   索引標籤，選取 [從支援 PXE 的發佈點部署此開機映像]  。  

-   如果您變更開機映像的內容，請將開機映像重新發佈至發佈點。 如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)。  

##  <a name="a-namebkmkpxeexclusionlista-create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> 建立 PXE 部署的排除清單  
 當您使用 PXE 部署作業系統時，您可以在每個發佈點建立排除清單，以略過排除清單中電腦上的 PXE 開機要求。 排除清單包含您要讓發佈點忽略的電腦 MAC 位址。 這些電腦將不會接收 Configuration Manager 用來進行 PXE 部署的部署工作順序。  

 利用下列步驟建立 PXE 排除清單。  

#### <a name="to-create-the-exclusion-list"></a>建立排除清單  

1.  在啟用 PXE 的發佈點上建立文字檔。 例如，將此文字檔命名為 **pxeExceptions.txt**。  

2.  使用標準文字編輯器 (像是記事本)，並新增啟用 PXE 的發佈點要忽略的電腦 MAC 位址。 以分號分隔 MAC 位址值，且一行輸入一個位址。 例如： `01:23:45:67:89:ab`  

3.  將文字檔儲存在啟用 PXE 的發佈點站台系統伺服器上。 文字檔可以儲存到伺服器上的任何位置。  

4.  編輯啟用 PXE 之發佈點的登錄建立 **MACIgnoreListFile** 登錄機碼，其中包含啟用 PXE 的發佈點站台系統伺服器上文字檔位置之完整路徑的字串值。 使用下列登錄路徑：  

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  如果您不當使用登錄編輯程式，可能造成嚴重的問題，而需要重新安裝作業系統。 Microsoft 無法保證您可以解決因不正確使用登錄編輯程式所造成的問題。 您必須自行承擔使用登錄編輯器的風險。  

     進行這項登錄變更後，不需要重新啟動伺服器。  

##  <a name="a-namebkmkramdisktftparamdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a>RamDisk TFTP 區塊大小和視窗大小  
您可以為支援 PXE 的發佈點自訂 RamDisk TFTP 區塊大小，而從 Configuration Manager 1606 版開始，也可以自訂視窗大小。 如果您已自訂網路，可能會導致開機映像下載因發生逾時錯誤而失敗，因為區塊或視窗大小太大。 自訂 RamDisk TFTP 區塊大小和視窗大小可讓您在使用 PXE 來滿足特定的網路需求時，將 TFTP 流量最佳化。 您將需要在您的環境中測試自訂的設定，以確定最有效率的設定是哪一個。 如需詳細資訊，請參閱[自訂支援 PXE 之發佈點的相關 RamDisk TFTP 區塊大小和視窗大小](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)。

## <a name="configure-deployment-settings"></a>設定部署設定  
 若要使用 PXE 起始的作業系統部署，必須設定部署，讓作業系統可供 PXE 開機要求使用。 您可以在 [部署軟體精靈] 的 [部署設定]  頁面上設定此項目，或是在部署的內容之 [部署設定]  索引標籤上設定此項目。  如果是 [供下列項目使用]  設定，請設定下列其中之一：  

-   Configuration Manager 用戶端、媒體與 PXE  

-   僅媒體與 PXE  

-   僅媒體與 PXE (隱藏)  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> 部署工作順序  
 將作業系統部署至目標集合。 如需詳細資訊，請參閱 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。 當您使用 PXE 部署作業系統時，可設定部署是否為需要部署或是提供進行部署。  

-   **必要的部署**：必要的部署將會使用 PXE，完全不需要任何使用者操作。 使用者將無法略過 PXE 開機。 然而，如果使用者在發佈點回應之前取消 PXE 開機，將不會部署作業系統。  

-   **可用的部署**：可用的部署會要求使用者出現在目的地電腦，如此，使用者就可按下 F12 鍵繼續處理 PXE 開機。 如果使用者不在電腦端，無法按下 F12 鍵，電腦將會開機到目前的作業系統，或是從下一個可用的開機裝置開機。  

 您可以藉由清除指派到 Configuration Manager 集合或電腦的最後一個 PXE 部署狀態，重新部署必要的 PXE 部署。 此動作會重設該部署的狀態，並重新部署最新的必要部署。  

> [!IMPORTANT]  
>  PXE 通訊協定不安全。 請確認 PXE 伺服器及 PXE 用戶端皆位於實體上安全的網路，例如位於資料中心可防止對於您站台的未授權存取。  

##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>如何為使用 PXE 開機的用戶端選取開機映像？
用戶端使用 PXE 開機時，Configuration Manager 會將要使用的開機映像提供給用戶端。 從 Configuration Manager 1606 版開始，Configuration Manager 使用具有確切相符架構的開機映像 (如果有的話)。 如果找不到具有確切架構的開機映像，Configuration Manager 會使用具有相容架構的開機映像。 下列清單提供如何為使用 PXE 開機的用戶端選取開機映像的詳細資料。
1. Configuration Manager 會查看站台資料庫中是否有系統記錄符合嘗試開機的用戶端的 MAC 位址或 SMBIOS。
    > [!NOTE]
    > 如果指派給站台的電腦會開機至不同站台的 PXE，就不會顯示適用於該電腦的原則。 例如，如果已經將用戶端指派給站台 A，站台 B 上的管理點和發佈點將無法存取站台 A 的原則，而用戶端就不會成功進行 PXE 開機。
2. Configuration Manager 會尋找部署至步驟 1 中所找到之系統記錄的工作順序。
3. 在步驟 2 中找到的工作順序清單中，Configuration Manager 會尋找符合嘗試開機的用戶端架構的開機映像。 如果找到相同架構的開機映像，則會使用該開機映像。

4. 如果找不到具有相同架構的開機映像，Configuration Manager 會尋找與嘗試開機的用戶端架構相符的開機映像 (從步驟 2 中找到的工作順序清單中)。 例如，64 位元用戶端與 32 位元和 64 位元開機映像相容。 32 位元用戶端僅與 32 位元開機映像相容。 UEFI 用戶端僅與 64 位元開機映像相容。



<!--HONumber=Dec16_HO3-->


