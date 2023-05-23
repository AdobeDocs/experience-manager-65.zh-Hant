---
title: 測試您的UI
seo-title: Testing Your UI
description: 為AEM您的UI提供自動test的框AEM架
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
ht-degree: 2%

---

# 測試您的UI{#testing-your-ui}

>[!NOTE]
>
>從AEM6.5開始，hobbes.js UI測試框架被棄用。 Adobe沒有計畫對其進行進一步的增強，並建議客戶使用硒自動化。
>
>請參閱 [已棄用和已刪除的功能](/help/release-notes/deprecated-removed-features.md)。

為AEM您的UI提供自動test的AEM框架。 使用框架，您可以直接在Web瀏覽器中編寫和運行UItest。 該框架提供用於建立test的javascript API。

該AEMtest框架使用Hobbes.js，這是一個用Javascript編寫的測試庫。 Hobbes.js框架是作為開發過程的一AEM部分，用於測試。 該框架現在可供公共使用，用於測試您的應AEM用程式。

>[!NOTE]
>
>請參閱Hobbes.js [文檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html) 的子菜單。

## test {#structure-of-tests}

在中使用自動testAEM時，以下術語非常重要，需要瞭解：

| 動作 | 安 **操作** 是網頁上的特定活動，如按一下連結或按鈕。 |
|---|---|
| Test案 | A **Test案** 是由一個或多個 **操作**。 |
| Test套件 | A **Test套件** 是一組 **Test案例** 一起test特定用例。 |

## 執行Test {#executing-tests}

### 查看Test套件 {#viewing-test-suites}

開啟測試控制台查看已註冊的Test套件。 test面板包含test套件及其test箱的清單。

通過以下方式導航至工具控制台： **全局導航 — >工具>操作 — >測試**。

![chlimage_1-63](assets/chlimage_1-63.png)

開啟控制台時，Test套件將列在左側，並帶有按順序運行所有套件的選項。 右邊顯示的帶方格背景的空間是test運行時顯示頁面內容的佔位符。

![chlimage_1-64](assets/chlimage_1-64.png)

### 運行單個Test套件 {#running-a-single-test-suite}

Test套房可以單獨運營。 運行Test套件時，頁面會隨Test案例及其操作的執行而改變，結果在test完成後顯示。 表徵圖表示結果。

複選標籤表徵圖表示傳遞的test:

![](do-not-localize/chlimage_1-2.png)

「X」表徵圖表示test失敗：

![](do-not-localize/chlimage_1-3.png)

要運行Test套件：

1. 在「Test」面板中，按一下或點擊要運行的Test案例的名稱，以展開「操作」的詳細資訊。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 按一下或點擊 **運行test** 按鈕

   ![](do-not-localize/chlimage_1-4.png)

1. 執行test時，佔位符將替換為頁面內容。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 按一下或按一下說明以開啟「Test」(Case)的結果 **結果** 的子菜單。 點擊或按一下Test的名稱 **結果** 面板顯示所有詳細資訊。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 運行多個Test {#running-multiple-tests}

Test套件按在控制台中顯示的順序執行。 您可以深入test查看詳細結果。

![chlimage_1-68](assets/chlimage_1-68.png)

1. 在「Test」面板上，點擊或按一下 **運行所有test** 按鈕 **運行test** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。

   ![](do-not-localize/chlimage_1-5.png)

1. 要查看每個Test案例的結果，請點擊或按一下Test案例的標題。 點擊或按一下test的名稱 **結果** 面板顯示所有詳細資訊。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 建立和使用簡單Test套件 {#creating-and-using-a-simple-test-suite}

以下過程用於完成建立和執行Test套件的過程 [We.Retail內容](/help/sites-developing/we-retail.md)，但您可以輕鬆修改test以使用其他網頁。

有關建立您自己的Test套件的完整詳細資訊，請參閱 [Hobbes.js API文檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html)。

1. 開啟CRXDE Lite。 ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. 按一下右鍵 `/etc/clientlibs` 資料夾，按一下 **「建立」>「建立資料夾」**。 類型 `myTests` ，然後按一下 **確定**。
1. 按一下右鍵 `/etc/clientlibs/myTests` 資料夾，按一下 **「建立」>「建立節點」**。 使用以下屬性值，然後按一下 **確定**:

   * 名稱: `myFirstTest`
   * 類型: `cq:ClientLibraryFolder`

1. 將以下屬性添加到myFirstTest節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | `categories` | 字串[] | `granite.testing.hobbes.tests` |
   | `dependencies` | 字串[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**僅AEM Forms**
   >
   >
   >要test自適應表單，請將以下值添加到類別和依賴項。 例如：
   >
   >
   >**類別**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**依賴**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. 按一下 **全部保存**。
1. 按一下右鍵 `myFirstTest` 按一下 **建立>建立檔案**。 命名檔案 `js.txt` 按一下 **確定**。
1. 在 `js.txt` ，輸入以下文本：

   ```
   #base=.
   myTestSuite.js
   ```

1. 按一下 **全部保存** 然後關閉 `js.txt` 的子菜單。
1. 按一下右鍵 `myFirstTest` 按一下 **建立>建立檔案**。 命名檔案 `myTestSuite.js` 按一下 **確定**。
1. 將以下代碼複製到 `myTestSuite.js` 檔案，然後保存檔案：

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

1. 導航到 **測試** 控制台以嘗試您的test套件。
