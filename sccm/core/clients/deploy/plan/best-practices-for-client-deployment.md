---
title: "用戶端部署的最佳做法 | System Center Configuration Manager"
description: "取得在 System Center Configuration Manager 中進行用戶端部署的最佳做法。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: 11
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 22a34dce45e655dca1ddcb3dfe1bb0105c4026c1


---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中進行用戶端部署的最佳做法

適用於：System Center Configuration Manager (最新分支)

請利用以下最佳做法資訊來協助您在 System Center Configuration Manager 的電腦上部署用戶端。  

## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>針對 Active Directory 電腦使用以軟體更新為基礎的用戶端安裝  
 此用戶端部署方法具備使用現有 Windows 技術的優勢，並與 Active Directory 基礎結構整合 (在 Configuration Manager 中需要最低的設定)，針對防火牆的設定最為輕鬆，同時安全性也最高。 針對群組原則設定使用安全性群組和 WMI 篩選之外，您還擁有許多彈性可控制哪些電腦安裝 Configuration Manager 用戶端。  

 如需詳細資訊，請參閱 [如何使用以軟體更新為基礎的安裝來安裝 Configuration Manager 用戶端](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP)。  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>延伸 Active Directory 架構並發佈站台，使您不用命令列選項就可執行 CCMSetup。  
 當您擴充 Configuration Manager 的 Active Directory 架構並將站台發佈至 Active Directory 網域服務時，許多用戶端安裝內容也會發佈至 Active Directory 網域服務。 如果電腦可以找到這些用戶端安裝內容，就可在 Configuration Manager 用戶端部署期間使用。 由於這是自動產生的資訊，因此可以排除手動輸入安裝內容所可能出現的人為錯誤風險。  

 如需詳細資訊，請參閱[關於 System Center Configuration Manager 中發佈至 Active Directory 網域服務的用戶端安裝內容](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)。  

## <a name="when-you-have-many-clients-to-deploy-plan-a-phased-rollout-outside-business-hours"></a>如果您有許多待部署的用戶端，請規劃工作時間以外的分階段導入  
 您可以規劃一段時間內的用戶端分階段導入，將站台伺服器上的 CPU 處理需求效應降到最低。 在工作時間以外部署用戶端可讓關鍵業務服務有較多的可用頻寬，且當電腦執行速度變慢或需要重新啟動以完成安裝時，使用者也不會受到干擾。  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>在完成主要用戶端部署之後啟用自動升級  
 當您想要針對一小部分可能已被主要用戶端安裝方法遺漏的用戶端電腦進行升級時，自動用戶端升級就非常有用。 例如，您已完成初始用戶端升級，但某些用戶端在升級部署期間離線。 當這些電腦下次啟用時，您就可以使用此方法來升級電腦上的用戶端。  

> [!NOTE]  
>  Configuration Manager 的效能提升可讓您使用自動升級作為主要的用戶端升級方法。 不過，實際效能將視階層基礎結構而定，例如用戶端的數目。  

 如需用戶端自動升級方法的詳細資訊，請參閱[如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>如果您使用 client.msi 內容安裝用戶端，請使用 SMSMP 和 FSP  
 SMSMP 內容會指定要與用戶端通訊的初始管理點，並移除 Active Directory 網域服務、DNS 和 WINS 等服務位置解決方案上的相依性。  

 使用 FSP 內容並安裝後援狀態點，使您可以監控用戶端安裝和指派，並識別任何的通訊問題。  

 如需這些選項的詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端安裝內容](../../../../core/clients/deploy/about-client-installation-properties.md)。  

## <a name="if-you-want-to-use-client-languages-other-than-english-install-the-client-language-packs-before-you-install-the-clients"></a>如果您要使用英文以外的用戶端語言，請在安裝用戶端之前安裝用戶端語言套件  
 如果您在安裝用戶端之後才在站台上安裝用戶端語言套件，則必須重新安裝用戶端才能讓其使用其他語言。 對行動裝置用戶端來說，這表示您必須在抹除行動裝置後再次進行註冊。  

 如需新增其他用戶端語言支援方式的詳細資訊，請參閱 [System Center Configuration Manager 中的語言套件](../../../../core/servers/deploy/install/language-packs.md)。  

## <a name="plan-and-prepare-any-required-pki-certificates-in-advance"></a>事先規劃並準備任何必要的 PKI 憑證  
 若要在網際網路、已註冊的行動裝置和 Mac 電腦上管理裝置，您的站台系統 (管理點和發佈點) 和用戶端裝置上都必須有 PKI 憑證。 對於許多的客戶來說，這需要進行進階的規劃和準備，尤其當 PKI 是由個別的團隊進行管理時更需如此。 在生產網路中，您可能需要變更管理核准才能使用新的憑證、重新啟動站台系統伺服器，或者使用者可能必須登出後再登入以取得新的群組成員資格。 此外，您可能必須提供足夠的時間來複寫安全性權限，並提供任何新的憑證範本。  

 如需必要 PKI 憑證的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>在安裝用戶端之前，設定任何必要的用戶端設定和維護期間  
 雖然您可以在安裝用戶端之前或之後設定用戶端設定和維護期間，仍建議您在安裝用戶端之前完成任何必要的設定，以便您在安裝用戶端後立即使用這些設定。 如需詳細資訊，請參閱 [如何在 System Center Configuration Manager 中設定用戶端設定](../../../../core/clients/deploy/configure-client-settings.md)  

 針對伺服器和 Windows Embedded 裝置設定維護期間，以確保這些經常攸關業務之電腦的商務持續性。 例如，維護期間可確保必要的軟體更新和反惡意程式碼軟體不會在工作時間內重新啟動電腦。  

> [!IMPORTANT]  
>  對於您打算要透過統一寫入篩選器 (UWF) 保護的 Windows 10 電腦，您必須先針對 UWF 設定裝置，才能安裝用戶端。 這可讓 Configuration Manager 安裝具有自訂認證提供者的用戶端，以鎖定低權限使用者，防止他們在維護模式期間登入裝置。  

## <a name="for-mac-computers-and-mobile-devices-that-are-enrolled-by-configuration-manager-plan-your-user-enrollment-experience"></a>針對由 Configuration Manager 註冊的 Mac 電腦和行動裝置，請規劃您的使用者註冊經驗  
 如果使用者將使用 Configuration Manager 來註冊他們自己的 Mac 電腦和行動裝置，請規劃並準備使用者體驗。 例如，您可以使用網頁來編寫安裝和註冊程序，讓使用者只需要輸入最少量的必要資訊，您也可以透過電子郵件傳送說明的連結。  

## <a name="when-you-manage-windows-embedded-devices-use-file-based-write-filters-fbwf-rather-than-enhanced-write-filters-ewf-for-higher-scalability"></a>當您管理 Windows Embedded 裝置時，請使用檔案型寫入篩選器 (FBWF) 而非增強式寫入篩選器 (EWF)，以取得更高的延展性  
 使用增強式寫入篩選器 (EWF) 的 Embedded 裝置可能會發生狀態訊息重新同步處理。 如果您只有少數的 Embedded 裝置會使用增強式寫入篩選器，您可能不會注意到此現象。 不過，如果您有許多 Embedded 裝置會重新同步處理其資訊 (例如傳送完整清查而非差異清查)，則會在站台伺服器上產生可觀的網路封包以及大量的 CPU 處理。  

 如果您可以選擇要啟用的寫入篩選器類型，請選擇檔案型寫入篩選器，並設定例外狀況以保存裝置重新啟動期間的用戶端狀態和清查資料，確保 Configuration Manager 用戶端上的網路和 CPU 效率。 如需寫入篩選器的詳細資訊，請參閱   [規劃將用戶端部署至 System Center Configuration Manager 中的Windows Embedded 裝置](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)。  

 如需主要站台可支援之 Windows Embedded 用戶端數量上限的詳細資訊，請參閱[支援的用戶端與裝置作業系統](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。  



<!--HONumber=Nov16_HO1-->


