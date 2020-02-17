---
title: 用戶端自訂
seo-title: 用戶端自訂
description: 自訂AEM Communities中的行為或外觀用戶端
seo-description: 自訂AEM Communities中的行為或外觀用戶端
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 用戶端自訂 {#client-side-customization}

| **[‹功能基本工具](essentials.md)** | **[伺服器端自訂‹](server-customize.md)** |
|---|---|
|  | **[SCF Handlepers ‡](handlebars-helpers.md)** |

若要自訂用戶端上AEM Communities元件的外觀和／或行為，有數種方法。

兩種主要方式是覆蓋或延伸元件。

[重疊元件](#overlays) (Overlaying a component)會變更預設元件，並影響元件的每個參照。

[擴充](#extensions) 元件（以唯一名稱命名）會限制變更範圍。 術語「extend」與「override」可互換使用。

## 覆蓋 {#overlays}

覆蓋元件是對預設元件進行修改並影響所有使用預設元件的實例的方法。

覆蓋是透過修改/**apps目錄中預設元件的復本** ，而非修改/**libs目錄中的原始元件來完成** 。 元件是使用相同的相對路徑建構的，但「libs」會取代為「apps」。

首先搜尋/apps目錄來解決請求，如果找不到，則會使用位於/libs目錄中的預設版本。

不得修改/libs目錄中的預設元件，因為以後的修補程式和升級可以在維護公共介面的同時，以任何必要的方式自由更改/libs目錄。

這與擴充 [預設元件](#extensions) （其中希望對特定用途進行修改）、建立到該元件的唯一路徑，以及依賴引用/libs目錄中的原始預設元件作為超級資源類型不同。

如需覆蓋注釋元件的快速範例，請試用「覆蓋注釋 [元件」教學課程](overlay-comments.md)。

## 擴充功能 {#extensions}

擴充（覆寫）元件是一種修改特定用途的方法，不會影響使用預設值的所有例項。 擴充元件在/apps資料夾中具有唯一名稱，且會參照/libs資料夾中的預設元件，因此不會修改元件的預設設計和行為。

這與在libs/檔案夾中 [搜尋前](#overlays) ,Sling的性質會先解析應用程式／檔案夾的相對參照，而將元件的設計或行為全域修改的預設元件不同。

如需擴充注釋元件的快速範例，請試用「擴充注釋元 [件」教學課程](extend-comments.md)。

## Javascript系結 {#javascript-binding}

元件的HBS指令碼必須系結至實作此功能的JavaScript物件、模型和檢視。

屬性的值可 `data-scf-component` 以是預設值，例如 **`social/tally/components/hbs/rating`**，或是自訂功能的擴充（自訂）元件，例如 **weretail/components/hbs/rating**。

要綁定元件，必須將整個元件指令碼包含在&lt;div>元素中，並包含以下屬性：

* `data-component-id`=&quot;{{id}}&quot;

   從內容解析至id屬性

* `data-scf-component`=&quot;*&lt;resourceType>*

例如，從 `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## 自訂屬性 {#custom-properties}

延伸或覆蓋元件時，可將屬性新增至已修改的對話方塊。

通過引用車把模板中的屬性鍵，可以訪問元件／資源上設定的所有屬性：

`{{properties.<property_name>}}`

## 設定CSS外觀 {#skinning-css}

自訂元件以符合網站的整體主題，可透過「外觀設定」來達成——在一定程度上變更顏色、字型、影像、按鈕、連結、間距甚至定位。

您可以選擇性覆寫架構樣式，或撰寫全新的樣式表，來設定外觀。 SCF元件定義了命名空間、模組化和語義CSS類，這些類會影響組成元件的各種元素。

設定元件外觀：

1. 識別您要變更的元素（例如，編譯器區域、工具列按鈕、訊息字型等）。
1. 識別影響這些元素的CSS類別／規則。
1. 建立樣式表檔案(.css)。
1. 將樣式表包含在您網站的用戶端程式庫檔案夾([clientlibs](#clientlibs-for-scf))中，並確保它已包含在您範本和頁面中，並 [包含ui:includeClientLib](../../help/sites-developing/clientlibs.md)。

1. 重新定義您在樣式表中識別(#2)的CSS類別和規則，並新增樣式。

自訂樣式現在會覆寫預設的架構樣式，而元件會以新的外觀呈現。

>[!CAUTION]
>
>任何前置詞** scf-js-&amp;ast;**的CSS類別名稱在javascript程式碼中都有特定用途。 這些類會影響元件的狀態（例如，從隱藏切換為可見），且不應覆蓋或移除。
>
>而scf-js-&amp;ast;類不影響樣式，類名可以在樣式表中使用，但須注意，由於它們控制了元素的狀態，可能會有副作用。

## 擴充Javascript {#extending-javascript}

若要擴充元件Javascript實作，您只需

1. 為應用程式建立元件，並將jcr:resourceSuperType設為延伸元件的jcr:resourceType值，例如social/forum/components/hbs/forum
1. 檢查預設SCF元件的Javascript以確定哪些方法需要使用SCF.registerComponent()進行註冊
1. 複製延伸元件的Javascript或從頭開始
1. 擴充方法
1. 使用SCF.registerComponent()註冊所有具有預設值或自定義對象和視圖的方法。

### forum.js:論壇的範例擴充- HBS {#forum-js-sample-extension-of-forum-hbs}

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

## 指令碼標籤 {#script-tags}

指令碼標籤是用戶端架構的固有部分。 它們可協助將伺服器端產生的標籤與用戶端的模型和檢視系結在一起。

在覆蓋或覆蓋元件時，不應刪除SCF指令碼中的指令碼標籤。 SCF指令碼標籤會以屬性 `data-scf-json=`true來識別為在HTML中注入JSON而自動建立。

## SCF的Clientlibs {#clientlibs-for-scf}

使用用戶 [端程式庫](../../help/sites-developing/clientlibs.md) (clientlibs)，提供組織和最佳化用來在用戶端上轉換內容的Javascript和CSS的方式。

SCF的clientlibs遵循兩個變體的非常特定命名模式，只有在類別名稱中出現&#39;author&#39;時不同：

| Clientlib變體 | 類別的模式屬性 |
|--- |--- |
| 完整的clientlib | cq.social.hbs.&lt;component name> |
| author clientlib | cq.social.author.hbs.&lt;component name> |

### 完整的Clientlibs {#complete-clientlibs}

完整（非作者）的clientlibs包含相依性，並方便與ui:includeClientLib一起加入。

這些版本位於：

* /etc/clientlibs/social/hbs/&lt;component name>

例如：

* 客戶端資料夾節點：/etc/clientlibs/social/hbs/forum
* 類別屬性：cq.social.hbs.forum

「社 [群元件」指南](components-guide.md) ，列出了每個SCF元件所需的完整客戶端。

[Clientlibs for Communities](clientlibs.md) Components說明如何將clientlibs新增至頁面。

### 作者Clientlibs {#author-clientlibs}

作者版本clientlib會清除至實作元件所需的最小Javascript。

這些clientlib永遠不應直接包含在內，但可嵌入為網站手工製作的其他clientlib。

這些版本位於SCF libs資料夾中：

* /libs/social/&lt;feature>/components/&lt;component name>/clientlibs

例如：

* 客戶端資料夾節點：/libs/social/forum/hbs/forum/clientlibs
* 類別屬性：cq.social.author.hbs.forum

注意：雖然作者clientlibs從不嵌入其他程式庫，但是他們確實會列出其相依性。 嵌入到其他庫時，不會自動提取從屬關係，也必須嵌入。

在「社群元件指南」中為每個SCF元件列出的clientlibs中插入&quot;author&quot;，即可識別所需的作者 [clientlibs](components-guide.md)。

### 使用考量事項 {#usage-considerations}

每個網站在管理用戶端程式庫的方式上都不同。 各種因素包括：

* 整體速度：可能是希望網站能夠回應，但是第一頁載入速度稍微慢一點，是可以接受的。 如果許多頁面使用相同的Javascript，則可將各種Javascript內嵌至一個clientlib，並從第一頁參考以載入。 此次下載中的Javascript會維持快取狀態，將後續頁面的資料下載量減至最少。
* 第一頁的簡短時間：可能是希望第一頁能快速載入。 在這種情況下，Javascript位於多個小檔案中，只有在需要時才會參考。
* 第一頁載入與後續下載之間的平衡。

| **[‹功能基本工具](essentials.md)** | **[伺服器端自訂‹](server-customize.md)** |
|---|---|
|  | **[SCF Handlepers ‡](handlebars-helpers.md)** |

