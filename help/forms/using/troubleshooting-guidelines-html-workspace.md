---
title: AEM Forms工作區疑難排解指引
seo-title: AEM Forms工作區疑難排解指引
description: 啟用記錄並使用瀏覽器中的除錯程式來疑難排解AEM Forms工作區。
seo-description: 啟用記錄並使用瀏覽器中的除錯程式來疑難排解AEM Forms工作區。
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Forms工作區疑難排解指引 {#troubleshooting-guidelines-for-aem-forms-workspace}

本文討論如何透過啟用記錄以及在瀏覽器中使用除錯程式來除錯AEM Forms工作區。 此外，它也說明使用AEM Forms工作區時可能會遇到的一些常見問題及解決方法。

## 無法安裝AEM Forms工作區套件 {#unable-to-install-aem-forms-workspace-package}

安裝修補程式後，請開啟AEM Forms工作區。 如果遇到「找不到資源」錯誤，請開啟CRX包管理器並重新安裝包 `adobe-lc-workspace-pkg-<version>.zip` 。

在安裝軟體包時，如果遇到錯誤， `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`請執行以下步驟：

1. 登入CRX DE lite。 預設URL為 `https://[localhost]:[port]/lc/crx/de/index.jsp`
1. 刪除以下節點：

   `/home/groups/P/PERM_WORKSPACE_USER`

1. 轉至「包管理器」。 預設URL為 `https://[localhost]:[port]/lc/crx/packmgr/index.jsp.`
1. 搜尋並安裝套 `adobe-lc-workspace-pkg-[version].zip` 件。
1. 重新啟動應用程式伺服器。

## AEM Forms工作區記錄 {#aem-forms-workspace-nbsp-logging}

您可以在不同層級產生記錄檔，以最佳化錯誤疑難排解。 例如，在複雜的應用程式中，在元件層級登入有助於除錯和疑難排解特定元件。

在AEM Forms工作區中：

* 若要取得特定元件檔案的記錄資訊，請在URL `/log/<ComponentFile>/<LogLevel>` 中附加，然後按 `Enter`。 在指定日誌級別上，元件檔案的所有日誌資訊都打印在控制台上。

* 若要取得所有元件檔案的記錄資訊，請 `/log/all/trace` 在URL中附加，然後按 `Enter`。

* 日誌格式： `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>預設情況下，所有元件的日誌級別都設定為INFO。

* 用戶設定的日誌級別僅用於該瀏覽器會話。 當使用者重新整理頁面時，所有元件的記錄層級都會設為其初始值。

### AEM Forms工作區中的元件檔案清單 {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>tasklistModel</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>tasklistView</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>taskModel</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>taskView</p> </td>
  </tr>
  <tr>
   <td><p>categorylistView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueuesView</p> </td>
  </tr>
  <tr>
   <td><p>categoryModel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>sharequeueModel</p> </td>
   <td><p>uisettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>sharequeueView</p> </td>
   <td><p>uisettingsView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>首選項視圖</p> </td>
   <td><p>startpointView</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserrorModel</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>wserrorView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>taskdetailsView</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### AEM Forms工作區中可用的記錄層級 {#log-levels-available-in-nbsp-aem-forms-workspace}

* 致命
* 錯誤
* 警告
* 資訊
* 除錯
* TRACE
* 關閉

## 瀏覽器的除錯資訊 {#debugging-information-for-browsers}

指令碼和樣式可在不同的瀏覽器中除錯。

* **在IE中除錯**:若要在IE中除錯AEM Forms工作區，請參閱： [https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx)。

* **在Chrome中除錯**:若要在Chrome中開啟除錯程式，請使用捷徑：Ctrl+Shift+I。如需詳細資訊，請參閱： [https://developer.chrome.com/extensions/tut_debugging.html](https://developer.chrome.com/extensions/tut_debugging.html)。

* **在Firefox中除錯**:Firefox中有數個可用來除錯指令碼和樣式的附加元件。 例如，Firebug是這類除錯公用程式([https://getfirebug.com](https://getfirebug.com))。

## 常見問答集 {#faqs}

1. PDF表格不會在Google Chrome中轉譯或提交。

   1. 安裝Adobe® Reader®增效模組。
   1. 在Chrome中，開啟chrome://plugins以檢視可用的增效模組。
   1. 停用Chrome PDF Viewer外掛程式，並啟用Adobe Reader外掛程式。

1. SWF表格或指南未在Google Chrome中轉譯。

   1. 在Chrome中，開啟chrome://plugins以檢視可用的增效模組。
   1. 請參閱Adobe Flash® Player增效模組的詳細資訊。
   1. 在Adobe Flash Player增效模組下停用PepperFlash。

1. 我已自訂AEM Forms工作區，但無法看到變更。

   清除瀏覽器的快取，然後存取AEM Forms工作區。

1. 使用者在案頭中開啟表單時，需要執行哪些動作才能在HTML中轉譯表單？

   使用「工作台」時，在分配任務步驟中為預設配置檔案選擇「HTML」單選按鈕。

1. 點按時不會顯示附件。

   若要檢視附件，請在瀏覽器中啟用快顯視窗。

1. 用戶已登錄到表單應用程式。 如果使用者嘗試登入工作區，當使用者沒有工作區權限時，可能不會載入。

   從其他表單應用程式登出，然後登入工作區。

1. 在AEM Forms工作區中轉譯時，使用「流程屬性」在其設計中的HTML表單，會在表單中顯示「提交」按鈕。

   在設計表單時，當您使用「流程屬性」時，會在表單中新增「提交」按鈕。 當在AEM Forms工作區中轉譯為PDF時，一般使用者看不到「提交」按鈕。 不過，當在AEM Forms工作區中以HTML表格呈現時，一般使用者會看到「提交」按鈕。 在表單內按一下此「提交」按鈕不會啟動任何動作。 按一下AEM Forms工作區底部的「送出」按鈕（在表單外部），即可完成工作。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
