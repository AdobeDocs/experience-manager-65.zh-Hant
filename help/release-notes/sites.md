---
title: AEM Sites發行說明
description: Adobe Experience Manager 6.5 Sites專屬發行說明。
exl-id: 0bd0933c-f14d-4be2-9ad0-3f8207d7fa5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 1%

---

# AEM Sites發行說明{#aem-sites-release-notes}

請參閱下列AEM Sites 6.5增強功能的詳細資訊：

## 元件和模板開發{#component-amp-template-development}

* 新專案的Maven專案原型18+，如需發行說明](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases)，請參閱[Github 。
* 適用於新專案的單頁應用程式Maven專案原型1.0.6+，如需發行說明](https://github.com/adobe/aem-spa-project-archetype/releases)，請參閱[Github 。
* HTL 1.4版，如需發行說明](https://github.com/adobe/htl-spec/releases/tag/1.4)，請參閱[Github 。

   * 字串、陣列和對象的「in」運算子：

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * 具有data-sly-set的變數宣告：
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 清單和重複控制參數：開始、步驟、結束：
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * data-sly-unwrap的識別碼：

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * 支援負數

* 核心元件2.3.2+如需發行說明](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases)，請參閱[Github 。
* 佈局容器的網格系統，請參閱[Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid)。
* Clientlib管理器：將「Google關閉編譯器」設為JavaScript clientlibs的縮制（舊預設為Yahoo UI），並將「Google關閉編譯器」更新為v20190121版
* 範本編輯器和原則

   * 為使用JS SDK的單頁應用程式建立和編輯範本(又稱為SPA編輯器)

* 參考網站We.Retail 4.0，請參閱[Github以取得發行說明](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)。
* 若要升級現有網站以運用最新編輯器功能，請參閱[Github存放庫](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM包含jQuery程式庫1.12.4版，可提供與現有自訂程式碼的最大相容性。 Adobe已修改以解決已知的安全問題。

## 站點管理{#site-administration}

* [參考](/help/sites-authoring/author-environment-tools.md#references)邊欄有一個新區段，可列出指向所選頁面的內部連結。 當計畫將頁面離線或刪除時，此功能相當實用，可讓您查看哪些頁面需要在離線前加以調整。
* [清單檢視](/help/sites-authoring/basic-handling.md#list-view)有新的工作流程欄，可顯示頁面目前處於工作流程中的狀態。
* 在[頁面屬性](/help/sites-authoring/editing-page-properties.md)中，現在可以在將縮圖指派給頁面時瀏覽現有資產（縮圖索引標籤）。

## 頁面編輯器{#page-editor}

* 允許使用運用JS SDK的React和Angular用戶端元件(也稱為SPA編輯器)來建立單頁應用程式體驗，並進行內容內編輯和組合
* 只有在頁面已設定支架頁面時，才會顯示支架模式。

## 內容片段與編輯器{#content-fragments-amp-editor}

* 在內容片段編輯器中新增[註解](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations)邊欄，以建立一般註解並查看文字內的註解（也顯示在時間軸邊欄中）
* 能夠將[內容片段模型](/help/assets/content-fragments/content-fragments-models.md)中多行文字元素的預設內容類型設定為簡單文字、RTF或標籤下拉式
* 在RTE中選取文字，新增[註解/註解](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)（全螢幕檢視）
* [透過](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) 參考邊欄並排比較內容片段的版本
* 「資產下載報表」現在會據以顯示內容片段
* 透過/api.json將[內容片段支援新增至資產HTTP API](/help/assets/assets-api-content-fragments.md)。 有可建立、更新、讀取和刪除內容片段的API。

## 體驗片段 {#experience-fragments}

* 改善[體驗片段](/help/sites-authoring/experience-fragments.md)的索引，以便在搜尋使用它們的頁面時找到其內容
* [匯出至Target](/help/sites-administering/experience-fragments-target.md)選項現在允許以JSON（預設為HTML）傳送體驗片段，或同時以兩者傳送

## 轉換 {#translation}

* 使用專案主版簡化建立翻譯專案
* 預設情況下，將翻譯作業設定為批准狀態，簡化翻譯項目的執行
* 允許使用第三方翻譯記憶庫中的更改更新翻譯的頁面
* 允許以JSON格式匯出翻譯工作
* 更新Microsoft翻譯整合以使用V3 API

## 多站點管理(MSM){#multi-site-management-msm}

* 針對使用PushOnModify的轉出設定，請更妥善處理頁面移動操作，以避免狀態不一致
* 依預設，現在會在Live Copy結構內建立新頁面時，會建立獨立頁面
* 在使用JS SDK的單頁應用程式中使用MSM功能(又稱為SPA Editor)

## 啟動 {#launches}

* 啟動的新審核和核准工作流程，以及僅可提升已核准啟動頁面的功能
* 在UI中新增[選項，以選擇在促銷步驟](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)之後刪除Launch

## 內容鎖定與模擬{#content-targeting-simulation}

* ContextHub資料層和用戶端規則引擎JavaScript已更新，依預設會使用jQuery 3。

## AEM和Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>目前：
>
>* 如果您在AEM Activities主控台內使用Adobe Target作為定位引擎，則僅支援`at.js 1.x`。
   >
   >
* 如果您使用體驗片段匯出至Target，並在Target的主控台內執行活動，則`at.js. 1.x`和`at.js 2.x`都受支援。


* Adobe Target整合現在可以使用Target Standard API。 舊版AEM會使用Target Classic HTTP API，現已淘汰。
* 包含Adobe Target `mbox.js`版本63。 Adobe強烈建議將實施切換為`at.js` v1.x。
* `at.js` 現已包含1.5.0版。Adobe建議您使用[Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html)將`at.js` v1.x布建到網站。

## AEM和Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` 包含H.27.5。Adobe建議將實施切換為`AppMeasurement.js`
* `AppMeasurement.js` 包含1.8.0版。Adobe建議使用[Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html)來布建AppMeasurement.js至網站。

## AEM與商務{#aem-commerce}

自AEM 6.4起，Commerce Integration Framework的改良更快於發行週期。 [如需詳細資訊，請參閱這裡](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html)。

## Communities附加元件{#communities-add-on}

請參閱[Communities發行說明頁面](../release-notes/communities-release-notes.md)

## 螢幕附加元件{#screens-add-on}

* 使用啟動來規劃看板內容的未來內容變更
* 序列通道中的計量播放
* 使用源檔案（如Excel工作表）自動建立項目結構

如需AEM Screens變更的詳細資訊 — 請參閱[AEM Screens使用手冊](https://docs.adobe.com/content/help/zh-Hant/experience-manager-screens/user-guide/aem-screens-introduction.html)中的發行說明。
