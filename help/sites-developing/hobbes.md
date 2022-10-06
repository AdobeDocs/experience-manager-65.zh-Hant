---
title: 測試您的UI
seo-title: Testing Your UI
description: AEM提供AEM UI測試自動化的架構
seo-description: AEM provides a framework for automating tests for your AEM UI
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 1%

---

# 測試您的UI{#testing-your-ui}

>[!NOTE]
>
>自AEM 6.5起，已棄用hobbes.js UI測試架構。 Adobe不打算對其進行進一步的增強，並建議客戶使用Selenium自動化。
>
>請參閱 [過時和移除的功能](/help/release-notes/deprecated-removed-features.md).

AEM提供AEM UI測試自動化的架構。 使用框架時，直接在Web瀏覽器中編寫並運行UI測試。 架構提供用於建立測試的javascript API。

AEM測試架構使用Hobbes.js，這是以Javascript撰寫的測試程式庫。 Hobbes.js架構是在開發程式中為測試AEM而開發。 此架構現已可供公開使用，以測試您的AEM應用程式。

>[!NOTE]
>
>請參閱Hobbes.js [檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html) 以取得API的完整詳細資訊。

## 測試結構 {#structure-of-tests}

在AEM內使用自動化測試時，下列辭彙是您務必了解的重要項目：

| 動作 | 安 **動作** 是網頁上的特定活動，例如按一下連結或按鈕。 |
|---|---|
| 測試案例 | A **測試案例** 是由一或多個組成的特定情況 **動作**. |
| 測試套裝 | A **測試套裝** 是一組 **測試案例** 一起測試特定使用案例。 |

## 執行測試 {#executing-tests}

### 檢視測試套裝 {#viewing-test-suites}

開啟測試主控台，查看已註冊的測試套裝。 「測試」面板包含測試套裝及其測試案例的清單。

透過導覽至工具主控台 **全局導航 — >工具>操作 — >測試**.

![chlimage_1-63](assets/chlimage_1-63.png)

開啟主控台時，測試套裝會列在左側，並附上可依序執行所有測試套裝的選項。 右側以方格背景顯示的空格是測試執行時顯示頁面內容的預留位置。

![chlimage_1-64](assets/chlimage_1-64.png)

### 執行單一測試套裝 {#running-a-single-test-suite}

測試套裝可個別執行。 當您執行測試套裝時，頁面會隨著測試案例及其動作執行而變更，結果會在測試完成後顯示。 圖示會指出結果。

勾選記號圖示表示通過的測試：

![](do-not-localize/chlimage_1-2.png)

「X」圖示表示測試失敗：

![](do-not-localize/chlimage_1-3.png)

若要執行測試套裝：

1. 在「測試」面板中，按一下或點選您要執行的「測試案例」名稱，以展開「動作」的詳細資訊。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 按一下或點選 **運行測試** 按鈕。

   ![](do-not-localize/chlimage_1-4.png)

1. 測試執行時，預留位置會以頁面內容取代。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 點選或按一下說明以開啟 **結果** 中。 點選或按一下 **結果** 面板會顯示所有詳細資料。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 執行多個測試 {#running-multiple-tests}

測試套裝會依其顯示在主控台中的順序執行。 您可以深入檢視測試，以查看詳細結果。

![chlimage_1-68](assets/chlimage_1-68.png)

1. 在「測試」面板上，點選或按一下 **運行所有測試** 按鈕或 **執行測試** 按鈕（位於要運行的測試套裝標題下）。

   ![](do-not-localize/chlimage_1-5.png)

1. 若要檢視每個測試案例的結果，請點選或按一下測試案例的標題。 在 **結果** 面板會顯示所有詳細資料。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 建立和使用簡單測試套裝 {#creating-and-using-a-simple-test-suite}

以下過程將逐步引導您使用 [We.Retail內容](/help/sites-developing/we-retail.md)，但您可以輕鬆修改測試，以使用不同的網頁。

如需建立自己測試套裝的完整詳細資訊，請參閱 [Hobbes.js API檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html).

1. 開啟CRXDE Lite。 ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. 以滑鼠右鍵按一下 `/etc/clientlibs` 資料夾，按一下 **建立>建立資料夾**. 類型 `myTests` 按一下 **確定**.
1. 以滑鼠右鍵按一下 `/etc/clientlibs/myTests` 資料夾，按一下 **建立>建立節點**. 使用下列屬性值，然後按一下 **確定**:

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
   >若要測試適用性表單，請將下列值新增至類別和相依性。 例如：
   >
   >
   >**類別**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**相依性**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. 按一下 **全部儲存**.
1. 以滑鼠右鍵按一下 `myFirstTest` 節點，按一下 **建立>建立檔案**. 為檔案命名 `js.txt` 按一下 **確定**.
1. 在 `js.txt` ，請輸入以下文本：

   ```
   #base=.
   myTestSuite.js
   ```

1. 按一下 **全部儲存** 然後關閉 `js.txt` 檔案。
1. 以滑鼠右鍵按一下 `myFirstTest` 節點，按一下 **建立>建立檔案**. 為檔案命名 `myTestSuite.js` 按一下 **確定**.
1. 將下列程式碼複製到 `myTestSuite.js` 檔案，然後儲存檔案：

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

1. 導覽至 **測試** 主控台以嘗試您的測試套裝。
