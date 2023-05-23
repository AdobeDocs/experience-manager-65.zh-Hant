---
title: 調試HTML5窗體
seo-title: Debugging HTML5 forms
description: 文檔清單中用於排除各種已知問題的步驟。
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

# 調試HTML5窗體 {#debugging-html-forms}

本文檔包括幾種故障排除方案。 對於每種情況，都提供了一些步驟來解決問題。 按照這些步驟操作，如果問題仍然存在，請配置記錄器以獲取並查看日誌中的錯誤/警告。 有關HTML5表單日誌記錄的詳細資訊，請參見 [為HTML5表單生成日誌](/help/forms/using/enable-logs.md)。

## 問題：在呈現表單時，我會看到org.apache.sling.api.SlingException異常頁 {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

在異常詳細資訊中，搜索單詞 **由**。

可能的原因是URL中的一個或多個參數不正確。

檢查以下參數：

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>範本</td>
   <td>模板的檔案名</td>
  </tr>
  <tr>
   <td>內容根</td>
   <td>模板和關聯資源所在的路徑</td>
  </tr>
  <tr>
   <td>資料引用</td>
   <td>與模板合併的資料檔案的絕對路徑。<br /> 注：路徑定義資料檔案的絕對路徑。</td>
  </tr>
  <tr>
   <td>資料</td>
   <td>與模板合併的UTF-8編碼資料位元組。</td>
  </tr>
 </tbody>
</table>

## 問題：無法呈現表單（顯示錯誤消息） {#problem-unable-to-render-form}

1. 確保指定的參數正確。 有關參數的詳細資訊，請參見 [渲染參數](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page)。
1. 登錄到CRX包管理器(https://)&lt;server>:&lt;port>/crx/packmgr/index.jsp)並檢查以下軟體包是否正確安裝：

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. 登錄CQ Web控制台（Felix控制台），網址為https://&lt;server>:&lt;port>/system/console/bundles。

   確保以下捆綁包的狀態為「活動」：

   * scala lang.bundle [四]

   (com.adobe.liveccyclala lang.bundle)

   * AdobeXFAForms渲染器

   (com.adobe.livecycle.adobe-lc-forms-core)

   * AdobeXFAFormsLC連接器

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## 問題：無樣式的窗體渲染 {#problem-form-renders-without-styles}

1. 在瀏覽器中，開啟 **開發人員工具**。 確保profile.css可用。
1. 如果profile.css檔案不可用，請登錄CRX DE，網址為https://&lt;server>:&lt;port>/crx/de。
1. 在左側的資料夾層次結構中，導航到/etc/clientlibs/fd/xfaforms/。 開啟資料夾中列出的css.txt檔案。

   * 側面像
   * 運行時
   * 滾動導航
   * 工具欄
   * xfalib

1. 驗證css.txt中提及的檔案是否在CRX DE lite中存在，地址為/libs/fd/xfaforms/clientlibs/xfalib/css。

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. 如果上述檔案不可用，請安裝adobe-lc-forms-runtime-pkg-&lt;version>.zip包。

### 問題：遇到意外錯誤 {#problem-unexpected-error-encountered}

1. 在表單URL中，添加查詢參數debugClientLibs並將其值設定為true(例如：https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path=&quot;&quot;>&amp;模板=&lt;name of=&quot;&quot; xdp=&quot;&quot; file=&quot;&quot;>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. 在案頭瀏覽器（如chrome）中，轉至「開發人員工具」 — >「控制台」。
1. 開啟日誌以標識錯誤類型。 有關日誌的詳細資訊，請參見 [日誌用於HTML5窗體](/help/forms/using/enable-logs.md)。
1. 轉至「開發人員工具」 — >「控制台」。 使用堆棧跟蹤查找導致錯誤的代碼。 調試錯誤以解決問題。

   >[!NOTE]
   >
   >如果指令碼編寫失敗，請檢查在表單的PDF格式副本期間是否也出現了相同的問題。 如果是，則表單指令碼邏輯中出現問題。

## 問題：無法提交表單 {#problem-unable-to-submit-the-form}

1. 確保您有權訪問服AEM務器，並且已連接到伺服器。
1. 檢查參數submitUrl是否正確。
1. 啟用客戶端日誌（如中所述） [HTML5窗體的日誌](/help/forms/using/enable-logs.md) 使用調試選項 **1-a5-b5-c5**。 然後呈現表單，然後按一下提交。 開啟瀏覽器調試控制台並檢查是否有錯誤。
1. 找到上所述的伺服器日誌 [HTML5窗體的日誌](/help/forms/using/enable-logs.md)。 檢查提交期間伺服器日誌中是否有錯誤。

## 問題：未顯示本地化的錯誤消息 {#problem-localized-error-messages-do-not-display}

1. 使用附加查詢參數呈現窗體 **debugClientLibs=true** 在案頭瀏覽器中，然後轉到「開發人員工具」 — >「資源」並檢查檔案I18N.css。
1. 如果檔案不可用，請登錄CRX DE，網址為https://&lt;server>:&lt;port>/crx/de。
1. 在左側的資料夾層次結構中，導航到/libs/fd/xfaforms/clientlibs/I18N，並確保存在以下檔案和資料夾：

   * Namespace.js
   * LogMessages.js
   * 語言資料夾

1. 如果上述任何檔案或資料夾不存在，請安裝 **adobe-lc-forms-runtime-pkg-&lt;version>.zip** 的子菜單。
1. 導航到與區域設定名稱同名的資料夾並檢查其內容。 資料夾必須包含以下檔案：

   * I18N.js
   * js.txt

1. 檢查js.txt的內容，並確保它具有以下條目。

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 問題：影像未顯示 {#problem-image-not-showing-up}

1. 確保影像URL正確。
1. 檢查您的瀏覽器是否支援此類型的影像。
1. 在異常詳細資訊中，搜索單詞 **由**。

   可能的原因是URL中的一個或多個參數不正確。

   檢查以下參數：步驟文本

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>範本</td>
   <td>模板的檔案名</td>
  </tr>
  <tr>
   <td>內容根</td>
   <td>模板和關聯資源所在的路徑</td>
  </tr>
  <tr>
   <td>資料引用</td>
   <td>與模板合併的資料檔案的絕對路徑。<br /> 注：路徑定義資料檔案的絕對路徑。</td>
  </tr>
  <tr>
   <td>資料</td>
   <td>與模板合併的UTF-8編碼資料位元組。</td>
  </tr>
 </tbody>
</table>

1. 在案頭瀏覽器中，轉至「開發人員工具」 — >「資源」。

   如果顯示該影像，請在「幀」中選中左側。
