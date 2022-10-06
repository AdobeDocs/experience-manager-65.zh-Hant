---
title: 設計與設計人員
seo-title: Designs and the Designer
description: 您需要為網站和AEM建立設計，需使用設計工具
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

# 設計與設計人員{#designs-and-the-designer}

>[!CAUTION]
>
>本文說明如何根據傳統UI建立網站。 Adobe建議您依照文章的詳細說明，將最新的AEM技術運用在您的網站 [開始開發AEM Sites](/help/sites-developing/getting-started.md).

設計工具可用來建立網站的設計，使用 [傳統UI](/help/release-notes/touch-ui-features-status.md) 在AEM中。

>[!NOTE]
>
>如需網頁協助工具的詳細資訊，請參閱 [AEM與網頁協助工具准則](/help/managing/web-accessibility.md).

## 使用設計工具 {#using-the-designer}

您的設計可在 **設計** 區段 **工具** 標籤：

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

您可以在此處建立儲存設計所需的結構，然後上傳所需的級聯樣式表和影像。

設計儲存在 `/apps/<your-project>`. 要用於網站的設計路徑是使用 `cq:designPath` 屬性 `jcr:content` 節點。

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>以設計模式在頁面上所做的所有變更都會保留在網站的設計節點下方，並自動套用至具有相同設計的所有頁面。

## 您需要的 {#what-you-will-need}

要實現您的設計，您需要：

**CSS**  — 級聯樣式表定義頁面上特定區域的格式。
**影像**  — 用於背景、按鈕等功能的任何影像。

### 設計網站時的考量事項 {#considerations-when-designing-your-website}

開發網站時，強烈建議將影像和CSS檔案儲存在 `/apps/<your-project>` 這樣，您就能根據目前的設計來參考資源，如下列程式碼片段所述。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

上例提供幾項優點：

* 元件可根據每個網站使用不同設計路徑而有不同的外觀/風格。
* 只需將設計路徑指向站點根目錄的不同節點，即可輕鬆完成網站的重新設計 `design/v1` to `design/v2.`

* `/etc/designs` 和 `/content` 是瀏覽器看到的唯一外部URL，可保護您的外部使用者，使其對您下方的內容有所好奇 `/apps` 樹。 上述URL的優點也有助於系統管理員設定更好的安全性，因為您會將資產的曝光限制在幾個不同的位置。
