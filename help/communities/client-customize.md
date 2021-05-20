---
title: 用戶端自訂
seo-title: 用戶端自訂
description: 在AEM Communities中自訂行為或外觀用戶端
seo-description: 在AEM Communities中自訂行為或外觀用戶端
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---

# 用戶端自訂{#client-side-customization}

| **[⇐功能要點](essentials.md)** | **[伺服器端自訂⇒](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

若要自訂用戶端上AEM Communities元件的外觀和/或行為，有數種方法。

覆蓋或延伸元件是兩種主要方法。

[](#overlays) 覆蓋元件會變更預設元件，並影響元件的每個參照。

[](#extensions) 延伸元件（名稱唯一）會限制變更的範圍。「extend」一詞與「override」可交互使用。

## 覆蓋 {#overlays}

覆蓋元件是對預設元件進行修改並影響使用預設值的所有實例的方法。

覆蓋通過修改/**apps**&#x200B;目錄中的預設元件的副本來完成，而不是修改/**libs**&#x200B;目錄中的原始元件。 元件是以相同的相對路徑建構，除了「libs」會取代為「apps」。

首先搜尋/apps目錄以解決請求，若找不到，則使用/libs目錄中的預設版本。

不得修改/libs目錄中的預設元件，因為將來的修補程式和升級可以在維護公共介面時，以任何必要的方式更改/libs目錄。

這與[extending](#extensions)預設元件不同，預設元件的用途是為特定用途進行修改，為元件建立唯一路徑，並依賴在/libs目錄中引用原始預設元件作為超級資源類型。

如需覆蓋注釋元件的快速範例，請嘗試[覆蓋注釋元件教學課程](overlay-comments.md)。

## 擴充功能 {#extensions}

擴充（覆寫）元件是修改特定用途而不影響使用預設值的所有執行個體的方法。 擴展元件在/apps資料夾中具有唯一名稱，並引用/libs資料夾中的預設元件，因此不會修改元件的預設設計和行為。

這與[overlaying](#overlays)預設元件不同，在預設元件中，Sling的性質會先解析應用程式/資料夾的相對參照，再在libs/資料夾中進行搜尋，因此元件的設計或行為會遭到全域修改。

有關擴展注釋元件的快速示例，請嘗試[擴展注釋元件教程](extend-comments.md)。

## Javascript綁定{#javascript-binding}

元件的HBS指令碼必須系結至實作此功能的JavaScript物件、模型和檢視。

`data-scf-component`屬性的值可以是預設值，如&#x200B;**`social/tally/components/hbs/rating`**，或用於自定義功能的擴展（自定義）元件，如&#x200B;**weretail/components/hbs/rating**。

若要系結元件，必須將整個元件指令碼圍在&lt;div>元素內，並包含下列屬性：

* `data-component-id`=&quot;{{id}}&quot;

   從內容解析為id屬性

* `data-scf-component`=&quot;*&lt;resourcetype>*

例如，從`/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## 自訂屬性 {#custom-properties}

在擴展或覆蓋元件時，可以將屬性添加到修改的對話框。

可通過參考handlebars模板中的屬性鍵來訪問元件/資源上設定的所有屬性：

`{{properties.<property_name>}}`

## 設定CSS {#skinning-css}外觀

定制元件以匹配網站的整體主題可以通過「外觀」（在一定程度上更改顏色、字型、影像、按鈕、連結、間距甚至定位）來實現。

可通過選擇性地覆蓋框架樣式或通過撰寫全新樣式表來實現外觀設定。 SCF元件定義命名節點、模組化和語義CSS類，這些類影響構成元件的各種元素。

要外觀元件，請執行以下操作：

1. 識別您要變更的元素（範例 — 撰寫器區域、工具列按鈕、訊息字型等）。
1. 識別影響這些元素的CSS類別/規則。
1. 建立樣式表檔案(.css)。
1. 將樣式表包含在您網站的用戶端程式庫資料夾([clientlibs](#clientlibs-for-scf))中，並確認該樣式表包含在您具有[ui:includeClientLib](../../help/sites-developing/clientlibs.md)的範本和頁面中。

1. 重新定義您在樣式表中識別的CSS類別和規則(#2)，並新增樣式。

自訂樣式現在會覆寫預設的架構樣式，而元件將會以新外觀呈現。

>[!CAUTION]
>
>任何以`scf-js`為首碼的CSS類別名稱在javascript程式碼中都有特定用途。 這些類會影響元件的狀態（例如，從隱藏切換為可見），不應覆蓋或移除。
>
>雖然`scf-js`類不影響樣式，但類名可以在樣式表中使用，但應注意，由於它們控制元素的狀態，可能會產生副作用。

## 擴充Javascript {#extending-javascript}

若要擴充元件Javascript實施，您必須：

1. 為應用程式建立元件，並將jcr:resourceSuperType設為延伸元件的jcr:resourceType的值，例如social/forum/components/hbs/forum。
1. 檢查預設SCF元件的Javascript，以確定需要使用SCF.registerComponent()註冊的方法。
1. 複製延伸元件的Javascript或從頭開始。
1. 擴充方法。
1. 使用SCF.registerComponent()註冊所有方法，其中包括預設值或自定義對象和視圖。

### forum.js:論壇的範例擴充功能 — HBS {#forum-js-sample-extension-of-forum-hbs}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";
    var GMForumView = SCF.ForumView.extend({
        viewName: "GMForum",
        showComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        },
        hideComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        }
    });

    SCF.registerComponent('social/forum/components/hbs/post', SCF.Post, SCF.PostView);
    SCF.registerComponent('social/forum/components/hbs/topic', SCF.Topic, SCF.TopicView);
    SCF.registerComponent('social/forum/components/hbs/forum', SCF.Forum, GMForumView );
})($CQ, _, Backbone, SCF);
```

## 指令碼標籤{#script-tags}

指令碼標籤是用戶端架構的固有部分。 它們是膠水，有助於將伺服器端產生的標籤與用戶端的模型和檢視系結。

覆蓋或覆蓋元件時，不應移除SCF指令碼中的指令碼標籤。 為在HTML中插入JSON而自動建立的SCF指令碼標籤以屬性`data-scf-json=true`標識。

## SCF {#clientlibs-for-scf}的客戶端

使用[用戶端資料庫](../../help/sites-developing/clientlibs.md)(clientlibs)，可提供組織和最佳化用於在用戶端上呈現內容的Javascript和CSS的方法。

SCF的clientlib會遵循兩種變體非常特定的命名模式，而這兩種模式只會因類別名稱中是否存在「author」而有所不同：

| Clientlib變體 | 類別屬性的模式 |
|--- |--- |
| 完整clientlib | cq.social.hbs.&lt;component name=&quot;&quot;> |
| author clientlib | cq.social.author.hbs.&lt;component name=&quot;&quot;> |

### 完成Clientlibs {#complete-clientlibs}

完整（非作者）clientlib包含相依性，且方便搭配ui:includeClientLib加入。

這些版本位於：

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

例如：

* 客戶端資料夾節點：`/etc/clientlibs/social/hbs/forum`
* 類別屬性：`cq.social.hbs.forum`

[社區元件指南](components-guide.md)列出每個SCF元件所需的完整客戶端。

[Communities元件的](clientlibs.md) Clientlibs說明如何將clientlibs新增至頁面。

### 作者Clientlibs {#author-clientlibs}

製作版本clientlib會去除至實作元件所需的最小Javascript。

這些clientlib絕不應直接包含在內，而是可內嵌至其他clientlib，這些clientlib是為網站手工編製。

在SCF libs資料夾中找到以下版本：

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

例如：

* 客戶端資料夾節點：`/libs/social/forum/hbs/forum/clientlibs`
* 類別屬性：`cq.social.author.hbs.forum`

注意：雖然作者clientlibs絕不內嵌其他程式庫，但會列出其相依性。 內嵌在其他程式庫時，不會自動提取相依性，也必須內嵌。

在[社群元件指南](components-guide.md)中針對每個SCF元件列出的clientlib中插入「author」，即可識別所需的作者clientlib。

### 使用考量事項{#usage-considerations}

每個網站在管理用戶端程式庫的方式上都不同。 各種因素包括：

* 整體速度：可能是希望網站能有回應，但第一個頁面載入速度有點慢是可接受的。 如果許多頁面使用相同的Javascript，則各種Javascript可內嵌至一個clientlib，並從第一個頁面參照以載入。 此單次下載中的Javascript會維持快取狀態，將後續頁面要下載的資料量減到最少。
* 第一頁的簡短時間：可能是想要快速載入第一個頁面。 在此情況下，Javascript位於多個小檔案中，只在需要時才要參考。
* 第一個頁面載入與後續下載之間的平衡。

| **[⇐功能要點](essentials.md)** | **[伺服器端自訂⇒](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
