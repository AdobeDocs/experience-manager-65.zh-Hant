---
title: 調試HTML5表單
seo-title: Debugging HTML5 forms
description: 檔案清單步驟可疑難排解各種已知問題。
seo-description: The document list steps to troubleshoot various known issues.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: Mobile Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 1%

---

# 調試HTML5表單 {#debugging-html-forms}

本檔案包含數個疑難排解案例。 對於每種情況，都提供一些步驟來排解問題。 請依照下列步驟操作，如果問題持續發生，請設定記錄器以取得並檢閱記錄檔，以取得錯誤/警告。 如需HTML5表單記錄的詳細資訊，請參閱 [為HTML5表單產生記錄](/help/forms/using/enable-logs.md).

## 問題：轉譯表單時，我會看到org.apache.sling.api.SlingException頁面 {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

在例外詳細資訊中，搜索單詞 **由**.

可能是因為URL中的一或多個參數不正確。

檢查下列參數：

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>範本</td>
   <td>範本的檔案名稱</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>範本和相關資源所在的路徑</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>與範本合併之資料檔案的絕對路徑。<br /> 注意：路徑定義資料檔案的絕對路徑。</td>
  </tr>
  <tr>
   <td>資料</td>
   <td>與範本合併的UTF-8編碼資料位元組。</td>
  </tr>
 </tbody>
</table>

## 問題：無法呈現表單（顯示錯誤消息） {#problem-unable-to-render-form}

1. 請確定指定的參數正確無誤。 如需參數的詳細資訊，請參閱 [呈現參數](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. 登入CRX封裝管理器(網址為https://)&lt;server>:&lt;port>/crx/packmgr/index.jsp)，並檢查下列套件是否已正確安裝：

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. 登入CQ Web Console(Felix Console)，網址為https://&lt;server>:&lt;port>/system/console/bundles。

   請確定下列套件組合的狀態為「作用中」：

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   * AdobeXFA Forms轉譯器

   (com.adobe.livecycle.adobe-lc-forms-core)

   * AdobeXFA Forms LC連接器

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## 問題：表單轉譯不含樣式 {#problem-form-renders-without-styles}

1. 在瀏覽器中，開啟 **開發人員工具**. 確認profile.css可供使用。
1. 如果profile.css檔案不可用，請登入CRX DE，網址為https://&lt;server>:&lt;port>/crx/de。
1. 在左側的資料夾階層中，導覽至/etc/clientlibs/fd/xfaforms/。 開啟資料夾中列出的css.txt檔案。

   * 側面像
   * 執行階段
   * 滾動導覽
   * 工具列
   * xfalib

1. 確認css.txt內提及的檔案存在於CRX DE lite中，網址為/libs/fd/xfaforms/clientlibs/xfalib/css。

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. 如果上述檔案不可用，請安裝adobe-lc-forms-runtime-pkg-&lt;version>.zip套件。

### 問題：遇到意外錯誤 {#problem-unexpected-error-encountered}

1. 在表單URL中，新增查詢參數debugClientLibs並將其值設為true(例如：https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path=&quot;&quot;>&amp;template=&lt;name of=&quot;&quot; xdp=&quot;&quot; file=&quot;&quot;>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. 在案頭瀏覽器（例如chrome）中，前往開發人員工具 — >主控台。
1. 開啟記錄檔以識別錯誤類型。 如需記錄檔的詳細資訊，請參閱 [HTML5表單記錄](/help/forms/using/enable-logs.md).
1. 前往開發人員工具 — >主控台。 使用堆疊追蹤來找出造成錯誤的程式碼。 對錯誤進行偵錯以解決問題。

   >[!NOTE]
   >
   >如果指令碼失敗，請檢查表單的PDF轉譯期間是否也出現相同問題。 如果是，則表單指令碼邏輯出現問題。

## 問題：無法提交表單 {#problem-unable-to-submit-the-form}

1. 請確定您擁有存取AEM伺服器的權限，且已連線至伺服器。
1. 檢查參數submitUrl是否正確。
1. 啟用用戶端記錄，如 [HTML5表單記錄](/help/forms/using/enable-logs.md) 使用偵錯選項作為 **1-a5-b5-c5**. 然後呈現表單並按一下提交。 開啟瀏覽器偵錯主控台，並檢查是否有錯誤。
1. 如下所述，找到伺服器記錄 [HTML5表單記錄](/help/forms/using/enable-logs.md). 檢查提交期間伺服器記錄中是否有任何錯誤。

## 問題：本地化錯誤訊息未顯示 {#problem-localized-error-messages-do-not-display}

1. 使用其他查詢參數呈現表單 **debugClientLibs=true** 在案頭瀏覽器中，然後前往「開發人員工具 — >資源」並檢查檔案I18N.css。
1. 如果檔案無法使用，請前往https://登入CRX DE&lt;server>:&lt;port>/crx/de。
1. 在左側的資料夾階層中，導覽至/libs/fd/xfaforms/clientlibs/I18N，並確認下列檔案和資料夾存在：

   * Namespace.js
   * LogMessages.js
   * 語言資料夾

1. 如果上述任何檔案或資料夾不存在，請安裝 **adobe-lc-forms-runtime-pkg-&lt;version>.zip** 封裝。
1. 導航到與區域設定名稱同名的資料夾並檢查其內容。 資料夾必須包含下列檔案：

   * I18N.js
   * js.txt

1. 檢查js.txt的內容，並確認其包含下列項目。

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 問題：影像未顯示 {#problem-image-not-showing-up}

1. 請確定影像URL正確。
1. 檢查您的瀏覽器是否支援此類型的影像。
1. 在例外詳細資訊中，搜索單詞 **由**.

   可能是因為URL中的一或多個參數不正確。

   檢查下列參數：步驟文字

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>範本</td>
   <td>範本的檔案名稱</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>範本和相關資源所在的路徑</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>與範本合併之資料檔案的絕對路徑。<br /> 注意：路徑定義資料檔案的絕對路徑。</td>
  </tr>
  <tr>
   <td>資料</td>
   <td>與範本合併的UTF-8編碼資料位元組。</td>
  </tr>
 </tbody>
</table>

1. 在案頭瀏覽器中，前往開發人員工具 — >資源。

   如果顯示影像，請在「幀」的左側檢查。
