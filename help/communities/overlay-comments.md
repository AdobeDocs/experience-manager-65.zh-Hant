---
title: 覆蓋社區元件
seo-title: Overlay communities components
description: 覆蓋社區元件
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

# 覆蓋社區元件 {#overlay-communities-components}

意圖 [疊](/help/communities/client-customize.md#overlays) 預設元件是全局改變元件的外觀或行為，以用於元件的所有相對參照。 在/libs資料夾中進行搜索之前，它依賴sling的性質來解析到/apps資料夾。 因此，元件的路徑與預設元件的路徑相同，只是它位於/apps資料夾中，而不是/libs資料夾中。

## 範例 {#example}

**覆蓋注釋元件**

假設您希望修改注釋功能，以便它與您網站的設計相匹配，方法是更改注釋標題，使其不再顯示任何注釋的虛擬形象。 隱藏虛擬形象的解決方案或使用CSS，或如此處所述，在apps資料夾中覆蓋header.jsp，以使包含虛擬形象的HTML從不發送到客戶端。

要覆蓋注釋，您需要：

1. [「注釋」頁](/help/communities/overlay-create-comments-page.md)
1. [建立節點](/help/communities/overlay-create-nodes.md)
1. [更改外觀](/help/communities/overlay-alter-appearance.md)

**覆蓋通知電子郵件**

假設您要自定義電子郵件通知的郵件，您可以通過 [疊](/help/communities/client-customize.md#overlays) 位於 **/libs/settings/community/templates/email/html**。

例如，要修改提及的電子郵件通知（針對建立ugc的特定社區元件），請添加 **如果** 動詞條件 **提及** 在為其啟用 **@mentions** 支援。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

要修改部落格注釋中@mention的電子郵件通知模板，請將模板置於： `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
