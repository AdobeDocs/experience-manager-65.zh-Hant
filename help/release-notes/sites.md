---
title: AEM Sites發行說明
description: Adobe Experience Manager 6.4 Sites的發行說明。
uuid: 676ead61-3d97-4f23-b616-c647d590bc8f
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: f82e9bd4-f7b6-492d-8e02-593e74fa1058
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# AEM Sites發行說明{#aem-sites-release-notes}

如需AEM Sites 6.5增強功能的詳細資訊，請參閱下列內容：

## 元件與範本開發 {#component-amp-template-development}

* Maven Project Archetype 18+，以取得新專案，如需版 [本注意事項，請參閱Github](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases)。
* 針對新專案的單頁App Maven專案原型1.0.6+，如需版本注意事項，請 [參閱Github](https://github.com/adobe/aem-spa-project-archetype/releases)。
* HTL 1.4版，請參閱 [Github以取得發行說明](https://github.com/adobe/htl-spec/releases/tag/1.4)。

   * 字串、陣列和對象的&quot;in&quot;運算子：

      ```
      ${'a' in 'abc’}
       ${100 in myArray}
       ${'a' in myObject}
      ```

   * 具有資料密集的變數聲明：
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 列出和重複控制參數：開始、步驟、結束：
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * 資料破解的標識符：

      ```
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
       text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
       </div>
      ```

   * 支援負數

* 核心元件2.3.2+，請參閱 [Github以取得發行說明](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases)。
* 版面容器的格線系統，請參 [閱Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid)。
* Clientlib管理器：將Google Closure Compiler預設為JavaScript用戶端的精簡化（舊預設為Yahoo UIY），並將Google Closure Compiler更新為v20190121版
* 範本編輯器與原則

   * 針對使用JS SDK的單頁應用程式建立和編輯範本（也稱為SPA編輯器）

* 參考網站We.Retail 4.0，請參閱 [Github以取得發行說明](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)。
* Toolkit to upgrade existing sites to lyperage least editor capabilities, see [Github repository](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM包含jQuery程式庫的1.12.4版，可提供與現有自訂程式碼的最大相容性。 Adobe已針對已知的安全性問題進行修改。

## 網站管理 {#site-administration}

* 「參 [考」](/help/sites-authoring/author-environment-tools.md#references) (Reference)邊欄有新區段，可列出指向所選頁面的內部連結。 當計畫讓頁面離線或刪除時，這很有用——查看哪些頁面需要在離線前進行調整。
* 清 [單檢視](/help/sites-authoring/basic-handling.md#list-view) ，有新的工作流程欄，可顯示頁面目前在工作流程中的狀態。
* 在頁面 [屬性中](/help/sites-authoring/editing-page-properties.md)，現在可在指派縮圖至頁面（縮表徵圖簽）時瀏覽現有資產。

## 頁面編輯器 {#page-editor}

* 使用運用JS SDK（也稱為SPA編輯器）的React和Angular用戶端元件，讓您在內容中編輯和組合單頁應用程式體驗
* 只有當頁面已設定支架頁面時，才會顯示支架模式。

## 內容片段與編輯器 {#content-fragments-amp-editor}

* 內容 [片段編輯器中](/help/assets/content-fragments-variations.md#viewing-editing-deleting-annotations) 「新註解」邊欄，以在文字中加上一般註解並檢視註解（也會顯示在時間軸邊欄中）
* 可將「內容片段」模型中多行文字元素的預設內容類型設為簡單文字 [](/help/assets/content-fragments-models.md) 、豐富式文字或標籤文字
* 通過 [在RTE（全屏視圖）中選擇文本](/help/assets/content-fragments-variations.md#annotating-a-content-fragment) ，添加註釋／注釋
* [透過參考邊欄](/help/assets/content-fragments-managing.md#comparing-fragment-versions) ，並排比較內容片段的版本
* 「資產下載報表」現在會相應顯示內容片段
* 透過 [/api.json將內容片段支援新增至Assets HTTP API](/help/assets/assets-api-content-fragments.md) 。 有建立、更新、讀取和刪除內容片段的API。

## 體驗片段 {#experience-fragments}

* 改進「體驗 [片段」的索引](/help/sites-authoring/experience-fragments.md)，以便在搜尋使用它們的頁面時找到其內容
* 「匯 [出至目標](/help/sites-administering/experience-fragments-target.md) 」選項現在允許將體驗片段傳送為JSON（預設為HTML），或兩者

## 轉換 {#translation}

* 使用專案主管簡化翻譯專案的製作
* 通過預設將翻譯作業設定為批准狀態簡化執行翻譯項目
* 允許使用第三方翻譯記憶庫中的更改來更新翻譯的頁面
* 允許以JSON格式導出翻譯作業
* 更新Microsoft Translation整合以使用V3 API

## 多網站管理(MSM) {#multi-site-management-msm}

* 對於使用PushOnModify的推出設定，請更妥善處理頁面移動作業，以避免狀態不一致
* 現在，依預設，在livecopy結構中建立新頁面時，將會建立獨立頁面
* 在使用JS SDK的單頁應用程式中使用MSM功能（也稱為SPA編輯器）

## 啟動 {#launches}

* 新的啟動審核和核准工作流程，並僅能提升已核准的啟動頁面
* 在UI [中新增選項，以選擇在促銷步驟後立即刪除啟動](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

## 內容定位與模擬 {#content-targeting-simulation}

* ContextHub資料層和用戶端規則引擎JavaScript已依預設更新為使用jQuery 3。

## AEM和Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>AEM在AEM 6.5發行時不支援at.js 2.x。 請使用最新版本的at.js 1.x

* Adobe target整合現在可以使用Target Standard API。 舊版AEM使用Target Classic HTTP API，現已過時。
* 隨附Adobe Target `mbox.js` 63版。 Adobe強烈建議將實作切 `at.js` 換為v1.x。
* `at.js` 現在已包含1.5.0版。 Adobe建議您使 [用Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) , `at.js` 將v1.x布建至網站。

## AEM和Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` 包含H.27.5。 Adobe建議您將實作切換至 `AppMeasurement.js`
* `AppMeasurement.js` 包含v1.8.0。 Adobe建議使 [用Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) ，將AppMeasurement.js布建至網站。

## AEM與商務 {#aem-commerce}

自AEM 6.4以來，Commerce Integration Framework的改良功能已加快發行週期。請 [在這裡進一步瞭解](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html)。

## 社群附加元件 {#communities-add-on}

請參閱 [社群發行說明頁面](../release-notes/communities-release-notes.md)

## 畫面附加元件 {#screens-add-on}

* 使用啟動計畫標牌內容的未來內容變更
* 序列頻道中的計量播放
* 使用來源檔案（例如Excel工作表）自動建立專案結構

如需AEM畫面變更的詳細資訊——請參閱 [AEM畫面使用指南中的發行說明](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)。
