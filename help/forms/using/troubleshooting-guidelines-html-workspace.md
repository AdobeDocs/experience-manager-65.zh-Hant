---
title: AEM Forms工作區疑難排解准則
seo-title: Troubleshooting guidelines for AEM Forms workspace
description: 啟用記錄檔，並在瀏覽器中使用除錯工具來疑難排解AEM Forms工作區。
seo-description: Enable logs and use debugger in browser to troubleshoot AEM Forms workspace.
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# AEM Forms工作區疑難排解准則 {#troubleshooting-guidelines-for-aem-forms-workspace}

本文探討如何在瀏覽器中啟用記錄和使用除錯工具來除錯AEM Forms工作區。 此外也說明使用AEM Forms工作區時可能遇到的一些常見問題及解決方法。

## 無法安裝AEM Forms工作區套件 {#unable-to-install-aem-forms-workspace-package}

安裝修補程式後，開啟AEM Forms工作區。 如果您遇到「找不到資源」錯誤，請開啟CRX Package Manager，然後重新安裝 `adobe-lc-workspace-pkg-<version>.zip` 包。

安裝套件時，如果您遇到錯誤 `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`，請執行下列步驟：

1. 登入CRX DE lite。 預設URL為 `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. 刪除以下節點：

   `/home/groups/P/PERM_WORKSPACE_USER`

1. 前往封裝管理器。 預設URL為 `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. 搜尋並安裝 `adobe-lc-workspace-pkg-[version].zip` 包。
1. 重新啟動應用程式伺服器。

## AEM Forms workspace記錄 {#aem-forms-workspace-nbsp-logging}

您可以在不同層級產生記錄，以最佳化錯誤疑難排解。 例如，在複雜的應用程式中，在元件層級記錄有助於偵錯特定元件並疑難排解。

在AEM Forms工作區中：

* 若要取得特定元件檔案的記錄資訊，請附加 `/log/<ComponentFile>/<LogLevel>` 在URL中，然後按 `Enter`. 指定日誌級別的元件檔案的所有日誌資訊都會打印在控制台上。

* 要獲取所有元件檔案的日誌資訊，請附加 `/log/all/trace` 在URL中，然後按 `Enter`.

* 日誌格式： `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>預設情況下，所有元件的日誌級別均設為「資訊」。

* 使用者設定的記錄層級只會針對該瀏覽器工作階段進行維護。 使用者重新整理頁面時，所有元件的記錄層級都會設為其初始值。

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
   <td><p>outofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outofficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>preferencesView</p> </td>
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

* **在IE中除錯**:若要在IE中偵錯AEM Forms工作區，請參閱： [https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx).

* **Chrome中的除錯**:若要在Chrome中開啟偵錯工具，請使用快速鍵：Ctrl+Shift+I。如需詳細資訊，請參閱： [https://developer.chrome.com/extensions/tut_debugging.html](https://developer.chrome.com/extensions/tut_debugging.html).

* **在Firefox中除錯**:Firefox中有數個附加元件可用來偵錯指令碼和樣式。 例如，Firebug是這類偵錯公用程式([https://getfirebug.com](https://getfirebug.com))。

## 常見問題集 {#faqs}

1. PDF表單無法在Google Chrome中轉譯或提交。

   1. 安裝Adobe®Reader®外掛程式。
   1. 在Chrome中，開啟chrome://plugins以檢視可用的外掛程式。
   1. 停用ChromePDF檢視器外掛程式，並啟用Adobe Reader外掛程式。

1. SWF表單或指南未在Google Chrome中轉譯。

   1. 在Chrome中，開啟chrome://plugins以檢視可用的外掛程式。
   1. 請參閱AdobeFlash® Player外掛程式的詳細資訊。
   1. 在「AdobeFlash Player」外掛程式下停用PepperFlash。

1. 我已自訂AEM Forms工作區，但看不到變更。

   清除瀏覽器的快取，然後存取AEM Forms工作區。

1. 當使用者在案頭中開啟表單時，需要執行哪些HTML?

   使用Workbench時，在指派任務步驟中為預設配置檔案選擇HTML單選按鈕。

1. 按一下後附件沒有顯示。

   若要檢視附件，請啟用瀏覽器中的快顯視窗。

1. 使用者已登入表單應用程式。 如果使用者嘗試登入工作區，如果使用者沒有工作區權限，則可能無法載入。

   從其他表單應用程式登出，然後登入工作區。

1. HTML表單時，在其設計中使用「處理屬性」，在AEM Forms工作區中呈現時，表單內會顯示「提交」按鈕。

   在設計表單時，使用「處理屬性」時，表單內會新增「提交」按鈕。 在AEM Forms工作區中以PDF呈現時，一般使用者看不到「提交」按鈕。 不過，在AEM Forms工作區中以HTML表單呈現時，一般使用者會看到「提交」按鈕。 在表單內按一下此「提交」按鈕時不會起始任何動作。 在表單外按一下AEM Forms工作區底部的「提交」按鈕，即可完成工作。
