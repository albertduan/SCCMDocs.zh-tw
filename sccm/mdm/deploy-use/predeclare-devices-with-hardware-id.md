---
title: "使用 IMEI 或 iOS 序號預先宣告裝置 | Microsoft Docs"
description: "使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置。"
ms.custom: na
ms.date: 03/24/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 7573590763c68a4c97d388be1e64054c318da9cc
ms.openlocfilehash: 4fe6741481c79ed4e4496846152902d6d8ca1f96
ms.lasthandoff: 03/24/2017

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>使用 IMEI 或 iOS 序號預先宣告裝置

*適用於：System Center Configuration Manager (最新分支)*

您可以透過匯入國際站移動設備識別碼 (IMEI) 號碼或 iOS 序號，識別公司擁有的裝置。 您可以上傳一個包含裝置 IMEI 編號的逗號分隔值 (.csv) 檔案，也可以手動輸入裝置資訊。  匯入的資訊將會設定裝置清單中註冊為**公司**之裝置的**擁有權**。 每一位存取服務的使用者還是需要 Intune 授權。  

當您上傳公司 iOS 裝置的序號時，它們必須與公司註冊設定檔搭配。 接著，必須使用 Apple 的裝置註冊計劃 (DEP) 或 Apple Configurator 來註冊裝置，以使它們顯示為公司所擁有。 

## <a name="how-to-predeclare-corporate-owned-devices"></a>如何預先宣告公司擁有的裝置

1.    在 Configuration Manager 主控台中，移至 [資產與合規性] > [概觀] > [公司擁有的所有裝置] > 「Predeclared devices」 (預先宣告的裝置)。

2.  按一下 「Create Predeclared Devices」 (建立預先宣告的裝置)。 隨即開啟 「Create Predeclared Devices Wizard」 (建立預先宣告的裝置精靈)。

3.    選擇您要如何新增裝置資訊：

     -    **上傳包含 IMEI 或序號及詳細資料的 CSV 檔案**

        針對這個選項，按一下 [瀏覽] 指定 .csv 檔案，這個檔案包含預先宣告公司擁有之裝置的資訊。 必須正確格式化 .csv 檔案。 如需詳細資訊，請參閱[上傳 .csv 檔案的格式](#format-for-uploading-csv-files)。

     -    **手動新增 IMEI 或序號及詳細資料**

        若要手動輸入資訊，請輸入裝置的 IMEI 編號或 iOS 序號和詳細資料。 請更正任何錯誤或警告後再繼續。

    按一下 [下一步] 。

4. 如果您已上傳 .csv 檔案，請檢閱檔案匯入的結果。 如果先前已匯入裝置號碼，則 Configuration Manager 會顯示那些裝置和取代 [詳細資料]。 選取您要覆寫其詳細資料的裝置。 只有重新匯入裝置識別碼或序號，才能修改裝置詳細資料。

  如果您選擇手動輸入號碼，請完成您想要預先宣告之裝置的表單。

  按 [下一步]  以繼續。

4. 如果您的清單包含 iOS 序號，請從可用設定檔清單中選取 「Enrollment Profile to Assign」 (要指派的註冊設定檔)，然後按一下 [下一步]。

5. 按一下 [下一步] 檢閱詳細資料，然後再按一下 [下一步] 上傳資料。

6. 按一下 [關閉] 完成。

## <a name="format-for-uploading-csv-files"></a>上傳 .csv 檔案的格式

用來依 IMEI 或序號識別裝置的 .csv 檔案必須具有下列格式，不包括僅提供作為指引的頂端資料列。 每個資料列都必須包含 IMEI 編號或 iOS 序號。 只能預先宣告 iOS 裝置的序號；請針對其他裝置平台使用 IMEI 編號。 此表格包含範例資料︰

| IMEI #  | iOS 序列 #  | OS | 詳細資料 |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | 公司擁有的 Windows 裝置|
|   | A1B2C3D4E5C6 | IOS |     公司擁有的 iOS 裝置|
| 223456789012345 | E6D5C4B3A210 |   IOS |     另一部 iOS 裝置|
| 323456789012345 |        |   IOS |     第三部 iOS 裝置|
| 123456789012346 |         |   ANDROID |     公司擁有的 Android 裝置|

.csv 檔案中不包含標頭資料列。 下列範例顯示 CSV 格式的相同範例資料︰

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

.csv 檔案中的資料行接受下列值：

| 第 1 欄 | 第 2 欄 | 第 3 欄 | 第 4 欄 |
|---|---|---|---|
|沒有空格的 IMEI 編號 | iOS 序號 | IOS、WINDOWS 或 ANDROID | 選擇性裝置詳細資料 (1024 個字元限制) |

