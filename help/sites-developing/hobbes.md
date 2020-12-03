---
title: 測試您的UI
seo-title: 測試您的UI
description: AEM提供自動化AEM UI測試的架構
seo-description: AEM提供自動化AEM UI測試的架構
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---


# 測試您的UI{#testing-your-ui}

>[!NOTE]
>
>從AEM 6.5開始，hobbes.js UI測試架構已過時。 Adobe不打算對它做進一步的增強，並建議客戶使用Selenium自動化。
>
>請參閱[已過時和已移除的功能](/help/release-notes/deprecated-removed-features.md)。

AEM提供自動化AEM UI測試的架構。 使用架構，您可直接在網頁瀏覽器中編寫並執行UI測試。 架構提供建立測試的javascript API。

AEM測試架構使用Hobbes.js，此為以Javascript撰寫的測試程式庫。 Hobbes.js架構是做為開發程式的一部份，用於測試AEM。 此架構現已可供公開使用，以測試您的AEM應用程式。

>[!NOTE]
>
>如需API的完整詳細資訊，請參閱Hobbes.js [檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html)。

## 測試結構{#structure-of-tests}

在AEM中使用自動測試時，下列術語很重要，請務必瞭解：

| 動作 | **Action**&#x200B;是網頁上的特定活動，例如按一下連結或按鈕。 |
|---|---|
| 測試案例 | **測試案例**&#x200B;是由一個或多個&#x200B;**動作**&#x200B;組成的特定情況。 |
| 測試套件 | A **測試套件**&#x200B;是一組相關的&#x200B;**測試案例**，可一起測試特定使用案例。 |

## 執行測試{#executing-tests}

### 檢視測試套裝{#viewing-test-suites}

開啟測試主控台，以查看已註冊的測試套裝。 「測試」面板包含測試套裝及其測試案例的清單。

透過&#x200B;**全域導覽->工具>作業->測試導覽至工具主控台。**

![chlimage_1-63](assets/chlimage_1-63.png)

當開啟主控台時，測試套裝會列在左側，並提供依序執行所有測試套裝的選項。 右方空格以方格背景顯示，是在測試執行時顯示頁面內容的預留位置。

![chlimage_1-64](assets/chlimage_1-64.png)

### 執行單一測試套裝{#running-a-single-test-suite}

測試套裝可個別執行。 當您執行測試套裝時，頁面會隨著測試案例及其動作的執行而變更，結果會在測試完成後顯示。 圖示表示結果。

複選標籤圖示表示通過的測試：

![](do-not-localize/chlimage_1-2.png)

「X」圖示表示測試失敗：

![](do-not-localize/chlimage_1-3.png)

若要執行測試套裝：

1. 在「測試」面板中，按一下或點選您要執行的測試案例名稱，以展開動作的詳細資訊。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 按一下或點選&#x200B;**運行test**&#x200B;按鈕。

   ![](do-not-localize/chlimage_1-4.png)

1. 測試執行時，預留位置會以頁面內容取代。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 點選或按一下說明以開啟&#x200B;**Result**&#x200B;面板，以檢視測試案例的結果。 在&#x200B;**Result**&#x200B;面板中點選或按一下測試案例名稱，可顯示所有詳細資訊。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 運行多個測試{#running-multiple-tests}

測試套裝會依其顯示在主控台中的順序執行。 您可以深入探究測試，以檢視詳細結果。

![chlimage_1-68](assets/chlimage_1-68.png)

1. 在「測試」面板上，點選或按一下您要執行之測試套裝標題下方的&#x200B;**執行所有測試**&#x200B;按鈕或&#x200B;**執行測試**&#x200B;按鈕。

   ![](do-not-localize/chlimage_1-5.png)

1. 若要檢視每個測試案例的結果，請點選或按一下測試案例的標題。 在&#x200B;**Result**&#x200B;面板中點選或按一下測試名稱會顯示所有詳細資料。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 建立和使用簡易測試套裝{#creating-and-using-a-simple-test-suite}

下列程式會逐步引導您使用[We.Retail內容](/help/sites-developing/we-retail.md)建立和執行測試套裝，但您可輕鬆修改測試以使用不同的網頁。

如需建立自己測試套裝的完整詳細資訊，請參閱[Hobbes.js API檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html)。

1. 開啟CRXDE Lite。 ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. 按一下右鍵`/etc/clientlibs`資料夾，然後按一下&#x200B;**建立>建立資料夾**。 鍵入`myTests`作為名稱，然後按一下&#x200B;**OK**。
1. 按一下右鍵`/etc/clientlibs/myTests`資料夾，然後按一下&#x200B;**建立>建立節點**。 使用下列屬性值，然後按一下&#x200B;**OK**:

   * 名稱: `myFirstTest`
   * 類型: `cq:ClientLibraryFolder`

1. 將下列屬性新增至myFirstTest節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | `categories` | String[] | `granite.testing.hobbes.tests` |
   | `dependencies` | 字串[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**僅限AEM Forms**
   >
   >
   >若要測試最適化表單，請將下列值新增至類別和相依性。 例如：
   >
   >
   >**類別**:  `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**相依性**:  `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. 按一下&#x200B;**保存全部**。
1. 按一下右鍵`myFirstTest`節點，然後按一下&#x200B;**建立>建立檔案**。 命名檔案`js.txt`並按一下&#x200B;**確定**。
1. 在`js.txt`檔案中，輸入以下文本：

   ```
   #base=.
   myTestSuite.js
   ```

1. 按一下「全部儲存」，然後關閉&#x200B;**檔案。**`js.txt`
1. 按一下右鍵`myFirstTest`節點，然後按一下&#x200B;**建立>建立檔案**。 命名檔案`myTestSuite.js`並按一下&#x200B;**確定**。
1. 將下列程式碼複製到`myTestSuite.js`檔案，然後儲存檔案：

   ```
   new hobs.TestSuite("Experience Content Test Suite", {path:"/etc/clientlibs/myTests/myFirstTest/myTestSuite.js"})
      .addTestCase(new hobs.TestCase("Navigate to Experience Content")
         .navigateTo("/content/we-retail/us/en/experience/arctic-surfing-in-lofoten.html")
      )
      .addTestCase(new hobs.TestCase("Hover Over Topnav")
         .mouseover("li.visible-xs")
      )
      .addTestCase(new hobs.TestCase("Click Topnav Link")
         .click("li.active a")
   );
   ```

1. 導覽至&#x200B;**Testing**&#x200B;主控台以試用您的測試套裝。
