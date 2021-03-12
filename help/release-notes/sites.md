---
title: AEM Sites發行說明
description: Adobe Experience Manager6.5網站的發行說明。
translation-type: tm+mt
source-git-commit: 23656e023a9a0bfc335655f9cfb0530aa917b3ef
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 1%

---


# AEM Sites發行說明{#aem-sites-release-notes}

如需AEM Sites6.5增強功能的詳細資訊，請參閱下列內容：

## 元件與範本開發{#component-amp-template-development}

* Maven Project Archetype 18+ for new projects，請參閱[Github for release notes](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases)。
* 針對新專案的單頁App Maven專案原型1.0.6+，請參閱[Github，以取得版本注意事項](https://github.com/adobe/aem-spa-project-archetype/releases)。
* HTL 1.4版，請參閱[Github以取得版本注意事項](https://github.com/adobe/htl-spec/releases/tag/1.4)。

   * 字串、陣列和對象的&quot;in&quot;運算子：

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * 具有資料密集的變數聲明：
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 列出和重複控制參數：開始、步驟、結束：
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * 資料破解的標識符：

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * 支援負數

* 核心元件2.3.2+，請參閱[Github，以取得發行說明](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases)。
* 版面容器的格線系統，請參閱[Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid)。
* Clientlib管理器：將Google Closure Compiler預設為JavaScript用戶端的精簡化（舊預設為Yahoo UIY），並將Google Closure Compiler更新為v20190121版
* 範本編輯器與原則

   * 針對使用JS SDK的單頁應用程式建立和編輯範本(也稱為「編SPA輯器」)

* 參考網站We.Retail 4.0，請參閱[Github，以取得發行說明](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)。
* Toolkit to upgrade existing sites to lyperace least editor capabilities, see [Github repository](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>包AEM含jQuery程式庫1.12.4版，可提供與現有自訂程式碼最大相容性。 Adobe已對已知安全性問題進行修改。

## 站點管理{#site-administration}

* [Reference](/help/sites-authoring/author-environment-tools.md#references)邊欄有新區段，可列出指向所選頁面的內部連結。 當計畫讓頁面離線或刪除時，這很有用——查看哪些頁面需要在離線前進行調整。
* [清單檢視](/help/sites-authoring/basic-handling.md#list-view)有新的工作流程欄，可顯示頁面目前在工作流程中的狀態。
* 在[頁面屬性](/help/sites-authoring/editing-page-properties.md)中，現在可在指派縮圖至頁面時瀏覽現有資產（縮表徵圖簽）。

## 頁面編輯器{#page-editor}

* 使用運用JS SDK（也稱為編輯器）的React和Angular用戶端元件，讓內容相關編輯和組合單頁應用程式體驗
* 只有當頁面已設定支架頁面時，才會顯示支架模式。

## 內容片段與編輯器{#content-fragments-amp-editor}

* 在內容片段編輯器中新增[註解](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations)邊欄，以進行一般注釋，並查看文字中的注釋（也顯示在時間軸邊欄中）
* 能夠將[內容片段模型](/help/assets/content-fragments/content-fragments-models.md)中多行文字元素的預設內容類型設為簡單文字、豐富式文字或標籤
* 通過選擇RTE中的文本（全屏視圖）添加[注釋／注釋](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [透過](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) 參考邊欄並排比較內容片段版本
* 「資產下載報表」現在會相應顯示內容片段
* 透過/api.json將[內容片段支援新增至資產HTTP API](/help/assets/assets-api-content-fragments.md)。 有建立、更新、讀取和刪除內容片段的API。

## 體驗片段 {#experience-fragments}

* 改進[體驗片段](/help/sites-authoring/experience-fragments.md)的索引，以便在搜尋使用它們的頁面時找到其內容
* [匯出至Target](/help/sites-administering/experience-fragments-target.md)選項現在允許將體驗片段傳送為JSON（預設為HTML），或兩者

## 轉換 {#translation}

* 使用專案主管簡化翻譯專案的製作
* 通過預設將翻譯作業設定為批准狀態簡化執行翻譯項目
* 允許使用第三方翻譯記憶庫中的更改更新翻譯的頁面
* 允許以JSON格式導出翻譯作業
* 更新Microsoft Translation整合以使用V3 API

## 多站點管理(MSM){#multi-site-management-msm}

* 對於使用PushOnModify的推出設定，請更妥善處理頁面移動作業，以避免狀態不一致
* 現在，依預設，在livecopy結構中建立新頁面時，將會建立獨立頁面
* 在使用JS SDK（也稱為編輯器）的單頁應用程式中使用MSMSPA功能

## 啟動 {#launches}

* 新的啟動審核和核准工作流程，並僅能提升已核准的啟動頁面
* 在UI中新增[選項，以選擇在促銷步驟](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)之後刪除啟動

## 內容定位與模擬{#content-targeting-simulation}

* ContextHub資料層和用戶端規則引擎JavaScript已依預設更新為使用jQuery 3。

## AEM和Adobe Target{#aem-amp-adobe-target}

>[!CAUTION]
>
>目前：
>
>* 如果您在「活動」主控台中使用Adobe Target作為定位引擎，則僅支援&lt;a0/AEM>。`at.js 1.x`
   >
   >
* 如果您使用Experience Fragment匯出至Target並在Target主控台中執行活動，則`at.js. 1.x`和`at.js 2.x`都受支援。


* Adobe Target整合現在可以使用Target Standard API。 舊版使AEM用Target Classic HTTP API，現已過時。
* 包含Adobe Target`mbox.js`版本63。 Adobe強烈建議將實施切換到`at.js` v1.x。
* `at.js` 現在已包含1.5.0版。Adobe建議您使用[Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html)將`at.js` v1.x布建到站點。

## AEM和Adobe Analytics{#aem-amp-adobe-analytics}

* `s_code.js` 包含H.27.5。Adobe建議您將實施切換至`AppMeasurement.js`
* `AppMeasurement.js` 包含v1.8.0。Adobe建議使用[Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html)將AppMeasurement.js布建至網站。

## AEM和商務{#aem-commerce}

自6.4以來，Commerce Integration Framework的改良功能已在更快速的發AEM行週期中加強。[在這裡瞭解詳細內容](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html)。

## 社群附加元件{#communities-add-on}

請參閱[社群發行說明頁面](../release-notes/communities-release-notes.md)

## 畫面附加元件{#screens-add-on}

* 使用啟動計畫標牌內容的未來內容變更
* 序列頻道中的計量播放
* 使用來源檔案（例如Excel工作表）自動建立專案結構

有關AEM Screens更改的詳細資訊——請參閱[AEM Screens使用手冊](https://docs.adobe.com/content/help/zh-Hant/experience-manager-screens/user-guide/aem-screens-introduction.html)中的發行說明。
