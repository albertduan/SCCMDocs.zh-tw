---
title: "使用診斷資料 | Microsoft Docs"
description: "了解 Microsoft 如何使用 System Center Configuration Manager 收集的診斷及使用方式資料。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: aa0ee7544e348025a80d32b4a816de6dbec31d7f


---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>診斷和使用方式資料如何用於 System Center Configuration Manager

*適用於：System Center Configuration Manager (最新分支)*

針對 System Center Configuration Manager 收集的診斷和使用方式資料會以近即時的方式，將產品的運作 (或無法運作) 狀況回饋給 Microsoft，以用來調整後續的更新。 我們也可以查看設定資料，以協助我們設計及測試生產環境中的設定。 例如：  

-   站台伺服器所使用的 Windows Server 版本  

-   安裝的語言套件  

-   SQL 結構描述與產品預設值的差異  

這份資料可協助工程團隊規劃未來測試，以確保獲得最常見設定的最佳體驗。 隨著 Configuration Manager 更新的發行頻率愈來愈快 (以便針對快速發展的 Windows 10 和 Microsoft Intune 等技術提供更佳的支援)，這份資料對於快速調整與採用至關重要。  

診斷和使用方式資料不被運用的情形也同樣重要。 Microsoft 不會將此資料用來︰  

-   授權稽核，例如針對授權合約比對用戶端使用方式  

-   稽核不支援的產品  

-   根據可用資料 (例如功能使用習慣或地理位置 (時區)) 推銷廣告  

##  <a name="a-namebkmkimprovea-examples-of-how-diagnostics-and-usage-data-is-improving-the-product"></a><a name="bkmk_improve"></a> 診斷和使用方式資料如何改進產品的範例  
Microsoft 會利用可用的資料來改進產品。 以下是幾個作法的範例：  

-   **修改較舊的伺服器作業系統的支援：**  

     System Center Configuration Manager 最新分支所提供的初始支援，在 Windows Server 2008 R2 的支援時間表上有所限制。 在檢查已升級至 Configuration Manager 最新分支的客戶使用方式資料後，我們意識到修改並延長此時間表的必要性，這樣才能支援仍使用此伺服器作業系統來裝載站台伺服器及站台系統角色的大量客戶。  

-   **改善必要條件檢查：**  

     根據使用方式資料，我們已經改善安裝更新的必要條件檢查，以移除過時的規則、處理額外情況，以及在某些情況下自動修補某些問題。  



<!--HONumber=Dec16_HO3-->


