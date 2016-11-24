---
title: "使用 IMEI 或 iOS 序號預先宣告裝置"
description: "使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置。"
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6cd640085e90b2945326e3fa942ae9bd7b8f7e24
ms.openlocfilehash: 2550fef062b5ef508e4c0492a5a9c63ffcb9084a

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>使用 IMEI 或 iOS 序號預先宣告裝置

*適用於：System Center Configuration Manager (最新分支)*

您可以透過匯入國際站移動設備識別碼 (IMEI) 號碼或 iOS 序號，識別公司擁有的裝置。 您可以上傳一個包含裝置 IMEI 編號的逗號分隔值 (.csv) 檔案，也可以手動輸入裝置資訊。  匯入的資訊將會設定裝置清單中註冊為**公司**之裝置的**擁有權**。 每一位存取服務的使用者還是需要 Intune 授權。  

## <a name="predeclare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置

1.  在 Configuration Manager 主控台中，瀏覽 [資產與相容性] > [概觀] > [公司擁有的所有裝置] > [預先宣告的裝置]，然後按一下 [Add Predeclared devices] (新增預先宣告的裝置)。 隨即開啟 [預先宣告的裝置精靈]。
2.  指定您要如何新增裝置資訊︰
     -  上傳包含 IMEI 編號和詳細資料的 .csv 檔案
     -  手動新增 IMEI 編號和詳細資料。 若要手動輸入資訊，請輸入裝置的 IMEI 編號或 iOS 序號和詳細資料。

      針對上傳的檔案，瀏覽至 .csv 檔案，這個檔案包含預先宣告公司擁有之裝置的資訊。 檔案必須具有下列格式，不包括僅提供作為指引的第一列。 每個資料列都必須包含 IMEI 編號或 iOS 序號。 只能預先宣告 iOS 裝置的序號；請針對其他裝置平台使用 IMEI 編號。 此表格包含範例資料︰
      | IMEI #  | iOS 序列 #  | OS | 詳細資料 |
      | :------------ |:---------------|:-----|:-----|
      | 123456789012345    |   | WINDOWS | 公司擁有的 Windows 裝置|
      |       | A1B2C3D4E5C6 |   iOS |  公司擁有的 iOS 裝置|
      | 223456789012345 | E6D5C4B3A210 |   iOS |    另一部 iOS 裝置|
      | 323456789012345 |        |   iOS |  第三部 iOS 裝置|
      | 123456789012346 |         |   Android |     公司擁有的 Android 裝置|

    .csv 檔案中不包含標頭資料列。 上述範例僅包含標頭來進行釐清。

    **資料行接受下列值：**    
      - 資料行 1：沒有空格的 IMEI 編號
      - 資料行 2：iOS 序號
      - 資料行 3︰裝置的作業系統︰
         - IOS – 所有 iOS 裝置
         - WINDOWS - 包含 Windows 手機、Window 10 行動裝置和 Windows 電腦
         - ANDROID – 所有 Android 裝置
      - 資料行 4：詳細資料 (選用) – Configuration Manager 主控台中所顯示的其他裝置資訊。 1024 個字元限制。

    按一下 [下一步] 。

3. 檢閱檔案匯入的結果。 如果已詳盡地匯入裝置號碼，則 Configuration Manager 會顯示那些裝置和取代 [詳細資料]。 選取您要覆寫其詳細資料的裝置。 只有重新匯入裝置識別碼或序號，才能修改裝置詳細資料。 按一下 [下一步] 繼續，或按一下 [上一步] 保留已更新的詳細資料，然後完成精靈。

4. 如果您的匯入包含 iOS 序號，則必須將這些裝置指派至註冊設定檔。 從可用的設定檔清單中，選取 [要指派的註冊設定檔]，然後按一下 [下一步]。

5. 按一下 [下一步] 檢視摘要，然後完成精靈。



<!--HONumber=Nov16_HO1-->


