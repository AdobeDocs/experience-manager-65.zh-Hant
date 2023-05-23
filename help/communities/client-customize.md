---
title: 客戶端自定義
seo-title: Client-side Customization
description: 在AEM Communities自定義行為或外觀客戶端
seo-description: Customizing behavior or appearance client-side in AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# 客戶端自定義  {#client-side-customization}

| **[⇐功能要點](essentials.md)** | **[伺服器端定制⇒](server-customize.md)** |
|---|---|
|  | **[SCF把手幫⇒](handlebars-helpers.md)** |

要定制客戶端上AEM Communities元件的外觀和/或行為，有幾種方法。

兩種主要方法是覆蓋或延伸元件。

[覆蓋](#overlays) 元件更改預設元件並影響對該元件的每個參照。

[擴展](#extensions) 唯一命名的元件限制更改的範圍。 術語「extend」與「override」可互換使用。

## 覆蓋 {#overlays}

覆蓋元件是對預設元件進行修改並影響使用預設元件的所有實例的方法。

覆蓋通過修改/中預設元件的副本來完成&#x200B;**應用** 目錄，而不是修改/中的原始元件&#x200B;**液體** 的子菜單。 元件由相同的相對路徑構建，但「libs」被「apps」替換。

/apps目錄是解決請求的首個搜索位置，如果找不到，則使用位於/libs目錄中的預設版本。

必須永遠不修改/libs目錄中的預設元件，因為以後的修補程式和升級可以在維護公共介面時以任何必要的方式自由更改/libs目錄。

這與 [延伸](#extensions) 一個預設元件，其中希望對特定用途進行修改，建立該元件的唯一路徑，並依賴在/libs目錄中引用原始預設元件作為超級資源類型。

有關覆蓋注釋元件的快速示例，請嘗試 [覆蓋注釋元件教程](overlay-comments.md)。

## 擴展 {#extensions}

擴展（覆蓋）元件是一種在不影響使用預設值的所有實例的情況下為特定用途進行修改的方法。 擴展元件在/apps資料夾中具有唯一名稱，並引用/libs資料夾中的預設元件，因此不會修改元件的預設設計和行為。

這與 [疊](#overlays) 預設元件，其中Sling的性質在在libs/資料夾中搜索之前解析對apps/資料夾的相對引用，從而全局修改元件的設計或行為。

有關擴展注釋元件的快速示例，請嘗試 [擴展注釋元件教程](extend-comments.md)。

## Javascript綁定 {#javascript-binding}

元件的HBS指令碼必須綁定到實現此功能的JavaScript對象、模型和視圖。

的值 `data-scf-component` 屬性可能是預設值，如 **`social/tally/components/hbs/rating`**&#x200B;或用於自定義功能的擴展（自定義）元件，如 **weretail/components/hbs/rating**。

要綁定元件，必須將整個元件指令碼包含在 &lt;div> 元素，具有以下屬性：

* `data-component-id`=&quot;{{id}}&quot;

   解析為上下文中的id屬性

* `data-scf-component`=&quot;*&lt;resourcetype>*

例如，從 `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## 自訂屬性 {#custom-properties}

在擴展或覆蓋元件時，可以向修改的對話框添加屬性。

通過引用車把模板中的屬性鍵，可以訪問元件/資源上設定的所有屬性：

`{{properties.<property_name>}}`

## 外觀CSS {#skinning-css}

定制元件以匹配網站的總體主題可以通過「外觀」實現 — 在一定程度上更改顏色、字型、影像、按鈕、連結、間距甚至定位。

通過選擇性地覆蓋框架樣式或通過編寫全新樣式表來實現外觀。 SCF元件定義了命名空間、模組化和語義CSS類，這些類影響組成元件的各種元素。

要使元件外觀，請執行以下操作：

1. 標識要更改的元素（例如，合成器區域、工具欄按鈕、消息字型等）。
1. 標識影響這些元素的CSS類/規則。
1. 建立樣式表檔案(.css)。
1. 在客戶端庫資料夾中包括樣式表([客戶端](#clientlibs-for-scf))，並確保它包含在您的模板和頁面中 [ui:includeClientLib](../../help/sites-developing/clientlibs.md)。

1. 重新定義在樣式表中標識(#2)的CSS類和規則，並添加樣式。

現在，自定義樣式將覆蓋預設框架樣式，並且元件將使用新外觀呈現。

>[!CAUTION]
>
>前置詞為的任何CSS類名 `scf-js` 在javascript代碼中具有特定用途。 這些類影響元件的狀態（例如，從隱藏切換到可見），不應覆蓋也不應移除。
>
>當 `scf-js` 類不影響樣式，類名可能用在樣式表中，但須注意，由於它們控制了元素的狀態，可能會產生副作用。

## 擴展Javascript {#extending-javascript}

要擴展元件Javascript實現，您需要：

1. 為應用建立元件，將jcr:resourceSuperType設定為擴展元件的jcr:resourceType的值，例如social/forum/components/hbs/forum。
1. 檢查預設SCF元件的Javascript以確定需要使用SCF.registerComponent()註冊哪些方法。
1. 複製擴展元件的Javascript或從頭開始。
1. 擴展方法。
1. 使用SCF.registerComponent()將所有方法註冊到預設值或自定義的對象和視圖。

### forum.js:論壇擴展示例 — HBS  {#forum-js-sample-extension-of-forum-hbs}

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

指令碼標籤是客戶端框架的固有部分。 它們是用於將在伺服器端生成的標籤與客戶端上的模型和視圖綁定在一起的粘合劑。

在覆蓋或覆蓋元件時不應刪除SCF指令碼中的指令碼標籤。 為在HTML中注入JSON而自動建立的SCF指令碼標籤由屬性標識 `data-scf-json=true`。

## SCF的客戶端 {#clientlibs-for-scf}

使用 [客戶端庫](../../help/sites-developing/clientlibs.md) （客戶端），提供了組織和優化用於在客戶端上呈現內容的Javascript和CSS的方法。

SCF的客戶端遵循兩個變體的非常特定的命名模式，這些模式僅因類別名稱中存在「author」而異：

| 客戶端庫變型 | 類別屬性的模式 |
|--- |--- |
| 完整客戶端庫 | cq.social.hbs.&lt;component name> |
| 作者客戶端庫 | cq.social.author.hbs.&lt;component name> |

### 完成客戶端 {#complete-clientlibs}

完整（非作者）客戶端包括依賴項，並且方便與ui:includeClientLib一起使用。

以下版本位於：

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

例如：

* 客戶端資料夾節點： `/etc/clientlibs/social/hbs/forum`
* 類別屬性： `cq.social.hbs.forum`

的 [社區元件指南](components-guide.md) 列出每個SCF元件所需的完整客戶端。

[社區元件的客戶端](clientlibs.md) 介紹如何將客戶端添加到頁面。

### 作者客戶端 {#author-clientlibs}

將作者版本的客戶端刪除為實現元件所需的最小Javascript。

這些客戶端永遠不應直接包含，而是可嵌入到為站點手工編製的其他客戶端中。

在SCF libs資料夾中找到以下版本：

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

例如：

* 客戶端資料夾節點： `/libs/social/forum/hbs/forum/clientlibs`
* 類別屬性： `cq.social.author.hbs.forum`

注：雖然作者客戶端從不嵌入其他庫，但他們確實會列出其依賴關係。 當嵌入到其他庫中時，依賴項不會自動被拉入，而且必須被嵌入。

通過將「author」插入為中的每個SCF元件列出的客戶端中，可以識別所需的作者客戶端 [社區元件指南](components-guide.md)。

### 使用注意事項 {#usage-considerations}

每個站點在管理客戶端庫的方式上都有所不同。 各種因素包括：

* 總體速度：也許希望網站能做出響應，但第一頁的載入速度稍慢是可以接受的。 如果許多頁使用相同的Javascript，則可以將各種Javascript嵌入到一個客戶端庫中，並從要載入的第一頁引用。 此單次下載中的Javascript保持快取狀態，從而最小化後續頁面要下載的資料量。
* 到第一頁的短時間：也許希望第一頁能快速載入。 在這種情況下，Javascript位於多個小檔案中，只在需要時引用。
* 第一頁載入和後續下載之間的平衡。

| **[⇐功能要點](essentials.md)** | **[伺服器端定制⇒](server-customize.md)** |
|---|---|
|  | **[SCF把手幫⇒](handlebars-helpers.md)** |
