---
title: We.Retail參考實作
seo-title: We.Retail Reference Implementation
description: We.Retail是參考實作的技術預覽，說明使用AEM設定線上存在的建議方式
seo-description: We.Retail is a technology preview of a reference implementation that illustrates the recommended way of setting up an online presence with AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 8%

---

# We.Retail參考實作{#we-retail-reference-implementation}

## 簡介 {#introduction}

We.Retail是參考實作和範例內容，說明使用Adobe Experience Manager設定線上存在的建議方式。

We.Retail運用最新的AEM技術，例如HTL、回應式配置、可編輯的範本、核心元件等。

雖然它說明的是零售垂直，但網站的設定方式可套用至任何垂直，而只有產品目錄和購物車功能是零售專用的。

## 功能 {#features}

We.Retail以AEM標準參考實作形式展示AEM的一些最強大功能。

| **功能** | **說明** | **有興趣嗎？** |
|---|---|---|
| [全球化網站結構](/help/sites-administering/tc-bp.md) | We.Retail包含語言主版，這些語言主版會即時複製至特定國家/地區的網站。 | [試試！](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [回應式版面](/help/sites-authoring/responsive-layout.md) | 所有頁面都具備回應式版面，可動態調整以適應螢幕和裝置大小。 | [試試！](/help/sites-developing/we-retail-responsive-layout.md) |
| [可編輯的範本](/help/sites-developing/page-templates-editable.md) | 所有頁面都以可編輯的範本為基礎，讓非開發人員可調整和自訂範本。 | [試試！](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML 範本語言](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | 所有元件皆以HTL為基礎 |  |
| [電子商務功能](/help/commerce/cif-classic/developing/ecommerce.md) | 功能產品目錄 |  |
| [社群網站](/help/communities/overview.md) | 允許訪客加入社群討論、閱讀部落格等 |  |
| [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) | 所有元件都以新的核心元件為基礎，且更可用且可供使用者立即設定 | [試試！](/help/sites-developing/we-retail-core-components.md) |
| [內容片段](/help/assets/content-fragments/content-fragments.md) | 「We.Retail體驗」區段展示透過內容片段重複使用內容的強大功能。 | [試試！](/help/sites-developing/we-retail-content-fragments.md) |
| [體驗片段](/help/sites-authoring/experience-fragments.md) | 體驗片段是一或多個元件的群組，包括可在頁面中參照的內容和版面。 | [試試！](/help/sites-developing/we-retail-experience-fragments.md) |

## 快速入門 {#getting-started}

We.Retail以AEM範例內容的形式提供。 為了使用 [啟動AEM](/help/sites-deploying/deploy.md#getting-started)，確保未停用範例內容。

>[!CAUTION]
>
>We.Retail不應安裝在生產執行個體上。 生產執行個體應在中啟動 `nosamplecontent` [runmode](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail以最新的AEM技術為基礎，因此不支援 [傳統UI編寫](/help/sites-classic-ui-authoring/home.md).

### 最新版本 {#latest-version}

雖然We.Retail是隨AEM版本而發行，但內容及其功能可能會在發行後更新。 因此， [從GitHub下載最新版本](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) 然後 [上傳](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) 和 [安裝](/help/sites-administering/package-manager.md#installing-packages) 作為AEM例項上的套件。

### 第一步 {#first-steps}

1. AEM啟動後（和/或安裝We.Retail），網站 **We.Retail** 在 [sites console](/help/sites-authoring/basic-handling.md#global-navigation).
1. 例如，下列頁面可以開啟，其外觀應如 [附錄](#appendix) 如下：

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail與Geometrixx {#we-retail-geometrixx}

Geometrixx及其許多化身，都是舊版AEM的範例內容。 自6.3版起，We.Retail便成為透過AEM提供的範例內容，可作為新的標準參考實作。

We.Retail在技術上更穩健，利用最新的AEM技術來提高靈活性和可擴充性，同時也展示產品的最新功能。

### 功能比較 {#feature-comparison}

下表提供We.Retail與Geometrixx相比之主要功能的概觀。

* **可用** 表示在範例內容中找到功能的範例。
* **不可用** 表示範例內容中沒有此功能的範例，但並不表示此功能本身不可用。

| **功能** | **We.Retail** | **Geometrixx** |
|---|---|---|
| 全球化網站結構 | 語言主版即時複製至特定國家/地區的網站 | 不可用 |
| 內容片段 | 可用 | 不可用 |
| 體驗片段 | 可用 | 不可用 |
| 回應式版面 | 適用於所有頁面 | 僅Geometrixx Media |
| 可編輯的範本 | 適用於所有頁面 | 不可用 |
| HTL | 所有元件 | 有限 |
| 定位 | 適用於所有頁面 | 僅Geometrixx Outdoors |
| 畫面 | 可用 | 不可用 |
| 行動 | 不可用 | 可用 |
| 手稿 | 不可用 | 可用 |
| 輪播，下載，圖表元件 | 不可用 | 可用 |
| 欄控制項 | 由版面容器取代 | 可用 |
| Forms | 不可用 | 可用 |
| 行銷活動 | 沒有電子郵件範例 | 可用 |

>[!NOTE]
>
>這份清單力求完整，但不應被視為詳盡無遺。

## Contribute {#contribute}

We.Retail已發佈為開放原始碼專案，且最新版原始碼可從GitHub下載。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-sample-we-retail專案](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

最新版本也可以 [直接下載](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) 作為可安裝的套件。

如果遇到問題，請提交檔案 [GitHub問題](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

您可以自行取用或貢獻內容 [提取請求](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## 預覽 {#preview}

We.Retail歡迎頁面預覽：

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
