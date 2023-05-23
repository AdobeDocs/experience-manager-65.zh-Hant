---
title: 內容片段的元件
seo-title: Components for Content Fragments
description: 將內AEM容片段建立並管理為與頁面無關的資產
seo-description: AEM content fragments are created and managed as page-independent assets
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 1%

---

# 內容片段的元件{#components-for-content-fragments}

## 片段創作元件 {#components-for-fragment-authoring}

>[!CAUTION]
>
>建議不要擴展或更改片段編輯器中使用的實際元件，因為這些元件仍可能更改。

查看 [內容片段管理API — 客戶端](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side)。

## 頁面創作元件 {#components-for-page-authoring}

>[!CAUTION]
>
>的 [內容片段核心元件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) 現在推薦。 請參閱 [開發核心元件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 的子菜單。
>
>本節詳細介紹為與內容片段一起使用而提供的原始元件(**內容片段** 的 **常規** 組)。

>[!NOTE]
>
>另請參閱 [內容片段配置用於呈現的元件](/help/sites-developing/content-fragments-config-components-rendering.md) 的上界。

Adobe Experience Manager(AEM)內容片段會建 [立並管理為不受頁面影響的資產](/help/assets/content-fragments/content-fragments.md)。它們允許您建立通道中性內容以及（可能特定於通道）變體。 [然後，在創作內容頁面時，可以使用這些片段及其變體](/help/sites-authoring/content-fragments.md)。 您還可以通過 [將其從資產瀏覽器拖到頁面](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) （對於其他基於資產的元件，如基礎元件映像）。 現成內容片段元件只顯示一個 [元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 的下界。 使用元件對話框可以定義 [片段段落的元素、變化和範圍](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 顯示在頁面上。

>[!NOTE]
>
>此內容片段元件在6.2AEM中作為增強版Article元件引入，但已棄用。

>[!NOTE]
>
>經典UI中不支援內容片段。

### 定義 {#definition}

的 **內容片段** 元件用於保存對內容片段資產（有效增強的文本資產）的引用。 內容片段的資源類型為：

`dam/cfm/components/contentfragment/contentfragment`

引用在屬性中定義：

`fileReference`

只有啟用觸摸的UI的編輯器完全支援內容片段元件，其中包括客戶端庫：

`cq.authoring.editor.plugin.cfm`

此庫將特定於內容片段的功能添加到編輯器中。 例如，支援在頁面上添加和配置內容片段、在資產瀏覽器中搜索內容片段資產以及在側面板中搜索相關內容的能力。

### 內部內容 {#in-between-content}

的 **內容碎片** t元件允許您在顯示的不同段落之間放置附加元件 [元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)。 基本上，所顯示的元素由不同的段落組成（每段都標有回車符）。 在每個段落之間，可以使用其他元件插入內容。

從技術角度看，所顯示元素* *的每個段落都位於其自己的parsys中，並且您在段落之間添加的每個元件都將（在框下）插入parsys中。

換句話說，如果內容片段元件的實例由三個段落組成，則該元件在儲存庫中將有三個不同的參數。 添加到內容片段的所有中間內容實際上將位於這些參數內。

在儲存庫中，中間內容相對於其在整體段落結構中的位置被儲存，即它不附加到實際段落內容。

為了說明這一點，我們考慮：

* 由三段組成的內容片段的實例
* 第二段之後已經插入了一些內容

   * 這意味著內容將儲存在第二個參數中。

基本上，如果此實例的段落結構發生更改（通過更改所顯示的段落的變化、元素或範圍），則當內容片段內容時，它可能會影響所顯示的內容：

* 編輯後，在第二段前增加一段：

   * 中間內容將顯示在新建立的段落之後（第二個參數現在保存新建立的段落）。

* 已編輯並刪除第二段：

   * 中間內容將顯示在先前是第三段的段後（第二個段現在包含前第三段）。

* 配置為僅顯示第一個段落：

   * 將不顯示中間內容（由於新配置，第二個參數不再呈現）。

### 自定義內容片段元件 {#customizing-the-content-fragment-component}

要將現成內容片段元件用作擴展藍圖，您應遵守以下合同：

* 重用HTL呈現指令碼及其關聯的POJO，查看如何實現內容功能。
* 重用內容片段節點： `cq:editConfig`

   * 的 `afterinsert`/ `afteredit`/ `afterdelete` 偵聽器用於觸發JS事件。 這些事件將在 `cq.authoring.editor.plugin.cfm` 客戶端庫，以在側面板中顯示關聯內容。
   * 的 `cq:dropTargets` 配置為支援拖動內容片段資產。
   * `cq:inplaceEditing` 配置為支援在頁面編輯器中創作內容片段。 片段就地編輯器在 `cq.authoring.editor.plugin.cfm` 客戶端庫，並允許快速連結開啟當前 [元素/變化](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 的 [片段編輯器](/help/assets/content-fragments/content-fragments-variations.md)。

### 在呈現前重寫資產 {#asset-rewriting-before-rendering}

內容片段管理使用內部呈現過程為頁面生成最終HTML輸出。 這由內容片段元件在內部使用，也由更新引用頁上引用的片段的後台進程使用。

在內部，Sling重寫器用於該渲染。 在以下位置找到相應的配置： `/libs/dam/config/rewriter/cfm` 如有需要可以調整。 查看 [阿帕奇Sling重寫器](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 的子菜單。

>[!CAUTION]
>
>如果確實調整/覆蓋重寫器的配置：
>
>* `/libs/dam/config/rewriter/cfm`
>
>然後 `serializerType` **必須** 更新為：
>
>* `serializerType="html5-serializer"`


出廠配置使用以下變壓器：

* `transformer-cfm-payloadfilter`  — 用於檢索 `body` 部件(P) `<body>...</body>`)的HTML

* `transformer-cfm-parfilter`  — 如果指定了段落範圍，則過濾掉不需要的段落（如使用「內容片段」元件所做）
* `transformer-cfm-assetprocessor`  — 用於在內部檢索嵌入到片段中的資產清單

呈現過程通過 [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) 並且可以根據需要由自定義元件來利用（例如）。
