---
title: We.Retail參考實作
seo-title: We.Retail參考實作
description: We.Retail是參考實作的技術預覽，說明建立線上呈現方式的建議方AEM式
seo-description: We.Retail是參考實作的技術預覽，說明建立線上呈現方式的建議方AEM式
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 8%

---

# We.Retail Reference Implementation{#we-retail-reference-implementation}

## 簡介 {#introduction}

We.Retail是參考實作和範例內容，說明與Adobe Experience Manager建立線上活動的建議方式。

We.Retail運用最新技術，例AEM如HTL、互動式版面、可編輯的範本、核心元件等。

雖然它說明零售垂直，但網站的設定方式可套用至任何垂直，而且只有產品目錄和購物車功能是零售專用的。

## 功能 {#features}

We.RetailAEM是標準的參考實作，展示其中一些最強大的功AEM能。

| **功能** | **說明** | **有興趣嗎？** |
|---|---|---|
| [全球化網站結構](/help/sites-administering/tc-bp.md) | We.Retail包含語言母版，可即時複製至國家／地區特定網站。 | [試試！](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [互動式版面](/help/sites-authoring/responsive-layout.md) | 所有頁面都具備回應式版面，可動態調整以配合螢幕和裝置大小。 | [試試！](/help/sites-developing/we-retail-responsive-layout.md) |
| [可編輯的範本](/help/sites-developing/page-templates-editable.md) | 所有頁面都以可編輯的範本為基礎，讓非開發人員可調整和自訂範本。 | [試試！](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML 範本語言](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html) | 所有元件都以HTL為基礎 |  |
| [電子商務功能](/help/commerce/cif-classic/developing/ecommerce.md) | 功能：產品目錄 |  |
| [社群網站](/help/communities/overview.md) | 允許訪客加入社群討論、閱讀部落格等 |  |
| [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) | 所有元件都以新的核心元件為基礎，而且更可用，而且可由使用者自行設定 | [試試！](/help/sites-developing/we-retail-core-components.md) |
| [內容片段](/help/assets/content-fragments/content-fragments.md) | 「We.Retail體驗」區段展示透過內容片段重複使用內容的強大功能。 | [試試！](/help/sites-developing/we-retail-content-fragments.md) |
| [體驗片段](/help/sites-authoring/experience-fragments.md) | 「體驗片段」是一組或多個元件，包括可在頁面中參考的內容和版面。 | [試試！](/help/sites-developing/we-retail-experience-fragments.md) |

## 快速入門 {#getting-started}

We.Retail以範例內容AEM形式提供。 為了使用，只需按照通常的](/help/sites-deploying/deploy.md#getting-started)AEM方式啟動[，確保未禁用示例內容。

>[!CAUTION]
>
>We.Retail不應安裝在生產實例上。 生產實例應在`nosamplecontent` [runmode](/help/sites-deploying/configure-runmodes.md)中啟動。

>[!CAUTION]
>
>We.Retail是以最新技術為基礎AEM，因此不支援[傳統UI編寫](/help/sites-classic-ui-authoring/home.md)。

### 最新版本 {#latest-version}

雖然We.Retail隨發行版本一起AEM發行，但內容及其功能的更新可能會在發行後進行。 因此，您可從GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)下載最新版本，然後[upload](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)和[以套件形式安裝&lt;a5/AEM>。[](/help/sites-administering/package-manager.md#installing-packages)

### 第一步{#first-steps}

1. 啟動AEM（和／或安裝We.Retail）後，**We.Retail**&#x200B;網站便可在[網站主控台](/help/sites-authoring/basic-handling.md#global-navigation)中使用。
1. 例如，可以開啟以下頁面，其外觀應如下面[附錄](#appendix)中所示：

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail &amp;Geometrixx{#we-retail-geometrixx}

Geometrixx及其許多化身在舊版中都是範例內AEM容。 自6.3版起，We.Retail便成為隨附的範例內容，AEM並成為新的標準參考實作。

We.Retail在技術上更健全，運用最AEM新技術，提供更靈活、更可擴充的功能，同時也展示產品的最新功能。

### 功能比較{#feature-comparison}

下表概述We.Retail與Geometrixx相比的主要功能。

* **可** 用意指在範例內容中找到功能範例。
* **不** 可用表示範例內容中不提供功能範例，但並不表示功能本身不可用。

| **功能** | **We.Retail** | **Geometrixx** |
|---|---|---|
| 全球化網站結構 | 將語言母版即時複製至國家／地區特定網站 | 不可用 |
| 內容片段 | 可用 | 不可用 |
| 體驗片段 | 可用 | 不可用 |
| 回應式版面 | 適用於所有頁面 | 僅Geometrixx Media |
| 可編輯的範本 | 適用於所有頁面 | 不可用 |
| HTL | 所有元件 | 有限 |
| 定位 | 適用於所有頁面 | 僅Geometrixx Outdoors |
| 畫面 | 可用 | 不可用 |
| 行動 | 不可用 | 可用 |
| 手稿 | 不可用 | 可用 |
| 轉盤、下載、圖表元件 | 不可用 | 可用 |
| 欄控制 | 由版面容器取代 | 可用 |
| 表單 | 不可用 | 可用 |
| 行銷活動 | 無電子郵件範例 | 可用 |

>[!NOTE]
>
>這份清單力求完整，但不應視為詳盡無遺。

## Contribute {#contribute}

We.Retail已以開放原始碼專案的形式發行，您可從GitHub下載最新版的原始碼。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-sample-we-retail專案](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* 將專案下載為[a ZIP file](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

最新版本也可以是直接下載的[可安裝的套件。](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest)

如果您遇到問題，請提交[GitHub問題](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues)。

您可以任意分叉或貢獻[pull requests](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls)。

## 預覽 {#preview}

We.Retail歡迎頁面預覽：

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
