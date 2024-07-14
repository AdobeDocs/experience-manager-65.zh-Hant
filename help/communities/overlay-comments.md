---
title: 覆蓋Communities元件
description: 瞭解如何覆蓋預設元件，以便針對元件的所有相對參照，全域變更元件的外觀或行為。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 覆蓋Communities元件 {#overlay-communities-components}

[覆蓋](/help/communities/client-customize.md#overlays)預設元件的目的是針對該元件的所有相對參照，全域變更元件的外觀或行為。 在/libs資料夾中搜尋之前，這會仰賴sling的性質解析至/apps資料夾。 因此，元件的路徑與預設元件的路徑相同，不同之處在於它位在/apps資料夾中，而非/libs資料夾中。

## 範例 {#example}

**覆蓋註解元件**

假設您想要修改註解功能，使其符合您網站的設計，方法是變更註解標題使其不再顯示任何註解的頭像。 隱藏頭像的解決方案是使用CSS，或如這裡所述，覆蓋apps資料夾中的header.jsp，因此包含頭像的HTML絕不會傳送給使用者端。

若要覆蓋註解，您必須：

1. [建立註解頁面](/help/communities/overlay-create-comments-page.md)
1. [建立節點](/help/communities/overlay-create-nodes.md)
1. [變更外觀](/help/communities/overlay-alter-appearance.md)

**覆蓋通知電子郵件**

假設您要自訂電子郵件通知的訊息，您可以透過[覆蓋](/help/communities/client-customize.md#overlays)位於`/libs/settings/community/templates/email/html`的範本來執行此操作。

例如，假設您要編輯提及電子郵件通知（針對建立UGC的特定Communities元件）。 在這種情況下，請在啟用&#x200B;**@mentions**&#x200B;支援的元件範本中，新增動詞&#x200B;**提及**&#x200B;的&#x200B;**if**&#x200B;條件。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

若要修改部落格評論中@mention的電子郵件通知範本，請將現成範本放置在： `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
