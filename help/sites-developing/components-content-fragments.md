---
title: 內容片段的元件
seo-title: 內容片段的元件
description: AEM內容片段會建立並管理為不受頁面影響的資產
seo-description: AEM內容片段會建立並管理為不受頁面影響的資產
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 內容片段的元件{#components-for-content-fragments}

## 片段製作的元件 {#components-for-fragment-authoring}

>[!CAUTION]
>
>建議不要擴充或變更片段編輯器中使用的實際元件，因為這些元件仍有可能變更。

請參閱 [內容片段管理API —— 用戶端](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side)。

## 頁面製作的元件 {#components-for-page-authoring}

>[!CAUTION]
>
>現在 [建議使用內容片段核心元件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) 。 如需詳 [細資訊，請參閱開發核心](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 元件。
>
>本節詳細說明傳送的原始元件，以便與內容片段(**「一般」群組中的「內** 容片段 **** 」)搭配使用。

>[!NOTE]
>
>如需詳細 [資訊，請參閱內容片段設定轉譯元件](/help/sites-developing/content-fragments-config-components-rendering.md) 。

Adobe Experience Manager(AEM)內容片段會建 [立並管理為不受頁面影響的資產](/help/assets/content-fragments.md)。 它們可讓您建立不受頻道影響的內容，以及（可能是特定頻道的）變化。 [然後，您可以在編寫內容頁面時使用這些片段及其變化](/help/sites-authoring/content-fragments.md)。 您也可以將現有內容片段資產從資 [產瀏覽器拖曳至頁面](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) （對於其他以資產為基礎的元件，例如基礎元件影像），以使用它。 現成可用的內容片段元件只顯示參考 [內容片段](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment) 的一個元素。 使用元件對話方塊，您可 [以定義要在頁面上顯示的元素](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment) 、變數和片段段落範圍。

>[!NOTE]
>
>此內容片段元件是在AEM 6.2中以增強版Article元件的形式引進，已過時。

>[!NOTE]
>
>傳統UI不支援內容片段。

### 定義 {#definition}

內 **容片段** (Content Fragment)元件用來保存對內容片段資產（有效增強的文字資產）的參考。 內容片段的資源類型為：

`dam/cfm/components/contentfragment/contentfragment`

引用在屬性中定義：

`fileReference`

只有觸控式UI的編輯器完全支援內容片段元件，其中包含用戶端程式庫：

`cq.authoring.editor.plugin.cfm`

此程式庫會將內容片段的特定功能新增至編輯器。 例如，支援在頁面上新增和設定內容片段、在資產瀏覽器中搜尋內容片段資產以及在側面板中搜尋相關內容。

### 內容 {#in-between-content}

「內 **容**&#x200B;片段」元件可讓您將其他元件拖放至顯示元素的不同段落 [之間](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment)。 基本上，顯示的元素由不同段落組成（每個段落標有回車符）。 在每個段落之間，您可以使用其他元件插入內容。

從技術角度看，顯示的元素* *的每個段落都以其自己的parsys為生，而您在段落之間添加的每個元件都將（在外罩下）插入parsys中。

換言之，如果內容片段元件的實例由三個段落組成，則該元件在儲存庫中將有三個不同的段落。 新增至內容片段的所有中間內容實際上都位於這些參數中。

在儲存庫中，中間內容相對於其在整體段落結構內的位置被儲存，即它不附加到實際段落內容。

為了說明這一點，我們考慮一下：

* 由三個段落組成的內容片段實例
* 第二段之後已經插入了一些內容

   * 這表示內容將儲存在第二個參數中。

基本上，如果此實例的段落結構改變（通過更改顯示的段落的變化、元素或範圍），則可能影響內容片段內容時顯示的中間內容：

* 已編輯，並在第二段前加入另一段：

   * 中間內容將顯示在新建立的段落之後（第二個段落現在保留新建立的段落）。

* 已編輯，並移除第二段：

   * 中間內容將顯示在先前是第三個段落的段落之後（第二個段落現在保留上一個第三個段落）。

* 已設定為只顯示第一個段落：

   * 不會顯示中間內容（第二個參數因新配置而不再呈現）。

### 自訂內容片段元件 {#customizing-the-content-fragment-component}

若要將現成可用的內容片段元件當做擴充藍圖，您應遵守下列合約：

* 重複使用HTL轉換指令碼及其相關的POJO，以檢視如何實作內容介入功能。
* 重複使用內容片段節點： `cq:editConfig`

   * 使用 `afterinsert`/ `afteredit`/ `afterdelete` 監聽器來觸發JS事件。 這些事件將在用戶端程式庫 `cq.authoring.editor.plugin.cfm` 中處理，以在側面面板中顯示相關內容。
   * 設定 `cq:dropTargets` 為支援拖曳內容片段資產。
   * `cq:inplaceEditing` 已設定為支援在頁面編輯器中編寫內容片段。 片段就地編輯器在客戶端庫中定 `cq.authoring.editor.plugin.cfm` 義，並允許快速連結在片段編輯器中 [開啟當前元](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment) 素／變化 [](/help/assets/content-fragments-variations.md)。

### 演算前重寫資產 {#asset-rewriting-before-rendering}

「內容片段管理」使用內部轉換程式來產生頁面的最終HTML輸出。 這由「內容片段」元件內部使用，也由更新參考頁面上參考片段的背景程式使用。

在內部，Sling Rewriter會用於該演算。 各自的配置位於， `/libs/dam/config/rewriter/cfm` 並可視需要調整。 如需詳細 [資訊，請參閱Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 。

現成配置使用以下變壓器：

* `transformer-cfm-payloadfilter` -僅用於 `body` 檢索片段 `<body>...</body>`的HTML的部件()

* `transformer-cfm-parfilter` -如果指定段落範圍，則過濾掉不要的段落（如「內容片段」元件所做）
* `transformer-cfm-assetprocessor` -用於內部檢索嵌入在片段中的資產清單

演算程式會透過公開， [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) 並可視需要由自訂元件（例如）運用。
