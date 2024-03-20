---
title: AEM Forms工作區的疑難排解准則
description: 啟用記錄並在瀏覽器中使用偵錯工具，針對AEM Forms工作區進行疑難排解。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---

# AEM Forms工作區的疑難排解准則 {#troubleshooting-guidelines-for-aem-forms-workspace}

本文會討論如何透過啟用記錄功能和使用瀏覽器中的除錯程式，來除錯AEM Forms工作區。 本檔案也會說明您在使用AEM Forms工作區時可能會遇到的一些常見問題及其因應措施。

## 無法安裝AEM Forms工作區套件 {#unable-to-install-aem-forms-workspace-package}

安裝修補程式後，請開啟AEM Forms工作區。 如果您遇到「找不到資源」錯誤，請開啟CRX封裝管理員，然後重新安裝 `adobe-lc-workspace-pkg-<version>.zip` 封裝。

安裝套件時，如果發生錯誤 `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`，請執行下列步驟：

1. 登入CRXDE Lite。 預設URL為 `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. 刪除下列節點：

   `/home/groups/P/PERM_WORKSPACE_USER`

1. 前往「封裝管理員」。 預設URL為 `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. 搜尋並安裝 `adobe-lc-workspace-pkg-[version].zip` 封裝。
1. 重新啟動應用程式伺服器。

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

## AEM Forms工作區記錄 {#aem-forms-workspace-nbsp-logging}

您可以產生不同層級的記錄，以最佳化錯誤的疑難排解。 例如，在複雜應用程式中，在元件層級記錄有助於對特定元件進行偵錯和疑難排解。

在AEM Forms工作區中：

* 若要取得特定元件檔案的記錄資訊，請附加 `/log/<ComponentFile>/<LogLevel>` 在URL中，然後按 `Enter`. 指定記錄層級之元件檔案的所有記錄資訊都會列印在主控台上。

* 若要取得所有元件檔案的記錄資訊，請附加 `/log/all/trace` 在URL中，然後按 `Enter`.

* 記錄格式： `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>依預設，所有元件的記錄層級都設為INFO。

* 使用者設定的記錄層級只會針對該瀏覽器作業階段進行維護。 當使用者重新整理頁面時，所有元件的記錄層級都會設定為其初始值。

### AEM Forms工作區中的元件檔案清單 {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>工作清單模型</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>tasklistView</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>任務模型</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>任務檢視</p> </td>
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
   <td><p>categoryview</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>sharequeuemodel</p> </td>
   <td><p>uissettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>共用檢視</p> </td>
   <td><p>uissettingsView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>使用者資訊模型</p> </td>
  </tr>
  <tr>
   <td><p>辦公室模型</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outofficeView</p> </td>
   <td><p>起點模型</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>偏好設定檢視</p> </td>
   <td><p>起點</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>伺服器模型</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>伺服器檢視</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>任務詳細資料檢視</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### AEM Forms工作區中可用的記錄層級 {#log-levels-available-in-nbsp-aem-forms-workspace}

* 致命
* 錯誤
* 警告
* 資訊
* 偵錯
* TRACE
* 關閉

## 瀏覽器除錯資訊 {#debugging-information-for-browsers}

指令碼和樣式可以在不同的瀏覽器中偵錯。

* **在IE中進行偵錯**：若要在IE中偵錯AEM Forms工作區，請參閱： [https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie](https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie).

* **在Chrome中除錯**：若要在Chrome中開啟Debugger，請使用捷徑：Ctrl+Shift+I。如需詳細資訊，請參閱： [https://developer.chrome.com/docs/extensions/mv3/tut_debugging/](https://developer.chrome.com/docs/extensions/mv3/tut_debugging/).

* **在Firefox中進行偵錯**：數個附加元件可用於在Firefox中除錯指令碼和樣式。 例如，Firebug就是這類偵錯公用程式([https://getfirebug.com](https://getfirebug.com))。

## 常見問題 {#faqs}

1. Google Chrome未轉譯或提交PDF表單。

   1. 安裝Adobe®Reader®外掛程式。
   1. 在Chrome中開啟chrome://plugins ，檢視可用的外掛程式。
   1. 停用ChromePDF檢視器外掛程式，並啟用Adobe Reader外掛程式。

1. Google Chrome中未轉譯SWF表單或指南。

   1. 在Chrome中開啟chrome://plugins ，檢視可用的外掛程式。
   1. 如需AdobeFlash®播放器外掛程式的詳細資訊，請參閱。
   1. 停用AdobeFlash Player外掛程式下的PepperFlash。

1. 我已自訂AEM Forms工作區，但看不到變更。

   清除瀏覽器的快取，然後存取AEM Forms工作區。

1. 使用者在案頭開啟表單時，需要採取哪些動作才能以HTML呈現表單？

   使用Workbench時，在指派工作步驟中，選取預設設定檔的「HTML」選項按鈕。

1. 按一下時附件未顯示。

   若要檢視附件，請在瀏覽器中啟用快顯視窗。

1. 使用者已登入表單應用程式。 如果使用者嘗試登入工作區，則可能無法載入（如果使用者沒有工作區許可權）。

   從其他表單應用程式登出，然後登入工作區。

1. HTML表單，在其設計中使用流程屬性，在AEM Forms工作區中呈現時，在表單內顯示提交按鈕。

   設計表單時，當您使用流程屬性時，它會在表單內新增提交按鈕。 在AEM Forms工作區中呈現為PDF時，一般使用者看不到提交按鈕。 不過，在AEM Forms工作區中以HTML表單形式呈現時，一般使用者可看到「提交」按鈕。 按一下表單內的此提交按鈕不會起始任何動作。 按一下AEM Forms工作區底部的「提交」按鈕（在表單外）即可完成工作。
