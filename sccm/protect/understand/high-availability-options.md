---
title: "高可用性 | System Center Configuration Manager"
description: "了解如何使用維持高可用度服務的選項部署 System Center Configuration Manager。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7d8dff8779fbf146a57f753dee9f98488fa5fa61

---
# <a name="high-availability-options-for-system-center-configuration-manager"></a>System Center Configuration Manager 的高可用性選項

*適用於：System Center Configuration Manager (最新分支)*



您可以使用維持高可用度服務的選項部署 System Center Configuration Manager。   

支援高可用性的選項︰   

-   站台可支援提供用戶端重要服務的多重站台系統伺服器執行個體。  

-   管理中心網站和主要站台皆支援站台資料庫備份。 站台資料庫包含站台及用戶端的所有設定，而且能在包含管理中心網站的階層各站台之間共用。  

-   內建站台復原選項可減少伺服器停機時間，而且所包含的進階選項可在您擁有內含管理中心網站之階層時簡化復原程序。  

-   用戶端可以自動補救常見的問題，不需要系統管理員操作。  

-   站台會產生關於用戶端提交最近資料失敗的警示，以警告系統管理員可能有問題發生。  

-   Configuration Manager 會提供數個內建報告，讓您能在問題影響到伺服器或用戶端操作之前就識別出問題與趨勢。  

 Configuration Manager 不提供即時服務，您必須對操作上的資料延遲有心理準備。 因此，多數涉及服務暫時中斷的情形通常不太會變成重大的問題。 當您以高可用性設定站台及階層時，可以將停機時間降到最低、維持自主性操作，並且提供高層級服務。  

 例如，Configuration Manager 用戶端通常會使用已知的排程與操作設定進行自主性操作，並且排定將資料提交至站台處理的時程。  

-   當用戶端無法連絡站台時，便會快取待提交的資料，直到連絡上站台。  

-   無法連絡站台的用戶端會使用最後的已知排程與快取資訊，持續進行操作 (例如先前已下載，而且必須執行或安裝的應用程式)，直到可以連絡上站台並接收新原則為止。  

-   站台會監視其站台系統與用戶端的定期狀態更新，並且在無法登錄時產生警示。  

-   內建報告可提供進行中操作，以及歷史操作與趨勢的深入探索。 Configuration Manager 也支援狀態訊息，其提供進行中操作的近即時資訊。  

  使用本主題及下列文章中的資訊︰
-   [建議的硬體](../../core/plan-design/configs/recommended-hardware.md)
-   [支援的站台系統伺服器作業系統](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  

-   [站台和站台系統必要條件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)


##  <a name="a-namebkmksnha-high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a> 站台和階層的高可用性  
 **使用 SQL Server 叢集裝載站台資料庫：**  

 當您將 SQL Server 叢集用於管理中心網站或次要站台的資料庫時，便會使用 SQL Server 內建的容錯轉移支援。  

 次要站台無法使用 SQL Server 叢集，並且不支援站台資料庫的備份或還原。 從父主要站台重新安裝次要站台，以復原次要站台。  

 **使用 SQL Server AlwaysOn 可用性群組裝載站台資料庫：**  

 從 1602 版開始，您可以使用 SQL Server AlwaysOn 可用性群組於主要站台和管理中心網站裝載站台資料庫，以做為高可用性和災害復原方案。 如需詳細資訊，請參閱[適用於 System Center Configuration Manager 之高可用性站台資料庫的 SQL Server AlwaysOn](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。  

 **使用管理中心網站及一個或多個子主要站台部署站台的階層：**  

 此設定可在您的站台管理網路的重疊區段時，提供容錯功能。 此外，此設定可提供其他的復原選項，如此才能使用其他站台可用的共用資料庫資訊，藉以在復原的站台重建站台資料庫。 您可以使用此選項，取代失敗或無法使用的失敗站台資料庫備份。  

 **在管理中心網站及主要站台建立標準備份**  

 當您建立和測試標準站台備份時，可確定您具有復原站台所需的資料，以及在最短時間內復原站台的經驗。  

 **安裝多重站台系統角色執行個體**  

 當您安裝多個重要站台系統角色執行個體時 (如管理點或發佈點)，便會提供用戶端特定站台系統伺服器離線時的重複連絡點。  

 **於站台安裝多個 SMS 提供者的執行個體：**SMS 提供者針對一或多個 Configuration Manager 主控台提供系統管理連絡點。 當您安裝多重 SMS 提供者時，可提供連絡點複本以管理站台和階層。  

##  <a name="a-namebkmkssra-high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a> 站台系統角色的高可用性  
 在各個站台，您可以部署站台系統角色以提供您要用戶端在該站台使用的服務。 站台資料庫中包含站台與所有用戶端的設定資訊。 使用一個或多個可用選項，提供站台資料庫的高可用性，如有必要也可提供站台與站台資料庫的復原。  

 **重要站台系統角色的複本**  

-   應用程式類別目錄 Web 服務點  

-   應用程式類別目錄網站點  

-   發佈點  

-   管理點  

-   軟體更新點  

-   狀態移轉點  

 您可以安裝 Reporting Services 點角色的多個執行個體，以提供站台與用戶端上的報告複本 ：

 您可以在 Windows 網路負載平衡 (NLB) 叢集上使用 PowerShell 安裝軟體更新點站台系統角色，以提供容錯移轉支援  


 **內建站台備份：**  

 Configuration Manager 包含內建的備份工作，可協助您依定期排程備份站台及重要資訊。 此外，Configuration Manager 安裝精靈支援站台還原動作，協助您將網站還原作業。  

 **發佈至 Active Directory 網域服務及 DNS**  

 您可以將各站台設定為將有關站台系統伺服器與服務的資料，發佈至 Active Directory 網域服務及 DNS。 如此可讓用戶端識別網路上最容易存取的伺服器，以及識別出可提供重要服務 (如管理點) 的新站台系統伺服器 可用時。  

 **SMS 提供者與 Configuration Manager 主控台：**  

 Configuration Manager 支援安裝多個 SMS 提供者，每一個都位於個別的電腦上，以確保 Configuration Manager 主控台的多個存取點。 如此可確保當 SMS 提供者電腦離線時，您仍可檢視及重新設定 Configuration Manager 站台與用戶端。  

 當 Configuration Manager 主控台連線至站台時，它會連線至該站台的 SMS 提供者的執行個體。 非確定性地選取 SMS 提供者執行個體。 如果選取的 SMS 提供者無法使用，下列選項可供您選擇：  

-   將主控台重新連線至站台。 各個新連線要求皆會被非確定性地指派一個 SMS 提供者執行個體，因此有可能會指派可用的執行個體給新連線。  

-   將主控台連線到不同的 Configuration Manager 站台，並從該連線管理設定。 如此會使設定變更稍微延遲幾分鐘不到。 在站台的 SMS 提供者上線後，您可以直接將 Configuration Manager 主控台重新連線至您要管理的站台。  

 您可以在多部電腦上安裝 Configuration Manager 主控台，以供系統管理使用者使用。 每個 SMS 提供者支援來自多個 Configuration Manager 主控台的連線。  

 **管理點：**  

 在各個主要站台上安裝多個管理點，並且使站台將站台資料發佈至 Active Directory 基礎結構及 DNS。  

 多個管理點有助於平衡多用戶端使用單一管理點時的負載。 此外，您也可以安裝一個或多個管理點的資料庫複本，以減少需要大量使用 CPU 的管理點的操作，並增加此重要站台系統角色的可用性。  

 由於您只能在次要站台 (必須位於次要站台伺服器) 中安裝一個管理點，因此不會將次要站台的管理點視為具有高度可用性設定。  

> [!NOTE]  
>  內部部署行動裝置管理所管理的裝置只能連接到主要站台的一個管理點。 管理點是由 Configuration Manager 在註冊期間指派至行動裝置，不會變更。 當您安裝多個管理點，並且啟用一個以上的的行動裝置時，指派至行動裝置用戶端的管理點不具有確定性。  
>   
>  如果行動裝置所使用的管理點變成無法使用，您必須解決該管理點的問題，或是清除行動裝置並重新註冊行動裝置，以便它可以重新指派至針對行動裝置啟用的操作管理點。  

 **發佈點：**  

 安裝多個發佈點，並將內容部署至多個發佈點。 您可以設定內容位置的重疊界限群組，以確保各子網路上的用戶端可從兩個或更多發佈點存取部署。 最後，請考慮將一個或多個發佈點設定為內容的後援位置。  

 如需內容後援位置的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

 **應用程式類別目錄 Web 服務點與應用程式類別目錄網站點：**  

 您可以安裝每個站台系統角色的多個執行個體，為了取得最佳效能，請在相同站台系統電腦上部署每個角色的其中一個。  

 不論此站台伺服器角色在階層中的位置為何，每個應用程式類別目錄站台系統角色提供的資訊會與該站台系統角色的其他執行個體相同。 因此，當用戶端要求應用程式類別目錄，而您已經將 [預設應用程式類別目錄網站點] 裝置用戶端設定設定為 [自動偵測] 時，可將用戶端導向至可用執行個體。 根據用戶端的目前網路位置，會慣用本機應用程式類別目錄站台系統伺服器。  

 如需此用戶端設定與自動偵測運作方法的詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端設定](../../core/clients/deploy/about-client-settings.md)主題中的[電腦代理程式](../../core/clients/deploy/about-client-settings.md#BKMK_ComputerAgentDeviceSettings)一節。  

##  <a name="a-namebkmkclienta-high-availability-for-clients"></a><a name="bkmk_client"></a> 用戶端的高可用性  
 **用戶端作業是自主性的：**  

 Configuration Manager 用戶端自主性包括下列各項︰  

-   用戶端不會要求持續與任何特定站台系統伺服器連絡。 用戶端會使用已知設定，按照排程執行預先設定的動作。  

-   用戶端可以使用提供用戶端服務之站台系統角色的任何可用執行個體，而且會嘗試連絡已知伺服器，直到找到可用的伺服器為止。  

-   用戶端可以執行清查、軟體部署以及類似的排程動作，不需要直接與站台系統伺服器連絡。  

-   設定為使用後援狀態點的用戶端，可以在無法與管理點通訊時，將詳細資料提交給後援狀態點。  

 **用戶端能夠自行修復：**  

 用戶端可以自動補救多數常見的問題，不需要系統管理者直接操作。  

-   用戶端會定期自我評估狀態，並且會使用補救步驟的本機快取以及需修復的來源檔案，以進行常見問題的補救動作。  

-   當用戶端無法提交狀態資訊至其站台時，站台會產生警示。 接收這些警示的系統管理使用者，可以立即採取動作，以還原用戶端的正常操作。  

 **未來使用的用戶端快取資訊：**  

 當用戶端與管理點通訊時，用戶端可以取得並快取以下資訊：  

-   用戶端設定。  

-   用戶端排程。  

-   針對此動作設定部署時，有關軟體部署與用戶端排定安裝之軟體下載的資訊。  

 當用戶端無法連絡管理點時，用戶端會在本機快取狀態、狀況，以及對站台報告的用戶端資訊，並在與管理點連絡之後傳送此資料。  

 **用戶端可以將狀態提交至後援狀態點：**  

 當您將用戶端設定為使用後援狀態點時，便會提供額外的連絡點讓用戶端提交有關其操作的重要詳細資料。 即使在用戶端無法與管理點通訊時，設定為使用後援狀態點的用戶端也會持續傳送有關其操作的狀態至其站台系統角色。  

 **用戶端資料與用戶端識別身分的中央管理：**  

 站台資料庫 (而非個別用戶端) 會保留有關各個用戶端識別身分的資訊，並且為該資料與特定電腦或使用者建立關聯性。 這表示︰  

-   電腦上的用戶端來源檔案可以解除安裝與重新安裝，完全不會影響用戶端安裝所在電腦的歷程記錄。  

-   用戶端電腦的失敗並不影響資料庫中所儲存的資訊完整性。 此資訊仍可供報告使用。  

##  <a name="a-namebkmknonhaoptionsa-options-for-sites-and-site-system-roles-that-are-not-highly-available"></a><a name="bkmk_nonHAoptions"></a> 不具高度可用性的站台與站台系統角色的選項  
 某些站台系統並不支援站台或階層內的多個執行個體。 此資訊可協助您準備這些要離線的站台系統。  

 **站台伺服器 (站台)：**  

 Configuration Manager 不支援為 Windows Server 叢集或 NLB 叢集上的每個站台安裝站台伺服器。  

 下列資訊可助您準備處理站台伺服器當機或無法運作的情況:  

-   使用內建備份工作以定期建立站台的備份。 在測試環境中，定期從備份還原站台。  

-   在包含管理中心網站的階層中部署多個 Configuration Manager 主要站台以建立複本。 如果站台失敗，請考慮使用 Windows 群組原則或是登入程式碼以重新指派用戶端至運作正常的站台。  

-   如果您的階層有管理中心網站，您可以使用此選項以從您階層中另一個站台復原站台資料庫，進而復原管理中心網站或是子主要站台。  

-   無法還原次要站台，而且必須重新安裝。  

 **Asset Intelligence 同步處理點 (階層)：**  

 此站台角色並非關鍵角色，而且提供 Configuration Manager 中的選用功能。 如果此站台系統離線，請使用下列其中一個選項：  

-   解析站台系統離線的原因。  

-   從目前伺服器解除安裝角色，並且在新伺服器上安裝角色。  

 **Endpoint Protection 點 (階層)：**  

 此站台角色並非關鍵角色，而且提供 Configuration Manager 中的選用功能。 如果此站台系統離線，請使用下列其中一個選項：  

-   解析站台系統離線的原因。  

-   從目前伺服器解除安裝角色，並且在新伺服器上安裝角色。  

 **註冊點 (站台)：**  

 此站台角色並非關鍵角色，而且提供 Configuration Manager 中的選用功能。 如果此站台系統離線，請使用下列其中一個選項：  

-   解析站台系統離線的原因。  

-   從目前伺服器解除安裝角色，並且在新伺服器上安裝角色。  

 **註冊 Proxy 點 (站台)：**  

 此站台角色並非關鍵角色，而且提供 Configuration Manager 中的選用功能。 但是，您可以在一個站台以及階層中的多個站台安裝此站台系統角色的多個執行個體。 如果此站台系統離線，請使用下列其中一個選項：  

-   解析站台系統離線的原因。  

-   從目前伺服器解除安裝角色，並且在新伺服器上安裝角色。  

 站台中有一個以上的註冊 Proxy 伺服器時，伺服器名稱請使用 DNS 別名。 如果您使用此設定，DNS 循環配置資源會在使用者註冊其行動裝置時，提供部分容錯與負載平衡。  

 **後援狀態點 (站台或階層)：**  

 此站台角色並非關鍵角色，而且提供 Configuration Manager 中的選用功能。 如果此站台系統離線，請使用下列其中一個選項：  

-   解析站台系統離線的原因。  

-   從目前伺服器解除安裝角色，並且在新伺服器上安裝角色。 由於用戶端在用戶端安裝期間已接受後援狀態點的指派，因此您必須修改現有用戶端以使用新的站台系統伺服器。  

### <a name="see-also"></a>請參閱  
 [System Center Configuration Manager 的支援設定](../../core/plan-design/configs/supported-configurations.md)



<!--HONumber=Nov16_HO1-->


