---
title: "文章標題 | Microsoft Docs"
description: 
keywords: 
author: GITHUB USERNAME
manager: ALIAS
ms.date: 10/06/2016
ms.topic: article
ms.prod: 
ms.service: 
ms.technology: 
ms.assetid: GET ONE FROM guidgenerator.com
ms.openlocfilehash: a218011ded1ff3acc1dbd24471119b701f2cce23
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="metadata-and-markdown-template"></a>中繼資料與 Markdown 範本

此 docs.ms 範本包含 Markdown 語法範例，以及有關如何設定中繼資料的指導方針。 您可以在每個 EM Pilot 存放庫的根目錄找到它 (例如 ~/Azure-RMSDocs-pr /template.md)，而且應該以 Markdown 檔案解譯它，您可以參閱[已發行的版本](https://stage.docs.microsoft.com/en-us/rights-management/template)以查看 Markdown 範例的呈現方式。

建立 Markdown 檔案時，您應該將範本複製為新檔案，如下面所指定填寫中繼資料，將上面的 H1 標題設定為文章的標題，然後刪除內容。


## <a name="metadata"></a>中繼資料

完整的中繼資料區塊如上，它區分為必要欄位與選擇性欄位；請參閱 [OPS 中繼資料速查表](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data)以取得詳細資訊。 一些重點：

- 冒號 (:) 與中繼資料元素值之間**必須**有空格。
- 若某個選擇性的中繼資料元素沒有值，請使用 # 將該元素變更為註解 (不要將它留白或使用 "na")；若您要將值讀入到已變更為註解的元素中，請務必移除 #。
- 值 (例如 title) 中的冒號會使得中繼資料剖析程式停止執行。 請將它取代為 &#58; 的 HTML 編碼 (例如 "title: Azure Rights Management&#58; 基本概念 | Azure RMS")。
- **title**：此標題將會出現在搜尋引擎結果中。 標題結尾必須是管道符號 (|)，後面接著服務的名稱 (例如，請參閱上述內容)。 標題不一定要與 H1 標題中的標題相同 (而且可能不應該相同)。 長度應為大約 65 個字元 (含 | 服務名稱)
- **author**、**manager**、**reviewer**：author 欄位應該包含作者的 **Github 使用者名稱**，而非其別名。  "manager" 與 "reviewer" 欄位則應該包含別名。 ms.reviewer 可指定與文章或服務關聯之 PM 的名稱。
- **ms.assetid**：這是來自 CAPS 之文章的 GUID。 建立新的 Markdown 檔案時，請從 [https://www.guidgenerator.com](https://www.guidgenerator.com) 取得 GUID。
- **ms.prod**、**ms.service****ms.technology****ms.devlang****ms.topic****ms.tgt_pltfrm**：您可以在[這裡](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default)找到這些元素的可能值。

## <a name="basic-markdown-and-gfm"></a>基本 Markdown 與 GFM

支援所有基本與 Github 版 Markdown。 如需詳細資訊，請參閱：

- [基本 Markdown 語法](https://daringfireball.net/projects/markdown/syntax) \(英文\)
- [Github 版 Markdown (GFM) 文件](https://guides.github.com/features/mastering-markdown) \(英文\)

## <a name="headings"></a>標題

第一層與第二層標題的範例如上。

您的主題中**只能**有一個第一層標題，它將會顯示為頁面標題。  

第二層標題將會產生頁面上的目錄，它會出現在頁面標題下的 [此文章內容] 小節中。

### <a name="third-level-heading"></a>第三層標題
#### <a name="fourth-level-heading"></a>第四層標題
##### <a name="fifth-level-heading"></a>第五層標題
###### <a name="sixth-level-heading"></a>第六層標題

## <a name="text-styling"></a>文字樣式設定

*斜體*

**粗體**

~~刪除線~~



## <a name="links"></a>連結

若要連結到相同存放庫中的 Markdown 檔案，請使用[相對連結](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2)。

- 範例：[什麼是 Azure Rights Management](./understand-explore/what-is-azure-rights-management.md)

若要連結到相同 Markdown 檔案中的標題，請檢視已發佈文章的原始檔並尋找標題的識別碼 (例如 `id="blockquote"`，然後使用 # + 識別碼來連結 (例如 `#blockquote`)。

- 範例：[區塊引述](#blockquote)

若要連結到相同存放庫之 Markdown 檔案中的標題，請使用相對連結 + 主題標籤連結。

- 範例：[註冊程序的技術概觀](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

若要連結到外部檔案，請使用完整 URL 作為連結。

- 範例：[Github](http://www.github.com)

若 URL 出現在 Markdown 檔案中，它將會被轉換為可點選的連結。

- 範例：http://www.github.com

## <a name="lists"></a>清單

### <a name="ordered-lists"></a>已排序的清單

1. 這
1. 是
1. 一個
1. 已排序的
1. 清單  


#### <a name="ordered-list-with-an-embedded-list"></a>具有內嵌清單的已排序清單

1. 這裡
1. 是
1. 一個
1. 內嵌
    1. Miss Scarlett
    1. Professor Plum
1. 已排序的
1. 清單


### <a name="unordered-lists"></a>未排序的清單

- 這
- 是
- 一個
- 項目符號
- 清單


##### <a name="unordered-list-with-an-embedded-lists"></a>具有內嵌清單的未排序清單

- 這
- 項目符號
- 清單
    - Mrs. Peacock
    - Mr. Green
- 包含  
- 其他
    1. Colonel Mustard
    1. Mrs. White
- 清單


## <a name="horizontal-rule"></a>水平尺規

---

## <a name="tables"></a>表格

| 表格        | 是           | 酷的  |
| ------------- |:-------------:| -----:|
| 第 3 欄是      | 靠右對齊 | $1600 |
| 第 2 欄是      | 置中對齊      |   $12 |
| 第 1 欄是預設值 | 靠左對齊     |    $1 |


## <a name="code"></a>程式碼

### <a name="codeblock"></a>程式碼區塊

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### <a name="in-line-code"></a>行內程式碼

這是 `in-line code` 的範例。

## <a name="blockquotes"></a>區塊引述

> 桃之夭夭，灼灼其華，之子于歸，宜其室家。 桃之夭夭，有蕡其實，之子于歸，宜其家室。 桃之夭夭，其葉蓁蓁，之子于歸，宜其家人。

## <a name="images"></a>影像

### <a name="static-image"></a>靜態影像

![這是替代文字](./media/AzRMS_elements.png)

### <a name="linked-image"></a>連結的影像

[![連結影像的替代文字](./media/AzRMS_elements.png)](https://azure.microsoft.com)

### <a name="animated-gif"></a>動畫 GIF

![動畫 GIF](./media/hololens.gif)

## <a name="alerts"></a>警示

### <a name="note"></a>附註

> [!NOTE]
> 這是附註

### <a name="warning"></a>警告

> [!WARNING]
> 這是警告

### <a name="tip"></a>祕訣

> [!TIP]
> 這是祕訣

### <a name="important"></a>重要

> [!IMPORTANT]
> 這很重要

## <a name="videos"></a>影片

### <a name="channel-9"></a>Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### <a name="youtube"></a>Youtube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## <a name="docsms-extentions"></a>docs.ms 延伸

### <a name="button"></a>按鈕

> [!div class="button"]
[按鈕連結](/rights-management)

### <a name="selector"></a>選取器

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### <a name="step-by-step"></a>逐步

>[!div class="step-by-step"]
[上一個](https://www.example.com)
[下一個](https://www.example.com)
