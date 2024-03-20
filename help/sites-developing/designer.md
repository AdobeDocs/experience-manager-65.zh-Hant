---
title: 設計與設計工具
description: 瞭解如何使用設計工具為您的網站和AEM建立設計。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 設計與設計工具{#designs-and-the-designer}

>[!CAUTION]
>
>本文會說明如何根據傳統UI建立網站。 Adobe建議對您的網站使用最新的AEM技術，如文章中詳述 [開始開發AEM Sites](/help/sites-developing/getting-started.md).

設計工具是用來建立您網站的設計，使用 [傳統UI](/help/release-notes/touch-ui-features-status.md) 在AEM中。

>[!NOTE]
>
>如需有關網頁協助工具的詳細資訊，請參閱 [AEM與網頁協助工具准則](/help/managing/web-accessibility.md).

## 使用設計工具 {#using-the-designer}

您的設計可在以下位置定義： **設計** 的區段 **工具** 標籤：

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

您可以在此處建立儲存設計所需的結構，然後上傳所需的階層式樣式表和影像。

設計儲存在 `/apps/<your-project>`. 指定網站使用之設計的路徑，使用 `cq:designPath` 的屬性 `jcr:content` 節點。

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>在設計模式中，對頁面所做的所有變更都會保留在網站的設計節點下方，並自動套用至具有相同設計的所有頁面。

## 您將需要什麼 {#what-you-will-need}

若要實現您的設計，您需要：

**CSS**  — 階層式樣式表可定義頁面上特定區域的格式。
**影像**  — 您用於如背景、按鈕等特徵的任何影像。

### 設計網站時的注意事項 {#considerations-when-designing-your-website}

開發網站時，強烈建議將影像和CSS檔案儲存在 `/apps/<your-project>` 因此，您可以根據目前設計參考資源，如以下程式碼片段所述。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

上述範例提供數項優點：

* 使用不同設計路徑的每個網站元件可能有不同的外觀/感覺。
* 網站的重新設計只需將設計路徑指向位於網站根目錄中的不同節點即可 `design/v1` 至 `design/v2.`

* `/etc/designs` 和 `/content` 是瀏覽器看到的唯一外部URL，可保護您免受外部使用者對您下方的內容產生好奇心的侵擾 `/apps` 樹狀結構。 上述URL優點也可協助您的系統管理員設定更佳的安全性，因為您將資產的曝光限制在幾個不同的位置。
