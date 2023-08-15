---
title: 內容片段的元件
seo-title: Components for Content Fragments
description: AEM內容片段會建立並管理為不受頁面影響的資產
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
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 1%

---

# 內容片段的元件{#components-for-content-fragments}

## 片段編寫的元件 {#components-for-fragment-authoring}

>[!CAUTION]
>
>不建議擴充或變更片段編輯器中使用的實際元件，因為這些元件仍可能會變更。

請參閱 [內容片段管理API — 使用者端](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## 用於頁面編寫的元件 {#components-for-page-authoring}

>[!CAUTION]
>
>此 [內容片段核心元件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) 現在建議使用。 另請參閱 [開發核心元件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 以取得更多詳細資料。
>
>本節詳細說明用於內容片段的原始元件(**內容片段** 在 **一般** 群組)。

>[!NOTE]
>
>另請參閱 [轉譯專用內容片段設定元件](/help/sites-developing/content-fragments-config-components-rendering.md) 以取得進一步資訊。

Adobe Experience Manager(AEM)內容片段會建 [立並管理為不受頁面影響的資產](/help/assets/content-fragments/content-fragments.md)。它們可讓您建立管道中性內容，連同（可能特定於管道）變數。 [接著，您可以在編寫內容頁面時，使用這些片段及其變數](/help/sites-authoring/content-fragments.md). 您也可以透過以下方式使用現有的內容片段資產： [將其從資產瀏覽器拖曳至頁面](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) （如同其他以資產為基礎的元件，例如基礎元件影像）。 現成可用的內容片段元件只會顯示一個 [元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 所參考的內容片段的。 您可以使用元件對話方塊來定義 [元素、變數和片段段落的範圍](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 要顯示在頁面上的資訊。

>[!NOTE]
>
>此內容片段元件已在AEM 6.2中作為文章元件的增強版本引入，但已淘汰。

>[!NOTE]
>
>傳統UI中不支援內容片段。

### 定義 {#definition}

此 **內容片段** 元件是用來儲存內容片段資產的參考（有效地增強文字資產）。 內容片段的資源型別為：

`dam/cfm/components/contentfragment/contentfragment`

參照是在屬性中定義：

`fileReference`

只有觸控式UI的編輯器完全支援內容片段元件，其中包括使用者端程式庫：

`cq.authoring.editor.plugin.cfm`

此程式庫會將內容片段的特定功能新增到編輯器中。 例如，可支援在頁面上新增和設定內容片段的功能、在資產瀏覽器中搜尋內容片段資產的功能，以及側面板中的相關內容。

### 中間內容 {#in-between-content}

此 **內容片段** t元件可讓您在顯示的不同段落之間放置其他元件 [元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). 基本上，顯示的元素由不同的段落組成（每個段落都標有歸位字元）。 在每個段落之間，您可以使用其他元件來插入內容。

從技術觀點來看，顯示的元素* *的每個段落都存在於它自己的parsys中，您在段落之間新增的每個元件都將（在機殼下）插入parsys中。

換言之，如果內容片段元件的例項由三個段落組成，則元件在存放庫中將有三個不同的parsys。 所有新增至內容片段的中間內容實際上將會位於這些parsys內。

在存放庫中，中間內容會相對於其在整個段落結構中的位置儲存，也就是說，它不會附加至實際的段落內容。

為了說明這一點，讓我們考慮以下事項：

* 由三個段落組成的內容片段例項
* 而且有些內容已經插入在第二段之後

   * 這表示內容會儲存在第二個parsys中。

基本上，如果此例項的段落結構有所變更（透過變更顯示的變化、元素或段落範圍），可能會影響內容片段內容時顯示的中間內容：

* 會進行編輯，並在第二段之前新增另一個段落：

   * 中間內容將顯示在新建立的段落之後（第二個parsys現在容納新建立的段落）。

* 已編輯並移除第二段：

   * 中間內容會顯示在先前為第三個的段落之後（第二個parsys現在包含前三個段落）。

* 設定為只顯示第一段：

   * 將不會顯示中間內容（由於新設定，第二個parsys將不會再呈現）。

### 自訂內容片段元件 {#customizing-the-content-fragment-component}

若要使用現成的內容片段元件作為擴充的藍圖，您應遵守下列合約：

* 重複使用HTL演算指令碼及其關聯的POJO，檢視中間內容功能的實作方式。
* 重複使用內容片段節點： `cq:editConfig`

   * 此 `afterinsert`/ `afteredit`/ `afterdelete` 監聽器可用來觸發JS事件。 這些事件將在以下位置處理： `cq.authoring.editor.plugin.cfm` 使用者端資源庫，以在側面板中顯示關聯內容。
   * 此 `cq:dropTargets` 設定為支援拖曳內容片段資產。
   * `cq:inplaceEditing` 設定為支援在頁面編輯器中編寫內容片段。 片段就地編輯器是在 `cq.authoring.editor.plugin.cfm` 使用者端程式庫，並允許快速連結以開啟目前的 [元素/變數](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 在 [片段編輯器](/help/assets/content-fragments/content-fragments-variations.md).

### 轉譯前的資產重新寫入 {#asset-rewriting-before-rendering}

內容片段管理會使用內部轉譯程式，為頁面產生最終HTML輸出。 這在內部供內容片段元件使用，同時也供在參考頁面上更新參考片段的背景程式使用。

在內部，Sling重寫程式會用於該轉譯。 您可在以下位置找到個別設定： `/libs/dam/config/rewriter/cfm` 如有需要，可調整和。 請參閱 [Apache Sling重寫程式](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 以取得詳細資訊。

>[!CAUTION]
>
>如果您確實調整/覆蓋重寫程式的設定：
>
>* `/libs/dam/config/rewriter/cfm`
>
>然後 `serializerType` **必須** 將更新至：
>
>* `serializerType="html5-serializer"`

現成可用的組態使用下列轉換器：

* `transformer-cfm-payloadfilter`  — 用於擷取 `body` 部分( `<body>...</body>`)僅片段HTML的

* `transformer-cfm-parfilter`  — 如果指定段落範圍，則篩選掉不需要的段落（與內容片段元件一樣）
* `transformer-cfm-assetprocessor`  — 在內部使用，用於擷取內嵌在片段中的資產清單

演算程式會透過以下方式公開 [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) 如有需要，自訂元件可運用和（例如）。
