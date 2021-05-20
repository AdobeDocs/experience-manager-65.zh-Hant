---
title: 「教學課程：測試最適化表單」
seo-title: 「教學課程：測試最適化表單」
description: 使用自動化測試一次測試多個最適化表單。
seo-description: 使用自動化測試一次測試多個最適化表單。
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
feature: 適用性表單
exl-id: 343e2e0b-d5ef-4f01-b3d6-45f90e2430fd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 3%

---

# 教學課程：測試最適化表單{#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

本教學課程是[建立第一個最適化表單](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的步驟。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

最適化表單準備就緒後，請務必先測試您的最適化，再將其轉出給一般使用者。 您可以手動測試（功能測試）每個欄位，或自動測試最適化表單。 當您有多個最適化表單時，手動測試所有最適化表單的每個欄位將是一項艱巨的任務。

AEM [!DNL Forms]提供測試框架Calvin，以自動測試最適化表單。 使用框架時，直接在Web瀏覽器中編寫並運行UI測試。 架構提供JavaScript API以用於建立測試。 自動化測試可讓您測試最適化表單的預填體驗、提交最適化表單的體驗、運算式規則、驗證、延遲載入和UI互動。 本教學課程會逐步引導您完成在最適化表單上建立和執行自動化測試的步驟。 在本教學課程結束時，您將能夠：

* [為最適化表單建立測試套裝](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [為最適化表單建立測試](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [執行為最適化表單建立的測試套裝和測試](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## 步驟1:建立測試套裝{#step-create-a-test-suite}

測試套裝包含測試案例的集合。 您可以有多個測試套裝。 建議為每個表單分別設定一個測試套裝。 若要建立測試套裝：

1. 以管理員身分登入AEM [!DNL Forms]製作執行個體。 開啟[!UICONTROL CRXDE Lite]。 您可以點選「AEM標誌> **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**」，或在瀏覽器中開啟[https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) URL以開啟CRXDE Lite。

1. 導覽至[!UICONTROL CRXDE Lite]中的/etc/clientlibs。 按一下右鍵/etc/clientlibs子資料夾，然後按一下&#x200B;**[!UICONTROL Create]** > **[!UICONTROL Create Node]**。 在&#x200B;**[!UICONTROL Name]**&#x200B;欄位中，鍵入&#x200B;**WeRetailFormTestCases**。 選擇類型為&#x200B;**cq:ClientLibraryFolder**，然後按一下&#x200B;**[!UICONTROL 確定]**。 它會建立一個節點。 您可以使用任何名稱來取代`WeRetailFormTestCases`。
1. 將以下屬性添加到`WeRetailFormTestCases`節點，然後點選&#x200B;**[!UICONTROL Save ALL]**。

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
      <td>相依性</td>
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

   ![相依性](assets/dependencies.png)

1. 按一下右鍵&#x200B;**[!UICONTROL WeRetailFormTestCases]**&#x200B;節點，按一下&#x200B;**[!UICONTROL Create]** > **[!UICONTROL Create File]**。 在&#x200B;**[!UICONTROL Name]**&#x200B;欄位中，鍵入`js.txt`並按一下&#x200B;**[!UICONTROL OK]**。
1. 開啟js.txt檔案進行編輯、新增下列程式碼並儲存檔案：

   ```text
   #base=.
    init.js
   ```

1. 在`WeRetailFormTestCases`節點中建立檔案init.js。 將下列程式碼新增至檔案，然後點選「**[!UICONTROL 儲存全部]**」。

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

1. 開啟AEM Testing UI(AEM > **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Testing]**)。 UI中列出測試套裝 — **We retail - Tests** -。

   ![we-retail-test-suite](assets/we-retail-test-suite.png)

## 步驟2:建立測試案例以在最適化表單{#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}中預填值

測試案例是測試特定功能的一組動作。 例如，預填表單的所有欄位，並驗證幾個欄位，以確保輸入正確的值。

動作是適用性表單上的特定活動，例如按一下按鈕。 若要建立測試案例和動作，以驗證每個最適化表單欄位的使用者輸入：

1. 在[!UICONTROL CRXDE lite]中，導覽至`/content/forms/af/create-first-adaptive-form`資料夾。 以滑鼠右鍵按一下&#x200B;**[!UICONTROL create-first-adaptive-form]**&#x200B;資料夾節點，然後按一下&#x200B;**[!UICONTROL Create]**> **[!UICONTROL Create File]**。 在&#x200B;**[!UICONTROL Name]**&#x200B;欄位中，鍵入`prefill.xml`並按一下&#x200B;**[!UICONTROL OK]**。 將下列程式碼新增至檔案中：

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

1. 導航到 `/etc/clientlibs`. 按一下右鍵`/etc/clientlibs`子資料夾，然後按一下&#x200B;**[!UICONTROL Create]** **[!UICONTROL Create Node]**。

   在&#x200B;**[!UICONTROL 名稱]**&#x200B;欄位中，鍵入`WeRetailFormTests`。 選擇類型`cq:ClientLibraryFolder`，然後按一下&#x200B;**[!UICONTROL 確定]**。

1. 將下列屬性添加到&#x200B;**[!UICONTROL WeRetailFormTests]**&#x200B;節點。

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
      <td>相依性</td>
      <td>字串</td>
      <td>已啟用</td>
      <td>
       <ul>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     </tbody>
   </table>

1. 在&#x200B;**[!UICONTROL WeRetailFormTests]**&#x200B;節點中建立檔案js.txt。 將下列項目新增至檔案：

   ```shell
   #base=.
   prefillTest.js
   ```

   按一下「**[!UICONTROL 全部保存]**」。

1. 在&#x200B;**[!UICONTROL WeRetailFormTests]**&#x200B;節點中建立檔案`prefillTest.js`。 將下列程式碼新增至檔案。 程式碼會建立測試案例。 測試案例會預填表單的所有欄位，並驗證某些欄位，以確保輸入正確的值。

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

   已建立測試案例並準備運行。 您可以建立測試案例來驗證適用性表單的各個方面，例如檢查計算指令碼的執行、驗證模式，以及驗證適用性表單的提交體驗。 如需適用性表單測試各個層面的相關資訊，請參閱自動測試適用性表單。

## 步驟3:在套裝或個別測試案例{#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}中執行所有測試

一個測試套裝可以有多個測試案例。 您可以一次或個別執行測試套裝中的所有測試案例。 當您執行測試時，圖示會指出結果：

* 勾選記號圖示表示通過的測試：![save_icon](assets/save_icon.svg)
* 「X」圖示表示測試失敗：![close-icon](assets/close-icon.svg)

1. 導覽至AEM圖示> **[!UICONTROL Tools]**> **[!UICONTROL Operations]**> **[!UICONTROL Testing]**
1. 要運行測試套裝的所有測試，請執行以下操作：

   1. 在「[!UICONTROL 測試]」面板中，點選「**[!UICONTROL We retail - Tests(1)]**」。 它套裝會展開並顯示測試清單。
   1. 點選&#x200B;**[!UICONTROL 執行測試]**&#x200B;按鈕。 測試執行時，螢幕右側的空白區域會以最適化表單取代。

      ![run-all-test](assets/run-all-test.png)

1. 若要從測試套裝執行單一測試：

   1. 在「測試」面板中，點選&#x200B;**[!UICONTROL We retail - Tests(1)]**。 它套裝會展開並顯示測試清單。
   1. 點選&#x200B;**[!UICONTROL 預填測試]**&#x200B;並點選&#x200B;**[!UICONTROL 執行測試]**&#x200B;按鈕。 測試執行時，螢幕右側的空白區域會以最適化表單取代。

1. 點選測試名稱「預填測試」 ，以檢閱測試案例的結果。 它會開啟[!UICONTROL Result]面板。 點選[!UICONTROL Result]面板中的測試案例名稱，以檢視測試的所有詳細資訊。

   ![review-results](assets/review-results.png)

現在最適化表單已可供發佈。
