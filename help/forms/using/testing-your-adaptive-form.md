---
title: 「教學課程：測試您的最適化表單」
seo-title: 「教學課程：測試您的最適化表單」
description: 使用自動化測試一次測試多個可調式表單。
seo-description: 使用自動化測試一次測試多個可調式表單。
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 3%

---


# 教學課程：測試您的最適化表單{#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

本教程是[建立第一個自適應表單](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的一個步驟。 建議依序依序依序排列，以瞭解、執行和展示完整的教學課程使用案例。

最適化表單準備就緒後，請務必先測試您的最適化，然後再將它推出給使用者。 您可以手動測試（功能測試）每個欄位，或自動測試最適化表單。 當您有多個可調式表單時，手動測試所有可調式表單的每個欄位將是一項艱巨的任務。

AEM[!DNL Forms]提供測試架構，Calvin，以自動測試您的調適性表單。 使用架構，您可直接在網頁瀏覽器中編寫並執行UI測試。 此架構提供JavaScript API以建立測試。 自動化測試可讓您測試自適應表單的預先填寫體驗、從驗證、延遲載入和UI互動提交自適應表單、運算式規則的體驗。 本教學課程會逐步引導您在最適化表單上建立和執行自動化測試的步驟。 在本教學課程結束時，您將能夠：

* [建立最適化表單的測試套裝](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [建立最適化表單的測試](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [執行為最適化表單建立的測試套裝和測試](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## 步驟1:建立測試套裝{#step-create-a-test-suite}

測試套裝包含一組測試案例。 您可以有多個測試套裝。 建議每個表單使用個別的測試套裝。 若要建立測試套裝：

1. 以管理員身AEM份登入[!DNL Forms]作者實例。 開啟[!UICONTROL CRXDE Lite]。 您可以點選AEM「標誌」>「工具」>「**** > **[!UICONTROL 「一般」>「CRXDE Lite」**[!UICONTROL &#x200B;或在瀏覽器中開啟「https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) URL」以開啟CRXDE Lite。]**]**[

1. 導覽至[!UICONTROL CRXDE Lite]中的/etc/clientlibs。 按一下右鍵/etc/clientlibs子資料夾，然後按一下&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 建立節點]**。 在&#x200B;**[!UICONTROL Name]**&#x200B;欄位中，鍵入&#x200B;**WeRetailFormTestCases**。 選擇類型為&#x200B;**cq:ClientLibraryFolder**，然後按一下&#x200B;**[!UICONTROL 確定]**。 它建立一個節點。 您可以使用任何名稱來取代`WeRetailFormTestCases`。
1. 將以下屬性添加到`WeRetailFormTestCases`節點並按一下「保存所有」(Save ALL)]**。**[!UICONTROL 

   <table>
    <tbody>
     <tr>
      <td><strong>屬性</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>多</strong></td>
      <td><strong>值</strong></td>
     </tr>
     <tr>
      <td>類別</td>
      <td>字串</td>
      <td>已啟用</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     <tr>
      <td>依賴性</td>
      <td>字串</td>
      <td>已啟用</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.testrunner <br /> </li>
        <li>granite.testing.calvin <br /> </li>
        <li>apps.testframework.all</li>
       </ul> </td>
     </tr>
    </tbody>
   </table>

   請確定每個屬性都新增至個別方塊，如下所示：

   ![依賴性](assets/dependencies.png)

1. 按一下右鍵&#x200B;**[!UICONTROL WeRetailFormTestCases]**&#x200B;節點，按一下&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 建立檔案]**。 在&#x200B;**[!UICONTROL Name]**&#x200B;欄位中，鍵入`js.txt`並按一下&#x200B;**[!UICONTROL OK]**。
1. 開啟js.txt檔案以進行編輯、新增下列程式碼並儲存檔案：

   ```text
   #base=.
    init.js
   ```

1. 在`WeRetailFormTestCases`節點中建立一個檔案init.js。 將下列程式碼新增至檔案，然後點選「全部儲存」。****

   ```javascript
   (function(window, hobs) {
       'use strict';
       window.testsuites = window.testsuites || {};
     // Registering the test form suite to the sytem
     // If there are other forms, all registration should be done here
       window.testsuites.testForm3 = new hobs.TestSuite("We retail - Tests", {
           path: '/etc/clientlibs/WeRetailFormTestCases/init.js',
           register: true
       });
    // window.testsuites.testForm2 = new hobs.TestSuite("testForm2");
   }(window, window.hobs));
   ```

   上述程式碼會建立名為&#x200B;**We retail - Tests**&#x200B;的測試套裝。

1. 開啟AEM測試UI(AEM> **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 測試]**)。 測試套件- **我們零售——測試** —— 列在UI中。

   ![we-retail-test-suite](assets/we-retail-test-suite.png)

## 步驟2:建立測試案例，以在最適化表單{#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}中預先填入值

測試案例是一組動作，可測試特定功能。 例如，預先填寫表單的所有欄位，並驗證幾個欄位，以確保輸入正確的值。

動作是最適化表單上的特定活動，例如按一下按鈕。 若要建立測試案例和動作，以驗證每個自適應表單欄位的使用者輸入：

1. 在[!UICONTROL CRXDE lite]中，導覽至`/content/forms/af/create-first-adaptive-form`資料夾。 按一下右鍵&#x200B;**[!UICONTROL create-first-adaptive-form]**&#x200B;資料夾節點，然後按一下&#x200B;**[!UICONTROL Create]****[!UICONTROL Create File]**。 在&#x200B;**[!UICONTROL Name]**&#x200B;欄位中，鍵入`prefill.xml`並按一下&#x200B;**[!UICONTROL OK]**。 將下列程式碼新增至檔案中：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?><afData>
     <afUnboundData>
       <data>
         <customer_ID>371767</customer_ID>
         <customer_Name>John Jacobs</customer_Name>
         <customer_Shipping_Address>1657 1657 Riverside Drive Redding</customer_Shipping_Address>
         <customer_State>California</customer_State>
         <customer_ZIPCode>096001</customer_ZIPCode>
        </data>
     </afUnboundData>
     <afBoundData>
       <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"/>
     </afBoundData>
   </afData>
   ```

1. 導航到 `/etc/clientlibs`. 按一下右鍵`/etc/clientlibs`子資料夾，然後按一下&#x200B;**[!UICONTROL 建立]****[!UICONTROL 建立節點]**。

   在&#x200B;**[!UICONTROL 名稱]**&#x200B;欄位中，鍵入`WeRetailFormTests`。 選擇類型`cq:ClientLibraryFolder`，然後按一下&#x200B;**[!UICONTROL 確定]**。

1. 將下列屬性新增至&#x200B;**[!UICONTROL WeRetailFormTests]**&#x200B;節點。

   <table>
    <tbody>
     <tr>
      <td><strong>屬性</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>多</strong></td>
      <td><strong>值</strong></td>
     </tr>
     <tr>
      <td>類別</td>
      <td>字串</td>
      <td>已啟用</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.hobbes.tests.testForm</li>
       </ul> </td>
     </tr>
     <tr>
      <td>依賴性</td>
      <td>字串</td>
      <td>已啟用</td>
      <td>
       <ul>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     </tbody>
   </table>

1. 在&#x200B;**[!UICONTROL WeRetailFormTests]**&#x200B;節點中建立js.txt檔案。 將下列項目新增至檔案：

   ```shell
   #base=.
   prefillTest.js
   ```

   按一下&#x200B;**[!UICONTROL 保存全部]**。

1. 在&#x200B;**[!UICONTROL WeRetailFormTests]**&#x200B;節點中建立`prefillTest.js`檔案。 將下列程式碼新增至檔案。 程式碼會建立測試案例。 測試案例會預先填寫表單的所有欄位，並驗證某些欄位，以確保輸入正確的值。

   ```javascript
   (function (window, hobs) {
       'use strict';
   
       var ts = new hobs.TestSuite("Prefill Test", {
           path: '/etc/clientlibs/WeRetailFormTests/prefillTest.js',
           register: false
       })
   
       .addTestCase(new hobs.TestCase("Prefill Test")
           // navigate to the testForm which is to be test
           .navigateTo("/content/forms/af/create-first-adaptive-form/shipping-address-add-update-form.html?wcmmode=disabled&dataRef=crx:///content/forms/af/create-first-adaptive-form/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ID").value == 371767;
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ZIPCode").value == 96001;
           })
       );
   
       // register the test suite with testForm
       window.testsuites.testForm3.add(ts);
   
   }(window, window.hobs));
   ```

   測試案例已建立並可供執行。 您可以建立測試案例來驗證自適應表單的各個方面，例如檢查計算指令碼的執行、驗證模式，以及驗證自適應表單的提交體驗。 如需有關最適化表單測試各方面的資訊，請參閱自動化最適化表單測試。

## 步驟3:在套裝或個別測試案例中執行所有測試{#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}

測試套裝可以有多個測試案例。 您可以一次或個別執行測試套裝中的所有測試案例。 當您執行測試時，圖示會指出結果：

* 複選標籤圖示表示通過的測試：![save_icon](assets/save_icon.svg)
* 「X」圖示表示測試失敗：![close-icon](assets/close-icon.svg)

1. 導航至AEM表徵圖> **[!UICONTROL 工具]**> **[!UICONTROL 操作]**> **[!UICONTROL 測試]**
1. 若要執行測試套裝的所有測試：

   1. 在[!UICONTROL Tests]面板中，點選&#x200B;**[!UICONTROL We retail - Tests(1)]**。 此套裝會展開以顯示測試清單。
   1. 點選&#x200B;**[!UICONTROL 執行測試]**&#x200B;按鈕。 當測試執行時，螢幕右側的空白區域會以最適化形式取代。

      ![run-all-test](assets/run-all-test.png)

1. 若要從測試套裝執行單一測試：

   1. 在「測試」面板中，點選&#x200B;**[!UICONTROL We retail - Tests(1)]**。 此套裝會展開以顯示測試清單。
   1. 點選&#x200B;**[!UICONTROL 預填Test]**&#x200B;並點選&#x200B;**[!UICONTROL Run tests]**&#x200B;按鈕。 當測試執行時，螢幕右側的空白區域會以最適化形式取代。

1. 點選測試名稱「預填」測試，以檢閱測試案例的結果。 它會開啟[!UICONTROL Result]面板。 在[!UICONTROL Result]面板中點選測試案例的名稱，以檢視測試的所有詳細資訊。

   ![審查結果](assets/review-results.png)

現在，最適化表單已可供發佈。
