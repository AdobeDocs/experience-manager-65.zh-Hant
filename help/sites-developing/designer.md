---
title: 設計與設計
seo-title: Designs and the Designer
description: 您需要為網站建立設計，在中AEM，使用設計器
seo-description: You will need to create a design for your website and in AEM, you do so by using the Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
source-git-commit: adbdff9ff5b5bd8f5f6b22fb724a0e5273072de2
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 設計與設計{#designs-and-the-designer}

>[!CAUTION]
>
>本文介紹如何基於經典UI建立網站。 Adobe建議利用AEM您網站的最新技術，如文章中所述 [開發AEM Sites](/help/sites-developing/getting-started.md)。

設計器用於使用 [經典UI](/help/release-notes/touch-ui-features-status.md) 的上AEM界。

>[!NOTE]
>
>有關Web輔助功能的詳細資訊，請參見 [和AEMWeb輔助功能指南](/help/managing/web-accessibility.md)。

## 使用設計器 {#using-the-designer}

可在 **設計** 的下界 **工具** 頁籤：

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

在此，您可以建立儲存設計所需的結構，然後上載所需的級聯樣式表和影像。

設計儲存在 `/apps/<your-project>`。 使用 `cq:designPath` 屬性 `jcr:content` 的下界。

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>在設計模式下對頁面所做的所有更改都保留在站點的設計節點下，並自動應用於具有相同設計的所有頁面。

## 您需要的 {#what-you-will-need}

要實現您的設計，您需要：

**CSS**  — 級聯樣式表定義頁面上特定區域的格式。
**影像**  — 用於背景、按鈕等功能的任何影像。

### 設計網站時的注意事項 {#considerations-when-designing-your-website}

在開發網站時，強烈建議將影像和CSS檔案儲存在 `/apps/<your-project>` 這樣，您就可以根據當前設計來引用您的資源，如下面的代碼段所述。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

上例提供了以下幾項好處：

* 使用不同的設計路徑，元件可以基於每個站點具有不同的外觀。
* 只需將設計路徑指向站點根部的不同節點即可完成網站的重新設計 `design/v1` 至 `design/v2.`

* `/etc/designs` 和 `/content` 是瀏覽器看到的唯一保護您的外部URL，使外部用戶對您的下面的內容產生好奇 `/apps` 樹。 上述URL的好處還有助於系統管理員設定更好的安全性，因為您將資產的暴露範圍限制在幾個不同的位置。
