#   了解及探索
##  [Configuration Manager 簡介](understand/introduction.md)
### [尋找 Configuration Manager 的說明](understand/find-help.md)
### [協助工具功能](understand/accessibility-features.md)
##  [Configuration Manager 的基礎](understand/fundamentals.md)
### [站台和階層的基本概念](understand/fundamentals-of-sites-and-hierarchies.md)
#### [關於站台及階層基礎結構的升級、更新及安裝](understand/upgrade-update-install.md)
### [管理裝置的基本概念](understand/fundamentals-of-managing-devices.md)
### [用戶端管理的基本概念](understand/fundamentals-of-client-management-tasks.md)
### [安全性的基本概念](understand/fundamentals-of-security.md)
### [以角色為基礎的系統管理基本概念](understand/fundamentals-of-role-based-administration.md)
##  [長期維護分支簡介](understand/introduction-to-the-ltsb.md)
### [支援的長期維護分支設定](understand/supported-configurations-for-ltsb.md)
### [安裝長期維護分支](understand/install-the-ltsb.md)
### [管理長期維護分支](understand/manage-the-ltsb.md)
### [將長期維護分支升級至最新分支](understand/convert-to-current-branch.md)
##  [應該使用的 Configuration Manager 分支](understand/which-branch-should-i-use.md)
##  [延伸互通性用戶端](understand/interoperability-client.md)
##  [System Center Configuration Manager 的授權](understand/learn-more-editions.md)
##  [使用雲端服務](understand/use-cloud-services.md)
### [Azure 上的 Configuration Manager](understand/configuration-manager-on-azure.md)
##  [產品與授權的常見問題集](understand/product-and-licensing-faq.md)
##  [診斷與使用方式資料的常見問題集](understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)

#    [規劃和設計](plan-design/get-ready.md)
##   產品變更
###  [特性和功能](plan-design/changes/features-and-capabilities.md)
###  [Configuration Manager 2012 的變更內容](plan-design/changes/what-has-changed-from-configuration-manager-2012.md)
###  [累加版本的新功能](plan-design/changes/whats-new-incremental-versions.md)
###  [1706 版的新功能](plan-design/changes/whats-new-in-version-1706.md)
###  [1702 版的新功能](plan-design/changes/whats-new-in-version-1702.md)
###  [1610 版的新功能](plan-design/changes/whats-new-in-version-1610.md)
<!--
###  [What's new in version 1606](plan-design/changes/whats-new-in-version-1606.md)
###  [What's new in version 1602](plan-design/changes/whats-new-in-version-1602.md)
-->
###  [已移除和已淘汰的功能](plan-design/changes/removed-and-deprecated-features.md)

##   [支援的設定](plan-design/configs/supported-configurations.md)
###  [大小和縮放比例](plan-design/configs/size-and-scale-numbers.md)
###  [站台和站台系統必要條件](plan-design/configs/site-and-site-system-prerequisites.md)
###  [支援的站台系統伺服器作業系統](plan-design/configs/supported-operating-systems-for-site-system-servers.md)
###  [用戶端和裝置的支援作業系統](plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
###  [Windows 10 用戶端的支援](plan-design/configs/support-for-windows-10.md)
###  [支援的主控台作業系統](plan-design/configs/supported-operating-systems-consoles.md)
###  [建議的硬體](plan-design/configs/recommended-hardware.md)
###  [SQL Server 版本支援](plan-design/configs/support-for-sql-server-versions.md)
###  [Active Directory 網域支援](plan-design/configs/support-for-active-directory-domains.md)
###  [Windows 功能和網路支援](plan-design/configs/support-for-windows-features-and-networks.md)
###  [虛擬化環境支援](plan-design/configs/support-for-virtualization-environments.md)

##   [選擇裝置管理解決方案](plan-design/choose-a-device-management-solution.md)
##   [設計站台階層](plan-design/hierarchy/design-a-hierarchy-of-sites.md)
###  [規劃 SMS 提供者](plan-design/hierarchy/plan-for-the-sms-provider.md)
###  [規劃站台資料庫](plan-design/hierarchy/plan-for-the-site-database.md)
###  [規劃站台系統伺服器](plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)
###  [內容管理的基本概念](plan-design/hierarchy/fundamental-concepts-for-content-management.md)
#### [使用雲端發佈點](plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
#### [使用提取發佈點](plan-design/hierarchy/use-a-pull-distribution-point.md)
#### [內容庫](plan-design/hierarchy/the-content-library.md)
#### [內容庫清理工具](plan-design/hierarchy/content-library-cleanup-tool.md)
#### [管理帳戶以存取內容](plan-design/hierarchy/manage-accounts-to-access-content.md)
#### [Configuration Manager 用戶端的對等快取](plan-design/hierarchy/client-peer-cache.md)
#### [內容來源位置案例](plan-design/hierarchy/content-source-location-scenarios.md)
#### [套件傳輸管理員](plan-design/hierarchy/package-transfer-manager.md)
#### [管理內容管理的網路頻寬](plan-design/hierarchy/manage-network-bandwidth.md)
#### [內容管理的安全性和隱私權](plan-design/hierarchy/security-and-privacy-for-content-management.md)
###  [用戶端如何尋找資源和服務](plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)
###  [站台系統管理的安全性和隱私權](plan-design/hierarchy/security-and-privacy-for-site-administration.md)

##   [規劃網路基礎結構](plan-design/network/configure-firewalls-ports-domains.md)
###  [準備 Active Directory 架構](plan-design/network/extend-the-active-directory-schema.md)
#### [架構延伸模組](plan-design/network/schema-extensions.md)
###  [準備 Windows Server 以支援站台系統](plan-design/network/prepare-windows-servers.md)
###  [站台系統伺服器的網站](plan-design/network/websites-for-site-system-servers.md)
###  [PKI 憑證需求](plan-design/network/pki-certificate-requirements.md)

##   [診斷和使用情況資料](plan-design/diagnostics/diagnostics-and-usage-data.md)
###  [診斷和使用情況資料的運用](plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)
###  [1706 的診斷資料](plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1706.md)
###  [1702 的診斷資料](plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702.md)
###  [1610 的診斷資料](plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610.md)

<!--
###  [Diagnostic data for 1606](plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606.md)
###  [Diagnostic data for 1602](plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602.md)
###  [Diagnostic data for 1511](plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511.md)

-->
###  [診斷和使用方式資料的收集方式](plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)
###  [如何檢視診斷和使用情況資料](plan-design/diagnostics/view-diagnostics-and-usage-data.md)
###  [客戶經驗改進計畫 (CEIP)](plan-design/diagnostics/customer-experience-improvement-program-ceip.md)

##   [Configuration Manager 的安全性和隱私權](plan-design/security/security-and-privacy.md)
###  [規劃安全性](plan-design/security/plan-for-security.md)
###  [安全性最佳作法和隱私權資訊](plan-design/security/security-best-practices-and-privacy-information.md)
###  [隱私權聲明 - Configuration Manager Cmdlet 庫](plan-design/security/privacy-statement-cmdlet-library.md)
###  [其他隱私權資訊](plan-design/security/additional-privacy.md)
###  [設定安全性](plan-design/security/configure-security.md)

#    開始使用
##   [在實驗室中評估 Configuration Manager](get-started/evaluate-with-lab-environment.md)
###  [設定實驗室](get-started/set-up-your-lab.md)

##   [Technical Preview](get-started/technical-preview.md)
###  [1710 的功能](get-started/capabilities-in-technical-preview-1710.md)
###  [1709 的功能](get-started/capabilities-in-technical-preview-1709.md)
###  [1708 的功能](get-started/capabilities-in-technical-preview-1708.md)
###  [1707 的功能](get-started/capabilities-in-technical-preview-1707.md)
###  [1706 的功能](get-started/capabilities-in-technical-preview-1706.md)
###  [1705 的功能](get-started/capabilities-in-technical-preview-1705.md)
###  [1704 的功能](get-started/capabilities-in-technical-preview-1704.md)
###  [1703 的功能](get-started/capabilities-in-technical-preview-1703.md)
###  [1702 的功能](get-started/capabilities-in-technical-preview-1702.md)
###  [1701 的功能](get-started/capabilities-in-technical-preview-1701.md)
###  [1612 的功能](get-started/capabilities-in-technical-preview-1612.md)
###  [1611 的功能](get-started/capabilities-in-technical-preview-1611.md)
###  [1610 的功能](get-started/capabilities-in-technical-preview-1610.md)
###  [1609 的功能](get-started/capabilities-in-technical-preview-1609.md)

<!-- No longer in support, and all features are in the Current Branch
###  [Capabilities in 1608](get-started/capabilities-in-technical-preview-1608.md)
###  [Capabilities in 1607](get-started/capabilities-in-technical-preview-1607.md)
###  [Capabilities in 1606](get-started/capabilities-in-technical-preview-1606.md)
###  [Capabilities in 1605](get-started/capabilities-in-technical-preview-1605.md)
###  [Capabilities in 1604](get-started/capabilities-in-technical-preview-1604.md)
###  [Capabilities in 1603](get-started/capabilities-in-technical-preview-1603.md)
###  [Capabilities in 1602](get-started/capabilities-in-technical-preview-1602.md)
###  [Capabilities in 1601](get-started/capabilities-in-technical-preview-1601.md)
###  [Capabilities in 1512](get-started/capabilities-in-technical-preview-1512.md)
###  [Capabilities in 1511](get-started/capabilities-in-technical-preview-1511.md)
-->

##   [在階層間移轉資料](migration/migrate-data-between-hierarchies.md)
###  [規劃移轉](migration/planning-for-migration.md)
#### [移轉必要條件](migration/prerequisites-for-migration.md)
#### [移轉檢查清單](migration/administrator-checklists-for-migration-planning.md)
#### [決定是否移轉資料](migration/determine-whether-to-migrate-data.md)
#### [規劃來源階層](migration/planning-a-source-hierarchy-strategy.md)
#### [規劃移轉作業](migration/planning-a-migration-job-strategy.md)
#### [規劃用戶端移轉](migration/planning-a-client-migration-strategy.md)
#### [規劃內容部署](migration/planning-a-content-deployment-migration-strategy.md)
#### [規劃移轉物件](migration/planning-for-the-migration-of-objects.md)
#### [規劃監視移轉](migration/planning-to-monitor-migration-activity.md)
#### [規劃完成移轉](migration/planning-to-complete-migration.md)
###  [設定來源階層和來源站台](migration/configuring-source-hierarchies-and-source-sites-for-migration.md)
###  [移轉的作業](migration/operations-for-migration.md)
###  [移轉的安全性和隱私權](migration/security-and-privacy-for-migration.md)

#    [部署伺服器和角色](servers/deploy/start-using.md)

##   安裝基礎結構
###  [取得安裝媒體](servers/deploy/install/get-install-media.md)
###  執行安裝程式之前
#### [設定參考](servers/deploy/install/setup-reference.md)
#### [安裝程式下載程式](servers/deploy/install/setup-downloader.md)
#### [先決條件檢查程式](servers/deploy/install/prerequisite-checker.md)
#### [先決條件檢查](servers/deploy/install/list-of-prerequisite-checks.md)
###  [安裝站台](servers/deploy/install/installing-sites.md)
#### [準備安裝站台](servers/deploy/install/prepare-to-install-sites.md)
#### [安裝站台的先決條件](servers/deploy/install/prerequisites-for-installing-sites.md)
#### [使用安裝精靈](servers/deploy/install/use-the-setup-wizard-to-install-sites.md)
#### [使用命令列](servers/deploy/install/use-a-command-line-to-install-sites.md)
##### [命令列選項](servers/deploy/install/command-line-options-for-setup.md)
#### [安裝主控台](servers/deploy/install/install-consoles.md)
#### [升級評估安裝](servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md)
#### [升級至 System Center Configuration Manager](servers/deploy/install/upgrade-to-configuration-manager.md)
#### [安裝簡化案例](servers/deploy/install/scenarios-to-streamline-your-installation.md)
#### [解除安裝站台和階層](servers/deploy/install/uninstall-sites-and-hierarchies.md)

##   [設定站台和階層](servers/deploy/configure/configure-sites-and-hierarchies.md)
###  [新增站台系統角色](servers/deploy/configure/add-site-system-roles.md)
#### [安裝站台系統角色](servers/deploy/configure/install-site-system-roles.md)
#### [安裝雲端發佈點](servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)
#### [關於服務連接點](servers/deploy/configure/about-the-service-connection-point.md)
#### [站台系統角色的設定選項](servers/deploy/configure/configuration-options-for-site-system-roles.md)
#### [管理點的資料庫複本](servers/deploy/configure/database-replicas-for-management-points.md)
###  [站台元件](servers/deploy/configure/site-components.md)
###  [發行站台資料](servers/deploy/configure/publish-site-data.md)
###  [管理內容和內容基礎結構](servers/deploy/configure/manage-content-and-content-infrastructure.md)
#### [安裝和設定發佈點](servers/deploy/configure/install-and-configure-distribution-points.md)
#### [部署和管理內容](servers/deploy/configure/deploy-and-manage-content.md)
#### [監視內容](servers/deploy/configure/monitor-content-you-have-distributed.md)
###  [執行探索](servers/deploy/configure/run-discovery.md)
#### [關於探索方法](servers/deploy/configure/about-discovery-methods.md)
#### [選取探索方法](servers/deploy/configure/select-discovery-methods-to-use.md)
#### [設定探索方法](servers/deploy/configure/configure-discovery-methods.md)
###  [站台界限和界限群組](servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)
#### [界限](servers/deploy/configure/boundaries.md)
#### [界限群組](servers/deploy/configure/boundary-groups.md)
###  [準備使用 SQL Server Alwayson](servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)
###  [設定 SQL Server Alwayson](servers/deploy/configure/configure-aoag.md)
###  [使用 SQL Server 叢集](servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)
###  [自訂資料庫檔案的位置](servers/deploy/configure/custom-locations-for-site-database-files.md)
###  [設定以角色為基礎的系統管理](servers/deploy/configure/configure-role-based-administration.md)
###  [設定 Azure 服務](servers/deploy/configure/azure-services-wizard.md)
##   技術參考
###  [帳戶](plan-design/hierarchy/accounts.md)
###  [端點之間的通訊](plan-design/hierarchy/communications-between-endpoints.md)
###  [階層維護工具](servers/manage/hierarchy-maintenance-tool-preinst.exe.md)
###  [國際支援](plan-design/hierarchy/international-support.md)
###  [不同版本之間的互通性](plan-design/hierarchy/interoperability-between-different-versions.md)
###  [語言套件](servers/deploy/install/language-packs.md)
###  [記錄檔](plan-design/hierarchy/log-files.md)
###  [連接埠](plan-design/hierarchy/ports.md)
###  [Proxy 伺服器支援](plan-design/network/proxy-server-support.md)
###  [版本資訊](servers/deploy/install/release-notes.md)
###  [Unicode 和 ASCII 支援](plan-design/hierarchy/unicode-and-ascii-support.md)
<!-- Deprecated from Content - still published but out of TOC:
#### [Boundary groups for versions prior to 1610](servers/deploy/configure/boundary-groups-for-1511-1602-and-1606.md)
-->

#    管理基礎結構
##   [維護工作](servers/manage/maintenance-tasks.md)
###  [維護工作的參考](servers/manage/reference-for-maintenance-tasks.md)
##   [修改基礎結構](servers/manage/modify-your-infrastructure.md)
###  [CD.Latest 資料夾](servers/manage/the-cd.latest-folder.md)
##   [升級內部部署基礎結構](servers/manage/upgrade-on-premises-infrastructure.md)
##   [Configuration Manager 的更新](servers/manage/updates.md)
###  [安裝主控台內更新](servers/manage/install-in-console-updates.md)
#### [更新重設工具](servers/manage/update-reset-tool.md)
#### [測試資料庫升級](servers/manage/test-database-upgrade.md)
#### [流程圖 - 下載更新](servers/manage/download-updates-flowchart.md)
#### [流程圖 - 更新複寫](servers/manage/update-replication-flowchart.md)
###  [發行前版本功能](servers/manage/pre-release-features.md)
###  [站台伺服器的服務保留時間](servers/manage/service-windows.md)
###  [使用服務連接工具](servers/manage/use-the-service-connection-tool.md)
###  [使用更新註冊工具](servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)
###  [使用 Hotfix 安裝程式](servers/manage/use-the-hotfix-installer-to-install-updates.md)
###  [安裝更新 1706 的檢查清單](servers/manage/checklist-for-installing-update-1706.md)
###  [安裝更新 1702 的檢查清單](servers/manage/checklist-for-installing-update-1702.md)
###  [安裝更新 1610 的檢查清單](servers/manage/checklist-for-installing-update-1610.md)
<!-- Deprecated from Content - still published but out of TOC:
###  [Checklist for installing update 1606](servers/manage/checklist-for-installing-update-1606.md)
###  [Checklist for installing update 1602](servers/manage/checklist-for-installing-update-1602.md)
-->
###  [最新分支版本支援](servers/manage/current-branch-versions-supported.md)  


##   監視基礎結構
###  [使用警示和狀態系統](servers/manage/use-alerts-and-the-status-system.md)
###  [健康情況證明](servers/manage/health-attestation.md)
###  [監視階層和複寫基礎結構](servers/manage/monitor-hierarchy-and-replication-infrastructure.md)
#### [站台間的資料傳輸](servers/manage/data-transfers-between-sites.md)
###  [查詢](servers/manage/queries-technical-reference.md)
#### [查詢簡介](servers/manage/introduction-to-queries.md)
#### [查詢的作業和維護](servers/manage/operations-and-maintenance-for-queries.md)
##### [如何管理查詢](servers/manage/manage-queries.md)
##### [如何建立查詢](servers/manage/create-queries.md)
#### [查詢的安全性和隱私權](servers/manage/security-and-privacy-for-queries.md)
###  [報告](servers/manage/reporting.md)
#### [報告簡介](servers/manage/introduction-to-reporting.md)
#### [規劃報告](servers/manage/planning-for-reporting.md)
##### [報告的先決條件](servers/manage/prerequisites-for-reporting.md)
##### [報告的最佳作法](servers/manage/best-practices-for-reporting.md)
##### [報告清單](servers/manage/list-of-reports.md)
#### [設定報告](servers/manage/configuring-reporting.md)
#### [報告的作業和維護](servers/manage/operations-and-maintenance-for-reporting.md)
#### [建立自訂報告模型](servers/manage/creating-custom-report-models-in-sql-server-reporting-services.md)
#### [報告的安全性和隱私權](servers/manage/security-and-privacy-for-reporting.md)
###  [資料倉儲](servers/manage/data-warehouse.md)

#    部署用戶端
##   規劃用戶端部署
###  [用戶端安裝方法](clients/deploy/plan/client-installation-methods.md)
###  [將用戶端部署至 Windows 電腦的先決條件](clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)
#### [用戶端適用的 Windows 防火牆和連接埠設定](clients/deploy/windows-firewall-and-port-settings-for-clients.md)
###  [判斷用戶端的站台系統角色](clients/deploy/plan/determine-the-site-system-roles-for-clients.md)
###  [用戶端的安全性和隱私權](clients/deploy/plan/security-and-privacy-for-clients.md)
###  [用戶端部署的最佳作法](clients/deploy/plan/best-practices-for-client-deployment.md)
###  [判斷是否封鎖用戶端](clients/deploy/plan/determine-whether-to-block-clients.md)
###  [規劃將用戶端部署至 Linux 和 UNIX 電腦](clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)
###  [規劃將用戶端部署至 Mac 電腦](clients/deploy/plan/planning-for-client-deployment-to-mac-computers.md)
###  [規劃將用戶端部署至 Windows Embedded 裝置](clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)
#### [範例案例](clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md)
###  [規劃如何喚醒用戶端](clients/deploy/plan/plan-wake-up-clients.md)
###  [在虛擬桌面基礎結構 (VDI) 中管理用戶端的考量](clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)

##   用戶端部署工作
###  [如何設定用戶端通訊連接埠](clients/deploy/configure-client-communication-ports.md)
###  [如何設定用戶端電腦使用 DNS 發行尋找管理點](clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md)
###  [如何設定用戶端設定](clients/deploy/configure-client-settings.md)
#### [關於用戶端設定](clients/deploy/about-client-settings.md)
###  [如何設定網路喚醒](clients/deploy/configure-wake-on-lan.md)
###  [如何將用戶端部署至 Windows 電腦](clients/deploy/deploy-clients-to-windows-computers.md)
#### [用戶端安裝內容](clients/deploy/about-client-installation-properties.md)
#### [發佈至 AD 的用戶端安裝內容](clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)
###  [如何將用戶端部署至 UNIX 和 Linux 伺服器](clients/deploy/deploy-clients-to-unix-and-linux-servers.md)
#### [Linux 和 UNIX 的用戶端命令](clients/deploy/linux-and-unix-clients-technical-reference.md)
###  [準備將用戶端部署到 Mac](clients/deploy/prepare-to-deploy-mac-clients.md)
###  [如何將用戶端部署至 Mac](clients/deploy/deploy-clients-to-macs.md)
###  [使用 Azure AD 從網際網路安裝用戶端](clients/deploy/deploy-clients-cmg-azure.md)
###  [如何將用戶端指派至站台](clients/deploy/assign-clients-to-a-site.md)
###  [如何設定用戶端狀態](clients/deploy/configure-client-status.md)
###  [如何監視用戶端部署狀態](clients/deploy/monitor-client-deployment-status.md)

#    [管理用戶端](clients/manage/monitor-and-manage-clients.md)

##   [監視和管理用戶端](clients/manage/monitor-clients.md)
###  [如何監視用戶端](clients/manage/monitor-clients.md)
###  [使用 Windows Analytics](clients/manage/monitor-windows-analytics.md)
###  [如何監視 Linux 和 UNIX 用戶端](clients/manage/monitor-clients-for-linux-and-unix-servers.md)
###  [如何管理用戶端](clients/manage/manage-clients.md)
###  [如何管理 Linux 和 UNIX 用戶端](clients/manage/manage-clients-for-linux-and-unix-servers.md)
###  [將資料同步處理至 OMS](clients/manage/sync-data-microsoft-operations-management-suite.md)
###  [維護 Mac 用戶端](clients/manage/maintain-mac-clients.md)

##   [管理網際網路上的用戶端](clients/manage/manage-clients-internet.md)
###  [規劃雲端管理閘道](clients/manage/plan-cloud-management-gateway.md)
###  [設定雲端管理閘道](clients/manage/setup-cloud-management-gateway.md)
###  [監視雲端管理閘道上的用戶端](clients/manage/monitor-clients-cloud-management-gateway.md)
###  [規劃以網際網路為基礎的用戶端管理](clients/manage/plan-internet-based-client-management.md)

##   集合
###  [集合簡介](clients/manage/collections/introduction-to-collections.md)
### [集合的先決條件](clients/manage/collections/prerequisites-for-collections.md)
### [集合的最佳作法](clients/manage/collections/best-practices-for-collections.md)
### [如何建立集合](clients/manage/collections/create-collections.md)
### [如何管理集合](clients/manage/collections/manage-collections.md)
### [如何使用維護時段](clients/manage/collections/use-maintenance-windows.md)
### [如何自動將裝置分類為集合](clients/manage/collections/automatically-categorize-devices-into-collections.md)
###  [集合的安全性和隱私權](clients/manage/collections/security-and-privacy-for-collections.md)

##   硬體清查
###  [硬體清查簡介](clients/manage/inventory/introduction-to-hardware-inventory.md)
###  [如何擴充硬體清查](clients/manage/inventory/extend-hardware-inventory.md)
###  [如何設定硬體清查](clients/manage/inventory/configure-hardware-inventory.md)
###  [如何使用資源總管檢視硬體清查](clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)
###  [Linux 和 UNIX 的硬體清查](clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)
###  [硬體清查的安全性和隱私權](clients/manage/inventory/security-and-privacy-for-hardware-inventory.md)

##   軟體清查
###  [軟體清查簡介](clients/manage/inventory/introduction-to-software-inventory.md)
###  [如何設定軟體清查](clients/manage/inventory/configure-software-inventory.md)
###  [如何使用資源總管檢視軟體清查](clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)
###  [軟體清查的安全性和隱私權](clients/manage/inventory/security-and-privacy-for-software-inventory.md)

##   Asset Intelligence
###  [Asset Intelligence 簡介](clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)
###  [Asset Intelligence 的先決條件](clients/manage/asset-intelligence/prerequisites-for-asset-intelligence.md)
###  [設定 Asset Intelligence](clients/manage/asset-intelligence/configuring-asset-intelligence.md)
###   [使用 Asset Intelligence](clients/manage/asset-intelligence/operations-for-asset-intelligence.md)
###  [Asset Intelligence 的安全性和隱私權](clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md)
###  [Asset Intelligence 驗證狀態轉換範例](clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence.md)
###  [範例 Asset Intelligence 一般授權匯入檔案](clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md)

##   遠端控制
###  [遠端控制簡介](clients/manage/remote-control/introduction-to-remote-control.md)
### [遠端控制的先決條件](clients/manage/remote-control/prerequisites-for-remote-control.md)
###  [設定遠端控制](clients/manage/remote-control/configuring-remote-control.md)
### [如何從遠端管理 Windows 用戶端電腦](clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)
### [如何稽核遠端控制使用情況](clients/manage/remote-control/audit-remote-control-usage.md)
###  [遠端控制的安全性和隱私權](clients/manage/remote-control/security-and-privacy-for-remote-control.md)

##   電源管理
###  [電源管理簡介](clients/manage/power/introduction-to-power-management.md)
### [電源管理的先決條件](clients/manage/power/prerequisites-for-power-management.md)
### [電源管理的最佳作法](clients/manage/power/best-practices-for-power-management.md)
###  [電源管理的系統管理員檢查清單](clients/manage/power/administrator-checklist-for-power-management.md)
###  [設定電源管理](clients/manage/power/configuring-power-management.md)
### [如何建立和套用電源計劃](clients/manage/power/create-and-apply-power-plans.md)
### [如何監視和規劃電源管理](clients/manage/power/monitor-and-plan-for-power-management.md)
###  [電源管理的安全性和隱私權](clients/manage/power/security-and-privacy-for-power-management.md)

##   [升級用戶端](clients/manage/upgrade/upgrade-clients.md)
###  [測試進入生產階段前集合的用戶端升級](clients/manage/upgrade/test-client-upgrades.md)
###  [讓 Windows 用戶端不要升級](clients/manage/upgrade/exclude-clients-windows.md)
###  [升級 Windows 用戶端](clients/manage/upgrade/upgrade-clients-for-windows-computers.md)
###  [升級 Linux 和 UNIX 用戶端](clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)
###  [升級 Mac 用戶端](clients/manage/upgrade/upgrade-clients-on-mac-computers.md)
###  [升級整備](clients/manage/upgrade/upgrade-analytics.md)
