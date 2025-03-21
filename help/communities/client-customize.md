---
title: 使用者端自訂
description: 在AEM Communities中自訂使用者端的行為或外觀
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# 使用者端自訂  {#client-side-customization}

| **[⇐ Feature Essentials](essentials.md)** | **[伺服器端自訂⇒](server-customize.md)** |
|---|---|
|   | **[SCF Handlebars協助程式⇒](handlebars-helpers.md)** |

若要自訂AEM Communities元件在使用者端的外觀和/或行為，有數種方法。

覆蓋或延伸元件是兩種主要方法。

[覆蓋](#overlays)元件會變更預設元件，並影響元件的每個參考。

[延伸](#extensions)唯一命名的元件會限制變更的範圍。 「延伸」一詞可與「覆寫」互換使用。

## 覆蓋 {#overlays}

覆蓋元件是修改預設元件並影響使用預設的所有例證的方法。

重疊是藉由修改/**apps**&#x200B;目錄中預設元件的復本來完成，而非修改/**libs**&#x200B;目錄中的原始元件。 元件是使用相同的相對路徑建構，但「libs」會取代為「apps」。

/apps目錄是第一個搜尋以解決請求的位置，如果未找到，則會使用/libs目錄中的預設版本。

/libs目錄中的預設元件絕不可修改，因為未來的修補程式和升級可以自由地以任何必要的方式變更/libs目錄，同時維護公用介面。

這與[延伸](#extensions)預設元件不同，在預設元件中，需要針對特定用途進行修改、建立元件的唯一路徑，並依賴將/libs目錄中的原始預設元件參照為超級資源型別。

如需重疊註解元件的快速範例，請嘗試[重疊註解元件教學課程](overlay-comments.md)。

## 擴充功能 {#extensions}

延伸（覆寫）元件是一種針對特定用途進行修改的方法，不會影響使用預設值的所有例證。 擴充元件在/apps資料夾中有唯一名稱，且會參照/libs資料夾中的預設元件，因此不會修改元件的預設設計和行為。

這與[覆蓋](#overlays)預設元件不同，在搜尋libs/資料夾之前，Sling的本質會解析應用程式/資料夾的相對參照，因此元件的設計或行為會全域修改。

如需擴充註解元件的快速範例，請嘗試[擴充註解元件教學課程](extend-comments.md)。

## JavaScript繫結 {#javascript-binding}

元件的HBS指令碼必須繫結至JavaScript物件、模型和檢視，才能實作此功能。

`data-scf-component`屬性的值可能是預設值，例如&#x200B;**`social/tally/components/hbs/rating`**，或是自訂功能的延伸（自訂）元件，例如&#x200B;**weretail/components/hbs/rating**。

若要繫結元件，整個元件指令碼必須包含在具有以下屬性的&lt;div>元素中：

* `data-component-id`=&quot;`{{id}}`&quot;

  會解析至內容中的id屬性

* `data-scf-component`=&quot;*&lt;resourceType>*

例如，從`/apps/weretail/components/hbs/rating/rating.hbs`：

```xml
<div class="we-Rating" data-component-id="`{{id}}`" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## 自訂屬性 {#custom-properties}

延伸或覆蓋元件時，可以將屬性新增到已修改的對話方塊。

參照handlebars範本中的屬性索引鍵，可存取元件/資源上設定的所有屬性：

`{{properties.<property_name>}}`

## 建立CSS外觀 {#skinning-css}

自訂元件以符合網站的整體主題，可透過「外觀設定」來達成 — 變更顏色、字型、影像、按鈕、連結、間距，甚至在一定程度上定位。

可以選擇覆寫框架樣式或撰寫全新的樣式表，以建立外觀元素。 SCF元件會定義名稱空間、模組化和語意CSS類別，這些類別會影響組成元件的各種元素。

若要建立元件的外觀，請執行下列動作：

1. 識別您要變更的元素（例如：撰寫器區域、工具列按鈕、訊息字型等）。
1. 識別影響這些元素的CSS類別/規則。
1. 建立樣式表檔案(.css)。
1. 將樣式表包含在您網站的使用者端資料庫資料夾([clientlibs](#clientlibs-for-scf))中，並確定它包含在您的範本和具有[ui：includeClientLib](../../help/sites-developing/clientlibs.md)的頁面中。

1. 重新定義已在樣式表中識別(#2)的CSS類別和規則，並新增樣式。

自訂樣式現在會覆寫預設框架樣式，且元件將會以新外觀元素呈現。

>[!CAUTION]
>
>任何以`scf-js`為前置詞的CSS類別名稱在JavaScript程式碼中都有特定的用途。 這些類別會影響元件的狀態（例如，從隱藏切換為可見），且不應覆寫或移除。
>
>雖然`scf-js`類別不會影響樣式，但在樣式表中可以使用類別名稱，但請注意，由於類別名稱控制元素的狀態，因此可能會產生副作用。

## 擴充JavaScript {#extending-javascript}

若要擴充元件JavaScript實作，您需要：

1. 為應用程式建立元件，並將jcr：resourceSuperType設定為擴充元件的jcr：resourceType值，例如social/forum/components/hbs/forum。
1. 檢查預設SCF元件的JavaScript，以決定需要使用SCF.registerComponent()註冊的方法。
1. 複製擴充元件的JavaScript或從頭開始。
1. 擴充方法。
1. 使用SCF.registerComponent()以預設值或自訂物件與檢視來註冊所有方法。

### forum.js： Forum範例擴充功能 — HBS  {#forum-js-sample-extension-of-forum-hbs}

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

指令碼標籤是使用者端架構的內在部分。 它們是膠水，有助於將伺服器端產生的標示與使用者端上的模型和檢視繫結。

重疊或覆寫元件時，不應移除SCF指令碼中的指令碼標籤。 在HTML中自動建立用來插入JSON的SCF指令碼標籤會以屬性`data-scf-json=true`識別。

## 適用於SCF的Clientlibs {#clientlibs-for-scf}

使用[使用者端資料庫](../../help/sites-developing/clientlibs.md) (clientlibs)提供整理和最佳化使用者端上用於呈現內容的JavaScript和CSS的方法。

SCF的clientlibs遵循兩個變體的非常特定命名模式，這些模式僅在類別名稱中存在「author」時有所不同：

| Clientlib變體 | 類別屬性的模式 |
|--- |--- |
| 完成clientlib | cq.social.hbs.&lt;元件名稱> |
| 作者clientlib | cq.social.author.hbs.&lt;元件名稱> |

### 完成Clientlibs {#complete-clientlibs}

完整的（非作者） clientlib包含相依性，並可方便地包含在ui：includeClientLib中。

您可以在下列位置找到這些版本：

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

例如：

* 使用者端資料夾節點： `/etc/clientlibs/social/hbs/forum`
* 類別屬性： `cq.social.hbs.forum`

[社群元件指南](components-guide.md)列出每個SCF元件所需的完整clientlibs。

[Communities元件的Clientlibs](clientlibs.md)說明如何將clientlibs新增至頁面。

### 創作Clientlibs {#author-clientlibs}

製作版本的clientlibs會被精簡為實施元件所需的最小JavaScript。

這些clientlibs絕不應該直接包含在內，而是可以內嵌到其他為網站手動打造的clientlibs中。

這些版本可在SCF libs資料夾中找到：

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

例如：

* 使用者端資料夾節點： `/libs/social/forum/hbs/forum/clientlibs`
* 類別屬性： `cq.social.author.hbs.forum`

注意：雖然作者clientlibs從未內嵌其他程式庫，但會列出其相依性。 內嵌於其他程式庫時，相依性不會自動提取，也必須內嵌。

在[社群元件指南](components-guide.md)中每個SCF元件所列出的clientlibs中插入&quot;author&quot;，即可識別所需的作者clientlibs。

### 使用注意事項 {#usage-considerations}

每個網站管理使用者端程式庫的方式都不同。 各種因素包括：

* 整體速度：也許您想要網站有回應，但第一頁載入有點緩慢是可以接受的。 如果許多頁面使用相同的JavaScript，則各種JavaScript可以嵌入到一個clientlib中，並從要載入的第一個頁面引用。 此單一下載中的JavaScript仍會維持快取狀態，將後續頁面的資料下載量減至最少。
* 第一頁時間短：可能是希望第一頁快速載入。 在此情況下，JavaScript位於多個小型檔案中，僅於需要時參考。
* 首次頁面載入與後續下載之間的平衡。

| **[⇐ Feature Essentials](essentials.md)** | **[伺服器端自訂⇒](server-customize.md)** |
|---|---|
|   | **[SCF Handlebars協助程式⇒](handlebars-helpers.md)** |
