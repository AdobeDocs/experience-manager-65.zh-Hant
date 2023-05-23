---
title: AEM Forms工作區故障排除指南
seo-title: Troubleshooting guidelines for AEM Forms workspace
description: 啟用日誌並在瀏覽器中使用調試器來排除AEM Forms工作區故障。
seo-description: Enable logs and use debugger in browser to troubleshoot AEM Forms workspace.
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
source-git-commit: d3923e5e693e7426ee57e81e203f31964a23af3a
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---

# AEM Forms工作區故障排除指南 {#troubleshooting-guidelines-for-aem-forms-workspace}

本文討論如何通過啟用日誌記錄和在瀏覽器中使用調試器來調試AEM Forms工作區。 它還解釋了使用AEM Forms工作區時可能遇到的一些常見問題及其解決方法。

## 無法安裝AEM Forms工作區包 {#unable-to-install-aem-forms-workspace-package}

安裝修補程式後，開啟AEM Forms工作區。 如果遇到「找不到資源」錯誤，請開啟CRX包管理器並重新安裝 `adobe-lc-workspace-pkg-<version>.zip` 檔案。

安裝包時，如果遇到錯誤 `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`，請執行以下步驟：

1. 登錄到CRXDE Lite。 預設URL為 `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. 刪除以下節點：

   `/home/groups/P/PERM_WORKSPACE_USER`

1. 轉到包管理器。 預設URL為 `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. 搜索並安裝 `adobe-lc-workspace-pkg-[version].zip` 檔案。
1. 重新啟動應用程式伺服器。

## AEM Forms工作區日誌 {#aem-forms-workspace-nbsp-logging}

您可以在不同級別生成日誌，以便對錯誤進行最佳故障排除。 例如，在複雜的應用程式中，在元件級別登錄有助於調試和排除特定元件的故障。

在AEM Forms工作區中：

* 要獲取有關特定元件檔案的日誌記錄資訊，請追加 `/log/<ComponentFile>/<LogLevel>` ，然後按 `Enter`。 在控制台上打印指定日誌級別的元件檔案的所有日誌資訊。

* 要獲取所有元件檔案的日誌記錄資訊，請追加 `/log/all/trace` ，然後按 `Enter`。

* 日誌格式： `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>預設情況下，所有元件的日誌級別都設定為INFO。

* 用戶設定的日誌級別僅用於該瀏覽器會話。 當用戶刷新頁面時，日誌級別將設定為所有元件的初始值。

### AEM Forms工作區中的元件檔案清單 {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategory模型</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>任務清單模型</p> </td>
  </tr>
  <tr>
   <td><p>appnavigation模型</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>任務清單視圖</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>進程名清單模型</p> </td>
   <td><p>任務模型</p> </td>
  </tr>
  <tr>
   <td><p>類別清單模型</p> </td>
   <td><p>進程名清單視圖</p> </td>
   <td><p>任務視圖</p> </td>
  </tr>
  <tr>
   <td><p>類別清單視圖</p> </td>
   <td><p>processname模型</p> </td>
   <td><p>teamqueuesView</p> </td>
  </tr>
  <tr>
   <td><p>類別模型</p> </td>
   <td><p>進程名稱視圖</p> </td>
   <td><p>todo視圖</p> </td>
  </tr>
  <tr>
   <td><p>類別視圖</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>跟蹤視圖</p> </td>
  </tr>
  <tr>
   <td><p>收藏夾類別模型</p> </td>
   <td><p>共用隊列模型</p> </td>
   <td><p>uisetings模型</p> </td>
  </tr>
  <tr>
   <td><p>過濾器清單視圖</p> </td>
   <td><p>共用隊列視圖</p> </td>
   <td><p>統計視圖</p> </td>
  </tr>
  <tr>
   <td><p>篩選器視圖</p> </td>
   <td><p>起始點清單模型</p> </td>
   <td><p>用戶資訊模型</p> </td>
  </tr>
  <tr>
   <td><p>烏托福菲斯模型</p> </td>
   <td><p>起始點清單視圖</p> </td>
   <td><p>用戶資訊視圖</p> </td>
  </tr>
  <tr>
   <td><p>烏托福菲切視圖</p> </td>
   <td><p>起始點模型</p> </td>
   <td><p>用戶搜索模型</p> </td>
  </tr>
  <tr>
   <td><p>首選項視圖</p> </td>
   <td><p>起始點視圖</p> </td>
   <td><p>用戶搜索視圖</p> </td>
  </tr>
  <tr>
   <td><p>進程實例歷史記錄視圖</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserror模型</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>wserror視圖</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>taskdetails查看</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### 可在AEM Forms工作區中使用的日誌級別 {#log-levels-available-in-nbsp-aem-forms-workspace}

* 致命
* 錯誤
* 警告
* 資訊
* 調試
* TRACE
* 關閉

## 瀏覽器的調試資訊 {#debugging-information-for-browsers}

指令碼和樣式可以在不同的瀏覽器中調試。

* **在IE中調試**:要在IE中調試AEM Forms工作區，請參閱： [https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie](https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie)。

* **在Chrome中調試**:要在Chrome中開啟調試器，請使用快捷方式：按Ctrl+Shift+I。有關詳細資訊，請參閱： [https://developer.chrome.com/docs/extensions/mv3/tut_debugging/](https://developer.chrome.com/docs/extensions/mv3/tut_debugging/)。

* **在Firefox中調試**:幾個載入項可用於調試Firefox中的指令碼和樣式。 例如，Firebug是此類調試實用程式([https://getfirebug.com](https://getfirebug.com))。

## 常見問題 {#faqs}

1. PDF表單未在GoogleChrome中呈現或提交。

   1. 安裝Adobe®Reader®插件。
   1. 在Chrome中，開啟chrome://plugins以查看可用插件。
   1. 禁用ChromePDF查看器插件並啟用Adobe Reader插件。

1. SWF表單或指南未在GoogleChrome中呈現。

   1. 在Chrome中，開啟chrome://plugins以查看可用插件。
   1. 有關AdobeFlash®播放器插件的詳細資訊。
   1. 在AdobeFlash Player插件下禁用PepperFlash。

1. 我已自定義了AEM Forms工作區，但無法看到更改。

   清除瀏覽器的快取，然後訪問AEM Forms工作區。

1. 當在案頭中開啟表單時，用戶需要執行什麼操作才能以HTML方式呈現表單？

   在使用Workbench時，在分配任務步驟中為預設配置檔案選擇HTML單選按鈕。

1. 按一下時未顯示附件。

   要查看附件，請在瀏覽器中啟用彈出窗口。

1. 用戶已登錄到表單應用程式。 如果用戶嘗試登錄到工作區，則如果用戶沒有工作區權限，則可能不會載入。

   從其他表單應用程式註銷，然後登錄到工作區。

1. HTML表單，在其設計中使用「流程屬性」，在AEM Forms工作區中呈現時，在表單內顯示「提交」按鈕。

   設計表單時，使用「流程屬性」時，它會在表單內添加「提交」按鈕。 在AEM Forms工作區中呈現為PDF時，最終用戶不能看到「提交」按鈕。 但是，在AEM Forms工作區中呈現為HTML表單時，最終用戶可以看到「提交」按鈕。 在表單內按一下此「提交」按鈕不會啟動任何操作。 按一下AEM Forms工作區底部表單外的「提交」按鈕可完成任務。
