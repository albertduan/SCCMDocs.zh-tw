---
title: "使用應用程式設定原則設定 iOS 應用程式 | System Center Configuration Manager"
description: "在使用者執行應用程式之前先將應用程式設定原則部署到使用者，以避免執行 iOS 8 或更新版本的裝置發生設定問題。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-app
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74d5d776-e37d-45de-bdba-43541b03d12c
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9cbf28afbbe69f9a027ffad2a699b9d6b625e690


---
# <a name="configure-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Configure iOS apps with app configuration policies in System Center Configuration Manager

*適用對象：System Center Configuration Manager (最新分支)*


您可以在 System Center Configuration Manager 中使用應用程式設定原則，提供使用者執行應用程式時可能需要的設定。 例如，應用程式可能需要使用者指定：
- 自訂連接埠號碼
- 語言設定
- 安全性設定
- 公司標誌等品牌設定

如果使用者輸入不正確的設定，可能會增加技術支援中心的負擔，並使新應用程式的採用速度變慢。
應用程式組態原則可協助您避免這些問題；您可以在使用者執行應用程式之前，先在原則中將這些設定部署給使用者。 接著會自動提供這些設定，使用者不需要採取任何動作。
您不會直接將這些原則部署給使用者和裝置。 而是，在部署應用程式時，建立原則與部署類型的關聯。 每當應用程式檢查是否有原則時 (通常是第一次執行時)，便會使用這些原則設定。

應用程式設定原則目前僅適用於執行 iOS 8 和更新版本的裝置，並支援下列應用程式類型：

- **iOS 應用程式套件 (*.ipa 檔案)**
- **App Store 上的 iOS 應用程式套件**

如需應用程式安裝類型的詳細資訊，請參閱[應用程式管理簡介](/sccm/apps/understand/introduction-to-application-management)。

## <a name="create-an-app-configuration-policy"></a>建立應用程式設定原則

1. 在 Configuration Manager 主控台中，按一下 [軟體程式庫] > [應用程式管理] > [應用程式設定原則]。
3. 在 [首頁] 索引標籤的 [應用程式設定原則] 群組中，按一下 [建立新的應用程式設定原則]。
4. 在 [建立應用程式設定原則精靈] 的 [一般] 頁面中，指定下列資訊：
    - **名稱**：指定原則的唯一名稱。
    - **描述**：(選擇性) 指定有利識別的原則描述。
    - **已指派類別來改善搜尋和篩選效果**：(選擇性) 按一下 [類別] 建立分類並指派給原則。 這讓您更容易在 Configuration Manager 主控台中排序及尋找項目。
5. 在 [iOS 原則] 頁面上，選擇指定設定原則資訊的方式︰
    - **指定名稱及值配對**︰您可以對不使用巢狀結構的內容清單檔案使用此選項。
    指定名稱及值配對
        - 若要加入新的配對，請按一下 [新增]。
        - 在 [加入成對的名稱/值] 對話方塊方塊中，指定下列各項︰
            - **類型**︰從清單中，選擇您想要指定的值類型。
            - **名稱**︰輸入您要指定值的內容清單索引鍵的名稱。
            - **值**︰輸入的值會套用到您輸入的金鑰。
        - [瀏覽至內容清單檔案]︰如果已經有應用程式設定 XML 檔案，或針對使用巢狀結構的較複雜檔案，請使用此選項。
        瀏覽至內容清單檔案
            - 在 [應用程式設定原則] 欄位中，以正確的 XML 格式輸入內容清單資訊。
            若要深入了解 XML 屬性清單，請參閱 iOS Developer Library 中的[了解 XML 屬性清單](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html)。
            XML 屬性清單的格式會依您所設定的應用程式而有所不同。 如需所要使用之確切格式的詳細資訊，請連絡應用程式供應商。
            Intune 支援內容清單中的下列資料類型：
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
            如需資料類型的詳細資訊，請參閱 iOS Developer Library 中的[關於屬性清單](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html)。
            此外，Intune 也支援下列內容清單的權杖類型︰
            ```
            {{userprincipalname}} - (Example: John@contoso.com)
            {{mail}} - (Example: John@contoso.com)
            {{partialupn}} - (Example: John)
            {{accountid}} - (Example: fc0dc142-71d8-4b12-bbea-bae2a8514c81)
            {{deviceid}} - (Example: b9841cd9-9843-405f-be28-b2265c59ef97)
            {{userid}} - (Example: 3ec2c00f-b125-4519-acf0-302ac3761822)
            {{username}} - (Example: John Doe)
            {{serialnumber}} - (Example: F4KN99ZUG5V2) for iOS devices
            {{serialnumberlast4digits}} - (Example: G5V2) for iOS devices

            The {{ and }} characters are used by token types only and must not be used for other purposes.
            ```
            您也可以按一下 [選取檔案] 匯入先前建立的 XML 檔案。
6. 按一下 [下一步] 。 如果 XML 程式碼有錯誤，您必須先更正這些錯誤才能繼續。
6. 完成精靈。

新的應用程式設定原則會顯示在 [軟體程式庫] 工作區的 [應用程式設定原則] 節點中。

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>建立應用程式組態原則與 Configuration Manager 應用程式的關聯

若要建立應用程式設定原則與 iOS 應用程式部署的關聯性，您可使用[部署應用程式](/sccm/apps/deploy-use/deploy-applications)主題中的程序像平常那樣部署應用程式。
在 [部署軟體精靈] 的 [應用程式設定原則] 頁面，按一下 [新增]。 然後，在 [選取應用程式設定原則] 對話方塊方塊中，選擇應用程式部署類型和您希望與它建立關聯的應用程式設定原則。
部署類型安裝後，就會自動套用應用程式設定原則設定。

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>行動應用程式設定 XML 檔案的範例格式

當您建立行動應用程式設定檔時，您可以指定一或多個使用此格式的下列值︰

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>
```



<!--HONumber=Nov16_HO1-->


