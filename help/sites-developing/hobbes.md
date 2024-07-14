---
title: 測試您的UI
description: AEM為AEM UI提供自動化測試框架
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 3%

---

# 測試您的UI{#testing-your-ui}

>[!NOTE]
>
>從AEM 6.5開始，不建議使用hobbes.js UI測試架構。 Adobe不打算進一步增強功能，因此建議客戶使用Selenium自動化。
>
>請參閱[已過時和已移除的功能](/help/release-notes/deprecated-removed-features.md)。

AEM為AEM UI提供自動化測試框架。 使用框架，您可以直接在網頁瀏覽器中編寫和執行UI測試。 此架構提供用來建立測試的JavaScript API。

AEM測試架構使用Hobbes.js，這是以JavaScript撰寫的測試程式庫。 Hobbes.js架構是作為開發流程的一部分開發用於測試AEM。 此架構現在可供公眾用來測試您的AEM應用程式。

>[!NOTE]
>
>如需API的完整詳細資訊，請參閱Hobbes.js [檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html)。

## 測試結構 {#structure-of-tests}

在AEM中使用自動化測試時，請務必瞭解下列詞語：

| 動作 | **動作**&#x200B;是網頁上的特定活動，例如按一下連結或按鈕。 |
|---|---|
| 測試案例 | **測試案例**&#x200B;是一種特定情況，可由一或多個&#x200B;**動作**&#x200B;組成。 |
| 測試套裝 | **測試套裝**&#x200B;是一組相關的&#x200B;**測試案例**，它們共同測試特定使用案例。 |

## 執行測試 {#executing-tests}

### 檢視測試套裝 {#viewing-test-suites}

開啟「測試主控台」以檢視已註冊的測試套裝。 「測試」面板包含測試套裝及其測試案例的清單。

透過&#x200B;**全域導覽>工具>作業>測試**&#x200B;來瀏覽工具主控台。

![chlimage_1-63](assets/chlimage_1-63.png)

開啟主控台時，左側會列出測試套裝，並附上可依序執行所有測試套裝的選項。 右側以格線型背景顯示的空格是測試執行時顯示頁面內容的預留位置。

![chlimage_1-64](assets/chlimage_1-64.png)

### 執行單一測試套裝 {#running-a-single-test-suite}

測試套裝可以個別執行。 當您執行測試套裝時，頁面會隨著測試案例及其動作的執行而變更，並且會在測試完成後顯示結果。 圖示會指出結果。

核取記號圖示表示測試通過：

![核取記號圖示。](do-not-localize/chlimage_1-2.png)

「X」圖示表示測試失敗：

![圓環內的X所指示的失敗測試圖示。](do-not-localize/chlimage_1-3.png)

若要執行測試套裝：

1. 在「測試」面板中，按一下您要執行的測試案例名稱以展開動作的詳細資訊。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 按一下&#x200B;**執行測試**。

   ![「執行測試」按鈕的影像，以圓圈內面向右的指標表示。](do-not-localize/chlimage_1-4.png)

1. 測試執行時，預留位置會取代為頁面內容。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 點選或按一下說明以開啟&#x200B;**結果**&#x200B;面板，以檢閱測試案例的結果。 在&#x200B;**結果**&#x200B;面板中，點選或按一下測試案例的名稱會顯示所有詳細資料。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 執行多項測試 {#running-multiple-tests}

測試套裝會依顯示在主控台中的順序執行。 您可以深入研究測試以檢視詳細結果。

![chlimage_1-68](assets/chlimage_1-68.png)

1. 在[測試]面板上，按一下[執行所有測試] **按鈕或您要執行之測試套裝標題下方的[執行測試]** [執行測試] **按鈕。**

   ![[執行全部測試]按鈕和[執行測試]按鈕的影像，以圓圈內面向右側的指標表示。](do-not-localize/chlimage_1-5.png)

1. 若要檢視每個測試案例的結果，請按一下測試案例的標題。 在&#x200B;**結果**&#x200B;面板中按一下測試名稱會顯示所有詳細資料。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 建立和使用簡單測試套裝 {#creating-and-using-a-simple-test-suite}

下列程式會逐步引導您使用[We.Retail內容](/help/sites-developing/we-retail.md)建立並執行測試套裝，但您可以輕鬆修改測試，以使用不同的網頁。

如需建立您自己的測試套裝的完整詳細資訊，請參閱[Hobbes.js API檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html)。

1. 開啟CRXDE Lite。 ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. 用滑鼠右鍵按一下`/etc/clientlibs`資料夾，然後按一下&#x200B;**建立>建立資料夾**。 輸入名稱`myTests`並按一下&#x200B;**確定**。
1. 以滑鼠右鍵按一下`/etc/clientlibs/myTests`資料夾，然後按一下&#x200B;**建立>建立節點**。 使用以下屬性值，然後按一下&#x200B;**確定**：

   * 名稱：`myFirstTest`
   * 類型：`cq:ClientLibraryFolder`

1. 將下列屬性新增至myFirstTest節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | `categories` | 字串[] | `granite.testing.hobbes.tests` |
   | `dependencies` | 字串[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**僅限AEM Forms**
   >
   >
   >若要測試調適型表單，請將下列值新增至類別和相依性。 例如：
   >
   >
   >**類別**： `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**相依性**： `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. 按一下&#x200B;**「儲存全部」**。
1. 以滑鼠右鍵按一下`myFirstTest`節點，然後按一下&#x200B;**建立>建立檔案**。 將檔案命名為`js.txt`並按一下&#x200B;**確定**。
1. 在`js.txt`檔案中，輸入下列文字：

   ```
   #base=.
   myTestSuite.js
   ```

1. 按一下[儲存全部]****，然後關閉`js.txt`檔案。
1. 以滑鼠右鍵按一下`myFirstTest`節點，然後按一下&#x200B;**建立>建立檔案**。 將檔案命名為`myTestSuite.js`並按一下&#x200B;**確定**。
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

1. 導覽至&#x200B;**測試**&#x200B;主控台，嘗試您的測試套裝。
