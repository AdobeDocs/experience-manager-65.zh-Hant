---
title: 覆蓋社群元件
seo-title: Overlay communities components
description: 覆蓋社群元件
seo-description: Overlay communities components
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# 覆蓋社群元件 {#overlay-communities-components}

其意圖 [覆蓋](/help/communities/client-customize.md#overlays) 預設元件是全局更改元件的外觀或行為，以用於元件的所有相對參照。 在/libs資料夾中搜尋之前，會仰賴Sling的性質來解析至/apps資料夾。 因此，元件的路徑與預設元件的路徑相同，只是它位於/apps資料夾中，而不是/libs資料夾中。

## 範例 {#example}

**覆蓋圖註解元件**

假設您要修改留言功能，以便變更留言標題，使其符合您網站的設計，以便不再顯示任何留言的頭像。 隱藏頭像的解決方案是使用CSS，或如此處所述，在應用程式資料夾中覆蓋header.jsp，這樣包含頭像的HTML就不會傳送給用戶端。

若要覆蓋留言，您必須：

1. [「注釋」頁](/help/communities/overlay-create-comments-page.md)
1. [建立節點](/help/communities/overlay-create-nodes.md)
1. [更改外觀](/help/communities/overlay-alter-appearance.md)

**覆蓋通知電子郵件**

假設您要自訂電子郵件通知的訊息，您可以透過 [覆蓋](/help/communities/client-customize.md#overlays) 範本位於 **/libs/settings/community/templates/email/html**.

例如，若要修改提及電子郵件通知（針對建立ugc的特定社群元件），請新增 **if** 動詞條件 **提及** 在元件的範本中啟用 **@mentions** 支援。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

若要修改部落格註解中@mention的電子郵件通知範本，請放置於： `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
