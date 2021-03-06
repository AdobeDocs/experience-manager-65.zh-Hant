---
title: 內容片段的元件
seo-title: 內容片段的元件
description: AEM內容片段會建立並管理為獨立於頁面的資產
seo-description: AEM內容片段會建立並管理為獨立於頁面的資產
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 1%

---

# 內容片段的元件{#components-for-content-fragments}

## 片段製作的元件{#components-for-fragment-authoring}

>[!CAUTION]
>
>不建議擴充或變更片段編輯器中使用的實際元件，因為這些元件仍可能變更。

請參閱[內容片段管理API — 用戶端](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side)。

## 頁面編寫元件{#components-for-page-authoring}

>[!CAUTION]
>
>現在建議使用[內容片段核心元件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)。 如需詳細資訊，請參閱[開發核心元件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)。
>
>本節詳細說明傳遞供內容片段（****&#x200B;一般&#x200B;**群組中的內容片段**）使用的原始元件。

>[!NOTE]
>
>如需詳細資訊，另請參閱[轉譯的內容片段設定元件](/help/sites-developing/content-fragments-config-components-rendering.md) 。

Adobe Experience Manager(AEM)內容片段會建 [立並管理為不受頁面影響的資產](/help/assets/content-fragments/content-fragments.md)。它們可讓您建立管道中性內容，以及（可能是管道特定的）變化。 [然後，您可以在編寫內容頁面時使用這些片段及其變體](/help/sites-authoring/content-fragments.md)。您也可以透過[將現有內容片段資產從資產瀏覽器拖曳至頁面](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page)來使用（如基礎元件影像等其他以資產為基礎的元件）。 現成內容片段元件只顯示所參考內容片段的一個[元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)。 使用元件對話框，您可以定義要在頁面上顯示的[元素、片段段落的變化和範圍。](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)

>[!NOTE]
>
>此內容片段元件在AEM 6.2中導入，作為文章元件的增強版本，現已淘汰。

>[!NOTE]
>
>傳統UI不支援內容片段。

### 定義 {#definition}

**內容片段**&#x200B;元件用於保留對內容片段資產（有效增強的文字資產）的參考。 內容片段的資源類型為：

`dam/cfm/components/contentfragment/contentfragment`

引用在屬性中定義：

`fileReference`

只有觸控式UI的編輯器完全支援內容片段元件，其中包含用戶端程式庫：

`cq.authoring.editor.plugin.cfm`

此程式庫會新增內容片段專屬的功能至編輯器。 例如，您可在頁面上新增及設定內容片段、在資產瀏覽器中搜尋內容片段資產，以及在側面板中搜尋相關內容，都能獲得支援。

### 內容之間{#in-between-content}

**內容片段** t元件可讓您將其他元件放置在所顯示[元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)的不同段落之間。 基本上，顯示的元素由不同的段落組成（每個段落都用歸位符標籤）。 您可以在這些段落之間使用其他元件插入內容。

從技術角度來看，顯示的元素* *的每個段落都存在於其自己的parsys中，而您在段落之間新增的每個元件都會（在外罩下）插入parsys中。

換句話說，如果內容片段元件的例項由三個段落組成，則元件在存放庫中會有三個不同的parsys。 新增至內容片段的所有中間內容實際上會位於這些parsys內。

在儲存庫中，中間內容與其在整體段落結構內的位置相關，即它不附加於實際段落內容。

為了說明這一點，讓我們考慮一下：

* 由三個段落組成的內容片段的例項
* 第二段後已經插入了一些內容

   * 這表示內容會儲存在第二個parsys中。

基本上，如果此實例的段落結構改變（通過更改所顯示段落的變化、元素或範圍），則可能影響內容片段內容時顯示的中間內容：

* 編輯，並在第二段前添加另一個段落：

   * 中間內容將顯示在新建立的段落之後（第二個parsys現在保有新建立的段落）。

* 已編輯且已移除第二段：

   * 中間內容的顯示會在先前是第三個段落的段落之後（第二個parsys現在保有前第三個段落）。

* 已設定，以便僅顯示第一個段落：

   * 不會顯示中間內容（由於新設定，第二個parsys不再呈現）。

### 自訂內容片段元件{#customizing-the-content-fragment-component}

若要將現成可用的內容片段元件作為擴充的藍圖，您應遵守下列合約：

* 重複使用HTL轉譯指令碼及其相關的POJO，以了解如何實作介入式內容功能。
* 重複使用內容片段節點：`cq:editConfig`

   * `afterinsert`/ `afteredit`/ `afterdelete`監聽器用於觸發JS事件。 這些事件將在`cq.authoring.editor.plugin.cfm`用戶端資料庫中處理，以在側面板中顯示相關內容。
   * `cq:dropTargets`設定為支援拖曳內容片段資產。
   * `cq:inplaceEditing` 已設定為支援在頁面編輯器中編寫內容片段。片段就地編輯器在`cq.authoring.editor.plugin.cfm`用戶端程式庫中定義，並允許快速連結在[片段編輯器](/help/assets/content-fragments/content-fragments-variations.md)中開啟目前的[元素/變異](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)。

### 轉譯{#asset-rewriting-before-rendering}前資產重新寫入

內容片段管理使用內部轉譯程式，為頁面產生最終HTML輸出。 內容片段元件會在內部使用，也會由更新參考頁面上參考片段的背景程式使用。

在內部，Sling重寫器會用於該轉譯。 在`/libs/dam/config/rewriter/cfm`找到各自的配置，並可視需要進行調整。 如需詳細資訊，請參閱[Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 。

現成配置使用以下變壓器：

* `transformer-cfm-payloadfilter`  — 僅用於 `body` 擷取片段HTML的部 `<body>...</body>`分()

* `transformer-cfm-parfilter`  — 如果指定了段落範圍，則過濾掉不需要的段落（內容片段元件可以執行此操作）
* `transformer-cfm-assetprocessor`  — 用於內部擷取片段中內嵌的資產清單

演算程式會透過[`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html)公開，並可視需要由自訂元件來運用（例如）。
