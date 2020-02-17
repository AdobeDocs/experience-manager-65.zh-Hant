---
title: 除錯HTML5表格
seo-title: 除錯HTML5表格
description: 文檔清單中列出各種已知問題的故障排除步驟。
seo-description: 文檔清單中列出各種已知問題的故障排除步驟。
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 除錯HTML5表格 {#debugging-html-forms}

本檔案包含數個疑難排解案例。 對於每種情況，都提供一些步驟來排除問題。 請依照這些步驟進行，如果問題仍然存在，請設定記錄程式以取得並檢視錯誤／警告的記錄檔。 如需HTML5表單記錄的詳細資訊，請參閱「 [產生HTML5表單的記錄檔」](/help/forms/using/enable-logs.md)。

## 問題：在轉譯表單時，我會看到org.apache.sling.api.SlingException頁面 {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

在例外詳細資訊中，搜索由 **引起的詞**。

可能的原因是URL中的一或多個參數不正確。

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
   <td>模板和相關資源所在的路徑</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>與模板合併的資料檔案的絕對路徑。<br /> 注意：路徑定義資料檔案的絕對路徑。</td>
  </tr>
  <tr>
   <td>資料</td>
   <td>與範本合併的UTF-8編碼資料位元組。</td>
  </tr>
 </tbody>
</table>

## 問題：無法呈現表單（顯示錯誤訊息） {#problem-unable-to-render-a-form-an-error-message-is-displayed}

1. 請確定指定的參數正確無誤。 有關參數的詳細資訊，請參 [閱Render Parameters](/help/forms/using/debug.md#main-pars-table)。
1. 登錄到CRX軟體包管理器(位於https://&lt;server>:&lt;port>/crx/packmgr/index.jsp)並檢查以下軟體包是否正確安裝：

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. 登入CQ Web Console(Felix Console)，網址為https://&lt;server>:&lt;port>/system/console/bundles。

   確保以下捆綁包的狀態為「活動」:

   * scala-lang.bundle [osgi]
   (com.adobe.livecyclescala-lang.bundle)

   * Adobe XFA Forms Renderer
   (com.adobe.livecycle.adobe-lc-forms-core)

   * Adobe XFA Forms LC連接器
   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## 問題：無樣式的表單轉換 {#problem-form-renders-without-styles}

1. 在您的瀏覽器中，開啟「開 **發人員工具」**。 請確定profile.css是可用的。
1. 如果profile.css檔案不可用，請登入https://&lt;server>:&lt;port>/crx/de的CRX DE。
1. 在左側的資料夾層次中，導航至/etc/clientlibs/fd/xfaforms/。 開啟資料夾中所列的css.txt檔案。

   * 側面像
   * 執行時期
   * scrollnav
   * 工具欄
   * xfalib

1. 驗證css.txt中提及的檔案是否存在於CRX DE lite中，網址為/libs/fd/xfaforms/clientlibs/xfalib/css。

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. 如果上述檔案不可用，請重新安裝adobe-lc-forms-runtime-pkg-&lt;version>.zip套件。

### 問題：遇到意外錯誤 {#problem-unexpected-error-encountered}

1. 在表單URL中，新增查詢參數debugClientLibs，並將其值設為true(例如：https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path>&amp;template=&lt;xdp檔案名稱>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. 在案頭瀏覽器（例如chrome）中，前往「開發人員工具->主控台」。
1. 開啟記錄檔以識別錯誤類型。 如需記錄檔的詳細資訊，請參 [閱HTML5表格的記錄檔](/help/forms/using/enable-logs.md)。
1. 前往「開發人員工具->主控台」。 使用堆疊追蹤來找出造成錯誤的程式碼。 除錯錯誤以解決問題。

   >[!NOTE]
   >
   >如果指令碼執行失敗，請檢查在表單的PDF轉譯期間是否也發生相同的問題。 如果是，表單指令碼邏輯中會發生問題。

## 問題：無法提交表單 {#problem-unable-to-submit-the-form}

1. 請確定您擁有存取AEM伺服器的權限，而且您已連線至伺服器。
1. 檢查參數submitUrl是否正確。
1. 使用除錯選項( [1-a5-b5-c5)，啟用HTML5表單的記錄檔](/help/forms/using/enable-logs.md) ( **Logs)中所述的用戶端記錄檔**。 然後演算表格，然後按一下「送出」。 開啟瀏覽器除錯主控台，並檢查是否有錯誤。
1. 如HTML5表單的記錄檔中 [所述，尋找伺服器記錄檔](/help/forms/using/enable-logs.md)。 檢查提交期間伺服器日誌中是否有任何錯誤。

## 問題：不顯示本地化的錯誤訊息 {#problem-localized-error-messages-do-not-display}

1. 在案頭瀏覽器中使用其他查詢參 **數debugClientLibs=true** ，然後前往「開發人員工具->資源」並檢查檔案I18N.css。
1. 如果檔案不可用，請登錄CRX DE，網址為https://&lt;server>:&lt;port>/crx/de。
1. 在左側的檔案夾階層中，導覽至/libs/fd/xfaforms/clientlibs/I18N，並確保有下列檔案和檔案夾：

   * Namespace.js
   * LogMessages.js
   * 語言資料夾

1. 如果上述任何檔案或資料夾不存在，請重新安裝 **adobe-lc-forms-runtime-pkg-&lt;version>.zip** 套件。
1. 導航到與區域設定名稱同名的資料夾並檢查其內容。 資料夾必須包含以下檔案：

   * I18N.js
   * js.txt

1. 檢查js.txt的內容，並確定它包含下列項目。

   ```
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 問題：未顯示影像 {#problem-image-not-showing-up}

1. 請確定影像URL正確。
1. 檢查您的瀏覽器是否支援此類影像。
1. 在例外詳細資訊中，搜索由 **引起的詞**。

   可能的原因是URL中的一或多個參數不正確。

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
   <td>模板和相關資源所在的路徑</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>與模板合併的資料檔案的絕對路徑。<br /> 注意：路徑定義資料檔案的絕對路徑。</td>
  </tr>
  <tr>
   <td>資料</td>
   <td>與範本合併的UTF-8編碼資料位元組。</td>
  </tr>
 </tbody>
</table>

1. 在案頭瀏覽器中，前往「開發人員工具->資源」。

   如果顯示影像，請在「影格」的左側檢查。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
