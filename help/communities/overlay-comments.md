---
title: 覆蓋社群元件
seo-title: 覆蓋社群元件
description: 覆蓋社群元件
seo-description: 覆蓋社群元件
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# 覆蓋社群元件 {#overlay-communities-components}

覆蓋缺 [省元件](/help/communities/client-customize.md#overlays) （對於元件的所有相對參照）的意圖是全局更改元件的外觀或行為。 在/libs檔案夾中搜尋前，會依循sling的性質解析至/apps檔案夾。 因此，元件的路徑與預設元件的路徑相同，只不過它位於/apps檔案夾而非/libs檔案夾中。

## 例如 {#example}

**覆蓋註解元件**

假設您想要修改註解功能，以符合您網站的設計，方法是變更註解標題，以便不再顯示任何註解的頭像。 隱藏頭像的解決方案是使用CSS，或如此處所述，在apps資料夾中覆蓋header.jsp，讓包含頭像的HTML永遠不會傳送給用戶端。

若要覆蓋注釋，您必須：

1. [「注釋」頁](/help/communities/overlay-create-comments-page.md)
1. [建立節點](/help/communities/overlay-create-nodes.md)
1. [改變外觀](/help/communities/overlay-alter-appearance.md)

**覆蓋通知電子郵件**

假設您想要自訂電子郵件通知的訊息，您可以 [在](/help/communities/client-customize.md#overlays)**/libs/settings/community/templates/email/html上覆寫範本**。

例如，若要修改提及次數電子郵件通知（針對建立ugc的特定社群元件），請在您啟用@mentions支援的元件範本中，新增**條件( ****&#x200B;若為動詞提及)**** 。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

若要修改部落格注釋中@提及的電子郵件通知範本，請將範本置於： **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**
